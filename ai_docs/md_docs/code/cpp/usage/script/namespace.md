# Library's Namespace

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


By default, all variables and functions are exported from C++ in the global namespace. Libraries provide a convenient way to organize exposed functionality by adding a library's namespace. This namespace is used instead of `Foo::Bar` syntax that is not allowed for export.


## Namespace Export Example


1. In order to use a library namespace, a library should be registered first via *[Unigine::Interpreter::addExternLibrary()](../../../../api/library/common/class.interpreter_cpp.md#addExternLibrary_const_char_ptr_int_void)*.
2. After that, you can use a library namespace to register your variables and functions.


```cpp
#include <UnigineEngine.h>
#include <UnigineInterpreter.h>
#include <UnigineInterface.h>

#include "AppSystemLogic.h"
#include "AppWorldLogic.h"

using namespace Unigine;

// A variable within a namespace for export.
namespace Foo {
	int i = 25;
}

#ifdef _WIN32
	int wmain(int argc,wchar_t *argv[]) {
#else
	int main(int argc,char *argv[]) {
#endif

	// Register a library in order to use a library namespace.
	Interpreter::addExternLibrary("Foo");

	// Export a variable with a library prefix.
	Interpreter::addExternVariable("Foo.integer",MakeExternVariable(&Foo::i));

	AppSystemLogic system_logic;
	AppWorldLogic world_logic;

	Unigine::EnginePtr engine(argc,argv);

	// Enter main loop.
	engine->main(&system_logic,&world_logic);

	return 0;
}

```


### Access from Scripts


You can simply call the registered variables, functions, classes from Unigine scripts using the registered name. (If *Foo* library is not registered, the first dot in an object or function name is treated as an operator of class member access, which is wrong in our case).


In the *init()* function of the world script `.usc` file add the following:


```cpp
// my_world.usc

int init() {
	/* ... code ... */

	log.message("Foo.i is %d\n",Foo.integer);
	engine.console.setActivity(1);

	/* ... code ... */

}

```


### Output


The following console message will be printed:


```text
Foo.i is 25
```
