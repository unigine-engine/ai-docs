# Unigine::BodyRigid Class (CS)

**Inherits from:** Body


This class is used to simulate [rigid bodies](../../../principles/physics/bodies/rigid/index.md) that move according to the [rigid bodies dynamics](../../../principles/physics/bodies/index.md#rigid_bodies_dynamics).


### See Also


- The [Handling Contacts on Collision](../../../code/usage/handling_contacts_on_collision/index_cs.md) usage example


## BodyRigid Class

### Properties

## vec3 AngularVelocity

The angular velocity of the body.
## vec3 LinearVelocity

The linear velocity of the body.
## float FrozenAngularVelocity

The angular velocity threshold for freezing body simulation. If the body angular velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_cs.md#setNumFrozenFrames_int_void) (together with linear one), it stops being updated.
## float FrozenLinearVelocity

The linear velocity threshold for freezing body simulation. If the body linear velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_cs.md#setNumFrozenFrames_int_void) (together with angular one), it stops being updated.
## float MaxAngularVelocity

The maximum angular velocity of the body.
## float MaxLinearVelocity

The maximum linear velocity of the body.
## float AngularDamping

The angular damping of the body.
## float LinearDamping

The linear damping of the body.
## vec3 AngularScale

The multiplier for the body's angular velocity per axis. If one of vec3 values is set to **0**, movement along this axis will be restricted. For example, for 2D physics with movement restricted to a X axis, set the body's angular scale to (1,0,0).
## vec3 LinearScale

The multiplier for the body's linear velocity per axis. if one of vec3 values is set to **0**, movement along this axis will be restricted. For example, for 2D physics with movement restricted to a X axis, set the body's linear scale to (0,1,1).
## 🔒︎ vec3 WorldCenterOfMass

The world coordinates of the body's center of mass.
## vec3 CenterOfMass

The coordinates of the center of mass of the body.
> **Notice:** If the [Shape-based](#setShapeBased_int_void) option is enabled, ajusting this parameter will cause the **assertion failure**, because in this case the center of mass is calculated (i.e. set) automatically.


## 🔒︎ mat3 IWorldInertia

The inverse [inertia tensor](#setInertia_mat3_void) of the body, in the world coordinates.
## mat3 Inertia

The [inertia tensor](#setInertia_mat3_void) of the body. The inertia tensor describes the distribution of the mass over the body relative to the body's center of mass.
> **Notice:** If the [Shape-based](#setShapeBased_int_void) option is enabled, ajusting this parameter will cause the **assertion failure**, because in this case the inertia tensor is calculated (i.e. set) automatically.


## 🔒︎ float IMass

The inverse mass of the body.
## float Mass

The body mass. If *g* (Earth's gravity) equals to 9.8 m/s2, and 1 unit equals to 1 m, the mass is measured in kilograms.
> **Notice:** If the [Shape-based](#setShapeBased_int_void) option is enabled, ajusting this parameter will cause the **assertion failure**, because in this case the mass is calculated (i.e. set) automatically.


## bool HighPriorityContacts

The value indicating if the body has the priority of handling detected contacts it participates in. A contact can be handled by any of the bodies that participate in it. To which body a contact is assigned is random. If the contact is assigned to and handled by the body it is called an *internal* one, otherwise it is called *external* (handled by another body). Iterating through internal contacts is much faster than through external ones, so this method can be used if you want a certain body to handle most of the contacts it participates in (i.e., have them as internal) to gain some performance.
> **Notice:** A contact between two bodies with high priority shall be handled by one of them determined at random.


## bool Freezable

The value indicating if the object is freezable, meaning that it is not simulated if both its linear and angular velocities are below "freeze" ones (see *[setFrozenLinearVelocity](#setFrozenLinearVelocity_float_void) and [setFrozenAngularVelocity](#setFrozenAngularVelocity_float_void)* functions).
## bool ShapeBased

The value indicating if mass and inertia of the body are bound to its shape properties and cannot be changed manually.
### Members

---

## BodyRigid ( )

Constructor. Creates a rigid body with default properties.
## BodyRigid ( Object object )

Constructor. Creates a rigid body with default properties for a given object.
### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object approximated with the new rigid body.

## vec3 GetVelocity ( vec3 radius )

Returns the total linear velocity of the point determined by a given radius vector, specified in the local coordinates.
### Arguments

- *vec3* **radius** - Radius vector starting in the body's center of mass.

### Return value

Total linear velocity in the given point of the body.
## vec3 GetWorldVelocity ( vec3 point )

Returns the total linear velocity of the point specified in world coordinates.
### Arguments

- *vec3* **point** - Point of the body, in world coordinates.

### Return value

Total linear velocity in the given point.
## void AddForce ( vec3 force )


Applies a force to the center of mass of the body.


Unlike [impulses](#addImpulse_vec3_vec3_void), all forces are accumulated first, then the resulting force is calculated and applied to the body (during the physics simulation stage, when the body *update()* function is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply forces in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *vec3* **force** - Force to be applied, in world coordinates.

## void AddForce ( vec3 radius , vec3 force )


Applies a force to a point determined by a given radius vector, specified in the local coordinates. This function calculates the cross product of the radius vector and the force vector. It acts like a lever arm that changes both linear and angular velocities of the body.


Unlike [impulses](#addImpulse_vec3_vec3_void), all forces are accumulated first, then the resulting force is calculated and applied to the body (during the physics simulation stage, when the body *update()* function is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply forces in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *vec3* **radius** - Radius vector, traced from the center of mass of the body to the point where the force is applied.
- *vec3* **force** - Force to be applied, in world coordinates.

## void AddImpulse ( vec3 radius , vec3 impulse )


Applies an impulse to a point determined by a given radius vector, specified in the local coordinates.


Unlike [forces](#addForce_vec3_void), impulses immediately affect both linear and angular velocities of the body.


### Arguments

- *vec3* **radius** - Radius vector, traced from the center of mass to the point where the impulse is applied.
- *vec3* **impulse** - Impulse to be applied, in world coordinates.

## void AddLinearImpulse ( vec3 impulse )

Applies an impulse similar to the [addImpulse()](#addImpulse_vec3_vec3_void) method, but affects only the linear velocity.
### Arguments

- *vec3* **impulse** - Impulse to be applied, in world coordinates.

## void AddAngularImpulse ( vec3 impulse )

Applies an impulse similar to the [addImpulse()](#addImpulse_vec3_vec3_void) method, but affects only the angular velocity.
### Arguments

- *vec3* **impulse** - Impulse to be applied, in world coordinates.

## void AddTorque ( vec3 torque )


Applies a torque with a pivot point at the center of mass of the body, specified in the local coordinates.


All torque values are accumulated first, then the resulting torque is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply forces in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *vec3* **torque** - Torque to be applied, in world coordinates.

## void AddTorque ( vec3 radius , vec3 torque )


Applies a torque with a pivot point, determined by a given radius vector, specified in the local coordinates.


This function calculates the cross product of the radius vector and the force vector.


It acts like a lever arm that changes both angular and linear velocities of the body.


All torque values are accumulated first, then the resulting torque is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply torques in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *vec3* **radius** - Radius vector starting at the body's center of mass. Its end is the pivot point for the torque to be applied.
- *vec3* **torque** - Torque to be applied, in world coordinates.

## void AddWorldForce ( vec3 point , vec3 force )


Applies a force to a given point of the body that is specified in world coordinates. This function calculates the cross product of the radius vector (a vector from the center of mass to the point where force is applied) and the force vector. It acts like a lever arm that changes both linear and angular velocities of the body.


Unlike [impulses](#addWorldImpulse_Vec3_vec3_void), all forces are accumulated first, then the resulting force is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply forces in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *vec3* **point** - Point of the body, in world coordinates.
- *vec3* **force** - Force to be applied, in world coordinates.

## void AddWorldImpulse ( vec3 point , vec3 impulse )

Applies an impulse to a given point of the body, that is specified in world coordinates. Unlike [forces](#addWorldForce_Vec3_vec3_void), impulses immediately affect both linear and angular velocities of the body.
### Arguments

- *vec3* **point** - Point of the body, in world coordinates.
- *vec3* **impulse** - Impulse to be applied, in world coordinates.

## void AddWorldTorque ( vec3 point , vec3 torque )


Applies a torque with a pivot point at a given point of the body, that is specified in world coordinates. This function calculates the cross product of the radius vector (a vector from the center of mass to the pivot point) and the torque vector. It acts like a lever arm that changes both angular and linear velocities of the body.


All torque values are accumulated first, then the resulting torque is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply torques in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *vec3* **point** - Point of the body, in world coordinates.
- *vec3* **torque** - Torque to be applied, in world coordinates.

## int CreateShapes ( int depth = 4 , float error = 0.01 , float threshold = 0.01 )

Removes all previously created shapes and creates one or more [convex shapes](../../../api/library/physics/class.shapeconvex_cs.md) approximating the mesh.
### Arguments

- *int* **depth** - Degree of decomposition of the mesh. If **0** or a negative value is provided, only one shape will be created. If a positive **n** is provided, the mesh will be decomposed **n** times. This is an optional parameter.
- *float* **error** - Approximation error, which is used to create convex hulls. This is an optional parameter.
- *float* **threshold** - Threshold, which is used to decide, whether two adjoining convex shapes can be replaced with one larger shape. A pair of shapes is replaced with a larger shape, if their volumes are roughly the same. This value is clamped in the range **[1 E-6; 1]**. This is an optional parameter.

### Return value

**1** if the convex shapes are created successfully; otherwise **0**.
