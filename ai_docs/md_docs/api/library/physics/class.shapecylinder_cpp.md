# Unigine::ShapeCylinder Class (CPP)

**Header:** #include <UniginePhysics.h>

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

## void setHeight ( float height )

Sets a new height of the cylinder, in units.
### Arguments

- *float* **height** - The height of the cylinder, in units

## float getHeight () const

Returns the current height of the cylinder, in units.
### Return value

Current height of the cylinder, in units
## void setRadius ( float radius )

Sets a new radius of the cylinder, in units.
### Arguments

- *float* **radius** - The radius of the cylinder, in units

## float getRadius () const

Returns the current radius of the cylinder, in units.
### Return value

Current radius of the cylinder, in units
---

## static ShapeCylinderPtr create ( )

Constructor. Creates a new cylinder with the zero radius and the zero height.
## static ShapeCylinderPtr create ( float radius , float height )

Constructor. Creates a new cylinder with given dimensions.
### Arguments

- *float* **radius** - Radius of the cylinder in units.
- *float* **height** - Height of the cylinder in units.

## static ShapeCylinderPtr create ( const Ptr < Body > & body , float radius , float height )

Constructor. Creates a new cylinder with given dimensions and adds it to a given body.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body** - Body, to which the cylinder will belong.
- *float* **radius** - Radius of the cylinder in units.
- *float* **height** - Height of the cylinder in units.
