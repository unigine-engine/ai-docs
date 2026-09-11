# Unigine::ShapeBox Class (CS)

**Inherits from:** Shape


This class is used to create collision shape in the form of a [box](../../../principles/physics/shapes/index.md#box).


### See Also


UnigineScript samples:


-
-
-
-
-
-
-
-
-
-


## ShapeBox Class

### Properties

## vec3 Size

The size of the box, in units.
### Members

---

## ShapeBox ( )

Constructor. Creates a new box with zero dimensions.
## ShapeBox ( vec3 size )

Constructor. Creates a new box with given dimensions.
### Arguments

- *vec3* **size** - Dimensions of the box in units.

## ShapeBox ( Body body , vec3 size )

Constructor. Creates a new box with given dimensions and adds it to a given body.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body** - Body, to which the box will belong.
- *vec3* **size** - Dimensions of the box in units.
