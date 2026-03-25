# Unigine::BodyFracture Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Body


This class is used to simulate destructable [fracture bodies](../../../principles/physics/bodies/fracture/index.md).

> **Notice:** Fracture body can be used with meshes in form of a simple primitive: boxes, spheres, capsules, cylinders, etc. Complex meshes cannot be fractured procedurally.

 There are three patterns of the fracturing:
- [Cracking](../../../principles/physics/bodies/fracture/index.md#crack) ([*createCrackPieces()*](#createCrackPieces_Vec3_vec3_int_int_float_int))
- [Shattering](../../../principles/physics/bodies/fracture/index.md#shatter) ([*createShatterPieces()*](#createShatterPieces_int_int))
- [Slicing](../../../principles/physics/bodies/fracture/index.md#slice) ([*createSlicePieces()*](#createSlicePieces_Vec3_vec3_int))


New surfces that are created when fracturing occurs are assigned their own [material](#setMaterial_Material_void) and [properties](#setSurfaceProperty_cstr_void).

> **Notice:** The [material](#setMaterial_Material_void) and properties must be specified before destructing the object.

 Also a [minimum volume threshold](#setThreshold_float_void) must be specified before breaking. The piece volume must be greater than the threshold value, otherwise the object won't be fractured.
Fracture body is, per se, a [rigid body](#getBodyRigid_BodyRigid) and moves according to the [rigid bodies dynamics](../../../principles/physics/bodies/index.md#rigid_bodies_dynamics).


### Shattering Example


[Shattering](../../../principles/physics/bodies/fracture/index.md#shatter) is a fracture pattern randomly dividing the mesh volume into the specified number of convex chunks.


### Slicing Example


[Slicing](../../../principles/physics/bodies/fracture/index.md#slice) is a fracture pattern separating the mesh volume into two pieces by a plane at a specified point of the body. The slicing angle is determined by a specified normal.


### Cracking Example


[Cracking](../../../principles/physics/bodies/fracture/index.md#crack) is a fracture pattern involving formation of radial cracks from the point of collision.


### See Also


- C++ samples:

  -
  -
  -
- C# Component samples:

  -
  -
  -
- UnigineScript samples:

  -
  -
  -
  -
  -
  -
  -


## BodyFracture Class

### Members

---

## static BodyFracture ( )

Constructor. Creates a fracture body with default properties.
## static BodyFracture ( Object object )

Constructor. Creates a fracture body with default properties for a given object.
### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Object represented with the new fracture body.

## void setAngularDamping ( float damping )

Sets the damping of the body angular velocity.
### Arguments

- *float* **damping** - Angular damping value.

## float getAngularDamping ( )

Returns the current damping of the body angular velocity.
### Return value

Angular damping value.
## BodyRigid getBodyRigid ( )

Returns an internal [body rigid](../../../api/library/physics/class.bodyrigid_usc.md) body that represents fracture body until it is broken.
### Return value

Internal body rigid.
## void setBroken ( int broken )

Sets a value indicating if the object is broken or remains its solid state.
### Arguments

- *int* **broken** - **1** to indicate the object as [broken](../../../principles/physics/bodies/fracture/index.md#broken); **0** for it to remain solid.

## int isBroken ( )

Returns a value indicating if the object is broken or remains its solid state.
### Return value

**1** if the object is already [broken](../../../principles/physics/bodies/fracture/index.md#broken); **0** if it is still solid.
## void setCollisionMask ( int mask )

Sets a collision bit mask for the body. Two objects collide, if they both have matching masks. See also details on additional [collision exclusion mask](#setExclusionMask_int_void).
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getCollisionMask ( )

Returns the collision bit mask for the body. Two objects collide, if they both have matching masks. See also details on additional [collision exclusion mask](#getExclusionMask_int).
### Return value

Integer, each bit of which is a mask.
## void setDensity ( float density )

Sets density of a body. Changing the density influences the mass, that is computed by multiplying body volume by density.
### Arguments

- *float* **density** - Density of the body.

## float getDensity ( )

Returns the current density of the body.
### Return value

Density of the body.
## void setError ( float error )

Sets approximation error permissible by creating convex shape for the mesh.
### Arguments

- *float* **error** - Approximation error. If a negative value is provided, **0** will be used instead.

## float getError ( )

Returns the current approximation error permissible by creating convex shape for the mesh.
### Return value

Approximation error.
## void setExclusionMask ( int mask )

Sets a bit mask to prevent collisions of the body with other ones. This mask is independent of the [collision mask](#setCollisionMask_int_void). For bodies with matching collision masks not to collide, at least one bit of their exclusion mask should match. **0** is to collide with all bodies with a matching collision mask.
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getExclusionMask ( )

Returns the bit mask that prevents collisions of the body with other ones. This mask is independent of the [collision mask](#getCollisionMask_int). For bodies with matching collision masks not to collide, at least one bit of their exclusion mask should match.
### Return value

Integer, each bit of which is a mask.
## void setFriction ( float friction )

Sets friction of the body against other surfaces.
### Arguments

- *float* **friction** - Friction value.

## float getFriction ( )

Returns the current friction of the body against other surfaces.
### Return value

Friction value.
## void setFrozenAngularVelocity ( float velocity )

Sets angular velocity threshold for freezing body simulation. If body angular velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_usc.md#setNumFrozenFrames_int_void) (together with linear one), it stops to be updated.
### Arguments

- *float* **velocity** - "Freeze" angular velocity. If the value is lower than the [engine.physics.setFrozenAngularVelocity](../../../api/library/physics/class.physics_usc.md#setFrozenAngularVelocity_float_void) one, it is overridden.

## float getFrozenAngularVelocity ( )

Returns the current angular velocity threshold for freezing body simulation. If body angular velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_usc.md#setNumFrozenFrames_int_void) (together with linear one), it stops to be updated.
### Return value

"Freeze" angular velocity.
## void setFrozenLinearVelocity ( float velocity )

Sets linear velocity threshold for freezing body simulation. If body linear velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_usc.md#setNumFrozenFrames_int_void) (together with angular one), it stops to be updated.
### Arguments

- *float* **velocity** - "Freeze" linear velocity. If the value is lower than the [engine.physics.setFrozenLinearVelocity](../../../api/library/physics/class.physics_usc.md#setFrozenLinearVelocity_float_void) one, it is overridden.

## float getFrozenLinearVelocity ( )

Returns the current linear velocity threshold for freezing body simulation. If body linear velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_usc.md#setNumFrozenFrames_int_void) (together with angular one), it stops to be updated.
### Return value

"Freeze" linear velocity.
## void setPhysicsIntersectionMask ( int mask )

Sets a [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for the body.
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getPhysicsIntersectionMask ( )

Returns the current [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for the body.
### Return value

Integer, each bit of which is a mask.
## void setLinearDamping ( float damping )

Sets the damping of the body linear velocity.
### Arguments

- *float* **damping** - Linear damping value.

## float getLinearDamping ( )

Returns the current damping of the body linear velocity.
### Return value

Linear damping value.
## void setMass ( float mass )

Sets a mass of the body. Changing the mass influences the density, that is computed by dividing the mass by body volume.
### Arguments

- *float* **mass** - Mass of the body.

## float getMass ( )

Returns the current mass of the body.
### Return value

Mass of the body.
## void setMaterial ( Material material )

Sets the material for fractured verge surfaces appearing after breaking the body.
### Arguments

- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - Material instance.

## Material getMaterial ( )

Returns the material for fractured verge surfaces appearing after breaking the body.
### Return value

Material instance for the fractured verges.
## void setMaxAngularVelocity ( float velocity )

Sets the maximum possible linear velocity for the body. If the value is lower than the [engine.physics.setMaxAngularVelocity](../../../api/library/physics/class.physics_usc.md#setMaxAngularVelocity_float_void) one, it is overridden.
### Arguments

- *float* **velocity** - Maximum possible angular velocity.

## float getMaxAngularVelocity ( )

Returns the current maximum possible angular velocity for the body. If the value is lower than the [engine.physics.setMaxAngularVelocity](../../../api/library/physics/class.physics_usc.md#setMaxAngularVelocity_float_void) one, it is overridden.
### Return value

Maximum possible angular velocity.
## void setMaxLinearVelocity ( float velocity )

Sets the maximum possible linear velocity for the body. If the value is lower than the [engine.physics.setMaxLinearVelocity](../../../api/library/physics/class.physics_usc.md#setMaxLinearVelocity_float_void) one, it is overridden.
### Arguments

- *float* **velocity** - Maximum possible linear velocity.

## float getMaxLinearVelocity ( )

Returns the current maximum possible linear velocity for the body. If the value is lower than the [engine.physics.setMaxLinearVelocity](../../../api/library/physics/class.physics_usc.md#setMaxLinearVelocity_float_void) one, it is overridden.
### Return value

Maximum possible linear velocity.
## void setSurfaceProperty ( string property )

Sets the property for cracked verge surfaces appearing after breaking the body.
### Arguments

- *string* **property** - Property name for the fractured verges.

## string getSurfaceProperty ( )

Returns the property for fractured verge surfaces appearing after breaking the body.
### Return value

Property name for the fractured verges.
## void setRestitution ( float restitution )

Sets the restitution that determines body bouncing off the surfaces.
### Arguments

- *float* **restitution** - Restitution value.

## float getRestitution ( )

Returns the current restitution that determines body bouncing off the surfaces.
### Return value

Restitution value.
## void setThreshold ( float threshold )

Sets the minimum volume threshold for breaking. If the piece volume is less than the threshold value, it cannot be fractured further.
### Arguments

- *float* **threshold** - Volume threshold. If a negative value is provided, **0** will be used instead.

## float getThreshold ( )

Returns the current minimum volume threshold for breaking. If the piece volume is less than the threshold value, it cannot be fractured further.
### Return value

Volume threshold.
## vec3 getVelocity ( vec3 radius )

Returns the total linear velocity in the point determined by a given radius vector, specified in the local coordinates.
### Arguments

- *vec3* **radius** - Radius vector starting in the body's center of mass.

### Return value

Total linear velocity in the given point.
## vec3 getWorldVelocity ( Vec3 point )

Returns the total linear velocity in the point specified in world coordinates.
### Arguments

- *Vec3* **point** - Point of the body in world coordinates.

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

- *vec3* **radius** - Radius vector, traced from the center of mass of the body to the point where the force is applied, in local coordinates.
- *vec3* **force** - Force to be applied, in world coordinates.

## void addImpulse ( vec3 radius , vec3 impulse )


Applies an impulse to a point determined by a given radius vector, specified in the local coordinates.


Unlike [forces](#addForce_vec3_void), impulses immediately affect both linear and angular velocities of the body.


### Arguments

- *vec3* **radius** - Radius vector, traced from the center of mass to the point where the impulse is applied, in local coordinates.
- *vec3* **impulse** - Impulse to be applied, in world coordinates.

## void addTorque ( vec3 torque )


Applies a torque with a pivot point at the center of mass of the body, specified in the local coordinates.


All torque values are accumulated first, then the resulting torque is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply torques in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *vec3* **torque** - Torque to be applied, in world coordinates.

## void addTorque ( vec3 radius , vec3 torque )


Applies a torque with a pivot point, determined by a given radius vector, specified in the local coordinates.


This function calculates the cross product of the radius vector and the force vector.


It acts like a lever arm that changes both angular and linear velocities of the body.


All torque values are accumulated first, then the resulting torque is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply torques in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *vec3* **radius** - Radius vector starting at the body's center of mass, in local coordinates. Its end is the pivot point for the torque to be applied.
- *vec3* **torque** - Torque to be applied, in world coordinates.

## void addWorldForce ( Vec3 point , vec3 force )


Applies a force to a given point of the body that is specified in world coordinates. This function calculates the cross product of the radius vector (a vector from the center of mass to the point where force is applied) and the force vector. It acts like a lever arm that changes both linear and angular velocities of the body.


Unlike [impulses](#addWorldImpulse_Vec3_vec3_void), all forces are accumulated first, then the resulting force is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply forces in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *Vec3* **point** - Point of the body in world coordinates.
- *vec3* **force** - Force to be applied, in world coordinates.

## void addWorldImpulse ( Vec3 point , vec3 impulse )

Applies an impulse to a given point of the body, that is specified in world coordinates. Unlike [forces](#addWorldForce_Vec3_vec3_void), impulses immediately affect both linear and angular velocities of the body.
### Arguments

- *Vec3* **point** - Point of the body in world coordinates.
- *vec3* **impulse** - Impulse to be applied, in world coordinates.

## void addWorldTorque ( Vec3 point , vec3 torque )


Applies a torque with a pivot point at a given point of the body, that is specified in world coordinates. This function calculates the cross product of the radius vector (a vector from the center of mass to the pivot point) and the torque vector. It acts like a lever arm that changes both angular and linear velocities of the body.


All torque values are accumulated first, then the resulting torque is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply torques in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *Vec3* **point** - Point of the body in world coordinates.
- *vec3* **torque** - Torque to be applied, in world coordinates.

## int createCrackPieces ( Vec3 point , vec3 normal , int num_cuts , int num_rings , float step )

Breaks the object into radial cracks combined with concentric splits. If the first concentric split is rendered further than the specified step distance, decrease the [volume threshold](#setThreshold_float_void) value.
### Arguments

- *Vec3* **point** - Point of contact.
- *vec3* **normal** - Normal of the contact point.
- *int* **num_cuts** - Number of radial cuts that are represented as rays coming from the center of contact point.
- *int* **num_rings** - Number of rings that form concentric splits. The number of rings that is will be actually rendered depends on the *step* value.
- *float* **step** - Distance between concentric splits.

### Return value

Positive number if the object was successfully broken; otherwise, **0**.
## int createShatterPieces ( int num_pieces )

Breaks the object into arbitrary shattered pieces.
### Arguments

- *int* **num_pieces** - The number of shattered pieces.

### Return value

Positive number if the object was successfully broken; otherwise, **0**.
## int createSlicePieces ( Vec3 point , vec3 normal )

Breaks the object into two slices, slitting the body according to the normal of the specified point.
### Arguments

- *Vec3* **point** - Point of contact.
- *vec3* **normal** - Normal of the contact point.

### Return value

Positive number if the object was successfully broken; otherwise, **0**.
## void setMaterialFilePath ( string path )

Sets the material to be used for fractured verge surfaces by file path.
### Arguments

- *string* **path** - Material file path.

## string getMaterialFilePath ( )

Returns the path of the material file used for fractured verge surfaces.
### Return value

Material path.
## void setMaterialGUID ( UGUID materialguid )

Sets the material for fractured verge surfaces by [GUID](../../../api/library/filesystem/class.uguid_usc.md).
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **materialguid** - Material [GUID](../../../api/library/filesystem/class.uguid_usc.md).

## UGUID getMaterialGUID ( )

Returns the [GUID](../../../api/library/filesystem/class.uguid_usc.md) of the material for fractured verge surfaces.
### Return value

Material [GUID](../../../api/library/filesystem/class.uguid_usc.md).
