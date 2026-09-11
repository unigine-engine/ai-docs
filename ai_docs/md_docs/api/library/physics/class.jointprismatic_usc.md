# Unigine::JointPrismatic Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Joint


This class is used to create [prismatic joints](../../../principles/physics/joints/index.md#prismatic).


### Example


The following code illustrates connection of two [bodies](../../../api/library/physics/class.body_usc.md) (b0 and b1) using a prismatic joint.


```cpp
JointPrismatic joint = class_remove(new JointPrismatic(b0, b1));

// setting joint axis coordinates
joint.setWorldAxis(vec3(0.0f, 0.0f, 1.0f));

// setting common joint constraint parameters
joint.setLinearRestitution(0.4f);
joint.setAngularRestitution(0.4f);
joint.setLinearSoftness(0.4f);
joint.setAngularSoftness(0.4f);

// setting linear damping
joint.setLinearDamping(4.0f);

// setting linear limits [-1.5; 1.5]
joint.setLinearLimitFrom(-1.5f);
joint.setLinearLimitTo(1.5f);

// setting number of iterations
joint.setNumIterations(16);

```


### See Also


- Usage example: [Creating a Simple Mechanism Using Various Types of Joints](../../../code/usage/simple_mechanism_joints/index_usc.md)
- UnigineScript samples:

  -
  -


## JointPrismatic Class

### Members

## float getCurrentLinearVelocity () const

Returns the current velocity of the linear motor.
### Return value

Current velocity in units per second.
## float getCurrentLinearDistance () const

Returns the current distance between the bodies.
### Return value

Current distance in units.
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
---

## static JointPrismatic ( )

Constructor. Creates a prismatic joint with an anchor at the origin of the world coordinates.
## static JointPrismatic ( Body body0 , Body body1 )

Constructor. Creates a prismatic joint connecting two given bodies. An anchor is placed between centers of mass of the bodies.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body0** - First body to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_usc.md)* **body1** - Second body to be connected with the joint.

## static JointPrismatic ( Body body0 , Body body1 , Vec3 anchor , vec3 axis )

Constructor. Creates a prismatic joint connecting two given bodies with specified axis coordinates and an anchor placed at specified coordinates.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body0** - First body to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_usc.md)* **body1** - Second body to be connected with the joint.
- *Vec3* **anchor** - Anchor coordinates.
- *vec3* **axis** - Axis coordinates.
