# Unigine::JointBall Class (CS)

**Inherits from:** Joint


This class is used to create [ball joints](../../../principles/physics/joints/index.md#ball).


### Example


The following code illustrates connection of two [bodies](../../../api/library/physics/class.body_cs.md) (b0 and b1) using a ball joint.


```csharp
JointBall joint = new JointBall(b0, b1);

	// setting joint axis coordinates
	joint.WorldAxis = new vec3(1.0f, 0.0f, 0.0f);

	// setting common joint constraint parameters
	joint.LinearRestitution = 0.8f;
	joint.AngularRestitution = 0.8f;
	joint.LinearSoftness = 0.0f;
	joint.AngularSoftness = 0.0f;

	// setting angular damping
	joint.AngularDamping = 16.0f;

	// setting swing angular limit, in degrees
	joint.AngularLimitAngle = 30.0f;

	// setting twist angular limits, in degrees [-20; 20]
	joint.AngularLimitFrom = -20.0f;
	joint.AngularLimitTo = 20.0f;

	// setting number of iterations
	joint.NumIterations = 16;

```


### See Also


UnigineScript samples:


-
-
-
-
-
-
-


## JointBall Class

### Properties

## vec3 WorldAxis

The joint axis. The joint axis is calculated based on the axes of the connected bodies.
## float AngularLimitTo

The high twist limit angle. twist limit specifies how much a connected body can twist around the joint axis.
## float AngularLimitFrom

The low twist limit angle. Twist limit specifies how much a connected body can twist around the joint axis.
## float AngularLimitAngle

The swing limit angle. Swing limit specifies how much connected bodies can bend from the joint axis.
## float AngularDamping

The angular damping of the joint.
## vec3 Axis0

The axis of the first connected body.
## vec3 Axis1

The axis of the second connected body.
### Members

---

## JointBall ( )

Constructor. Creates a ball joint with an anchor at the origin of the world coordinates.
## JointBall ( Body body0 , Body body1 )

Constructor. Creates a ball joint connecting two given bodies. An anchor is placed between centers of mass of the bodies.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - First body to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - Second body to be connected with the joint.

## JointBall ( Body body0 , Body body1 , vec3 anchor )

Constructor. Creates a ball joint connecting two given bodies with an anchor placed at specified coordinates.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - First body to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - Second body to be connected with the joint.
- *vec3* **anchor** - Anchor coordinates.

## JointBall ( Body body0 , Body body1 , vec3 anchor , vec3 axis )

Constructor. Creates a ball joint connecting two given bodies with specified axis coordinates and an anchor placed at specified coordinates.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - First body to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - Second body to be connected with the joint.
- *vec3* **anchor** - Anchor coordinates.
- *vec3* **axis** - Axis coordinates.
