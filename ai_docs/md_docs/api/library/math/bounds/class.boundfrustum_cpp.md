# Unigine::BoundFrustum Struct (CPP)

**Header:** #include <UnigineMathLibBounds.h>


This structure serves to construct the bounding frustum in single precision coordinates.


> **Notice:** Instances of this structure are deleted automatically, when necessary.


In case of double precision coordinates, the bounding frustum should be constructed by using the **[WorldBoundFrustum](../../../../api/library/math/bounds/class.worldboundfrustum_cpp.md)** structure.  It includes the same functions as the *BoundFrustum* structure, but its functions deal with the double precision coordinates.


> **Notice:** To support both single and double precision builds, you can use the *WorldBoundFrustum* structure only. The engine will automatically substitute it with the *BoundFrustum*, if required.


*BoundFrustum* enables you to check:


- if the specified bound volume (box, sphere, or other frustum) gets inside the frustum (even partially) - use *[inside( bound )](#inside_const_BoundSphere_ref_bool)* methods for this purpose.
- if the specified bound volume (box, sphere, or other frustum) is inside the frustum completely - use *[insideAll( bound )](#insideAll_const_BoundSphere_ref_bool)* methods for this purpose.
- if certain points of your object are inside the frustum (may be necessary in case **more accurate results** are required than the ones obtained using the two methods above) - here you should use *[inside( point )](#inside_const_vec3_ref_bool)* methods and check all points of interest. ![](../check_points.jpg)


> **Notice:** Make sure that you use proper **aspect-corrected projection** for the frustum when necessary. See the picture in the spoiler below: *red* - default projection matrix, *green* - aspect-corrected projection matrix.


<details>
<summary>Aspect Correction for Frustum's Projection | close</summary>

![](../boundfrustum1.jpg)
![](../boundfrustum2.jpg)

</details>


### Usage Example


For example you can use a *BoundFrustum* in order to check whether a node is inside the viewing frustum of a camera. Check the component below.


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
	Unigine::Math::mat4 model_view = camera->getModelview();
	Unigine::Math::BoundFrustum bfrustum(proj, model_view);

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


## BoundFrustum Class

### Members

---

## BoundFrustum ( )

Constructor. Creates an empty bounding frustum.
## static BoundFrustumPtr create ( const mat4& projection , const mat4& modelview )

Initialization by the projection and modelview matrices.
### Arguments

- *const mat4&* **projection** - Projection matrix.
- *const mat4&* **modelview** - Modelview matrix.

## BoundFrustum ( const BoundFrustum & bf )

Initialization by the bounding frustum.
### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - The bounding frustum.

## BoundFrustum ( const BoundFrustum& bf , const mat4& itransform )

Initialization by the bounding frustum and transformation matrix.
### Arguments

- *const BoundFrustum&* **bf** - The bounding frustum.
- *const mat4&* **itransform** - The inverse transformation matrix.

## BoundFrustum & operator= ( const BoundFrustum & bf )

Assignment operator.
### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - The bounding frustum.

### Return value

Bounding frustum.
## void clear ( )

Clears the bounding frustum.
## void set ( const Math:: mat4 & proj )

Sets the bounding frustum by the specified projection matrix.
### Arguments

- *const  Math::[mat4](../../../../api/library/math/class.mat4_cpp.md) &* **proj** - Projection matrix.

## void set ( const Math:: mat4 & projection , const Math:: mat4 & modelview )

Sets the bounding frustum by matrices.
### Arguments

- *const  Math::[mat4](../../../../api/library/math/class.mat4_cpp.md) &* **projection** - Projection matrix.
- *const  Math::[mat4](../../../../api/library/math/class.mat4_cpp.md) &* **modelview** - Modelview matrix.

## void set ( const BoundFrustum & bf )

Sets the bounding frustum by the bounding frustum.
### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - The bounding frustum.

## void set ( const BoundFrustum & bf , const Math:: mat4 & itransform )

Sets the bounding frustum by the bounding frustum and transformation matrix.
### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - The bounding frustum.
- *const  Math::[mat4](../../../../api/library/math/class.mat4_cpp.md) &* **itransform** - The inverse transformation matrix.

## void setTransform ( const mat4& transform )

Sets the current transformation matrix by the specified source transformation matrix.
### Arguments

- *const mat4&* **transform** - Source transformation matrix.

## void setTransform ( const dmat4& transform )

Sets the current transformation matrix by the specified source transformation matrix.
### Arguments

- *const dmat4&* **transform** - Source transformation matrix.

## void setITransform ( const Math:: mat4 & itransform )

Sets the current transformation matrix by an inverse transformation matrix.
### Arguments

- *const  Math::[mat4](../../../../api/library/math/class.mat4_cpp.md) &* **itransform** - Inverse transformation matrix.

## void setITransform ( const Math:: dmat4 & itransform )

Sets the current transformation matrix by an inverse transformation matrix.
### Arguments

- *const  Math::[dmat4](../../../../api/library/math/class.dmat4_cpp.md) &* **itransform** - Inverse transformation matrix.

## int compare ( const BoundFrustum & bf ) const

Compares the current bounding frustum with the given one.
### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - Bounding frustum.

### Return value

**true** if the current bounding frustum is equal to the given one; otherwise, **false**.
## int operator== ( const BoundFrustum & bf ) const

Bounding frustum equal comparison operator.
### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - The bounding frustum to compare with.

### Return value

**true** if the current bounding frustum is equal to the given one; otherwise, **false**.
## int operator!= ( const BoundFrustum & bf ) const

Bounding frustum not equal comparison operator.
### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - The bounding frustum to compare with.

### Return value

**true** if the current bounding frustum is not equal to the given one; otherwise, **false**.
## bool inside ( const Math:: vec3 & point ) const

Checks if the point is inside the bounding frustum.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - The coordinates of the point.

### Return value

**true** if the point is inside the bounding frustum; otherwise, **false**.
## bool inside ( const Math:: vec3 & point , float radius ) const

Checks if the sphere is inside the bounding frustum.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - The coordinates of the center of the sphere.
- *float* **radius** - The sphere radius.

### Return value

**true** if the sphere is inside the bounding frustum; otherwise, **false**.
## bool inside ( const Math:: vec3 & min , const Math:: vec3 & max ) const

Checks if the box is inside the bounding frustum.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **min** - The box minimum coordinate.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **max** - The box maximum coordinate.

### Return value

**true** if the box is inside the bounding frustum; otherwise, **false**.
## bool inside ( const Math:: vec3 * points , int num ) const

Checks if a set of points is inside the bounding frustum.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - Vector of points.
- *int* **num** - Number of points.

### Return value

**true** if the points are inside the bounding frustum; otherwise, **false**.
## bool inside ( const BoundSphere & bs ) const

Checks if the bounding sphere is inside the bounding frustum.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.

### Return value

**true** if the bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool inside ( const BoundBox & bb ) const

Checks if the bounding box is inside the bounding frustum.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

### Return value

**true** if the bounding box is inside the bounding frustum; otherwise, **false**.
## bool inside ( const BoundFrustum & bf ) const

Checks if the specified bounding frustum is inside the current bounding frustum.
### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - Bounding frustum.

### Return value

**true** if the specified bounding frustum is inside the bounding frustum; otherwise, **false**.
## bool insideFast ( const Math:: vec3 & point ) const

Performs a fast check if the point is inside the bounding frustum.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Point.

### Return value

**true** if the point is inside the bounding frustum; otherwise, **false**.
## bool insideFast ( const Math:: vec3 & point , float radius ) const

Performs a fast check if the sphere is inside the bounding frustum.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **point** - Center point.
- *float* **radius** - Radius.

### Return value

**true** if the sphere is inside the bounding frustum; otherwise, **false**.
## bool insideFast ( const Math:: vec3 & min , const Math:: vec3 & max ) const

Performs a fast check if the box is inside the bounding frustum.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **min** - Minimum point.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **max** - Maximum point.

### Return value

**true** if the box is inside the bounding frustum; otherwise, **false**.
## bool insideFast ( const Math:: vec3 * points , int num ) const

Performs a fast check if the set of points is inside the bounding frustum.
### Arguments

- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) ** **points** - Vector of points.
- *int* **num** - Number of points.

### Return value

**true** if the point is inside the bounding frustum; otherwise, **false**.
## bool insideValid ( const BoundSphere & bs ) const


Checks if the given bounding sphere is inside the bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**true** if the given bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool insideValid ( const BoundBox & bb ) const


Checks if the given bounding box is inside the bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**true** if the given bounding box is inside the bounding frustum; otherwise, **false**.
## bool insideValid ( const BoundFrustum & bf ) const


Checks if the given bounding frustum is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - The bounding frustum.

### Return value

**true** if the given bounding frustum is inside the bounding frustum; otherwise, **false**.
## bool insideValidFast ( const BoundSphere & bs ) const


Performs a fast check if the given bounding sphere is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**true** if the given bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool insideValidFast ( const BoundBox & bb ) const


Performs a fast check if the given bounding box is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**true** if the given bounding box is inside the bounding frustum; otherwise, **false**.
## bool insideValidFast ( const BoundFrustum & bf ) const


Performs a fast check if the given bounding frustum is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - The bounding frustum.

### Return value

**true** if the given bounding frustum is inside the bounding frustum; otherwise, **false**.
## bool insideAll ( const BoundBox & bb ) const

Checks if the whole given bounding box is inside the current bounding frustum.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

### Return value

**true** if the whole bounding box is inside the bounding frustum; otherwise, **false**.
## bool insideAll ( const BoundSphere & bs ) const

Checks if the whole given bounding sphere is inside the current bounding frustum.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.

### Return value

**true** if the whole bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool insideAll ( const BoundFrustum & bf ) const

Checks if the whole specified bounding frustum is inside the current bounding frustum.
### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - Bounding frustum.

### Return value

**true** if the whole specified bounding frustum is inside the current bounding frustum; otherwise, **false**.
## bool insideAllValid ( const BoundSphere & bs ) const


Checks if the whole given bounding sphere is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**true** if the given bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool insideAllValid ( const BoundBox & bb ) const


Checks if the whole given bounding box is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**true** if the given bounding box is inside the bounding frustum; otherwise, **false**.
## bool insideAllValid ( const BoundFrustum & bf ) const


Checks if the whole given bounding frustum is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - The bounding frustum.

### Return value

**true** if the given bounding frustum is inside the bounding frustum; otherwise, **false**.
## bool insideAllValidFast ( const BoundSphere & bs ) const


Performs a fast check if the whole given bounding sphere is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**true** if the given bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool insideAllValidFast ( const BoundBox & bb ) const


Performs a fast check if the whole given bounding box is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**true** if the given bounding box is inside the bounding frustum; otherwise, **false**.
## bool insideAllValidFast ( const BoundFrustum & bf ) const


Performs a fast check if the whole given bounding frustum is inside the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - The bounding frustum.

### Return value

**true** if the given bounding frustum is inside the bounding frustum; otherwise, **false**.
## bool insidePlanes ( const BoundSphere & bs ) const

Checks if the given bounding sphere is inside the volume defined by the planes of the current bounding frustum.
### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - Bounding sphere.

### Return value

**true** if the given bounding sphere is inside the volume; otherwise, **false**.
## bool insidePlanes ( const BoundBox & bb ) const

Checks if the given bounding box is inside the volume defined by the planes of the current bounding frustum.
### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - Bounding box.

### Return value

**true** if the given bounding box is inside the volume; otherwise, **false**.
## bool insidePlanes ( const BoundFrustum & bf ) const

Checks if the given bounding frustum is inside the volume defined by the planes of the current bounding frustum.
### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - Bounding frustum.

### Return value

**true** if the given bounding frustum is inside the volume; otherwise, **false**.
## bool insidePlanesValid ( const BoundSphere & bs ) const


Checks if the given bounding sphere is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**true** if the given bounding sphere is inside the volume; otherwise, **false**.
## bool insidePlanesValid ( const BoundBox & bb ) const


Checks if the given bounding box is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**true** if the given bounding box is inside the volume; otherwise, **false**.
## bool insidePlanesValid ( const BoundFrustum & bf ) const


Checks if the given bounding frustum is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - The bounding frustum.

### Return value

**true** if the given bounding frustum is inside the volume; otherwise, **false**.
## bool insidePlanesValidFast ( const BoundSphere & bs ) const


Performs a fast check if the given bounding sphere is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.

### Return value

**true** if the given bounding sphere is inside the volume; otherwise, **false**.
## bool insidePlanesValidFast ( const BoundBox & bb ) const


Performs a fast check if the given bounding box is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundBox](../../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - The bounding box.

### Return value

**true** if the given bounding box is inside the volume; otherwise, **false**.
## bool insidePlanesValidFast ( const BoundFrustum & bf ) const


Performs a fast check if the given bounding frustum is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundFrustum](../../../../api/library/math/bounds/class.boundfrustum_cpp.md) &* **bf** - The bounding frustum.

### Return value

**true** if the given bounding frustum is inside the volume; otherwise, **false**.
## bool insideShadowValid ( const BoundSphere & object , const Math:: vec3 & direction ) const


Checks if the given bounding sphere is inside the shadow of the current bounding frustum.


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **object** - Bounding sphere.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **direction** - The direction vector.

### Return value

**true** if the given bounding sphere is inside the shadow; otherwise, **false**.
## bool insideShadowValid ( const BoundSphere & object , const BoundSphere & light , const Math:: vec3 & offset ) const


Checks if the given bounding sphere is inside the shadow of the current bounding frustum and outside the bounding sphere of a light source.


> **Notice:** The method doesn't check the [status](#isValid_bool) of the current bounding frustum.


### Arguments

- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **object** - Bounding sphere.
- *const [BoundSphere](../../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **light** - The bounding sphere of the light source.
- *const  Math::[vec3](../../../../api/library/math/class.vec3_cpp.md) &* **offset** - The offset vector.

### Return value

**true** if the given bounding sphere is inside the shadow and outside the given light source bounding sphere; otherwise, **false**.
## bool isValid ( ) const

Checks the bounding frustum status.
### Return value

**true** if the bounding frustum is valid, otherwise false.
