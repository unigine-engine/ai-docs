# Unigine::BodyFracture Class (CPP)

**Header:** #include <UniginePhysics.h>

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
<summary>Shattering.h | Close</summary>

```cpp
#pragma once
#include <UnigineGame.h>
#include <UnigineControls.h>

// include the header file of the Component System
#include <UnigineComponentSystem.h>

using namespace Unigine;

class Shattering : public ComponentBase
{
public:

	COMPONENT_DEFINE(Shattering, ComponentBase)

	// declare methods to be called at the corresponding stages of the execution sequence
	COMPONENT_INIT(init);
	COMPONENT_UPDATE(update);
	COMPONENT_SHUTDOWN(shutdown);

	// parameter that specifies an object to be shattered
	PROP_PARAM(Node, dynamicObject);
	// parameter that specifies a material to be applied to the shattered pieces
	PROP_PARAM(Material, shatteredObjectMaterial);

protected:

	// world main loop overrides
	void init();
	void update();
	void shutdown();

	// a fracture body for the object to be shattered
	BodyFracturePtr bf;
};

```

</details>


<details>
<summary>Shattering.cpp | Close</summary>

```cpp
#include "Shattering.h"
#include <UnigineConsole.h>
#include <UnigineRender.h>

REGISTER_COMPONENT(Shattering);		// macro for component registration by the Component System

void Shattering::init()
{
	// create a fracture body for the object to be shattered
	bf = BodyFracture::create(checked_ptr_cast<ObjectMeshDynamic>(dynamicObject->getNode(dynamicObject->getID())));
	// specify the minimum volume threshold for shattering
	bf->setThreshold(0.01f);
	// set the material for the shattered pieces
	bf->setMaterial(shatteredObjectMaterial);
	// break the object into shattered pieces.
	bf->createShatterPieces(2);
	// change the broken flag
	bf->setBroken(true);
}

void Shattering::update() {}
void Shattering::shutdown() {}

```

</details>


### Slicing Example


