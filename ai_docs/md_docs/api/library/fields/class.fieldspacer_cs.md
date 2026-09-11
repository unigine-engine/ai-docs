# Unigine.FieldSpacer Class (CS)

**Inherits from:** Field


This class allows you to create and modify field spacer objects.


### See Also


- *[FieldSpacer](../../../api/library/fields/class.fieldspacer_cs.md)* class to edit spacer fields by using C++ API
- UnigineScript samples:

  -
  -
  -


## FieldSpacer Class

### Properties

## float Attenuation

The attenuation factor for the Field Spacer.
## vec3 Size

The size of the Field Spacer. For the cube-shaped field the cube size is set, for the ellipse-shaped field - the radius.
## bool Ellipse

The value indicating if the Field Spacer is of an ellipse or a cube shape.
### Members

---

## FieldSpacer ( vec3 size )


Creates a new Field Spacer of the specified size:


- If the Field Spacer is of an ellipse shape, its radius values along the axes must be specified.
- Otherwise, dimensions of the cube must be specified.


### Arguments

- *vec3* **size** - A size of the Field Spacer along *X*, *Y* and *Z* axes in units.

## static int type ( )

Returns the type of the object.
### Return value

[FieldSpacer](../../../api/library/nodes/class.node_cs.md#FIELD_SPACER) type identifier.
