# Script Debugging

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The Unigine Debugger allows you to inspect your UnigineScript code at run-time. For example, it can help you to determine when a function is called and with which values. Furthermore, you can locate bugs or logic problems in your scripts by executing them step by step.


An additional information from the scripting system of Unigine is obtained if you use *debug builds*.


The engine may cause the errors of two types: compile-time and run-time.


## Compile-Time Errors


### Error Message


When a compile-time error occurs, it means that the interpreter could not parse and load the script. In this case, the log file will contain an error message with:

1. A source code string with an invalid statement.
2. An error description from the interpreter.


Mismatched curly braces are the most frequent compile-time error. For example:

```cpp
class Foo {
	Foo(int a) {
		this.a = a;
	// missing closing curly brace
	~Foo() {}

	void print() {
		log.message("a is %d\n",a);
	}
};

```


```text
Parser::check_braces(): some errors with count of '{' and '}' symbols
Parser::preprocessor(): wrong number of braces

```


### Unigine-Specific Warnings


Among the obvious errors like incorrect [syntax](../../../code/uniginescript/language/index.md), there are some not so evident and more confusing. The most important are:

- Recursive [includes](../../../code/uniginescript/language/preprocessor.md#include) are not tracked, so be careful with file inclusions and use [defines](../../../code/uniginescript/language/preprocessor.md#define) when in doubt.
- In [user class definitions](../../../code/uniginescript/language/oop.md#classes) make sure that all member variables are declared before they are used in a constructor or a method. ```cpp class Foo { Foo(int a) { this.a = a; } ~Foo() {} void print() { log.message("a is %d\n",a); } }; ``` Variable *a* is not declared, so an error occurs: ```text Interpreter::parse(): unknown "Foo" class member "a" ```
- The following and alike complex expressions lead to errors: ```cpp object.doSomething().doSomethingElse(); object.doSomething()[4]; ``` For the first expression, the following error message occurs: ```text Parser::expectSymbol(): bad '.' symbol expecting end of string ``` For the second expression, the error message is: ```text Parser::expectSymbol(): bad '[' symbol expecting end of string ``` The point is that due to a dynamic typing the interpreter does not know what will be returned by *object.doSomething()*, maybe, even nothing, and that may lead to a run-time error.


## Run-Time Errors


### Error Message


When a run-time error occurs, it usually means that you are trying to manipulate a corrupt or even a non-existent object. In this case, the log file will contain an error message with:

1. An error description from the interpreter.
2. Current stack of function calls.
3. An assembly dump of an invalid statement.

For example:
```text
Interpreter::run(): "int: 0" is not an extern class
Call stack:
00: 0x0001a84c update()
01: 0x00016565 nodesUpdate()
02: 0x0001612c Nodes::update()
Disassemble:
0x00016134: callecf  Node.getName
0x00016137: pop
0x00016138: pushv    parameters_tb
0x0001613a: callecf  WidgetTabBox.getCurrentTab

```


> **Notice:** You can debug run-time errors with a console [debugger](#debugger).


### Common Errors


Common run-time errors:

- NULL objects. Please, don't forget to initialize declared objects and check the values returned from functions.
- Stack underflow (or overflow) when less (or more) arguments than required are provided to a function.
- Dynamic typing allows assigning a value of one type to a variable of another, for example: ```cpp // the following is ok Object object = new ObjectMesh("file.mesh"); object = new LightWorld(vec4_one); ``` However, people tend to forget what they've assigned to a variable and call inappropriate methods: ```cpp // the following is NOT ok, as object is not of type ObjectMesh any more Material m = object.getMaterial(0); ``` In this case, the error message is: ```text ExternClass::run_function(): can't find "class Object * __ptr64" base class in "class LightWorld * __ptr64" class ```
- When creating a [vector](../../../code/uniginescript/language/containers/index.md#vector), make sure you provide a correct capacity (non-negative). If the negative capacity is specified, a vector size is set to 0 by default. Also, when addressing vector contents, make sure an index being used exists; the same is true for [maps](../../../code/uniginescript/language/containers/index.md#maps) and their keys. Also, a map key cannot be NULL. ```cpp int vector[2] =	( 1, 2, 3 );	// vector of 3 elements is defined log.message("%d\n", vector[4]);	// addressing the 4th component, which doesn't exist ``` In this case, the error message is: ```text UserArray::get(): bad array index 4 ```
- Make sure you use correct [swizzles](../../../code/uniginescript/language/data_types.md#swizzling) with proper objects. For example, you cannot use swizzles with [scalar types](../../../code/uniginescript/language/data_types.md#fundata). ```cpp int a = 10;	// value of the scalar type log.message("%d\n", a.x); // swizzling ``` The exapmle produces the following error message: ```text Variable::getSwizzle(): bad component 0 for int variable ```
- If a user class overloads some operator, do not forget to preserve the order of operands in the code: ```cpp class Foo { int f; Foo(int f = 0) { this.f = f; } int operator+(Foo arg1,int arg2) { return arg1.f + arg2; } }; // this is ok int ret = new Foo() + 5; // this is NOT ok ret = 5 + new Foo(); ``` The example produces an error: ```text Variable::add(): bad operands int and user class ```
- Make sure that if you use *[wait](../../../code/uniginescript/language/control_statements/other_statements/wait.md)* control structure in the class method, this class method is called as a static one. ```cpp class Foo { void update() { while(true) wait 1; } }; Foo f = new Foo(); Foo::update();		// this is valid, because the method is called as a static function f.update();		// this would cause a crash, because a class instance is passed ``` The error message is: ```text Interpreter::runFunction(): depth of stack is not zero ```
- Use *class_cast()* with caution. Remember that it converts an instance of one user class to another without warnings, even if those classes have nothing in common.
- Lots of transient objects. This is not exactly an error, but if you create in a short period plenty of user class objects that soon become unused, the performance will drop every 32 frames because of garbage collector clean-ups, until all unused objects are gone. In this case, the performance drop will be caused by both a multitude of objects and expensive object destruction.


## Debugger


The Unigine debugger allows you to:

- Set the breakpoints directly in the script
- Set and remove the breakpoints via the console
- View memory stack
- View function call stack
- View current variables values
- Step through instructions


To run the debug process, you can insert the [breakpoint;](#debugger_breakpoint) instruction in your code or set the [run-time breakpoint](#debugger_runtime).

> **Notice:** Note that the debugger opens in the main (external) console, which is available only in the debug builds.


The console debugger window (in Windows):


![](script_debugger.jpg)


### Set a Breakpoint


To invoke the console debugger, insert a breakpoint; instruction in the script you are working on. This type of instructions used for the precise breakpoints placing. You can insert more than one breakpoint; instruction in your script.


For example:

```cpp
int a = 10;
breakpoint;	// the breakpoint instruction
int b = 1;
forloop(int i = 0; a){
	b += i;
	log.message("Iteration: %d\n",i);
	log.message("Value: %d\n",b);
}

```


When a breakpoint is encountered, the engine execution stops, and the application stops responding to user actions. Instead, the external console starts receiving user input.


In this console, you can step through instructions using the [next](#cmd_next) command. Also it is possible to set the breakpoint during the debug process by using the [break](#cmd_break) command. It is useful, for example, when you debug a loop. Or you can run the other [debugger commands](#debugger_commands), if necessary.


If the console is unavailable, as in Windows release builds, this will seem as a hang-up of the engine. To avoid that, use a "breakpoint" macro defined in the file `data/core/unigine.h`. This macro also correctly preserves FPS values.


### Set a Run-Time Breakpoint


There is also a way to set a run-time per-function interpreter breakpoints with the specified number of arguments via the editor [console](../../../code/console/index.md). A required script instruction is triggered for breakpoint, so the engine execution stops and the external console starts to receive the user input. Moreover, it is also possible to set the breakpoint flag inside the debugger.


There are 3 types of such breakpoints: system_breakpoint, world_breakpoint and editor_breakpoint, used for [system, world, and editor scripts](../../../code/fundamentals/execution_sequence/app_logic_system.md#scripts) respectively.


> **Notice:** This type of breakpoints does not require the script recompilation.


The syntax to set the breakpoint is the following: `system_breakpoint/world_breakpoint/editor_breakpoint set/remove function_name number_of_arguments`.


For example, to set the breakpoint on the custom function with zero arguments *printMyMessage()*, type in the editor [console](../../../code/console/index.md) the following:

```text
world_breakpoint set printMyMessage 0
```

 When the breakpoint is encountered, the console debugger is invoked, and you can run [debugger commands](#debugger_commands).
> **Notice:** The last parameter `number_of_arguments` is optional.


### Features


The debugger also supports limited autocompletion and history of commands.


With the debugger, you *cannot*:

- Call functions.
- Evaluate arbitrary expressions.
- Retrieve [map](../../../code/uniginescript/language/containers/index.md#maps) values by arbitrary keys. Only [*int*](../../../code/uniginescript/language/data_types.md#int), [*float*](../../../code/uniginescript/language/data_types.md#float),and [*string*](../../../code/uniginescript/language/data_types.md#string) keys are supported.


### Commands


The debugger supports several console commands listed below.


#### help


Lists all available commands.


| Short form | Long form |
|---|---|
| *h* | *help* |


#### run


Continues interpreter execution until the next breakpoint or the end of the script is reached.


| Short form | Long form |
|---|---|
| *r [N]* | *run [N]* |


Here *N* is an optional argument specifying the number of breakpoints to skip. By default, *N* equals to **0**.


#### next


Executes the next instruction. This command is used to step through instructions starting from the breakpoint.


| Short form | Long form |
|---|---|
| *n [N]* | *next [N]* |


Here *N* is an optional argument specifying the number of instructions to skip. By default, *N* equals to **0**.


For example, you debug the following code:

```cpp
breakpoint;	// here the breakpoint is set
int a = 10;
int b = 1;
int vector [3] = ( 1, 2, 3, 4);
forloop(int i = 0; a){
	b += i;
	log.message("Iteration: %d\n",i);
	log.message("Value: %d\n",b);
}

```

  To execute the next instruction after the breakpoint, type the next command:
```text
Breakpoint at 0x00000455: setvc a = int: 10
# next
Breakpoint at 0x00000458: setvc b = int: 1

```


#### stack


Dumps the memory stack.


| Short form | Long form |
|---|---|
| *s* | *stack* |


#### calls


Dumps the function call stack.


| Short form | Long form |
|---|---|
| *c* | *calls* |


Some notes:

- Function calls are listed starting from a C++ function call, which is not included in the stack. For example, if some script function is invoked as a callback, you will not see the invoking C++ function.
- If a function address is intact, a function name will be displayed, otherwise, you will see gibberish instead of the name. The address changes, if there are [*yield*](../../../code/uniginescript/language/control_statements/other_statements/yield.md) or [*wait*](../../../code/uniginescript/language/control_statements/other_statements/wait.md) instructions in the function body.


#### dasm


Disassembles a certain number of instructions starting from the current instruction.


| Short form | Long form |
|---|---|
| *d [N]* | *dasm [N]* |


Here *N* is an optional argument specifying the number of instructions to process. By default, *N* equals to **8**.


For example:

```text
# dasm
Disassemble:
0x00000465: addvv	b i
0x00000468: popv	b
0x0000046a: pushv	i
0x0000046c: pushc	string: "Iteration: %d\n"
0x0000046e: callefr	log.message
0x00000470: pushv	b
0x00000472: pushc	string: "Value: %d\n"
0x00000474: callefr	log.message

```


See also: [Assembly Mnemonics](#run_mnemonics).


#### info


Displays contents of given variables.


| Short form | Long form |
|---|---|
| *i var_list* | *info var_list* |


Here *var_list* is a list of space-separated variable names. If a variable is not local to the current [scope](../../../code/uniginescript/language/scope.md#scope), its name should contain a namespace prefix.


Some notes:

- Both ordinary and [array](../../../code/uniginescript/language/containers/index.md) variables are supported
- Values of map and vector elements can be accessed via constant keys/indices in brackets (**[]**). Only *int*, *float*, and *string* keys are supported
- User class members can be accessed via a dot (**.**). Autocompletion of user class members is not supported


Usage example:

```text
# info a b vector
a: int: 3
b: int: 1
vector: Vector of 4 elements
0: int: 1
1: int: 2
2: int: 3
3: int: 4
# info vector[1]
vector[1]: int: 2

```


This command is useful, when you want to check, for example, which instruction changes variable values.


See also: [list](#cmd_list).


#### list


Displays all variables in the current scope.


| Short form | Long form |
|---|---|
| *l* | *list* |


See also: [info](#cmd_info).


#### fault


Crashes interpreter. Useful when the enigne itself is run in a debugger (for example, `gdb`), as it allows seeing the stack of C++ function calls.


| Short form | Long form |
|---|---|
| *f* | *fault* |


#### break


Toggles the current breakpoint. You can add or remove the breakpoint for each script instruction during the debug process.


| Short form | Long form |
|---|---|
| *b* | *break* |


For example, you debug the following code:

```cpp
int a = 10;
int b = 1;
forloop(int i = 0; a){
	b += i;
	log.message("Iteration: %d\n",i);
	log.message("Value: %d\n",b);
}

```

 To add a breakpoint during the debug process, type `b` or `break` in the debugger:
```text
Breakpoint at 0x00000455: setvc a = int: 10
# next
Breakpoint at 0x00000458: setvc b = int: 1
# break

```

 If you disassemble instructions, the instruction with the new breakpoint is marked with `!`:
```text
Disassemble:
0x00000458: ! setvc	b = int: 1
0x00000468:	  setvc	i = int: 0

```

 To remove the breakpoint, type `break` or `b` again:
```text
Breakpoint at 0x00000455: setvc a = int: 10
# next
Breakpoint at 0x00000458: setvc b = int: 1
# break
# break

```


> **Notice:** By using this command, you cannot remove the breakpoint (breakpoint; instruction) you set in the script.


### Assembly Mnemonics


Here is a list of assembly mnemonics for the assembly dump.


| Mnemonic | Operation |
|---|---|
| NOP | No operation |


Set operations:


| Mnemonic | Operation |
|---|---|
| SETX | Set temporary register X |
| SET - *Set variable by:* For example, the SETVC mnemonic in the assembly dump: ```text 0x00000458: setvc b = int: 1 ``` |  |
| V | Stack |
| VV | Variable |
| VC | Constant |
| VEV | Extern variable |
| UAV | User array variable |
| UAVV | User array variable by variable |
| UAVC | User array variable by constant |
| SET - *Set user array variable by:* |  |
| UAVCV | Variable |
| UAVCC | Constant |


Pop operations:


| Mnemonic | Operation |
|---|---|
| POP | Pop stack |
| POP - *Pop:* For example, the POPV mnemonic in the assembly dump: ```text 0x00000468: popv	b ``` |  |
| Y | Temporary register X |
| Z | Temporary register Z |
| V | Variable |
| VV | Variable by variable |
| VE | Variable element |
| VS | Variable swizzle |
| UAID | User array ID |
| UAV | User array variable |
| UAVV | User array variable by variable |
| UAVC | User array variable by constant |
| UAVS | User array variable swizzle |
| UAVE | User array variable element |
| UC | User class |
| UCX | Pop user class and save stack |
| UCR | Pop user class and stack remove |


Push operations:


| Mnemonic | Operation |
|---|---|
| PUSH - *Push:* For example, the PUSHC mnemonic in the assembly dump: ```text 0x0000046c: pushc	string: "Iteration: %d\n" ``` |  |
| X | Temporary register X |
| Y | Temporary register X |
| Z | Temporary register Z |
| C | Constant |
| CC | Two constants |
| V | Variable |
| VV | Variable by variable |
| VE | Variable element |
| VS | Variable swizzle |
| EV | Extern variable |
| EVE | Extern variable element |
| EVS | Extern variable swizzle |
| UAID | User array ID |
| UAV | User array variable |
| UAVV | User array variable by variable |
| UAVC | User array variable by constant |
| UAVS | User array variable swizzle |
| UAVE | User array variable element |
| UC | User class |
| UCV | User class variable |
| UCVE | User class variable element |
| UCVS | User class variable swizzle |
| UCAV | User class array variable |
| UCC | User class current object |


Call operations:


| Mnemonic | Operation |
|---|---|
| CALL | Call address |
| CALL - *Call:* For example, the CALLEFR mnemonic in the assembly dump: ```text 0x0000046e: callefr	log.message ``` |  |
| F | Function |
| FD | Function dynamic |
| FT | Function thread |
| EF | Extern function |
| EFR | Extern stack remove function |
| UAC | User array constructor |
| UAF | User array function |
| UAFR | User array stack remove function |
| UCC | User class constructor |
| UCF | User class function |
| UCFV | User class virtual function |
| UCFVC | User class virtual current function |
| ECC | External class constructor |
| ECF | External class function address |
| ECFR | External class stack remove function |
| CCD | Class dynamic constructor |
| CFD | Class dynamic function |
| CD | Class destructor |


Math operations:


| Mnemonic | Operation |
|---|---|
| INV | Inverse |
| ONE | One's complement |
| NEG | Negate |
|  |  |
| INC | Increment |
| DEC | Decrement |
| INCV | Variable increment |
| DECV | Variable decrement |
|  |  |
| MUL | Multiplication |
| DIV | Division |
| MOD | Modulus |
| ADD | Addition |
| SUB | Subtraction |
| MUL - *Multiplication by:* For example, the MULVC mnemonic in the assembly dump: ```text 0x0000044c: mulvc	a int: 1 ``` DIV - *Division by:* For example, the DIVVC mnemonic in the assembly dump: ```text 0x0000044c: mulvc	a int: 2 ``` MOD - *Modulus by:* ADD - *Addition by:* SUB - *Subtraction by:* |  |
| V | Variable |
| C | Constant |
| VV | Variable by variable |
| VC | Variable by constant |
| CV | Constant by variable |
|  |  |
| SHL | Shift left |
| SHR | Shift right |
| SHL - *Shift left by:* SHR - *Shift right by:* For example, the SHLC mnemonic in the assembly dump: ```text 0x0000046b: shlc	int: 1 ``` |  |
| V | Variable |
| C | Constant |
|  |  |
| BAND | Bit and |
| BXOR | Bit xor |
| BOR | Bit or |
| BAND - *Bit and by:* BXOR - *Bit xor by:* BOR - *Bit or by:* For example, the BORVV mnemonic in the assembly dump: ```text 0x00000462: borvv	a b ``` |  |
| V | Variable |
| C | Constant |
| VV | Variable by variable |
| VC | Variable by constant |
|  |  |
| EQ | Equal |
| NE | Not equal |
| LE | Less than or equal |
| GE | Greater than or equal |
| LT | Less than |
| GT | Greater than |
| EQ - *Equal:* NE - *Not equal:* LE - *Less or equal:* For example, the LEV mnemonic in the assembly dump: ```text 0x00000461: lev	b ``` GE - *Greater or equal:* LT - *Less than:* GT - *Greater than:* |  |
| V | Variable |
| C | Constant |


Branch operations:


| Mnemonic | Operation |
|---|---|
| JMP | Jump to address |
| JZ | Jump if zero |
| JNZ | Jump if not zero |
| JEQ - *Jump if equal to:* JNE - *Jump if not equal to:* For example, the JNEVV mnemonic in the assembly dump: ```text 0x00000456: jnevv	a b 0x0000045f ``` JLE - *Jump if less or equal to:* JGE - *Jump if greater or equal to:* JLT - *Jump if less than to:* JGT - *Jump if greater than to:* |  |
| V | Variable |
| C | Constant |
| VV | Variable by variable |
| VC | Variable by constant |
|  |  |
| GOTOD | Go to label by name |
| YIELD | Yield return |
| WAIT | Wait return |
| RET | Return |
| RETZ | Return zero |
| RETC | Return constant |
|  |  |
| SWITCH | Switch |


Loops:


| Mnemonic | Operation |
|---|---|
| FORLOOP | For loop |
| FOREINIT | Foreach loop initialization |
| FORESTEP | Foreach loop step |
| FOREKINIT | Foreachkey loop initialization |
| FOREKSTEP | Foreachkey loop step |
