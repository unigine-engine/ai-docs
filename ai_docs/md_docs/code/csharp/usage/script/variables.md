# Variable Export

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


To use variables from your C# code in UnigineScript, you need to export them. After that, they will be available on the script side.


- External variables are **read-only**.


### See also


An example can be found in `<UnigineSDK>/source/csharp/samples/Api/Scripts/Variables/` directory.


## Variable Export Example


Let's say, you declared a number of variables on C# side. To export them, you will need to do the following:


1. Register the variable via *Unigine.Interpreter.addExternVariable()* (the same as the C++ API *[Unigine::Interpreter::addExternVariable()](../../../../api/library/common/class.interpreter_cpp.md#addExternVariable_const_char_ptr_ExternVariableBase_ptr_int_void)* function.


```csharp
using System;
using Unigine;

class UnigineApp {

	/*
	 */
	[STAThread]
	static void Main(string[] args) {

		// export a variable and specify a name to access it from Unigine scripts
		Interpreter.AddExternVariable("my_variable_int",13);
		Interpreter.AddExternVariable("my_variable_float",13.17f);
		Interpreter.AddExternVariable("my_variable_double",13.17);
		Interpreter.AddExternVariable("my_variable_string","13.17s");
		Interpreter.AddExternVariable("my_variable_vec3",new Variable(new vec3(13.0f,17.0f,137.0f)));
		Interpreter.AddExternVariable("my_variable_vec4",new Variable(new vec4(13.0f,17.0f,137.0f,173.0f)));

		// init engine
		Engine engine = Engine.Init(Engine.VERSION,args);

		// enter main loop
		engine.Main();

		// shutdown engine
		Engine.Shutdown();
	}
}

```


### Access from Scripts


After the registration, you can access variables from a script by their registered names:


```cpp
// variables.cpp

int init() {

	log.message("\n");

	log.warning("int:      %s\n",typeinfo(my_variable_int));
	log.warning("float:    %s\n",typeinfo(my_variable_float));
	log.warning("double:   %s\n",typeinfo(my_variable_double));
	log.warning("string:   %s\n",typeinfo(my_variable_string));
	log.warning("variable: %s\n",typeinfo(my_variable_vec3));
	log.warning("variable: %s\n",typeinfo(my_variable_vec4));

	// show console
	engine.console.setActivity(1);

	return 1;
}

```


### Output


The following results will be printed into the console after launching the application:


```text
int:		int: 13
float:		float: 13.17
double:		double: 13.17
string:		string: "13.17s"
variable: 	vec3: 13 17 137
variable: 	vec4: 13 17 137 173

```
