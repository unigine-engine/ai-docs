# A Car with Wheel Joints (CPP)


![Car with wheel joints](car_joints_main.jpg)

*Car with wheel joints*


This example shows how to:


- Add and setup a simple car with a frame and wheels attached to it with [wheel joints](../../../principles/physics/joints/index.md#wheel).
- [Enable car movement](#velocity) using [joint motors](../../../principles/physics/joints/index.md#motors).
- Use a keyboard to control car movement.


The **basic workflow** is as follows:


1. Prepare visual geometry of the car (frame and wheels) and add it to the scene.
2. Set up a third-person camera that follows the car and orbits around it.
3. Assign [rigid bodies](../../../principles/physics/bodies/rigid/index.md) and [collision shapes](../../../principles/physics/shapes/index.md) to the wheels and the frame.
4. Set up parameters of the bodies and shapes (mass, rotation, radius, hegiht, etc.).
5. Connect the wheels to the frame using [wheel joints](../../../principles/physics/joints/index.md#wheel). Set up parameters of the joints. > **Notice:** Do not use real masses (e.g. 2000 kg for the frame and 10 kg for the wheels), as joints may become unstable! It might be better to use 64 kg for the body and 25 kg for each wheel to provide realistic behavior.
6. Enable the car movement using [joint motors](../../../principles/physics/joints/index.md#motors) by setting up the movement controls with the corresponding keyboard keys.


## Step 1. Importing Vehicle Geometry


The first thing we are going to address in this tutorial is the geometry of our car. It is possible to use any other custom made model for the vehicle appearance. Every wheel and the frame will be individual independent [nodes](../../../objects/nodes/index.md) in the world, so make sure that your vehicle model includes separate meshes for the wheels and the frame.


Right now we are going to take the vehicle model from the content addon included in the SDK and then add some physical parameters to the geometry to achieve a viable driving simulation.


1. Let's create [an empty C++ project](../../../sdk/projects/index_cpp.md#creation).
2. Download the *[Eastern European Countryside add-on](../../../sdk/addons/eastern_european_countryside/index.md)* from Add-On Store at [https://store.unigine.com/](https://store.unigine.com/) and add it to the project by dragging into the project `data/` folder in the Asset Browser. In the *Import Package* window that opens, click the *Import Package* button and wait until the add-on contents are imported.
3. Launch the Editor via the *Open Editor* button. For your vehicle you can choose any of the minibus nodes located in `data/countryside/minibus` or [import](../../../editor2/assets_workflow/assets_create_import.md) your own model in any [supported file format](../../../editor2/assets_workflow/asset_types.md). ![](models.png) A minibus vehicle model has the body frame as the parent node and its wheels as child nodes. ![](hierarchy.png)
4. In the Asset Browser, right-click on a minibus node you like the most and choose *Place as Node Content*. Place the vehicle on the ground in the world. As we don't plan to use multiple instances of the car, we simply put all its parts directly to the scene, without the *NodeReference* container. ![](place_cpp.jpg)


## Step 2. Setting Up Camera


Let�s create a camera for a third-person view. While the camera follows the car, the player can control the viewing direction (rotate the camera) with the mouse. To achieve this, perform the following:


1. In the *World Nodes* window, delete the *first_person_controller* containing the default camera.
2. Create a custom *Persecutor Camera* to follow the car. Go to *Create -> Camera -> Persecutor* and then place it near the vehicle.
3. Check the **Main Player** option in the *Parameters* tab of the *PlayerPersecutor* to make it the default camera in the world.
4. Delete the default *Persecutor_Target* node from the *World Nodes* window hierarchy and set our **minibus** as the target node for the *PlayerPersecutor* camera instead. ![](target.png)
5. To put the camera closer to the vehicle, set the *Max Distance* parameter for the PlayerPersecutor to 8.


## Step 3. Setting Up Physical Bodies and Shapes


In order to give our car some physical properties, we must [assign](../../../principles/physics/bodies/rigid/index.md#assign) physical bodies and approximating volumetric shapes to its frame and wheels. To achieve this, do the following:


> **Notice:** Do not change the scale of the frame or wheel nodes, since the physics simulation does not support it. The scale of all nodes should be equal to 1 along all axes, to ensure correct physics simulation.


1. Go to the *Parameters* tab of the minibus frame (the *minibus_ambulance* node) and, in the *Physics* tab, assign a physical [rigid body](../../../principles/physics/bodies/rigid/index.md) by selecting *Body* -> **Rigid**. Also, add a [box shape](../../../principles/physics/shapes/index.md#box) to the body (*Shape* -> **Box**). ![](body.png)
2. Set the *mass* of *ShapeBox* to 100. ![](shapebox_mass.png)
3. Disable the *Shape-Based* option for the frame�s rigid body to turn off automatic calculation and customize mass distribution of the vehicle. Set the third component of the *CMass* parameter to 0.25 effectively lowering the center of mass. ![](cmass.png)
4. For each wheel (child nodes of *minibus_ambulance*), go to the *Parameters* tab and, in the *Physics* section, assign **a rigid body** with **a cylinder shape** that roughly approximates the shape of the wheel mesh. You may need to rotate *ShapeCylinder* and adjust its radius and height to position it properly (see the image below). ![](cylinder.png) > **Notice:** In the *World Nodes* window, you can select multiple wheel nodes at the same time by holding **Shift** key and selecting the first and the last one. This way you will be able to add bodies and shapes to all wheels simultaneously.


## Step 4. Setting Up Joints


For the wheels to be connected to the frame and behave realistically, we must connect them using [wheel joints](../../../principles/physics/joints/index.md#wheel). These joints not only remove degrees of freedom providing motion constraints, but also simulate vehicle suspension and motor torque for wheels.


We need to connect the body of **every wheel** to the frame�s body using **wheel joints**.


1. To do so, select the frame of the minibus (the *minibus_ambulance* node) in the *World Nodes* hierarchy window and go to the *Joints* section of the *Physics* tab. There you must specify the *Wheel* type for the joint and click the *Add* button. ![](wheel_joint.png)
2. You shall see the following dialog window. Connect the frame body to every wheel�s body by selecting every wheel one by one. The specified rigid body will be connected to the rigid body of the car using a wheel joint. ![](add_wheel_joint.png)


You will end up with four wheel joints connecting corresponding wheels� bodies to the frame�s body (you may name them accordingly).


![](wheel_joints.png)


To configure the setup, do the following for every wheel joint (select them one by one and tweak settings below):


1. Press **Fix 0** button to fix *Anchor 0* point to the wheel position. This will place the joint in the correct position for this wheel. ![](fix.png) ![](axes.jpg)
2. Set the number of joint solving *Iterations* to 16 making the physical simulation more stable. > **Notice:** You can select multiple joints at the same time by holding **Shift** key and selecting the first and the last one. This way you will be able to set the same settings to all joints simultaneously.
3. Next, set the following values to the joint�s parameters to achieve a plausible simulation behavior. ![](values.png)
4. Wheel joints are based on physics raycasting. To make them interact with the ground properly, enable **Physics Intersection** for the surface of the *ground_plane* node in the *Parameters* tab. ![](physics_intersection.png)


## Step 5. Applying Velocity to Wheels


Now let�s create a C++ component to implement driving and steering functionality for the car. To achieve this, do the following:


1. To start writing code we should open our project in an IDE. Go to *SDK Browser* and choose the **Open Code IDE** button.
2. In an IDE create a new C++ class (***.h** and ***.cpp** files) and call it ***Car***. Make sure it inherits from the *Unigine::ComponentBase* class.
3. Get references to joints from the wheel nodes and define variables for the *velocity*, *acceleration* and *torque* values. <details> <summary>Car.h | Close</summary> `Car.h` ```cpp #pragma once #include <UnigineComponentSystem.h> #include <UniginePhysics.h> #include <UniginePlayers.h> #include <UnigineControls.h> #include <UnigineGame.h> #include <UnigineMathLib.h> class Car : public Unigine::ComponentBase { public: // declare constructor and destructor for our class and define a property name COMPONENT_DEFINE(Car, ComponentBase) // declare methods to be called at the corresponding stages of the execution sequence COMPONENT_INIT(init); COMPONENT_UPDATE(update); COMPONENT_UPDATE_PHYSICS(updatePhysics); // driving parameters PROP_PARAM(Float, acceleration, 50.0f); PROP_PARAM(Float, max_velocity, 90.0f); PROP_PARAM(Float, default_torque, 5.0f); // wheel joints PROP_PARAM(Node, wheel_bl); PROP_PARAM(Node, wheel_br); PROP_PARAM(Node, wheel_fl); PROP_PARAM(Node, wheel_fr); protected: void init(); void update(); void updatePhysics(); private: // wheel joints Unigine::JointWheelPtr joint_wheel_bl; Unigine::JointWheelPtr joint_wheel_br; Unigine::JointWheelPtr joint_wheel_fl; Unigine::JointWheelPtr joint_wheel_fr; // settings of input controls Unigine::ControlsPtr controls; // current driving parameters float current_velocity = 0.0f; float current_torque = 0.0f; }; ``` </details> <details> <summary>Car.cpp | Close</summary> `Car.cpp` ```cpp #include "Car.h" using namespace Unigine; REGISTER_COMPONENT(Car); void Car::init() { // get the wheel joints from the nodes if (wheel_bl) joint_wheel_bl = checked_ptr_cast<JointWheel>(wheel_bl->getObjectBody()->getJoint(0)); if (wheel_br) joint_wheel_br = checked_ptr_cast<JointWheel>(wheel_br->getObjectBody()->getJoint(0)); if (wheel_fl) joint_wheel_fl = checked_ptr_cast<JointWheel>(wheel_fl->getObjectBody()->getJoint(0)); if (wheel_fr) joint_wheel_fr = checked_ptr_cast<JointWheel>(wheel_fr->getObjectBody()->getJoint(0)); // get the settings of input controls relevant to the player (camera) controls = Game::getPlayer()->getControls(); } ``` </details>
4. Then add *control inputs* processing to determine the current torque and velocity to be applied to wheel joints. <details> <summary>Car.cpp | Close</summary> `Car.cpp` ```cpp void Car::update() { // get the time it took to render the previous frame float deltaTime = Game::getIFps(); // process control inputs if (controls) { // set the torque and increase the current velocity if the forward button is pressed if (controls->getState(Controls::STATE_FORWARD) != 0) { current_torque = default_torque; current_velocity = Math::max(current_velocity, 0.0f); current_velocity += deltaTime * acceleration; } // set the torque and decrease the current velocity if the backward button is pressed else if (controls->getState(Controls::STATE_BACKWARD) != 0) { current_torque = default_torque; current_velocity = Math::min(current_velocity, 0.0f); current_velocity -= deltaTime * acceleration; } // exponentially decrease the current velocity when neither throttle nor brakes are applied else { current_velocity *= Math::exp(-deltaTime); } } ``` </details>
5. To move the car forward or backward, we are going to use [joint motors](../../../principles/physics/joints/index.md#motors) of the front wheels: Each physics frame, we apply current angular velocity and torque to the wheel joints based on the user input. <details> <summary>Car.cpp | Close</summary> `Car.cpp` ```cpp // actually apply the torque and velocity to the front wheel joints void Car::updatePhysics() { joint_wheel_fl->setAngularVelocity(current_velocity); joint_wheel_fr->setAngularVelocity(current_velocity); joint_wheel_fl->setAngularTorque(current_torque); joint_wheel_fr->setAngularTorque(current_torque); } ``` </details>

  - Setting a **positive** velocity value will move our car **forward**.
  - Setting a **negative** velocity value will move our car **backward**.


## Step 6. Implementing Steering and Braking


To provide the ability to turn left or right as well as the ability to slow down with brakes, we shall implement some additional logic that turns the front wheels and stops the rear ones. To achieve this, do the following:


1. Add the following code to the *Car* component to add the front wheels *turning* and *braking* support. <details> <summary>Car.h | Close</summary> `Car.cpp` ```cpp PROP_PARAM(Float, turn_speed, 50.0f); PROP_PARAM(Float, car_base, 3.0f); PROP_PARAM(Float, car_width, 2.0f); float current_turn_angle = 0.0f; float max_turn_angle = 30.0f; ``` </details> <details> <summary>Car.cpp | Close</summary> `Car.cpp` ```cpp void Car::update() { // get the time it took to render the previous frame float deltaTime = Game::getIFps(); current_torque = 0.0f; // process control inputs if (controls) { /*...*/ // turn the front wheels based on the direction input if (controls->getState(Controls::STATE_MOVE_LEFT) != 0) current_turn_angle += deltaTime * turn_speed; else if (controls->getState(Controls::STATE_MOVE_RIGHT) != 0) current_turn_angle -= deltaTime * turn_speed; else { // get rid of the front wheel wiggle if (Math::abs(current_turn_angle) < 0.25f) current_turn_angle = 0.0f; // align the front wheels if there are no more direction input current_turn_angle -= Math::sign(current_turn_angle) * turn_speed * deltaTime; } // apply braking by maxing out the angular damping if the brake button is pressed if (controls->getState(Controls::STATE_USE) != 0) { joint_wheel_bl->setAngularDamping(10000.0f); joint_wheel_br->setAngularDamping(10000.0f); } else { joint_wheel_bl->setAngularDamping(0.0f); joint_wheel_br->setAngularDamping(0.0f); } } // clamp the velocity and the front wheels turn angle current_velocity = Math::clamp(current_velocity, -max_velocity, max_velocity); current_turn_angle = Math::clamp(current_turn_angle, -max_turn_angle, max_turn_angle); // figure out the correct turn angle for the front wheels float angle_0 = current_turn_angle; float angle_1 = current_turn_angle; if (Math::abs(current_turn_angle) > Math::Consts::EPS) { float radius = car_base / Math::tan(current_turn_angle * Math::Consts::DEG2RAD); float radius_0 = radius - car_width * 0.5f; float radius_1 = radius + car_width * 0.5f; angle_0 = Math::atan(car_base / radius_0) * Math::Consts::RAD2DEG; angle_1 = Math::atan(car_base / radius_1) * Math::Consts::RAD2DEG; } joint_wheel_fr->setAxis10(Math::rotateZ(angle_1).getColumn3(0)); joint_wheel_fl->setAxis10(Math::rotateZ(angle_0).getColumn3(0)); } ``` </details>
2. Before you can use the C++ component you should initialize the Component System. Modify the *init()* method of the AppSystemLogic class as shown below (*AppSystemLogic.cpp* file). <details> <summary>AppSystemLogic.cpp | Close</summary> `AppSystemLogic.cpp` ```cpp #include <UnigineComponentSystem.h> int AppSystemLogic::init() { // initialize ComponentSystem and register all components ComponentSystem::get()->initialize(); return 1; } ``` </details>
3. Build and run the project via your IDE (press **Ctrl + F5** in Visual Studio), the Component System will generate a property-file for the *Car* component.
4. Switch back to *UnigineEditor* and select the root **minibus** node in the *World Nodes* window. Then click *Add New Property* in the *Parameters* window and assign the newly generated **Car** property.
5. Next, assign wheels (*ObjectMeshStatic* nodes) to the corresponding **fields** of the *Car* property as specified below. ![](fields_cpp.png)


Congratulations! Now you can finally drive the car around the world. If the current physics of the car is not suitable for your needs, you can always fine tune the parameters of the wheel joints and achieve the results you need. Also, see the [Basic Programming How-To Livestream](https://youtu.be/ROy9oGPnABE) for the hands-on vehicle implementation and discussions. The full source code of the *Car* component is given below.


<details>
<summary>Car.h | Close</summary>

`Car.h`


```cpp
#pragma once
#include <UnigineComponentSystem.h>

#include <UniginePhysics.h>
#include <UniginePlayers.h>
#include <UnigineControls.h>
#include <UnigineGame.h>
#include <UnigineMathLib.h>

class Car : public Unigine::ComponentBase
{
public:
	// declare constructor and destructor for our class and define a property name
	COMPONENT_DEFINE(Car, ComponentBase)
	// declare methods to be called at the corresponding stages of the execution sequence
	COMPONENT_INIT(init);
	COMPONENT_UPDATE(update);
	COMPONENT_UPDATE_PHYSICS(updatePhysics);

	// driving parameters
	PROP_PARAM(Float, acceleration, 50.0f);
	PROP_PARAM(Float, max_velocity, 90.0f);
	PROP_PARAM(Float, default_torque, 5.0f);
	PROP_PARAM(Float, turn_speed, 50.0f);
	PROP_PARAM(Float, car_base, 3.0f);
	PROP_PARAM(Float, car_width, 2.0f);

	// wheel joints
	PROP_PARAM(Node, wheel_bl);
	PROP_PARAM(Node, wheel_br);
	PROP_PARAM(Node, wheel_fl);
	PROP_PARAM(Node, wheel_fr);

protected:
	void init();
	void update();
	void updatePhysics();

private:
	// wheel joints
	Unigine::JointWheelPtr joint_wheel_bl;
	Unigine::JointWheelPtr joint_wheel_br;
	Unigine::JointWheelPtr joint_wheel_fl;
	Unigine::JointWheelPtr joint_wheel_fr;

	// settings of input controls
	Unigine::ControlsPtr controls;

	// current driving parameters
	float current_velocity = 0.0f;
	float current_torque = 0.0f;
	float current_turn_angle = 0.0f;

	float max_turn_angle = 30.0f;

};

```

</details>


<details>
<summary>Car.cpp | Close</summary>

`Car.cpp`


```cpp
#include "Car.h"

using namespace Unigine;

REGISTER_COMPONENT(Car);

void Car::init()
{
	// get the wheel joints from the nodes
	if (wheel_bl)
		joint_wheel_bl = checked_ptr_cast<JointWheel>(wheel_bl->getObjectBody()->getJoint(0));

	if (wheel_br)
		joint_wheel_br = checked_ptr_cast<JointWheel>(wheel_br->getObjectBody()->getJoint(0));

	if (wheel_fl)
		joint_wheel_fl = checked_ptr_cast<JointWheel>(wheel_fl->getObjectBody()->getJoint(0));

	if (wheel_fr)
		joint_wheel_fr = checked_ptr_cast<JointWheel>(wheel_fr->getObjectBody()->getJoint(0));

	// get the settings of input controls relevant to the player (camera)
	controls = Game::getPlayer()->getControls();
}

void Car::update()
{
	// get the time it took to render the previous frame
	float deltaTime = Game::getIFps();

	current_torque = 0.0f;

	// process control inputs
	if (controls)
	{
		// set the torque and increase the current velocity if the forward button is pressed
		if (controls->getState(Controls::STATE_FORWARD) != 0)
		{
			current_torque = default_torque;
			current_velocity = Math::max(current_velocity, 0.0f);
			current_velocity += deltaTime * acceleration;
		}
		// set the torque and decrease the current velocity if the backward button is pressed
		else if (controls->getState(Controls::STATE_BACKWARD) != 0)
		{
			current_torque = default_torque;
			current_velocity = Math::min(current_velocity, 0.0f);
			current_velocity -= deltaTime * acceleration;
		}
		// exponentially decrease the current velocity when neither throttle nor brakes are applied
		else
		{
			current_velocity *= Math::exp(-deltaTime);
		}
		/*...*/
		// turn the front wheels based on the direction input
		if (controls->getState(Controls::STATE_MOVE_LEFT) != 0)
			current_turn_angle += deltaTime * turn_speed;
		else if (controls->getState(Controls::STATE_MOVE_RIGHT) != 0)
			current_turn_angle -= deltaTime * turn_speed;
		else
		{
			// get rid of the front wheel wiggle
			if (Math::abs(current_turn_angle) < 0.25f)
				current_turn_angle = 0.0f;

			// align the front wheels if there are no more direction input
			current_turn_angle -= Math::sign(current_turn_angle) * turn_speed * deltaTime;
		}

		// apply braking by maxing out the angular damping if the brake button is pressed
		if (controls->getState(Controls::STATE_USE) != 0)
		{
			joint_wheel_bl->setAngularDamping(10000.0f);
			joint_wheel_br->setAngularDamping(10000.0f);
		}
		else
		{
			joint_wheel_bl->setAngularDamping(0.0f);
			joint_wheel_br->setAngularDamping(0.0f);
		}
	}

	// clamp the velocity and the front wheels turn angle
	current_velocity = Math::clamp(current_velocity, -max_velocity, max_velocity);
	current_turn_angle = Math::clamp(current_turn_angle, -max_turn_angle, max_turn_angle);

	// figure out the correct turn angle for the front wheels
	float angle_0 = current_turn_angle;
	float angle_1 = current_turn_angle;
	if (Math::abs(current_turn_angle) > Math::Consts::EPS)
	{
		float radius = car_base / Math::tan(current_turn_angle * Math::Consts::DEG2RAD);
		float radius_0 = radius - car_width * 0.5f;
		float radius_1 = radius + car_width * 0.5f;

		angle_0 = Math::atan(car_base / radius_0) * Math::Consts::RAD2DEG;
		angle_1 = Math::atan(car_base / radius_1) * Math::Consts::RAD2DEG;
	}

	joint_wheel_fr->setAxis10(Math::rotateZ(angle_1).getColumn3(0));
	joint_wheel_fl->setAxis10(Math::rotateZ(angle_0).getColumn3(0));
}

// actually apply the torque and velocity to the front wheel joints
void Car::updatePhysics()
{
	joint_wheel_fl->setAngularVelocity(current_velocity);
	joint_wheel_fr->setAngularVelocity(current_velocity);

	joint_wheel_fl->setAngularTorque(current_torque);
	joint_wheel_fr->setAngularTorque(current_torque);
}

```

</details>
