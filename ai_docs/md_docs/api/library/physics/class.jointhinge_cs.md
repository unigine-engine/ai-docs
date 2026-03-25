# Unigine::JointHinge Class (CS)

**Inherits from:** Joint


This class is used to create [hinge joints](../../../principles/physics/joints/index.md#hinge).


### Example


The following code illustrates connection of two [bodies](../../../api/library/physics/class.body_cs.md) (b0 and b1) using a hinge joint.


```csharp
	JointHinge joint = new JointHinge(b0, b1);

	// setting joint axis coordinates
	joint.WorldAxis = new vec3(1.0f, 0.0f, 0.0f);

	// setting common joint constraint parameters
	joint.LinearRestitution = 0.4f;
	joint.AngularRestitution = 0.4f;
	joint.LinearSoftness = 0.4f;
	joint.AngularSoftness = 0.4f;

	// setting angular damping
	joint.AngularDamping = 8.0f;

	// setting angular limits, in degrees [-20; 20]
	joint.AngularLimitFrom = -20.0f;
	joint.AngularLimitTo = 20.0f;

	// setting spring rigidity coefficient
	joint.AngularSpring = 8.0f;

	// setting number of iterations
	joint.NumIterations = 16;

```


### See Also


- Usage example: [Creating a Simple Mechanism Using Various Types of Joints](../../../code/usage/simple_mechanism_joints/index_cs.md)
- UnigineScript samples:

  -
  -
  -


## JointHinge Class

### Properties

## 🔒︎ float CurrentAngularVelocity

The velocity of the motor, i.e. the difference between angular velocities of two bodies connected with a hinge relative the hinge axis.
> **Notice:** The valid velocity is returned only if both bodies are of [BodyRigid](../../../api/library/physics/class.bodyrigid_cs.md) type. Otherwise, **0** is returned.


## 🔒︎ float CurrentAngularAngle

The angle between the bodies.
## float AngularVelocity

The target velocity of the attached angular motor.
## float AngularSpring

The rigidity coefficient of the angular spring. **0** means that the spring is not attached.
## float AngularLimitTo

The high rotation limit angle. Rotation limit specifies how much a connected body can rotate around the joint axis
## float AngularLimitFrom

The low rotation limit angle. Rotation limit specifies how much a connected body can rotate around the joint axis.
## float AngularTorque

The maximum torque of the attached angular motor. **0** means that the motor is not attached.
## float AngularDamping

The angular damping of the joint.
## float AngularAngle

The target angle of the attached angular spring. The spring tries to rotate the connected bodies so that they make this angle.
## vec3 WorldAxis

The joint axis. The joint axis is calculated based on the axes of the connected bodies.
## vec3 Axis0

The axis of the first connected body.
## vec3 Axis1

The axis of the second connected body.
### Members

---

## JointHinge ( )

Constructor. Creates a hinge joint with an anchor at the origin of the world coordinates.
## JointHinge ( Body body0 , Body body1 )

Constructor. Creates a hinge joint connecting two given bodies. An anchor is placed between centers of mass of the bodies.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - First body to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - Second body to be connected with the joint.

## JointHinge ( Body body0 , Body body1 , vec3 anchor , vec3 axis )

Constructor. Creates a hinge joint connecting two given bodies with specified axis coordinates and an anchor placed at specified coordinates.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - First body to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - Second body to be connected with the joint.
- *vec3* **anchor** - Anchor coordinates.
- *vec3* **axis** - Axis coordinates.
