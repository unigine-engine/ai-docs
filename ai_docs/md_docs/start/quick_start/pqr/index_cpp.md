# Programming Quick References (CPP)


## Introduction


In the next chapters you will find the basic information on how to start programming 3D applications and videogames with UNIGINE. This FAQ consists of the following chapters:


1. [Basic Scene Objects](#objects_basic)
2. [Coordinate System](#basis)
3. [Logging and Printing Messages to Console](#logging)
4. [Saving and Loading a World](#worlds)
5. [Closing the Application](#application)
6. [Creating and Deleting Nodes at Runtime](#creating_nodes)
7. [Creating and Setting Up a Camera](#camera)
8. [Creating and Setting up Light Sources](#light)
9. [Creating, Applying and Deleting Materials at Runtime](#materials)
10. [Managing Existing Scene Objects](#objects)
11. [Performing Basic Transformations (Move, Rotate, Scale)](#transformations)
12. [Making the Game Process Framerate-independent](#time)
13. [Managing Intersections](#intersection)
14. [Getting and Managing User Inputs](#inputs)
15. [Creating User Interface](#ui)
16. [Playing Sound and Music](#sound)
17. [Setting Up Physics](#physics)
18. [Catching Nodes with World Triggers](#world_triggers)


## Basic Scene Objects


In terms of UNIGINE, **node** is a basic type from which all types of scene objects are inherited. Some of them appear visually: [Objects](../../../objects/objects/index.md), [Decals](../../../objects/decals/index.md), and [Effects](../../../objects/effects/index.md). Objects have [surfaces](../../../start/index.md#surface) to represent their geometry (mesh). Others ([Light Sources](../../../objects/lights/index.md), [Players](../../../objects/players/index.md), etc.) are invisible.


Each node has a transformation matrix, which encodes position, rotation, and scale of the node in the world.


All scene objects added to the scene regardless of their type are called nodes.


### Additional information:


- For more information on UNIGINE node types, see [Built-in Node Types](../../../objects/index.md) section.
- For more information on managing nodes via API, see [Node-Related Classes](../../../api/library/nodes/index.md) section.


## Coordinate System


The 3D space in UNIGINE is represented by the right-handed Cartesian coordinate system: **X** and **Y** axes form a horizontal plane, **Z** axis points up. When [exporting](../../../editor2/assets_workflow/assets_create_import.md#export) an animation from 3D editors, **Y** is considered a forward direction.


![](coordinates.gif)

*Coordinate System*


Positive rotation angle sets the rotation counterclockwise. It corresponds to the right-hand rule: if you set right hand thumb along the axis, other fingers wrapped will show rotation direction.


![](coordinates_rotation.gif)

*Rotation Directions*


### Additional information:


1. For more information on UNIGINE node types, see [Built-in Node Types](../../../objects/index.md) section.
2. For more information on managing nodes via API, see [Node-Related Classes](../../../api/library/nodes/index.md) section.


## Logging and Printing Messages to Console


Printing messages to the log file and console helps to monitor overall progress of execution of your application and report errors which can be used in debugging. *[Log](../../../api/library/common/class.log_cpp.md)* class makes it possible to print formatted string messages to the log file and the console. The code below demonstrates how to print various types of messages:


> **Notice:** To enable displaying messages in the onscreen overlay use the following command: `console_onscreen 1`


```cpp
using namespace Unigine;

// auxiliary variables for messages
const char* file_name = "file.txt";
int ID = 10;

	// reporting an error message
	Log::error("Loading mesh: can't open \"%s\" file\n", file_name);

	// reporting a message
	Log::message("-> Added %d UI elements.\n", ID);

	// reporting a warning message
	Log::warning("ID of the \"%s\" file: %d.\n", file_name, ID);

	// reporting a fatal error message to the log file and closing the application (Windows only)
	Log::fatal("FATAL ERROR reading \"%s\" file!\n", file_name);


```


**Additional information:**


- For more information on the console, see *[Console](../../../code/console/index.md)* article.
- For more information on the *Log* class, see *[Log](../../../api/library/common/class.log_cpp.md)* class article.


## Saving and Loading a World


Some applications manage a single world, while other require several worlds to be managed. In any case, it is very useful to know how to save our current world and load some other. In order to solve this task, we should use the *[World](../../../api/library/engine/class.world_cpp.md)* class, which is designed as a singleton.


> **Notice:** In order to use the *[World](../../../api/library/engine/class.world_cpp.md)* class, include the `UnigineWorld.h` library.


```cpp
#include <UnigineWorld.h>

using namespace Unigine;
/* .. */

// loading world from the my_world.world file
World::loadWorld("my_world");

```


We can also do the same via the [console](../../../code/console/index.md) by using the *[Console](../../../api/library/engine/class.console_cpp.md)* class, which is also designed as a singleton.


> **Notice:** In order to use the *[Console](../../../api/library/engine/class.console_cpp.md)* class, include the `UnigineConsole.h` library.


```cpp
#include <UnigineConsole.h>

using namespace Unigine;
/* .. */

// saving current world to the my_world.world file
Console::run("world_save my_world");

// loading world from the my_world.world file
Console::run("world_load my_world");

```


**Additional information:**


- For more information on managing worlds via API, see the *[World](../../../api/library/engine/class.world_cpp.md)* class article.
- For more information on the console and available commands, see [Console](../../../code/console/index.md) article.
- For more information on managing the console via API, see *[Console](../../../api/library/engine/class.console_cpp.md)* class article.
- For more information on managing world nodes that are to be saved via API, see the methods of the *[Node](../../../api/library/nodes/class.node_cpp.md#setSaveToWorldEnabled_int_void)* class.


## Closing the Application


Any application needs to be closed at some moment. To close your application you should use the *[Engine](../../../api/library/engine/class.engine_cpp.md)* class.


To close the application the following code is to be used:


```cpp
using namespace Unigine;

/* .. */

// closing the application
Engine::get()->quit();

```


## Creating and Deleting Nodes at Runtime


Nodes can be created and deleted at runtime almost as easy as in the Editor. The basic set of actions is as follows:


- **Creation**. To create a node we should declare a smart pointer for the type of the node we are going to create and call a constructor of the corresponding class providing construction parameters if necessary.
- **Deletion**. To delete a node we simply call the *[deleteLater()](../../../api/library/common/class.ptr_cpp.md#deleteLater_void)* method for the node we are going to remove.


```cpp
// creating a node of the NodeType named nodename
<NodeType>Ptr nodename = <NodeType>::create(<construction_parameters>);

// removing the node
nodename.deleteLater();

```


Now let us illustrate the process of creating and deleting a node using a simple static mesh (*[ObjectMeshStatic](../../../objects/objects/mesh/index.md)*) by loading a mesh from an asset as an example.


```cpp
int AppWorldLogic::init()
{

	//create an ObjectMeshStatic node from an fbx model imported to the data/fbx/ folder using the Editor
	ObjectMeshStaticPtr my_object = ObjectMeshStatic::create("fbx/model.fbx/model.mesh");

	// removing the node
	my_object.deleteLater();

	return 1;
}


```


**Additional information:**


- You can create primitives via code using the *[Primitives](../../../api/library/rendering/class.primitives_cpp.md)* class.
- For more information on managing world nodes, see the methods of the *[Node](../../../api/library/nodes/class.node_cpp.md)* class.


## Creating and Setting Up a Camera


A **camera** is a viewport to the world, without it you actually won't be able to see anything. Cameras in UNIGINE are managed using *[players](../../../objects/players/index.md)*. When you add a new player, it creates a [camera](../../../api/library/rendering/class.camera_cpp.md) and specifies controls, [masks](../../../api/library/players/class.player_cpp.md#player_masks), postprocess materials for this camera.


In order to set a new player as active one we should use the *[Game](../../../api/library/engine/class.game_cpp.md)* class which is designed as a singleton.


> **Notice:** In order to use the *[Game](../../../api/library/engine/class.game_cpp.md)* class and *[PlayerSpectator](../../../api/library/engine/class.game_cpp.md)* class we must include the `UnigineGame.h` and the `UniginePlayers.h` libraries.


The following code illustrates creation of a [PlayerSpectator](../../../objects/players/spectator/index.md) and setting it as the active game camera.


> **Notice:** By default the player uses a standard set of controls which can be overridden if necessary.


```cpp
#include <UnigineGame.h>
using namespace Unigine;

/* ... */

int AppWorldLogic::init()
{
	// creating a new PlayerSpectator instance
	PlayerSpectatorPtr playerSpectator = PlayerSpectator::create();

	// setting necessary parameters: FOV, ZNear, ZFar, view direction vector and position.
	playerSpectator->setFov(90.0f);
	playerSpectator->setZNear(0.1f);
	playerSpectator->setZFar(10000.0f);
	playerSpectator->setViewDirection(Math::vec3(0.0f, 1.0f, 0.0f));
	playerSpectator->setWorldPosition(Math::Vec3(-1.6f, -1.7f, 1.7f));

	// setting the player as a default one via the Game singleton instance
	Game::setPlayer(playerSpectator);

	return 1;
}

```


**Additional information:**


- For more information on players, see the [Players](../../../objects/players/index.md) article.
- For more information on players API, see the [Players-Related Classes](../../../api/library/players/index.md) article.
- For more information on the Game class, see the *[Game](../../../api/library/engine/class.game_cpp.md)* class article.


## Creating and Setting up Light Sources


**Lighting** is the basis of every scene defining colors and final look of your objects. Lights in UNIGINE are created the same way as all nodes.


Let us consider creation of a world light source as an example:


```cpp
#include <UnigineLights.h>
using namespace Unigine;

int AppWorldLogic::init()
{
	// creating a world light source and setting its color to white
	LightWorldPtr sun = LightWorld::create(Math::vec4(1.0f, 1.0f, 1.0f, 1.0f));

	// setting light source's parameters (intensity, disable angle, scattering type, name and rotation)
	sun->setName("Sun");
	sun->setDisableAngle(90.0f);
	sun->setIntensity(1.0f);
	sun->setScattering(LightWorld::SCATTERING::SCATTERING_SUN);
	sun->setWorldRotation(Math::quat(86.0f, 30.0f, 300.0f));

	return 1;
}

```


**Additional information:**


- For more information on light sources, see the [Light sources](../../../objects/lights/index.md) article.
- For more information on light sources API, see the [Lights-Related Classes](../../../api/library/lights/index.md) article.


## Creating, Applying and Deleting Materials at Runtime


**Materials** assigned to particular surfaces of a node determine how the node is to be rendered. They implement the [shaders](../../../principles/world_structure/index.md#material_shaders) and control what [options](../../../principles/world_structure/index.md#material_options), [states](../../../principles/world_structure/index.md#material_states), [parameters](../../../principles/world_structure/index.md#material_parameters) of different types and [textures](../../../principles/world_structure/index.md#material_textures) are used to render the node during the [rendering passes](../../../principles/render/sequence/index.md). To manage materials we use the following two classes:


- *[Materials](../../../api/library/rendering/class.materials_cpp.md)* class which represents an interface for managing loaded materials.
- *[Material](../../../api/library/rendering/class.materials_cpp.md)* class which is used to manage each individual material.


> **Notice:** In order to use materials we must include the `UnigineMaterials.h` library


The following code can be used to create a new material inherited from the *[mesh_base](../../../content/materials/library/mesh_base/index.md)* material.


```cpp
#include <UnigineMaterials.h>
#include <UnigineObjects.h>
using namespace Unigine;

/* .. */

int AppWorldLogic::init()
{

	// creating a box (ObjectMeshDynamic node)
	MeshPtr mesh = Mesh::create();
	mesh->addBoxSurface("box_surface", Math::vec3(1.5f, 1.5f, 1.5f));
	ObjectMeshDynamicPtr my_mesh = ObjectMeshDynamic::create(mesh);

	// getting the base mesh_base material to inherit from
	MaterialPtr mesh_base = Materials::findManualMaterial("Unigine::mesh_base");

	// inherit a new child material from it
	MaterialPtr my_mesh_base = mesh_base->inherit();

	// save it to  "materials/my_mesh_base0.mat"
	my_mesh_base->createMaterialFile("materials/my_mesh_base0.mat");

	// setting the albedo color of the material to red
	my_mesh_base->setParameterFloat4("albedo_color", Math::vec4(255, 0, 0, 255));

	// assigning a "my_mesh_base0.mat" material to the surface 0 of the my_mesh ObjectMeshDynamic node
	my_mesh->setMaterialPath("materials/my_mesh_base0.mat", 0);

	// assigning a "my_mesh_base0.mat" material to all surfaces of the my_mesh ObjectMeshDynamic node
	my_mesh->setMaterialPath("materials/my_mesh_base0.mat", "*");

}

int AppWorldLogic::shutdown()
{
	// deleting the material "materials/my_mesh_base0.mat"
	Materials::removeMaterial(Materials::findMaterialByPath("materials/my_mesh_base0.mat")->getGUID());

	return 1;
}

```


**Additional information:**


- For more information on creating and editing materials via API, see the *[Material](../../../api/library/rendering/class.material_cpp.md)* class article.
- For more information on managing loaded materials via API, see the *[Materials](../../../api/library/rendering/class.materials_cpp.md)* class article.
- For more information on materials files formats, see the [Materials Files](../../../code/formats/materials_formats/index.md) section.
- For more information on materials parameters, see the materials files in the `%UNIGINE_SDK_BROWSER_INSTALLATION_FOLDER%/sdks/%CURRENT_SDK%/data/core/materials/default/` folder.


## Managing Existing Scene Objects


Not all content in the world is created at runtime, so we should be able to operate with nodes that already exist. How do we get pointers to existing objects in order to manage them? This is where the *[World](../../../api/library/engine/class.world_cpp.md)* class comes into play again. Basically, there are two ways we can get a pointer to a certain node using the methods of the *World* class:


- *[getNodeByName()](../../../api/library/engine/class.world_cpp.md#getNodeByName_cstr_Node)* method - when we know node's name
- *[getNodeByID()](../../../api/library/engine/class.world_cpp.md#getNodeByID_int_Node)* method - when we know the node's ID


> **Notice:** In order to be able to use the methods of the *World* class we must include the `UnigineWorld.h` library.


These methods return a *NodePtr* value, which is a pointer to the base class, but in order to perform operations with a certain object (e.g.  *ObjectMeshDynamicPtr*) we need to perform **downcasting** (i.e. convert from a pointer-to-base to a pointer-to-derived).


Sometimes you may also need to perform **upcasting** (i.e. convert from a pointer-to-derived to a pointer-to-base), in this case you can use the derived class itself. The code below demonstrates the points described above.


```cpp
#include <UnigineWorld.h>
using namespace Unigine;
/* .. */

// find a pointer to node by a given name
NodePtr baseptr = World::getNodeByName("my_meshdynamic");

// cast a pointer-to-derived from pointer-to-base with automatic type checking
ObjectMeshDynamicPtr derivedptr = checked_ptr_cast<ObjectMeshDynamic>(baseptr);

// static cast (pointer-to-derived from pointer-to-base)
ObjectMeshDynamicPtr derivedptr = static_ptr_cast<ObjectMeshDynamic>(World::getNodeByName("my_meshdynamic"));

// upcast to the pointer to the Object class which is a base class for ObjectMeshDynamic
ObjectPtr object = derivedptr;

// upcast to the pointer to the Node class which is a base class for all scene objects
NodePtr node = derivedptr;

```


There are the following ways to get a component from a node:


```cpp
// get the component assigned to a node by type "MyComponent"
MyComponent* my_component = ComponentBase::getComponent<MyComponent>(node);

// // do the same by using the function of the Component System
MyComponent* my_component = ComponentSystem::get()->getComponent<MyComponent>(color_zone);

```


**Additional information:**


- For more information on working managing smart pointers, see the [Working with Smart Pointers](../../../code/fundamentals/smartpointers.md) article.
- For more information see the *[World](../../../api/library/engine/class.world_cpp.md)* class article.


## Performing Basic Transformations (Move, Rotate, Scale)


Every node has a transformation matrix, which encodes position, rotation, and scale of the node in the world. If a node is added as a child of another node, it has a transformation matrix that is related to its parent node. That is why the *[Node](../../../api/library/nodes/class.node_cpp.md)* class has different functions: *[getTransform()](../../../api/library/nodes/class.node_cpp.md#getTransform_Mat4), [setTransform()](../../../api/library/nodes/class.node_cpp.md#setTransform_Mat4_void)* and *[getWorldTransform()](../../../api/library/nodes/class.node_cpp.md#getWorldTransform_Mat4), [setWorldTransform()](../../../api/library/nodes/class.node_cpp.md#setWorldTransform_Mat4_void)* that operate with local and world transformation matrices respectively. The following code illustrates how to perform basic node transformations:


```cpp
// injecting Unigine namespace to the global namespace
using namespace Unigine;
using namespace Unigine::Math;

// move the node by X, Y, Z units along the corresponding axes
node->setWorldPosition(node->getWorldPosition() + Vec3(X, Y, Z));

// move the node by one unit along the Y axis
node->worldTranslate(0.0f, 1.0f, 0.0f);

// rotate the node around the axis (X, Y, Z) by the Alpha angle
node->setWorldRotation(node->getWorldRotation() * quat(Vec3(X, Y, Z), Alpha));

// rotate the node around X, Y, and Z axes by the corresponding angle (angle_X, angle_Y, angle_Z)
node->setWorldRotation(node->getWorldRotation() * quat(angle_X, angle_Y, angle_Z));

// rotate the node by 45 degrees along the Z axis
node->worldRotate(0.0f, 0.0f, 45.0f);

// orient the node using a direction vector and a vector pointing upwards
node->setWorldDirection(vec3(0.5f, 0.5f, 0.0f), vec3_up, AXIS_Y);

// setting node scale to Scale_X, Scale_Y, Scale_Z along the corresponding axes
node->setWorldScale(vec3(Scale_X, Scale_Y, Scale_Z));

// setting new transformation matrix to scale the node 2 times along all axes, rotate it by 45 degrees around the Z-axis and move it by 1 unit along all axes
Mat4 transform = Mat4(translate(vec3(1.0f, 1.0f, 1.0f)) * rotate(quat(0.0f, 0.0f, 1.0f, 45.0f)) * scale(vec3(2.0f)));

// setting node transformation matrix relative to its parent
node->setTransform(transform);

// setting node transformation matrix relative to the world origin
node->setWorldTransform(transform);

```


**Additional information:**


- For more information on matrix transformations, see the [Matrix Transformations](../../../code/fundamentals/matrix_transformations/index_cpp.md) article.


## Making the Game Process Framerate-independent


As the frame rate of our application may vary (i.e. the *[AppWorldLogic::update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* method will be called more or less frequently) depending on hardware, we should do something to ensure that certain actions are performed at the same time periods regardless of the frame rate (e.g. change something once per second etc). To make your game frame rate independent you can use a scaling multiplier (the time in seconds it took to complete the last frame) returned by the following methods:


- *[Engine::getIfps()](../../../api/library/engine/class.engine_cpp.md#getIFps_float)* returns the inverse FPS value for your application.
- *[Game::getIfps()](../../../api/library/engine/class.game_cpp.md#getIFps_float)* returns the scaled inverse FPS value. This class is to be used when you want to speed up, slow down or pause rendering, physics or game logic.


To change the transformations you can use the following code:


```cpp
// AppWorldLogic.cpp
#include <UnigineGame.h>

// injecting Unigine namespace to the global namespace
using namespace Unigine;

/* .. */

int AppWorldLogic::update() {

	// getting an inverse FPS value (the time in seconds it took to complete the last frame)
	float ifps = Game::getIFps();

	// moving the node up by 0.3 units every second instead of every frame
	node->worldTranslate(Math::Vec3(0.0f, 0.0f, 0.3f * ifps));

	return 1;
}
/* .. */

```


To perform some changes once in a certain period of time you can use the following code:


```cpp
#include <UnigineGame.h>

// injecting Unigine namespace to the global namespace
using namespace Unigine;
// AppWorldLogic.cpp

	const float INTERVAL_DURATION = 5;		// interval duration
	float elapsed_time = INTERVAL_DURATION;	// current time left to make changes

/* .. */

int AppWorldLogic::update() {

	// getting an inverse FPS value (the time in seconds it took to complete the last frame)
	float ifps = Game::getIFps();

	// checking if it's time to make changes
	if (elapsed_time < 0.0f)
	{

		/* .. DO SOME CHANGES .. */

		// resetting elapsed time counter
		elapsed_time = INTERVAL_DURATION;
	}

	// decreasing elapsed time counter
	elapsed_time -= ifps;

	return 1;
}
/* .. */


```


**Additional information:**


- For more information on the *Game* class, see the *[Game](../../../api/library/engine/class.game_cpp.md)* class article.
- For more information on the *Engine* class, see the *[Engine](../../../api/library/engine/class.engine_cpp.md)* class article.


## Managing Intersections


**Intersections** are widely used in 3D applications. In UNIGINE there are three main types of intersections:


- **World intersection** - an intersection with [objects](../../../api/library/objects/class.object_cpp.md) and [nodes](../../../api/library/nodes/class.node_cpp.md).
- **Physics intersection** - an intersection with [shapes](../../../api/library/physics/class.shape_cpp.md) and [collision objects](../../../principles/physics/collision/index.md).
- **Game intersection** - an intersection with pathfinding nodes like [obstacles](../../../api/library/pathfinding/class.obstacle_cpp.md).


But there are some conditions to detect intersections with the surface:


1. The surface is enabled.
2. The surface has a material assigned.
3. Per-surface Intersection flag is enabled. > **Notice:** You can set this flag to the object's surface by using the *[Object.setIntersection()](../../../api/library/objects/class.object_cpp.md#setIntersection_int_int_void)* function.


The code below illustrates several ways of using world intersections:


- to find all nodes intersected by a bounding box
- to find all nodes intersected by a bounding sphere
- to find all nodes intersected by a bounding frustum
- to find the first object intersected by a ray


```cpp
#include <UnigineGame.h>

#include <UnigineWorld.h>

// injecting Unigine namespace to the global namespace
using namespace Unigine;

int listNodes(Vector<Ptr<Node>>& nodes, const char* intersection_with)
{
	Log::message("Total number of nodes intersecting a %s is: %i \n", intersection_with, nodes.size());

	for (int i = 0; i < nodes.size(); i++)
	{
		Log::message("Intersected node: %s \n", nodes.get(i)->getName());
	}

	// clearing the list of nodes
	nodes.clear();

	return 1;
}

int AppWorldLogic::update()
{

	// getting a player pointer
	PlayerPtr player = Game::getPlayer();

	// creating a vector to store intersected nodes
	Vector<Ptr<Node>> nodes;

	//-------------------------- FINDING INTERSECTIONS WITH A BOUNDING BOX -------------------------

	// initializing a bounding box with a size of 3 units, located at the World's origin
	WorldBoundBox boundBox(Math::Vec3(0.0f), Math::Vec3(3.0f));

	// finding nodes intersecting a bounding box and listing them if any
	if (World::getIntersection(boundBox, nodes))
		listNodes(nodes, "bounding box");

	//------------------------- FINDING INTERSECTIONS WITH A BOUNDING SPHERE ------------------------

	// initializing a bounding sphere with a radius of 3 units, located at the World's origin
	WorldBoundSphere boundSphere(Math::Vec3(0.0f), 3.0f);

	// finding nodes intersecting a bounding sphere and listing them if any
	if (World::getIntersection(boundSphere, nodes))
		listNodes(nodes, "bounding sphere");

	//------------------------- FINDING INTERSECTIONS WITH A BOUNDING FRUSTUM -----------------------

	// initializing a bounding frustum with a  frustum of the player's camera
	WorldBoundFrustum boundFrustum(player->getCamera()->getProjection(), player->getCamera()->getModelview());

	// finding ObjectMeshStaticNodes intersecting a bounding frustum and listing them if any
	if (World::getIntersection(boundFrustum, Node::OBJECT_MESH_STATIC, nodes))
		listNodes(nodes, "bounding frustum");

	//---------------- FINDING THE FIRST OBJECT INTERSECTED BY A RAY CAST FROM P0 to P1 --------------

	// initializing points of the ray from player's position in the direction pointed by the mouse cursor
	Math::ivec2 mouse = Input::getMousePosition();
	Math::Vec3 p0 = player->getWorldPosition();
	Math::Vec3 p1 = p0 + Math::Vec3(player->getDirectionFromMainWindow(mouse.x, mouse.y)) * 100;

	//creating a WorldIntersection object to store the information about the intersection
	WorldIntersectionPtr intersection = WorldIntersection::create();

	// casting a ray from p0 to p1 to find the first intersected object
	ObjectPtr obj = World::getIntersection(p0, p1, 1, intersection);

	// print the name of the first intersected object and coordinates of intersection point if any
	if (obj)
	{
		Math::Vec3 p = intersection->getPoint();
		Log::message("The first object intersected by the ray at point (%f, %f, %f) is: %s \n ", p.x, p.y, p.z, obj->getName());
	}

	return 1;
}


```


**Additional information:**


- For more information on intersections, see the [Intersections](../../../code/usage/intersections/index_cpp.md) article.
- For more information on managing *World* intersections via API, see the *[World](../../../api/library/engine/class.world_cpp.md#getIntersection_Vec3_Vec3_int_Object)* class article.
- For more information on managing *Game* intersections via API, see the *[Game](../../../api/library/engine/class.game_cpp.md#getIntersection_Vec3_Vec3_float_int_VECNode_Vec3_Obstacle)* class article.
- For more information on managing *Physics* intersections via API, see the *[Physics](../../../api/library/physics/class.physics_cpp.md#getIntersection_Vec3_Vec3_int_VECNode_PhysicsIntersection_Object)* class article.


## Getting and Managing User Inputs


The majority of applications are designed to interact with the user. In UNIGINE you can manage user inputs using the following classes:


- [Input class](../../../api/library/controls/class.input_cpp.md)
- [Controls class](../../../api/library/controls/class.controls_cpp.md)
- [ControlsApp class](../../../api/library/controls/class.controlsapp_cpp.md)


The following code illustrates how to use **Input** class to get mouse coordinates in case if a right mouse button was clicked and to close the application if "q" key was pressed (ignoring this key if the console is opened):


```cpp
#include <UnigineInput.h>

#include <UnigineConsole.h>

int AppWorldLogic::update()
{

	// if right mouse button is clicked
	if (Input::isMouseButtonDown(Input::MOUSE_BUTTON_RIGHT))
	{
		Math::ivec2 mouse = Input::getMousePosition();
		// report mouse cursor coordinates to the console
		Log::message("Right mouse button was clicked at (%d, %d)\n", mouse.x, mouse.y);
	}

	// closing the application if a 'Q' key is pressed, ignoring the key if the console is opened
	if (Input::isKeyDown(Input::KEY_Q) && !Console::isActive())
	{
		Engine::get()->quit();
	}

	return 1;
}


```


The following code illustrates how to use **Controls** class to handle keyboard input:


```cpp
#include <UnigineGame.h>

int AppWorldLogic::update()
{

	// getting current controls
	ControlsPtr controls = Game::getPlayer()->getControls();

	// checking controls states and reporting which buttons were pressed
	if (controls->clearState(Controls::STATE_FORWARD) || controls->clearState(Controls::STATE_TURN_UP))
	{
		Log::message("FORWARD or UP key pressed\n");
	}
	else if (controls->clearState(Controls::STATE_BACKWARD) || controls->clearState(Controls::STATE_TURN_DOWN))
	{
		Log::message("BACKWARD or DOWN key pressed\n");
	}
	else if (controls->clearState(Controls::STATE_MOVE_LEFT) || controls->clearState(Controls::STATE_TURN_LEFT))
	{
		Log::message("MOVE_LEFT or TURN_LEFT key pressed\n");
	}
	else if (controls->clearState(Controls::STATE_MOVE_RIGHT) || controls->clearState(Controls::STATE_TURN_RIGHT))
	{
		Log::message("MOVE_RIGHT or TURN_RIGHT key pressed\n");
	}

	return 1;
}


```


The following code illustrates how to use **ControlsApp** class to map keys and buttons to states and then to handle user input:


```cpp
#include <UnigineGame.h>

int AppWorldLogic::init()
{

	// remapping states to other keys and buttons
	ControlsApp::setStateKey(Controls::STATE_FORWARD, Input::KEY_PGUP);
	ControlsApp::setStateKey(Controls::STATE_BACKWARD, Input::KEY_PGDOWN);
	ControlsApp::setStateKey(Controls::STATE_MOVE_LEFT, Input::KEY_L);
	ControlsApp::setStateKey(Controls::STATE_MOVE_RIGHT, Input::KEY_R);
	ControlsApp::setStateMouseButton(Controls::STATE_JUMP, Input::MOUSE_BUTTON_LEFT);

	return 1;
}

int AppWorldLogic::update()
{

	if (ControlsApp::clearState(Controls::STATE_FORWARD))
	{
		Log::message("FORWARD key pressed\n");
	}
	else if (ControlsApp::clearState(Controls::STATE_BACKWARD))
	{
		Log::message("BACKWARD key pressed\n");
	}
	else if (ControlsApp::clearState(Controls::STATE_MOVE_LEFT))
	{
		Log::message("MOVE_LEFT key pressed\n");
	}
	else if (ControlsApp::clearState(Controls::STATE_MOVE_RIGHT))
	{
		Log::message("MOVE_RIGHT key pressed\n");
	}
	else if (ControlsApp::clearState(Controls::STATE_JUMP))
	{
		Log::message("JUMP button pressed\n");
	}

	return 1;
}


```


**Additional information:**


- For more information on managing user inputs using *Input* class, see the *[Input class](../../../api/library/controls/class.input_cpp.md)* article.
- For more information on managing user inputs using *Controls* class, see the *[Controls class](../../../api/library/controls/class.controls_cpp.md)* article.
- For more information on managing user inputs using *ControlsApp* class, see the *[ControlsApp class](../../../api/library/controls/class.controlsapp_cpp.md)* article.


## Creating User Interface


In UNIGINE a **Graphical User Interface** (GUI) is composed of different types of [widgets](../../../api/library/gui/index.md) added to it. Basically, there are two ways of creating GUI:


- By adding widgets to the system GUI (Unigine user interface) that is rendered on top of application window.
- By adding widgets to a [GUI object](../../../objects/objects/gui/gui_object.md) positioned in the world. In this case, any postprocessing filter can be applied.


To add elements to the system GUI you should use the *[Gui](../../../api/library/gui/class.gui_cpp.md)* class.


> **Notice:** In order to use GUI widgets we must include the `UnigineUserInterface.h` library.


There are 2 ways to create the GUI layout:


- Directly from the code via [GUI-related classes](../../../api/library/gui/index.md)
- By using [User interface](../../../code/gui/ui/index.md) (UI) files


The following code demonstrates how to add a label and a slider to the system GUI:


```cpp
#include <UnigineUserInterface.h>

// injecting Unigine namespace to the global namespace
using namespace Unigine;

GuiPtr gui;

int AppWorldLogic::init()
{

	// getting a GUI pointer
	gui = Gui::getCurrent();

	// creating a label widget and setting up its parameters
	WidgetLabelPtr widget_label = WidgetLabel::create(gui, "Label text:");
	widget_label->setToolTip("This is my label!");
	widget_label->arrange();
	widget_label->setPosition(10, 10);

	// creating a slider widget and setting up its parameters
	WidgetSliderPtr widget_slider = WidgetSlider::create(gui, 0, 360, 90);
	widget_slider->setToolTip("This is my slider!");
	widget_slider->arrange();
	widget_slider->setPosition(100, 10);

	gui->addChild(widget_label, Gui::ALIGN_OVERLAP | Gui::ALIGN_FIXED);
	gui->addChild(widget_slider, Gui::ALIGN_OVERLAP | Gui::ALIGN_FIXED);

	return 1;
}


```


In order to use GUI elements we must specify handlers for various events (click, change, etc.). The following code demonstrates how to set event handlers:


```cpp
#include <UnigineUserInterface.h>

// injecting Unigine namespace to the global namespace
using namespace Unigine;

GuiPtr gui;

// EventConnections class instance to manage event subscriptions
EventConnections econnections;

/// function to be called when button1 is clicked
int onButton1Clicked(const WidgetPtr &button)
{
	/* .. */
}

/// method to be called when button2 is clicked
int AppWorldLogic::onButton2Clicked(const WidgetPtr &button)
{
	/* .. */
}

/// method to be called when delete button is clicked
int AppWorldLogic::onButtonDelClicked(const WidgetPtr &button)
{
	/* .. */
}

/// method to be called when slider position is changed
int AppWorldLogic::onSliderChanged(const WidgetPtr &slider)
{
	/* .. */
}

int AppWorldLogic::init()
{

	/* .. */

	// getting a GUI pointer
	gui = Gui::getCurrent();

	// subscbribing for the clicked event with the onButton1Clicked function as a handler
	buttonwidget1->getEventClicked().connect(econnections, onButton1Clicked);

	// subscbribing for the clicked event with the onButton2Clicked function as a handler
	buttonwidget2->getEventClicked().connect(econnections, this, &AppWorldLogic::onButton2Clicked);

	buttonwidget1->getEventClicked().connect(econnections, this, &AppWorldLogic::onButtonDelClicked);

	// setting AppWorldLogic::onSliderChanged method as a changed event handler for a widget_slider
	widget_slider->getEventChanged().connect(econnections, this, &AppWorldLogic::onSliderChanged);
	/* .. */

	return 1;
}

int AppWorldLogic::shutdown()
{

	// removing all event subscriptions somewhere on shutdown
	econnections.disconnectAll();

	return 1;
}


```


**Additional information:**


- For more information on UI files, see the [UI files](../../../code/gui/ui/index.md) article.
- For more information on GUI-related API, see the *[GUI-related classes](../../../api/library/gui/index.md)* section.
- For more information on the *Gui* class, see the *[Gui class](../../../api/library/gui/class.gui_cpp.md)* article.
- For more information on handling events, see the [Events Handling](../../../code/fundamentals/events/index_cpp.md) article.


## Playing Sound and Music


### Sound Source


The *[SoundSource](../../../api/library/sounds/class.soundsource_cpp.md)* class is used to create directional [sound sources](../../../objects/sounds/sound_source.md). To create a sound source, create an instance of the *SoundSource* class and specify all required settings:


```cpp
// create a new sound source using the given sound sample file
SoundSourcePtr sound = SoundSource::create("sound.mp3");

// disable sound muffling when being occluded
sound->setOcclusion(0);
// set the distance at which the sound gets clear
sound->setMinDistance(10.0f);
// set the distance at which the sound becomes out of audible range
sound->setMaxDistance(100.0f);
// set the gain that result in attenuation of 6 dB
sound->setGain(0.5f);
// loop the sound
sound->setLoop(1);
// start playing the sound sample
sound->play();


```


### Ambient Source


To play ambient background music create an instance of the *[AmbientSource](../../../api/library/sounds/class.ambientsource_cpp.md)* class, specify all required parameters and enable it. Make sure to import the sound asset to the project.


> **Notice:** For an ambient source to be played, a [player](../../../api/library/players/index.md) is always required. In case an ambient source needs to be played when neither a world, nor the editor are loaded, a player, as well as the sound source (see code below), should be created in the *[SystemLogic.Init()](../../../api/library/common/logic/class.systemlogic_cpp.md#init_int)* method; otherwise, no sound will be heard.


```cpp
// create a player so that an ambient sound source is played
PlayerSpectatorPtr player = PlayerSpectator::create();
player->setPosition(Vec3(0.0f, -3.401f, 1.5f));
player->setViewDirection(vec3(0.0f, 1.0f, -0.4f));
Game::setPlayer(player);

// create the ambient sound source
AmbientSourcePtr sound = AmbientSource::create("sound.mp3");

// set necessary sound settings
sound->setGain(0.5f);
sound->setPitch(1.0f);
sound->setLoop(1);
sound->play();


```


**Additional information:**


- For more information on directional sound, see the *[SoundSource](../../../api/library/sounds/class.soundsource_cpp.md)* class article.
- For more information on ambient sound, see the *[AmbientSource](../../../api/library/sounds/class.ambientsource_cpp.md)* class article.


## Setting Up Physics


An [object](../../../objects/objects/index.md) should have a [body](../../../principles/physics/bodies/index.md) and a [shape](../../../principles/physics/shapes/index.md) to be affected by gravity and to collide with other physical objects:


```cpp
// cube
ObjectMeshStaticPtr box = ObjectMeshStatic::create("core/meshes/box.mesh");

// create a body and a shape based on the mesh
BodyRigidPtr bodyBox = BodyRigid::create(box);
ShapeBoxPtr shapeBox = ShapeBox::create(bodyBox, Math::vec3(1.0f));


```


## Catching Nodes with World Triggers


A *[World trigger](../../../api/library/worlds/class.worldtrigger_cpp.md)* triggers events when any nodes (colliders or not) get inside or outside of them. The trigger can detect a node of any type by its bounding box. The trigger reacts to all nodes (default behavior).


**World Triggers** detect only the nodes with *Triggers Interaction* enabled - either in the Editor or via API using *[setTriggerInteractionEnabled()](../../../api/library/nodes/class.node_cpp.md#setTriggerInteractionEnabled_int_void)*.


![](triggers_interaction.png)


The handler function of *World Trigger* is actually executed only when the next engine function is called: that is, before *[updatePhysics()](../../../code/fundamentals/execution_sequence/main_loop.md#physics_updatePhysics)* (in the current frame) or before *[update()](../../../code/fundamentals/execution_sequence/main_loop.md#world_update)* (in the next frame) - whatever comes first.


> **Notice:** If you have moved some nodes and want to execute handler functions based on changed positions in the same frame, you need to call *[updateSpatial()](../../../api/library/engine/class.world_cpp.md#updateSpatial_void)* first.


You can subscribe for *[Enter](../../../api/library/worlds/class.worldtrigger_cpp.md#getEventEnter_Event)* and *[Leave](../../../api/library/worlds/class.worldtrigger_cpp.md#getEventLeave_Event)* events with handler functions to be executed when a node enters or leaves the *World Trigger*. A handler function must receive a [Node](../../../api/library/nodes/class.node_cpp.md) as its first argument.


```cpp
// EventConnections class instance to manage event subscriptions
EventConnections econnections;

// implement the enter event handler
void AppWorldLogic::enter_event_handler(const NodePtr &node)
{
	Log::message("\nA node named %s has entered the trigger\n", node->getName());
}

// implement the leave event handler
void AppWorldLogic::leave_event_handler(const NodePtr &node)
{
	Log::message("\nA node named %s has left the trigger\n", node->getName());
}

WorldTriggerPtr trigger;

int AppWorldLogic::init()
{

	// create a world trigger node
	trigger = WorldTrigger::create(Math::vec3(3.0f));

	// add the enter event handler to be executed when a node enters the world trigger
	trigger->getEventEnter().connect(econnections, this, &AppWorldLogic::enter_event_handler);

	// add the leave event handler to be executed when a node leaves the world trigger
	trigger->getEventLeave().connect(econnections, this, &AppWorldLogic::leave_event_handler);

	return 1;
}

int AppWorldLogic::shutdown()
{

	// removing all event subscriptions somewhere on shutdown
	econnections.disconnectAll();

	return 1;
}


```
