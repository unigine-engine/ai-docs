# Thread

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## int thread ( string function_name , variable arguments )

Places a function into the list (FIFO) for thread initialization. The functions from this list are started at the end of any script function execution, which was called from C++ (*init()*, *shutdown()*, *update()* of any script).  Target functions must use the [wait](../../../../../code/uniginescript/language/control_statements/other_statements/wait.md) statement to free the processor for other tasks. Each thread has its own scope.
### Arguments

- *string* **function_name** - Name of the function to place into the list for thread initialization.
- *variable* **arguments** - Function arguments.

### Return value

Thread ID. It can be used to terminate the thread via kill_thread().
### Examples


```cpp
void log_argument(int arg) {
	while(1) {
		log.message("Argument: %d",arg);
		wait;
	}
}

for(int i = 0; i < 10; i++) {
	thread("log_argument",i);
}

```


## int thread ( string function_name , variable array )

Places a function into the list (FIFO) for thread initialization. The number of function arguments can vary.
### Arguments

- *string* **function_name** - Name of the function to place into the list for thread initialization.
- *variable* **array** - Function arguments. The number of arguments can vary.

### Return value

Thread ID. It can be used to terminate the thread via kill_thread().
See also: [Execution Sequence](../../../../../code/fundamentals/execution_sequence/index.md).
