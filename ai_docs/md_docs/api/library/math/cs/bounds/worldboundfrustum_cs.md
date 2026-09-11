# Unigine.WorldBoundFrustum Struct (CS)


> **Notice:** The functions listed below are the members of the **Unigine.MathLib** namespace.


This structure serves to construct the bounding frustum in double precision coordinates.


*WorldBoundFrustum* enables you to check:


- if the specified bound volume (box, sphere, or other frustum) gets inside the frustum (even partially) - use *[Inside( bound )](#Inside_WorldBoundSphere_bool)* methods for this purpose.
- if the specified bound volume (box, sphere, or other frustum) is inside the frustum completely - use *[InsideAll( bound )](#InsideAll_WorldBoundSphere_bool)* methods for this purpose.
- if certain points of your object are inside the frustum (may be necessary in case **more accurate results** are required than the ones obtained using the two methods above) - here you should use *[Inside( point )](#Inside_dvec3_bool)* methods and check all points of interest. ![](../../check_points.jpg)


> **Notice:** Make sure that you use proper **aspect-corrected projection** for the frustum when necessary. See the picture in the spoiler below: *red* - default projection matrix, *green* - aspect-corrected projection matrix.


<details>
<summary>Aspect Correction for Frustum's Projection | close</summary>

![](../../boundfrustum1.jpg)
![](../../boundfrustum2.jpg)

</details>


### Usage Example


For example you can use a *WorldBoundFrustum* in order to check whether a node is inside the viewing frustum of a camera. Check the component below.


<details>
<summary>FrustumChecker.cs | close</summary>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#region Math Variables
#if UNIGINE_DOUBLE
using WorldBoundFrustum = Unigine.WorldBoundFrustum;
using Mat4 = Unigine.dmat4;
#else
using WorldBoundFrustum = Unigine.BoundFrustum;
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
		WorldBoundFrustum bfrustum = new WorldBoundFrustum(proj, model_view);

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


## WorldBoundFrustum Class

### Members

---

## WorldBoundFrustum ( mat4 projection , dmat4 modelview )

Constructor. Initializes the bounding frustum by the projection and modelview matrices.
### Arguments

- *mat4* **projection** - Projection matrix.
- *dmat4* **modelview** - Modelview matrix.

## WorldBoundFrustum ( WorldBoundFrustum bf )

Constructor. Initializes the bounding frustum using the specified argument.
### Arguments

- *[WorldBoundFrustum](../../../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum.

## WorldBoundFrustum ( BoundFrustum bf )

Constructor. Initializes the bounding frustum using the specified argument.
### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.

## WorldBoundFrustum ( WorldBoundFrustum bf , dmat4 itransform )

Constructor. Initializes the bounding frustum using the specified arguments.
### Arguments

- *[WorldBoundFrustum](../../../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum.
- *dmat4* **itransform** - The inverse transformation matrix.

## WorldBoundFrustum ( BoundFrustum bf , dmat4 itransform )

Constructor. Initializes the bounding frustum using the specified arguments.
### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.
- *dmat4* **itransform** - The inverse transformation matrix.

## void Set ( mat4 projection , dmat4 modelview )

Sets the bounding frustum by the projection and modelview matrices.
### Arguments

- *mat4* **projection** - Projection matrix.
- *dmat4* **modelview** - Modelview matrix.

## void Set ( WorldBoundFrustum bf )

Sets the bounding frustum using the specified argument.
### Arguments

- *[WorldBoundFrustum](../../../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum.

## void Set ( BoundFrustum bf )

Sets the bounding frustum using the specified argument.
### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.

## void Set ( WorldBoundFrustum bf , dmat4 itransform )

Sets the bounding frustum using the specified arguments.
### Arguments

- *[WorldBoundFrustum](../../../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum.
- *dmat4* **itransform** - The inverse transformation matrix.

## void Set ( BoundFrustum bf , dmat4 itransform )

Sets the bounding frustum using the specified arguments.
### Arguments

- *[BoundFrustum](../../../../../api/library/math/cs/bounds/boundfrustum_cs.md)* **bf** - Bounding frustum.
- *dmat4* **itransform** - The inverse transformation matrix.

## void Clear ( )

Clears the bounding frustum by setting all components/elements to 0.
## bool Equals ( WorldBoundFrustum other )

Checks if the current bounding frustum and the specified argument are equal considering the predefined accuracy (epsilon).
### Arguments

- *[WorldBoundFrustum](../../../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **other** - Value to be checked for equality.

### Return value

**true** if the current bounding frustum is equal to the given one; otherwise, **false**.
## bool EqualsNearly ( WorldBoundFrustum other , double epsilon )

Checks if the current bounding frustum and the specified argument represent the same value with regard to the specified accuracy (epsilon).
### Arguments

- *[WorldBoundFrustum](../../../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **other** - Value to be checked for equality.
- *double* **epsilon** - Epsilon value, that determines accuracy of comparison.

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
## void SetITransform ( dmat4 itransform )

Sets the transformation matrix by an inverse transformation matrix.
### Arguments

- *dmat4* **itransform** - The inverse transformation matrix.

## void SetTransform ( dmat4 transform )

Sets the transformation matrix.
### Arguments

- *dmat4* **transform** - Transformation matrix (*dmat4*) to be set.

## WorldBoundFrustum operator* ( dmat4 m , WorldBoundFrustum bf )

Multiplies the matrix by the bounding frustum and returns the resulting bounding frustum.
### Arguments

- *dmat4* **m** - Matrix.
- *[WorldBoundFrustum](../../../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

Resulting bounding frustum.
## void Expand ( double radius )

Expands the current bounding frustum by the given radius.
### Arguments

- *double* **radius** - Radius.

## bool Inside ( dvec3 point )

Checks if the point is inside the bounding frustum.
### Arguments

- *dvec3* **point** - The coordinates of the point.

### Return value

**true** if the point is inside the bounding frustum; otherwise, **false**.
## bool Inside ( dvec3 point , double radius )

Checks if the sphere is inside the bounding frustum.
### Arguments

- *dvec3* **point** - The coordinates of the center of the sphere.
- *double* **radius** - The sphere radius.

### Return value

**true** if the sphere is inside the bounding frustum; otherwise, **false**.
## bool Inside ( dvec3 p_min , dvec3 p_max )

Checks if the box is inside the bounding frustum.
### Arguments

- *dvec3* **p_min** - Minimum coordinate of the box.
- *dvec3* **p_max** - Maximum coordinate of the box.

### Return value

**true** if the box is inside the bounding frustum; otherwise, **false**.
## bool Inside ( dvec3[] points )

Checks if the bound specified in the argument is inside the current bound.
### Arguments

- *dvec3[]* **points** - Array of points.

### Return value

**true** if the points are inside the bounding frustum; otherwise, **false**.
## bool InsideFast ( dvec3 point )

Performs a fast check if the point is inside the bounding frustum.
### Arguments

- *dvec3* **point** - Point coordinates.

### Return value

**true** if the point is inside the bounding frustum; otherwise, **false**.
## bool InsideFast ( dvec3 point , double radius )

Performs a fast check if the sphere is inside the bounding frustum.
### Arguments

- *dvec3* **point** - Center point.
- *double* **radius** - Radius.

### Return value

**true** if the sphere is inside the bounding frustum; otherwise, **false**.
## bool InsideFast ( dvec3 p_min , dvec3 p_max )

Performs a fast check if the box is inside the bounding frustum.
### Arguments

- *dvec3* **p_min** - Minimum coordinate of the box.
- *dvec3* **p_max** - Maximum coordinate of the box.

### Return value

**true** if the box is inside the bounding frustum; otherwise, **false**.
## bool InsideFast ( dvec3[] points )

Performs a fast check if the set of points is inside the bounding frustum.
### Arguments

- *dvec3[]* **points** - Vector of points.

### Return value

**true** if the point is inside the bounding frustum; otherwise, **false**.
## bool Inside ( WorldBoundSphere bs )

Checks if the bounding sphere is inside the bounding frustum.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool Inside ( WorldBoundBox bb )

Checks if the bounding box is inside the bounding frustum.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the bounding box is inside the bounding frustum; otherwise, **false**.
## bool Inside ( WorldBoundFrustum bf )

Checks if the specified bounding frustum is inside the current bounding frustum.
### Arguments

- *[WorldBoundFrustum](../../../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the specified bounding frustum is inside the bounding frustum; otherwise, **false**.
## bool InsideValid ( WorldBoundSphere bs )


Checks if the given bounding sphere is inside the bounding frustum (assuming that the current bound coordinates are valid).


> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.


### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the given bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool InsideValid ( WorldBoundBox bb )

Checks if the given bounding box is inside the bounding frustum.

> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.

### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the given bounding box is inside the bounding frustum; otherwise, **false**.
## bool InsideValid ( WorldBoundFrustum bf )

Checks if the given bounding frustum is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.

### Arguments

- *[WorldBoundFrustum](../../../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the given bounding frustum is inside the bounding frustum; otherwise, **false**.
## bool InsideValidFast ( WorldBoundSphere bs )

Performs a fast check if the given bounding sphere is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check the status of the current bound.

### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the given bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool InsideValidFast ( WorldBoundBox bb )

Performs a fast check if the given bounding box is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check the status of the current bound.

### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the given bounding box is inside the bounding frustum; otherwise, **false**.
## bool InsideValidFast ( WorldBoundFrustum bf )

Performs a fast check if the given bounding frustum is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check the status of the current bound.

### Arguments

- *[WorldBoundFrustum](../../../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the given bounding frustum is inside the bounding frustum; otherwise, **false**.
## bool InsideAll ( WorldBoundSphere bs )

Checks if the whole given bounding sphere is inside the current bounding frustum.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the whole bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool InsideAll ( WorldBoundBox bb )

Checks if the whole given bounding box is inside the current bounding frustum.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the whole bounding box is inside the bounding frustum; otherwise, **false**.
## bool InsideAll ( WorldBoundFrustum bf )

Checks if the whole specified bounding frustum is inside the current bounding frustum.
### Arguments

- *[WorldBoundFrustum](../../../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the whole specified bounding frustum is inside the current bounding frustum; otherwise, **false**.
## bool InsideAllValid ( WorldBoundSphere bs )

Checks if the whole given bounding sphere is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.

### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the given bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool InsideAllValid ( WorldBoundBox bb )

Checks if the whole given bounding box is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.

### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the given bounding box is inside the bounding frustum; otherwise, **false**.
## bool InsideAllValid ( WorldBoundFrustum bf )

Checks if the whole given bounding frustum is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check if the minimum and maximum coordinates of the current bound are valid.

### Arguments

- *[WorldBoundFrustum](../../../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the given bounding frustum is inside the bounding frustum; otherwise, **false**.
## bool InsideAllValidFast ( WorldBoundSphere bs )

Performs a fast check if the whole given bounding sphere is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check the status of the current bound.

### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the given bounding sphere is inside the bounding frustum; otherwise, **false**.
## bool InsideAllValidFast ( WorldBoundBox bb )

Performs a fast check if the whole given bounding box is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check the status of the current bound.

### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the given bounding box is inside the bounding frustum; otherwise, **false**.
## bool InsideAllValidFast ( WorldBoundFrustum bf )

Performs a fast check if the whole given bounding frustum is inside the current bounding frustum (assuming that the current bound coordinates are valid).

> **Notice:** The method doesn't check the status of the current bound.

### Arguments

- *[WorldBoundFrustum](../../../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the given bounding frustum is inside the bounding frustum; otherwise, **false**.
## bool InsidePlanes ( WorldBoundSphere bs )

Checks if the given bounding sphere is inside the volume defined by the planes of the current bounding frustum.
### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the given bounding sphere is inside the volume; otherwise, **false**.
## bool InsidePlanes ( WorldBoundBox bb )

Checks if the given bounding box is inside the volume defined by the planes of the current bounding frustum.
### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the given bounding box is inside the volume; otherwise, **false**.
## bool InsidePlanes ( WorldBoundFrustum bf )

Checks if the given bounding frustum is inside the volume defined by the planes of the current bounding frustum.
### Arguments

- *[WorldBoundFrustum](../../../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the given bounding frustum is inside the volume; otherwise, **false**.
## bool InsidePlanesValid ( WorldBoundSphere bs )


Checks if the given bounding sphere is inside the volume defined by the planes of the current bounding frustum.


> **Notice:** The method doesn't check the status of the current bound.


### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the given bounding sphere is inside the volume; otherwise, **false**.
## bool InsidePlanesValid ( WorldBoundBox bb )


Checks if the given bounding box is inside the volume defined by the planes of the current bounding frustum.


> **Notice:** The method doesn't check the status of the current bound.


### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the given bounding box is inside the volume; otherwise, **false**.
## bool InsidePlanesValid ( WorldBoundFrustum bf )


Checks if the given bounding frustum is inside the volume defined by the planes of the current bounding frustum.


> **Notice:** The method doesn't check the status of the current bound.


### Arguments

- *[WorldBoundFrustum](../../../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the given bounding frustum is inside the volume; otherwise, **false**.
## bool InsidePlanesValidFast ( WorldBoundSphere bs )


Performs a fast check if the given bounding sphere is inside the volume defined by the planes of the current bounding frustum.


> **Notice:** The method doesn't check the status of the current bound.


### Arguments

- *[WorldBoundSphere](../../../../../api/library/math/cs/bounds/worldboundsphere_cs.md)* **bs** - Bounding sphere.

### Return value

**true** if the given bounding sphere is inside the volume; otherwise, **false**.
## bool InsidePlanesValidFast ( WorldBoundBox bb )


Performs a fast check if the given bounding box is inside the volume defined by the planes of the current bounding frustum.


> **Notice:** The method doesn't check the status of the current bound.


### Arguments

- *[WorldBoundBox](../../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box.

### Return value

**true** if the given bounding box is inside the volume; otherwise, **false**.
## bool InsidePlanesValidFast ( WorldBoundFrustum bf )


Performs a fast check if the given bounding frustum is inside the volume defined by the planes of the current bounding frustum.


> **Notice:** The method doesn't check the status of the current bound.


### Arguments

- *[WorldBoundFrustum](../../../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum.

### Return value

**true** if the given bounding frustum is inside the volume; otherwise, **false**.
