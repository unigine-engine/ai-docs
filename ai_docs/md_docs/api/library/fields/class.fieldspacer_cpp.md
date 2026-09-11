# Unigine.FieldSpacer Class (CPP)

**Header:** #include <UnigineFields.h>

**Inherits from:** Field


This class allows you to create and modify field spacer objects.


### See Also


- *[FieldSpacer](../../../api/library/fields/class.fieldspacer_cpp.md)* class to edit spacer fields by using C++ API
- UnigineScript samples:

  -
  -
  -


## FieldSpacer Class

### Members

## void setAttenuation ( float attenuation )

Sets a new attenuation factor for the Field Spacer.
### Arguments

- *float* **attenuation** - The attenuation factor value. This factor indicates how much geometry is cut off gradually starting from the center of the Field Spacer: If too small a value is provided, 1E-6 will be used instead.

  - By the minimum value of 0, all geometry inside the Field Spacer will be rendered.
  - The higher the value, the less geometry will be rendered inside the Field Spacer.

## float getAttenuation () const

Returns the current attenuation factor for the Field Spacer.
### Return value

Current
attenuation factor value. This factor indicates how much geometry is cut off gradually starting from the center of the Field Spacer:


- By the minimum value of 0, all geometry inside the Field Spacer will be rendered.
- The higher the value, the less geometry will be rendered inside the Field Spacer.


If too small a value is provided, 1E-6 will be used instead.


## void setSize ( const Math:: vec3 & size )

Sets a new size of the Field Spacer. For the cube-shaped field the cube size is set, for the ellipse-shaped field - the radius.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The field spacer size. A [vec3](../../../api/library/math/class.vec3_cpp.md) vector with components representing the sizes along the **X**, **Y** and **Z** axes, in units. If a negative value is provided, 0 will be used instead.

## Math:: vec3 getSize () const

Returns the current size of the Field Spacer. For the cube-shaped field the cube size is set, for the ellipse-shaped field - the radius.
### Return value

Current field spacer size. A [vec3](../../../api/library/math/class.vec3_cpp.md) vector with components representing the sizes along the **X**, **Y** and **Z** axes, in units. If a negative value is provided, 0 will be used instead.
## void setEllipse ( bool ellipse )

Sets a new value indicating if the Field Spacer is of an ellipse or a cube shape.
### Arguments

- *bool* **ellipse** - Set **true** to enable ellipse-shaped Field Spacer; **false** - to disable it.

## bool isEllipse () const

Returns the current value indicating if the Field Spacer is of an ellipse or a cube shape.
### Return value

**true** if ellipse-shaped Field Spacer is enabled ; otherwise **false**.
---

## static FieldSpacerPtr create ( const Math:: vec3 & size )


Creates a new Field Spacer of the specified size:


- If the Field Spacer is of an ellipse shape, its radius values along the axes must be specified.
- Otherwise, dimensions of the cube must be specified.


### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - A size of the Field Spacer along *X*, *Y* and *Z* axes in units.

## static int type ( )

Returns the type of the object.
### Return value

[FieldSpacer](../../../api/library/nodes/class.node_cpp.md#FIELD_SPACER) type identifier.
