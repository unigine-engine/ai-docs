# Unigine.Camera Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The **Camera** class is used to create a new camera, set it up (set all the required matrices, field of view, masks and so on) and then pass it to an instance of the [Viewport](../../../api/library/rendering/class.viewport_usc.md) class to render an image from this camera.


> **Notice:** An instance of this class is **not a node**.


A camera instance can have the following masks:


- Sound Source mask
- Sound Reverberation mask
- Viewport mask
- Reflection Viewport mask


Camera settings can be set up in the [Camera Settings in UnigineEditor](../../../editor2/camera_settings/index.md).


## Camera Class

### Members

## int getNumScriptableMaterials () const

Returns the current The total number of [scriptable materials](../../../content/materials/scriptable.md) attached to the camera.
### Return value

Current number of scriptable materials attached to the camera.
## void setReverbMask ( int mask )

Sets a new bit mask that determines what reverberation zones can be heard. for sound to reverberate, at least one bit of this mask should match a reverb mask of the sound source and a reverb mask of the reverberation zone. masks of a sound source and reverberation zone can match with the camera's one in several bits, not necessarily one.
### Arguments

- *int* **mask** - The integer, each bit of which is used to set a mask for reverberating sound sources and reverberation zones.

## int getReverbMask () const

Returns the current bit mask that determines what reverberation zones can be heard. for sound to reverberate, at least one bit of this mask should match a reverb mask of the sound source and a reverb mask of the reverberation zone. masks of a sound source and reverberation zone can match with the camera's one in several bits, not necessarily one.
### Return value

Current integer, each bit of which is used to set a mask for reverberating sound sources and reverberation zones.
## void setSourceMask ( int mask )

Sets a new bit mask that determines what sound channels can be heard. for a sound source to be heard, its mask should match this one in at least one bit. Plus, the volume of sound channel in which the sound plays (its number also depends on this mask) should not be equal to **0**.
### Arguments

- *int* **mask** - The integer, each bit of which specifies a sound channel.

## int getSourceMask () const

Returns the current bit mask that determines what sound channels can be heard. for a sound source to be heard, its mask should match this one in at least one bit. Plus, the volume of sound channel in which the sound plays (its number also depends on this mask) should not be equal to **0**.
### Return value

Current integer, each bit of which specifies a sound channel.
## void setReflectionViewportMask ( int mask )

Sets a new bit mask for rendering reflections into the camera viewport. Reflections are rendered in the camera viewport if masks of reflective materials match this one (one bit at least).
### Arguments

- *int* **mask** - The integer, each bit of which is used to set a mask.

## int getReflectionViewportMask () const

Returns the current bit mask for rendering reflections into the camera viewport. Reflections are rendered in the camera viewport if masks of reflective materials match this one (one bit at least).
### Return value

Current integer, each bit of which is used to set a mask.
## void setViewportMask ( int mask )

Sets a new bit mask for rendering into the viewport. Object surfaces, materials, decals, lights and GUI objects will be rendered into the viewport only if their viewport mask matches the camera's one (one matching bit is enough).
### Arguments

- *int* **mask** - The integer, each bit of which is used to set a mask.

## int getViewportMask () const

Returns the current bit mask for rendering into the viewport. Object surfaces, materials, decals, lights and GUI objects will be rendered into the viewport only if their viewport mask matches the camera's one (one matching bit is enough).
### Return value

Current integer, each bit of which is used to set a mask.
## void setObliqueFrustum ( int frustum )

Sets a new value indicating if the viewing frustum is oblique.
> **Notice:** It is recommended to set oblique viewing frustum using this method, as it doesn't affect the projection matrix. To specify the near clipping plane use the *[setObliqueFrustumPlane()](#setObliqueFrustumPlane_Vec4_void)* method.


### Arguments

- *int* **frustum** - The oblique viewing frustum

## int isObliqueFrustum () const

Returns the current value indicating if the viewing frustum is oblique.
> **Notice:** It is recommended to set oblique viewing frustum using this method, as it doesn't affect the projection matrix. To specify the near clipping plane use the *[setObliqueFrustumPlane()](#setObliqueFrustumPlane_Vec4_void)* method.


