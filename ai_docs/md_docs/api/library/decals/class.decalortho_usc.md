# Unigine.DecalOrtho Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Decal


This class describes how to create and modify [orthographic decals](../../../objects/decals/ortho/index.md).


### Creating an Orthographic Decal


The following code illustrates how to create an orthographic decal, set its parameters and add the node to UnigineEditor.


```cpp
#include <core/unigine.h>

int init() {

	DecalOrtho decal_ortho;

	// creating an ortho decal and setting its radius to 10, width and height to 2
	decal_ortho = new DecalOrtho();
	decal_ortho.setRadius(10.0f);
	decal_ortho.setWidth(2.0f);
	decal_ortho.setHeight(2.0f);

	// set the name and position of the decal
	decal_ortho.setName("Ortho Decal");
    decal_ortho.setWorldPosition(vec3(0.0f, 0.0f, 5.0f));

	return 1;
}

```


## DecalOrtho Class

### Members

---

## static DecalOrtho ( )

Constructor. Creates a new orthographic decal with default parameters.
## void setHeight ( float height )

Sets a new length of the projection box along the Y axis.
### Arguments

- *float* **height** - The length of the projection box along the Y axis, in units. If a negative value is provided, 0 will be used instead.

## float getHeight ( )

Returns the current length of the projection box along the Y axis.
### Return value

The length of the projection box along the Y axis, in units.
## mat4 getProjection ( )

Returns the projection matrix.
### Return value

The projection matrix of the decal.
## void setWidth ( float width )

Sets the new length of the projection box along the X axis.
### Arguments

- *float* **width** - The length of the projection box along the *X* axis, in units.

## float getWidth ( )

Returns the current length of the projection box along the X axis, in units.
### Return value

The length of the projection box along the X axis, in units.
## void setZNear ( float znear )

Sets the new value of the near clipping plane.
### Arguments

- *float* **znear** - The value of the near clipping plane, ranging from **0** to **1**.

## float getZNear ( )

Returns the value of the near clipping plane.
### Return value

The value of the near clipping plane, ranging from 0 to 1.
## static int type ( )

Returns a type identifier.
### Return value

Type identifier.
