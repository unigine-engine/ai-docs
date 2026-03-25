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

## void setRadius ( float radius )

Sets a radius of the sphere.
### Arguments

- *float* **radius** - Radius of the sphere, in units.

## float getRadius ( )

Returns the current radius of the sphere.
### Return value

Radius of the sphere, in units.
## void setCenter ( Vec3 center )

Sets the coordinates of the center of the sphere.
### Arguments

- *Vec3* **center** - Sphere center coordinates.

## Vec3 getCenter ( )

Returns the current coordinates of the center of the sphere.
### Return value

Current sphere center coordinates.
