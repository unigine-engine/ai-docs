# Unigine::ShapeCapsule Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Shape


This class is used to create collision shape in the form of a [capsule](../../../principles/physics/shapes/index.md#capsule).


### See Also


UnigineScript samples:


-
-
-
-


## ShapeCapsule Class

### Members

## void setHeight ( float height )

Sets a new height of the capsule, in units.
### Arguments

- *float* **height** - The height of the capsule, in units

## float getHeight () const

Returns the current height of the capsule, in units.
### Return value

Current height of the capsule, in units
## void setRadius ( float radius )

Sets a new radius of the capsule, in units.
### Arguments

- *float* **radius** - The radius of the capsule, in units

## float getRadius () const

Returns the current radius of the capsule, in units.
### Return value

Current radius of the capsule, in units
## Vec3 getTopCap () const

Returns the current coordinates of the center of the top hemisphere of the capsule.
### Return value

Current coordinates of the center of the top hemisphere of the capsule
## Vec3 getBottomCap () const

Returns the current coordinates of the center of the bottom hemisphere of the capsule.
### Return value

Current coordinates of the center of the bottom hemisphere of the capsule
---

## static ShapeCapsule ( )

Constructor. Creates a new capsule with the zero radius and the zero height.
## static ShapeCapsule ( float radius , float height )

Constructor. Creates a new capsule with given dimensions.
### Arguments

- *float* **radius** - Radius of the capsule in units.
- *float* **height** - Height of the capsule in units.

## static ShapeCapsule ( Body body , float radius , float height )

Constructor. Creates a new capsule with given dimensions and adds it to a given body.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body** - Body, to which the capsule will belong.
- *float* **radius** - Radius of the capsule in units.
- *float* **height** - Height of the capsule in units.
