# Structure of a Program

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Like any other computer program, Unigine script program is a sequence of instructions that tell the computer what to do. Lets take a quick look at the basic components of the UnigineScript program.


## Statements and Expressions


The most common type of instructions in a program is the **statement**. A statement in UnigineScript is the smallest independent unit in the language. We write statements in order to convey to the interpreter that we want to perform a task. Statements in UnigineScript are terminated by a semicolon.


The most common types of simple statements:


```cpp
int x;
```


*int x* is a **declaration statement**. It tells the interpreter that *x* is a [variable](#variables). All variables in a program must be declared before they are used.


```cpp
x = 5;
```


*x = 5* is an **assignment statement**. It assigns a value (5) to a variable (x).


The interpreter is also capable of resolving expressions. An **expression** is a mathematical entity that evaluates to a value. Expressions can involve values (such as *2*), variables (such as *x*), operators (such as *+*) and functions. They can be singular (such as *2*, or *x*), or compound (such as *2 + 3*, *2 + x*, *x + y*, or *(2 + x)*(y - 3)*).


```cpp
x = 2 + 3;
```


*x = 2 + 3* is a valid assignment statement. The expression *2+3* evaluates to the value of *5*. This value of *5* is then assigned to *x*.


## Variables


A **variable** is the name for a place in the computer's memory where you store some data. To be distinguished from others each variable needs an **identifier** (a sequence of characters used to name the variable, type, class, function etc.) In UnigineScript variables are declared to be of a **type** (however, the language uses [dynamic typing](../../../code/uniginescript/language/features.md#dynamic_typing) in fact).


Here is an example of a variable declaration.


```cpp
int x; // x - identifier, int - type
```


> **Notice:** All the variables in UnigineScript are **static** by default.


For example:

```cpp
int foo() {
	int i;
	return i++;
}

log.message("%d\n",foo());

// the output is: 0,1,2,3...

```


You can also specify a reference variable if you want to allow your function to modify passed values:

```cpp
void foo(int &v) {
	if(v) log.message("%d\n",v);
	v = 13;
}

int v = 0;
foo(v);
foo(v);

// the output is: 13

```


## Comments


UnigineScript supports both single- and multi-line comments. Comments are ignored during code execution.

1. Single-line comments. Everything starting from *//* to the end of a line is a comment: ```cpp // single-line comment int x; // one more comment ```
2. Everything between */** and **/* is a multi-line comment: ```cpp /* multi-line comment: * comment line * one more line */ int foo() { return 0; } ```


## Functions


In UnigineScript, statements are typically grouped into units called functions. A **function** is a collection of statements that executes sequentially. Read [more](../../../code/uniginescript/language/functions.md) information about functions.


## Libraries


**Libraries** are groups of functions that have been �packaged up� for reuse in many different programs. The core UnigineScript language is actually very small and minimalistic � however, UnigineScript comes with a bunch of [libraries](../../../api/index.md), that provide programmers with lots of extra functionality. To include the library in your program use [Preprocessor Directives](../../../code/uniginescript/language/preprocessor.md).
