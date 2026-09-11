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

## void setBroken ( int broken )

Sets a new value indicating if the object is broken or remains its solid state.
### Arguments

- *int* **broken** - The true if the object is broken; false if it remains solid

## int isBroken () const

Returns the current value indicating if the object is broken or remains its solid state.
### Return value

Current true if the object is broken; false if it remains solid
## void setCollisionMask ( int mask )

Sets a new collision bit mask for the body. two objects collide, if they both have matching masks. see also details on additional [collision exclusion mask](#getExclusionMask_int).
### Arguments

- *int* **mask** - The collision bit mask for the body

## int getCollisionMask () const

Returns the current collision bit mask for the body. two objects collide, if they both have matching masks. see also details on additional [collision exclusion mask](#getExclusionMask_int).
### Return value

Current collision bit mask for the body
## void setDensity ( float density )

Sets a new density of the body.
### Arguments

- *float* **density** - The density of the body

## float getDensity () const

Returns the current density of the body.
### Return value

Current density of the body
## void setError ( float error )

Sets a new approximation error permissible by creating convex shape for the mesh.
### Arguments

- *float* **error** - The approximation error permissible when creating a convex shape

## float getError () const

Returns the current approximation error permissible by creating convex shape for the mesh.
### Return value

Current approximation error permissible when creating a convex shape
## void setExclusionMask ( int mask )

Sets a new bit mask that prevents collisions of the body with other ones. this mask is independent of the [collision mask](#getCollisionMask_int). For bodies with matching collision masks not to collide, at least one bit of their exclusion mask should match.
### Arguments

- *int* **mask** - The collision exclusion bit mask for the body

## int getExclusionMask () const

Returns the current bit mask that prevents collisions of the body with other ones. this mask is independent of the [collision mask](#getCollisionMask_int). For bodies with matching collision masks not to collide, at least one bit of their exclusion mask should match.
### Return value

Current collision exclusion bit mask for the body
## void setFriction ( float friction )

Sets a new friction of the body against other surfaces.
### Arguments

- *float* **friction** - The friction of the body against other surfaces

## float getFriction () const

Returns the current friction of the body against other surfaces.
### Return value

Current friction of the body against other surfaces
## void setThreshold ( float threshold )

Sets a new minimum volume threshold for breaking. if the piece volume is less than the threshold value, it cannot be fractured further.
### Arguments

- *float* **threshold** - The minimum volume threshold for breaking

## float getThreshold () const

Returns the current minimum volume threshold for breaking. if the piece volume is less than the threshold value, it cannot be fractured further.
### Return value

Current minimum volume threshold for breaking
## void setRestitution ( float restitution )

Sets a new restitution that determines body bouncing off the surfaces.
### Arguments

- *float* **restitution** - The restitution that determines body bouncing off surfaces

## float getRestitution () const

Returns the current restitution that determines body bouncing off the surfaces.
### Return value

Current restitution that determines body bouncing off surfaces
## void setPhysicsIntersectionMask ( int mask )

Sets a new [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for the body.
### Arguments

- *int* **mask** - The physics intersection mask for the body

## int getPhysicsIntersectionMask () const

Returns the current [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for the body.
### Return value

Current physics intersection mask for the body
## void setMaxAngularVelocity ( float velocity )

Sets a new maximum possible angular velocity for the body. if the value is lower than the [engine.physics.setMaxAngularVelocity](../../../api/library/physics/class.physics_usc.md#setMaxAngularVelocity_float_void) one, it is overridden.
### Arguments

- *float* **velocity** - The maximum possible angular velocity for the body

## float getMaxAngularVelocity () const

Returns the current maximum possible angular velocity for the body. if the value is lower than the [engine.physics.setMaxAngularVelocity](../../../api/library/physics/class.physics_usc.md#setMaxAngularVelocity_float_void) one, it is overridden.
### Return value

Current maximum possible angular velocity for the body
## void setMaxLinearVelocity ( float velocity )

Sets a new maximum possible linear velocity for the body. if the value is lower than the [engine.physics.setMaxLinearVelocity](../../../api/library/physics/class.physics_usc.md#setMaxLinearVelocity_float_void) one, it is overridden.
### Arguments

- *float* **velocity** - The maximum possible linear velocity for the body

## float getMaxLinearVelocity () const

Returns the current maximum possible linear velocity for the body. if the value is lower than the [engine.physics.setMaxLinearVelocity](../../../api/library/physics/class.physics_usc.md#setMaxLinearVelocity_float_void) one, it is overridden.
### Return value

Current maximum possible linear velocity for the body
## void setFrozenAngularVelocity ( float velocity )

Sets a new angular velocity threshold for freezing body simulation. if body angular velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_usc.md#setNumFrozenFrames_int_void) (together with linear one), it stops to be updated.
### Arguments

- *float* **velocity** - The angular velocity threshold for freezing body simulation

## float getFrozenAngularVelocity () const

Returns the current angular velocity threshold for freezing body simulation. if body angular velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_usc.md#setNumFrozenFrames_int_void) (together with linear one), it stops to be updated.
### Return value

Current angular velocity threshold for freezing body simulation
## void setFrozenLinearVelocity ( float velocity )

Sets a new linear velocity threshold for freezing body simulation. if body linear velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_usc.md#setNumFrozenFrames_int_void) (together with angular one), it stops to be updated.
### Arguments

- *float* **velocity** - The linear velocity threshold for freezing body simulation

## float getFrozenLinearVelocity () const

Returns the current linear velocity threshold for freezing body simulation. if body linear velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_usc.md#setNumFrozenFrames_int_void) (together with angular one), it stops to be updated.
### Return value

Current linear velocity threshold for freezing body simulation
## void setMass ( float mass )

Sets a new mass of the body.
### Arguments

- *float* **mass** - The mass of the body

## float getMass () const

Returns the current mass of the body.
### Return value

Current mass of the body
## BodyRigid getBodyRigid () const

Returns the current internal [body rigid](../../../api/library/physics/class.bodyrigid_usc.md) body that represents fracture body until it is broken.
### Return value

Current internal rigid body representing the fracture body
## void setLinearDamping ( float damping )

Sets a new damping of the body linear velocity.
### Arguments

- *float* **damping** - The damping of the body linear velocity

## float getLinearDamping () const

Returns the current damping of the body linear velocity.
### Return value

Current damping of the body linear velocity
## void setAngularDamping ( float damping )

Sets a new damping of the body angular velocity.
### Arguments

- *float* **damping** - The damping of the body angular velocity

## float getAngularDamping () const

Returns the current damping of the body angular velocity.
### Return value

Current damping of the body angular velocity
## void setMaterial ( Material material )

Sets a new material for fractured verge surfaces appearing after breaking the body.
### Arguments

- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - The material for fractured verge surfaces

## Material getMaterial () const

Returns the current material for fractured verge surfaces appearing after breaking the body.
### Return value

Current material for fractured verge surfaces
## void setSurfaceProperty ( string property )

Sets a new property for cracked verge surfaces appearing after breaking the body.
### Arguments

- *string* **property** - The property for cracked verge surfaces

## const char * getSurfaceProperty () const

Returns the current property for cracked verge surfaces appearing after breaking the body.
### Return value

Current property for cracked verge surfaces
## void setMaterialGUID ( UGUID guid )

Sets a new [GUID](../../../api/library/filesystem/class.uguid_usc.md) of the material used for fractured verge surfaces.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_usc.md)* **guid** - The Material [GUID](../../../api/library/filesystem/class.uguid_usc.md).

## UGUID getMaterialGUID () const

Returns the current [GUID](../../../api/library/filesystem/class.uguid_usc.md) of the material used for fractured verge surfaces.
### Return value

Current Material [GUID](../../../api/library/filesystem/class.uguid_usc.md).
## void setMaterialFilePath ( )

Sets a new path of the material file used for fractured verge surfaces.
### Arguments

- **path** - The Material file path.

## String getMaterialFilePath () const

Returns the current path of the material file used for fractured verge surfaces.
### Return value

Current Material file path.
---

## static BodyFracture ( )

Constructor. Creates a fracture body with default properties.
## static BodyFracture ( Object object )

Constructor. Creates a fracture body with default properties for a given object.
### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Object represented with the new fracture body.

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
