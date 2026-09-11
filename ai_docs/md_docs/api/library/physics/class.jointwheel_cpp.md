# Unigine::JointWheel Class (CPP)

**Header:** #include <UniginePhysics.h>

**Inherits from:** Joint


This class is used to create [ray-cast](../../../principles/physics/joints/index.md#vehicles) wheels. Both a frame and a wheel are [rigid bodies](../../../principles/physics/bodies/rigid/index.md). There is no need to assign a shape to the wheel: ray casting is used to detect collision of the wheel with a surface.


### Example


The following code illustrates connection of two [rigid bodies](../../../api/library/physics/class.bodyrigid_cpp.md) (frame and wheel) using a wheel joint.


```cpp
include <UniginePhysics.h>

/* .. */

JointWheelPtr joint = JointWheel::create(frame, wheel);

// setting joint anchor coordinates
joint->setWorldAnchor(wheel->getObject()->getWorldTransform() * Vec3(0.0f));

// setting joint axes coordinates
joint->setWorldAxis0(vec3(0.0f,0.0f,1.0f));
joint->setWorldAxis1(vec3(0.0f,1.0f,0.0f));

// setting linear damping and spring rigidity
joint->setLinearDamping(200.0f);
joint->setLinearSpring(100.0f);

// setting lower and upper suspension ride limits [-1.0; 0.0]
joint->setLinearLimitFrom(-1.0f);
joint->setLinearLimitTo(0.0f);

// setting target suspension height
joint->setLinearDistance(0.5f);

// setting maximum angular velocity and torque
joint->setAngularVelocity(-20.0f);
joint->setAngularTorque(10.0f);

// setting wheel parameters
joint->setWheelRadius(0.5f);
joint->setWheelMass(4.0f);
joint->setWheelThreshold(0.1f);

// setting tyre friction parameters
joint->setTangentFriction(4.0f);
joint->setBinormalFriction(5.0f);

// setting number of iterations
joint->setNumIterations(8);

```


### See Also


- Usage example: [Creating a Car with Wheel Joints](../../../code/usage/car_wheel_joints/index_cpp.md)
- UnigineScript samples:

  -
  -


## JointWheel Class

### Members

## float getCurrentSlipRatio () const

Returns the current ratio of wheel spin to ground speed.
### Return value

Current slip ratio, in percent. **0** means that the velocities are equal. If the throttle is pressed, the value will be positive. If the brake is pressed, the value will be negative.
## float getCurrentSlipAngle () const

Returns the current angle between the wheel direction and the frame direction.
### Return value

Current slip angle in degrees.
## void setWheelThreshold ( float threshold )

Sets a new threshold difference between the wheel and ground velocities. When it is too small, the longitudinal force is scaled down to prevent unnatural vibrations.
### Arguments

- *float* **threshold** - The difference threshold. If a negative value is provided, **0** will be used instead.

## float getWheelThreshold () const

Returns the current threshold difference between the wheel and ground velocities. When it is too small, the longitudinal force is scaled down to prevent unnatural vibrations.
### Return value

Current difference threshold. If a negative value is provided, **0** will be used instead.
## void setWheelRadius ( float radius )

Sets a new radius of the attached wheel.
### Arguments

- *float* **radius** - The radius of the wheel, in units. If a negative value is provided, **0** will be used instead.

## float getWheelRadius () const

Returns the current radius of the attached wheel.
### Return value

Current radius of the wheel, in units. If a negative value is provided, **0** will be used instead.
## void setWheelMass ( float mass )

Sets a new mass of the attached wheel.
> **Notice:** If *g* (Earth's gravity) equals to 9.8 m/s 2, and 1 unit equals to 1 m, the mass is measured in kilograms.


### Arguments

- *float* **mass** - The mass of the wheel. If a negative value is provided, **0** will be used instead.

## float getWheelMass () const

Returns the current mass of the attached wheel.
> **Notice:** If *g* (Earth's gravity) equals to 9.8 m/s 2, and 1 unit equals to 1 m, the mass is measured in kilograms.


### Return value

Current mass of the wheel. If a negative value is provided, **0** will be used instead.
## void setTangentFriction ( float friction )

Sets a new longitudinal (forward) friction of the tire.
### Arguments

- *float* **friction** - The longitudinal friction. If a negative value is provided, **0** will be used instead.

## float getTangentFriction () const

Returns the current longitudinal (forward) friction of the tire.
### Return value

Current longitudinal friction. If a negative value is provided, **0** will be used instead.
## void setTangentAngle ( float angle )

Sets a new coefficient specifying how fast the optimal longitudinal force can be achieved. The larger this value, the more is the impulse produced by the tire.
### Arguments

- *float* **angle** - The coefficient characterizing the tire longitudinal impulse. If a negative value is provided, **0** will be used instead.

## float getTangentAngle () const

Returns the current coefficient specifying how fast the optimal longitudinal force can be achieved. The larger this value, the more is the impulse produced by the tire.
### Return value

Current coefficient characterizing the tire longitudinal impulse. If a negative value is provided, **0** will be used instead.
## void setBinormalFriction ( float friction )

Sets a new lateral (sideways) friction of the tire.
### Arguments

- *float* **friction** - The lateral friction. If a negative value is provided, **0** will be used instead.

## float getBinormalFriction () const

Returns the current lateral (sideways) friction of the tire.
### Return value

Current lateral friction. If a negative value is provided, **0** will be used instead.
## void setBinormalAngle ( float angle )

Sets a new coefficient specifying how fast the optimal lateral force can be achieved. The larger this value, the more is the impulse produced by the tire.
### Arguments

- *float* **angle** - The coefficient characterizing the tire lateral impulse. If a negative value is provided, **0** will be used instead.

## float getBinormalAngle () const

Returns the current coefficient specifying how fast the optimal lateral force can be achieved. The larger this value, the more is the impulse produced by the tire.
### Return value

Current coefficient characterizing the tire lateral impulse. If a negative value is provided, **0** will be used instead.
## void setCurrentAngularVelocity ( float velocity )

Sets a new rotation velocity of the attached wheels.
### Arguments

- *float* **velocity** - The angular velocity in radians per second. Setting the value to 0 allows stopping the car when necessary.

## float getCurrentAngularVelocity () const

Returns the current rotation velocity of the attached wheels.
### Return value

Current angular velocity in radians per second. Setting the value to 0 allows stopping the car when necessary.
## void setAngularVelocity ( float velocity )

Sets a new target velocity of wheel rotation.
### Arguments

- *float* **velocity** - The target velocity, in radians per second.

## float getAngularVelocity () const

Returns the current target velocity of wheel rotation.
### Return value

Current target velocity, in radians per second.
## void setAngularTorque ( float torque )

Sets a new maximum torque of the attached angular motor. **0** means that the motor is not attached.
### Arguments

- *float* **torque** - The maximum torque. If a negative value is provided, **0** will be used instead. **0** detaches the motor.

## float getAngularTorque () const

Returns the current maximum torque of the attached angular motor. **0** means that the motor is not attached.
### Return value

Current maximum torque. If a negative value is provided, **0** will be used instead. **0** detaches the motor.
## void setAngularDamping ( float damping )

Sets a new angular damping of the joint (wheel rotation damping).
### Arguments

- *float* **damping** - The angular damping. If a negative value is provided, **0** will be used instead.

## float getAngularDamping () const

Returns the current angular damping of the joint (wheel rotation damping).
### Return value

Current angular damping. If a negative value is provided, **0** will be used instead.
## void setCurrentLinearDistance ( float distance )

Sets a new suspension compression (i.e. the length of the suspension).
### Arguments

- *float* **distance** - The suspension length, in units.

## float getCurrentLinearDistance () const

Returns the current suspension compression (i.e. the length of the suspension).
### Return value

Current suspension length, in units.
## void setLinearSpring ( float spring )

Sets a new rigidity coefficient of the suspension. **0** means that the suspension is not attached.
### Arguments

- *float* **spring** - The rigidity coefficient. If a negative value is provided, **0** will be used instead. **0** detaches the suspension.

## float getLinearSpring () const

Returns the current rigidity coefficient of the suspension. **0** means that the suspension is not attached.
### Return value

Current rigidity coefficient. If a negative value is provided, **0** will be used instead. **0** detaches the suspension.
## void setLinearLimitTo ( float to )

Sets a new high limit of the suspension ride. This limit specifies how far a connected body can move along the joint axis.
### Arguments

- *float* **to** - The high limit in units.

## float getLinearLimitTo () const

Returns the current high limit of the suspension ride. This limit specifies how far a connected body can move along the joint axis.
### Return value

Current high limit in units.
## void setLinearLimitFrom ( float from )

Sets a new low limit of the suspension ride. This limit specifies how far a connected body can move along the joint axis.
### Arguments

- *float* **from** - The low limit in units.

## float getLinearLimitFrom () const

Returns the current low limit of the suspension ride. This limit specifies how far a connected body can move along the joint axis.
### Return value

Current low limit in units.
## void setLinearDistance ( float distance )

Sets a new target height of the suspension.
### Arguments

- *float* **distance** - The height, in units.

## float getLinearDistance () const

Returns the current target height of the suspension.
### Return value

Current height, in units.
## void setLinearDamping ( float damping )

Sets a new linear damping of the suspension.
### Arguments

- *float* **damping** - The linear damping. If a negative value is provided, **0** will be used instead.

## float getLinearDamping () const

Returns the current linear damping of the suspension.
### Return value

Current linear damping. If a negative value is provided, **0** will be used instead.
## void setPhysicsIntersectionMask ( int mask )

Sets a new [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) of the joint.
### Arguments

- *int* **mask** - The physics intersection mask of the joint

## int getPhysicsIntersectionMask () const

Returns the current [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) of the joint.
### Return value

Current physics intersection mask of the joint
## void setWorldAxis0 ( const Math:: vec3 & axis0 )

Sets a new suspension axis in the world coordinates.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **axis0** - The suspension axis in the world coordinates.

## Math:: vec3 getWorldAxis0 () const

Returns the current suspension axis in the world coordinates.
### Return value

Current suspension axis in the world coordinates.
## void setWorldAxis1 ( const Math:: vec3 & axis1 )

Sets a new wheel spindle axis in the world coordinates.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **axis1** - The wheel spindle axis in the world coordinates.

## Math:: vec3 getWorldAxis1 () const

Returns the current wheel spindle axis in the world coordinates.
### Return value

Current wheel spindle axis in the world coordinates.
## void setAxis00 ( const Math:: vec3 & axis00 )

Sets a new coordinates of suspension axis, along which a wheel moves vertically. This is a shock absorber.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **axis00** - The suspension axis, in the world coordinates.

## Math:: vec3 getAxis00 () const

Returns the current coordinates of suspension axis, along which a wheel moves vertically. This is a shock absorber.
### Return value

Current suspension axis, in the world coordinates.
## void setAxis10 ( const Math:: vec3 & axis10 )

Sets a new wheel spindle axis in coordinates of the frame (body 0): an axis around which a wheel rotates when moving forward (or backward).
![](../../../principles/physics/joints/wheel_joint1.jpg)


### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **axis10** - The wheel spindle axis in coordinates of the frame (body 0).

## Math:: vec3 getAxis10 () const

Returns the current wheel spindle axis in coordinates of the frame (body 0): an axis around which a wheel rotates when moving forward (or backward).
![](../../../principles/physics/joints/wheel_joint1.jpg)


### Return value

Current wheel spindle axis in coordinates of the frame (body 0).
## void setAxis11 ( const Math:: vec3 & axis11 )

Sets a new wheel spindle axis in coordinates of the wheel (body 1): an axis around which a wheel rotates when steering.
![](../../../principles/physics/joints/wheel_joint1.jpg)


### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **axis11** - The wheel spindle axis in coordinates of the wheel (body 1).

## Math:: vec3 getAxis11 () const

Returns the current wheel spindle axis in coordinates of the wheel (body 1): an axis around which a wheel rotates when steering.
![](../../../principles/physics/joints/wheel_joint1.jpg)


### Return value

Current wheel spindle axis in coordinates of the wheel (body 1).
---

## static JointWheelPtr create ( )

Constructor. Creates a wheel joint with an anchor at the origin of the world coordinates.
## static JointWheelPtr create ( const Ptr < Body > & body0 , const Ptr < Body > & body1 )

Constructor. Creates a wheel joint connecting two given bodies. An anchor is placed between centers of mass of the bodies.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body0** - Frame to be connected with the joint.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body1** - Wheel to be connected with the joint.

## static JointWheelPtr create ( const Ptr < Body > & body0 , const Ptr < Body > & body1 , const Math:: Vec3 & anchor , const Math:: vec3 & axis0 , const Math:: vec3 & axis1 )

Constructor. Creates a wheel joint connecting two given bodies with specified suspension and spindle axis coordinates and an anchor placed at specified coordinates.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body0** - Frame to be connected with the joint.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body1** - Wheel to be connected with the joint.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **anchor** - Anchor coordinates.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **axis0** - Suspension axis coordinates.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **axis1** - Wheel spindle axis coordinates.

## Math:: vec3 getContactNormal ( ) const

Returns a normal of a point of contact with the ground, in world coordinates.
### Return value

Normal.
## Ptr < Object > getContactObject ( ) const

Returns an object representing the ground.
### Return value

Ground object.
## Math:: Vec3 getContactPoint ( ) const

Returns a point of contact with the ground, in world coordinates.
### Return value

Point coordinates.
## Ptr < Shape > getContactShape ( ) const

Returns a shape of the object representing the ground.
### Return value

Shape of the ground object.
## int getContactSurface ( ) const

Returns a surface of a ground object, which is in contact.
### Return value

Surface number.
## void setCanBeUnderTerrain ( bool val )

Sets a value indicating if the *Wheel Joint* should be used under the surface of the terrain (drive in an underground parking or tunnel). This flag ensures proper behavior of the joint underground , otherwise the *Wheel Joint* will tend to pop up on the terrain surface above.
### Arguments

- *bool* **val** - true if the *Wheel Joint* is to be used under the surface of the terrain; otherwise, false.
