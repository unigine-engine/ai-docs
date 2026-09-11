# Unigine.Camera Class (CS)


The **Camera** class is used to create a new camera, set it up (set all the required matrices, field of view, masks and so on) and then pass it to an instance of the [Viewport](../../../api/library/rendering/class.viewport_cs.md) class to render an image from this camera.


> **Notice:** An instance of this class is **not a node**.


A camera instance can have the following masks:


- Sound Source mask
- Sound Reverberation mask
- Viewport mask
- Reflection Viewport mask


Camera settings can be set up in the [Camera Settings in UnigineEditor](../../../editor2/camera_settings/index.md).


### Usage Example


In this example Camera and *[PlayerSpectator](../../../api/library/players/class.playerspectator_cs.md)* (which inherited from *Player* class) instances created and added to the current scene. Here is a code from the `AppWorldLogic.cs` file.


```csharp
namespace UnigineApp
{
	class AppWorldLogic : WorldLogic
	{
		PlayerSpectator playerSpectator;
		Camera camera;

		/* ... */

		public override bool Init()
		{
			/* ... */
			// initialize PlayerSpectator and Camera instances
			playerSpectator = new PlayerSpectator();
			camera = new Camera();

			// specify the necessary camera parameters: FOV, ZNear, ZFar.
			// add the post_sensor_red post-effect to camera
			camera.Fov = 110.0f;
			camera.ZNear = 0.1f;
			camera.ZFar = 10000.0f;

			// set camera to the player
			playerSpectator.Camera = camera;

			// specify the position and view direction of playerSpectator
			playerSpectator.ViewDirection = new vec3(0.0f, 1.0f, 0.0f);
			playerSpectator.WorldPosition = new vec3(-1.6f, -1.7f, 1.7f);

			Game.Player = playerSpectator;

			return 1;
		}
	}
}

```


## Camera Class

### Enums

## PROJECTION_MODE

| Name | Description |
|---|---|
| **PERSPECTIVE** = 0 | Perspective projection. |
| **ORTHOGRAPHIC** = 1 | Orthographic projection. |

## FOV_FIXED

| Name | Description |
|---|---|
| **VERTICAL** = 0 | Vertical FOV component is fixed. |
| **HORIZONTAL** = 1 | Horizontal FOV component is fixed. |

## FOV_MODE