### Return value

Current oblique viewing frustum
## void setObliqueFrustumPlane ( Vec4 plane )

Sets a new oblique near clipping plane of the viewing frustum.
> **Notice:** This method does not affect the projection matrix. To enable the oblique frustum use the *[setObliqueFrustum()](#setObliqueFrustum_int_void)* method.


```cpp
/* .. */

int update() {

	float time = engine.game.getTime();

	// initializing a plane to be set as a near clipping plane
	Vec4 plane = Vec4(1.0f, 1.0f, 1.0f, 1.0f + sin(time) * 4.0f);

	// getting a player and a camera
	Player player = engine.game.getPlayer();
	Camera camera = player.getCamera();
	if (camera != NULL)
	{
		// enabling oblique frustum
		camera.setObliqueFrustum(1);

		// setting our plane as an oblique near clipping plane
		camera.setObliqueFrustumPlane(plane);
	}
	player.setCamera(camera);

	return 1;
}

/* .. */

```


### Arguments

- *Vec4* **plane** - The world coordinates of the oblique near clipping plane (Nx, Ny, Nz, D), where Nx, Ny, Nz - coordinates of the plane normal, D - distance from the origin to the plane.

## Vec4 getObliqueFrustumPlane () const

Returns the current oblique near clipping plane of the viewing frustum.
> **Notice:** This method does not affect the projection matrix. To enable the oblique frustum use the *[setObliqueFrustum()](#setObliqueFrustum_int_void)* method.


```cpp
/* .. */

int update() {

	float time = engine.game.getTime();

	// initializing a plane to be set as a near clipping plane
	Vec4 plane = Vec4(1.0f, 1.0f, 1.0f, 1.0f + sin(time) * 4.0f);

	// getting a player and a camera
	Player player = engine.game.getPlayer();
	Camera camera = player.getCamera();
	if (camera != NULL)
	{
		// enabling oblique frustum
		camera.setObliqueFrustum(1);

		// setting our plane as an oblique near clipping plane
		camera.setObliqueFrustumPlane(plane);
	}
	player.setCamera(camera);

	return 1;
}

/* .. */

```


### Return value

Current world coordinates of the oblique near clipping plane (Nx, Ny, Nz, D), where Nx, Ny, Nz - coordinates of the plane normal, D - distance from the origin to the plane.
## void setUp ( vec3 up )

Sets a new up direction of the camera's viewport (i.e. tilt of the camera's viewport).
### Arguments

- *vec3* **up** - The upward direction vector. The vector is normalized to 1.

## vec3 getUp () const

Returns the current up direction of the camera's viewport (i.e. tilt of the camera's viewport).
### Return value

Current upward direction vector. The vector is normalized to 1.
## void setZFar ( float zfar )

Sets a new distance to the far clipping plane of the camera's viewing frustum. Changing the value updates the projection matrix.
### Arguments

- *float* **zfar** - The distance in units. If a negative value is provided, 0 will be used instead.

## float getZFar () const

Returns the current distance to the far clipping plane of the camera's viewing frustum. Changing the value updates the projection matrix.
### Return value

Current distance in units. If a negative value is provided, 0 will be used instead.
## void setZNear ( float znear )

Sets a new distance to the near clipping plane of the camera's viewing frustum. Changing the value updates the projection matrix.
### Arguments

- *float* **znear** - The distance in units. If a negative value is provided, 0 will be used instead.

## float getZNear () const

Returns the current distance to the near clipping plane of the camera's viewing frustum. Changing the value updates the projection matrix.
### Return value

Current distance in units. If a negative value is provided, 0 will be used instead.
## void setFocalLength ( float length )

Sets a new focal length of the physically-based camera lens.
### Arguments

- *float* **length** - The camera lens focal length.

## float getFocalLength () const

Returns the current focal length of the physically-based camera lens.
### Return value

Current camera lens focal length.
## void setFilmGate ( float gate )

Sets a new film gate for the physically-based camera with horizontal fov.
### Arguments

- *float* **gate** - The film gate.

## float getFilmGate () const

