# Unigine::BodyWater Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Body


This class is used to simulate [water body](../../../principles/physics/bodies/water/index.md) that provide buoyancy and waves from other physical bodies. It is simulated as a 2D grid with point particles positioned in the vertices of the mesh.


### See Also


- UnigineScript samples:

  -
  -
  -
  -


## BodyWater Class

### Members

## void setLiquidity ( float liquidity )

Sets a new fluidity of the water.
### Arguments

- *float* **liquidity** - The fluidity of the water

## float getLiquidity () const

Returns the current fluidity of the water.
### Return value

Current fluidity of the water
## void setIntersection ( int intersection )

Sets a new value indicating if intersection with the ground is enabled. the ground should be a parent node.
### Arguments

- *int* **intersection** - The true if intersection with the ground is enabled; false if it is disabled

## int getIntersection () const

Returns the current value indicating if intersection with the ground is enabled. the ground should be a parent node.
### Return value

Current true if intersection with the ground is enabled; false if it is disabled
## void setInteractionForce ( float force )

Sets a new interaction force that determines how much velocity values of water and objects that get into it are leveled.
### Arguments

- *float* **force** - The interaction force between water and objects

## float getInteractionForce () const

Returns the current interaction force that determines how much velocity values of water and objects that get into it are leveled.
### Return value

Current interaction force between water and objects
## void setLinearDamping ( float damping )

Sets a new value indicating how much the linear velocity of the objects decreases when they get into the water.
### Arguments

- *float* **damping** - The damping of the objects linear velocity in the water

## float getLinearDamping () const

Returns the current value indicating how much the linear velocity of the objects decreases when they get into the water.
### Return value

Current damping of the objects linear velocity in the water
## void setAngularDamping ( float damping )

Sets a new value indicating how much the angular velocity of the objects decreases when they get into the water.
### Arguments

- *float* **damping** - The damping of the objects angular velocity in the water

## float getAngularDamping () const

Returns the current value indicating how much the angular velocity of the objects decreases when they get into the water.
### Return value

Current damping of the objects angular velocity in the water
## void setDistance ( float distance )

Sets a new distance of water simulation. it does not interfere with objects buoyancy.
### Arguments

- *float* **distance** - The distance of water simulation

## float getDistance () const

Returns the current distance of water simulation. it does not interfere with objects buoyancy.
### Return value

Current distance of water simulation
## void setDepth ( float depth )

Sets a new depth of the water (unless intersection has occurred).
### Arguments

- *float* **depth** - The depth of the water

## float getDepth () const

Returns the current depth of the water (unless intersection has occurred).
### Return value

Current depth of the water
## void setDensity ( float density )

Sets a new density of the water that determines objects buoyancy.
### Arguments

- *float* **density** - The density of the water

## float getDensity () const

Returns the current density of the water that determines objects buoyancy.
### Return value

Current density of the water
## void setAbsorption ( int absorption )

Sets a new value indicating if the waves are dispersed along the mesh perimeter.
### Arguments

- *int* **absorption** - The true if the waves are dispersed along the mesh perimeter; false if they are not

## int getAbsorption () const

Returns the current value indicating if the waves are dispersed along the mesh perimeter.
### Return value

Current true if the waves are dispersed along the mesh perimeter; false if they are not
---

## static BodyWater ( )

Constructor. Creates a water body with default properties.
## static BodyWater ( Object object )

Constructor. Creates a water body with default properties for a given object.
### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Object with a new water body.

## float getParticleHeight ( vec3 position )

Returns the vertical shift of the given point of the water.
### Arguments

- *vec3* **position** - Point local coordinates (only along *X* and *Y* axes).

### Return value

Height in units of the vertical water shift.
## vec3 getParticleVelocity ( vec3 position )

Returns the velocity value in the given point of the water.
### Arguments

- *vec3* **position** - Point local coordinates (only along *X* and *Y* axes).

### Return value

Velocity value.
## void addParticleHeight ( vec3 position , float height )

Adds the vertical shift to the water. Nearby water particles, that form a plane water grid, will change their height accordingly, simulating rings on the water.
### Arguments

- *vec3* **position** - Point local coordinates (only along *X* and *Y* axes) of the vertical shift.
- *float* **height** - Height in units of the vertical water shift.

## void addParticleVelocity ( vec3 position , vec3 velocity )

Applies the force to the water. To nearby water particles, that form a plane water grid, will be passed appropriate velocity values, simulating wake from the moving object.
### Arguments

- *vec3* **position** - Point local coordinates (only along *X* and *Y* axes) of applying the force.
- *vec3* **velocity** - Velocity value.
