# Unigine::ShapeCapsule Class (CPP)

**Header:** #include <UniginePhysics.h>

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

---

## static ShapeCapsulePtr create ( )

Constructor. Creates a new capsule with the zero radius and the zero height.
## static ShapeCapsulePtr create ( float radius , float height )

Constructor. Creates a new capsule with given dimensions.
### Arguments

- *float* **radius** - Radius of the capsule in units.
- *float* **height** - Height of the capsule in units.

## static ShapeCapsulePtr create ( const Ptr < Body > & body , float radius , float height )

Constructor. Creates a new capsule with given dimensions and adds it to a given body.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body** - Body, to which the capsule will belong.
- *float* **radius** - Radius of the capsule in units.
- *float* **height** - Height of the capsule in units.

## void setHeight ( float height )

Sets a height of the capsule.
### Arguments

- *float* **height** - Height of the capsule in units.

## float getHeight ( )

Returns the current height of the capsule.
### Return value

Height of the capsule in units.
## void setRadius ( float radius )

Sets a radius of the capsule.
### Arguments

- *float* **radius** - Radius of the capsule in units.

## float getRadius ( )

Returns the current radius of the capsule.
### Return value

Radius of the capsule in units.
## Math:: Vec3 getBottomCap ( )

Returns the coordinates of the center of the top hemisphere of the capsule.
### Return value

Coordinates of the center of the capsule's top hemisphere.
## Math:: Vec3 getTopCap ( )

Returns the coordinates of the center of the bottom hemisphere of the capsule.
### Return value

Coordinates of the center of the capsule's bottom hemisphere.