| Name | Description |
|---|---|
| **VERTICAL** = 0 | Vertical FOV mode. Vertical FOV of the camera is determined by the [FOV](#setFov_float_void) value. |
| **PHYSICALLY_BASED_CAMERA** = 1 | Physically based mode. Horizontal FOV of the physically-based camera is calculated using the [focal length](#setFocalLength_float_void) and [film gate](#setFilmGate_float_void) values according to the following formula: **FOV_h = 2 * atan(film_gate / (2 * focal_length)) * RAD2DEG** |

### Properties

## 🔒︎ int NumScriptableMaterials

The total number of [scriptable materials](../../../content/materials/scriptable.md) attached to the camera.
## int ReverbMask

The bit mask that determines what reverberation zones can be heard. for sound to reverberate, at least one bit of this mask should match a reverb mask of the sound source and a reverb mask of the reverberation zone. masks of a sound source and reverberation zone can match with the camera's one in several bits, not necessarily one.
## int SourceMask

The bit mask that determines what sound channels can be heard. for a sound source to be heard, its mask should match this one in at least one bit. Plus, the volume of sound channel in which the sound plays (its number also depends on this mask) should not be equal to **0**.
## int ReflectionViewportMask

The bit mask for rendering reflections into the camera viewport. Reflections are rendered in the camera viewport if masks of reflective materials match this one (one bit at least).
## int ViewportMask

The bit mask for rendering into the viewport. Object surfaces, materials, decals, lights and GUI objects will be rendered into the viewport only if their viewport mask matches the camera's one (one matching bit is enough).
## bool ObliqueFrustum

The value indicating if the viewing frustum is oblique.
> **Notice:** It is recommended to set oblique viewing frustum using this method, as it doesn't affect the projection matrix. To specify the near clipping plane use the *[setObliqueFrustumPlane()](#setObliqueFrustumPlane_Vec4_void)* method.


## vec4 ObliqueFrustumPlane

The oblique near clipping plane of the viewing frustum.
> **Notice:** This method does not affect the projection matrix. To enable the oblique frustum use the *[setObliqueFrustum()](#setObliqueFrustum_int_void)* method.


```csharp
// AppWorldLogic.cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Unigine;

namespace UnigineApp
{
	class AppWorldLogic : WorldLogic
	{
		/* .. */

		public override bool Update()
		{

			float time = Game.Time;

				// initializing a plane to be set as a near clipping plane
				vec4 plane = new vec4(1.0f, 1.0f, 1.0f, 1.0f + MathLib.Sin(time) * 4.0f);

				// getting a camera
				Camera camera = Game.Player.Camera;
				if (camera != null)
				{
					// enabling oblique frustum
					camera.ObliqueFrustum = true;

					// setting our plane as an oblique near clipping plane
					camera.ObliqueFrustumPlane = plane;
				}

			return true;
		}

		/* .. */
	}
}

```


## vec3 Up

The up direction of the camera's viewport (i.e. tilt of the camera's viewport).
## float ZFar

The distance to the far clipping plane of the camera's viewing frustum. Changing the value updates the projection matrix.
## float ZNear

The distance to the near clipping plane of the camera's viewing frustum. Changing the value updates the projection matrix.
## float FocalLength

The focal length of the physically-based camera lens.
## float FilmGate

The film gate for the physically-based camera with horizontal fov.
## float Fov

The vertical field of view of the camera.
> **Notice:** Horizontal FOV cannot be used since it varies depending on the viewport's aspect ratio. Setting FOV recalculates projection matrix with **aspect ratio = 1**.


You can use the following formula to calculate horizontal FOV from the vertical one for the given aspect ratio (width/height): **FOV_h = 2 � atan ( (width / height) � tan(FOV_v / 2))**.


## 🔒︎ Camera.FOV_FIXED FovFixed

The value indicating which fov component (horizontal or vertical) is currently fixed.
## Camera.FOV_MODE FovMode

The value indicating the type of FOV that is used for the camera:
- For the classic camera, the vertical FOV should be set. In this case, FOV is directly set in [degrees](#setFov_float_void).
- For the physically-based camera, the horizontal FOV should be set. In this case, FOV is calculated depending on the [film gate](#setFilmGate_float_void) and [focal length](#setFocalLength_float_void) of the camera.


## mat4 Projection

The projection matrix with unit (1.0) aspect ratio.
> **Notice:** It is not recommended to use this method for setting obliqueness of the near clipping plane of the frustum, as in this case a number of features (such as clouds, shadows, TAA, a number of engine optimizations, etc.) will not function properly. Please, use the [setObliqueFrustum()](#setObliqueFrustum_int_void) method instead.


This method allows you to set your camera to use [perspective](../../../principles/world_management/index.md#camera_perspective) or [orthographic](../../../principles/world_management/index.md#camera_orthographic) projection, depending on your project's requirements.


For example, you can use the following code to set up **orthographic projection** or **perspective projection** for your camera depending on a flag value:


```csharp
// AppWorldLogic.cs

namespace UnigineApp
{
	class AppWorldLogic : WorldLogic
	{
		Camera camera;
		Player player;
		/* ... */

		// ortho flag - change this value to switch projection type
		bool ortho = false;
		public override bool Init()
		{
			/* ... */

			// getting the camera of the current player
			camera = Game.Player.Camera;

			// setting up near and far clipping planes and aspect ratio
			float znear = 0.001f;
			float zfar = 10000.0f;
			float aspect = 16.0f / 9.0f;

			if (ortho)
			{
				// setting up orthographic projection
				camera.Projection = MathLib.Ortho(-1.0f, 1.0f, -1.0f, 1.0f, znear, zfar);
			}
			else
			{
				// setting up perspective projection
				camera.Projection = MathLib.Perspective(60.0f, aspect, znear, zfar);
			}
			// setting player's camera
			Game.Player.Camera = camera;

			return true;
		}
	}
}

```


## mat4 Offset

The additional transformation (an offset matrix) set for the camera. This transformation is applied after modelview transformation. The offset matrix does not affect the view matrix or the position of the camera. For example, it can be used to simulate camera shake from an explosion.
## vec3 Position

The position of the camera. The position vector is stored in the 3rd column of the view matrix (modelview and inverse modelview).
## 🔒︎ mat4 IModelview

The inverted view matrix of the camera.
## mat4 Modelview

The view matrix of the camera.
## float OrthoHeight

The height of the camera with the orthographic [projection mode](#getProjectionMode_int) enabled.
## Camera.PROJECTION_MODE ProjectionMode

The projection mode: orthographic or perspective.
### Members

---

## Camera ( )

Constructor. Creates a new camera with default settings:
- [Modelview](#setModelview_Mat4_void), [inverse modelview](#getIModelview_Mat4) and [offset matrices](#setOffset_mat4_void) are 4�4 identity matrices.
- FOV is 60 degrees.
- [Distance to the near clipping plane](#setZNear_float_void) is 0.1 unit.
- [Distance to the far clipping plane](#setZFar_float_void) is 10000 units.
- [Up direction vector](#setUp_vec3_void) is (0,0,1).
- Viewport, reflection, source and reverb masks are set to 00000001.


## void GetDirectionFromScreen ( out Vec3 p0 , out Vec3 p1 , float screen_x , float screen_y , float aspect )

Casts the ray from a certain position on the screen.
### Arguments

- *out Vec3* **p0** - Start coordinate of the ray.
- *out Vec3* **p1** - End coordinate of the ray.
- *float* **screen_x** - X-coordinate of screen, in the [0;1] range, where 0 is the left upper point, 1 is the right lower point.
- *float* **screen_y** - Y-coordinate of screen, in the [0;1] range, where 0 is the left upper point, 1 is the right lower point.
- *float* **aspect** - Screen's aspect ratio (height to width).

## vec3 GetDirectionFromScreen ( float screen_x , float screen_y , float aspect )

Casts the ray from a certain position on the screen.
### Arguments

- *float* **screen_x** - X-coordinate of screen, in the [0;1] range, where 0 is the left upper point, 1 is the right lower point.
- *float* **screen_y** - Y-coordinate of screen, in the [0;1] range, where 0 is the left upper point, 1 is the right lower point.
- *float* **aspect** - Screen's aspect ratio (height to width).

### Return value

Point coordinate.
## mat4 GetProjectionFromScreen ( float screen_x0 , float screen_y0 , float screen_x1 , float screen_y1 , float aspect )

Creates a projection matrix out of 2 screen positions. This is required for the frame selection.
### Arguments

- *float* **screen_x0** - X-coordinate of the first screen position, in the [0;1] range, where 0 is the left upper point, 1 is the right lower point.
- *float* **screen_y0** - Y-coordinate of the first screen position, in the [0;1] range, where 0 is the left upper point, 1 is the right lower point.
- *float* **screen_x1** - X-coordinate of the second screen position, in the [0;1] range, where 0 is the left upper point, 1 is the right lower point.
- *float* **screen_y1** - Y-coordinate of the second screen position, in the [0;1] range, where 0 is the left upper point, 1 is the right lower point.
- *float* **aspect** - Screen's aspect ratio (height to width).

### Return value

Projection matrix.
## int GetScreenPosition ( out float screen_x , out float screen_y , vec3 point , float aspect )

Projects the point in world coordinates to the screen. Screen coordinates are written into the first 2 variables passed to the method.
### Arguments

- *out float* **screen_x** - X-coordinate of the screen position.
- *out float* **screen_y** - Y-coordinate of the screen position.
- *vec3* **point** - Point coordinates.
- *float* **aspect** - Aspect ratio (screen height to width).

### Return value

**1** if the point has been projected successfully; otherwise, **0**.
## Camera Clone ( )

Clones the current camera and saves it to the given camera instance.
### Return value

Copy of the camera.
## mat4 GetAspectCorrectedProjection ( float aspect )

Returns projection matrix after correction for the specified aspect ratio. [Currently fixed FOV component](#getFovFixed_int) is taken into account.
### Arguments

- *float* **aspect** - Aspect ratio.

### Return value

Projection matrix after correction for the specified aspect ratio.
## void AddScriptableMaterial ( Material material )

Attaches a new [scriptable material](../../../content/materials/scriptable.md) to the camera.
To apply a scriptable material globally, use the *[AddScriptableMaterial()](../../../api/library/rendering/class.render_cs.md#addScriptableMaterial_Material_void)* method of the *Render* class. The order of execution for scripts assigned to scriptable materials is defined by material's number in the list of the camera.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cs.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-camera.


### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Scriptable material to be attached to the camera.

## void InsertScriptableMaterial ( int num , Material material )

Inserts a new [scriptable material](../../../content/materials/scriptable.md) into the list of the ones assigned to the camera.
To apply a scriptable material globally, use the [*insertScriptableMaterial()*](../../../api/library/rendering/class.render_cs.md#insertScriptableMaterial_int_Material_void) method of the *Render* class. The order of execution for scripts assigned to scriptable materials is defined by material's number in the camera's list.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cs.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-camera.


### Arguments

- *int* **num** - Position at which a new scriptable material is to be inserted.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Scriptable material to be inserted.

## void RemoveScriptableMaterial ( int num )

Removes the [scriptable material](../../../content/materials/scriptable.md) with the specified number from the camera.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

## int FindScriptableMaterial ( Material material )

 Returns the number of the specified [scriptable material](../../../content/materials/scriptable.md) for the camera.
This number is camera-specific (valid for this camera only) and determines the order in which the assigned expressions are executed.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cs.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-camera.


### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Scriptable material for which a number is to be found.

### Return value

Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int), or -1 if the specified material was not found.
## void SetScriptableMaterial ( int num , Material material )

Replaces the [scriptable material](../../../content/materials/scriptable.md) with the specified number with the new scriptable material specified.
The number of material determines the order in which the expressions assigned to it are executed. This number is camera-specific (valid for this camera only).


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cs.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-camera.


### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - New scriptable material to replace the one with the specified number.

## Material GetScriptableMaterial ( int num )

Returns a [scriptable material](../../../content/materials/scriptable.md) attached to the camera by its number.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

### Return value

Scriptable material attached to the camera with the specified number.
## void SetScriptableMaterialEnabled ( int num , bool enabled )

Enables or disables the [scriptable material](../../../content/materials/scriptable.md) with the specified number. When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *bool* **enabled** - true to enable the scriptable material with the specified number, false to disable it.

## bool GetScriptableMaterialEnabled ( int num )

Returns a value indicating if the [scriptable material](../../../content/materials/scriptable.md) with the specified number attached to the camera is enabled (active). When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

### Return value

true if the scriptable material with the specified number is enabled; otherwise, false.
## void SwapScriptableMaterials ( int num_0 , int num_1 )

Swaps two [scriptable materials](../../../content/materials/scriptable.md) with specified numbers.
The number of material determines the order in which the expressions assigned to it are executed.


> **Notice:** The number is camera-specific (valid for this camera only).


### Arguments

- *int* **num_0** - Number of the first scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *int* **num_1** - Number of the second scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

## void ClearScriptableMaterials ( )

Clears all [scriptable materials](../../../content/materials/scriptable.md) attached to the camera.
## Camera Copy ( Camera camera )

Copies the parameters from the source camera to this camera instance.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Source camera instance.

### Return value

This camera instance.
## void Swap ( Camera camera )

Swaps the parameters between the specified camera and this camera instance.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - Camera instance.
