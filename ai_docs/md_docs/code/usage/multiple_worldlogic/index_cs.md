# Splitting Logic Between Several WorldLogic Classes (CS)


Each [world script](../../../code/fundamentals/execution_sequence/app_logic_system.md#world_script) is associated with a certain world. Although the basic recommended workflow when writing application logic in *[C++](../../../code/cpp/index.md) / [C#](../../../code/csharp/index.md)* is to have a single *AppWorldLogic* class to process all worlds in your project, sometimes it might be necessary to split world logic between several separate classes. In such a case the basic *AppWorldLogic* class is used as a manager calling corresponding methods (*[init()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_init), [update()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_update), [postUpdate()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_postUpdate)*, etc.) of a particular class implementing logic of the current world.


This example illustrates how to split world-specific code between separate classes. Suppose in our project we have a default world named "*world1*" and another one named "*world2*" and we want to have two separate world logic classes (*WorldLogic1* and *WorldLogic2*) for each of these worlds. Suppose we also want to switch between these worlds by pressing *PGUP* and *PGDOWN* keys.


## 1. Creating WorldLogic Classes


First, we just inherit two new classes (*WorldLogic1* and *WorldLogic2*) from *[Unigine.WorldLogic](../../../api/library/common/logic/class.worldlogic_cs.md)*. You can simply copy the contents of **AppWorldLogic.cs** file and modify their *init()* and *update()* methods like this:


> **Notice:** You can implement your logic for other methods of the [execution sequence](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic) if necessary.


<details>
<summary>WorldLogic1.cs | Close</summary>

**WorldLogic1.cs**


```csharp
// ...

namespace UnigineApp
{
    class WorldLogic1 : WorldLogic
    {
        public WorldLogic1()
		{
		}

		public override bool Init()
		{
            Log.Message("Initializing the FIRST world ({0})\n", World.Path);

			// insert your init logic for the first world

			return true;
		}

		public override bool Update()
		{
			// insert your update logic for the first world

			return true;
		}

		// ...
    }
}

```

</details>


<details>
<summary>WorldLogic2.cs | Close</summary>

**WorldLogic2.cs**


```csharp
// ...

namespace UnigineApp
{
    class WorldLogic2: WorldLogic
    {
        public WorldLogic2()
		{
		}

		public override bool Init()
		{
            Log.Message("Initializing the SECOND world ({0})\n", World.Path;

			// insert your init logic for the second world
			return true;
		}

		public override bool Update()
		{
			// insert your update logic for the second world

			return true;
		}

		// ...
    }
}

```

</details>


## 2. Managing World Logics via AppWorldLogic


Now, we implement world logic management in the *AppWorldLogic*, so we should add all our world logics, and a pointer to the one currently used. Inside each method of the *AppWorldLogic* class, we simply call the corresponding method of the current world logic class, like for the *init()* and *update()* methods below. In the *init()* method, as it is called each time a new world is loaded, we should change the current world logic. So, we modify the **AppWorldLogic.cs** file as follows:


<details>
<summary>AppWorldLogic.cs | Close</summary>

**AppWorldLogic.cs**


```csharp
// ...

using Unigine;

namespace UnigineApp
{
	class AppWorldLogic : WorldLogic
	{
		public WorldLogic1 wl1;						//<-- world logic for the first world
		public WorldLogic2 wl2;						//<-- world logic for the second world
		public WorldLogic current_world_logic;		//<-- pointer to the current world logic

		public AppWorldLogic()
		{
			// creating world logic instances and setting the first one as current
			wl1 = new WorldLogic1();
			wl2 = new WorldLogic2();
			current_world_logic = wl2;
		}

		public override bool Init()
		{
			// checking the name of the loaded world and changing current world logic if necessary
			if (string.Compare(World.Path, "world1.world") == 0)
				current_world_logic = wl1;
			else if (string.Compare(World.Path, "world2.world") == 0)
				current_world_logic = wl2;

			// calling the init() method of the current world logic
			current_world_logic.Init();

			return true;
		}

		// start of the main loop
		public override bool Update()
		{

			// calling the update() method of the current world logic
			current_world_logic.Update();

			return true;
		}

		// ...
	}
}

```

</details>


## 3. Keyboard World Loading via AppSystemLogic


Switching between the worlds is to be performed in the *AppSystemLogic* class. In the *update()* method we should check keyboard input and load the corresponding world, if necessary. So, we modify the **AppSystemLogic.cs** file as follows:


<details>
<summary>AppSystemLogic.cs | Close</summary>

**AppSystemLogic.cs**


```csharp
// ...

using Unigine;

namespace UnigineApp
{
	class AppSystemLogic : SystemLogic
	{
		// ...

		// start of the main loop
		public override bool Update()
		{

			// checking key states and switching worlds
			if (Input.IsKeyPressed(Input.KEY.PGUP))
			{
				// loading the first world if it is not already loaded
				if (World.Path.EndsWith("world2.world"))
					World.LoadWorld("world1");
			}
			else if (Input.IsKeyPressed(Input.KEY.PGDOWN))
			{
				// loading the second world if it is not already loaded
				if (World.Path.EndsWith("world1.world"))
					World.LoadWorld("world2");
			}
			return true;
		}
}

```

</details>


Now, the logic of each of our world files (*world1* and *world2*) is controlled by the corresponding *WorldLogic* class.