[Slicing](../../../principles/physics/bodies/fracture/index.md#slice) is a fracture pattern separating the mesh volume into two pieces by a plane at a specified point of the body. The slicing angle is determined by a specified normal.


<details>
<summary>Slicing.h | Close</summary>

```cpp
#pragma once
#include <UnigineGame.h>
#include <UnigineControls.h>

// include the header file of the Component System
#include <UnigineComponentSystem.h>

using namespace Unigine;

class Slicing : public ComponentBase
{
public:

	COMPONENT_DEFINE(Slicing, ComponentBase)

	// declare methods to be called at the corresponding stages of the execution sequence
	COMPONENT_INIT(init);
	COMPONENT_UPDATE(update);
	COMPONENT_SHUTDOWN(shutdown);

	// parameter that specifies an object to be sliced
	PROP_PARAM(Node, dynamicObject);
	// parameter that specifies a material to be applied to the slices
	PROP_PARAM(Material, slicedObjectMaterial);

protected:

	// world main loop overrides
	void init();
	void update();
	void shutdown();

	// a fracture body for the object to be sliced
	BodyFracturePtr bf;
};

```

</details>


<details>
<summary>Slicing.cpp | Close</summary>

```cpp
#include "Slicing.h"
#include <UnigineConsole.h>
#include <UnigineRender.h>

REGISTER_COMPONENT(Slicing);		// macro for component registration by the Component System

using namespace Math;

void Slicing::init()
{
	// create a fracture body for the object to be sliced
	bf = BodyFracture::create(checked_ptr_cast<ObjectMeshDynamic>(dynamicObject->getNode(dynamicObject->getID())));
	// specify the minimum volume threshold for slicing
	bf->setThreshold(0.01f);
	// set the material for the slices
	bf->setMaterial(slicedObjectMaterial);
	// cut the body at the specified point
	vec3 point = bf->getTransform() * vec3_zero;
	bf->createSlicePieces(point, vec3_one);
	// change the broken flag
	bf->setBroken(true);
}

void Slicing::update() {}
void Slicing::shutdown() {}

```

</details>


### Cracking Example


[Cracking](../../../principles/physics/bodies/fracture/index.md#crack) is a fracture pattern involving formation of radial cracks from the point of collision.


<details>
<summary>Cracking.h | Close</summary>

```cpp
#pragma once
#include <UnigineGame.h>
#include <UnigineControls.h>

// include the header file of the Component System
#include <UnigineComponentSystem.h>

using namespace Unigine;

class Cracking : public ComponentBase
{
public:

	COMPONENT_DEFINE(Cracking, ComponentBase)

	// declare methods to be called at the corresponding stages of the execution sequence
	COMPONENT_INIT(init);
	COMPONENT_UPDATE(update);
	COMPONENT_SHUTDOWN(shutdown);

	// parameter that specifies an object to be cracked
	PROP_PARAM(Node, dynamicObject);
	// parameter that specifies a material to be applied to the pieces
	PROP_PARAM(Material, crackedObjectMaterial);

protected:

	// world main loop overrides
	void init();
	void update();
	void shutdown();

	// a fracture body for the object to be cracked
	BodyFracturePtr bf;
};

```

</details>


<details>
<summary>Cracking.cpp | Close</summary>

```cpp
#include "Cracking.h"
#include <UnigineConsole.h>
#include <UnigineRender.h>

REGISTER_COMPONENT(Cracking);		// macro for component registration by the Component System

using namespace Math;

void Cracking::init()
{
	// create a fracture body for the object to be cracked
	bf = BodyFracture::create(checked_ptr_cast<ObjectMeshDynamic>(dynamicObject->getNode(dynamicObject->getID())));
	// specify the minimum volume threshold for cracking
	bf->setThreshold(0.01f);
	// set the material for the pieces
	bf->setMaterial(crackedObjectMaterial);
	// break the body at the specified point
	vec3 point = bf->getTransform() * vec3_zero;
	bf->createCrackPieces(point, vec3_one,7,3,0.1f);
	// change the broken flag
	bf->setBroken(true);
}

void Cracking::update() {}
void Cracking::shutdown() {}

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

### Members

## void setBroken ( bool broken )

Sets a new value indicating if the object is broken or remains its solid state.
### Arguments

- *bool* **broken** - true if the object is broken; false if it remains solid

## bool isBroken () const

Returns the current value indicating if the object is broken or remains its solid state.
### Return value

true if the object is broken; false if it remains solid
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

Sets a new maximum possible angular velocity for the body. if the value is lower than the [engine.physics.setMaxAngularVelocity](../../../api/library/physics/class.physics_cpp.md#setMaxAngularVelocity_float_void) one, it is overridden.
### Arguments

- *float* **velocity** - The maximum possible angular velocity for the body

## float getMaxAngularVelocity () const

Returns the current maximum possible angular velocity for the body. if the value is lower than the [engine.physics.setMaxAngularVelocity](../../../api/library/physics/class.physics_cpp.md#setMaxAngularVelocity_float_void) one, it is overridden.
### Return value

Current maximum possible angular velocity for the body
## void setMaxLinearVelocity ( float velocity )

Sets a new maximum possible linear velocity for the body. if the value is lower than the [engine.physics.setMaxLinearVelocity](../../../api/library/physics/class.physics_cpp.md#setMaxLinearVelocity_float_void) one, it is overridden.
### Arguments

- *float* **velocity** - The maximum possible linear velocity for the body

## float getMaxLinearVelocity () const

Returns the current maximum possible linear velocity for the body. if the value is lower than the [engine.physics.setMaxLinearVelocity](../../../api/library/physics/class.physics_cpp.md#setMaxLinearVelocity_float_void) one, it is overridden.
### Return value

Current maximum possible linear velocity for the body
## void setFrozenAngularVelocity ( float velocity )

Sets a new angular velocity threshold for freezing body simulation. if body angular velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_cpp.md#setNumFrozenFrames_int_void) (together with linear one), it stops to be updated.
### Arguments

- *float* **velocity** - The angular velocity threshold for freezing body simulation

## float getFrozenAngularVelocity () const

Returns the current angular velocity threshold for freezing body simulation. if body angular velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_cpp.md#setNumFrozenFrames_int_void) (together with linear one), it stops to be updated.
### Return value

Current angular velocity threshold for freezing body simulation
## void setFrozenLinearVelocity ( float velocity )

Sets a new linear velocity threshold for freezing body simulation. if body linear velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_cpp.md#setNumFrozenFrames_int_void) (together with angular one), it stops to be updated.
### Arguments

- *float* **velocity** - The linear velocity threshold for freezing body simulation

## float getFrozenLinearVelocity () const

Returns the current linear velocity threshold for freezing body simulation. if body linear velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_cpp.md#setNumFrozenFrames_int_void) (together with angular one), it stops to be updated.
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
## Ptr < BodyRigid > getBodyRigid () const

Returns the current internal [body rigid](../../../api/library/physics/class.bodyrigid_cpp.md) body that represents fracture body until it is broken.
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
## void setMaterial ( const Ptr < Material >& material )

Sets a new material for fractured verge surfaces appearing after breaking the body.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)>&* **material** - The material for fractured verge surfaces

## Ptr < Material > getMaterial () const

Returns the current material for fractured verge surfaces appearing after breaking the body.
### Return value

Current material for fractured verge surfaces
## void setSurfaceProperty ( const char * property )

Sets a new property for cracked verge surfaces appearing after breaking the body.
### Arguments

- *const char ** **property** - The property for cracked verge surfaces

## const char * getSurfaceProperty () const

Returns the current property for cracked verge surfaces appearing after breaking the body.
### Return value

Current property for cracked verge surfaces
## void setMaterialGUID ( UGUID guid )

Sets a new [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the material used for fractured verge surfaces.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cpp.md)* **guid** - The Material [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

## UGUID getMaterialGUID () const

Returns the current [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the material used for fractured verge surfaces.
### Return value

Current Material [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
## void setMaterialFilePath ( const char * path )

Sets a new path of the material file used for fractured verge surfaces.
### Arguments

- *const char ** **path** - The Material file path.

## String getMaterialFilePath () const

Returns the current path of the material file used for fractured verge surfaces.
### Return value

Current Material file path.
---

## static BodyFracturePtr create ( )

Constructor. Creates a fracture body with default properties.
## static BodyFracturePtr create ( const Ptr < Object > & object )

Constructor. Creates a fracture body with default properties for a given object.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)> &* **object** - Object represented with the new fracture body.

## Math:: vec3 getVelocity ( const Math::vec3& radius ) const

Returns the total linear velocity in the point determined by a given radius vector, specified in the local coordinates.
### Arguments

- *const  Math::vec3&* **radius** - Radius vector starting in the body's center of mass.

### Return value

Total linear velocity in the given point.
## Math:: vec3 getWorldVelocity ( const Math::Vec3& point ) const

Returns the total linear velocity in the point specified in world coordinates.
### Arguments

- *const  Math::Vec3&* **point** - Point of the body in world coordinates.

### Return value

Total linear velocity in the given point.
## void addForce ( const Math::vec3& force ) const


Applies a force to the center of mass of the body.


Unlike [impulses](#addImpulse_vec3_vec3_void), all forces are accumulated first, then the resulting force is calculated and applied to the body (during the physics simulation stage, when the body *update()* function is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply forces in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *const  Math::vec3&* **force** - Force to be applied, in world coordinates.

## void addForce ( const Math::vec3& radius , const Math::vec3& force ) const


Applies a force to a point determined by a given radius vector, specified in the local coordinates. This function calculates the cross product of the radius vector and the force vector. It acts like a lever arm that changes both linear and angular velocities of the body.


Unlike [impulses](#addImpulse_vec3_vec3_void), all forces are accumulated first, then the resulting force is calculated and applied to the body (during the physics simulation stage, when the body *update()* function is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply forces in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *const  Math::vec3&* **radius** - Radius vector, traced from the center of mass of the body to the point where the force is applied, in local coordinates.
- *const  Math::vec3&* **force** - Force to be applied, in world coordinates.

## void addImpulse ( const Math::vec3& radius , const Math::vec3& impulse )


Applies an impulse to a point determined by a given radius vector, specified in the local coordinates.


Unlike [forces](#addForce_vec3_void), impulses immediately affect both linear and angular velocities of the body.


### Arguments

- *const  Math::vec3&* **radius** - Radius vector, traced from the center of mass to the point where the impulse is applied, in local coordinates.
- *const  Math::vec3&* **impulse** - Impulse to be applied, in world coordinates.

## void addTorque ( const Math::vec3& torque ) const


Applies a torque with a pivot point at the center of mass of the body, specified in the local coordinates.


All torque values are accumulated first, then the resulting torque is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply torques in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *const  Math::vec3&* **torque** - Torque to be applied, in world coordinates.

## void addTorque ( const Math::vec3& radius , const Math::vec3& torque ) const


Applies a torque with a pivot point, determined by a given radius vector, specified in the local coordinates.


This function calculates the cross product of the radius vector and the force vector.


It acts like a lever arm that changes both angular and linear velocities of the body.


All torque values are accumulated first, then the resulting torque is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply torques in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *const  Math::vec3&* **radius** - Radius vector starting at the body's center of mass, in local coordinates. Its end is the pivot point for the torque to be applied.
- *const  Math::vec3&* **torque** - Torque to be applied, in world coordinates.

## void addWorldForce ( const Math::Vec3& point , const Math::vec3& force )


Applies a force to a given point of the body that is specified in world coordinates. This function calculates the cross product of the radius vector (a vector from the center of mass to the point where force is applied) and the force vector. It acts like a lever arm that changes both linear and angular velocities of the body.


Unlike [impulses](#addWorldImpulse_Vec3_vec3_void), all forces are accumulated first, then the resulting force is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply forces in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *const  Math::Vec3&* **point** - Point of the body in world coordinates.
- *const  Math::vec3&* **force** - Force to be applied, in world coordinates.

## void addWorldImpulse ( const Math::Vec3& point , const Math::vec3& impulse )

Applies an impulse to a given point of the body, that is specified in world coordinates. Unlike [forces](#addWorldForce_Vec3_vec3_void), impulses immediately affect both linear and angular velocities of the body.
### Arguments

- *const  Math::Vec3&* **point** - Point of the body in world coordinates.
- *const  Math::vec3&* **impulse** - Impulse to be applied, in world coordinates.

## void addWorldTorque ( const Math::Vec3& point , const Math::vec3& torque )


Applies a torque with a pivot point at a given point of the body, that is specified in world coordinates. This function calculates the cross product of the radius vector (a vector from the center of mass to the pivot point) and the torque vector. It acts like a lever arm that changes both angular and linear velocities of the body.


All torque values are accumulated first, then the resulting torque is calculated and applied to the body (during the physics simulation stage, when the body update is called).


> **Notice:** You can call this function only from *[updatePhysics()](../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics)* function in the world script. Do not apply torques in the *[update()](../../../code/fundamentals/execution_sequence/code_update.md#code_update)* function, because you will get unstable result that varies each rendering frame.


### Arguments

- *const  Math::Vec3&* **point** - Point of the body in world coordinates.
- *const  Math::vec3&* **torque** - Torque to be applied, in world coordinates.

## int createCrackPieces ( const Math::Vec3& point , const Math::vec3& normal , int num_cuts , int num_rings , float step )

Breaks the object into radial cracks combined with concentric splits. If the first concentric split is rendered further than the specified step distance, decrease the [volume threshold](#setThreshold_float_void) value.
### Arguments

- *const  Math::Vec3&* **point** - Point of contact.
- *const  Math::vec3&* **normal** - Normal of the contact point.
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
## int createSlicePieces ( const Math::Vec3& point , const Math::vec3& normal )

Breaks the object into two slices, slitting the body according to the normal of the specified point.
### Arguments

- *const  Math::Vec3&* **point** - Point of contact.
- *const  Math::vec3&* **normal** - Normal of the contact point.

### Return value

Positive number if the object was successfully broken; otherwise, **0**.
