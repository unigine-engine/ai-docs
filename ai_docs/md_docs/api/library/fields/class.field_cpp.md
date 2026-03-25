# Unigine.Field Class (CPP)

**Header:** #include <UnigineFields.h>

**Inherits from:** Node


This class allows you to modify [fields](../../../objects/effects/fields/index.md) masks.


## Field Class

### Members

## void setViewportMask ( int mask )

Sets a new bit mask for rendering the field node into the viewport.
### Arguments

- *int* **mask** - The integer value, each bit of which is used to set a mask.

## int getViewportMask () const

Returns the current bit mask for rendering the field node into the viewport.
### Return value

Current integer value, each bit of which is used to set a mask.
## void setFieldMask ( int mask )

Sets a new mask specifying the area of the Field node to be applied. The object will be influenced by the field if they both have [matching masks](../../../principles/bit_masking/index.md).
### Arguments

- *int* **mask** - The integer value, each bit of which is used to set a mask.

## int getFieldMask () const

Returns the current mask specifying the area of the Field node to be applied. The object will be influenced by the field if they both have [matching masks](../../../principles/bit_masking/index.md).
### Return value

Current integer value, each bit of which is used to set a mask.
