# Unigine::ShapeCylinder Class (CS)

**Inherits from:** Shape


This class is used to create collision shape in the form of a [cylinder](../../../principles/physics/shapes/index.md#cylinder).


### See Also


UnigineScript samples:


-
-
-
-
-
-


## ShapeCylinder Class

### Properties

## float Height

The height of the cylinder, in units.
## float Radius

The radius of the cylinder, in units.
### Members

---

## ShapeCylinder ( )

Constructor. Creates a new cylinder with the zero radius and the zero height.
## ShapeCylinder ( float radius , float height )

Constructor. Creates a new cylinder with given dimensions.
### Arguments

- *float* **radius** - Radius of the cylinder in units.
- *float* **height** - Height of the cylinder in units.

## ShapeCylinder ( Body body , float radius , float height )

Constructor. Creates a new cylinder with given dimensions and adds it to a given body.
### Arguments

- *[Body](../../../api/library/physics/class.body_cs.md)* **body** - Body, to which the cylinder will belong.
- *float* **radius** - Radius of the cylinder in units.
- *float* **height** - Height of the cylinder in units.
