# Unigine::JointPath Class (CS)

**Inherits from:** Joint


A path joint is used with [BodyPath](../../../api/library/physics/class.bodypath_cs.md): it attaches an arbitrary BodyRigid to move along its path.


> **Notice:** The *path* is a spline along which an object can be moved.


### See Also


UnigineScript samples:


-
-


### Example


The following code illustrates connection of a [rigid body](../../../api/library/physics/class.bodyrigid_cs.md) (b0) and a [path body](../../../api/library/physics/class.bodypath_cs.md) (b1) using a path joint.


```csharp
	JointPath joint = new JointPath(b0, b1);

	// setting linear damping, velocity and force limits
	joint.LinearDamping = 200.0f;
	joint.LinearVelocity = -100.0f;
	joint.LinearForce = 1000.0f;

	// setting body orientation with reference to the path
	joint.Rotation0 = MathLib.RotateZ3(90.0f);

	// setting number of iterations
	joint.NumIterations = 4;

```


## JointPath Class

### Properties

## 🔒︎ float CurrentLinearVelocity

The velocity of the linear motor.
## mat3 WorldRotation

The rotation matrix of the anchor point in the world system of coordinates.
## mat3 Rotation0

The rotation matrix of the anchor point in a system of coordinates of the connected rigid body.
## float LinearVelocity

The target velocity of the attached linear motor.
## float LinearForce

The maximum force of the attached linear motor. **0** means that the motor is not attached.
## float LinearDamping

The linear damping of the joint.
### Members

---

## JointPath ( )

Constructor. Creates a path joint with an anchor at the origin of the world coordinates.
## JointPath ( Body body0 , Body body1 )

Constructor. Creates a path joint connecting two given bodies. An anchor is placed in the center of the rigid body attached the path body.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - [BodyRigid](../../../api/library/physics/class.bodyrigid_cs.md) to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - [BodyPath](../../../api/library/physics/class.bodypath_cs.md) to be connected with the joint.

## JointPath ( Body body0 , Body body1 , vec3 anchor )

Constructor. Creates a path joint connecting two given bodies with an anchor placed at specified coordinates.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - [BodyRigid](../../../api/library/physics/class.bodyrigid_cs.md) to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - [BodyPath](../../../api/library/physics/class.bodypath_cs.md) to be connected with the joint.
- *vec3* **anchor** - Anchor coordinates.
