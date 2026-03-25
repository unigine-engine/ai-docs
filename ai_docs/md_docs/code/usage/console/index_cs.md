# Working with Console (CS)


## Calling a Console Command from Code


To call a console command from the code, you should call the *[run()](../../../api/library/engine/class.console_cs.md#run_cstr_void)* function.


```csharp
// For example, to show the onscreen overlay:
Console.Run("console_onscreen 1");

```


Console commands (regardless of whether they were typed in the console or called from code) cannot be executed in the middle of the frame. Instead, they are executed in the [beginning of the next frame](../../../code/fundamentals/execution_sequence/main_loop.md#console_executed) not to interrupt the current rendering process and physics calculations.


## Creating a Console Command


1. Implement a callback for a console command and a method for an action performed on the console command call. Both methods should be implemented as *[AppWorldLogic](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic)* instance methods. > **Notice:** If you want the console command to take more than one argument, you need to implement a separate method per each number of arguments.
2. Get the console instance (which has a singleton implementation) and call *[addCommand()](../../../api/library/engine/class.console_cs.md#addCommand_cstr_cstr_CommandCallback_int)* to add a new command.


In the example below, a new command takes no arguments or one argument. For this, three methods are implemented in the *AppWorldLogic.cs* file:


- *choose_command()* calls the appropriate method for the console command.
- *action_no_args()* is called if there are no arguments.
- *action_one_arg()* is called if one argument has been passed.


```csharp
// AppWorldLogic.cs

public static void choose_command(int argc, string[] argv)
{
	// print all console command arguments
	// note: the first element of argv is the name of console command
	for (int i = 1; i < argc; i++) {
		Log.Message("arg[{0}]: {1}\n", i, argv[i]);
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
public static void action_no_args()
{
	Log.Message("first action! no arguments!\n");
}

// print the message into console, if an argument was passed
public static void action_one_arg(string s)
{
	Log.Message("second action! the argument is:{0} \n", s);
}

 public override bool Init()
{
	// get the existing singleton Console instance and add a command
	Console.AddCommand("console_command", "Performs custom console action", choose_command);

	return true;
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


> **Notice:** C# API doesn't provide the ability to add console variables.


### Disabling Console


To disable console (for example, for an application production version), you need to call *[setLock()](../../../api/library/engine/class.console_cs.md#setLock_int_void)*.


```csharp
// disable the console
Console.Lock = 1;

```


## See Also


- The [video tutorial](https://youtu.be/6MUeatvw9v0) demonstrating how to print user messages to console using C# Component System
