# Unigine::JointWheel Class (CS)

**Inherits from:** Joint


This class is used to create [ray-cast](../../../principles/physics/joints/index.md#vehicles) wheels. Both a frame and a wheel are [rigid bodies](../../../principles/physics/bodies/rigid/index.md). There is no need to assign a shape to the wheel: ray casting is used to detect collision of the wheel with a surface.


### Example


The following code illustrates connection of two [rigid bodies](../../../api/library/physics/class.bodyrigid_cs.md) (frame and wheel) using a wheel joint.


```csharp
	JointWheel joint = new JointWheel(frame, wheel);

	// setting joint anchor coordinates
	joint.WorldAnchor = wheel.Object.WorldTransform * new Vec3(0.0f);

	// setting joint axes coordinates
	joint.WorldAxis0 = new vec3(0.0f, 0.0f, 1.0f);
	joint.WorldAxis1 = new vec3(0.0f, 1.0f, 0.0f);

	// setting linear damping and spring rigidity
	joint.LinearDamping = 200.0f;
	joint.LinearSpring = 100.0f;

	// setting lower and upper suspension ride limits [-1.0; 0.0]
	joint.LinearLimitFrom = -1.0f;
	joint.LinearLimitTo = 0.0f;

	// setting target suspension height
	joint.LinearDistance = 0.5f;

	// setting maximum angular velocity and torque
	joint.AngularVelocity = -20.0f;
	joint.AngularTorque = 10.0f;

	// setting wheel parameters
	joint.WheelRadius = 0.5f;
	joint.WheelMass = 4.0f;
	joint.WheelThreshold = 0.1f;

	// setting tyre friction parameters
	joint.TangentFriction = 4.0f;
	joint.BinormalFriction = 5.0f;

	// setting number of iterations
	joint.NumIterations = 8;

```


### See Also


- Usage example: [Creating a Car with Wheel Joints](../../../code/usage/car_wheel_joints/index_cs.md)
- UnigineScript samples:

  -
  -


## JointWheel Class

### Properties

## 🔒︎ float CurrentSlipRatio

The ratio of wheel spin to ground speed.
## 🔒︎ float CurrentSlipAngle

The angle between the wheel direction and the frame direction.
## float WheelThreshold

The threshold difference between the wheel and ground velocities. When it is too small, the longitudinal force is scaled down to prevent unnatural vibrations.
## float WheelRadius

The radius of the attached wheel.
## float WheelMass

The mass of the attached wheel.
> **Notice:** If *g* (Earth's gravity) equals to 9.8 m/s 2, and 1 unit equals to 1 m, the mass is measured in kilograms.


## float TangentFriction

The longitudinal (forward) friction of the tire.
## float TangentAngle

The coefficient specifying how fast the optimal longitudinal force can be achieved. The larger this value, the more is the impulse produced by the tire.
## float BinormalFriction

The lateral (sideways) friction of the tire.
## float BinormalAngle

The coefficient specifying how fast the optimal lateral force can be achieved. The larger this value, the more is the impulse produced by the tire.
## float CurrentAngularVelocity

The rotation velocity of the attached wheels.
## float AngularVelocity

The target velocity of wheel rotation.
## float AngularTorque

The maximum torque of the attached angular motor. **0** means that the motor is not attached.
## float AngularDamping

The angular damping of the joint (wheel rotation damping).
## float CurrentLinearDistance

The suspension compression (i.e. the length of the suspension).
## float LinearSpring

The rigidity coefficient of the suspension. **0** means that the suspension is not attached.
## float LinearLimitTo

The high limit of the suspension ride. This limit specifies how far a connected body can move along the joint axis.
## float LinearLimitFrom

The low limit of the suspension ride. This limit specifies how far a connected body can move along the joint axis.
## float LinearDistance

The target height of the suspension.
## float LinearDamping

The linear damping of the suspension.
## int PhysicsIntersectionMask

The [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) of the joint.
## vec3 WorldAxis0

The suspension axis in the world coordinates.
## vec3 WorldAxis1

The wheel spindle axis in the world coordinates.
## vec3 Axis00

The coordinates of suspension axis, along which a wheel moves vertically. This is a shock absorber.
## vec3 Axis10

The wheel spindle axis in coordinates of the frame (body 0): an axis around which a wheel rotates when moving forward (or backward).
![](../../../principles/physics/joints/wheel_joint1.jpg)


## vec3 Axis11

The wheel spindle axis in coordinates of the wheel (body 1): an axis around which a wheel rotates when steering.
![](../../../principles/physics/joints/wheel_joint1.jpg)


### Members

---

## JointWheel ( )

Constructor. Creates a wheel joint with an anchor at the origin of the world coordinates.
## JointWheel ( Body body0 , Body body1 )

Constructor. Creates a wheel joint connecting two given bodies. An anchor is placed between centers of mass of the bodies.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - Frame to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - Wheel to be connected with the joint.

## JointWheel ( Body body0 , Body body1 , vec3 anchor , vec3 axis0 , vec3 axis1 )

Constructor. Creates a wheel joint connecting two given bodies with specified suspension and spindle axis coordinates and an anchor placed at specified coordinates.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - Frame to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - Wheel to be connected with the joint.
- *vec3* **anchor** - Anchor coordinates.
- *vec3* **axis0** - Suspension axis coordinates.
- *vec3* **axis1** - Wheel spindle axis coordinates.

## vec3 GetContactNormal ( )

Returns a normal of a point of contact with the ground, in world coordinates.
### Return value

Normal.
## Object GetContactObject ( )

Returns an object representing the ground.
### Return value

Ground object.
## vec3 GetContactPoint ( )

Returns a point of contact with the ground, in world coordinates.
### Return value

Point coordinates.
## Shape GetContactShape ( )

Returns a shape of the object representing the ground.
### Return value

Shape of the ground object.
## int GetContactSurface ( )

Returns a surface of a ground object, which is in contact.
### Return value

Surface number.
## void SetCanBeUnderTerrain ( bool val )

Sets a value indicating if the *Wheel Joint* should be used under the surface of the terrain (drive in an underground parking or tunnel). This flag ensures proper behavior of the joint underground , otherwise the *Wheel Joint* will tend to pop up on the terrain surface above.
### Arguments

- *bool* **val** - true if the *Wheel Joint* is to be used under the surface of the terrain; otherwise, false.
