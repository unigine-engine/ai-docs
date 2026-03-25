# Unigine::JointFixed Class (CS)

**Inherits from:** Joint


This class is used to create [fixed joints](../../../principles/physics/joints/index.md#fixed).


### Example


The following code illustrates connection of two [bodies](../../../api/library/physics/class.body_cs.md) (b0 and b1) using a fixed joint.


```csharp
	JointFixed joint = new JointFixed(b0, b1);

	// setting common joint constraint parameters
	joint.LinearRestitution = 0.8f;
	joint.AngularRestitution = 0.8f;
	joint.LinearSoftness = 0.0f;
	joint.AngularSoftness = 0.0f;

	// setting number of iterations
	joint.NumIterations = 4;

```


### See Also


- Usage example: [Creating a Simple Mechanism Using Various Types of Joints](../../../code/usage/simple_mechanism_joints/index_cs.md)
- UnigineScript samples:

  -
  -
  -
  -
  -
  -


## JointFixed Class

### Properties

## mat3 WorldRotation

The rotation matrix of the anchor point in the world system of coordinates.
## mat3 Rotation0

The rotation matrix of the anchor point in the system of coordinates of the first connected body.
## mat3 Rotation1

The rotation matrix of the anchor point in the system of coordinates of the second connected body.
### Members

---

## JointFixed ( )

Constructor. Creates a joint with an anchor at the origin of the world coordinates.
## JointFixed ( Body body0 , Body body1 )

Constructor. Creates a joint connecting two given bodies. An anchor is placed between centers of mass of the bodies.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - First body to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - Second body to be connected with the joint.

## JointFixed ( Body body0 , Body body1 , vec3 anchor )

Constructor. Creates a fixed joint connecting two given bodies with an anchor placed at specified coordinates.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body0** - First body to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_cs.md)* **body1** - Second body to be connected with the joint.
- *vec3* **anchor** - Anchor coordinates.
