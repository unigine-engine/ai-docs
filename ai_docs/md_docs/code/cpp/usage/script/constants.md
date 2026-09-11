# Constant Export

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Constants are variables, the value of which does not change no matter what happens in C++ code. To be available in Unigine scripts, they need to be exported on C++ side.


- External constants are **read-only**.
- If a value of a registered constant is changed in the C++ code, on script side it will remain the **same** (unlike [variables](../../../../code/cpp/usage/script/variables.md)).


## Constant Export Example


Constants are exported in the similar way as [variables](../../../../code/cpp/usage/script/variables.md):


1. Create a pointer to an external constant via `MakeExternConstant()`.
2. Register the constant via `Unigine::Interpreter::addExternVariable()`.
3. All variables are exported into a global namespace. To limit the scope of variable, use [library namespace](../../../../code/cpp/usage/script/namespace.md).


```cpp
#include <UnigineEngine.h>
#include <UnigineInterpreter.h>

using namespace Unigine;

int main(int argc,char **argv) {

	int i = 0;
	float f = 0.0f;

	// export a variable and specify a name to access it from Unigine scripts
	Interpreter::addExternVariable("int_constant",MakeExternConstant(i));
	// you can also specify a template parameter to make sure the proper type is passed
	Interpreter::addExternVariable("float_constant",MakeExternConstant<float>(f));

	Engine *engine = Engine::init(argc,argv);
	// enter the main loop
	while(engine->isDone() == 0) {
		engine->update();
		engine->render();
		engine->swap();
		// if a variable value is changed after it was registered, the value in scripts will not be changed
		i = 42;
		f = 57.55f;
	}
	// engine shutdown
	Engine::shutdown();

}

```


### Access from Scripts


After the registration, you can access constants from a script by their registered names:


```cpp
// my_world.usc

log.message("Integer: %d\nFloat: %f\n",int_constant,float_constant);

```


### Output


The following results will be printed into the console:


```text
Integer: 0
Float: 0.000000

```


> **Notice:** If you reload the world, the values of the constants that have been changed on the C++ side will remain the same.
