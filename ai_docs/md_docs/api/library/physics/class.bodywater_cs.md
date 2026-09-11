# Unigine::BodyWater Class (CS)

**Inherits from:** Body


This class is used to simulate [water body](../../../principles/physics/bodies/water/index.md) that provide buoyancy and waves from other physical bodies. It is simulated as a 2D grid with point particles positioned in the vertices of the mesh.


### See Also


- UnigineScript samples:

  -
  -
  -
  -


## BodyWater Class

### Properties

## float Liquidity

The fluidity of the water.
## bool Intersection

The value indicating if intersection with the ground is enabled. the ground should be a parent node.
## float InteractionForce

The interaction force that determines how much velocity values of water and objects that get into it are leveled.
## float LinearDamping

The value indicating how much the linear velocity of the objects decreases when they get into the water.
## float AngularDamping

The value indicating how much the angular velocity of the objects decreases when they get into the water.
## float Distance

The distance of water simulation. it does not interfere with objects buoyancy.
## float Depth

The depth of the water (unless intersection has occurred).
## float Density

The density of the water that determines objects buoyancy.
## bool Absorption

The value indicating if the waves are dispersed along the mesh perimeter.
### Members

---

## BodyWater ( )

Constructor. Creates a water body with default properties.
## BodyWater ( Object object )

Constructor. Creates a water body with default properties for a given object.
### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object with a new water body.

## float GetParticleHeight ( vec3 position )

Returns the vertical shift of the given point of the water.
### Arguments

- *vec3* **position** - Point local coordinates (only along *X* and *Y* axes).

### Return value

Height in units of the vertical water shift.
## vec3 GetParticleVelocity ( vec3 position )

Returns the velocity value in the given point of the water.
### Arguments

- *vec3* **position** - Point local coordinates (only along *X* and *Y* axes).

### Return value

Velocity value.
## void AddParticleHeight ( vec3 position , float height )

Adds the vertical shift to the water. Nearby water particles, that form a plane water grid, will change their height accordingly, simulating rings on the water.
### Arguments

- *vec3* **position** - Point local coordinates (only along *X* and *Y* axes) of the vertical shift.
- *float* **height** - Height in units of the vertical water shift.

## void AddParticleVelocity ( vec3 position , vec3 velocity )

Applies the force to the water. To nearby water particles, that form a plane water grid, will be passed appropriate velocity values, simulating wake from the moving object.
### Arguments

- *vec3* **position** - Point local coordinates (only along *X* and *Y* axes) of applying the force.
- *vec3* **velocity** - Velocity value.
