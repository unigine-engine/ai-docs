# Unigine.FieldSpacer Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Field


This class allows you to create and modify field spacer objects.


### See Also


- *[FieldSpacer](../../../api/library/fields/class.fieldspacer_usc.md)* class to edit spacer fields by using C++ API
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


## void setSize ( vec3 size )

Sets a new size of the Field Spacer. For the cube-shaped field the cube size is set, for the ellipse-shaped field - the radius.
### Arguments

- *vec3* **size** - The field spacer size. A [vec3](../../../api/library/math/class.vec3_usc.md) vector with components representing the sizes along the **X**, **Y** and **Z** axes, in units. If a negative value is provided, 0 will be used instead.

## vec3 getSize () const

Returns the current size of the Field Spacer. For the cube-shaped field the cube size is set, for the ellipse-shaped field - the radius.
### Return value

Current field spacer size. A [vec3](../../../api/library/math/class.vec3_usc.md) vector with components representing the sizes along the **X**, **Y** and **Z** axes, in units. If a negative value is provided, 0 will be used instead.
## void setEllipse ( int ellipse )

Sets a new value indicating if the Field Spacer is of an ellipse or a cube shape.
### Arguments

- *int* **ellipse** - The ellipse-shaped Field Spacer

## int isEllipse () const

Returns the current value indicating if the Field Spacer is of an ellipse or a cube shape.
### Return value

Current ellipse-shaped Field Spacer
---

## static FieldSpacer ( vec3 size )


Creates a new Field Spacer of the specified size:


- If the Field Spacer is of an ellipse shape, its radius values along the axes must be specified.
- Otherwise, dimensions of the cube must be specified.


### Arguments

- *vec3* **size** - A size of the Field Spacer along *X*, *Y* and *Z* axes in units.

## static int type ( )

Returns the type of the object.
### Return value

[FieldSpacer](../../../api/library/nodes/class.node_usc.md#FIELD_SPACER) type identifier.
