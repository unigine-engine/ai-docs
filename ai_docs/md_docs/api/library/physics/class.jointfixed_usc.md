# Unigine::JointFixed Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Joint


This class is used to create [fixed joints](../../../principles/physics/joints/index.md#fixed).


### Example


The following code illustrates connection of two [bodies](../../../api/library/physics/class.body_usc.md) (b0 and b1) using a fixed joint.


```cpp
JointFixed joint = class_remove(new JointFixed(b0, b1));

// setting common joint constraint parameters
joint.setLinearRestitution(0.8f);
joint.setAngularRestitution(0.8f);
joint.setLinearSoftness(0.0f);
joint.setAngularSoftness(0.0f);

// setting number of iterations
joint.setNumIterations(4);

```


### See Also


- Usage example: [Creating a Simple Mechanism Using Various Types of Joints](../../../code/usage/simple_mechanism_joints/index_usc.md)
- UnigineScript samples:

  -
  -
  -
  -
  -
  -


## JointFixed Class

### Members

## void setWorldRotation ( mat3 rotation )

Sets a new rotation matrix of the anchor point in the world system of coordinates.
### Arguments

- *mat3* **rotation** - The rotation matrix in the world coordinate space.

## mat3 getWorldRotation () const

Returns the current rotation matrix of the anchor point in the world system of coordinates.
### Return value

Current rotation matrix in the world coordinate space.
## void setRotation0 ( mat3 rotation0 )

Sets a new rotation matrix of the anchor point in the system of coordinates of the first connected body.
### Arguments

- *mat3* **rotation0** - The rotation matrix in the body coordinate space.

## mat3 getRotation0 () const

Returns the current rotation matrix of the anchor point in the system of coordinates of the first connected body.
### Return value

Current rotation matrix in the body coordinate space.
## void setRotation1 ( mat3 rotation1 )

Sets a new rotation matrix of the anchor point in the system of coordinates of the second connected body.
### Arguments

- *mat3* **rotation1** - The rotation matrix in the body coordinate space.

## mat3 getRotation1 () const

Returns the current rotation matrix of the anchor point in the system of coordinates of the second connected body.
### Return value

Current rotation matrix in the body coordinate space.
---

## static JointFixed ( )

Constructor. Creates a joint with an anchor at the origin of the world coordinates.
## static JointFixed ( Body body0 , Body body1 )

Constructor. Creates a joint connecting two given bodies. An anchor is placed between centers of mass of the bodies.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body0** - First body to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_usc.md)* **body1** - Second body to be connected with the joint.

## static JointFixed ( Body body0 , Body body1 , Vec3 anchor )

Constructor. Creates a fixed joint connecting two given bodies with an anchor placed at specified coordinates.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body0** - First body to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_usc.md)* **body1** - Second body to be connected with the joint.
- *Vec3* **anchor** - Anchor coordinates.
