# Unigine::JointFixed Class (CPP)

**Header:** #include <UniginePhysics.h>

**Inherits from:** Joint


This class is used to create [fixed joints](../../../principles/physics/joints/index.md#fixed).


### Example


The following code illustrates connection of two [bodies](../../../api/library/physics/class.body_cpp.md) (b0 and b1) using a fixed joint.


```cpp
include <UniginePhysics.h>

/* .. */

JointFixedPtr joint = JointFixed::create(b0, b1);

// setting common joint constraint parameters
joint->setLinearRestitution(0.8f);
joint->setAngularRestitution(0.8f);
joint->setLinearSoftness(0.0f);
joint->setAngularSoftness(0.0f);

// setting number of iterations
joint->setNumIterations(4);

```


### See Also


- Usage example: [Creating a Simple Mechanism Using Various Types of Joints](../../../code/usage/simple_mechanism_joints/index_cpp.md)
- UnigineScript samples:

  -
  -
  -
  -
  -
  -


## JointFixed Class

### Members

## void setWorldRotation ( const Math:: mat3 & rotation )

Sets a new rotation matrix of the anchor point in the world system of coordinates.
### Arguments

- *const  Math::[mat3](../../../api/library/math/class.mat3_cpp.md)&* **rotation** - The rotation matrix in the world coordinate space.

## Math:: mat3 getWorldRotation () const

Returns the current rotation matrix of the anchor point in the world system of coordinates.
### Return value

Current rotation matrix in the world coordinate space.
## void setRotation0 ( const Math:: mat3 & rotation0 )

Sets a new rotation matrix of the anchor point in the system of coordinates of the first connected body.
### Arguments

- *const  Math::[mat3](../../../api/library/math/class.mat3_cpp.md)&* **rotation0** - The rotation matrix in the body coordinate space.

## Math:: mat3 getRotation0 () const

Returns the current rotation matrix of the anchor point in the system of coordinates of the first connected body.
### Return value

Current rotation matrix in the body coordinate space.
## void setRotation1 ( const Math:: mat3 & rotation1 )

Sets a new rotation matrix of the anchor point in the system of coordinates of the second connected body.
### Arguments

- *const  Math::[mat3](../../../api/library/math/class.mat3_cpp.md)&* **rotation1** - The rotation matrix in the body coordinate space.

## Math:: mat3 getRotation1 () const

Returns the current rotation matrix of the anchor point in the system of coordinates of the second connected body.
### Return value

Current rotation matrix in the body coordinate space.
---

## static JointFixedPtr create ( )

Constructor. Creates a joint with an anchor at the origin of the world coordinates.
## static JointFixedPtr create ( const Ptr < Body > & body0 , const Ptr < Body > & body1 )

Constructor. Creates a joint connecting two given bodies. An anchor is placed between centers of mass of the bodies.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body0** - First body to be connected with the joint.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body1** - Second body to be connected with the joint.

## static JointFixedPtr create ( const Ptr < Body > & body0 , const Ptr < Body > & body1 , const Math:: Vec3 & anchor )

Constructor. Creates a fixed joint connecting two given bodies with an anchor placed at specified coordinates.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body0** - First body to be connected with the joint.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body1** - Second body to be connected with the joint.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **anchor** - Anchor coordinates.
