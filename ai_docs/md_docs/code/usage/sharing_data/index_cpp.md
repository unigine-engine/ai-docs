# Sharing Data between the Logic System Components (CPP)


Sometimes it is necessary to share data between the elements of the [Logic System](../../../code/fundamentals/execution_sequence/app_logic_system.md): *[WorldLogic](../../../api/library/common/logic/class.worldlogic_cpp.md), [SystemLogic](../../../api/library/common/logic/class.systemlogic_cpp.md)* classes. Basically, there are three ways to do that:


1. Using a global variable.
2. Using a script variable.
3. Using a member variable of *AppSystemLogic* or *AppWorldLogic* classes.


This example illustrates all three ways of sharing data, showing:


- how to declare and use a global variable;
- how to declare a variable in the world script and use it in the methods of the *AppSystemLogic* class;
- how to use member variables of *AppSystemLogic* class in the methods of *AppWorldLogic* and vice versa.


## Using a Global Variable


We can declare a global variable in a separate file, so we add a couple of files to our project:


- `global.h` file. ```cpp // global.h #ifndef __GLOBAL_H__ #define __GLOBAL_H__ extern int global_var; #endif // __GLOBAL_H__ ```
- `global.cpp` file. ```cpp // global.cpp #include "global.h" int global_var = 33; ```


Now in order to use this variable in the methods of *AppSystemLogic* or *AppWorldLogic* classes we just need to include the **global.h** in the corresponding header or implementation file.


## Using a Script Variable


We can declare a variable in our world script file (UnigineScript) named **<YOUR_PROJECT_NAME>.usc**.


```cpp
// <YOUR_PROJECT_NAME>.usc
#include <core/unigine.h>
// This file is in UnigineScript language.
// World script, it takes effect only when the world is loaded.

// world script variable
int worldscript_var = 100;

/*  */

```


