# Unigine::JointPath Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Joint


A path joint is used with [BodyPath](../../../api/library/physics/class.bodypath_usc.md): it attaches an arbitrary BodyRigid to move along its path.


> **Notice:** The *path* is a spline along which an object can be moved.


### See Also


UnigineScript samples:


-
-


### Example


The following code illustrates connection of a [rigid body](../../../api/library/physics/class.bodyrigid_usc.md) (b0) and a [path body](../../../api/library/physics/class.bodypath_usc.md) (b1) using a path joint.


```cpp
JointPath joint = class_remove(new JointPath(b0, b1));

// setting linear damping, velocity and force limits
joint.setLinearDamping(200.0f);
joint.setLinearVelocity(-100.0f);
joint.setLinearForce(1000.0f);

// setting body orientation regarding the path
joint.setRotation0(rotateZ(90.0f));

// setting number of iterations
joint.setNumIterations(4);

```


## JointPath Class

### Members

## float getCurrentLinearVelocity () const

Returns the current velocity of the linear motor.
### Return value

Current velocity of the attached motor, in units per second.
## void setWorldRotation ( mat3 rotation )

Sets a new rotation matrix of the anchor point in the world system of coordinates.
### Arguments

- *mat3* **rotation** - The rotation matrix in the world coordinate space.

## mat3 getWorldRotation () const

Returns the current rotation matrix of the anchor point in the world system of coordinates.
### Return value

Current rotation matrix in the world coordinate space.
## void setRotation0 ( mat3 rotation0 )

Sets a new rotation matrix of the anchor point in a system of coordinates of the connected rigid body.
### Arguments

- *mat3* **rotation0** - The rotation matrix of the anchor point in a system of coordinates of the connected rigid body.

## mat3 getRotation0 () const

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

## static JointPath ( )

Constructor. Creates a path joint with an anchor at the origin of the world coordinates.
## static JointPath ( Body body0 , Body body1 )

Constructor. Creates a path joint connecting two given bodies. An anchor is placed in the center of the rigid body attached the path body.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body0** - [BodyRigid](../../../api/library/physics/class.bodyrigid_usc.md) to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_usc.md)* **body1** - [BodyPath](../../../api/library/physics/class.bodypath_usc.md) to be connected with the joint.

## static JointPath ( Body body0 , Body body1 , Vec3 anchor )

Constructor. Creates a path joint connecting two given bodies with an anchor placed at specified coordinates.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body0** - [BodyRigid](../../../api/library/physics/class.bodyrigid_usc.md) to be connected with the joint.
- *[Body](../../../api/library/physics/class.body_usc.md)* **body1** - [BodyPath](../../../api/library/physics/class.bodypath_usc.md) to be connected with the joint.
- *Vec3* **anchor** - Anchor coordinates.
