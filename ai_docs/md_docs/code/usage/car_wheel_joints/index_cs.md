# A Car with Wheel Joints (CS)


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


The first thing we are going to address in this tutorial is the geometry of our car. It is possible to use any custom made model for the vehicle appearance. Every wheel and the frame will be individual independent [nodes](../../../objects/nodes/index.md) in the world, so make sure that your vehicle model includes separate meshes for the wheels and the frame.


Right now we are going to take the vehicle model from the content addon included in the SDK and then add some physical parameters to the geometry to achieve a viable driving simulation.


1. Let's create [an empty C# project](../../../sdk/projects/index_cs.md#creation).
2. Download the *[Eastern European Countryside add-on](../../../sdk/addons/eastern_european_countryside/index.md)* from Add-On Store at [https://store.unigine.com/](https://store.unigine.com/) and add it to the project by dragging into the project `data/` folder in the Asset Browser. In the *Import Package* window that opens, click the *Import Package* button and wait until the add-on contents are imported.
3. Launch the Editor via the *Open Editor* button. For your vehicle you can choose any of the minibus nodes located in `data/countryside/minibus` or [import](../../../editor2/assets_workflow/assets_create_import.md) your own model in any [supported file format](../../../editor2/assets_workflow/asset_types.md). ![](models.png) A minibus vehicle model has the body frame as the parent node and its wheels as child nodes. ![](hierarchy.png)
4. In the Asset Browser, right-click on a minibus node you like the most and choose *Place as Node Content*. Place the vehicle on the ground in the world. As we don't plan to use multiple instances of the car, we simply put all its parts directly to the scene, without the *NodeReference* container. ![](place.jpg)


## Step 2. Setting Up Camera


Let�s create a camera for a third-person view. While the camera follows the car, the player can control the viewing direction (rotate the camera) with the mouse. To achieve this, perform the following:


1. In the *World Nodes* window, delete the *first_person_controller* containing the default camera.
2. Create a custom *Persecutor Camera* to follow the car. Go to *Create -> Camera -> Persecutor* and then place it near the vehicle.
3. Check the **Main Player** option in the *Parameters* tab of the *PlayerPersecutor* to make it the default camera in the world.
4. Delete the default *Persecutor_Target* node from the *World Nodes* window hierarchy and set our **minibus** as the target node for the *PlayerPersecutor* camera instead. ![](target.png)
5. To put the camera closer to the vehicle, set the *Max Distance* parameter for the PlayerPersecutor to 8.
6. You can press the *F5* or *Run* button in the Editor to test out the resulting camera behavior. ![](play.png)


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


Now let�s [create a C# component](../../../principles/component_system/component_system_cs/index.md#create) to implement driving and steering functionality for the car. To achieve this, do the following:


1. In *Asset Browser*, right-click and select *Create Code -> C# Component*. Name it **Car**, [assign](../../../principles/component_system/component_system_cs/index.md#apply) it to the minibus node and then double-click on the newly created component to open it in an IDE. ![](component.png)
2. Get references to joints from the wheel nodes and define variables for the *velocity*, *acceleration* and *torque* values. <details> <summary>Car.cs | Close</summary> `Car.cs` ```csharp using System; using System.Collections; using System.Collections.Generic; using Unigine; public partial class Car : Component { // driving parameters public float acceleration = 50.0f; public float max_velocity = 90.0f; private float max_turn_angle = 30.0f; // nodes with the joints public Node wheel_bl = null; public Node wheel_br = null; public Node wheel_fl = null; public Node wheel_fr = null; // camera class public Player player = null; // wheel joints private JointWheel joint_wheel_bl = null; private JointWheel joint_wheel_br = null; private JointWheel joint_wheel_fl = null; private JointWheel joint_wheel_fr = null; // settings of input controls private Controls controls = null; // current driving parameters private float current_velocity = 0.0f; private float current_torque = 0.0f; private void Init() { // get the wheel joints from the nodes if (wheel_bl) joint_wheel_bl = wheel_bl.ObjectBody.GetJoint(0) as JointWheel; if (wheel_br) joint_wheel_br = wheel_br.ObjectBody.GetJoint(0) as JointWheel; if (wheel_fl) joint_wheel_fl = wheel_fl.ObjectBody.GetJoint(0) as JointWheel; if (wheel_fr) joint_wheel_fr = wheel_fr.ObjectBody.GetJoint(0) as JointWheel; // get the settings of input controls relevant to the player (camera) if (player) controls = player.Controls; } } ``` </details>
3. Then add *control inputs* processing to determine the current torque and velocity to be applied to wheel joints. <details> <summary>Car.cs | Close</summary> `Car.cs` ```csharp private void Update() { // get the time it took to render the previous frame float deltaTime = Game.IFps; current_torque = 0.0f; // process control inputs if (controls) { // set the torque and increase the current velocity if the forward button is pressed if (controls.GetState(Controls.STATE_FORWARD) != 0) { current_torque = default_torque; current_velocity = MathLib.Max(current_velocity, 0.0f); current_velocity += deltaTime * acceleration; } // set the torque and decrease the current velocity if the backward button is pressed else if (controls.GetState(Controls.STATE_BACKWARD) != 0) { current_torque = default_torque; current_velocity = MathLib.Min(current_velocity, 0.0f); current_velocity -= deltaTime * acceleration; } // exponentially decrease the current velocity when neither throttle nor brakes are applied else { current_velocity *= MathLib.Exp(-deltaTime); } } } ``` </details>
4. To move the car forward or backward, we are going to use [joint motors](../../../principles/physics/joints/index.md#motors) of the front wheels: Each physics frame, we apply current angular velocity and torque to the wheel joints based on the user input. <details> <summary>Car.cs | Close</summary> `Car.cs` ```csharp // actually apply the torque and velocity to the front wheel joints private void UpdatePhysics() { joint_wheel_fl.AngularVelocity = current_velocity; joint_wheel_fr.AngularVelocity = current_velocity; joint_wheel_fl.AngularTorque = current_torque; joint_wheel_fr.AngularTorque = current_torque; } ``` </details>

  - Setting a **positive** velocity value will move our car **forward**.
  - Setting a **negative** velocity value will move our car **backward**.


## Step 6. Implementing Steering and Braking


To provide the ability to turn left or right as well as the ability to slow down with brakes, we shall implement some additional logic that turns the front wheels and stops the rear ones. To achieve this, do the following:


1. Add the following code to the *Car* component to add the front wheels *turning* and *braking* support. <details> <summary>Car.cs | Close</summary> `Car.cs` ```csharp public float turn_speed = 50.0f; public float default_torque = 5.0f; public float car_base = 3.0f; public float car_width = 2.0f; private float current_turn_angle = 0.0f; private void Update() { // get the time it took to render the previous frame float deltaTime = Game.IFps; current_torque = 0.0f; // process control inputs if (controls) { /*...*/ // turn the front wheels based on the direction input if (controls.GetState(Controls.STATE_MOVE_LEFT) != 0) current_turn_angle += deltaTime * turn_speed; else if (controls.GetState(Controls.STATE_MOVE_RIGHT) != 0) current_turn_angle -= deltaTime * turn_speed; else { // get rid of the front wheel wiggle if (MathLib.Abs(current_turn_angle) < 0.25f) current_turn_angle = 0.0f; // align the front wheels if there are no more direction input current_turn_angle -= MathLib.Sign(current_turn_angle) * turn_speed * deltaTime; } // apply braking by maxing out the angular damping if the brake button is pressed if (controls.GetState(Controls.STATE_USE) != 0) { joint_wheel_bl.AngularDamping = 10000.0f; joint_wheel_br.AngularDamping = 10000.0f; } else { joint_wheel_bl.AngularDamping = 0.0f; joint_wheel_br.AngularDamping = 0.0f; } } // clamp the velocity and the front wheels turn angle current_velocity = MathLib.Clamp(current_velocity, -max_velocity, max_velocity); current_turn_angle = MathLib.Clamp(current_turn_angle, -max_turn_angle, max_turn_angle); // figure out the correct turn angle for the front wheels float angle_0 = current_turn_angle; float angle_1 = current_turn_angle; if (MathLib.Abs(current_turn_angle) > MathLib.EPSILON) { float radius = car_base / MathLib.Tan(current_turn_angle * MathLib.DEG2RAD); float radius_0 = radius - car_width * 0.5f; float radius_1 = radius + car_width * 0.5f; angle_0 = MathLib.Atan(car_base / radius_0) * MathLib.RAD2DEG; angle_1 = MathLib.Atan(car_base / radius_1) * MathLib.RAD2DEG; } joint_wheel_fr.Axis10 = MathLib.RotateZ(angle_1).GetColumn3(0); joint_wheel_fl.Axis10 = MathLib.RotateZ(angle_0).GetColumn3(0); } ``` </details>
2. In the Editor, assign wheels (*ObjectMeshStatic* nodes) and the camera (*PlayerPersecutor* node) to the corresponding **fields** of the *Car* component as specified below. ![](fields.png)


Congratulations! Now you can finally drive the car around the world. If the current physics of the car is not suitable for your needs, you can always fine tune the parameters of the wheel joints and achieve the results you need. Also, see the [Basic Programming How-To Livestream](https://youtu.be/ROy9oGPnABE) for the hands-on vehicle implementation and discussions. The full source code of the *Car* component is given below.


<details>
<summary>Car.cs | Close</summary>

`Car.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class Car : Component
{
	// driving parameters
	public float acceleration = 50.0f;
	public float max_velocity = 90.0f;
	private float max_turn_angle = 30.0f;
	public float turn_speed = 50.0f;
	public float default_torque = 5.0f;
	public float car_base = 3.0f;
	public float car_width = 2.0f;

	// nodes with the joints
	public Node wheel_bl = null;
	public Node wheel_br = null;
	public Node wheel_fl = null;
	public Node wheel_fr = null;

	// camera class
	public Player player = null;

	// wheel joints
	private JointWheel joint_wheel_bl = null;
	private JointWheel joint_wheel_br = null;
	private JointWheel joint_wheel_fl = null;
	private JointWheel joint_wheel_fr = null;

	// settings of input controls
	private Controls controls = null;

	// current driving parameters
	private float current_velocity = 0.0f;
	private float current_torque = 0.0f;
	private float current_turn_angle = 0.0f;

	private void Init()
	{
		// get the wheel joints from the nodes
		if (wheel_bl)
			joint_wheel_bl = wheel_bl.ObjectBody.GetJoint(0) as JointWheel;

		if (wheel_br)
			joint_wheel_br = wheel_br.ObjectBody.GetJoint(0) as JointWheel;

		if (wheel_fl)
			joint_wheel_fl = wheel_fl.ObjectBody.GetJoint(0) as JointWheel;

		if (wheel_fr)
			joint_wheel_fr = wheel_fr.ObjectBody.GetJoint(0) as JointWheel;

		// get the settings of input controls relevant to the player (camera)
		if (player)
			controls = player.Controls;
	}

	private void Update()
	{
		// get the time it took to render the previous frame
		float deltaTime = Game.IFps;

		current_torque = 0.0f;

		// process control inputs
		if (controls)
		{
			// set the torque and increase the current velocity if the forward button is pressed
			if (controls.GetState(Controls.STATE_FORWARD) != 0)
			{
				current_torque = default_torque;
				current_velocity = MathLib.Max(current_velocity, 0.0f);
				current_velocity += deltaTime * acceleration;
			}
			// set the torque and decrease the current velocity if the backward button is pressed
			else if (controls.GetState(Controls.STATE_BACKWARD) != 0)
			{
				current_torque = default_torque;
				current_velocity = MathLib.Min(current_velocity, 0.0f);
				current_velocity -= deltaTime * acceleration;
			}
			// exponentially decrease the current velocity when neither throttle nor brakes are applied
			else
			{
				current_velocity *= MathLib.Exp(-deltaTime);
			}
			/*...*/
			// turn the front wheels based on the direction input
			if (controls.GetState(Controls.STATE_MOVE_LEFT) != 0)
				current_turn_angle += deltaTime * turn_speed;
			else if (controls.GetState(Controls.STATE_MOVE_RIGHT) != 0)
				current_turn_angle -= deltaTime * turn_speed;
			else
			{
				// get rid of the front wheel wiggle
				if (MathLib.Abs(current_turn_angle) < 0.25f)
					current_turn_angle = 0.0f;

				// align the front wheels if there are no more direction input
				current_turn_angle -= MathLib.Sign(current_turn_angle) * turn_speed * deltaTime;
			}

			// apply braking by maxing out the angular damping if the brake button is pressed
			if (controls.GetState(Controls.STATE_USE) != 0)
			{
				joint_wheel_bl.AngularDamping = 10000.0f;
				joint_wheel_br.AngularDamping = 10000.0f;
			}
			else
			{
				joint_wheel_bl.AngularDamping = 0.0f;
				joint_wheel_br.AngularDamping = 0.0f;
			}
		}
		// clamp the velocity and the front wheels turn angle
		current_velocity = MathLib.Clamp(current_velocity, -max_velocity, max_velocity);
		current_turn_angle = MathLib.Clamp(current_turn_angle, -max_turn_angle, max_turn_angle);

		// figure out the correct turn angle for the front wheels
		float angle_0 = current_turn_angle;
		float angle_1 = current_turn_angle;
		if (MathLib.Abs(current_turn_angle) > MathLib.EPSILON)
		{
			float radius = car_base / MathLib.Tan(current_turn_angle * MathLib.DEG2RAD);
			float radius_0 = radius - car_width * 0.5f;
			float radius_1 = radius + car_width * 0.5f;

			angle_0 = MathLib.Atan(car_base / radius_0) * MathLib.RAD2DEG;
			angle_1 = MathLib.Atan(car_base / radius_1) * MathLib.RAD2DEG;
		}

		joint_wheel_fr.Axis10 = MathLib.RotateZ(angle_1).GetColumn3(0);
		joint_wheel_fl.Axis10 = MathLib.RotateZ(angle_0).GetColumn3(0);
	}
	// actually apply the torque and velocity to the front wheel joints
	private void UpdatePhysics()
	{
		joint_wheel_fl.AngularVelocity = current_velocity;
		joint_wheel_fr.AngularVelocity = current_velocity;

		joint_wheel_fl.AngularTorque = current_torque;
		joint_wheel_fr.AngularTorque = current_torque;
	}
}

```

</details>
