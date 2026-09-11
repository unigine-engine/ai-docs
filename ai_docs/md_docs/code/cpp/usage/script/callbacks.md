# Callbacks

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Any function from system, world or editor scripts can be called in a C++ code. UnigineScript functions that are called from an external code are known as callbacks. Via callbacks scripts can communicate with each other, as well as with the external application.


- Callbacks support up to **4** arguments and can return a value of an arbitrary type.


### See also


An example can be found in `<UnigineSDK>/source/samples/Api/Scripts/Callbacks/` directory.


## Callbacks Usage Example


### C++ Side


To demonstrate how callbacks can be used, let's code the C++ part first. Here's code from `your_project_name.cpp` file:


```cpp
#include <UnigineEngine.h>
#include <UnigineInterpreter.h>
#include <UnigineInterface.h>

#include "AppSystemLogic.h"
#include "AppWorldLogic.h"

using namespace Unigine;

/*
	World function
*/
const Variable &runWorldFunction(const Variable &name,const Variable &v) {

	Log::warning("runWorldFunction(%s,%s) is called\n",name.getTypeName().get(),v.getTypeName().get());

	Engine *engine = Engine::get();
	return engine->runWorldFunction(name,v);
}

/*
*/
#ifdef _WIN32
	int wmain(int argc,wchar_t *argv[]) {
#else
	int main(int argc,char *argv[]) {
#endif

	// export the runWorldFunction() function defined above
	Unigine::Interpreter::addExternFunction("runWorldFunction", MakeExternFunction(&runWorldFunction));

	AppSystemLogic system_logic;
	AppWorldLogic world_logic;

	Unigine::EnginePtr engine(argc,argv);

	engine->main(&system_logic,&world_logic);

	return 0;
}

```


The following code should be in `AppWorldLogic.cpp`


```cpp
#include "AppWorldLogic.h"
#include "UnigineEditor.h"
#include "UnigineGame.h"

#include <UnigineInterpreter.h>

using namespace Unigine;
/*
 */
AppWorldLogic::AppWorldLogic() {

}

AppWorldLogic::~AppWorldLogic() {

}

/*
 */
int AppWorldLogic::init() {
	return 1;
}

int AppWorldLogic::shutdown() {
	return 1;
}

/*
 */
int AppWorldLogic::update() {
	/*
		Callbacks usage example
	*/

	// call the counter() function of the script
	Variable ret = Engine::get()->runWorldFunction(Variable("counter"));
	// print a message depending on the value returned by the counter() script function:
	// print the current value of the counter
	if (ret.getInt() != -1) Log::message("counter is: %d\n", ret.getInt());
	// print the path to the world file
	if (ret.getInt() == 3) Log::message("\nworld-file path is: \"%s\"\n", Engine::get()->runWorldFunction(Variable("engine.world.getPath")).getString());

	return 1;
}

int AppWorldLogic::postUpdate() {
	return 1;
}

int AppWorldLogic::updatePhysics() {
	return 1;
}

```


### Unigine Script Side


> **Notice:** The required world should be loaded and the script assigned to this `*.world` should not contain any compilation errors.


The world script file where callbacks are defined:


```cpp
// unigine_project.usc

/*
*/
int callback(int value) {

	log.warning("callback(%s) is called\n",typeinfo(value));

	return value;
}

/*
*/
void counter() {

	for(int i = 0; i < 4; i++) {
		log.warning("counter(): called\n");
		yield i;
	}

	return -1;
}

/*
*/
int init() {

	log.message("\n");

	// run the callback() script function via the API runWorldFunction() function
	log.message("result is: %s\n\n",typeinfo(runWorldFunction("callback",10)));
	log.message("result is: %s\n\n",typeinfo(runWorldFunction("callback",vec3(1,2,3))));
	log.message("result is: %s\n\n",typeinfo(runWorldFunction("callback","a string")));

	/////////////////////////////////

	// show a console
	engine.console.setActivity(1);

	return 1;
}

```


### Calling Sequence


The sequence of function call will be as follows:


1. The interpreter exports the *runWorldFunction()* function to make it available from the script.
2. The engine is initialized, and the *init()* function of the script is called. This function calls the exported *runWorldFunction()* function.
3. The exported *runWorldFunction()* function calls the *callback()* function from the script.
4. The engine enters the main loop, where it calls the *counter()* function from the script by using the [*Unigine::Engine::runWorldFunction()*](../../../../api/library/engine/class.engine_cpp.md#runWorldFunction_const_Variable_ref_const_Variable_ref) function.


### Output


The following result will be printed into the console:


```text
runWorldFunction(string,int): called
callback(int: 10): called
result is: int: 10

runWorldFunction(string,vec3): called
callback(vec3: 1 2 3): called
result is: vec3: 1 2 3

runWorldFunction(string,string): called
callback(string: "a string") is called
result is: string: "a string"

counter(): called
counter is: 0
counter(): called
counter is: 1
counter(): called
counter is: 2
counter(): called
counter is: 3

world world-file path is: "unigine_project/unigine_project"

```
