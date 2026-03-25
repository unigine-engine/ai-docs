# Working with Console (CPP)


To work with console commands from the code, `UnigineConsole.h` must be included:


```cpp
#include <UnigineConsole.h>

```


## Calling a Console Command from Code


To call a console command from the code, you should call the *[run()](../../../api/library/engine/class.console_cpp.md#run_cstr_void)* function.


```cpp
// For example, to show the onscreen overlay:
Console::run("console_onscreen 1");

```


Console commands (regardless of whether they were typed in the console or called from code) cannot be executed in the middle of the frame. Instead, they are executed in the [beginning of the next frame](../../../code/fundamentals/execution_sequence/main_loop.md#console_executed) not to interrupt the current rendering process and physics calculations.


## Creating a Console Command


1. Implement a callback for a console command and a method for an action performed on the console command call. Both methods should be implemented as *[AppWorldLogic](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic)* instance methods. > **Notice:** If you want the console command to take more than one argument, you need to implement a separate method per each number of arguments.
2. Get the console instance (which has a singleton implementation) and call *[addCommand()](../../../api/library/engine/class.console_cpp.md#addCommand_cstr_cstr_CommandCallback_int)* to add a new command.


In the example below, a new command takes no arguments or one argument. For this, three methods are declared in the *AppWorldLogic.h* header file:


- *choose_command()* calls the appropriate method for the console command.
- *action_no_args()* is called if there are no arguments.
- *action_one_arg()* is called if one argument has been passed.


```cpp
// AppWorldLogic.h

#ifndef __APP_WORLD_LOGIC_H__
#define __APP_WORLD_LOGIC_H__

#include <UnigineLogic.h>
#include <UnigineStreams.h>

class AppWorldLogic : public Unigine::WorldLogic {

	public:
		AppWorldLogic();
		virtual ~AppWorldLogic();

		virtual int init();

		virtual int update();
		virtual int postUpdate();
		virtual int updatePhysics();

		virtual int shutdown();

		virtual int save(const Unigine::StreamPtr &stream);
		virtual int restore(const Unigine::StreamPtr &stream);

	private:
		// chooses the method to run on the console command call
		void choose_command(int argc, char **argv);
		// performs an action if there are no arguments
		void action_no_args();
		// performs another action if an argument was passed
		void action_one_arg(const char *s);
};

#endif // __APP_WORLD_LOGIC_H__

```


*AppWorldLogic.cpp* contains implementation of the declared methods:


```cpp
// AppWorldLogic.cpp

#include <UnigineConsole.h>
#include <UnigineCallback.h>

using namespace Unigine;

// check the number of arguments and call the corresponding method
void AppWorldLogic::choose_command(int argc, char **argv) {
	// print all console command arguments
	// note: the first element of argv is the name of console command
	for (int i = 1; i < argc; i++) {
		Unigine::Log::message("arg[%d]: %s\n", i, argv[i]);
	}
	// if no arguments is specified
	if (argc == 1) {
		action_no_args();
	}
	// if one argument is specified
	else if (argc == 2) {
		action_one_arg(argv[1]);
	}
	// for more arguments:
	//else if (...) {
	//	// etc
	//}
}

// print the message into console, if there are no arguments
void AppWorldLogic::action_no_args() {
	Unigine::Log::message("first action! no arguments!\n");
}
// print the message into console, if one argument has been passed
void AppWorldLogic::action_one_arg(const char *arg) {
	Unigine::Log::message("second action! the argument is: %s \n", arg);
}

// application initialization
int AppWorldLogic::init() {
	// get the existing singleton Console instance and add a new console command
	Unigine::Console::addCommand("console_command", "Performs custom console action", Unigine::MakeCallback(this, &AppWorldLogic::choose_command));

	return 1;
}

```


Arguments ***argc*** and ***argv*** are used to get the arguments count and arguments vector.


> **Notice:** The first element of ***argv*** always keeps the name of a console command. Thus, ***argc*** is always >= 1. To get the first passed argument, you should use argv[1].


To check the result, run the added command:


```text
Unigine~# console_command
first action! no arguments!

Unigine~# console_command arg
arg[1]: arg
second action! the argument is: arg

```


## Creating a Console Variable


To create a custom console variable, you should declare it as an instance of *[ConsoleVariableInt](../../../api/library/common/class.consolevariableint_cpp.md#ConsoleVariableInt_constcharm_constcharm_int_int_int_int), [ConsoleVariableFloat](../../../api/library/common/class.consolevariablefloat_cpp.md#ConsoleVariableFloat_constcharm_constcharm_int_float_float_float)* or *[ConsoleVariableString](../../../api/library/common/class.consolevariablestring_cpp.md#ConsoleVariableString_constcharm_constcharm_int_constcharm)* class depending on the variable type.


```cpp
// define console variables of different types
ConsoleVariableInt my_console_variable_int("my_console_variable_int", "my_console_variable_int", 1, 0, 0, 1000);
ConsoleVariableFloat my_console_variable_float("my_console_variable_float", "my_console_variable_float", 1, 0.0f, 0.0f, 1.0f);
ConsoleVariableString my_console_variable_string("my_console_variable_string", "my_console_variable_string", 1, NULL);

int AppWorldLogic::init() {

	// set console variable values
	my_console_variable_int = 13;
	my_console_variable_float = 0.13f;
	my_console_variable_string = "String variable";

	return 1;
}

```


If you run, for example, the `my_console_variable_int` command, the following will be shown in the console:


```text
Unigine~# my_console_variable_int
my_console_variable_int
my_console_variable_int = 13

```


You can also set a new value for the variable:


```text
Unigine~# my_console_variable_int 24

```


### Disabling Console


To disable console (for example, for an application production version), you need to call *[setLock()](../../../api/library/engine/class.console_cpp.md#setLock_int_void)*.


```cpp
// disable the console
Console::setLock(1);

```
