# Unigine::JointSuspension Class (CS)

**Inherits from:** Joint


> **Warning:** This joint type is deprecated and will be removed in the upcoming releases. It is recommended to use the [Wheel Joint](../../../api/library/physics/class.jointwheel_cs.md) instead.


This class is used to create a suspension joint. The bodies that represent both a frame and a wheel must be [rigid bodies](../../../principles/physics/bodies/rigid/index.md).


### Example


The following code illustrates connection of two [rigid bodies](../../../api/library/physics/class.bodyrigid_cs.md) (frame and wheel) using a suspension joint.


```csharp
	JointSuspension joint = new JointSuspension(frame, wheel);

	// setting joint anchor coordinates
	joint.WorldAnchor = wheel.Object.WorldTransform * new Vec3(0.0f);

	// setting joint axes coordinates
	joint.WorldAxis0 = new vec3(0.0f, 0.0f, 1.0f);
	joint.WorldAxis1 = new vec3(0.0f, 1.0f, 0.0f);

	// setting linear damping and spring rigidity
	joint.LinearDamping = 2.0f;
	joint.LinearSpring = 200.0f;

	// setting lower and upper suspension ride limits [-0.5; 0.0]
	joint.LinearLimitFrom = -0.5f;
	joint.LinearLimitTo = 0.0f;

	// setting target suspension height
	joint.LinearDistance = 0.5f;

	// setting maximum angular velocity and torque
	joint.AngularVelocity = -20.0f;
	joint.AngularTorque = 10.0f;

	// setting common joint constraint parameters
	joint.LinearRestitution = 0.2f;
	joint.AngularRestitution = 0.2f;
	joint.LinearSoftness = 0.2f;
	joint.AngularSoftness = 0.2f;

	// setting number of iterations
	joint.NumIterations = 8;

```


### See Also


- UnigineScript samples:

  -
  -
  -


## JointSuspension Class

### Properties

## 🔒︎ float CurrentLinearDistance

The suspension compression.
## 🔒︎ float CurrentAngularVelocity

The velocity of wheel rotation.
## float AngularVelocity

The target velocity of wheel rotation.
## float AngularTorque

The maximum torque of the attached angular motor. **0** means that the motor is not attached.
## float AngularDamping

The angular damping of the joint (wheel rotation damping).
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

## JointSuspension ( )

Constructor. Creates a suspension joint with an anchor at the origin of the world coordinates.
## JointSuspension ( Body body0 , Body body1 )

Constructor. Creates a suspension joint connecting two given bodies. An anchor is placed between centers of mass of the bodies.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - Frame to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - Wheel to be connected with the joint.

## JointSuspension ( Body body0 , Body body1 , vec3 anchor , vec3 axis0 , vec3 axis1 )

Constructor. Creates a suspension joint connecting two given bodies with specified suspension and spindle axis coordinates and an anchor placed at specified coordinates.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - Frame to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - Wheel to be connected with the joint.
- *vec3* **anchor** - Anchor coordinates.
- *vec3* **axis0** - Suspension axis coordinates.
- *vec3* **axis1** - Wheel spindle axis coordinates.
