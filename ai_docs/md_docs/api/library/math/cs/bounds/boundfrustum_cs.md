# Unigine.BoundFrustum Struct (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


This structure serves to construct the bounding frustum in single precision coordinates.


*BoundFrustum* enables you to check:


- if the specified bound volume (box, sphere, or other frustum) gets inside the frustum (even partially) - use *[Inside( bound )](#Inside_BoundSphere_bool)* methods for this purpose.
- if the specified bound volume (box, sphere, or other frustum) is inside the frustum completely - use *[InsideAll( bound )](#InsideAll_BoundSphere_bool)* methods for this purpose.
- if certain points of your object are inside the frustum (may be necessary in case **more accurate results** are required than the ones obtained using the two methods above) - here you should use *[Inside( point )](#Inside_vec3_bool)* methods and check all points of interest. ![](../../check_points.jpg)


> **Notice:** Make sure that you use proper **aspect-corrected projection** for the frustum when necessary. See the picture in the spoiler below: *red* - default projection matrix, *green* - aspect-corrected projection matrix.


<details>
<summary>Aspect Correction for Frustum's Projection | close</summary>

![](../../boundfrustum1.jpg)
![](../../boundfrustum2.jpg)

</details>


### Usage Example


For example you can use a *BoundFrustum* in order to check whether a node is inside the viewing frustum of a camera. Check the component below.


<details>
<summary>FrustumChecker.cs | close</summary>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#region Math Variables
#if UNIGINE_DOUBLE
using BoundFrustum = Unigine.BoundFrustum;
using Mat4 = Unigine.mat4;
#else
using BoundFrustum = Unigine.BoundFrustum;
using Mat4 = Unigine.mat4;
#endif
#endregion

public partial class FrustumChecker : Component
{
	private void Init()
	{
		// write here code to be called on component initialization

	}

	private void Update()
	{
		// getting the current camera
		Camera camera = Game.Player.Camera;

		// getting the main window of the application
		EngineWindow main_window = WindowManager.MainWindow;
		if (!main_window)
			Engine.Quit();

		// calculating the current aspect ratio to obtain proper aspect-corrected projection matrix
		// default projection matrix does not take aspect ratio into account
		ivec2 main_size = main_window.Size;
		float aspect = (float)main_size.y / main_size.x;
		mat4 proj = camera.GetAspectCorrectedProjection(aspect);

		// getting model-view matrix of the camera
		Mat4 model_view = camera.Modelview;
		BoundFrustum bfrustum = new BoundFrustum(proj, model_view);

		// checking if the node's bound gets inside the viewing frustum of the camera
		if (bfrustum.Inside(node.WorldBoundBox)){
			Log.Message("Node's bound is visible inside the frustum.");

			// checking whether the bound is completely or partially inside the frustum
			Log.Message(bfrustum.InsideAll(node.WorldBoundBox) ? " COMPLETELY!\n": " PARTIALLY!\n");

			// checking whether a certain point of the object (WorldPosition here) is inside the frustum
			Log.Message(bfrustum.Inside(node.WorldPosition) ? "(The point is INSIDE)\n": "(The point is OUTSIDE)\n");
		}
		else
			Log.Message("Node's bound is outside the frustum.\n");

		// displaying node's BoundBox, the Bound Frustum, and a point using the Visualizer
		Visualizer.RenderFrustum(proj, MathLib.Inverse(model_view), new vec4(1.0f, 0.0f,0.0f,1.0f));
		Visualizer.RenderBoundBox(node.BoundBox, node.Transform, new vec4(0.0f, 1.0f, 0.0f, 1.0f));
		Visualizer.RenderSphere(0.01f, MathLib.Translate(node.WorldPosition), new vec4(1.0f, 0.0f, 0.0f, 1.0f));
	}
}

```

</details>


## BoundFrustum Class

### Members

---

## BoundFrustum ( mat4 projection , mat4 modelview )

Constructor. Initializes the bounding frustum by the projection and modelview matrices.
### Arguments

- *mat4* **projection** - Projection matrix.
- *mat4* **modelview** - Modelview matrix.

## BoundFrustum ( BoundFrustum bf )

Constructor. Initializes the bounding frustum using the specified argument.
### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.

## BoundFrustum ( BoundFrustum bf , mat4 itransform )

Constructor. Initializes the bounding frustum using the specified arguments.
### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.
- *mat4* **itransform** - The inverse transformation matrix.

## void Set ( mat4 projection , mat4 modelview )

Sets the bounding frustum by the projection and modelview matrices.
### Arguments

- *mat4* **projection** - Projection matrix.
- *mat4* **modelview** - Modelview matrix.

## void Set ( mat4 proj )

Sets the bounding frustum by the projection matrix.
### Arguments

- *mat4* **proj** - Projection matrix.

## void Set ( BoundFrustum bf )

Sets the bounding frustum using the specified argument.
### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.

## void Set ( BoundFrustum bf , mat4 itransform )

Sets the bounding frustum using the specified arguments.
### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.
- *mat4* **itransform** - The inverse transformation matrix.

## void Clear ( )

Clears the bounding frustum by setting all components/elements to 0.
## bool Equals ( BoundFrustum other )

Checks if the current bounding frustum and the specified argument are equal considering the predefined accuracy (epsilon).
### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **other** - Value to be checked for equality.

### Return value

**true** if the current bounding frustum is equal to the given one; otherwise, **false**.
## bool EqualsNearly ( BoundFrustum other , float epsilon )

Checks if the current bounding frustum and the specified argument represent the same value with regard to the specified accuracy (epsilon).
### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **other** - Value to be checked for equality.
- *float* **epsilon** - Epsilon value, that determines accuracy of comparison.

### Return value

**true** if the current bounding frustum is equal to the given one; otherwise, **false**.
## bool Equals ( object obj )

Checks if the current bounding frustum and the specified argument are equal considering the predefined accuracy (epsilon).
### Arguments

- *[object](../../../../../api/library/objects/class.object_cs.md)* **obj** - Object.

### Return value

**true** if the current bounding frustum is equal to the given object; otherwise, **false**.
## int GetHashCode ( )

Returns a hash code for the current bounding frustum. Serves as the default hash function.
### Return value

Hash code.
## void SetITransform ( mat4 itransform )

Sets the transformation matrix by an inverse transformation matrix.
### Arguments

- *mat4* **itransform** - The inverse transformation matrix.

## void SetITransform ( dmat4 itransform )

Sets the transformation matrix by an inverse transformation matrix.
### Arguments

- *dmat4* **itransform** - The inverse transformation matrix.

## void SetTransform ( mat4 transform )

Sets the transformation matrix.
### Arguments

- *mat4* **transform** - Transformation matrix (*mat4*) to be set.

## void SetTransform ( dmat4 transform )

Sets the transformation matrix.
### Arguments

- *dmat4* **transform** - Transformation matrix (*dmat4*) to be set.

## BoundFrustum operator* ( mat4 m , BoundFrustum bf )

Multiplies the matrix by the bounding frustum and returns the resulting bounding frustum.
### Arguments

- *mat4* **m** - Matrix.
- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

Resulting bounding frustum.
## BoundFrustum operator* ( dmat4 m , BoundFrustum bf )

Multiplies the matrix by the bounding frustum and returns the resulting bounding frustum.
### Arguments

- *dmat4* **m** - Matrix.
- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

Resulting bounding frustum.
## void Expand ( float radius )

Expands the current bounding frustum by the given radius.
### Arguments

- *float* **radius** - Radius.

## bool Inside ( vec3 point )

Checks if the point is inside the bounding frustum.
### Arguments

- *vec3* **point** - The coordinates of the point.

### Return value

**true** if the point is inside the bounding frustum; otherwise, **false**.
## bool Inside ( vec3 point , float radius )

Checks if the sphere is inside the bounding frustum.
### Arguments

- *vec3* **point** - The coordinates of the center of the sphere.
- *float* **radius** - The sphere radius.

### Return value

**true** if the sphere is inside the bounding frustum; otherwise, **false**.
## bool Inside ( vec3 p_min , vec3 p_max )

Checks if the box is inside the bounding frustum.
### Arguments

- *vec3* **p_min** - Minimum coordinate of the box.
- *vec3* **p_max** - Maximum coordinate of the box.

### Return value

**true** if the box is inside the bounding frustum; otherwise, **false**.
## bool Inside ( vec3[] points )

Checks if the bound specified in the argument is inside the current bound.
### Arguments

- *vec3[]* **points** - Array of points.

### Return value

**true** if the points are inside the bounding frustum; otherwise, **false**.
## bool InsideFast ( vec3 point )

Performs a fast check if the point is inside the bounding frustum.
### Arguments

- *vec3* **point** - Point coordinates.

### Return value

**true** if the point is inside the bounding frustum; otherwise, **false**.
## bool InsideFast ( vec3 point , float radius )

Performs a fast check if the sphere is inside the bounding frustum.
### Arguments

- *vec3* **point** - Center point.
- *float* **radius** - Radius.

### Return value

**true** if the sphere is inside the bounding frustum; otherwise, **false**.
## bool InsideFast ( vec3 p_min , vec3 p_max )

Performs a fast check if the box is inside the bounding frustum.
### Arguments

- *vec3* **p_min** - Minimum coordinate of the box.
- *vec3* **p_max** - Maximum coordinate of the box.

### Return value

**true** if the box is inside the bounding frustum; otherwise, **false**.
## bool InsideFast ( vec3[] points )

Performs a fast check if the set of points is inside the bounding frustum.
### Arguments

- *vec3[]* **points** - Vector of points.

### Return value

**true** if the point is inside the bounding frustum; otherwise, **false**.
## bool Inside ( BoundSphere bs )

Checks if the bounding sphere is inside the bounding frustum.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool Inside ( BoundBox bb )

Checks if the bounding box is inside the bounding frustum.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the bounding box is inside the bounding frustum; otherwise, **false**.
## bool Inside ( BoundFrustum bf )

Checks if the specified bounding frustum is inside the current bounding frustum.
### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the specified bounding frustum is inside the bounding frustum; otherwise, **false**.
## bool InsideValid ( BoundSphere bs )


Checks if the given bounding sphere is inside the bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.


### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the given bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool InsideValid ( BoundBox bb )

Checks if the given bounding box is inside the bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.

### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the given bounding box is inside the bounding frustum; otherwise, **false**.
## bool InsideValid ( BoundFrustum bf )

Checks if the given bounding frustum is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.

### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the given bounding frustum is inside the bounding frustum; otherwise, **false**.
## bool InsideValidFast ( BoundSphere bs )

Performs a fast check if the given bounding sphere is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check the status of the current bound.

### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the given bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool InsideValidFast ( BoundBox bb )

Performs a fast check if the given bounding box is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check the status of the current bound.

### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the given bounding box is inside the bounding frustum; otherwise, **false**.
## bool InsideValidFast ( BoundFrustum bf )

Performs a fast check if the given bounding frustum is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check the status of the current bound.

### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the given bounding frustum is inside the bounding frustum; otherwise, **false**.
## bool InsideAll ( BoundSphere bs )

Checks if the whole given bounding sphere is inside the current bounding frustum.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the whole bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool InsideAll ( BoundBox bb )

Checks if the whole given bounding box is inside the current bounding frustum.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the whole bounding box is inside the bounding frustum; otherwise, **false**.
## bool InsideAll ( BoundFrustum bf )

Checks if the whole specified bounding frustum is inside the current bounding frustum.
### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the whole specified bounding frustum is inside the current bounding frustum; otherwise, **false**.
## bool InsideAllValid ( BoundSphere bs )

Checks if the whole given bounding sphere is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.

### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the given bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool InsideAllValid ( BoundBox bb )

Checks if the whole given bounding box is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.

### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the given bounding box is inside the bounding frustum; otherwise, **false**.
## bool InsideAllValid ( BoundFrustum bf )

Checks if the whole given bounding frustum is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.

### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the given bounding frustum is inside the bounding frustum; otherwise, **false**.
## bool InsideAllValidFast ( BoundSphere bs )

Performs a fast check if the whole given bounding sphere is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check the status of the current bound.

### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the given bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool InsideAllValidFast ( BoundBox bb )

Performs a fast check if the whole given bounding box is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check the status of the current bound.

### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the given bounding box is inside the bounding frustum; otherwise, **false**.
## bool InsideAllValidFast ( BoundFrustum bf )

Performs a fast check if the whole given bounding frustum is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check the status of the current bound.

### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the given bounding frustum is inside the bounding frustum; otherwise, **false**.
## bool InsidePlanes ( BoundSphere bs )

Checks if the given bounding sphere is inside the volume defined by the planes of the current bounding frustum.
### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the given bounding sphere is inside the volume; otherwise, **false**.
## bool InsidePlanes ( BoundBox bb )

Checks if the given bounding box is inside the volume defined by the planes of the current bounding frustum.
### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the given bounding box is inside the volume; otherwise, **false**.
## bool InsidePlanes ( BoundFrustum bf )

Checks if the given bounding frustum is inside the volume defined by the planes of the current bounding frustum.
### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the given bounding frustum is inside the volume; otherwise, **false**.
## bool InsidePlanesValid ( BoundSphere bs )


Checks if the given bounding sphere is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the status of the current bound.


### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the given bounding sphere is inside the volume; otherwise, **false**.
## bool InsidePlanesValid ( BoundBox bb )


Checks if the given bounding box is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the status of the current bound.


### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the given bounding box is inside the volume; otherwise, **false**.
## bool InsidePlanesValid ( BoundFrustum bf )


Checks if the given bounding frustum is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the status of the current bound.


### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the given bounding frustum is inside the volume; otherwise, **false**.
## bool InsidePlanesValidFast ( BoundSphere bs )


Performs a fast check if the given bounding sphere is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the status of the current bound.


### Arguments

- *[BoundSphere](../../../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the given bounding sphere is inside the volume; otherwise, **false**.
## bool InsidePlanesValidFast ( BoundBox bb )


Performs a fast check if the given bounding box is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the status of the current bound.


### Arguments

- *[BoundBox](../../../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the given bounding box is inside the volume; otherwise, **false**.
## bool InsidePlanesValidFast ( BoundFrustum bf )


Performs a fast check if the given bounding frustum is inside the volume defined by the planes of the current bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check the status of the current bound.


### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the given bounding frustum is inside the volume; otherwise, **false**.
