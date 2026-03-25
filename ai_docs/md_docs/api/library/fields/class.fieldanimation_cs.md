# Unigine.FieldAnimation Class (CS)

**Inherits from:** Field


This class allows you to create and modify [field animation](../../../objects/effects/fields/field_animation/index.md) objects.


### See also


- UnigineScript samples:

  -
  -


## FieldAnimation Class

### Properties

## vec3 Wind

The wind coefficient values that define the wind direction inside the animation field.
## float AnimationScale

The animation scale value that affects the vegetation swaying speed.
## float Leaf

The leaf animation coefficient value.
## float Stem

The stem animation coefficient value.
## float Attenuation

The attenuation coefficient for the field animation. This value indicates how much animation attenuates starting from the center of the animation field to its edges:
- By the minimum value of 0, no animation will be visible.
- The higher the value, the more intensive animation will be at the edges of the animation field.


## vec3 Size

The animation field size. For the cube-shaped field the cube size is set, for the ellipse-shaped field - the radius.
## bool Ellipse

The value indicating if the Field Animation is of an ellipse or a cube shape.
### Members

---

## FieldAnimation ( vec3 size )

Creates a new Field Animation node of the specified size:
- If the Field Animation is of an ellipse shape, its radius values along the axes must be specified.
- Otherwise, dimensions of the cube must be specified.


### Arguments

- *vec3* **size** - A size of the Field Animation along X, Y and Z axes in units.

## static int type ( )

Returns the type of the object.
### Return value

[FieldAnimation](../../../api/library/nodes/class.node_cs.md#FIELD_ANIMATION) type identifier.
