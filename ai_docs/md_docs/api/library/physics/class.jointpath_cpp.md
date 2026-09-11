# Unigine::JointPath Class (CPP)

**Header:** #include <UniginePhysics.h>

**Inherits from:** Joint


A path joint is used with [BodyPath](../../../api/library/physics/class.bodypath_cpp.md): it attaches an arbitrary BodyRigid to move along its path.


> **Notice:** The *path* is a spline along which an object can be moved.


### See Also


UnigineScript samples:


-
-


### Example


The following code illustrates connection of a [rigid body](../../../api/library/physics/class.bodyrigid_cpp.md) (b0) and a [path body](../../../api/library/physics/class.bodypath_cpp.md) (b1) using a path joint.


```cpp
include <UniginePhysics.h>

/* .. */

JointPathPtr joint = JointPath::create(b0, b1);

// setting linear damping, velocity and force limits
joint->setLinearDamping(200.0f);
joint->setLinearVelocity(-100.0f);
joint->setLinearForce(1000.0f);

// setting body orientation regarding the path
joint->setRotation0(mat3(rotateZ(90.0f)));

// setting number of iterations
joint->setNumIterations(4);

```


## JointPath Class

### Members

## float getCurrentLinearVelocity () const

Returns the current velocity of the linear motor.
### Return value

Current velocity of the attached motor, in units per second.
## void setWorldRotation ( const Math:: mat3 & rotation )

Sets a new rotation matrix of the anchor point in the world system of coordinates.
### Arguments

- *const  Math::[mat3](../../../api/library/math/class.mat3_cpp.md)&* **rotation** - The rotation matrix in the world coordinate space.

## Math:: mat3 getWorldRotation () const

Returns the current rotation matrix of the anchor point in the world system of coordinates.
### Return value

Current rotation matrix in the world coordinate space.
## void setRotation0 ( const Math:: mat3 & rotation0 )

Sets a new rotation matrix of the anchor point in a system of coordinates of the connected rigid body.
### Arguments

- *const  Math::[mat3](../../../api/library/math/class.mat3_cpp.md)&* **rotation0** - The rotation matrix of the anchor point in a system of coordinates of the connected rigid body.

## Math:: mat3 getRotation0 () const

Returns the current rotation matrix of the anchor point in a system of coordinates of the connected rigid body.
### Return value

Current rotation matrix of the anchor point in a system of coordinates of the connected rigid body.
## void setLinearVelocity ( float velocity )

Sets a new target velocity of the attached linear motor.
### Arguments

- *float* **velocity** - The target velocity in units per second.

## float getLinearVelocity () const

Returns the current target velocity of the attached linear motor.
### Return value

Current target velocity in units per second.
## void setLinearForce ( float force )

Sets a new maximum force of the attached linear motor. **0** means that the motor is not attached.
### Arguments

- *float* **force** - The maximum force. If a negative value is provided, **0** will be used instead. **0** detaches the motor.

## float getLinearForce () const

Returns the current maximum force of the attached linear motor. **0** means that the motor is not attached.
### Return value

Current maximum force. If a negative value is provided, **0** will be used instead. **0** detaches the motor.
## void setLinearDamping ( float damping )

Sets a new linear damping of the joint.
### Arguments

- *float* **damping** - The linear damping. If a negative value is provided, **0** will be used instead.

## float getLinearDamping () const

Returns the current linear damping of the joint.
### Return value

Current linear damping. If a negative value is provided, **0** will be used instead.
---

## static JointPathPtr create ( )

Constructor. Creates a path joint with an anchor at the origin of the world coordinates.
## static JointPathPtr create ( const Ptr < Body > & body0 , const Ptr < Body > & body1 )

Constructor. Creates a path joint connecting two given bodies. An anchor is placed in the center of the rigid body attached the path body.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body0** - [BodyRigid](../../../api/library/physics/class.bodyrigid_cpp.md) to be connected with the joint.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body1** - [BodyPath](../../../api/library/physics/class.bodypath_cpp.md) to be connected with the joint.

## static JointPathPtr create ( const Ptr < Body > & body0 , const Ptr < Body > & body1 , const Math:: Vec3 & anchor )

Constructor. Creates a path joint connecting two given bodies with an anchor placed at specified coordinates.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body0** - [BodyRigid](../../../api/library/physics/class.bodyrigid_cpp.md) to be connected with the joint.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body1** - [BodyPath](../../../api/library/physics/class.bodypath_cpp.md) to be connected with the joint.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **anchor** - Anchor coordinates.
