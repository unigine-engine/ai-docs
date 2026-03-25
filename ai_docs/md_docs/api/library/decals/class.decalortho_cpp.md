# Unigine.DecalOrtho Class (CPP)

**Header:** #include <UnigineDecals.h>

**Inherits from:** Decal


This class describes how to create and modify [orthographic decals](../../../objects/decals/ortho/index.md).


### Creating an Orthographic Decal


The following code illustrates how to create an orthographic decal, set its parameters and add the node to UnigineEditor.


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
	Unigine::DecalOrthoPtr decal_ortho;
};

```


```cpp
// AppWorldLogic.cpp

#include "AppWorldLogic.h";

using namespace Unigine;

int AppWorldLogic::init()
{

	// create an ortho decal and setting its radius to 10, width and height to 2
	decal_ortho = DecalOrtho::create();
	decal_ortho->setRadius(10.0f);
	decal_ortho->setWidth(2.0f);
	decal_ortho->setHeight(2.0f);

	// set the name and position of the decal
	decal_ortho->setName("Ortho Decal");
	decal_ortho->setWorldPosition(Math::Vec3(0.0f, 0.0f, 5.0f));

	return 1;
}

```


## DecalOrtho Class

### Members

---

## static DecalOrthoPtr create ( )

Constructor. Creates a new orthographic decal with default parameters.
## void setHeight ( float height )

Sets a new length of the projection box along the Y axis.
### Arguments

- *float* **height** - The length of the projection box along the Y axis, in units. If a negative value is provided, 0 will be used instead.

## float getHeight ( ) const

Returns the current length of the projection box along the Y axis.
### Return value

The length of the projection box along the Y axis, in units.
## Math:: mat4 getProjection ( ) const

Returns the projection matrix.
### Return value

The projection matrix of the decal.
## void setWidth ( float width )

Sets the new length of the projection box along the X axis.
### Arguments

- *float* **width** - The length of the projection box along the X axis, in units. If a negative value is provided, 0 will be used instead.

## float getWidth ( ) const

Returns the current length of the projection box along the X axis, in units.
### Return value

The length of the projection box along the X axis, in units.
## void setZNear ( float znear )

Sets a new value of the near clipping plane.
### Arguments

- *float* **znear** - A value of the near clipping plane, ranging from 0 to 1. If a negative value is provided, 0 will be used instead.

## float getZNear ( ) const

Returns the value of the near clipping plane.
### Return value

The value of the near clipping plane, ranging from 0 to 1.
## static int type ( )

Returns a type identifier.
### Return value

Type identifier.
