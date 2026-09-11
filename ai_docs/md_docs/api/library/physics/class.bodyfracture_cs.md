# Unigine::BodyFracture Class (CS)

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


<details>
<summary>Shattering.cs | Close</summary>

```csharp
public partial class Shattering : Component
{
	// declare a parameter that specifies an object to be shattered
	[ShowInEditor]
	[Parameter(Tooltip = "Object to be shattered")]
	private ObjectMeshDynamic dynamicObject = null;

	// declare a parameter that specifies a material to be applied to the shattered pieces
	[ShowInEditor]
	[Parameter(Tooltip = "Shattered object material")]
	private Material shatteredObjectMaterial = null;

	// a fracture body for the object to be shattered
	BodyFracture bf;

	private void Init()
	{
		// create a fracture body for the object to be shattered
		bf = new BodyFracture(dynamicObject);
		// specify the minimum threshold for shattering
		bf.Threshold = 0.01f;
		// set the material for the shattered pieces
		bf.Material = shatteredObjectMaterial;
		// break the object into shattered pieces
		bf.CreateShatterPieces(2);
		// change the broken flag
		bf.Broken = true;
	}
}


```

</details>


### Slicing Example


[Slicing](../../../principles/physics/bodies/fracture/index.md#slice) is a fracture pattern separating the mesh volume into two pieces by a plane at a specified point of the body. The slicing angle is determined by a specified normal.


<details>
<summary>Slicing.cs | Close</summary>

```csharp
public partial class Slicing : Component
{
	// declare a parameter that specifies an object to be sliced
	[ShowInEditor]
	[Parameter(Tooltip = "Object to be sliced")]
	private ObjectMeshDynamic dynamicObject = null;

	// declare a parameter that specifies a material to be applied to the slices
	[ShowInEditor]
	[Parameter(Tooltip = "Sliced object material")]
	private Material slicedObjectMaterial = null;

	BodyFracture bf;

	private void Init()
	{
		// create a fracture body for the object to be sliced
		bf = new BodyFracture(dynamicObject);
		// specify the minimum threshold for slicing
		bf.Threshold = 0.01f;
		// set the material for the slices
		bf.Material = slicedObjectMaterial;
		// cut the body at the specified point
		Vec3 point = bf.Transform * vec3.ZERO;
		bf.CreateSlicePieces(point, vec3.ONE);
		// change the broken flag
		bf.Broken = true;
	}
}


```

</details>


### Cracking Example


[Cracking](../../../principles/physics/bodies/fracture/index.md#crack) is a fracture pattern involving formation of radial cracks from the point of collision.


<details>
<summary>Cracking.cs | Close</summary>

```csharp
public partial class Cracking : Component
{
	// declare a parameter that specifies an object to be cracked
	[ShowInEditor]
	[Parameter(Tooltip = "Object to be cracked")]
	private ObjectMeshDynamic dynamicObject = null;

	// declare a parameter that specifies a material to be applied to the pieces
	[ShowInEditor]
	[Parameter(Tooltip = "Cracked object material")]
	private Material crackedObjectMaterial = null;

	BodyFracture bf;

	private void Init()
	{
		// create a fracture body for the object to be cracked
		bf = new BodyFracture(dynamicObject);
		// specify the minimum threshold for cracking
		bf.Threshold = 0.01f;
		// set the material for the pieces
		bf.Material = crackedObjectMaterial;
		// crack the body at the specified point
		Vec3 point = bf.Transform * vec3.ZERO;
		bf.CreateCrackPieces(point, vec3.ONE, 7,3,0.1f);
		// change the broken flag
		bf.Broken = true;
	}
}


```

</details>


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

### Properties

## bool Broken

The value indicating if the object is broken or remains its solid state.
## int CollisionMask

The collision bit mask for the body. two objects collide, if they both have matching masks. see also details on additional [collision exclusion mask](#getExclusionMask_int).
## float Density

The density of the body.
## float Error

The approximation error permissible by creating convex shape for the mesh.
## int ExclusionMask

The bit mask that prevents collisions of the body with other ones. this mask is independent of the [collision mask](#getCollisionMask_int). For bodies with matching collision masks not to collide, at least one bit of their exclusion mask should match.
## float Friction

The friction of the body against other surfaces.
## float Threshold

The minimum volume threshold for breaking. if the piece volume is less than the threshold value, it cannot be fractured further.
## float Restitution

The restitution that determines body bouncing off the surfaces.
## int PhysicsIntersectionMask

The [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for the body.
## float MaxAngularVelocity

The maximum possible angular velocity for the body. if the value is lower than the [engine.physics.setMaxAngularVelocity](../../../api/library/physics/class.physics_cs.md#setMaxAngularVelocity_float_void) one, it is overridden.
## float MaxLinearVelocity

The maximum possible linear velocity for the body. if the value is lower than the [engine.physics.setMaxLinearVelocity](../../../api/library/physics/class.physics_cs.md#setMaxLinearVelocity_float_void) one, it is overridden.
## float FrozenAngularVelocity

The angular velocity threshold for freezing body simulation. if body angular velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_cs.md#setNumFrozenFrames_int_void) (together with linear one), it stops to be updated.
## float FrozenLinearVelocity

The linear velocity threshold for freezing body simulation. if body linear velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_cs.md#setNumFrozenFrames_int_void) (together with angular one), it stops to be updated.
## float Mass

The mass of the body.
## 🔒︎ BodyRigid BodyRigid

The internal [body rigid](../../../api/library/physics/class.bodyrigid_cs.md) body that represents fracture body until it is broken.
## float LinearDamping

The damping of the body linear velocity.
## float AngularDamping

The damping of the body angular velocity.
## Material Material

The material for fractured verge surfaces appearing after breaking the body.
## string SurfaceProperty

The property for cracked verge surfaces appearing after breaking the body.
## UGUID MaterialGUID

The [GUID](../../../api/library/filesystem/class.uguid_cs.md) of the material used for fractured verge surfaces.
## string MaterialFilePath

The path of the material file used for fractured verge surfaces.
### Members

---

## BodyFracture ( )

Constructor. Creates a fracture body with default properties.
## BodyFracture ( Object object )

Constructor. Creates a fracture body with default properties for a given object.
### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object represented with the new fracture body.

## vec3 GetVelocity ( vec3 radius )

Returns the total linear velocity in the point determined by a given radius vector, specified in the local coordinates.
### Arguments

- *vec3* **radius** - Radius vector starting in the body's center of mass.

### Return value

Total linear velocity in the given point.
## vec3 GetWorldVelocity ( vec3 point )

Returns the total linear velocity in the point specified in world coordinates.
### Arguments

- *vec3* **point** - Point of the body in world coordinates.

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

- *vec3* **radius** - Radius vector, traced from the center of mass of the body to the point where the force is applied, in local coordinates.
- *vec3* **force** - Force to be applied, in world coordinates.

## void AddImpulse ( vec3 radius , vec3 impulse )


Applies an impulse to a point determined by a given radius vector, specified in the local coordinates.


Unlike [forces](#addForce_vec3_void), impulses immediately affect both linear and angular velocities of the body.


### Arguments

- *vec3* **radius** - Radius vector, traced from the center of mass to the point where the impulse is applied, in local coordinates.
- *vec3* **impulse** - Impulse to be applied, in world coordinates.

## void AddTorque ( vec3 torque )


Applies a torque with a pivot point at the center of mass of the body, specified in the local coordinates.


All torque values are accumulated first, then the resulting torque is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply torques in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *vec3* **torque** - Torque to be applied, in world coordinates.

## void AddTorque ( vec3 radius , vec3 torque )


Applies a torque with a pivot point, determined by a given radius vector, specified in the local coordinates.


This function calculates the cross product of the radius vector and the force vector.


It acts like a lever arm that changes both angular and linear velocities of the body.


All torque values are accumulated first, then the resulting torque is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply torques in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *vec3* **radius** - Radius vector starting at the body's center of mass, in local coordinates. Its end is the pivot point for the torque to be applied.
- *vec3* **torque** - Torque to be applied, in world coordinates.

## void AddWorldForce ( vec3 point , vec3 force )


Applies a force to a given point of the body that is specified in world coordinates. This function calculates the cross product of the radius vector (a vector from the center of mass to the point where force is applied) and the force vector. It acts like a lever arm that changes both linear and angular velocities of the body.


Unlike [impulses](#addWorldImpulse_Vec3_vec3_void), all forces are accumulated first, then the resulting force is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply forces in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *vec3* **point** - Point of the body in world coordinates.
- *vec3* **force** - Force to be applied, in world coordinates.

## void AddWorldImpulse ( vec3 point , vec3 impulse )

Applies an impulse to a given point of the body, that is specified in world coordinates. Unlike [forces](#addWorldForce_Vec3_vec3_void), impulses immediately affect both linear and angular velocities of the body.
### Arguments

- *vec3* **point** - Point of the body in world coordinates.
- *vec3* **impulse** - Impulse to be applied, in world coordinates.

## void AddWorldTorque ( vec3 point , vec3 torque )


Applies a torque with a pivot point at a given point of the body, that is specified in world coordinates. This function calculates the cross product of the radius vector (a vector from the center of mass to the pivot point) and the torque vector. It acts like a lever arm that changes both angular and linear velocities of the body.


All torque values are accumulated first, then the resulting torque is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply torques in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *vec3* **point** - Point of the body in world coordinates.
- *vec3* **torque** - Torque to be applied, in world coordinates.

## int CreateCrackPieces ( vec3 point , vec3 normal , int num_cuts , int num_rings , float step )

Breaks the object into radial cracks combined with concentric splits. If the first concentric split is rendered further than the specified step distance, decrease the [volume threshold](#setThreshold_float_void) value.
### Arguments

- *vec3* **point** - Point of contact.
- *vec3* **normal** - Normal of the contact point.
- *int* **num_cuts** - Number of radial cuts that are represented as rays coming from the center of contact point.
- *int* **num_rings** - Number of rings that form concentric splits. The number of rings that is will be actually rendered depends on the *step* value.
- *float* **step** - Distance between concentric splits.

### Return value

Positive number if the object was successfully broken; otherwise, **0**.
## int CreateShatterPieces ( int num_pieces )

Breaks the object into arbitrary shattered pieces.
### Arguments

- *int* **num_pieces** - The number of shattered pieces.

### Return value

Positive number if the object was successfully broken; otherwise, **0**.
## int CreateSlicePieces ( vec3 point , vec3 normal )

Breaks the object into two slices, slitting the body according to the normal of the specified point.
### Arguments

- *vec3* **point** - Point of contact.
- *vec3* **normal** - Normal of the contact point.

### Return value

Positive number if the object was successfully broken; otherwise, **0**.
