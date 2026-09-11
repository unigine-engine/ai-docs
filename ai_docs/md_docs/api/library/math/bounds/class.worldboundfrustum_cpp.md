# Unigine::WorldBoundFrustum Struct (CPP)

**Header:** #include <UnigineMathLibBounds.h>


This structure serves to construct the bounding frustum in double precision coordinates.


*WorldBoundFrustum* enables you to check:


- if the specified bound volume (box, sphere, or other frustum) gets inside the frustum (even partially) - use *[inside( bound )](#inside_WorldBoundSphere_int)* methods for this purpose.
- if the specified bound volume (box, sphere, or other frustum) is inside the frustum completely - use *[insideAll( bound )](#insideAll_WorldBoundSphere_int)* methods for this purpose.
- if certain points of your object are inside the frustum (may be necessary in case **more accurate results** are required than the ones obtained using the two methods above) - here you should use *[inside( point )](#inside_dvec3_int)* methods and check all points of interest. ![](../check_points.jpg)


> **Notice:** Make sure that you use proper **aspect-corrected projection** for the frustum when necessary. See the picture in the spoiler below: *red* - default projection matrix, *green* - aspect-corrected projection matrix.


<details>
<summary>Aspect Correction for Frustum's Projection | close</summary>

![](../boundfrustum1.jpg)
![](../boundfrustum2.jpg)

</details>


### Usage Example


For example you can use a *WorldBoundFrustum* in order to check whether a node is inside the viewing frustum of a camera. Check the component below.


<details>
<summary>FrustumChecker.h | close</summary>

```cpp
#pragma once
#include <UnigineComponentSystem.h>
class FrustumChecker :
	public Unigine::ComponentBase
{
public:
	COMPONENT_DEFINE(FrustumChecker, Unigine::ComponentBase);
	COMPONENT_UPDATE(update);

private:
	void update();
};

```

</details>


<details>
<summary>FrustumChecker.cpp | close</summary>

```cpp
#include "FrustumChecker.h"
#include "UnigineGame.h"
#include "UnigineMathLibBounds.h"
#include "UnigineVisualizer.h"
REGISTER_COMPONENT(FrustumChecker);

using namespace Unigine;

void FrustumChecker::update()
{
	// getting the current camera
	Unigine::CameraPtr camera = Game::getPlayer()->getCamera();

	// getting the main window of the application
	Unigine::EngineWindowPtr main_window = WindowManager::getMainWindow();
	if (!main_window) {
		Engine::get()->quit();
		return;
	}

	// calculating the current aspect ratio to obtain proper aspect-corrected projection matrix
	// default projection matrix does not take aspect ratio into account
	Unigine::Math::ivec2 main_size = WindowManager::getMainWindow()->getSize();
	float aspect = float(main_size.y) / main_size.x;
	Unigine::Math::mat4 proj = camera->getAspectCorrectedProjection(aspect);

	// getting model-view matrix of the camera
	Unigine::Math::Mat4 model_view = camera->getModelview();
	Unigine::Math::WorldBoundFrustum bfrustum(proj, model_view);

	// checking if the node's bound gets inside the viewing frustum of the camera
	if (bfrustum.inside(node->getWorldBoundBox())) {
		Log::message("Node's bound is visible inside the frustum.");

		// checking whether the bound is completely or partially inside the frustum
		Log::message(bfrustum.insideAll(node->getWorldBoundBox()) ? " COMPLETELY!\n": " PARTIALLY!\n");

		// checking whether a certain point of the object (WorldPosition here) is inside the frustum
		Log::message(bfrustum.inside(node->getWorldPosition()) ? "(The point is INSIDE)\n" : "(The point is OUTSIDE)\n");
	}
	else
		Log::message("Node's bound is outside the frustum.\n");

	// displaying node's BoundBox, the Bound Frustum, and a point using the Visualizer
	Visualizer::renderFrustum(proj, Math::inverse(model_view), Math::vec4(1.0f, 0.0f, 0.0f, 1.0f));
	Visualizer::renderBoundBox(node->getBoundBox(), node->getTransform(), Math::vec4(0.0f, 1.0f, 0.0f, 1.0f));
	Visualizer::renderSphere(0.01f, Math::translate(node->getWorldPosition()), Math::vec4(1.0f, 0.0f, 0.0f, 1.0f));
}

```

</details>


## WorldBoundFrustum Class

### Members

---

## static WorldBoundFrustumPtr create ( )

Default constructor.
## WorldBoundFrustum ( const Math:: mat4 & projection , const Math:: Mat4 & modelview )

Constructor. Initializes the bounding frustum by given matrices.
### Arguments

- *const  Math::[mat4](../../../../api/library/math/class.mat4_cpp.md) &* **projection** - A projection matrix.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **modelview** - A modelview matrix.

## WorldBoundFrustum ( const WorldBoundFrustum & bf )

Constructor. Initializes by given bounding frustum.
### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - The bounding frustum.

## WorldBoundFrustum ( const BoundFrustum & bf )

Constructor. Initializes by given bounding frustum.
### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - The bounding frustum.

## WorldBoundFrustum ( const WorldBoundFrustum & bf , const Math:: Mat4 & itransform )

Constructor. Initializes by given bounding frustum and transformation matrix.
### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - The bounding frustum.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **itransform** - The inverse transformation matrix.

## WorldBoundFrustum ( const BoundFrustum & bf , const Math:: Mat4 & itransform )

Constructor. Initializes by given bounding frustum and transformation matrix.
### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - The bounding frustum.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **itransform** - The inverse transformation matrix.

## WorldBoundFrustum & operator= ( const WorldBoundFrustum & bf )

Assignment operator.
### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - The bounding frustum.

### Return value

Bounding frustum.
## void clear ( )

Clears the bounding frustum.
## void set ( const Math:: mat4 & projection , const Math:: Mat4 & modelview )

Sets the bounding frustum by given matrices.
### Arguments

- *const  Math::[mat4](../../../../api/library/math/class.mat4_cpp.md) &* **projection** - A projection matrix.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **modelview** - A modelview matrix.

## void set ( const WorldBoundFrustum & bf )

Sets the bounding frustum by given bounding frustum.
### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - The bounding frustum.

## void set ( const WorldBoundFrustum & bf , const Math:: Mat4 & itransform )

Sets the bounding frustum by given bounding frustum and transformation matrix.
### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - The bounding frustum.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **itransform** - The inverse transformation matrix.

## void set ( const BoundFrustum & bf )

Sets the bounding frustum by given bounding frustum.
### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - The bounding frustum.

## void set ( const BoundFrustum & bf , const Math:: Mat4 & itransform )

Sets the bounding frustum by given bounding frustum and transformation matrix.
### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - The bounding frustum.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **itransform** - The inverse transformation matrix.

## bool isValid ( ) const

Checks the bounding frustum status.
### Return value

true if the bounding frustum is valid, otherwise false.
## void setITransform ( const Math:: dmat4 & itransform )

Sets the current transformation matrix by an inverse transformation matrix.
### Arguments

- *const  Math::[dmat4](../../../../api/library/math/class.dmat4_cpp.md) &* **itransform** - Inverse transformation matrix.

## void setTransform ( const Math:: dmat4& transform )

Sets the current transformation matrix by the specified source transformation matrix.
### Arguments

- *const  Math:: dmat4&* **transform** - Source transformation matrix.

## int compare ( const WorldBoundFrustum & bf ) const

Compares the current bounding frustum with the given one.
### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - Bounding frustum.

### Return value

**true** if the current bounding frustum is equal to the given one; otherwise, **false**.
## int operator== ( const WorldBoundFrustum & bf ) const

Bounding frustum equal comparison operator.
### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - The bounding frustum to compare with.

### Return value

**true** if the current bounding frustum is equal to the given one; otherwise, **false**.
## int operator!= ( const WorldBoundFrustum & bf ) const

Bounding frustum not equal comparison operator.
### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - The bounding frustum to compare with.

### Return value

**true** if the current bounding frustum is not equal to the given one; otherwise, **false**.
## int inside ( const Math:: Vec3 & point ) const

Checks if the point is inside the bounding frustum.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - The coordinates of the point.

### Return value

**1** if the point is inside the bounding frustum; otherwise, **0**.
## int inside ( const Math:: Vec3 & point , Math::Scalar radius ) const

Checks if the sphere is inside the bounding frustum.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - The coordinates of the center of the sphere.
- *Math::Scalar* **radius** - The sphere radius.

### Return value

**1** if the sphere is inside the bounding frustum; otherwise, **0**.
## int inside ( const Math:: Vec3 & min , const Math:: Vec3 & max ) const

Checks if the box is inside the bounding frustum.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **min** - The box minimum coordinate.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **max** - The box maximum coordinate.

### Return value

**1** if the box is inside the bounding frustum; otherwise, **0**.
## int inside ( const Math:: Vec3 * points , int num ) const

Checks if a set of points is inside the bounding frustum.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - Vector of points.
- *int* **num** - Number of points.

### Return value

**1** if the points are inside the bounding frustum; otherwise, **0**.
## int inside ( const WorldBoundSphere & bs ) const

Checks if the bounding sphere is inside the bounding frustum.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**1** if the bounding sphere is inside the bounding frustum; otherwise, **0**.
## int inside ( const WorldBoundBox & bb ) const

Checks if the bounding box is inside the bounding frustum.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**1** if the bounding box is inside the bounding frustum; otherwise, **0**.
## int inside ( const WorldBoundFrustum & bb ) const

Checks if the bounding frustum specified in the argument is inside the bounding frustum.
### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bb** - The bounding frustum.

### Return value

**1** if the specified bounding frustum is inside the bounding frustum; otherwise, **0**.
## int insideFast ( const Math:: Vec3 & point ) const

Performs a fast check if the point is inside the bounding frustum.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Point.

### Return value

**1** if the point is inside the bounding frustum; otherwise, **0**.
## int insideFast ( const Math:: Vec3 & point , Math::Scalar radius ) const

Performs a fast check if the sphere is inside the bounding frustum.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Center point.
- *Math::Scalar* **radius** - Radius.

### Return value

**1** if the sphere is inside the bounding frustum; otherwise, **0**.
## int insideFast ( const Math:: Vec3 & min , const Math:: Vec3 & max ) const

Performs a fast check if the box is inside the bounding frustum.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **min** - Minimum point.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **max** - Maximum point.

### Return value

**1** if the box is inside the bounding frustum; otherwise, **0**.
## int insideFast ( const Math:: Vec3 * points , int num_points ) const

Performs a fast check if the set of points is inside the bounding frustum.
### Arguments

- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - Vector of points.
- *int* **num_points** - Number of points.

### Return value

**1** if the point is inside the bounding frustum; otherwise, **0**.
## int insideValid ( const WorldBoundSphere & bs ) const


Checks if the given bounding sphere is inside the bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**1** if the given bounding sphere is inside the bounding frustum; otherwise, **0**.
## int insideValid ( const WorldBoundBox & bb ) const


Checks if the given bounding box is inside the bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**1** if the given bounding box is inside the bounding frustum; otherwise, **0**.
## int insideValid ( const WorldBoundFrustum & bb ) const


Checks if the given bounding frustum is inside the bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bb** - The bounding frustum.

### Return value

**1** if the given bounding frustum is inside the bounding frustum; otherwise, **0**.
## int insideValidFast ( const WorldBoundSphere & bs ) const


Performs a fast check if the given bounding sphere is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**1** if the given bounding sphere is inside the bounding frustum; otherwise, **0**.
## int insideValidFast ( const WorldBoundBox & bb ) const


Performs a fast check if the given bounding box is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**1** if the given bounding box is inside the bounding frustum; otherwise, **0**.
## int insideValidFast ( const WorldBoundFrustum & bb ) const


Performs a fast check if the given bounding frustum is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bb** - The bounding frustum.

### Return value

**1** if the given bounding frustum is inside the bounding frustum; otherwise, **0**.
## int insideAll ( const WorldBoundBox & bb ) const

Checks if the whole given bounding box is inside the current bounding frustum.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**1** if the whole box is inside the bounding frustum; otherwise, **0**.
## int insideAll ( const WorldBoundSphere & bs ) const

Checks if the whole given bounding sphere is inside the current bounding frustum.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**1** if the whole sphere is inside the bounding frustum; otherwise, **0**.
## int insideAll ( const WorldBoundFrustum & bs ) const

Checks if the whole given bounding frustum is inside the current bounding frustum.
### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bs** - The bounding frustum.

### Return value

**1** if the given frustum is inside the bounding frustum; otherwise, **0**.
## int insideAllValid ( const WorldBoundSphere & bs ) const


Checks if the whole given bounding sphere is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**1** if the given bounding sphere is inside the bounding frustum; otherwise, **0**.
## int insideAllValid ( const WorldBoundBox & bb ) const


Checks if the whole given bounding box is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**1** if the given bounding box is inside the bounding frustum; otherwise, **0**.
## int insideAllValid ( const WorldBoundFrustum & bb ) const


Checks if the whole given bounding frustum is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bb** - The bounding frustum.

### Return value

**1** if the given bounding frustum is inside the bounding frustum; otherwise, **0**.
## int insideAllValidFast ( const WorldBoundSphere & bs ) const


Performs a fast check if the whole given bounding sphere is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**1** if the given bounding sphere is inside the bounding frustum; otherwise, **0**.
## int insideAllValidFast ( const WorldBoundBox & bb ) const


Performs a fast check if the whole given bounding box is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**1** if the given bounding box is inside the bounding frustum; otherwise, **0**.
## int insideAllValidFast ( const WorldBoundFrustum & bb ) const


Performs a fast check if the whole given bounding frustum is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bb** - The bounding frustum.

### Return value

**1** if the given bounding frustum is inside the bounding frustum; otherwise, **0**.
## bool insidePlanes ( const WorldBoundSphere & bs ) const

Checks if the given bounding sphere is inside the volume defined by the planes of the current bounding frustum.
### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - Bounding sphere.

### Return value

**true** if the given bounding sphere is inside the volume; otherwise, **false**.
## bool insidePlanes ( const WorldBoundBox & bb ) const

Checks if the given bounding box is inside the volume defined by the planes of the current bounding frustum.
### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - Bounding box.

### Return value

**true** if the given bounding box is inside the volume; otherwise, **false**.
## bool insidePlanes ( const WorldBoundFrustum & bf ) const

Checks if the given bounding frustum is inside the volume defined by the planes of the current bounding frustum.
### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - Bounding frustum.

### Return value

**true** if the given bounding frustum is inside the volume; otherwise, **false**.
## bool insidePlanesValid ( const WorldBoundSphere & bs ) const


Checks if the given bounding sphere is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**true** if the given bounding sphere is inside the volume; otherwise, **false**.
## bool insidePlanesValid ( const WorldBoundBox & bb ) const


Checks if the given bounding box is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**true** if the given bounding box is inside the volume; otherwise, **false**.
## bool insidePlanesValid ( const WorldBoundFrustum & bf ) const


Checks if the given bounding frustum is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - The bounding frustum.

### Return value

**true** if the given bounding frustum is inside the volume; otherwise, **false**.
## bool insidePlanesValidFast ( const WorldBoundSphere & bs ) const


Performs a fast check if the given bounding sphere is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**true** if the given bounding sphere is inside the volume; otherwise, **false**.
## bool insidePlanesValidFast ( const WorldBoundBox & bb ) const


Performs a fast check if the given bounding box is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**true** if the given bounding box is inside the volume; otherwise, **false**.
## bool insidePlanesValidFast ( const WorldBoundFrustum & bf ) const


Performs a fast check if the given bounding frustum is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - The bounding frustum.

### Return value

**true** if the given bounding frustum is inside the volume; otherwise, **false**.
## int insideShadowValid ( const WorldBoundSphere & object , const Math:: Vec3 & direction ) const


Checks if the given bounding sphere is inside the shadow of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **object** - Bounding sphere.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **direction** - The direction vector.

### Return value

**1** if the given bounding sphere is inside the shadow; otherwise, **0**.
## bool insideShadowValid ( const WorldBoundSphere & object , const WorldBoundSphere & light , const Math:: Vec3 & offset ) const


Checks if the given bounding sphere is inside the shadow of the current bounding frustum and outside the bounding sphere of a light source.


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **object** - Bounding sphere.
- *const [WorldBoundSphere](../../../../api/library/math/bounds/class.worldboundsphere_cpp.md) &* **light** - The bounding sphere of the light source.
- *const  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) &* **offset** - The offset vector.

### Return value

**true** if the given bounding sphere is inside the shadow and outside the given light source bounding sphere; otherwise, **false**.
