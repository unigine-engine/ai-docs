# Using C++ Component System


The **[C++ Component System](../../../principles/component_system/component_system_cpp/index.md)** enables you to implement your application's logic via a set of building blocks - **components**, and assign these blocks to nodes. A logic component integrates a node, a property, and a C++ class containing logic implementation.


This example demonstrates how to:


- Decompose application logic into building blocks.
- Create your own logic components.
- Implement interaction between your components.


Let's make a simple game to demonstrate how the whole system works.


### See Also


This case is also provided as a SDK sample.


### Game Description


In the center of the play area, we are going to have an object (*Pawn*) controlled by the player via the keyboard. It has certain amount of HP and movement parameters (movement and rotation speed).


Four corners of the play area are occupied by rotating objects (*Spinner*) that throw other small objects (*Projectile*) in all directions while rotating.


Each Projectile moves along a straight line in the directon it has been initially thrown by the Spinner. If a Projectile hits a Pawn, the latter takes damage according to the value set for the hitting Projectile (each of them has a random speed and damage value). The pawn is destroyed if the amount of HP drops below zero.


![](game.gif)


We use boxes for simplicity, but you can easily replace them with any other objects.


The basic workflow for implementing application logic using the C++ Component System is given below.


## 1. Prepare a Project


Before we can start creating components and implementing our game logic, we should [create a new C++ project](../../../sdk/projects/index_cpp.md#creation).


![](create.png)


## 2. Decompose Application Logic into Building Blocks


First of all, we should decompose our application logic in terms of building blocks - components. So, we should define parameters for each component (all these parameters will be stored in a corresponding `*.prop` file) and decide in which functions of the [execution sequence](../../../code/fundamentals/execution_sequence/index.md) the component's logic will be implemented.


For our small game, we are going to use one component for each type of object. Thus, we need **3** components:


- **Pawn** with the following parameters: We are going to initialize the Pawn, do something with it each frame, and report a message, when the Pawn dies. Therefore, this logic will be implemented inside the *init(), update()*, and *shutdown()* methods.

  - *name* - name of the Pawn
  - *moving speed* - how fast the Pawn moves
  - *rotation speed* - how fast the Pawn rotates
  - *health* - HP count for the Pawn
- **Spinner** with the following parameters: We are going to initialize a Spinner and do something with it each frame. Therefore, this logic will go to the *init()* and *update()*.

  - *rotation speed* - how fast the Spinner rotates
  - *acceleration* - how fast Spinner's rotation rate increases
  - node to be used as a projectile
  - minimum spawn delay
  - maximum spawn delay
- **Projectile** with the following parameters: As for the projectile, it will be spawned and initialized by the Spinner. The only thing we are going to do with it, is checking for a hit and controlling the life time left every frame. All of this goes to *update()*.

  - *speed* - how fast the Projectile moves
  - *lifetime* - how long the Projectile lives
  - *damage* - how much damage the Projectile causes to the Pawn it hits


## 3. Create a C++ Class for Each Component


For each of our components, we should derive a new C++ class from the **ComponentBase** class. Therefore, we should do the following in the header file:


- Declare a component class. The name of the class is used as the name of the [property](../../../principles/properties/index.md) (the corresponding `*.prop` file is automatically saved in your project's `data` folder). To declare a class, use the following: ```cpp COMPONENT_DEFINE(my_property_name, Unigine::ComponentBase); ```
- Declare all parameters defined above with their default values (if any). To declare a parameter we can use the following macros (optional parameters are enclosed in square brackets []): ```cpp PROP_PARAM(type, name[, default_value, title, tooltip, group]); PROP_STRUCT(type, name); PROP_ARRAY(type, name); PROP_ARRAY_STRUCT(type, name); ```
- Declare which methods we are going to use to implement our logic, and during which stages of the [execution sequence](../../../code/fundamentals/execution_sequence/index.md) to call them: ```cpp public: COMPONENT_INIT(my_init); COMPONENT_UPDATE(my_update); COMPONENT_SHUTDOWN(my_shutdown); // ... protected: void my_init(); void my_update(); void my_shutdown(); ```
- Declare all necessary auxiliary parameters and functions.


Thus, for our *Pawn, Spinner*, and *Projectile* classes, we will have the following declarations:


<details>
<summary>Pawn.h | Close</summary>

`Pawn.h`


```cpp
#pragma once
#include <UnigineGame.h>
#include <UnigineControls.h>

// include the header file of the Component System
#include <UnigineComponentSystem.h>

using namespace Unigine;
using namespace Math;

// derive our class from the ComponentBase
class Pawn : public ComponentBase
{
public:
	// declare constructor and destructor for our class and define a property name. The Pawn.prop file containing all parameters listed below will be saved in your project's data folder
	COMPONENT_DEFINE(Pawn, ComponentBase)
		// declare methods to be called at the corresponding stages of the execution sequence
		COMPONENT_INIT(init);
	COMPONENT_UPDATE(update);
	COMPONENT_SHUTDOWN(shutdown);

	// parameters
	PROP_PARAM(String, name, "Pawn1");		// Pawn's name
	PROP_PARAM(Int, health, 200);			// health points
	PROP_PARAM(Float, move_speed, 4.0f);	// move speed (meters/s)
	PROP_PARAM(Float, turn_speed, 90.0f);	// turn speed (deg/s)

	// methods
	void hit(int damage);	// decrease Pawn's HP

protected:
	// world main loop overrides
	void init();
	void update();
	void shutdown();

private:
	// auxiliary parameters and functions
	ControlsPtr controls;
	PlayerPtr player;

	float damage_effect_timer = 0;
	Mat4 default_model_view;

	void show_damage_effect();
};

```

</details>


<details>
<summary>Spinner.h | Close</summary>

`Spinner.h`


```cpp
#pragma once
#include <UnigineMaterial.h>
#include <UnigineComponentSystem.h>

using namespace Unigine;
using namespace Math;

class Spinner : public ComponentBase
{
public:
	// declare constructor and destructor for the Spinner class
	COMPONENT_DEFINE(Spinner, ComponentBase);

	// declare methods to be called at the corresponding stages of the execution sequence
	COMPONENT_INIT(init);
	COMPONENT_UPDATE(update);

	// parameters
	PROP_PARAM(Float, turn_speed, 30.0f);
	PROP_PARAM(Float, acceleration, 5.0f);

	PROP_PARAM(Node, spawn_node);
	PROP_PARAM(Float, min_spawn_delay, 1.0f);
	PROP_PARAM(Float, max_spawn_delay, 4.0f);

protected:
	// world main loop
	void init();
	void update();

private:
	float start_turn_speed = 0;
	float color_offset = 0;
	float time_to_spawn = 0;
	MaterialPtr material;

	// converter from HSV to RGB color model
	vec3 hsv2rgb(float h, float s, float v);
};

```

</details>


<details>
<summary>Projectile.h | Close</summary>

`Projectile.h`


```cpp
#pragma once
#include <UnigineMaterial.h>
#include <UnigineComponentSystem.h>

using namespace Unigine;

class Projectile : public ComponentBase
{
public:
	// declare constructor and destructor for the Projectile class
	COMPONENT_DEFINE(Projectile, ComponentBase);

	// declare methods to be called at the corresponding stages of the execution sequence
	COMPONENT_UPDATE(update);

	// parameters
	PROP_PARAM(Float, speed, 5.0f);
	PROP_PARAM(Float, lifetime, 5.0f);	// life time of the projectile (declaration with a default value)
	PROP_PARAM(Int, damage);			// damage caused by the projectile (declaration with no default value)

	// methods
	void setMaterial(const MaterialPtr &mat);

protected:
	// world main loop
	void update();
};

```

</details>


## 4. Implement Each Component's Logic


After making necessary declarations, we should implement logic for all our components. Let's do it in the corresponding `*.cpp` files.


In each of these files, we should add the following macro to ensure automatic registration of the corresponding component by the Component System:


```cpp
REGISTER_COMPONENT ( your_component_name );

```


> **Warning:** Do not put this macro to header (`*.h`) files, otherwise your project won't be built!


### Pawn's Logic


The Pawn's logic is divided into the following elements:


- **Initialization** - here we set necessary parameters, and the Pawn reports its name: ```cpp Log::message("PAWN: INIT \"%s\"\n", name.get()); ``` > **Notice:** You can access parameters of your component via: **<parameter_name>.get()**
- **Main loop** - here we implement the player's keyboard control. > **Notice:** To access the node from the component, we can simply use **node**, e.g. to get the current node's direction we can write: > > > ```cpp > Vec3 direction = node->getWorldTransform().getColumn3(1); > > ```
- **Shutdown** - here we implement actions to be performed when a Pawn dies. We'll just print a message to the console.
- **Auxiliary** - a method to be called when the pawn is hit, and some visual effects.


Implementation of the Pawn's logic is given below:


<details>
<summary>Pawn.cpp | Close</summary>

`Pawn.cpp`


```cpp
#include "Pawn.h"
#include <UnigineConsole.h>
#include <UnigineRender.h>
REGISTER_COMPONENT(Pawn);		// macro for component registration by the Component System
#define DAMAGE_EFFECT_TIME 0.5f

void Pawn::init()
{
	player = Game::getPlayer();
	controls = player->getControls();

	default_model_view = player->getCamera()->getModelview();
	damage_effect_timer = 0;
	show_damage_effect();

	Log::message("PAWN: INIT \"%s\"\n", name.get());
}

void Pawn::update()
{
	// get delta time between frames
	float ifps = Game::getIFps();

	// show damage effect
	if (damage_effect_timer > 0)
	{
		damage_effect_timer = Math::clamp(damage_effect_timer - ifps, 0.0f, DAMAGE_EFFECT_TIME);
		show_damage_effect();
	}

	// if console is opened we disable any controls
	if (Console::isActive())
		return;

	// get the direction vector of the mesh from the second column (y axis) of the transformation matrix
	Vec3 direction = node->getWorldTransform().getColumn3(1);

	// checking controls states and changing pawn position and rotation
	if (controls->getState(Controls::STATE_FORWARD) || controls->getState(Controls::STATE_TURN_UP))
	{
		node->setWorldPosition(node->getWorldPosition() + direction * move_speed * ifps);
	}

	if (controls->getState(Controls::STATE_BACKWARD) || controls->getState(Controls::STATE_TURN_DOWN))
	{
		node->setWorldPosition(node->getWorldPosition() - direction * move_speed * ifps);
	}

	if (controls->getState(Controls::STATE_MOVE_LEFT) || controls->getState(Controls::STATE_TURN_LEFT))
	{
		node->setWorldRotation(node->getWorldRotation() * quat(0.0f, 0.0f, turn_speed * ifps));
	}

	if (controls->getState(Controls::STATE_MOVE_RIGHT) || controls->getState(Controls::STATE_TURN_RIGHT))
	{
		node->setWorldRotation(node->getWorldRotation() * quat(0.0f, 0.0f, -turn_speed * ifps));
	}
}

void Pawn::shutdown()
{
	Log::message("PAWN: DEAD!\n");
}

// method to be called when the Pawn is hit by a Projectile
void Pawn::hit(int damage)
{
	// take damage
	health = health - damage;

	// show effect
	damage_effect_timer = DAMAGE_EFFECT_TIME;
	show_damage_effect();

	// destroy
	if (health <= 0)
		node.deleteLater();

	Log::message("PAWN: damage taken (%d) - HP left (%d)\n", damage, health.get());
}

// auxiliary method implementing visual damage effect
void Pawn::show_damage_effect()
{
	float strength = damage_effect_timer / DAMAGE_EFFECT_TIME;
	Render::setFadeColor(vec4(0.5f, 0, 0, saturate(strength - 0.5f)));
	player->getCamera()->setModelview(default_model_view * Mat4(
		rotateX(Game::getRandomFloat(-5, 5) * strength) *
		rotateY(Game::getRandomFloat(-5, 5) * strength)));
}

```

</details>


### Projectile's Logic


The Projectile's logic is simpler - we just have to perform a check each frame whether we hit the Pawn or not. This means that we have to access the *Pawn* component from the *Projectile* component.


> **Notice:** To access certain component on a certain node (e.g. the one that was intersected in our case) we can write the following:
>
>
> ```cpp
> // get the component assigned to a node by type "MyComponent"
> MyComponent *my_component = getComponent<MyComponent>(some_node);
>
> // access some method of MyComponent
> my_component->someMyComponentMethod();
>
> ```


The Projectile has a limited life time, so we should destroy the node when its life time is expired.


> **Notice:** To destroy a node, to which a component is added, simply call: **node.deleteLater()**. The node will be destroyed with all its properties and components.


Implementation of the Projectile's logic is given below:


<details>
<summary>Projectile.cpp | Close</summary>

*Projectile.cpp*


```cpp
#include "Projectile.h"
#include "Pawn.h"
#include "Spinner.h"
#include <UnigineGame.h>
#include <UnigineWorld.h>

REGISTER_COMPONENT(Projectile);		// macro for component registration by the Component System

void Projectile::update()
{
	// get delta time between frames
	float ifps = Game::getIFps();

	// get the direction vector of the mesh from the second column (y axis) of the transformation matrix
	Vec3 direction = node->getWorldTransform().getColumn3(1);

	// move forward
	node->setWorldPosition(node->getWorldPosition() + direction * speed * ifps);

	// lifetime
	lifetime = lifetime - ifps;
	if (lifetime < 0)
	{
		// destroy current node with its properties and components

		node.deleteLater();
		return;
	}

	// check the intersection with nodes
	VectorStack<NodePtr> nodes; // VectorStack is much faster than Vector, but has some limits
	World::getIntersection(node->getWorldBoundBox(), nodes);
	if (nodes.size() > 1) // (because the current node is also in this list)
	{
		for (int i = 0; i < nodes.size(); i++)
		{
			Pawn *pawn = getComponent<Pawn>(nodes[i]);
			if (pawn)
			{
				// hit the player!
				pawn->hit(damage);

				// ...and destroy current node

				node.deleteLater();
				return;
			}
		}
	}
}

void Projectile::setMaterial(const MaterialPtr &mat)
{
	checked_ptr_cast<Object>(node)->setMaterial(mat, "*");
}

```

</details>


### Spinner's Logic


The Spinner's logic is divided into the following elements:


- **Initialization** - here we set necessary parameters to be used in the main loop.
- **Main loop** - here we rotate our Spinner and spawn nodes with Projectile components. We also set some parameters of the Projectile. There are **3** ways to change variables of another component:

  1. Directly via component (fast, easy) ```cpp component->int_parameter = component->int_parameter + 1; ```
  2. Via node's property (slower, more awkward) ```cpp for (int i = 0; i < node->getNumProperties(); i++) { PropertyPtr prop = node->getProperty(i); if (prop && (!strcmp(prop->getName(), "my_prop_name") || prop->isParent("my_prop_name"))) prop->setParameterInt(prop->findParameter("int_parameter"), 5); } ```
  3. Via component's property ```cpp PropertyPtr prop = component->getProperty(); prop->setParameterInt(prop->findParameter("int_parameter"), 5); ```
- **Auxiliary** - color conversion function.


Implementation of the Spinner's logic is given below:


<details>
<summary>Spinner.cpp | Close</summary>

`Spinner.cpp`


```cpp
#include "Spinner.h"
#include "Projectile.h"
#include <UnigineGame.h>
#include <UnigineEditor.h>

REGISTER_COMPONENT(Spinner);		// macro for component registration by the Component System

void Spinner::init()
{
	// get current material (from the first surface)
	ObjectPtr obj = checked_ptr_cast<Object>(node);

	if (obj && obj->getNumSurfaces())
		material = obj->getMaterialInherit(0);

	// init randoms
	time_to_spawn = Game::getRandomFloat(min_spawn_delay, max_spawn_delay);
	color_offset = Game::getRandomFloat(0, 360.0f);
	start_turn_speed = turn_speed;
}

void Spinner::update()
{
	// rotate spinner
	float ifps = Game::getIFps();
	turn_speed = turn_speed + acceleration * ifps;
	node->setRotation(node->getRotation() * quat(0, 0, turn_speed * ifps));

	// change color
	int id = material->findParameter("albedo_color");
	if (id != -1)
	{
		float hue = Math::mod(Game::getTime() * 60.0f + color_offset, 360.0f);
		material->setParameterFloat4(id, vec4(hsv2rgb(hue, 1, 1), 1.0f));
	}

	// spawn projectiles
	time_to_spawn -= ifps;
	if (time_to_spawn < 0 && spawn_node)
	{
		// reset timer and increase difficulty
		time_to_spawn = Game::getRandomFloat(min_spawn_delay, max_spawn_delay) / (turn_speed / start_turn_speed);

		// create node
		NodePtr spawned = spawn_node->clone();
		spawned->setEnabled(1);
		spawned->setWorldTransform(node->getWorldTransform());

		// don't destroy it on quitting the current scope
		// note: if you plan to add some components to this object
		// you have to use release() method and transfer ownership of this
		// object to the Editor

		// create component
		Projectile *proj_component = addComponent<Projectile>(spawned);

		// there are three ways to change variables inside another component:
		// 1) direct change via component (fast, easy)
		proj_component->speed = Game::getRandomFloat(proj_component->speed * 0.5f, proj_component->speed * 1.5f);

		// 2) change via property of the node (more slow, more awkward)
		for (int i = 0; i < spawned->getNumProperties(); i++)
		{
			PropertyPtr prop = spawned->getProperty(i);
			if (prop && (!strcmp(prop->getName(), "Projectile") || prop->isParent("Projectile")))
				prop->getParameterPtr("damage")->setValueInt(Game::getRandomInt(75, 100));
		}

		// 3) change via property of the component
		PropertyPtr proj_property = proj_component->getProperty();
		proj_property->getParameterPtr("lifetime")->setValueFloat(Game::getRandomFloat(5.0f, 10.0f));

		// call public method of another component
		proj_component->setMaterial(material);
	}
}

// color conversion H - [0, 360), S,V - [0, 1]
vec3 Spinner::hsv2rgb(float h, float s, float v)
{
	float p, q, t, fract;

	h /= 60.0f;
	fract = h - Math::floor(h);

	p = v * (1.0f - s);
	q = v * (1.0f - s * fract);
	t = v * (1.0f - s * (1.0f - fract));

	if (0.0f <= h && h < 1.0f) return vec3(v, t, p);
	else if (1.0f <= h && h < 2.0f) return vec3(q, v, p);
	else if (2.0f <= h && h < 3.0f) return vec3(p, v, t);
	else if (3.0f <= h && h < 4.0f) return vec3(p, q, v);
	else if (4.0f <= h && h < 5.0f) return vec3(t, p, v);
	else if (5.0f <= h && h < 6.0f) return vec3(v, p, q);
	else return vec3(0, 0, 0);
}

```

</details>


## 5. Register Components in the Component System


Now we have all our game logic implemented in the corresponding components: *Pawn, Spinner*, and *Projectile*. There is one more thing to be done before we can start using them. We should register our components in the Component System.


All components having the *[REGISTER_COMPONENT](#REGISTER_COMPONENT)* macro declared in their implementation files (`*.cpp`), are registered automatically by the Component System upon its initialization, just add a single line to the *[AppSystemLogic::init()](../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic_init)* method:


```cpp
#include <UnigineComponentSystem.h>

/* ... */

int AppSystemLogic::init()
{
	/* ... */

	// initialize ComponentSystem and register all components
	Unigine::ComponentSystem::get()->initialize();

	/* ... */
}

```


Voila! All our components are registered at once!


## 6. Add Components to Nodes


As we implemented our game logic in the components and registered them in the System, we can actually start using them. There are two ways to add a logic component to a node:


- By simply assigning the corresponding property to it [via UnigineEditor](../../../editor2/properties_settings/organizing_properties/index.md#assign_property) or code: ```cpp object1->addProperty("MyComponentProperty"); object2->setProperty(0, "MyComponentProperty"); ```
- By calling the corresponding method of the Component System: ```cpp ComponentSystem::get()->addComponent<MyComponent>(object); ```


Here is the resulting code for our game including registration of components as well as adding them to nodes:


<details>
<summary>game.cpp | Close</summary>

`game.cpp`


```cpp
#include <UnigineEngine.h>
#include <UnigineLights.h>
#include <UnigineWidgets.h>

#include <UnigineComponentSystem.h>
#include "Spinner.h"
#include "Projectile.h"
#include "Pawn.h"

using namespace Unigine;
using namespace Math;
//////////////////////////////////////////////////////////////////////////
// System logic class
//////////////////////////////////////////////////////////////////////////

class AppSystemLogic : public SystemLogic
{
public:
	AppSystemLogic() {}
	virtual ~AppSystemLogic() {}
	virtual int init()
	{
		// initialize ComponentSystem and register all components
		Unigine::ComponentSystem::get()->initialize();

		// run in background
		Engine::get()->setBackgroundUpdate(Engine::BACKGROUND_UPDATE_RENDER_NON_MINIMIZED);

		// load world
		World::loadWorld("cs");

		return 1;
	}
};

//////////////////////////////////////////////////////////////////////////
// World logic class
//////////////////////////////////////////////////////////////////////////

class AppWorldLogic : public WorldLogic
{
public:
	AppWorldLogic() {}
	virtual ~AppWorldLogic() {}
	virtual int init()
	{
		// create static camera
		player = PlayerDummy::create();

		player->setPosition(Vec3(17.0f));
		player->setDirection(vec3(-1.0f), vec3(0.0f, 0.0f, 1.0f));
		Game::setPlayer(player);

		// create light
		sun = LightWorld::create(vec4_one);

		sun->setName("Sun");
		sun->setWorldRotation(Math::quat(45.0f, 30.0f, 300.0f));

		// Note: objects are added to the world when created

		// create objects
		ObjectMeshDynamicPtr obj[4];
		obj[0] = create_box(translate(Vec3(-16.0f, 0.0f, 0.0f)), vec3(1.0f));
		obj[1] = create_box(translate(Vec3(16.0f, 0.0f, 0.0f)), vec3(1.0f));
		obj[2] = create_box(translate(Vec3(0.0f, -16.0f, 0.0f)), vec3(1.0f));
		obj[3] = create_box(translate(Vec3(0.0f, 16.0f, 0.0f)), vec3(1.0f));

		// there are two ways to create components on nodes:
		// 1) via component system
		ComponentSystem::get()->addComponent<Spinner>(obj[0]);
		ComponentSystem::get()->addComponent<Spinner>(obj[1]);

		// 2) via property
		obj[2]->addProperty("Spinner");
		obj[3]->setProperty(0, "Spinner");

		// set up spinners (set "spawn_node" variable)
		ObjectMeshDynamicPtr projectile_obj = create_box(Mat4_identity, vec3(0.15f));
		projectile_obj->setEnabled(0);
		for (int i = 0; i < 4; i++)
			ComponentSystem::get()->getComponent<Spinner>(obj[i])->spawn_node = projectile_obj;

		// create player
		ObjectMeshDynamicPtr my_pawn_object = create_box(translate(Vec3(1.0f, 1.0f, 0.0f)), vec3(1.3f, 1.3f, 0.3f));
		my_pawn = ComponentSystem::get()->addComponent<Pawn>(my_pawn_object);
		my_pawn->setDestroyCallback(MakeCallback(this, &AppWorldLogic::my_pawn_destroyed));
		time = 0;

		// create info label
		label = WidgetLabel::create(Gui::getCurrent());
		label->setPosition(10, 10);
		label->setFontSize(24);
		label->setFontOutline(1);
		Gui::getCurrent()->addChild(label, Gui::ALIGN_OVERLAP);

		return 1;
	}

	virtual int update()
	{
		// increase time while player is alive
		if (my_pawn)
			time += Game::getIFps();

		// show game info
		label->setText(String::format(
			"Player:\n"
			"Health Points: %d\n"
			"Time: %.1f sec\n"
			"\n"
			"Statisics:\n"
			"Components: %d",
			(my_pawn ? my_pawn->health.get() : 0),
			time,
			ComponentSystem::get()->getNumComponents()).get());

		return 1;
	}

private:
	Pawn* my_pawn{ nullptr };	// Pawn player
	float time = 0;
	WidgetLabelPtr label;
	PlayerDummyPtr player;
	LightWorldPtr sun;

	void my_pawn_destroyed()
	{
		my_pawn = nullptr;
	}
	// method creating a box
	ObjectMeshDynamicPtr create_box(const Mat4 &transform, const vec3 &size)
	{
		MeshPtr mesh = Mesh::create();
		mesh->addBoxSurface("box", size);

		ObjectMeshDynamicPtr object = ObjectMeshDynamic::create(1);
		object->setMesh(mesh);
		object->setWorldTransform(transform);

		return object;
	}
};

//////////////////////////////////////////////////////////////////////////
// Main
//////////////////////////////////////////////////////////////////////////

int main(int argc, char **argv)
{
	// init engine
	Unigine::Engine::InitParameters init_params;
	init_params.window_title = "UNIGINE Engine: Component System Usage Example (C++)";
	Unigine::EnginePtr engine(init_params, argc, argv);

	// enter main loop
	AppWorldLogic world_logic;
	AppSystemLogic system_logic;
	engine->main(&system_logic, &world_logic, NULL);

	return 0;
}


```

</details>
