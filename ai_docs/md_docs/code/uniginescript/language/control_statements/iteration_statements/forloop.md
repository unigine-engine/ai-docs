# Forloop

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Since one often uses simple expressions as loop conditions, and loops often iterate over numerical sequences, there is an accelerated variant of the [*for*](../../../../../code/uniginescript/language/control_statements/iteration_statements/for.md) loop, which runs 1,5�2 times faster.


### Syntax


```cpp
forloop(initial_instruction; maximum_value; step) {
	// some_code;
}

```


### Parts


- *initial_instruction* is executed before the first loop iteration starts.
- *maximum_value* is an expression.
- *step* is an expression. *step* can be omitted, it is **1** by default.


> **Notice:** The loop counter of *forloop* must always increase, so *step* must be a positive value or you will get stuck in an infinite loop.


### Examples


- Common form: ```cpp forloop(int i = 0; 10; 2) { log.message("%d ",i); } //the output is: 0 2 4 6 8 ```
- Reduced form: ```cpp int stop = 10; forloop(int i = 0; stop) { log.message("%d ",i); } //the result is: 0 1 2 3 4 5 6 7 8 9 ```
- Another way to use *forloop*: ```cpp class Foo { int a = 10; int foo() { return a; } }; int a = 10; Foo f = new Foo(); forloop(int i = 0; f.foo() + 1) { log.message("%d ",i); } //the output is: 0 1 2 3 4 ```
