# Unigine::JointBall Class (CPP)

**Header:** #include <UniginePhysics.h>

**Inherits from:** Joint


This class is used to create [ball joints](../../../principles/physics/joints/index.md#ball).


### Example


The following code illustrates connection of two [bodies](../../../api/library/physics/class.body_cpp.md) (b0 and b1) using a ball joint.


```cpp
#include <UniginePhysics.h>

using namespace Unigine;
using namespace Unigine::Math;

/* .. */

JointBallPtr joint = JointBall::create(b0, b1);

// setting joint axis coordinates
joint->setWorldAxis(vec3(1.0f, 0.0f, 0.0f));

// setting common joint constraint parameters
joint->setLinearRestitution(0.8f);
joint->setAngularRestitution(0.8f);
joint->setLinearSoftness(0.0f);
joint->setAngularSoftness(0.0f);

// setting angular damping
joint->setAngularDamping(16.0f);

// setting swing angular limit, in degrees
joint->setAngularLimitAngle(30.0f);

// setting twist angular limits, in degrees [-20; 20]
joint->setAngularLimitFrom(-20.0f);
joint->setAngularLimitTo(20.0f);

// setting number of iterations
joint->setNumIterations(16);

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

### Members

## void setWorldAxis ( const Math:: vec3 & axis )

Sets a new joint axis. The joint axis is calculated based on the axes of the connected bodies.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **axis** - The joint axis.

## Math:: vec3 getWorldAxis () const

Returns the current joint axis. The joint axis is calculated based on the axes of the connected bodies.
### Return value

Current joint axis.
## void setAngularLimitTo ( float to )

Sets a new high twist limit angle. twist limit specifies how much a connected body can twist around the joint axis.
### Arguments

- *float* **to** - The high twist limit angle, in degrees. The provided value is saturated in the range **[-180; 180]**.

## float getAngularLimitTo () const

Returns the current high twist limit angle. twist limit specifies how much a connected body can twist around the joint axis.
### Return value

Current high twist limit angle, in degrees. The provided value is saturated in the range **[-180; 180]**.
## void setAngularLimitFrom ( float from )

Sets a new low twist limit angle. Twist limit specifies how much a connected body can twist around the joint axis.
### Arguments

- *float* **from** - The Low twist limit angle, in degrees. The provided value is saturated in the range **[-180; 180]**.

## float getAngularLimitFrom () const

Returns the current low twist limit angle. Twist limit specifies how much a connected body can twist around the joint axis.
### Return value

Current Low twist limit angle, in degrees. The provided value is saturated in the range **[-180; 180]**.
## void setAngularLimitAngle ( float angle )

Sets a new swing limit angle. Swing limit specifies how much connected bodies can bend from the joint axis.
### Arguments

- *float* **angle** - The Swing limit angle, in degrees. The provided value is saturated in the range **[-180; 180]**. **0** means there is no limit.

## float getAngularLimitAngle () const

Returns the current swing limit angle. Swing limit specifies how much connected bodies can bend from the joint axis.
### Return value

Current Swing limit angle, in degrees. The provided value is saturated in the range **[-180; 180]**. **0** means there is no limit.
## void setAngularDamping ( float damping )

Sets a new angular damping of the joint.
### Arguments

- *float* **damping** - The angular damping. If a negative value is provided, **0** will be used instead.

## float getAngularDamping () const

Returns the current angular damping of the joint.
### Return value

Current angular damping. If a negative value is provided, **0** will be used instead.
## void setAxis0 ( const Math:: vec3 & axis0 )

Sets a new axis of the first connected body.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **axis0** - The axis of the first body. The provided vector will be normalized.

## Math:: vec3 getAxis0 () const

Returns the current axis of the first connected body.
### Return value

Current axis of the first body. The provided vector will be normalized.
## void setAxis1 ( const Math:: vec3 & axis1 )

Sets a new axis of the second connected body.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **axis1** - The axis of the second body. The provided vector will be normalized.

## Math:: vec3 getAxis1 () const

Returns the current axis of the second connected body.
### Return value

Current axis of the second body. The provided vector will be normalized.
---

## static JointBallPtr create ( )

Constructor. Creates a ball joint with an anchor at the origin of the world coordinates.
## static JointBallPtr create ( const Ptr < Body > & body0 , const Ptr < Body > & body1 )

Constructor. Creates a ball joint connecting two given bodies. An anchor is placed between centers of mass of the bodies.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body0** - First body to be connected with the joint.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body1** - Second body to be connected with the joint.

## static JointBallPtr create ( const Ptr < Body > & body0 , const Ptr < Body > & body1 , const Math:: Vec3 & anchor )

Constructor. Creates a ball joint connecting two given bodies with an anchor placed at specified coordinates.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body0** - First body to be connected with the joint.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body1** - Second body to be connected with the joint.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **anchor** - Anchor coordinates.

## static JointBallPtr create ( const Ptr < Body > & body0 , const Ptr < Body > & body1 , const Math:: Vec3 & anchor , const Math:: vec3 & axis )

Constructor. Creates a ball joint connecting two given bodies with specified axis coordinates and an anchor placed at specified coordinates.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body0** - First body to be connected with the joint.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body1** - Second body to be connected with the joint.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **anchor** - Anchor coordinates.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **axis** - Axis coordinates.