Returns the current film gate for the physically-based camera with horizontal fov.
### Return value

Current film gate.
## void setFov ( float fov )

Sets a new vertical field of view of the camera.
> **Notice:** Horizontal FOV cannot be used since it varies depending on the viewport's aspect ratio. Setting FOV recalculates projection matrix with **aspect ratio = 1**.


You can use the following formula to calculate horizontal FOV from the vertical one for the given aspect ratio (width/height): **FOV_h = 2 � atan ( (width / height) � tan(FOV_v / 2))**.


### Arguments

- *float* **fov** - The vertical field of view in degrees. The provided value will be saturated in the range [0;180].

## float getFov () const

Returns the current vertical field of view of the camera.
> **Notice:** Horizontal FOV cannot be used since it varies depending on the viewport's aspect ratio. Setting FOV recalculates projection matrix with **aspect ratio = 1**.


You can use the following formula to calculate horizontal FOV from the vertical one for the given aspect ratio (width/height): **FOV_h = 2 � atan ( (width / height) � tan(FOV_v / 2))**.


### Return value

Current vertical field of view in degrees. The provided value will be saturated in the range [0;180].
## int getFovFixed () const

Returns the current value indicating which fov component (horizontal or vertical) is currently fixed.
### Return value

Current fixed FOV component, one of the *[CAMERA_FOV_FIXED_*](#FOV_FIXED_HORIZONTAL)* values.
## void setFovMode ( int mode )

Sets a new value indicating the type of FOV that is used for the camera:
- For the classic camera, the vertical FOV should be set. In this case, FOV is directly set in [degrees](#setFov_float_void).
- For the physically-based camera, the horizontal FOV should be set. In this case, FOV is calculated depending on the [film gate](#setFilmGate_float_void) and [focal length](#setFocalLength_float_void) of the camera.


### Arguments

- *int* **mode** - The value indicating the type of FOV that is used for the camera. 0 if the camera with the vertical FOV is used; 1 if the physically-based camera with the horizontal FOV is used.

## int getFovMode () const

Returns the current value indicating the type of FOV that is used for the camera:
- For the classic camera, the vertical FOV should be set. In this case, FOV is directly set in [degrees](#setFov_float_void).
- For the physically-based camera, the horizontal FOV should be set. In this case, FOV is calculated depending on the [film gate](#setFilmGate_float_void) and [focal length](#setFocalLength_float_void) of the camera.


### Return value

Current value indicating the type of FOV that is used for the camera. 0 if the camera with the vertical FOV is used; 1 if the physically-based camera with the horizontal FOV is used.
## void setProjection ( mat4 projection )

Sets a new projection matrix with unit (1.0) aspect ratio.
> **Notice:** It is not recommended to use this method for setting obliqueness of the near clipping plane of the frustum, as in this case a number of features (such as clouds, shadows, TAA, a number of engine optimizations, etc.) will not function properly. Please, use the [setObliqueFrustum()](#setObliqueFrustum_int_void) method instead.


This method allows you to set your camera to use [perspective](../../../principles/world_management/index.md#camera_perspective) or [orthographic](../../../principles/world_management/index.md#camera_orthographic) projection, depending on your project's requirements.


For example, you can use the following code to set up **orthographic projection** or **perspective projection** for your camera depending on a flag value:


```cpp
// world.usc

Camera camera;
Player player;
/* ... */

// ortho flag - change this value to switch projection type
int ortho_flag = 0;

int init(){
	/* ... */

	// getting the camera of the current player
	camera = engine.game.getPlayer().getCamera();

	// setting up near and far clipping planes and aspect ratio
	float znear = 0.001f;
	float zfar = 10000.0f;
	float aspect = 16.0f / 9.0f;

	if (ortho_flag)
	{
		// setting up orthographic projection
		camera.setProjection(ortho(-1.0f, 1.0f, -1.0f, 1.0f, znear, zfar));
	}
	else
	{
		// setting up perspective projection
		camera.setProjection(perspective(60.0f, aspect, znear, zfar));
	}
	// setting player's camera
	player = engine.game.getPlayer();
	player.setCamera(camera);

	return 1;
}

```


### Arguments

- *mat4* **projection** - The projection matrix.

## mat4 getProjection () const

Returns the current projection matrix with unit (1.0) aspect ratio.
> **Notice:** It is not recommended to use this method for setting obliqueness of the near clipping plane of the frustum, as in this case a number of features (such as clouds, shadows, TAA, a number of engine optimizations, etc.) will not function properly. Please, use the [setObliqueFrustum()](#setObliqueFrustum_int_void) method instead.


This method allows you to set your camera to use [perspective](../../../principles/world_management/index.md#camera_perspective) or [orthographic](../../../principles/world_management/index.md#camera_orthographic) projection, depending on your project's requirements.


For example, you can use the following code to set up **orthographic projection** or **perspective projection** for your camera depending on a flag value:


```cpp
// world.usc

Camera camera;
Player player;
/* ... */

// ortho flag - change this value to switch projection type
int ortho_flag = 0;

int init(){
	/* ... */

	// getting the camera of the current player
	camera = engine.game.getPlayer().getCamera();

	// setting up near and far clipping planes and aspect ratio
	float znear = 0.001f;
	float zfar = 10000.0f;
	float aspect = 16.0f / 9.0f;

	if (ortho_flag)
	{
		// setting up orthographic projection
		camera.setProjection(ortho(-1.0f, 1.0f, -1.0f, 1.0f, znear, zfar));
	}
	else
	{
		// setting up perspective projection
		camera.setProjection(perspective(60.0f, aspect, znear, zfar));
	}
	// setting player's camera
	player = engine.game.getPlayer();
	player.setCamera(camera);

	return 1;
}

```


### Return value

Current projection matrix.
## void setOffset ( mat4 offset )

Sets a new additional transformation (an offset matrix) set for the camera. This transformation is applied after modelview transformation. The offset matrix does not affect the view matrix or the position of the camera. For example, it can be used to simulate camera shake from an explosion.
### Arguments

- *mat4* **offset** - The offset matrix.

## mat4 getOffset () const

Returns the current additional transformation (an offset matrix) set for the camera. This transformation is applied after modelview transformation. The offset matrix does not affect the view matrix or the position of the camera. For example, it can be used to simulate camera shake from an explosion.
### Return value

Current offset matrix.
## void setPosition ( Vec3 position )

Sets a new position of the camera. The position vector is stored in the 3rd column of the view matrix (modelview and inverse modelview).
### Arguments

- *Vec3* **position** - The camera position in the world space.

## Vec3 getPosition () const

Returns the current position of the camera. The position vector is stored in the 3rd column of the view matrix (modelview and inverse modelview).
### Return value

Current camera position in the world space.
## Mat4 getIModelview () const

inverted view matrix of the camera.
### Return value

Inverted view matrix.
## void setModelview ( Mat4 modelview )

Sets a new view matrix of the camera.
### Arguments

- *Mat4* **modelview** - The view matrix.

## Mat4 getModelview () const

Returns the current view matrix of the camera.
### Return value

Current view matrix.
## void setOrthoHeight ( float height )

Sets a new height of the camera with the orthographic [projection mode](#getProjectionMode_int) enabled.
### Arguments

- *float* **height** - The orthographic camera height.

## float getOrthoHeight () const

Returns the current height of the camera with the orthographic [projection mode](#getProjectionMode_int) enabled.
### Return value

Current orthographic camera height.
## void setProjectionMode ( int mode )

Sets a new projection mode: orthographic or perspective.
### Arguments

- *int* **mode** - The projection mode, 1 for the orthographic mode; 0 for the perspective mode.

## int getProjectionMode () const

Returns the current projection mode: orthographic or perspective.
### Return value

Current projection mode, 1 for the orthographic mode; 0 for the perspective mode.
---

## static Camera ( )

Constructor. Creates a new camera with default settings:
- [Modelview](#setModelview_Mat4_void), [inverse modelview](#getIModelview_Mat4) and [offset matrices](#setOffset_mat4_void) are 4�4 identity matrices.
- FOV is 60 degrees.
- [Distance to the near clipping plane](#setZNear_float_void) is 0.1 unit.
- [Distance to the far clipping plane](#setZFar_float_void) is 10000 units.
- [Up direction vector](#setUp_vec3_void) is (0,0,1).
- Viewport, reflection, source and reverb masks are set to 00000001.


## Camera clone ( )

Clones the current camera and saves it to the given camera instance.
### Return value

Copy of the camera.
## mat4 getAspectCorrectedProjection ( float aspect )

Returns projection matrix after correction for the specified aspect ratio. [Currently fixed FOV component](#getFovFixed_int) is taken into account.
### Arguments

- *float* **aspect** - Aspect ratio.

### Return value

Projection matrix after correction for the specified aspect ratio.
## void addScriptableMaterial ( Material material )

Attaches a new [scriptable material](../../../content/materials/scriptable.md) to the camera.
To apply a scriptable material globally, use the *[addScriptableMaterial()()](../../../api/library/rendering/class.render_usc.md#addScriptableMaterial_Material_void)* method of the *Render* class. The order of execution for scripts assigned to scriptable materials is defined by material's number in the list of the camera.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_usc.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-camera.


### Arguments

- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - Scriptable material to be attached to the camera.

## void insertScriptableMaterial ( int num , Material material )

Inserts a new [scriptable material](../../../content/materials/scriptable.md) into the list of the ones assigned to the camera.
To apply a scriptable material globally, use the [*insertScriptableMaterial()*](../../../api/library/rendering/class.render_usc.md#insertScriptableMaterial_int_Material_void) method of the *Render* class. The order of execution for scripts assigned to scriptable materials is defined by material's number in the camera's list.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_usc.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-camera.


### Arguments

- *int* **num** - Position at which a new scriptable material is to be inserted.
- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - Scriptable material to be inserted.

## void removeScriptableMaterial ( int num )

Removes the [scriptable material](../../../content/materials/scriptable.md) with the specified number from the camera.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

## int findScriptableMaterial ( Material material )

 Returns the number of the specified [scriptable material](../../../content/materials/scriptable.md) for the camera.
This number is camera-specific (valid for this camera only) and determines the order in which the assigned expressions are executed.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_usc.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-camera.


### Arguments

- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - Scriptable material for which a number is to be found.

### Return value

Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int), or -1 if the specified material was not found.
## void setScriptableMaterial ( int num , Material material )

Replaces the [scriptable material](../../../content/materials/scriptable.md) with the specified number with the new scriptable material specified.
The number of material determines the order in which the expressions assigned to it are executed. This number is camera-specific (valid for this camera only).


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_usc.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-camera.


### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - New scriptable material to replace the one with the specified number.

## Material getScriptableMaterial ( int num )

Returns a [scriptable material](../../../content/materials/scriptable.md) attached to the camera by its number.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

### Return value

Scriptable material attached to the camera with the specified number.
## void setScriptableMaterialEnabled ( int num , int enabled )

Enables or disables the [scriptable material](../../../content/materials/scriptable.md) with the specified number. When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *int* **enabled** - **1** to enable the scriptable material with the specified number, **0** to disable it.

## int getScriptableMaterialEnabled ( int num )

Returns a value indicating if the [scriptable material](../../../content/materials/scriptable.md) with the specified number attached to the camera is enabled (active). When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

### Return value

**1** if the scriptable material with the specified number is enabled; otherwise, **0**.
## void swapScriptableMaterials ( int num_0 , int num_1 )

Swaps two [scriptable materials](../../../content/materials/scriptable.md) with specified numbers.
The number of material determines the order in which the expressions assigned to it are executed.


> **Notice:** The number is camera-specific (valid for this camera only).


### Arguments

- *int* **num_0** - Number of the first scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *int* **num_1** - Number of the second scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

## void clearScriptableMaterials ( )

Clears all [scriptable materials](../../../content/materials/scriptable.md) attached to the camera.
## Camera copy ( Camera camera )

Copies the parameters from the source camera to this camera instance.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera**

### Return value

## void swap ( Camera camera )

Swaps the parameters between the specified camera and this camera instance.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera**
