# Unigine.FieldAnimation Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Field


This class allows you to create and modify [field animation](../../../objects/effects/fields/field_animation/index.md) objects.


### See also


- UnigineScript samples:

  -
  -


## FieldAnimation Class

### Members

## void setWind ( vec3 wind )

Sets a new wind coefficient values that define the wind direction inside the animation field.
### Arguments

- *vec3* **wind** - The wind coefficient values along the X, Y and Z directions.

## vec3 getWind () const

Returns the current wind coefficient values that define the wind direction inside the animation field.
### Return value

Current wind coefficient values along the X, Y and Z directions.
## void setAnimationScale ( float scale )

Sets a new animation scale value that affects the vegetation swaying speed.
### Arguments

- *float* **scale** - The vegetation swaying speed value.

## float getAnimationScale () const

Returns the current animation scale value that affects the vegetation swaying speed.
### Return value

Current vegetation swaying speed value.
## void setLeaf ( float leaf )

Sets a new leaf animation coefficient value.
### Arguments

- *float* **leaf** - The leaf animation coefficient value. If a negative value is provided, 0 will be used instead.

## float getLeaf () const

Returns the current leaf animation coefficient value.
### Return value

Current leaf animation coefficient value. If a negative value is provided, 0 will be used instead.
## void setStem ( float stem )

Sets a new stem animation coefficient value.
### Arguments

- *float* **stem** - The stem animation coefficient value. If a negative value is provided, 0 will be used instead.

## float getStem () const

Returns the current stem animation coefficient value.
### Return value

Current stem animation coefficient value. If a negative value is provided, 0 will be used instead.
## void setAttenuation ( float attenuation )

Sets a new attenuation coefficient for the field animation. This value indicates how much animation attenuates starting from the center of the animation field to its edges:
- By the minimum value of 0, no animation will be visible.
- The higher the value, the more intensive animation will be at the edges of the animation field.


### Arguments

- *float* **attenuation** - The attenuation coefficient value. If too small a value is provided, 1E-6 will be used instead.

## float getAttenuation () const

Returns the current attenuation coefficient for the field animation. This value indicates how much animation attenuates starting from the center of the animation field to its edges:
- By the minimum value of 0, no animation will be visible.
- The higher the value, the more intensive animation will be at the edges of the animation field.


### Return value

Current attenuation coefficient value. If too small a value is provided, 1E-6 will be used instead.
## void setSize ( vec3 size )

Sets a new animation field size. For the cube-shaped field the cube size is set, for the ellipse-shaped field - the radius.
### Arguments

- *vec3* **size** - The animation field size along the X, Y and Z axes in units.

## vec3 getSize () const

Returns the current animation field size. For the cube-shaped field the cube size is set, for the ellipse-shaped field - the radius.
### Return value

Current animation field size along the X, Y and Z axes in units.
## void setEllipse ( int ellipse )

Sets a new value indicating if the Field Animation is of an ellipse or a cube shape.
### Arguments

- *int* **ellipse** - The ellipse-shaped Field Animation

## int isEllipse () const

Returns the current value indicating if the Field Animation is of an ellipse or a cube shape.
### Return value

Current ellipse-shaped Field Animation
---

## static FieldAnimation ( vec3 size )

Creates a new Field Animation node of the specified size:
- If the Field Animation is of an ellipse shape, its radius values along the axes must be specified.
- Otherwise, dimensions of the cube must be specified.


### Arguments

- *vec3* **size** - A size of the Field Animation along X, Y and Z axes in units.

## static int type ( )

Returns the type of the object.
### Return value

[FieldAnimation](../../../api/library/nodes/class.node_usc.md#FIELD_ANIMATION) type identifier.
