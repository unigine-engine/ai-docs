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

---

## static BodyFracturePtr create ( )

Constructor. Creates a fracture body with default properties.
## static BodyFracturePtr create ( const Ptr < Object > & object )

Constructor. Creates a fracture body with default properties for a given object.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)> &* **object** - Object represented with the new fracture body.

## void setAngularDamping ( float damping )

Sets the damping of the body angular velocity.
### Arguments

- *float* **damping** - Angular damping value.

## float getAngularDamping ( ) const

Returns the current damping of the body angular velocity.
### Return value

Angular damping value.
## Ptr < BodyRigid > getBodyRigid ( ) const

Returns an internal [body rigid](../../../api/library/physics/class.bodyrigid_cpp.md) body that represents fracture body until it is broken.
### Return value

Internal body rigid.
## void setBroken ( bool broken )

Sets a value indicating if the object is broken or remains its solid state.
### Arguments

- *bool* **broken** - true to indicate the object as [broken](../../../principles/physics/bodies/fracture/index.md#broken); false for it to remain solid.

## bool isBroken ( ) const

Returns a value indicating if the object is broken or remains its solid state.
### Return value

true if the object is already [broken](../../../principles/physics/bodies/fracture/index.md#broken); false if it is still solid.
## void setCollisionMask ( int mask )

Sets a collision bit mask for the body. Two objects collide, if they both have matching masks. See also details on additional [collision exclusion mask](#setExclusionMask_int_void).
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getCollisionMask ( ) const

Returns the collision bit mask for the body. Two objects collide, if they both have matching masks. See also details on additional [collision exclusion mask](#getExclusionMask_int).
### Return value

Integer, each bit of which is a mask.
## void setDensity ( float density )

Sets density of a body. Changing the density influences the mass, that is computed by multiplying body volume by density.
### Arguments

- *float* **density** - Density of the body.

## float getDensity ( ) const

Returns the current density of the body.
### Return value

Density of the body.
## void setError ( float error )

Sets approximation error permissible by creating convex shape for the mesh.
### Arguments

- *float* **error** - Approximation error. If a negative value is provided, **0** will be used instead.

## float getError ( ) const

Returns the current approximation error permissible by creating convex shape for the mesh.
### Return value

Approximation error.
## void setExclusionMask ( int mask )

Sets a bit mask to prevent collisions of the body with other ones. This mask is independent of the [collision mask](#setCollisionMask_int_void). For bodies with matching collision masks not to collide, at least one bit of their exclusion mask should match. **0** is to collide with all bodies with a matching collision mask.
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getExclusionMask ( ) const

Returns the bit mask that prevents collisions of the body with other ones. This mask is independent of the [collision mask](#getCollisionMask_int). For bodies with matching collision masks not to collide, at least one bit of their exclusion mask should match.
### Return value

Integer, each bit of which is a mask.
## void setFriction ( float friction )

Sets friction of the body against other surfaces.
### Arguments

- *float* **friction** - Friction value.

## float getFriction ( ) const

Returns the current friction of the body against other surfaces.
### Return value

Friction value.
## void setFrozenAngularVelocity ( float velocity )

Sets angular velocity threshold for freezing body simulation. If body angular velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_cpp.md#setNumFrozenFrames_int_void) (together with linear one), it stops to be updated.
### Arguments

- *float* **velocity** - "Freeze" angular velocity. If the value is lower than the [engine.physics.setFrozenAngularVelocity](../../../api/library/physics/class.physics_cpp.md#setFrozenAngularVelocity_float_void) one, it is overridden.

## float getFrozenAngularVelocity ( ) const

Returns the current angular velocity threshold for freezing body simulation. If body angular velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_cpp.md#setNumFrozenFrames_int_void) (together with linear one), it stops to be updated.
### Return value

"Freeze" angular velocity.
## void setFrozenLinearVelocity ( float velocity )

Sets linear velocity threshold for freezing body simulation. If body linear velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_cpp.md#setNumFrozenFrames_int_void) (together with angular one), it stops to be updated.
### Arguments

- *float* **velocity** - "Freeze" linear velocity. If the value is lower than the [engine.physics.setFrozenLinearVelocity](../../../api/library/physics/class.physics_cpp.md#setFrozenLinearVelocity_float_void) one, it is overridden.

## float getFrozenLinearVelocity ( ) const

Returns the current linear velocity threshold for freezing body simulation. If body linear velocity remains lower than this threshold during the number of [Frozen frames](../../../api/library/physics/class.physics_cpp.md#setNumFrozenFrames_int_void) (together with angular one), it stops to be updated.
### Return value

"Freeze" linear velocity.
## void setPhysicsIntersectionMask ( int mask )

Sets a [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for the body.
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getPhysicsIntersectionMask ( ) const

Returns the current [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) for the body.
### Return value

Integer, each bit of which is a mask.
## void setLinearDamping ( float damping )

Sets the damping of the body linear velocity.
### Arguments

- *float* **damping** - Linear damping value.

## float getLinearDamping ( ) const

Returns the current damping of the body linear velocity.
### Return value

Linear damping value.
## void setMass ( float mass )

Sets a mass of the body. Changing the mass influences the density, that is computed by dividing the mass by body volume.
### Arguments

- *float* **mass** - Mass of the body.

## float getMass ( ) const

Returns the current mass of the body.
### Return value

Mass of the body.
## void setMaterial ( const Ptr < Material > & material )

Sets the material for fractured verge surfaces appearing after breaking the body.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Material smart pointer.

## Ptr < Material > getMaterial ( ) const

Returns the material for fractured verge surfaces appearing after breaking the body.
### Return value

Smart pointer for the material of the fractured verges.
## void setMaxAngularVelocity ( float velocity )

Sets the maximum possible linear velocity for the body. If the value is lower than the [engine.physics.setMaxAngularVelocity](../../../api/library/physics/class.physics_cpp.md#setMaxAngularVelocity_float_void) one, it is overridden.
### Arguments

- *float* **velocity** - Maximum possible angular velocity.

## float getMaxAngularVelocity ( ) const

Returns the current maximum possible angular velocity for the body. If the value is lower than the [engine.physics.setMaxAngularVelocity](../../../api/library/physics/class.physics_cpp.md#setMaxAngularVelocity_float_void) one, it is overridden.
### Return value

Maximum possible angular velocity.
## void setMaxLinearVelocity ( float velocity )

Sets the maximum possible linear velocity for the body. If the value is lower than the [engine.physics.setMaxLinearVelocity](../../../api/library/physics/class.physics_cpp.md#setMaxLinearVelocity_float_void) one, it is overridden.
### Arguments

- *float* **velocity** - Maximum possible linear velocity.

## float getMaxLinearVelocity ( ) const

Returns the current maximum possible linear velocity for the body. If the value is lower than the [engine.physics.setMaxLinearVelocity](../../../api/library/physics/class.physics_cpp.md#setMaxLinearVelocity_float_void) one, it is overridden.
### Return value

Maximum possible linear velocity.
## void setSurfaceProperty ( const char * property )

Sets the property for cracked verge surfaces appearing after breaking the body.
### Arguments

- *const char ** **property** - Property name for the fractured verges.

## const char * getSurfaceProperty ( ) const

Returns the property for fractured verge surfaces appearing after breaking the body.
### Return value

Property name for the fractured verges.
## void setRestitution ( float restitution )

Sets the restitution that determines body bouncing off the surfaces.
### Arguments

- *float* **restitution** - Restitution value.

## float getRestitution ( ) const

Returns the current restitution that determines body bouncing off the surfaces.
### Return value

Restitution value.
## void setThreshold ( float threshold )

Sets the minimum volume threshold for breaking. If the piece volume is less than the threshold value, it cannot be fractured further.
### Arguments

- *float* **threshold** - Volume threshold. If a negative value is provided, **0** will be used instead.

## float getThreshold ( ) const

Returns the current minimum volume threshold for breaking. If the piece volume is less than the threshold value, it cannot be fractured further.
### Return value

Volume threshold.
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
## void setMaterialFilePath ( const char * path )

Sets the material to be used for fractured verge surfaces by file path.
### Arguments

- *const char ** **path** - Material file path.

## String getMaterialFilePath ( ) const

Returns the path of the material file used for fractured verge surfaces.
### Return value

Material path.
## void setMaterialGUID ( const UGUID& materialguid )

Sets the material for fractured verge surfaces by [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
### Arguments

- *const UGUID&* **materialguid** - Material [GUID](../../../api/library/filesystem/class.uguid_cpp.md).

## UGUID getMaterialGUID ( ) const

Returns the [GUID](../../../api/library/filesystem/class.uguid_cpp.md) of the material for fractured verge surfaces.
### Return value

Material [GUID](../../../api/library/filesystem/class.uguid_cpp.md).
