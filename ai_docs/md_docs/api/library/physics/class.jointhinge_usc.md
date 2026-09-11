# Unigine::JointHinge Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Joint


This class is used to create [hinge joints](../../../principles/physics/joints/index.md#hinge).


### Example


The following code illustrates connection of two [bodies](../../../api/library/physics/class.body_usc.md) (b0 and b1) using a hinge joint.


```cpp
JointHinge joint = class_remove(new JointHinge(b0, b1));

// setting joint axis coordinates
joint.setWorldAxis(vec3(1.0f, 0.0f, 0.0f));

// setting common joint constraint parameters
joint.setLinearRestitution(0.4f);
joint.setAngularRestitution(0.4f);
joint.setLinearSoftness(0.4f);
joint.setAngularSoftness(0.4f);

// setting angular damping
joint.setAngularDamping(8.0f);

// setting angular limits, in degrees [-20; 20]
joint.setAngularLimitFrom(-20.0f);
joint.setAngularLimitTo(20.0f);

// setting spring rigidity coefficient
joint.setAngularSpring(8.0f);

// setting number of iterations
joint.setNumIterations(16);

```


### See Also


- Usage example: [Creating a Simple Mechanism Using Various Types of Joints](../../../code/usage/simple_mechanism_joints/index_usc.md)
- UnigineScript samples:

  -
  -
  -


## JointHinge Class

### Members

## float getCurrentAngularVelocity () const

Returns the current velocity of the motor, i.e. the difference between angular velocities of two bodies connected with a hinge relative the hinge axis.
> **Notice:** The valid velocity is returned only if both bodies are of [BodyRigid](../../../api/library/physics/class.bodyrigid_usc.md) type. Otherwise, **0** is returned.


### Return value

Current motor velocity, in radians per second.
## float getCurrentAngularAngle () const

Returns the current angle between the bodies.
### Return value

Current angle in degrees.
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

Sets a new target angle of the attached angular spring. The spring tries to rotate the connected bodies so that they make this angle.
### Arguments

- *float* **angle** - The target angle in degrees. The provided value will be saturated in the range **[-180; 180]**.

## float getAngularAngle () const

Returns the current target angle of the attached angular spring. The spring tries to rotate the connected bodies so that they make this angle.
### Return value

Current target angle in degrees. The provided value will be saturated in the range **[-180; 180]**.
## void setWorldAxis ( vec3 axis )

Sets a new joint axis. The joint axis is calculated based on the axes of the connected bodies.
### Arguments

- *vec3* **axis** - The joint axis.

## vec3 getWorldAxis () const

Returns the current joint axis. The joint axis is calculated based on the axes of the connected bodies.
### Return value

Current joint axis.
## void setAxis0 ( vec3 axis0 )

Sets a new axis of the first connected body.
### Arguments

- *vec3* **axis0** - The axis of the first body. The provided vector will be normalized.

## vec3 getAxis0 () const

Returns the current axis of the first connected body.
### Return value

Current axis of the first body. The provided vector will be normalized.
## void setAxis1 ( vec3 axis1 )

Sets a new axis of the second connected body.
### Arguments

- *vec3* **axis1** - The axis of the second body. The provided vector will be normalized.

## vec3 getAxis1 () const

Returns the current axis of the second connected body.
### Return value

Current axis of the second body. The provided vector will be normalized.
---

## static JointHinge ( )

Constructor. Creates a hinge joint with an anchor at the origin of the world coordinates.
## static JointHinge ( Body body0 , Body body1 )

Constructor. Creates a hinge joint connecting two given bodies. An anchor is placed between centers of mass of the bodies.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body0** - First body to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_usc.md)* **body1** - Second body to be connected with the joint.

## static JointHinge ( Body body0 , Body body1 , Vec3 anchor , vec3 axis )

Constructor. Creates a hinge joint connecting two given bodies with specified axis coordinates and an anchor placed at specified coordinates.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body0** - First body to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_usc.md)* **body1** - Second body to be connected with the joint.
- *Vec3* **anchor** - Anchor coordinates.
- *vec3* **axis** - Axis coordinates.
