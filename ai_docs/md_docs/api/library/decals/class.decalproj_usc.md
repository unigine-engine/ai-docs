# Unigine.DecalProj Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Decal


This class describes how to create and modify [projected decals](../../../objects/decals/proj/index.md).


### Creating a Projected Decal


The following code illustrates how to create a projected decal, set its parameters and add the node to UnigineEditor.


```cpp
#include <core/unigine.h>

int init() {

	DecalProj decal_proj;

	// create an proj decal and setting its radius to 10, fov to 60, aspect to 1.0f, material to "decal_base"
	decal_proj = new DecalProj();
	decal_proj.setRadius(10.0f);
	decal_proj.setFov(60.0f);
	decal_proj.setAspect(1.0f);

	// set the name and position of the decal
	decal_proj.setName("Proj Decal");
    decal_proj.setWorldPosition(vec3(0.0f, 0.0f, 5.0f));

	return 1;
}

```


## DecalProj Class

### Members

---

## static DecalProj ( )

Constructor. Creates a new projected decal with default parameters.
## void setAspect ( float aspect )

Sets the new aspect ratio of the decal, in units.
### Arguments

- *float* **aspect** - The aspect ratio of the decal, in units.

## float getAspect ( )

Returns the current aspect ratio of the decal.
### Return value

The aspect ratio of the decal, in units.
## void setFov ( float fov )

Sets the new field of view of the decal's projector.
### Arguments

- *float* **fov** - The field of view of the decal's projector, in degrees.

## float getFov ( )

Returns the current field of view of the decal's projector.
### Return value

The field of view of the decal's projector, in degrees.
## mat4 getProjection ( )

Returns the projection matrix.
### Return value

The projection matrix of the decal.
## void setZNear ( float znear )

Sets a distance to the near clipping plane of the decal.
### Arguments

- *float* **znear** - Distance to the near clipping plane, units.

## float getZNear ( )

Returns a distance to the near clipping plane of the decal.
### Return value

Distance to the near clipping plane, units.
## static int type ( )

Returns the type of the node.
### Return value

[Decal](../../../api/library/decals/class.decal_usc.md) type identifier.
