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

---

## static BodyWater ( )

Constructor. Creates a water body with default properties.
## static BodyWater ( Object object )

Constructor. Creates a water body with default properties for a given object.
### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Object with a new water body.

## void setAbsorption ( int absorption )

Updates a value indicating if the waves should be dispersed along the mesh perimeter.
### Arguments

- *int* **absorption** - Positive number to allow wave dispersion, **0** for the waves to be reflected.

## int getAbsorption ( )

Returns a value indicating if the waves are dispersed along the mesh perimeter.
### Return value

Positive value, if the waves are dispersed along the mesh perimeter; **0** if they are reflected.
## void setAngularDamping ( float damping )

Updates a value indicating how much the angular velocity of the objects decreases when they get into the water.
### Arguments

- *float* **damping** - Anglular damping value. If a negative value is provided, **0** will be used instead.

## float getAngularDamping ( )

Returns the current value indicating how much the angular velocity of the objects decreases when they get into the water.
### Return value

Anglular damping value.
## void setDensity ( float density )

Updates the density of the water that determines objects buoyancy.
### Arguments

- *float* **density** - Density value. If a negative value is provided, **0** will be used instead.

## float getDensity ( )

Returns the current density of the water that determines objects buoyancy.
### Return value

Density value.
## void setDepth ( float depth )

Updates the depth of the water (unless [intersection](#setIntersection_int_void) has occurred).
### Arguments

- *float* **depth** - Depth value. If a negative value is provided, **0** will be used instead.

## float getDepth ( )

Returns the current depth of the water (unless [intersection](#setIntersection_int_void) has occurred).
### Return value

Depth value.
## void setDistance ( float distance )

Updates the distance of water simulation. It does not interfere with objects buoyancy.
### Arguments

- *float* **distance** - Simulation distance. If a negative value is provided, **0** will be used instead.

## float getDistance ( )

Returns the current distance of water simulation. It does not interfere with objects buoyancy.
### Return value

Simulation distance.
## void setInteractionForce ( float force )

Updates the interaction force that determines how much velocity values of water and objects that get into it are leveled.
### Arguments

- *float* **force** - Interaction force value. If a negative value is provided, **0** will be used instead.

## float getInteractionForce ( )

Returns the current interaction force that determines how much velocity values of water and objects that get into it are leveled.
### Return value

Interaction force value.
## void setIntersection ( int intersection )

Updates a value indicating if intersection with the ground is enabled. The ground should be a parent node.
### Arguments

- *int* **intersection** - Positive value to enable intersection, **0** to disable it.

## int getIntersection ( )

Returns a value indicating if intersection with the ground is enabled. The ground should be a parent node.
### Return value

Positive value if intersection is enabled, **0** if disabled.
## void setLinearDamping ( float damping )

Updates a value indicating how much the linear velocity of the objects decreases when they get into the water.
### Arguments

- *float* **damping** - Linear damping value. If a negative value is provided, **0** will be used instead.

## float getLinearDamping ( )

Returns the current value indicating how much the linear velocity of the objects decreases when they get into the water.
### Return value

Linear damping value.
## void setLiquidity ( float liquidity )

Updates the viscosity of the water.
### Arguments

- *float* **liquidity** - Liquidity value. If a negative value is provided, **0** will be used instead.

## float getLiquidity ( )

Returns the current fluidity of the water.
### Return value

Liquidity value.
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
