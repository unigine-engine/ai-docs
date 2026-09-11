# Unigine::ShapeBox Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

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

### Members

## void setSize ( vec3 size )

Sets a new size of the box, in units.
### Arguments

- *vec3* **size** - The size of the box, in units

## vec3 getSize () const

Returns the current size of the box, in units.
### Return value

Current size of the box, in units
---

## static ShapeBox ( )

Constructor. Creates a new box with zero dimensions.
## static ShapeBox ( vec3 size )

Constructor. Creates a new box with given dimensions.
### Arguments

- *vec3* **size** - Dimensions of the box in units.

## static ShapeBox ( Body body , vec3 size )

Constructor. Creates a new box with given dimensions and adds it to a given body.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body** - Body, to which the box will belong.
- *vec3* **size** - Dimensions of the box in units.