Now in order to use this world script variable in the methods of *AppSystemLogic* class as an example, we can use the *[Engine::getWorldVariable()](../../../api/library/engine/class.engine_cpp.md#getWorldVariable_const_char_ptr_const_Variable_ref)* method. So, we must include the `UnigineInterface.h` library and add the following code to the `AppSystemLogic.cpp` file:


```cpp
// AppSystemLogic.cpp
#include <UnigineInterface.h>

/*  */

using namespace Unigine;

// engine pointer
Engine *engine;

/*  */

int AppSystemLogic::init() {

	// getting the engine pointer
	engine = Engine::get();

/*  */

	return 1;
}

int AppSystemLogic::update() {

/*  */

	// checking if there is a variable with a given name in the world script
	if (engine->isWorldVariable("worldscript_var"))
	{
		// getting the value of the world script variable
		int ws_var = engine->getWorldVariable("worldscript_var").getInt();
		if (ws_var <= 110)
		{
			Log::message("\nSYSTEMLOGIC UPDATE: Worldscript variable (modified value) worldscript_var = %d\n\n", ws_var);
			// changing the value of the world script variable
			engine->setWorldVariable("worldscript_var", Variable(ws_var + 1));
		}
	}

	return 1;
}
/*  */

```


## Using Member Variables


In the `AppWorldLogic.h` file, add the following code to define a pointer to the AppSystemLogic instance and a world logic variable. We must also include the `AppSystemLogic.h` header file.


```cpp
// AppWorldLogic.h

/*  */

#include "AppSystemLogic.h"

class AppSystemLogic;

class AppWorldLogic : public Unigine::WorldLogic {

public:

/*  */

	// pointer to the systemlogic
	AppSystemLogic *systemlogic_ptr;

	// world logic variable
	int worldlogic_var = 11;
};

/*  */

```


In the `AppSystemLogic.h` file, add the following code to define a pointer to the *AppWorldLogic* instance and a system logic variable. And again we must include the `AppWorldLogic.h` header file.


```cpp
// AppSystemLogic.h

/*  */

#include "AppWorldLogic.h"

class AppWorldLogic;

class AppSystemLogic : public Unigine::SystemLogic {

public:

/*  */

	// pointer to the worldlogic
	AppWorldLogic *worldlogic_ptr;

	// system logic variable
	int systemlogic_var = 22;
};

/*  */

```


In order to get access to the member variables of the instances of the *AppSystemLogic* and *AppWorldLogic* classes we should initialize our pointers. So we must insert the following code to the main file of our project called **<YOUR_PROJECT_NAME>.cpp** file.


```cpp
// <YOUR_PROJECT_NAME>.cpp
#include <UnigineEngine.h>
#include "AppSystemLogic.h"
#include "AppWorldLogic.h"

#ifdef _WIN32
	int wmain(int argc,wchar_t *argv[]) {
#else
	int main(int argc,char *argv[]) {
#endif

	Unigine::EnginePtr engine(argc,argv);


	AppSystemLogic system_logic;
	AppWorldLogic world_logic;

	// initialize pointers
	system_logic.worldlogic_ptr = &world_logic;
	world_logic.systemlogic_ptr = &system_logic;

	engine->main(&system_logic,&world_logic);

	return 0;
}

```


Now we can manage these variables in the methods of *AppWorldLogic* and *AppSystemLogic* classes by simply using *systemlogic_ptr->systemlogic_var* and *worldlogic_ptr->worldlogic_var* respectively.


## Combining All Three Approaches


Let us combine the three approaches and use our global, world script and member variables in the methods of the *AppWorldLogic* class:


```cpp
// AppWorldLogic.cpp
/*  */

// including the global.h to use our global variable
#include "global.h"
using namespace Unigine;

/*  */

int AppWorldLogic::init() {

	Log::warning("\nWorldlogic reporting:\n");

	// modifying a global variable
	global_var += 1000;
	Log::message("\nGlobal variable (+1000 value) global_var = %d", global_var);
	Log::message("\nSystemlogic variable (initial value) system_var = %d", systemlogic_ptr->systemlogic_var);

	// modifying a system logic variable
	systemlogic_ptr->systemlogic_var = 11;
	Log::message("\nSystemlogic variable (modified value) system_var = %d \n\n", systemlogic_ptr->systemlogic_var);

	return 1;
}

int AppWorldLogic::update() {

	// managing a system logic variable
	if (systemlogic_ptr->systemlogic_var > 0){
		systemlogic_ptr->systemlogic_var--;
		Log::message("\nWORLDLOGIC UPDATE: Systemlogic variable (modified value) system_var = %d", systemlogic_ptr->systemlogic_var);
	}
	return 1;
}

/* .. */

```


and the *AppSystemLogic* class:


```cpp
// AppSystemLogic.cpp
/*  */

#include <UnigineInterface.h>

// including the global.h to use our global variable
#include "global.h"

using namespace Unigine;
Engine *engine;

/*  */

int AppSystemLogic::init() {
	// getting an engine pointer
	engine = Engine::get();

	Log::warning("\nSystemlogic reporting:\n ");

	// modifying a global variable
	global_var += 1000;
	Log::message("\nGlobal variable (+1000 value) global_var = %d", global_var);
	Log::message("\nWorldlogic variable (initial value) world_var = %d", worldlogic_ptr->worldlogic_var);

	// modifying a world logic variable
	worldlogic_ptr->worldlogic_var += 100;
	Log::message("\nWorldlogic variable (modified value) world_var = %d\n\n", worldlogic_ptr->worldlogic_var);

	return 1;
}

int AppSystemLogic::update() {
	// checking if there is a variable with a given name in the world script
	if (engine->isWorldVariable("worldscript_var")){
		// getting the value of the world script variable
		int ws_var = engine->getWorldVariable("worldscript_var").getInt();
		if (ws_var <= 110)
		{
			Log::message("\nSYSTEMLOGIC UPDATE: Worldscript variable (modified value) worldscript_var = %d\n\n", ws_var);
			// changing the value of the world script variable
			engine->setWorldVariable("worldscript_var", Variable(ws_var + 1));
		}
	}

	return 1;
}

/* .. */

```
