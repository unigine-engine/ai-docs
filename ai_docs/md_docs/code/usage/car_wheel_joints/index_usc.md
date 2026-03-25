# A Car with Wheel Joints (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


![Simple car with wheel joints](car_joints.jpg)

*Simple car with wheel joints*


This example shows how to:


- [Create a simple car](#geometry) with a frame and wheels attached to it using [wheel joints](../../../principles/physics/joints/index.md#wheel).
- [Enable car movement](#motors_usc) using [joint motors](../../../principles/physics/joints/index.md#motors).
- [Use keyboard](#controls_usc) to control car movement.


The **basic workflow** of creating a simple car with keyboard control is as follows:


1. Create car geometry: frame and wheels.
2. Assign [rigid bodies](../../../principles/physics/bodies/rigid/index.md) and [collision shapes](../../../principles/physics/shapes/index.md) to the frame and just a rigid body to all the wheels.
3. Set up masses for the wheels and the frame. > **Notice:** Do not use real masses (e.g. 2000 kg for the frame and 10 kg for the wheels), as joints may become unstable! It might be better to use 64 kg for the body and 25 kg for each wheel to provide realistic behavior.
4. Connect the wheels to the frame using [wheel joints](../../../principles/physics/joints/index.md#wheel). Set up joint parameters.
5. Enable car movement using [joint motors](../../../principles/physics/joints/index.md#motors) and assign movement control to corresponding keyboard keys.


## Creating Geometry and Adding Some Physics


The first thing we are going to address in this tutorial is the geometry of our car. We are going to create a rectangular car body and four wheels. We are also going to add some physical parameters to the geometry. So, we need two functions:


- The first one to create a box with specified parameters representing the car body:


```cpp
/// function, creating a car body having a specified size, color and transformation with a body and a shape
Object createBody(string name, Vec3 size, float mass, Vec4 color, Mat4 transform)
{
	// creating a car body and setting up its parameters (name, color and transformation)
	ObjectMeshDynamic OMD = Unigine::createBox(size);

	OMD.setWorldTransform(transform);
	OMD.setMaterialParameterFloat4("albedo_color", color, 0);
	OMD.setCollision(1, 0);
	OMD.setName(name);

	// adding physics, i.e. a rigid body and a box shape with specified mass
	BodyRigid body = class_remove(new BodyRigid(OMD));
	ShapeBox shape = class_remove(new ShapeBox(size));

	shape.setMass(mass);
	body.addShape(shape, translate(0.0f, 0.0f, 0.0f));

	body.setFreezable(0);

	return OMD;
}

```


- The second one to create a cylinder with specified parameters representing a wheel:


```cpp
/// function, creating a wheel having a specified size and transformation
/// with a physical body and attaching it to the frame
Object createWheel(Node frame, string name, float radius, float height, float mass, Mat4 transform)
{
	// creating a wheel, adding it to the frame as a child,
	// and setting up its parameters (name, color and transformation)
	ObjectMeshDynamic OMD = Unigine::createCylinder(radius, height, 1, 32);
	frame.addChild(OMD);
	OMD.setTransform(transform);
	OMD.setMaterialParameterFloat4("albedo_color", Vec4(0.1f, 0.1f, 0.1f, 1.0f), 0);
	OMD.setCollision(1, 0);
	OMD.setName(name);

	// adding a rigid body
	class_remove(new BodyRigid(OMD));

	return OMD;
}

```


Now using these functions we can create our car. We are going to use *[DynamicMesh](../../../api/library/objects/class.objectmeshdynamic_usc.md)* objects for the frame and four wheels. For a proper mass balance let us set frame mass equal to 64 kg and the mass of each wheel - to 25 kg.


```cpp
// defining DynamicMesh objects for the frame and four wheels
ObjectMeshDynamic car_frame;
ObjectMeshDynamic wheels[4];

// creating car frame
car_frame = createBody("car_frame", Vec3(frame_width, frame_length, frame_height), 64.0f, Vec4(1.0f, 0.0f, 0.0f, 1.0f), transform);

// creating car wheels
// front left wheel
wheels[0] = createWheel(car_frame, "car_wheel_f_l", wheel_radius, wheel_width, 25.0f, Mat4(translate( -(frame_width + wheel_width)/2 - delta, frame_length/2 - wheel_radius,   -frame_height/2)  * rotateY(90.0f)));

// front right wheel
wheels[1] = createWheel(car_frame, "car_wheel_f_r", wheel_radius, wheel_width, 25.0f, Mat4(translate(  (frame_width + wheel_width)/2 + delta, frame_length/2 - wheel_radius,   -frame_height/2) * rotateY(90.0f)));

// rear left wheel
wheels[2] = createWheel(car_frame, "car_wheel_r_l", wheel_radius, wheel_width, 25.0f, Mat4(translate(-(frame_width + wheel_width)/2 - delta, -0.25f * frame_length,-frame_height/2) * rotateY(90.0f)));

// rear right wheel
wheels[3] = createWheel(car_frame, "car_wheel_r_r", wheel_radius, wheel_width, 25.0f, Mat4(translate((frame_width + wheel_width)/2 + delta, -0.25f * frame_length, -frame_height/2) * rotateY(90.0f)));

```


## Adding and Setting Up Joints


Now that we have the frame and four wheels we can attach each wheel to the frame with a [wheel joint](../../../principles/physics/joints/index.md#wheel).


To create a wheel joint we call the *[JointWheel()](../../../api/library/physics/class.jointwheel_usc.md#JointWheel_constPtrBody_constPtrBody_constMathVec3_constMathvec3_constMathvec3)* constructor and then set necessary parameters:


1. Rigid body of the car frame
2. Rigid body of the wheel
3. Anchor point coordinates (this point is determined by the position(translation) of the wheel relative to the frame)
4. Coordinates of suspension axis (a vertical axis along which a wheel moves vertically and rotates when steering)
5. Coordinates of wheel spindle axis (a horizontal around which a wheel rotates when moving forward or backward)


```cpp
for(int i = 0; i < 4; i++)
{
	wheel_joints[i] = class_remove(new JointWheel(car_frame.getBodyRigid(), // car frame body
													wheels[i].getBodyRigid(), // car wheel body
													);

	// calculating axes and anchor coordinates
	Object frame = wheel_body.getObject();
	Mat4 wheel_t = frame.getTransform();
	Vec3 anchor0 = Vec3(wheel_t.col3);
	Vec3 anchor1 = Vec3_zero;
	vec3 axis00 = vec3(0.0f, 0.0f, 1.0f);
	vec3 axis10 = vec3(1.0, 0.0, 0.0);
	vec3 axis11 = rotation(wheel_t) * axis10;

	// setting up joint's anchor and axes
	joint.setAnchor0(anchor0);
	joint.setAnchor1(anchor1);

	joint.setAxis00(axis00);
	joint.setAxis10(axis10);
	joint.setAxis11(axis11);

	// setting restitution parameters
	wheel_joints[i].setLinearRestitution(0.1f);
	wheel_joints[i].setAngularRestitution(0.1f);

	// setting linear damping and spring rigidity
	wheel_joints[i].setLinearDamping(2.0f);
	wheel_joints[i].setLinearSpring(40.0f);

	// setting lower and upper suspension ride limits [-0.15; 0.15] and target distance
	wheel_joints[i].setLinearLimitFrom(-0.15f);
	wheel_joints[i].setLinearLimitTo(0.15f);
	wheel_joints[i].setLinearDistance(0.0f);

	// setting number of iterations
	wheel_joints[i].setNumIterations(8);
}

```


## Using Joint Motors


So, we have a car, let's make it move.


To move the car forward or backward, we are going to use [joint motors](../../../principles/physics/joints/index.md#motors) of the rear wheels (2 and 3):


- Setting a **positive** velocity value will move our car **forward**.
- Setting a **negative** velocity value will move our car **backward**.


See the following code:


```cpp

wheel_joints[2].setAngularVelocity(velocity);
wheel_joints[3].setAngularVelocity(velocity);

wheel_joints[2].setAngularTorque(torque);
wheel_joints[3].setAngularTorque(torque);


```


To steer the car left or right, we are going to change *Axis10* coordinates of the front wheels (0 and 1) using *[setAxis10()](../../../api/library/physics/class.jointsuspension_usc.md#setAxis10_vec3_void)* method:


```cpp

wheel_joints[0].setAxis10(rotateZ(angle_0).getColumn3(0));
wheel_joints[1].setAxis10(rotateZ(angle_1).getColumn3(0));


```


To stop the car, we are going to set a high angular damping value for all wheels via the *[setAngularDamping()](../../../api/library/physics/class.jointwheel_usc.md#setAngularDamping_float_void)* method:


```cpp

for (int i = 0; i < 4; i++)
	wheel_joints[i].setAngularDamping(20000.0f);


```


## Adding Keyboard Controls


To add keyboard control, we are going to make a handler for the keys that we need. The handler must be put in the world script *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function to be called for each frame. We are going to update car physics (joint motors) in the *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* method.


```cpp
int update()
{
	// forward and backward movement by setting joint motor's velocity and torque
	if(engine.controls.getState(CONTROLS_STATE_FORWARD) || engine.controls.getState(CONTROLS_STATE_TURN_UP)) {
		// TODO: increase velocity by delta
		// set desired torque
	} else if(engine.controls.getState(CONTROLS_STATE_BACKWARD) || engine.controls.getState(CONTROLS_STATE_TURN_DOWN)) {
		// TODO: decrease velocity by delta
		// set desired torque
	} else {
		// TODO: decrease velocity gradually
	}

	// clamp velocity value
	velocity = clamp(velocity,-90.0f,90.0f);

	// steering left and right by changing Axis01 for front wheel joints
	if(engine.controls.getState(CONTROLS_STATE_MOVE_LEFT) || engine.controls.getState(CONTROLS_STATE_TURN_LEFT)) {
		// TODO: increase steering angle by some delta
	} else if(engine.controls.getState(CONTROLS_STATE_MOVE_RIGHT) || engine.controls.getState(CONTROLS_STATE_TURN_RIGHT)) {
		// TODO: decrease steering angle
	} else {
		// TODO: return steering angle to zero value gradually
	}

	// clamp steering angle value
	angle = clamp(angle,-30.0f,30.0f);

	// TODO: calculate steering angles for front joints (angle_0 and angle_1)

	// set new Axis10 coordinates for front joints
	wheel_joints[0].setAxis10(Vec3(rotateZ(angle_0).col0));
	wheel_joints[1].setAxis10(Vec3(rotateZ(angle_1).col0));

	if(engine.controls.getState(CONTROLS_STATE_USE)) {
		// TODO: set a very high angular damping value for all joints
		// set velocity to zero
	} else {
		// TODO: set angular damping value to zero for all joints
	}

	return 1;
}

int updatePhysics ()
{
	// set angular velocity for rear joints
	wheel_joints[2].setAngularVelocity(velocity);
	wheel_joints[3].setAngularVelocity(velocity);

	// set torque for rear joints
	wheel_joints[2].setAngularTorque(torque);
	wheel_joints[3].setAngularTorque(torque);

	return 1;
}

```


## Putting it All Together


In this section let's sum up all described above and create a new class for our car. The final code for our tutorial will be as follows:


```cpp
#include <core/scripts/primitives.h>
Car car = NULL;

/// function setting up bodies for a wheel joint
void setBodies(JointWheel joint, BodyRigid car_body, BodyRigid wheel_body)
{
	joint.setBody0(car_body);
	joint.setBody1(wheel_body);
	Object frame = wheel_body.getObject();
	Mat4 wheel_t = frame.getTransform();

	Vec3 anchor0 = Vec3(wheel_t.col3);
	Vec3 anchor1 = Vec3_zero;

	vec3 axis00 = vec3(0.0f, 0.0f, 1.0f);
	vec3 axis10 = vec3(1.0, 0.0, 0.0);

	vec3 axis11 = rotation(wheel_t) * axis10;

	// setting up joint's anchor and axes
	joint.setAnchor0(anchor0);
	joint.setAnchor1(anchor1);

	joint.setAxis00(axis00);
	joint.setAxis10(axis10);
	joint.setAxis11(axis11);
}

/// function, creating a car body having a specified size, color and transformation with a body and a shape
Object createBody(string name, Vec3 size, float mass, Vec4 color, Mat4 transform)
{
	// creating a car body and setting up its parameters (name, color and transformation)
	ObjectMeshDynamic OMD = Unigine::createBox(size);

	OMD.setWorldTransform(transform);
	OMD.setMaterialParameterFloat4("albedo_color", color, 0);
	OMD.setName(name);

	// enabling collision detection for the frame
	OMD.setCollision(1, 0);

	// adding physics, i.e. a rigid body and a box shape with specified mass
	BodyRigid body = class_remove(new BodyRigid(OMD));
	ShapeBox shape = class_remove(new ShapeBox(size));

	shape.setMass(mass);
	body.addShape(shape, translate(0.0f, 0.0f, 0.0f));

	body.setFreezable(0);

	return OMD;
}

/// function, creating a wheel having a specified size, color and transformation with a body
Object createWheel(Node frame, string name, float radius, float height, float mass, Mat4 transform)
{
	// creating a wheel, adding it to the frame as a child, and setting up its parameters (name, color and transformation)
	ObjectMeshDynamic OMD = Unigine::createCylinder(radius, height, 1, 32);
	frame.addChild(OMD);
	OMD.setTransform(transform);
	OMD.setMaterialParameterFloat4("albedo_color", Vec4(0.1f, 0.1f, 0.1f, 1.0f), 0);
	OMD.setName(name);

	// enabling collision detection for the wheel
	OMD.setCollision(1, 0);

	// adding a rigid body
	class_remove(new BodyRigid(OMD));

	return OMD;
}

/// Car class definition
class Car
{
	// car parameters
	float frame_width;
	float frame_height;
	float frame_length;
	float wheel_radius;
	float wheel_width;

	// car elements
	ObjectMeshDynamic car_frame;
	ObjectMeshDynamic wheels[4];
	JointWheel wheel_joints[4];

	// initialization of movement parameters
	float angle = 0.0f;
	float velocity = 0.0f;
	float torque = 0.0f;

	/// Car constructor creating a car with specified frame and wheel parameters
	Car(float blength, float bwidth, float bheight, float wradius, float wwidth, float wmass, Mat4 transform)
	{

		frame_width = bwidth;
		frame_height = bheight;
		frame_length = blength;
		wheel_radius = wradius;
		wheel_width = wwidth;
		float delta = 0.2f;

		car_frame = createBody("car_frame", Vec3(frame_width, frame_length, frame_height), 64.0f, Vec4(1.0f, 0.0f, 0.0f, 1.0f), transform);

		// initialization of wheels
		wheels[0] = createWheel(car_frame, "car_wheel_f_l", wheel_radius, wheel_width, 25.0f, Mat4(translate( -(frame_width + wheel_width)/2 - delta, frame_length/2 - wheel_radius,   -frame_height/2)  * rotateY(90.0f)));
		wheels[1] = createWheel(car_frame, "car_wheel_f_r", wheel_radius, wheel_width, 25.0f, Mat4(translate(  (frame_width + wheel_width)/2 + delta, frame_length/2 - wheel_radius,   -frame_height/2) * rotateY(90.0f)));
		wheels[2] = createWheel(car_frame, "car_wheel_r_l", wheel_radius, wheel_width, 25.0f, Mat4(translate(-(frame_width + wheel_width)/2 - delta, -0.25f * frame_length,			-frame_height/2) * rotateY(90.0f)));
		wheels[3] = createWheel(car_frame, "car_wheel_r_r", wheel_radius, wheel_width, 25.0f, Mat4(translate(	  (frame_width + wheel_width)/2 + delta, -0.25f * frame_length, 		  -frame_height/2) * rotateY(90.0f)));

		// initialization of wheel joints
		for(int i=0; i < 4; i++)
		{
			wheel_joints[i] = class_remove(new JointWheel());

			// setting bodies and wheel parameters
			setBodies(wheel_joints[i], car_frame.getBodyRigid(), wheels[i].getBodyRigid());
			wheel_joints[i].setWheelRadius(wradius);
			wheel_joints[i].setWheelMass(wmass);

			// setting restitution parameters
			wheel_joints[i].setLinearRestitution(0.1f);
			wheel_joints[i].setAngularRestitution(0.1f);

			// setting linear damping and spring rigidity
			wheel_joints[i].setLinearDamping(400.0f);
			wheel_joints[i].setLinearSpring(100.0f);

			// setting lower and upper suspension ride limits [-0.15; 0.15]
			wheel_joints[i].setLinearLimitFrom(-0.15f);
			wheel_joints[i].setLinearLimitTo(0.15f);
			wheel_joints[i].setLinearDistance(0.0f);

			// setting number of iterations
			wheel_joints[i].setNumIterations(8);
		}

	}

	/// method updating current car state with a keyboard control handler
	int  update()
	{
		float ifps = engine.game.getIFps();

		// forward and backward movement by setting joint motor's velocity and torque
		if(engine.controls.getState(CONTROLS_STATE_FORWARD) || engine.controls.getState(CONTROLS_STATE_TURN_UP)) {
			velocity = max(velocity,0);
			velocity += ifps * 50.0f;
			torque = 15.0f;
		} else if(engine.controls.getState(CONTROLS_STATE_BACKWARD) || engine.controls.getState(CONTROLS_STATE_TURN_DOWN)) {
			velocity = min(velocity,0);
			velocity -= ifps * 50.0f;
			torque = 15.0f;
		} else {
			velocity *= exp(-ifps);
		}
		velocity = clamp(velocity,-90.0f,90.0f);

		// steering left and right by changing Axis01 for front wheel joints
		if(engine.controls.getState(CONTROLS_STATE_MOVE_LEFT) || engine.controls.getState(CONTROLS_STATE_TURN_LEFT)) {
			angle += ifps * 100.0f;
		} else if(engine.controls.getState(CONTROLS_STATE_MOVE_RIGHT) || engine.controls.getState(CONTROLS_STATE_TURN_RIGHT)) {
			angle -= ifps * 100.0f;
		} else {
			if(abs(angle) < 0.25f) angle = 0.0f;
			else angle -= sign(angle) * ifps * 45.0f;
		}
		angle = clamp(angle,-30.0f,30.0f);

		// calculating steering angles for front joints (angle_0 and angle_1)
		float base = 3.3f;
		float width = 3.0f;
		float angle_0 = angle;
		float angle_1 = angle;
		if(abs(angle) > EPSILON) {
			float radius = base / tan(angle * DEG2RAD);
			angle_0 = atan(base / (radius + width / 2.0f)) * RAD2DEG;
			angle_1 = atan(base / (radius - width / 2.0f)) * RAD2DEG;
		}

		wheel_joints[0].setAxis10(Vec3(rotateZ(angle_0).col0));
		wheel_joints[1].setAxis10(Vec3(rotateZ(angle_1).col0));

		// enabling or disabling a brake
		if(engine.controls.getState(CONTROLS_STATE_USE)) {
			velocity = 0.0f;
			for (int i = 0; i < 4; i++)
				wheel_joints[i].setAngularDamping(20000.0f);
		} else {
			for (int i = 0; i < 4; i++)
				wheel_joints[i].setAngularDamping(0.0f);
		}

		return 1;
	}

	/// method updating car physics
	int updatePhysics()
	{
		// set angular velocity for rear joints
		wheel_joints[0].setAngularVelocity(velocity);
		wheel_joints[1].setAngularVelocity(velocity);

		// set torque for rear joints
		wheel_joints[0].setAngularTorque(torque);
		wheel_joints[1].setAngularTorque(torque);

		return 1;
	}
};

int init() {

	// setting up physics parameters
	engine.physics.setGravity(vec3(0.0f,0.0f,-9.8f * 2.0f));
	engine.physics.setFrozenLinearVelocity(0.1f);
	engine.physics.setFrozenAngularVelocity(0.1f);

	//enabling collision for the ground
	Object ground = node_cast(engine.world.getNodeByName("ground"));
	if (ground != NULL)
	{
		ground.setCollision(1, 0);
		ground.setPhysicsIntersection(1, 0);
	}

	//creating a car with specified parameters
	car = new Car(4.0f, 2.0f, 0.5f, 0.5f, 0.5f, 25.0f, translate(Vec3(0.0f, 0.0f, 1.0f)));

	// setting up player and controls
	PlayerPersecutor player = new PlayerPersecutor();
	player.setFixed(1);
	player.setTarget(car.car_frame);
	player.setMinDistance(6.0f);
	player.setMaxDistance(11.0f);
	player.setPosition(Vec3(0.0f, -10.0f, 6.0f));
	player.setControlled(0);
	engine.game.setPlayer(player);

	return 1;
}

int update() {

	// updating current car state
	car.update();

	return 1;
}

int updatePhysics() {

	// updating car physics
	car.updatePhysics();

	return 1;
}

```
