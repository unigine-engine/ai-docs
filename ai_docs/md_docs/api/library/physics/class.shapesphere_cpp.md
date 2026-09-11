# Unigine::ShapeSphere Class (CPP)

**Header:** #include <UniginePhysics.h>

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

## void setCenter ( const Math:: Vec3 & center )

Sets a new center of the sphere, in world coordinates.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)&* **center** - The center of the sphere, in world coordinates

## Math:: Vec3 getCenter () const

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

## static ShapeSpherePtr create ( )

Constructor. Creates a new sphere with the zero radius.
## static ShapeSpherePtr create ( float radius )

Constructor. Creates a new sphere with a given radius.
### Arguments

- *float* **radius** - Radius of the sphere in units.

## static ShapeSpherePtr create ( const Ptr < Body > & body , float radius )

Constructor. Creates a new sphere with a given radius and adds it to a given body.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body** - Body, to which the shape will belong.
- *float* **radius** - Radius of the sphere in units.
