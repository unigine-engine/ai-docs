# Unigine::ShapeCylinder Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

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

### Members

---

## static ShapeCylinder ( )

Constructor. Creates a new cylinder with the zero radius and the zero height.
## static ShapeCylinder ( float radius , float height )

Constructor. Creates a new cylinder with given dimensions.
### Arguments

- *float* **radius** - Radius of the cylinder in units.
- *float* **height** - Height of the cylinder in units.

## static ShapeCylinder ( Body body , float radius , float height )

Constructor. Creates a new cylinder with given dimensions and adds it to a given body.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body** - Body, to which the cylinder will belong.
- *float* **radius** - Radius of the cylinder in units.
- *float* **height** - Height of the cylinder in units.

## void setHeight ( float height )

Sets a height of the cylinder.
### Arguments

- *float* **height** - Height of the cylinder in units.

## float getHeight ( )

Returns the current height of the cylinder.
### Return value

Height of the cylinder in units.
## void setRadius ( float radius )

Sets a radius of the cylinder.
### Arguments

- *float* **radius** - Radius of the cylinder in units.

## float getRadius ( )

Returns the current radius of the cylinder.
### Return value

Radius of the cylinder in units.
