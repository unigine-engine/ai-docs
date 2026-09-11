# Unigine::JointCylindrical Class (CPP)

**Header:** #include <UniginePhysics.h>

**Inherits from:** Joint


This class is used to create [cylindrical joints](../../../principles/physics/joints/index.md#cylindrical).


### Example


The following code illustrates connection of two [bodies](../../../api/library/physics/class.body_cpp.md) (b0 and b1) using a cylindrical joint.


```cpp
include <UniginePhysics.h>

/* .. */

JointCylindricalPtr joint = JointCylindrical::create(b0, b1);

// setting joint axis coordinates
joint->setWorldAxis(vec3(0.0f, 0.0f, 1.0f));

// setting common joint constraint parameters
joint->setLinearRestitution(0.4f);
joint->setAngularRestitution(0.4f);
joint->setLinearSoftness(0.4f);
joint->setAngularSoftness(0.4f);

// setting linear and angular damping
joint->setLinearDamping(4.0f);
joint->setAngularDamping(2.0f);

// setting linear limits [-1.5; 1.5]
joint->setLinearLimitFrom(-1.5f);
joint->setLinearLimitTo(1.5f);

// setting number of iterations
joint->setNumIterations(16);

```


### See Also


- Usage example: [Creating a Simple Mechanism Using Various Types of Joints](../../../code/usage/simple_mechanism_joints/index_cpp.md)
- UnigineScript samples:

  -
  -


## JointCylindrical Class

### Members

## float getCurrentLinearVelocity () const

Returns the current velocity of the linear motor.
### Return value

Current velocity in units per second.
## float getCurrentLinearDistance () const

Returns the current distance between the bodies.
### Return value

Current distance in units.
## float getCurrentAngularVelocity () const

Returns the current velocity of the angular motor.
### Return value

Current velocity in radians per second.
## float getCurrentAngularAngle () const

Returns the current angle between the bodies.
### Return value

Current angle in degrees.
## void setLinearVelocity ( float velocity )

Sets a new target velocity of the attached linear motor.
### Arguments

- *float* **velocity** - The target velocity in units per second.

## float getLinearVelocity () const

Returns the current target velocity of the attached linear motor.
### Return value

Current target velocity in units per second.
## void setLinearSpring ( float spring )

Sets a new rigidity coefficient of the linear spring. **0** means that the spring is not attached.
### Arguments

- *float* **spring** - The rigidity coefficient. If a negative value is provided, **0** will be used instead. **0** detaches the spring.

## float getLinearSpring () const

Returns the current rigidity coefficient of the linear spring. **0** means that the spring is not attached.
### Return value

Current rigidity coefficient. If a negative value is provided, **0** will be used instead. **0** detaches the spring.
## void setLinearLimitTo ( float to )

Sets a new high limit distance. This limit specifies how far a connected body can move along the joint axis.
### Arguments

- *float* **to** - The high limit distance in units.

## float getLinearLimitTo () const

Returns the current high limit distance. This limit specifies how far a connected body can move along the joint axis.
### Return value

Current high limit distance in units.
## void setLinearLimitFrom ( float from )

Sets a new low limit distance. This limit specifies how far a connected body can move along the joint axis.
### Arguments

- *float* **from** - The low limit distance in units.

## float getLinearLimitFrom () const

Returns the current low limit distance. This limit specifies how far a connected body can move along the joint axis.
### Return value

Current low limit distance in units.
## void setLinearForce ( float force )

Sets a new maximum force of the attached linear motor. **0** means that the motor is not attached.
### Arguments

- *float* **force** - The maximum force. If a negative value is provided, **0** will be used instead. **0** detaches the motor.

## float getLinearForce () const

Returns the current maximum force of the attached linear motor. **0** means that the motor is not attached.
### Return value

Current maximum force. If a negative value is provided, **0** will be used instead. **0** detaches the motor.
## void setLinearDistance ( float distance )

Sets a new target distance of the attached linear spring. The spring tries to move the connected bodies so that to keep this distance between them.
### Arguments

- *float* **distance** - The target distance in units.

## float getLinearDistance () const

Returns the current target distance of the attached linear spring. The spring tries to move the connected bodies so that to keep this distance between them.
### Return value

Current target distance in units.
## void setLinearDamping ( float damping )

Sets a new linear damping of the joint.
### Arguments

- *float* **damping** - The linear damping. If a negative value is provided, **0** will be used instead.

## float getLinearDamping () const

Returns the current linear damping of the joint.
### Return value

Current linear damping. If a negative value is provided, **0** will be used instead.
## void setAngularVelocity ( float velocity )

Sets a new target velocity of the attached angular motor.
### Arguments

- *float* **velocity** - The target velocity in radians per second.

## float getAngularVelocity () const

Returns the current target velocity of the attached angular motor.
### Return value

Current target velocity in radians per second.
## void setAngularSpring ( float spring )

Sets a new rigidity coefficient of the angular spring. **0** means that the spring is not attached.
### Arguments

- *float* **spring** - The rigidity coefficient. If a negative value is provided, **0** will be used instead. **0** detaches the spring.

## float getAngularSpring () const

Returns the current rigidity coefficient of the angular spring. **0** means that the spring is not attached.
### Return value

Current rigidity coefficient. If a negative value is provided, **0** will be used instead. **0** detaches the spring.
## void setAngularLimitTo ( float to )

Sets a new high rotation limit angle. Rotation limit specifies how much a connected body can rotate around the joint axis
### Arguments

- *float* **to** - The high rotation limit angle in degrees. The provided value will be saturated in the range **[-180; 180]**.

## float getAngularLimitTo () const

Returns the current high rotation limit angle. Rotation limit specifies how much a connected body can rotate around the joint axis
### Return value

Current high rotation limit angle in degrees. The provided value will be saturated in the range **[-180; 180]**.
## void setAngularLimitFrom ( float from )

Sets a new low rotation limit angle. Rotation limit specifies how much a connected body can rotate around the joint axis.
### Arguments

- *float* **from** - The Low rotation limit angle in degrees. The provided value will be saturated in the range **[-180; 180]**.

## float getAngularLimitFrom () const

Returns the current low rotation limit angle. Rotation limit specifies how much a connected body can rotate around the joint axis.
### Return value

Current Low rotation limit angle in degrees. The provided value will be saturated in the range **[-180; 180]**.
## void setAngularTorque ( float torque )

Sets a new maximum torque of the attached angular motor. **0** means that the motor is not attached.
### Arguments

- *float* **torque** - The Maximum torque. If a negative value is provided, **0** will be used instead. **0** detaches the motor.

## float getAngularTorque () const

Returns the current maximum torque of the attached angular motor. **0** means that the motor is not attached.
### Return value

Current Maximum torque. If a negative value is provided, **0** will be used instead. **0** detaches the motor.
## void setAngularDamping ( float damping )

Sets a new angular damping of the joint.
### Arguments

- *float* **damping** - The angular damping. If a negative value is provided, **0** will be used instead.

## float getAngularDamping () const

Returns the current angular damping of the joint.
### Return value

Current angular damping. If a negative value is provided, **0** will be used instead.
## void setAngularAngle ( float angle )

Sets a new target angle of the attached angular spring. the spring tries to rotate the connected bodies so that they make this angle.
### Arguments

- *float* **angle** - The target angle in degrees. The provided value will be saturated in the range **[-180; 180]**.

## float getAngularAngle () const

Returns the current target angle of the attached angular spring. the spring tries to rotate the connected bodies so that they make this angle.
### Return value

Current target angle in degrees. The provided value will be saturated in the range **[-180; 180]**.
## void setWorldAxis ( const Math:: vec3 & axis )

Sets a new joint axis. The joint axis is calculated based on the axes of the connected bodies.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **axis** - The joint axis.

## Math:: vec3 getWorldAxis () const

Returns the current joint axis. The joint axis is calculated based on the axes of the connected bodies.
### Return value

Current joint axis.
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

## static JointCylindricalPtr create ( )

Constructor. Creates a cylindrical joint with an anchor at the origin of the world coordinates.
## static JointCylindricalPtr create ( const Ptr < Body > & body0 , const Ptr < Body > & body1 )

Constructor. Creates a cylindrical joint connecting two given bodies. An anchor is placed between centers of mass of the bodies.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body0** - First body to be connected with the joint.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body1** - Second body to be connected with the joint.

## static JointCylindricalPtr create ( const Ptr < Body > & body0 , const Ptr < Body > & body1 , const Math:: Vec3 & anchor , const Math:: vec3 & axis )

Constructor. Creates a cylindrical joint connecting two given bodies with specified axis coordinates and an anchor placed at specified coordinates.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body0** - First body to be connected with the joint.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body1** - Second body to be connected with the joint.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **anchor** - Anchor coordinates.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **axis** - Axis coordinates.
