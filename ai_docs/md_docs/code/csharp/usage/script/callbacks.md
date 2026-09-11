# Callbacks

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Any function from system, world or editor scripts can be called in a C# code. UnigineScript functions that are called from an external code are known as callbacks. Via callbacks scripts can communicate with each other, as well as with the external application.


The callback functions can receive optional arguments of the *int* or *IntPtr* type that are used to store user data. *IntPtr* values can be wrapped in classes, for example:


```csharp
IntPtr ptr;
// create a node and then create a Unigine object
Unigine.Object.create(new Node(ptr));

```


See the article on [Widget Dialog usage example](../../../../code/csharp/usage/widgetdialog.md) for more details.


### See also


An example can be found in `<UnigineSDK>/source/csharp/samples/Api/Scripts/Callbacks/` directory.


## Callbacks Usage Example


### C# Side


To demonstrate how callbacks can be used, let's code the C# part first. Here's code from `your_project_name.cs` file:


```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Unigine;

namespace UnigineApp
{
	class UnigineApp
	{
		// world function
		private static Variable runWorldFunction(Variable name, Variable v)
		{
			Log.Warning("runWorldFunction({0},{1}): called\n", name.TypeName, v.TypeName);

			return Engine.engine.RunWorldFunction(name, v);
		}

		static void Main(string[] args)
		{
			// export the runWorldFunction() function defined above
			Interpreter.AddExternFunction("runWorldFunction", new Interpreter.Function2v(runWorldFunction));

			AppSystemLogic systemLogic = new AppSystemLogic();
			AppWorldLogic worldLogic = new AppWorldLogic();
			Engine engine = Engine.Init(Engine.VERSION, args);

			engine.Main(systemLogic, worldLogic);

			Engine.Shutdown();
		}
	}
}

```


The following code should be in `AppWorldLogic.cs`


```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Unigine;

namespace UnigineApp
{
	class AppWorldLogic : WorldLogic
	{
		public AppWorldLogic()
		{
		}

		public override bool Init()
		{
			return true;
		}

		public override bool Shutdown()
		{
			return true;
		}

		public override bool Update()
		{
			/*
			 * Callbacks usage example
			 */
			// call the counter() function of the script (defined below)
			Variable ret = Engine.engine.RunWorldFunction(new Variable("counter"));
			// print a message depending on the value returned by the counter() script function:
			// print the current value of the counter
			if (ret.GetInt() != -1) Log.Message("counter is: {0}\n", ret.GetInt());
			// print the path to the world file
			if (ret.getInt() == 3) Log.Message("\nworld-file path is: \"{0}\"\n", Engine.engine.RunWorldFunction(new Variable("engine.world.getPath")).GetString());
			return true;
		}

		public override bool PostUpdate()
		{
			return true;
		}

		public override bool UpdatePhysics()
		{
			return true;
		}
	}
}

```


### Unigine Script Side


And now the UnigineScript side where callbacks are defined:


```cpp
#include <core/unigine.h>

int callback(int value) {

	log.warning("callback(%s) is called\n",typeinfo(value));

	return value;
}

void counter() {

	for(int i = 0; i < 4; i++) {
		log.warning("counter(): called\n");
		yield i;
	}

	return -1;
}

int init() {
	Player player = new PlayerSpectator();
	player.setPosition(Vec3(0.0f,-3.401f,1.5f));
	player.setDirection(Vec3(0.0f,1.0f,-0.4f));
	engine.game.setPlayer(player);

	log.message("\n");

	// run the callback() script function via the API runWorldFunction() function
	log.message("result is: %s\n\n",typeinfo(runWorldFunction("callback",10)));
	log.message("result is: %s\n\n",typeinfo(runWorldFunction("callback",vec3(1,2,3))));
	log.message("result is: %s\n\n",typeinfo(runWorldFunction("callback","a string")));

	// show a console
	engine.console.setActivity(1);

	return 1;
}

int shutdown() {
	return 1;
}

int update() {
	return 1;
}

```


### Calling Sequence


The sequence of function call will be as follows:


1. The interpreter exports the *RunWorldFunction()* function to make it available from the script.
2. The engine is initialized, and the *Init()* function of the script is called. This function calls the exported *RunWorldFunction()* function.
3. The exported *runWorldFunction()* function calls the *callback()* function from the script.
4. The engine enters the main loop, where it calls the *counter()* function from the script by using the *Unigine.Engine.RunWorldFunction()* function which has the same behavior as the [*Unigine::Engine::runWorldFunction()*](../../../../api/library/engine/class.engine_cpp.md#runWorldFunction_const_Variable_ref_const_Variable_ref) C++ API function.


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
callback(string: "a string"): called
result is: string: "a string"

counter(): called
counter is: 0
counter(): called
counter is: 1
counter(): called
counter is: 2
counter(): called
counter is: 3

world-file path is: "unigine_project/unigine_project.world"

```
