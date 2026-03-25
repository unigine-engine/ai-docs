# Unigine::BodyRigid Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Body


This class is used to simulate [rigid bodies](../../../principles/physics/bodies/rigid/index.md) that move according to the [rigid bodies dynamics](../../../principles/physics/bodies/index.md#rigid_bodies_dynamics).


### See Also


- The [Handling Contacts on Collision](../../../code/usage/handling_contacts_on_collision/index.md) usage example


## BodyRigid Class

### Members

## void setAngularVelocity ( vec3 velocity )

Sets a new angular velocity of the body.
### Arguments

- *vec3* **velocity** - The angular velocity in radians per second, in world coordinates.

## vec3 getAngularVelocity () const

Returns the current angular velocity of the body.
### Return value

Current angular velocity in radians per second, in world coordinates.
## void setLinearVelocity ( vec3 velocity )

Sets a new linear velocity of the body.
### Arguments

- *vec3* **velocity** - The linear velocity in units per second, in world coordinates.

## vec3 getLinearVelocity () const

Returns the current linear velocity of the body.
### Return value

Current linear velocity in units per second, in world coordinates.
## void setFrozenAngularVelocity ( float velocity )

Sets a new angular velocity threshold for freezing body simulation. If the body angular velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_usc.md#setNumFrozenFrames_int_void) (together with linear one), it stops being updated.
### Arguments

- *float* **velocity** - The "freeze" angular velocity. If the value is lower than the [setFrozenAngularVelocity](../../../api/library/physics/class.physics_usc.md#setFrozenAngularVelocity_float_void) of the Physics class, it is overridden.

## float getFrozenAngularVelocity () const

Returns the current angular velocity threshold for freezing body simulation. If the body angular velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_usc.md#setNumFrozenFrames_int_void) (together with linear one), it stops being updated.
### Return value

Current "freeze" angular velocity. If the value is lower than the [setFrozenAngularVelocity](../../../api/library/physics/class.physics_usc.md#setFrozenAngularVelocity_float_void) of the Physics class, it is overridden.
## void setFrozenLinearVelocity ( float velocity )

Sets a new linear velocity threshold for freezing body simulation. If the body linear velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_usc.md#setNumFrozenFrames_int_void) (together with angular one), it stops being updated.
### Arguments

- *float* **velocity** - The "freeze" linear velocity. If the value is lower than the [setFrozenLinearVelocity](../../../api/library/physics/class.physics_usc.md#setFrozenLinearVelocity_float_void) of the Physics class, it is overridden.

## float getFrozenLinearVelocity () const

Returns the current linear velocity threshold for freezing body simulation. If the body linear velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_usc.md#setNumFrozenFrames_int_void) (together with angular one), it stops being updated.
### Return value

Current "freeze" linear velocity. If the value is lower than the [setFrozenLinearVelocity](../../../api/library/physics/class.physics_usc.md#setFrozenLinearVelocity_float_void) of the Physics class, it is overridden.
## void setMaxAngularVelocity ( float velocity )

Sets a new
### Arguments

- *float* **velocity** - The maximum angular velocity in radians per second. If a negative value is provided, **0** will be used instead.

## float getMaxAngularVelocity () const

Returns the current
### Return value

Current maximum angular velocity in radians per second. If a negative value is provided, **0** will be used instead.
## void setMaxLinearVelocity ( float velocity )

Sets a new
### Arguments

- *float* **velocity** - The maximum linear velocity in radians per second. If a negative value is provided, **0** will be used instead.

## float getMaxLinearVelocity () const

Returns the current
### Return value

Current maximum linear velocity in radians per second. If a negative value is provided, **0** will be used instead.
## void setAngularDamping ( float damping )

Sets a new angular damping of the body.
### Arguments

- *float* **damping** - The angular damping. If a negative value is provided, **0** will be used instead.

## float getAngularDamping () const

Returns the current angular damping of the body.
### Return value

Current angular damping. If a negative value is provided, **0** will be used instead.
## void setLinearDamping ( float damping )

Sets a new linear damping of the body.
### Arguments

- *float* **damping** - The linear damping. If a negative value is provided, **0** will be used instead.

## float getLinearDamping () const

Returns the current linear damping of the body.
### Return value

Current linear damping. If a negative value is provided, **0** will be used instead.
## void setAngularScale ( vec3 scale )

Sets a new multiplier for the body's angular velocity per axis. If one of vec3 values is set to **0**, movement along this axis will be restricted. For example, for 2D physics with movement restricted to a X axis, set the body's angular scale to (1,0,0).
### Arguments

- *vec3* **scale** - The angular scale per axis, in world coordinates.

## vec3 getAngularScale () const

Returns the current multiplier for the body's angular velocity per axis. If one of vec3 values is set to **0**, movement along this axis will be restricted. For example, for 2D physics with movement restricted to a X axis, set the body's angular scale to (1,0,0).
### Return value

Current angular scale per axis, in world coordinates.
## void setLinearScale ( vec3 scale )

Sets a new multiplier for the body's linear velocity per axis. if one of vec3 values is set to **0**, movement along this axis will be restricted. For example, for 2D physics with movement restricted to a X axis, set the body's linear scale to (0,1,1).
### Arguments

- *vec3* **scale** - The linear scale per axis, in world coordinates.

## vec3 getLinearScale () const

Returns the current multiplier for the body's linear velocity per axis. if one of vec3 values is set to **0**, movement along this axis will be restricted. For example, for 2D physics with movement restricted to a X axis, set the body's linear scale to (0,1,1).
### Return value

Current linear scale per axis, in world coordinates.
## Vec3 getWorldCenterOfMass () const

Returns the current world coordinates of the body's center of mass.
### Return value

Current world coordinates of the body's center of mass.
## void setCenterOfMass ( vec3 mass )

Sets a new coordinates of the center of mass of the body.
> **Notice:** If the [Shape-based](#setShapeBased_int_void) option is enabled, ajusting this parameter will cause the **assertion failure**, because in this case the center of mass is calculated (i.e. set) automatically.


### Arguments

- *vec3* **mass** - The coordinates of the center of mass in local space of the body.

## vec3 getCenterOfMass () const

Returns the current coordinates of the center of mass of the body.
> **Notice:** If the [Shape-based](#setShapeBased_int_void) option is enabled, ajusting this parameter will cause the **assertion failure**, because in this case the center of mass is calculated (i.e. set) automatically.


### Return value

Current coordinates of the center of mass in local space of the body.
## mat3 getIWorldInertia () const

Returns the current inverse [inertia tensor](#setInertia_mat3_void) of the body, in the world coordinates.
### Return value

Current inverse inertia tensor of the body, in the world coordinates.
## void setInertia ( mat3 inertia )

Sets a new [inertia tensor](#setInertia_mat3_void) of the body. The inertia tensor describes the distribution of the mass over the body relative to the body's center of mass.
> **Notice:** If the [Shape-based](#setShapeBased_int_void) option is enabled, ajusting this parameter will cause the **assertion failure**, because in this case the inertia tensor is calculated (i.e. set) automatically.


### Arguments

- *mat3* **inertia** - The inertia tensor.

## mat3 getInertia () const

Returns the current [inertia tensor](#setInertia_mat3_void) of the body. The inertia tensor describes the distribution of the mass over the body relative to the body's center of mass.
> **Notice:** If the [Shape-based](#setShapeBased_int_void) option is enabled, ajusting this parameter will cause the **assertion failure**, because in this case the inertia tensor is calculated (i.e. set) automatically.


### Return value

Current inertia tensor.
## float getIMass () const

Returns the current inverse mass of the body.
### Return value

Current inverse mass of the body.
## void setMass ( float mass )

Sets a new body mass. If *g* (Earth's gravity) equals to 9.8 m/s2, and 1 unit equals to 1 m, the mass is measured in kilograms.
> **Notice:** If the [Shape-based](#setShapeBased_int_void) option is enabled, ajusting this parameter will cause the **assertion failure**, because in this case the mass is calculated (i.e. set) automatically.


### Arguments

- *float* **mass** - The mass of the body.

## float getMass () const

Returns the current body mass. If *g* (Earth's gravity) equals to 9.8 m/s2, and 1 unit equals to 1 m, the mass is measured in kilograms.
> **Notice:** If the [Shape-based](#setShapeBased_int_void) option is enabled, ajusting this parameter will cause the **assertion failure**, because in this case the mass is calculated (i.e. set) automatically.


### Return value

Current mass of the body.
## void setHighPriorityContacts ( int contacts )

Sets a new value indicating if the body has the priority of handling detected contacts it participates in. A contact can be handled by any of the bodies that participate in it. To which body a contact is assigned is random. If the contact is assigned to and handled by the body it is called an *internal* one, otherwise it is called *external* (handled by another body). Iterating through internal contacts is much faster than through external ones, so this method can be used if you want a certain body to handle most of the contacts it participates in (i.e., have them as internal) to gain some performance.
> **Notice:** A contact between two bodies with high priority shall be handled by one of them determined at random.


### Arguments

- *int* **contacts** - The high priority of handling detected contacts for the body

## int isHighPriorityContacts () const

Returns the current value indicating if the body has the priority of handling detected contacts it participates in. A contact can be handled by any of the bodies that participate in it. To which body a contact is assigned is random. If the contact is assigned to and handled by the body it is called an *internal* one, otherwise it is called *external* (handled by another body). Iterating through internal contacts is much faster than through external ones, so this method can be used if you want a certain body to handle most of the contacts it participates in (i.e., have them as internal) to gain some performance.
> **Notice:** A contact between two bodies with high priority shall be handled by one of them determined at random.


### Return value

Current high priority of handling detected contacts for the body
## void setFreezable ( int freezable )

Sets a new value indicating if the object is freezable, meaning that it is not simulated if both its linear and angular velocities are below "freeze" ones (see *[setFrozenLinearVelocity](#setFrozenLinearVelocity_float_void) and [setFrozenAngularVelocity](#setFrozenAngularVelocity_float_void)* functions).
### Arguments

- *int* **freezable** - The the "freezable" state of the body

## int isFreezable () const

Returns the current value indicating if the object is freezable, meaning that it is not simulated if both its linear and angular velocities are below "freeze" ones (see *[setFrozenLinearVelocity](#setFrozenLinearVelocity_float_void) and [setFrozenAngularVelocity](#setFrozenAngularVelocity_float_void)* functions).
### Return value

Current the "freezable" state of the body
## void setShapeBased ( int based )

Sets a new value indicating if mass and inertia of the body are bound to its shape properties and cannot be changed manually.
### Arguments

- *int* **based** - The calculation of mass and inertia based on shape properties

## int isShapeBased () const

Returns the current value indicating if mass and inertia of the body are bound to its shape properties and cannot be changed manually.
### Return value

Current calculation of mass and inertia based on shape properties
---

## static BodyRigid ( )

Constructor. Creates a rigid body with default properties.
## static BodyRigid ( Object object )

Constructor. Creates a rigid body with default properties for a given object.
### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Object approximated with the new rigid body.

## vec3 getVelocity ( vec3 radius )

Returns the total linear velocity of the point determined by a given radius vector, specified in the local coordinates.
### Arguments

- *vec3* **radius** - Radius vector starting in the body's center of mass.

### Return value

Total linear velocity in the given point of the body.
## vec3 getWorldVelocity ( Vec3 point )

Returns the total linear velocity of the point specified in world coordinates.
### Arguments

- *Vec3* **point** - Point of the body, in world coordinates.

### Return value

Total linear velocity in the given point.
## void addForce ( vec3 force )


Applies a force to the center of mass of the body.


Unlike [impulses](#addImpulse_vec3_vec3_void), all forces are accumulated first, then the resulting force is calculated and applied to the body (during the physics simulation stage, when the body *update()* function is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply forces in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *vec3* **force** - Force to be applied, in world coordinates.

## void addForce ( vec3 radius , vec3 force )


Applies a force to a point determined by a given radius vector, specified in the local coordinates. This function calculates the cross product of the radius vector and the force vector. It acts like a lever arm that changes both linear and angular velocities of the body.


Unlike [impulses](#addImpulse_vec3_vec3_void), all forces are accumulated first, then the resulting force is calculated and applied to the body (during the physics simulation stage, when the body *update()* function is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply forces in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *vec3* **radius** - Radius vector, traced from the center of mass of the body to the point where the force is applied.
- *vec3* **force** - Force to be applied, in world coordinates.

## void addImpulse ( vec3 radius , vec3 impulse )


Applies an impulse to a point determined by a given radius vector, specified in the local coordinates.


Unlike [forces](#addForce_vec3_void), impulses immediately affect both linear and angular velocities of the body.


### Arguments

- *vec3* **radius** - Radius vector, traced from the center of mass to the point where the impulse is applied.
- *vec3* **impulse** - Impulse to be applied, in world coordinates.

## void addLinearImpulse ( vec3 impulse )

Applies an impulse similar to the [addImpulse()](#addImpulse_vec3_vec3_void) method, but affects only the linear velocity.
### Arguments

- *vec3* **impulse** - Impulse to be applied, in world coordinates.

## void addAngularImpulse ( vec3 impulse )

Applies an impulse similar to the [addImpulse()](#addImpulse_vec3_vec3_void) method, but affects only the angular velocity.
### Arguments

- *vec3* **impulse** - Impulse to be applied, in world coordinates.

## void addTorque ( vec3 torque )


Applies a torque with a pivot point at the center of mass of the body, specified in the local coordinates.


All torque values are accumulated first, then the resulting torque is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply forces in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *vec3* **torque** - Torque to be applied, in world coordinates.

## void addTorque ( vec3 radius , vec3 torque )


Applies a torque with a pivot point, determined by a given radius vector, specified in the local coordinates.


This function calculates the cross product of the radius vector and the force vector.


It acts like a lever arm that changes both angular and linear velocities of the body.


All torque values are accumulated first, then the resulting torque is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply torques in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *vec3* **radius** - Radius vector starting at the body's center of mass. Its end is the pivot point for the torque to be applied.
- *vec3* **torque** - Torque to be applied, in world coordinates.

## void addWorldForce ( Vec3 point , vec3 force )


Applies a force to a given point of the body that is specified in world coordinates. This function calculates the cross product of the radius vector (a vector from the center of mass to the point where force is applied) and the force vector. It acts like a lever arm that changes both linear and angular velocities of the body.


Unlike [impulses](#addWorldImpulse_Vec3_vec3_void), all forces are accumulated first, then the resulting force is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply forces in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *Vec3* **point** - Point of the body, in world coordinates.
- *vec3* **force** - Force to be applied, in world coordinates.

## void addWorldImpulse ( Vec3 point , vec3 impulse )

Applies an impulse to a given point of the body, that is specified in world coordinates. Unlike [forces](#addWorldForce_Vec3_vec3_void), impulses immediately affect both linear and angular velocities of the body.
### Arguments

- *Vec3* **point** - Point of the body, in world coordinates.
- *vec3* **impulse** - Impulse to be applied, in world coordinates.

## void addWorldTorque ( Vec3 point , vec3 torque )


Applies a torque with a pivot point at a given point of the body, that is specified in world coordinates. This function calculates the cross product of the radius vector (a vector from the center of mass to the pivot point) and the torque vector. It acts like a lever arm that changes both angular and linear velocities of the body.


All torque values are accumulated first, then the resulting torque is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply torques in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *Vec3* **point** - Point of the body, in world coordinates.
- *vec3* **torque** - Torque to be applied, in world coordinates.

## int createShapes ( int depth = 4 , float error = 0.01 , float threshold = 0.01 )

Removes all previously created shapes and creates one or more [convex shapes](../../../api/library/physics/class.shapeconvex_usc.md) approximating the mesh.
### Arguments

- *int* **depth** - Degree of decomposition of the mesh. If **0** or a negative value is provided, only one shape will be created. If a positive **n** is provided, the mesh will be decomposed **n** times. This is an optional parameter.
- *float* **error** - Approximation error, which is used to create convex hulls. This is an optional parameter.
- *float* **threshold** - Threshold, which is used to decide, whether two adjoining convex shapes can be replaced with one larger shape. A pair of shapes is replaced with a larger shape, if their volumes are roughly the same. This value is clamped in the range **[1 E-6; 1]**. This is an optional parameter.

### Return value

**1** if the convex shapes are created successfully; otherwise **0**.
