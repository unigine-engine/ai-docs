# Unigine::BodyRope Class (CS)

**Inherits from:** BodyParticles


This class is used to simulate [ropes, cables, wires](../../../principles/physics/bodies/rope/index.md), etc. This body uses the [Mass-Spring model](../../../principles/physics/bodies/rope/index.md#model) for simulation, ensuring the rope ability to [fold, stretch](../../../principles/physics/bodies/rope/index.md#stretching) and even [tear](../../../principles/physics/bodies/rope/index.md#tearing). Unlike the flat [BodyCloth](../../../api/library/physics/class.bodycloth_cs.md), they always preserve the same number of polygons in cross-section as in the source rope mesh. It means, the rope, when twisted, will never appear flat.


#### See Also


- The [Creating Pylons and Wires Using Ropes](../../../code/usage/ropes_creating_pylons_and_wires/index_cs.md) usage example demonstrating how to assign a rope body to a dynamic mesh object and set its parameters
- UnigineScript samples:

  -
  -
  -
  -


## BodyRope Class

### Members

---

## BodyRope ( )

Constructor. Creates a rope body with default properties.
## BodyRope ( Object object )

Constructor. Creates a rope body with default properties for a given object.
### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object represented with the new rope body.
