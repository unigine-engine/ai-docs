# Splitting Logic Between Several WorldLogic Classes (CPP)


Each [world script](../../../code/fundamentals/execution_sequence/app_logic_system.md#world_script) is associated with a certain world. Although the basic recommended workflow when writing application logic in *[C++](../../../code/cpp/index.md) / [C#](../../../code/csharp/index.md)* is to have a single *AppWorldLogic* class to process all worlds in your project, sometimes it might be necessary to split world logic between several separate classes. In such a case the basic *AppWorldLogic* class is used as a manager calling corresponding methods (*[init()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_init), [update()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_update), [postUpdate()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_postUpdate)*, etc.) of a particular class implementing logic of the current world.


This example illustrates how to split world-specific code between separate classes. Suppose in our project we have a default world named "*world1*" and another one named "*world2*" and we want to have two separate world logic classes (*WorldLogic1* and *WorldLogic2*) for each of these worlds. Suppose we also want to switch between these worlds by pressing *PGUP* and *PGDOWN* keys.


## 1. Creating WorldLogic Classes


First, we just inherit two new classes (*WorldLogic1* and *WorldLogic2*) from *[Unigine::WorldLogic](../../../api/library/common/logic/class.worldlogic_cpp.md)*. You can simply copy the contents of **AppWorldLogic.h** and **AppWorldLogic.cpp** files and modify their *init()* and *update()* methods like this:


> **Notice:** You can implement your logic for other methods of the [execution sequence](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic) if necessary.


<details>
<summary>WorldLogic1.cpp | Close</summary>

**WorldLogic1.cpp**


```cpp
// ...

int WorldLogic1::init()
{
	// reporting that we're processing the first world and displaying a path to the .world file
	Log::message("Initializing the FIRST world (%s)\n", World::getPath());

	// insert your init logic for the first world

	return 1;
}

int WorldLogic1::update()
{
	// insert your update logic for the first world

	return 1;
}

// ...


```

</details>


<details>
<summary>WorldLogic2.cpp | Close</summary>

**WorldLogic2.cpp**


```cpp
// ...

int WorldLogic2::init()
{
	// reporting that we're processing the first world and displaying a path to the .world file
	Log::message("Initializing the SECOND world (%s)\n", World::getPath());

	// insert your init logic for the second world

	return 1;
}

int WorldLogic2::update()
{
	// insert your update logic for the second world

	return 1;
}

// ...


```

</details>


## 2. Managing World Logics via AppWorldLogic


Now, we implement world logic management in the *AppWorldLogic*, so we should add all our world logics, and a pointer to the one currently used. In the *init()* method, as it is called each time a new world is loaded, we should change the current world logic. So we modify the **AppWorldLogic.h** file as follows:


<details>
<summary>AppWorldLogic.h | Close</summary>

**AppWorldLogic.h**


```cpp
// ...

#include "WorldLogic1.h"		//<-- include world logic class declaration for the first world
#include "WorldLogic2.h"		//<-- include world logic class declaration for the second world

class AppWorldLogic : public Unigine::WorldLogic
{

public:

// ...


	Unigine::WorldLogic* current_world_logic = &wl1;	//<-- pointer to the current world logic, we set the first one by default

private:
	WorldLogic1 wl1;									//<-- world logic for the first world
	WorldLogic2 wl2;									//<-- world logic for the second world
};

//...


```

</details>


Inside each method of the *AppWorldLogic* class, we simply call the corresponding method of the current world logic class, like for the *init()* and *update()* methods below. In the *init()* method, as it is called each time a new world is loaded, we also should change the current world logic, if necessary:


<details>
<summary>AppWorldLogic.cpp | Close</summary>

**AppWorldLogic.cpp**


```cpp
#include <UnigineWorld.h>	//<-- include the UnigineWorld.h for the World class

using namespace Unigine;
// ...

int AppWorldLogic::init()
{
	// checking the name of the loaded world and updating current world logic
	if (strstr(World::getPath(), "world1.world"))
		current_world_logic = &wl1;
	else if (strstr(World::getPath(), "world2.world"))
		current_world_logic = &wl2;

	// calling the init() method of the current world logic
	current_world_logic->init();

	return 1;
}

int AppWorldLogic::update()
{
	// calling the update() method of the current world logic
	current_world_logic->update();

	return 1;
}


```

</details>


## 3. Keyboard World Loading via AppSystemLogic


Switching between the worlds is to be performed in the *AppSystemLogic* class. In the *update()* method we should check keyboard input and load the corresponding world, if necessary. So, we modify the **AppSystemLogic.cpp** file as follows:


<details>
<summary>AppSystemLogic.cpp | Close</summary>

**AppSystemLogic.cpp**


```cpp
#include <UnigineWorld.h>

// ...
int AppSystemLogic::update()
{
	// checking key states and loading worlds
	if (Input::isKeyPressed(Input::KEY_PGUP))
	{	// loading the second world if it is not already loaded
		if (strstr(World::getPath(), "world1.world"))
			World::loadWorld("world2");
	}
	else if (Input::isKeyPressed(Input::KEY_PGDOWN))
	{	// loading the first world if it is not already loaded
		if (strstr(World::getPath(), "world2.world"))
			World::loadWorld("world1");
	}

	return 1;
}


```

</details>
