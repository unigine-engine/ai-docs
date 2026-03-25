# Sharing Data between the Logic System Components (CS)


Sometimes it is necessary to share data between the elements of the [Logic System](../../../code/fundamentals/execution_sequence/app_logic_system.md): *[WorldLogic](../../../api/library/common/logic/class.worldlogic_cs.md), [SystemLogic](../../../api/library/common/logic/class.systemlogic_cs.md)* classes. Basically, there are three ways to do that:


1. Using a global variable.
2. Using a script variable.
3. Using a member variable of *AppSystemLogic* or *AppWorldLogic* classes.


This example illustrates all three ways of sharing data, showing:


- how to declare and use a global variable;
- how to declare a variable in the world script and use it in the methods of the *AppSystemLogic* class;
- how to use member variables of *AppSystemLogic* class in the methods of *AppWorldLogic* and vice versa.


## Using a Global Variable


We can declare a global variable class in a separate file, so we add a file to our project:


- `GlobalVar.cs` file. ```csharp // GlobalVar.cs namespace UnigineApp { public static class GlobalVar { public static int int_var = 33; } } ```


Now we can manage this global variable in the methods of *AppSystemLogic* or *AppWorldLogic* classes by simply typing *GlobalVar.int_var*.


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


Now in order to use this world script variable in the methods of *AppSystemLogic* class as an example, we can use the *[Engine.getWorldVariable()](../../../api/library/engine/class.engine_cs.md#getWorldVariable_const_char_ptr_const_Variable_ref)* method. So, we must add the following code to the `AppSystemLogic.cs` file:


```csharp
// AppSystemLogic.cs

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Unigine;

namespace UnigineApp
{
    class AppSystemLogic : SystemLogic
    {

        /*  */

        public override bool Update()
        {
            /*  */

            // checking if there is a variable with a given name in the world script
            if (Engine.engine.IsWorldVariable("worldscript_var"))
            {
                // getting the value of the world script variable
                int ws_var = Engine.engine.GetWorldVariable("worldscript_var").Int;
                if (ws_var <= 110)
                {
                    Log.Message("\nSYSTEMLOGIC UPDATE: Worldscript variable (modified value) worldscript_var = {0}\n\n", ws_var);
                    // changing the value of the world script variable
                    Engine.engine.SetWorldVariable("worldscript_var", new Variable(ws_var + 1));
                }
            }

            return true;
        }

        /*  */

    }
}

```


## Using Member Variables


In the `AppWorldLogic.cs` file, add the following code to define a pointer to the AppSystemLogic instance and a world logic variable.


```csharp
// AppWorldLogic.cs

/*  */

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Unigine;

namespace UnigineApp
{
	class AppWorldLogic : WorldLogic
	{
        // world logic variable
		public int worldlogic_var = 11;

		// pointer to the systemlogic
        AppSystemLogic system_logic;

		// method setting the pointer to the systemlogic
        public void setSL(AppSystemLogic SL)
        {
            system_logic = SL;
        }

		/*  */

	}
}

```


In the `AppSystemLogic.cs` file, add the following code to define a pointer to the *AppWorldLogic* instance and a system logic variable.


```cpp
// AppSystemLogic.cs

/*  */

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Unigine;

namespace UnigineApp
{

	class AppSystemLogic : SystemLogic
	{
        // system logic variable
        public int systemlogic_var = 22;

		// pointer to the worldlogic
        AppWorldLogic world_logic;

		// method setting the pointer to the worldlogic
        public void setWL(AppWorldLogic WL)
        {
            world_logic = WL;
        }

		/*  */

	}
}

```


In order to get access to the member variables of the instances of the *AppSystemLogic* and *AppWorldLogic* classes we should initialize our pointers. So we must insert the following code to the main file of our project called **<YOUR_PROJECT_NAME>.cs** file.


```csharp
// <YOUR_PROJECT_NAME>.cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Unigine;

namespace UnigineApp
{
	class UnigineApp
	{

		static void Main(string[] args)
		{
			AppSystemLogic systemLogic = new AppSystemLogic();
			AppWorldLogic worldLogic = new AppWorldLogic();

			// initialize pointers
			worldLogic.setSL(systemLogic);
			systemLogic.setWL(worldLogic);

			Engine engine = Engine.Init(Engine.VERSION, args);

			engine.Main(systemLogic, worldLogic);

			Engine.Shutdown();
		}
	}
}

```


Now we can manage these variables in the methods of *AppWorldLogic* and *AppSystemLogic* classes by simply using *system_logic->systemlogic_var* and *world_logic->worldlogic_var* respectively.


### Accessing Member Variables from C# Components


In case of using the [C# Component System](../../../principles/component_system/component_system_cs/index.md), you might want to organize access from components to some shared data stored by the instances of *[WorldLogic](../../../api/library/common/logic/class.worldlogic_cs.md), [SystemLogic](../../../api/library/common/logic/class.systemlogic_cs.md)* classes as member variables.


A simple way to implement that would be to use the desired class as a singleton. For example, let's take the *[SystemLogic](../../../api/library/common/logic/class.systemlogic_cs.md)* in case you want to have shared data at the system level available across multiple worlds):


```csharp
// AppSystemLogic.cs

class AppSystemLogic : SystemLogic
{
	// singleton design pattern
	private static AppSystemLogic instance;
	public static AppSystemLogic Get() { return instance; }

	// global variable to be used by components across multiple worlds
	public int GlobalVar = 30;

	public override bool Init()
	{
		instance = this;
		return true;
	}
}

```


Then, in your component's code, your can access the variable like this:


```csharp
// MyComponent.cs

// ...
public partial class MyComponent : Component
{

	private void Init()
	{
		// getting the value of the GlobalVar variable
		Log.Message("-> The global variable is equal to {0}\n", AppSystemLogic.Get().GlobalVar);
		// ...
	}
}

```


## Combining All Three Approaches


Let us combine the three approaches and use our global, world script and member variables in the methods of the *AppWorldLogic* class:


```csharp
// AppWorldLogic.cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Unigine;

namespace UnigineApp
{
	class AppWorldLogic : WorldLogic
	{
        // world logic variable
		public int worldlogic_var = 11;

		// pointer to the systemlogic
        AppSystemLogic system_logic;

		/*  */

        // method setting the pointer to the systemlogic
        public void setSL(AppSystemLogic SL)
        {
            system_logic = SL;
        }

		public override bool Init()
		{

        	// modifying a global variable
	        GlobalVar.int_var += 1000;
            Log.Message("\nGlobal variable (+1000 value) global_var = {0}", GlobalVar.int_var);
            Log.Message("\nSystemlogic variable (initial value) system_var = {0}", system_logic.systemlogic_var);

	        // modifying a system logic variable
	        system_logic.systemlogic_var = 11;
            Log.Message("\nSystemlogic variable (modified value) system_var = {0} \n\n", system_logic.systemlogic_var);

			return true;
		}

		// start of the main loop
		public override bool Update()
		{
	        // managing a system logic variable
            if (system_logic.systemlogic_var > 0)
            {
                system_logic.systemlogic_var--;

                Log.Message("\nWORLDLOGIC UPDATE: Systemlogic variable (modified value) system_var = {0}", system_logic.systemlogic_var);
            }
			return true;
		}

		/*  */
	}
}

```


and the *AppSystemLogic* class:


```csharp
// AppSystemLogic.cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Unigine;

namespace UnigineApp
{
	class AppSystemLogic : SystemLogic
	{
		// system logic variable
        public int systemlogic_var = 22;

		// pointer to the worldlogic
        AppWorldLogic world_logic;

        /*  */

        public void setWL(AppWorldLogic WL)
        {
            world_logic = WL;
        }

		public override bool Init()
		{
	        Log.Warning("\nSystemlogic reporting:\n ");

	        // modifying a global variable
            GlobalVar.int_var += 1000;
            Log.Message("\nGlobal variable (+1000 value) global_var = {0}", GlobalVar.int_var);

        	// managing a world logic variable
			Log.Message("\nWorldlogic variable (initial value) world_var = {0}", world_logic.worldlogic_var);
	        world_logic.worldlogic_var += 100;
            Log.Message("\nWorldlogic variable (modified value) world_var = {0}\n\n", world_logic.worldlogic_var);

			return true;
		}

		// start of the main loop
		public override bool Update()
		{
	        // managing a worldscript variable
	        if (Engine.engine.IsWorldVariable("worldscript_var")){
	    	    int ws_var = Engine.engine.GetWorldVariable("worldscript_var").Int;
	    	    if (ws_var <= 110)
	    	    {
	    		    Log.Message("\nSYSTEMLOGIC UPDATE: Worldscript variable (modified value) worldscript_var = {0}\n\n", ws_var);
	    		    Engine.engine.SetWorldVariable("worldscript_var", new Variable(ws_var + 1));
	    	    }
	        }

			return true;
		}

		/*  */
	}
}

```
