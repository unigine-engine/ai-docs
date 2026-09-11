# Unigine::ShapeSphere Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Shape


This class is used to create collision shape in the form of a [sphere](../../../principles/physics/shapes/index.md#sphere).


### See Also


UnigineScript samples:


-
-
-
-
-
-


## ShapeSphere Class

### Members

## void setCenter ( Vec3 center )

Sets a new center of the sphere, in world coordinates.
### Arguments

- *Vec3* **center** - The center of the sphere, in world coordinates

## Vec3 getCenter () const

Returns the current center of the sphere, in world coordinates.
### Return value

Current center of the sphere, in world coordinates
## void setRadius ( float radius )

Sets a new radius of the sphere, in units.
### Arguments

- *float* **radius** - The radius of the sphere, in units

## float getRadius () const

Returns the current radius of the sphere, in units.
### Return value

Current radius of the sphere, in units
---

## static ShapeSphere ( )

Constructor. Creates a new sphere with the zero radius.
## static ShapeSphere ( float radius )

Constructor. Creates a new sphere with a given radius.
### Arguments

- *float* **radius** - Radius of the sphere in units.

## static ShapeSphere ( Body body , float radius )

Constructor. Creates a new sphere with a given radius and adds it to a given body.
### Arguments

- *[Body](../../../api/library/physics/class.body_usc.md)* **body** - Body, to which the shape will belong.
- *float* **radius** - Radius of the sphere in units.
