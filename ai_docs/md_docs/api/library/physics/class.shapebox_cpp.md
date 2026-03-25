# Unigine::ShapeBox Class (CPP)

**Header:** #include <UniginePhysics.h>

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

---

## static ShapeBoxPtr create ( )

Constructor. Creates a new cylinder with the zero dimensions.
## static ShapeBoxPtr create ( const Math:: vec3 & size )

Constructor. Creates a new box with given dimensions.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Dimensions of the box in units.

## static ShapeBoxPtr create ( const Ptr < Body > & body , const Math:: vec3 & size )

Constructor. Creates a new box with given dimensions and adds it to a given body.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Body](../../../api/library/physics/class.body_cpp.md)> &* **body** - Body, to which the box will belong.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Dimensions of the box in units.

## void setSize ( const Math:: vec3 & size )

Sets box dimensions.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Dimensions of the box in units.

## Math:: vec3 getSize ( )

Returns the current dimensions of the box.
### Return value

Dimensions of the box in units.
