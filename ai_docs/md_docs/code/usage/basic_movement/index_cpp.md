# Basic Object Movements (CPP)


After adding an object to UNIGINE, you can control its transformations with your control devices. This article shows how to control basic object movements and combine different transformations.


### See Also


- Article on [Matrix Transformations](../../../code/fundamentals/matrix_transformations/index_cpp.md)
- Article on *[mat4](../../../code/uniginescript/language/data_types.md#mat4)* and *[dmat4](../../../code/uniginescript/language/data_types.md#dmat4)* UNIGINE data types


## Direction Vector


The direction vector is an important concept of mesh transformation. To move the node forward, you should know where the forward direction of the mesh is. When the mesh is exported from a 3D editor, it saves the information about the forward direction. And when you add the mesh to UNIGINE, it has the same orientation it had in a 3D editor.


| ![](direction_maya.png) | ![](direction_unigine.png) |
|---|---|
| *A mesh in Maya* | *The same mesh in UNIGINE* |


In the images above, the direction vector has the positive Y direction. To move this mesh forward, you should get the direction of the mesh by using the Y component (the second column) of the world transformation matrix of the mesh.


The point is that content creators and programmers should make an arrangement for the direction vector.


## Basic Movements


### Prearrangement


We are going to make a component that allows moving and rotating an object. To make the explanation unobstructed, we give supplementary parts of code and additional links here. The complete code is provided at the [bottom of this article](#combining).


To use the [component system](../../../principles/component_system/component_system_cpp/index.md), we need to initialize it. This is done in `AppSystemLogic.cpp` as follows:


```cpp
#include "AppSystemLogic.h"

int AppSystemLogic::init()
{
	Unigine::ComponentSystem::get()->initialize();
	return 1;
}


```


We need the camera to observe the scene and an object that we are going to manipulate. We define these two nodes in `AppWorldLogic.h` and add all related logic in `AppWorldLogic.cpp`:


```cpp
#include <UnigineLogic.h>
#include <UnigineStreams.h>
#include <UnigineObjects.h>
#include <UniginePlayers.h>

using namespace Unigine;

class AppWorldLogic : public Unigine::WorldLogic
{

public:
	AppWorldLogic();
	virtual ~AppWorldLogic();

	int init() override;

	int update() override;
	int postUpdate() override;
	int updatePhysics() override;

	int shutdown() override;

private:
	// define the ObjectMeshStatic instance
	// so that it will be deleted with the AppWorldLogic instance
	Unigine::ObjectMeshStaticPtr mesh;

	//define the player camera
	Unigine::PlayerPtr player;
};


```


```cpp
#include "AppWorldLogic.h"
#include <UnigineMathLib.h>
#include <UnigineGame.h>
#include <UnigineMesh.h>

using namespace Math;

AppWorldLogic::AppWorldLogic(){}

AppWorldLogic::~AppWorldLogic(){}
int AppWorldLogic::init()
{
	// get the current game camera
	player = Game::getPlayer();

	// set the camera position and direction to look at the object
	player->setPosition(Vec3(4.0f, -3.401f, 1.5f));
	player->setDirection(vec3(0.0f, 1.0f, -0.4f), player->getUp());

	// create the ObjectMeshStatic by using the new mesh
	mesh = ObjectMeshStatic::create("core/meshes/box.mesh");

	// set the mesh position
	mesh->setPosition(Vec3(4.0f, 0.0f, 1.0f));
	return 1;
}


```


### Creating and Adding the Property


We are going to write the code that controls the object's movements as a separate component to make it reusable. [Create a new C++ class](https://docs.microsoft.com/en-us/cpp/windows/walkthrough-creating-a-standard-cpp-program-cpp?view=msvc-170#add-a-new-source-file) (the header and `*.cpp` files) in the project. Let's name this component *MovementControls*. You can also check [this article](../../../code/usage/using_component_system/index.md#create_class) for more details about adding components.


```cpp
#pragma once

#include <UnigineComponentSystem.h>
#include <UnigineLogic.h>
#include <UnigineStreams.h>

class MovementControls : public Unigine::ComponentBase
{
public:
	COMPONENT_DEFINE(MovementControls, Unigine::ComponentBase);

	COMPONENT_INIT(init);
	COMPONENT_UPDATE(update);

	void init();
	void update();
};

```


```cpp
#include "MovementControls.h"
#include <UnigineControls.h>
#include <UnigineEditor.h>
#include <UnigineMathLib.h>
#include <UnigineGame.h>
#include <UnigineVisualizer.h>

REGISTER_COMPONENT(MovementControls);

using namespace Unigine;
using namespace Math;

void MovementControls::init() {

}

void MovementControls::update() {

}


```


And to assign this property to the mesh we want to move, we add the following line in the *init()* method in `AppWorldLogic.cpp`:


```cpp
int AppWorldLogic::init()
{
	/* ... */
	// assign the movement controlling property to the mesh
	mesh->addProperty("MovementControls");
	return 1;
}


```


### Moving Forward


This section demonstrates how to set the forward movement of the mesh.


In this example, we use the *"p"* key pressing to move the mesh forward. The direction vector is visualized for clarity.


In `MovementControls.h`, we add the property parameters to access them via Editor and set their initial values:


```cpp
#pragma once

#include <UnigineComponentSystem.h>
#include <UnigineLogic.h>
#include <UnigineStreams.h>

class MovementControls : public Unigine::ComponentBase
{
public:
	COMPONENT_DEFINE(MovementControls, Unigine::ComponentBase);
	// define the property parameters that can be adjusted via the Editor as well
	PROP_PARAM(Node, moving_node);
	// define the movement speed
	PROP_PARAM(Float, movement_speed, 5.0f);

	COMPONENT_INIT(init);
	COMPONENT_UPDATE(update);

	void init();
	void update();
};

```


In `MovementControls.cpp`, we add the movement-related logic:


```cpp
#include "MovementControls.h"
#include <UnigineControls.h>
#include <UnigineEditor.h>
#include <UnigineMathLib.h>
#include <UnigineGame.h>
#include <UnigineVisualizer.h>

REGISTER_COMPONENT(MovementControls);

using namespace Unigine;
using namespace Math;

void MovementControls::init() {

	// enable visualizer
	Visualizer::setEnabled(1);

	// check if the key is pressed and update the state of the specified control

	ControlsApp::setStateKey(Controls::STATE_AUX_0, 'p');

}

void MovementControls::update() {

	// get the frame duration
	float ifps = Game::getIFps();

	// get the current world transformation matrix of the node this property is assigned to
	Mat4 transform = node->getWorldTransform();

	// get the direction vector of the node from the second column of the transformation matrix
	Vec3 direction = transform.getColumn3(1);

	// render the direction vector for visual clarity
	Visualizer::renderDirection(node->getWorldPosition(), vec3(direction), vec4(1.0f, 0.0f, 0.0f, 1.0f), 0.1f, 0);

	// check if the control key is pressed
	if (ControlsApp::getState(Controls::STATE_AUX_0)) {

		// calculate the delta of movement
		Vec3 delta_movement = direction * movement_speed * ifps;

		// set a new position to the node
		node->setWorldPosition(node->getWorldPosition() + delta_movement);
	}

}


```


#### Another Way of Setting Mesh Position


The new position can be also set by setting the *[WorldTransform](../../../api/library/nodes/class.node_cpp.md#WorldTransform)* variable. The following examples contain the code from the *Update()* function of the *[AppWorldLogic](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic)* class. The part of controls initialization is the same for this method, the difference is in the *Update()* function only.


```cpp
// check if the control key is pressed
if (ControlsApp::getState(Controls::STATE_AUX_0)) {

	// calculate the delta of movement
	Vec3 delta_movement = direction * movement_speed * ifps;

	// set a new position to the node
	node->setWorldTransform(translate(delta_movement) * transform);
}


```


Or you can change the translation column of the world transformation matrix (see the [Matrix Transformations](../../../code/fundamentals/matrix_transformations/index_cpp.md) article) to move the node:


```cpp
// check if the control key is pressed.
if (ControlsApp::getState(Controls::STATE_AUX_0)) {

	// calculate the delta of movement
	Vec3 delta_movement = direction * movement_speed * ifps;

	// set a new position
	// here, you can also use transform.setColumn3(3, transform.getColumn3(3) + delta_movement);
	transform.setColumn(3, transform.getColumn(3) + Vec4(delta_movement, 1.0f));

	// set a new world transform matrix to the mesh
	node->setWorldTransform(transform);
}


```


### Rotation


This section contains implementation of the mesh rotation.


You can rotate the mesh in two ways, by changing the transformation matrix represented by the *[WorldTransform](../../../api/library/nodes/class.node_cpp.md#WorldTransform)* variable (recommended way) or via the *[SetWorldRotation()](../../../api/library/nodes/class.node_cpp.md#setWorldRotation_quat_int_void)* function. The following example uses the second one:


```cpp
#pragma once

#include <UnigineComponentSystem.h>
#include <UnigineLogic.h>
#include <UnigineStreams.h>

class MovementControls : public Unigine::ComponentBase
{
public:
	COMPONENT_DEFINE(MovementControls, Unigine::ComponentBase);
	// define the property parameters that can be adjusted via the Editor as well
	PROP_PARAM(Node, moving_node);
	// define the rotation speed
	PROP_PARAM(Float, rotation_speed, 30.0f);

	COMPONENT_INIT(init);
	COMPONENT_UPDATE(update);

	void init();
	void update();
};

```


```cpp
#include "MovementControls.h"
#include <UnigineControls.h>
#include <UnigineEditor.h>
#include <UnigineMathLib.h>
#include <UnigineGame.h>
#include <UnigineVisualizer.h>

REGISTER_COMPONENT(MovementControls);

using namespace Unigine;
using namespace Math;

void MovementControls::init() {

	// enable visualizer
	Visualizer::setEnabled(1);

	// check if the key is pressed and update the state of the specified control

	ControlsApp::setStateKey(Controls::STATE_AUX_1, 'o');

}

void MovementControls::update() {

	// get the frame duration
	float ifps = Game::getIFps();

	// check if the control key is pressed
	if (ControlsApp::getState(Controls::STATE_AUX_1)) {

		// set the node rotation along the Z axis assuming node's scale equal to 1
		node->setWorldRotation(node->getWorldRotation() * quat(rotateZ(rotation_speed * ifps)), 1);
	}
}


```


In the example above, the node is rotated to the left by pressing the *"o"* keyboard key.


> **Notice:** - It is recommended to set the second argument of the *[SetWorldRotation()](../../../api/library/nodes/class.node_cpp.md#setWorldRotation_quat_int_void)* function to 1 for all non-scaled nodes to improve performance and accuracy.
> - **Scaling of nodes should be avoided whenever possible**, as it requires addidional calculations and may lead to error accumulation.


To rotate the object by via the *[WorldTransform](../../../api/library/nodes/class.node_cpp.md#WorldTransform)* variable, you should replace the line containing the *SetWorldRotation()* function in the example above with the following one:


```cpp
node->setWorldTransform(node->getWorldTransform() * Mat4(rotateZ(rotation_speed * ifps)));


```


This way is preferred, especially in case of [complex transformations](#combining), as it allows composing the transformation matrix and setting it only once.


## Combining Movements


Combining different movement controls is not more difficult than adding only one movement control.


The following code is an example that adds a mesh to the world and assigns a component on it that allows controlling its movements. You can rotate the mesh by using the *"o", "["* keyboard keys and move forward by using the *"p"* key.


```cpp
#include "AppSystemLogic.h"
#include <UnigineComponentSystem.h>

using namespace Unigine;

AppSystemLogic::AppSystemLogic(){}

AppSystemLogic::~AppSystemLogic(){}
int AppSystemLogic::init()
{
	Unigine::ComponentSystem::get()->initialize();
	return 1;
}
////////////////////////////////////////////////////////////////////////////////
// start of the main loop
////////////////////////////////////////////////////////////////////////////////

int AppSystemLogic::update()
{
	// Write here code to be called before updating each render frame.
	return 1;
}

int AppSystemLogic::postUpdate()
{
	// Write here code to be called after updating each render frame.
	return 1;
}

////////////////////////////////////////////////////////////////////////////////
// end of the main loop
////////////////////////////////////////////////////////////////////////////////

int AppSystemLogic::shutdown()
{
	// Write here code to be called on engine shutdown.
	return 1;
}

```


```cpp
#ifndef __APP_WORLD_LOGIC_H__
#define __APP_WORLD_LOGIC_H__

 #include <UnigineLogic.h>
#include <UnigineStreams.h>
#include <UnigineObjects.h>
#include <UniginePlayers.h>

using namespace Unigine;

class AppWorldLogic : public Unigine::WorldLogic
{

public:
	AppWorldLogic();
	virtual ~AppWorldLogic();

	int init() override;

	int update() override;
	int postUpdate() override;
	int updatePhysics() override;

	int shutdown() override;

private:
	// define the ObjectMeshStatic instance
	// so that it will be deleted with the AppWorldLogic instance
	Unigine::ObjectMeshStaticPtr mesh;

	//define the player camera
	Unigine::PlayerPtr player;
};
#endif // __APP_WORLD_LOGIC_H__

```


```cpp
#include "AppWorldLogic.h"
#include <UnigineMathLib.h>
#include <UnigineGame.h>
#include <UnigineMesh.h>

using namespace Math;

AppWorldLogic::AppWorldLogic(){}

AppWorldLogic::~AppWorldLogic(){}
int AppWorldLogic::init()
{
	// get the current game camera
	player = Game::getPlayer();

	// set the camera position and direction to look at the object
	player->setPosition(Vec3(4.0f, -3.401f, 1.5f));
	player->setDirection(vec3(0.0f, 1.0f, -0.4f), player->getUp());

	// create the ObjectMeshStatic by using the new mesh
	mesh = ObjectMeshStatic::create("core/meshes/box.mesh");

	// set the mesh position
	mesh->setPosition(Vec3(4.0f, 0.0f, 1.0f));
	// assign the movement controlling property to the mesh
	mesh->addProperty("MovementControls");
	return 1;
}

////////////////////////////////////////////////////////////////////////////////
// start of the main loop
////////////////////////////////////////////////////////////////////////////////

int AppWorldLogic::update()
{
	// Write here code to be called before updating each render frame: specify all graphics-related functions you want to be called every frame while your application executes.
	return 1;
}

int AppWorldLogic::postUpdate()
{
	// The engine calls this function after updating each render frame: correct behavior after the state of the node has been updated.
	return 1;
}

int AppWorldLogic::updatePhysics()
{
	// Write here code to be called before updating each physics frame: control physics in your application and put non-rendering calculations.
	// The engine calls updatePhysics() with the fixed rate (60 times per second by default) regardless of the FPS value.
	// WARNING: do not create, delete or change transformations of nodes here, because rendering is already in progress.
	return 1;
}

////////////////////////////////////////////////////////////////////////////////
// end of the main loop
////////////////////////////////////////////////////////////////////////////////

int AppWorldLogic::shutdown()
{
	// Write here code to be called on world shutdown: delete resources that were created during world script execution to avoid memory leaks.
	return 1;
}

```


```cpp
#pragma once

#include <UnigineComponentSystem.h>
#include <UnigineLogic.h>
#include <UnigineStreams.h>

class MovementControls : public Unigine::ComponentBase
{
public:
	COMPONENT_DEFINE(MovementControls, Unigine::ComponentBase);
	// define the property parameters that can be adjusted via the Editor as well
	PROP_PARAM(Node, moving_node);
	// define the movement speed
	PROP_PARAM(Float, movement_speed, 5.0f);
	// define the rotation speed
	PROP_PARAM(Float, rotation_speed, 30.0f);

	COMPONENT_INIT(init);
	COMPONENT_UPDATE(update);

	void init();
	void update();
};

```


```cpp
#include "MovementControls.h"
#include <UnigineControls.h>
#include <UnigineEditor.h>
#include <UnigineMathLib.h>
#include <UnigineGame.h>
#include <UnigineVisualizer.h>

REGISTER_COMPONENT(MovementControls);

using namespace Unigine;
using namespace Math;

void MovementControls::init() {
	// enable visualizer
	Visualizer::setEnabled(1);

	// check if the key is pressed and update the state of the specified control
	// you can use both 'p', 'o', '[' or ASCII codes (112, 111, 113)
	ControlsApp::setStateKey(Controls::STATE_AUX_0, 'p');
	ControlsApp::setStateKey(Controls::STATE_AUX_1, 'o');
	ControlsApp::setStateKey(Controls::STATE_AUX_2, '[');
}

void MovementControls::update() {

	// get the frame duration
	float ifps = Game::getIFps();

	// get the current world transformation matrix of the node this property is assigned to
	Mat4 transform = node->getWorldTransform();

	// get the direction vector of the node from the second column of the transformation matrix
	Vec3 direction = transform.getColumn3(1);

	// initialize the update flag and declare rotation and movement
	int update_transform = 0;
	Mat4 rotation;
	Vec3 delta_movement;

	// render the direction vector for visual clarity
	Visualizer::renderDirection(node->getWorldPosition(), vec3(direction), vec4(1.0f, 0.0f, 0.0f, 1.0f), 0.1f, 0);

	// check if the control key for movement is pressed
	if (ControlsApp::getState(Controls::STATE_AUX_0))
	{
		// calculate the delta of movement
		delta_movement = direction * movement_speed * ifps;

		update_transform = 1;
	}

	// check if the control key for left rotation is pressed
	if (ControlsApp::getState(Controls::STATE_AUX_1))
	{
		// set the node left rotation along the Z axis
		rotation.setRotateZ(rotation_speed * ifps);
		update_transform = 1;
	}
	// check if the control key for right rotation is pressed
	else if (ControlsApp::getState(Controls::STATE_AUX_2))
	{
		// set the node right rotation along the Z axis
		rotation.setRotateZ(-rotation_speed * ifps);
		update_transform = 1;
	}

	// update transformation if necessary
	if (update_transform)
	{
		// combine transformations: movement + rotation
		transform = transform * rotation;
		transform.setColumn3(3, transform.getColumn3(3) + delta_movement);

		// set the resulting transformation
		node->setWorldTransform(transform);
	}

}
void MovementControls::forward() {
	// get the frame duration
	float ifps = Game::getIFps();

	// get the current world transformation matrix of the node this property is assigned to
	Mat4 transform = node->getWorldTransform();

	// get the direction vector of the node from the second column of the transformation matrix
	Vec3 direction = transform.getColumn3(1);

	// render the direction vector for visual clarity
	Visualizer::renderDirection(node->getWorldPosition(), vec3(direction), vec4(1.0f, 0.0f, 0.0f, 1.0f), 0.1f, 0);

	// check if the control key is pressed
	if (ControlsApp::getState(Controls::STATE_AUX_0)) {

		// calculate the delta of movement
		Vec3 delta_movement = direction * movement_speed * ifps;

		// set a new position to the node
		node->setWorldPosition(node->getWorldPosition() + delta_movement);
	}

}
void MovementControls::position_var_1() {
	// get the frame duration
	float ifps = Game::getIFps();
	// get the current world transformation matrix of the mesh
	Mat4 transform = node->getWorldTransform();
	Vec3 direction = transform.getColumn3(1);

	// check if the control key is pressed
	if (ControlsApp::getState(Controls::STATE_AUX_0)) {

		// calculate the delta of movement
		Vec3 delta_movement = direction * movement_speed * ifps;

		// set a new position to the node
		node->setWorldTransform(translate(delta_movement) * transform);
	}
}

void MovementControls::position_var_2() {
	// get the frame duration
	float ifps = Game::getIFps();
	// get the current world transformation matrix of the mesh
	Mat4 transform = node->getWorldTransform();
	Vec3 direction = transform.getColumn3(1);

	// check if the control key is pressed.
	if (ControlsApp::getState(Controls::STATE_AUX_0)) {

		// calculate the delta of movement
		Vec3 delta_movement = direction * movement_speed * ifps;

		// set a new position
		// here, you can also use transform.setColumn3(3, transform.getColumn3(3) + delta_movement);
		transform.setColumn(3, transform.getColumn(3) + Vec4(delta_movement, 1.0f));

		// set a new world transform matrix to the mesh
		node->setWorldTransform(transform);
	}
}

void MovementControls::rotation_var_1() {
	// get the frame duration
	float ifps = Game::getIFps();

	// check if the control key is pressed
	if (ControlsApp::getState(Controls::STATE_AUX_1)) {

		// set the node rotation along the Z axis assuming node's scale equal to 1
		node->setWorldRotation(node->getWorldRotation() * quat(rotateZ(rotation_speed * ifps)), 1);
	}
}
void MovementControls::rotation_var_2() {
	// get the frame duration
	float ifps = Game::getIFps();

	// check if the control key is pressed
	if (ControlsApp::getState(Controls::STATE_AUX_1)) {

		// set the node rotation along the Z axis assuming node's scale equal to 1
		node->setWorldTransform(node->getWorldTransform() * Mat4(rotateZ(rotation_speed * ifps)));
	}
}

```
