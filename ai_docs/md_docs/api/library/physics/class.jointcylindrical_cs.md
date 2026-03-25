# Unigine::JointCylindrical Class (CS)

**Inherits from:** Joint


This class is used to create [cylindrical joints](../../../principles/physics/joints/index.md#cylindrical).


### Example


The following code illustrates connection of two [bodies](../../../api/library/physics/class.body_cs.md) (b0 and b1) using a cylindrical joint.


```csharp
JointCylindrical joint = new JointCylindrical(b0, b1);

	// setting joint axis coordinates
	joint.WorldAxis = new vec3(0.0f, 0.0f, 1.0f);

	// setting common joint constraint parameters
	joint.LinearRestitution = 0.4f;
	joint.AngularRestitution = 0.4f;
	joint.LinearSoftness = 0.4f;
	joint.AngularSoftness = 0.4f;

	// setting linear and angular damping
	joint.LinearDamping = 4.0f;
	joint.AngularDamping = 2.0f;

	// setting linear limits [-1.5; 1.5]
	joint.LinearLimitFrom = -1.5f;
	joint.LinearLimitTo = 1.5f;

	// setting number of iterations
	joint.NumIterations = 16;

```


### See Also


- Usage example: [Creating a Simple Mechanism Using Various Types of Joints](../../../code/usage/simple_mechanism_joints/index_cs.md)
- UnigineScript samples:

  -
  -


## JointCylindrical Class

### Properties

## 🔒︎ float CurrentLinearVelocity

The velocity of the linear motor.
## 🔒︎ float CurrentLinearDistance

The distance between the bodies.
## 🔒︎ float CurrentAngularVelocity

The velocity of the angular motor.
## 🔒︎ float CurrentAngularAngle

The angle between the bodies.
## float LinearVelocity

The target velocity of the attached linear motor.
## float LinearSpring

The rigidity coefficient of the linear spring. **0** means that the spring is not attached.
## float LinearLimitTo

The high limit distance. This limit specifies how far a connected body can move along the joint axis.
## float LinearLimitFrom

The low limit distance. This limit specifies how far a connected body can move along the joint axis.
## float LinearForce

The maximum force of the attached linear motor. **0** means that the motor is not attached.
## float LinearDistance

The target distance of the attached linear spring. The spring tries to move the connected bodies so that to keep this distance between them.
## float LinearDamping

The linear damping of the joint.
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

The target angle of the attached angular spring. the spring tries to rotate the connected bodies so that they make this angle.
## vec3 WorldAxis

The joint axis. The joint axis is calculated based on the axes of the connected bodies.
## vec3 Axis0

The axis of the first connected body.
## vec3 Axis1

The axis of the second connected body.
### Members

---

## JointCylindrical ( )

Constructor. Creates a cylindrical joint with an anchor at the origin of the world coordinates.
## JointCylindrical ( Body body0 , Body body1 )

Constructor. Creates a cylindrical joint connecting two given bodies. An anchor is placed between centers of mass of the bodies.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - First body to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - Second body to be connected with the joint.

## JointCylindrical ( Body body0 , Body body1 , vec3 anchor , vec3 axis )

Constructor. Creates a cylindrical joint connecting two given bodies with specified axis coordinates and an anchor placed at specified coordinates.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - First body to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - Second body to be connected with the joint.
- *vec3* **anchor** - Anchor coordinates.
- *vec3* **axis** - Axis coordinates.
