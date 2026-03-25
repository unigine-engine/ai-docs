# USC Interpreter


The stand-alone interpreter (called `USC` due to its script file extension) enables to make Unigine scripts into executable programs (USC scripts) that are run directly from the environment or from the command-line. As the USC interpreter works independently, it offers an easy way for developers to extend the functionality and solve the specific or recurring tasks for which it is not necessary to create a separate executable application.


Source code of the USC interpreter can be found under `<UnigineSDK>/source/tools/Interpreter`.


## Available Functionality


The USC interpreter provides the following functionality:


| Core library | You can use the USC interpreter for reading/writing [files](../../api/library/filesystem/class.file_cpp.md), parsing [XML](../../api/library/common/class.xml_cpp.md) files, handling [images](../../api/library/common/class.image_cpp.md), performing mathematical calculations and so on as the USC interpreter includes the core library. |
|---|---|
| Static and skinned meshes | You can load and save both the static and skinned meshes, modify or clear all their data. You can add and set transformation to mesh surfaces, add animations and bones (if you handle a skinned mesh), change position, normal vectors and texture coordinates for separate vertices and so on.  See the [*Mesh*](../../api/library/rendering/class.mesh_cpp.md) class for available functions. |
| Paths | You can load, manipulate and save paths. See the [*Path*](../../api/library/common/class.path_cpp.md) class for available functions. |
| Command line arguments | You can pass any number of arguments to the executable script via the command line and process them in this script. See examples [below](#print_cla). |
| Logging | You can print notification messages, warnings and errors to track progress of script execution, if necessary. |


The described functionality is used to [implement USC scripts](#implement).


## Command-Line Options


USC interpreter recognizes the following command-line option:

- **-define *DEFINE_NAME*** - pass an external definition (#DEFINE) to the USC interpreter. > **Notice:** You should specify this option after a USC script in the command prompt (terminal).

For example:
```bash
usc_x64.exe my_script.usc -define PRINT_MSG
```


## Implementing USC Script


To implement a USC script (written in [UnigineScript](../../code/uniginescript/index.md)) that should be run by the USC interpreter, use ***main()*** function as an entry point:

```cpp
void main() {
  // put your code here
}

```


Then you should save the script with the `*.usc` extension and [run](#run) it by the USC interpreter.


If you pass command-line arguments to the script, you should implement parsing logic for them. Otherwise, they won't affect the script behavior.

> **Notice:** You can parse any argument except [***-define***](#options). This is the standard argument which is used to pass external definition to the USC interpreter.

To access the arguments, use the following functions:
- ***int getNumArgs ()*** - returns the number of command line arguments.
- ***string getArg (int num)*** - returns a command line argument by its number.


### Parsing Passed Command-Line Arguments


The following example demonstrates how to assign values of the command-line arguments to the script variables:

```cpp
#!/usr/bin/env usc

// declare variables
int value1 = 0;
int value2 = 0;

/*
 */
void main() {
	// parse arguments
	for(int i = 0; i < getNumArgs(); i++) {
		// get the argument value
		string arg = getArg(i);

		// process all required arguments
		if(arg == "-set_value_1") {
			if(i + 1 >= getNumArgs()) {
				continue;
			}
			// assign an argument value to the variable
			value1 = int(getArg(++i));
			continue;
		}

		if(arg == "-set_value_2") {
			if(i + 1 >= getNumArgs()) {
				continue;
			}
			// assign an argument value to the variable
			value2 = int(getArg(++i));
			continue;
		}
	}

	// print the variables
	log.message("value1: %d\nvalue2: %d\n",value1,value2);
}

```

 If you pass the following to this script:
```bash
usc_x64.exe my_script.usc -set_value_1 3 -set_value_2 7
```

 The script will output:
```text
value1: 3
value2: 7

```


### Printing All Command-line Arguments


The following example demonstrates how to print all command-line arguments passed to the USC script:

```cpp
#!/usr/bin/env usc

void main() {
	forloop(int i = 0; getNumArgs()) {
		log.message("Arg [%d]: %s\n",i,getArg(i));
	}
}

```

 If you run the script with the following arguments:
```bash
usc_x64.exe my_script.usc -arg1 -arg2
```

 The `my_script.usc` script will output the following:
```text
Arg [0]: my_script.usc
Arg [1]: -arg1
Arg [2]: -arg2

```


### See Also


For more examples see the `*.usc` scripts in the following folders:

- `<UnigineSDK>/utils/Upgrade`
- `<UnigineSDK>/source/tools/Interpreter/scripts` (available only in the full source version of UNIGINE SDK)


## Running USC Script


The USC scripts are run by the USC interpreter.


### Running USC on Windows


To run a [USC script](#implement) on Windows:

1. Add a path to `<UnigineSDK>/bin/usc_*.exe` binary executable to environment variables. Depending on the postfix, it can be 64-bit debug (*d*) or release (no postfix) version of the USC interpreter. > **Notice:** You can also associate the `*.usc` file with the `<UnigineSDK>/bin/usc_*.exe` binary executable. In this case, you will run the script by double-clicking it.
2. In the command prompt, go to the folder with the `*.usc` file and run it by the USC interpreter with all required [arguments](#process_cli), for example: ```bash C:\Windows\system32>d: D:\>cd my_project\usc_scripts D:\my_project\usc_scripts>usc_x64.exe my_script.usc -define USE_DEFINE -arg1 4 ```


### Running USC on Linux


To run a [USC script](#implement) on Linux, follow the instructions:

1. In the first line of your script, specify the following: ```bash #!/usr/bin/env usc ```
2. Add a path to the `<UnigineSDK>/bin/usc_*` binary executable to environment variables. Depending on the postfix, you can use 64-bit debug (*d*) or release (no postfix) version of the USC interpreter. > **Notice:** Make sure that your terminal takes environment variables into account.
3. In the terminal, go to the folder with the `*.usc` file and run it by the USC interpreter with all required [arguments](#process_cli), for example: On Linux: ```bash username@pc-name:~$ cd my_project/usc_script username@pc-name:~/my_project/usc_script$ usc_x64 my_script.usc ```
