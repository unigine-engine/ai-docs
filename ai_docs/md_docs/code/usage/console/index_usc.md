# Working with Console (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## Calling a Console Command from Code


To call a console command from any of the scripts, you should call *[engine.console.run()](../../../api/library/engine/class.console_usc.md#run_cstr_void)*.


```cpp
// For example, to show the onscreen overlay:
engine.console.run("console_onscreen 1");

```


Console commands (regardless of whether they were typed in the console or called from code) cannot be executed in the middle of the frame. Instead, they are executed in the [beginning of the next frame](../../../code/fundamentals/execution_sequence/main_loop.md#console_executed) not to interrupt the current rendering process and physics calculations.


## Creating a Console Command


To create a custom console command, you should:


1. Implement a function that will be run on the console command call. If you want your console command to take more than one argument, you need to implement a separate function per each number of arguments.
2. Call *[engine.console.addCommand()](../../../api/library/engine/class.console_usc.md#addCommand_cstr_cstr_CommandCallback_int)* to add a new command.


In the example below, a new command takes no arguments or one argument:


```cpp
// a script function to be executed for no arguments input
void console() {
	log.message("console_command with no arguments has been called\n");
}

// a script function to be executed for 1 argument input
void console(string arg) {
	log.message("console_command with 1 argument has been called\n Argument: %s\n", arg);
}

int init() {
	// create a console command
	engine.console.addCommand("console_command","console_command description","console");

	return 1;
}

```


To check the result, run the added command:


```text
Unigine~# console_command
console_command with no arguments has been called

Unigine~# console_command arg
console_command with 1 argument has been called
Argument: arg

```


You can also remove custom console commands via *[engine.console.removeCommand()](../../../api/library/engine/class.console_usc.md#removeCommand_cstr_int)*.


## Creating a Console Variable


> **Notice:** UnigineScript API doesn't provide the ability to add console variables.


### Disabling Console


To disable console (for example, for an application production version), you need to call *[engine.console.setLock()](../../../api/library/engine/class.console_usc.md#setLock_int_void)*.


```cpp
// disable the console
engine.console.setLock(1);

```
