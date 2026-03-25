# Unigine.DecalProj Class (CPP)

**Header:** #include <UnigineDecals.h>

**Inherits from:** Decal


This class describes how to create and modify [projected decals](../../../objects/decals/proj/index.md).


### Creating a Projected Decal


The following code illustrates how to create a projected decal, set its parameters and add the node to UnigineEditor.


```cpp
// AppWorldLogic.h

#include <UnigineLogic.h>
#include <UnigineEditor.h>
#include <UnigineDecals.h>

class AppWorldLogic : public Unigine::WorldLogic {

public:
	AppWorldLogic();
	virtual ~AppWorldLogic();

	virtual int init();

	virtual int update();
	virtual int postUpdate();
	virtual int updatePhysics();

	virtual int shutdown();

	virtual int save(const Unigine::StreamPtr &stream);
	virtual int restore(const Unigine::StreamPtr &stream);

private:
	Unigine::DecalProjPtr decal_proj;
};

```


```cpp
// AppWorldLogic.cpp

#include "AppWorldLogic.h";

using namespace Unigine;

int AppWorldLogic::init()
{

	// create an proj decal and setting its radius to 10, fov to 60, aspect to 1.0f, material to "decal_base"
	decal_proj = DecalProj::create();
	decal_proj->setRadius(10.0f);
	decal_proj->setFov(60.0f);
	decal_proj->setAspect(1.0f);

	// set the name and position of the decal
	decal_proj->setName("Proj Decal");
	decal_proj->setWorldPosition(Math::Vec3(0.0f, 0.0f, 5.0f));

	return 1;
}

```


## DecalProj Class

### Members

---

## static DecalProjPtr create ( )

Constructor. Creates a new projected decal with default parameters.
## void setAspect ( float aspect )

Sets the new aspect ratio of the decal, in units.
### Arguments

- *float* **aspect** - The aspect ratio of the decal, in units. If a negative value is provided, 0 will be used instead.

## float getAspect ( ) const

Returns the current aspect ratio of the decal.
### Return value

The aspect ratio of the decal, in units.
## void setFov ( float fov )

Sets a new field of view of the decal's projector.
### Arguments

- *float* **fov** - A field of view of the decal's projector, in degrees. The provided value will be clamped in the range [1;90].

## float getFov ( ) const

Returns the current field of view of the decal's projector.
### Return value

The field of view of the decal's projector, in degrees.
## Math:: mat4 getProjection ( ) const

Returns the projection matrix.
### Return value

The projection matrix of the decal.
## void setZNear ( float znear )

Sets a distance to the near clipping plane of the decal.
### Arguments

- *float* **znear** - A new distance to the near clipping plane, in units. If a negative value is provided, 0 will be used instead.

## float getZNear ( ) const

Returns the distance to the near clipping plane of the decal.
### Return value

The distance to the near clipping plane, in units.
## static int type ( )

Returns the type of the node.
### Return value

[Decal](../../../api/library/decals/class.decal_cpp.md) type identifier.
