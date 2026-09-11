# Unigine.Camera Class (CPP)

**Header:** #include <UnigineCamera.h>


The **Camera** class is used to create a new camera, set it up (set all the required matrices, field of view, masks and so on) and then pass it to an instance of the [Viewport](../../../api/library/rendering/class.viewport_cpp.md) class to render an image from this camera.


> **Notice:** An instance of this class is **not a node**.


A camera instance can have the following masks:


- Sound Source mask
- Sound Reverberation mask
- Viewport mask
- Reflection Viewport mask


Camera settings can be set up in the [Camera Settings in UnigineEditor](../../../editor2/camera_settings/index.md).


### Usage Example


In this example we create a Camera instance and [PlayerSpectator](../../../objects/players/spectator/index.md) player, specify camera parameters, set camera to the PlayerSpectator and set it as current game player.


In the `AppWorldLogic.h` header file include the `UniginePlayers.h` header and declare a [PlayerSpectator](../../../api/library/players/class.playerspectator_cpp.md) and Camera smart pointers.


```cpp
#include <UnigineLogic.h>
#include <UnigineStreams.h>
#include <UniginePlayers.h>

class AppWorldLogic : public Unigine::WorldLogic {

public:

	/* public methods */

private:
	Unigine::PlayerSpectatorPtr playerSpectator;
	Unigine::CameraPtr camera;
};

```


In the `AppWorldLogic.cpp` implementation file do the following:


- Include the `UnigineGame.h` header to set a new player by using *[setPlayer()](../../../api/library/engine/class.game_cpp.md#setPlayer_Player_void)* method.
- Use **using namespace Unigine** directive: names of the Unigine namespace will be injected into global namespace.
- Specify the necessary parameters of the created *Camera* instance and set it to *PlayerSpectator*.
- Set PlayerSpectator as a current game player.
- Clear the pointer to the PlayerSpectator to avoid memory leaks.


Here are the necessary parts of code:


```cpp
#include "AppWorldLogic.h"
#include "UnigineGame.h"

// inject Unigine namespace names to global namespace
using namespace Unigine;

/* ... */

int AppWorldLogic::init() {

	// create a new PlayerSpectator and camera instance
	playerSpectator = PlayerSpectator::create();
	camera = Camera::create();

	// specify the necessary camera parameters: FOV, ZNear, ZFar.
	// add the post_sensor_red post-effect to camera
	camera->setFov(110.0f);
	camera->setZNear(0.1f);
	camera->setZFar(10000.0f);

	// set camera to the player
	playerSpectator->setCamera(camera);

	// specify the position and view direction of playerSpectator
	playerSpectator->setViewDirection(Math::vec3(0.0f, 1.0f, 0.0f));
	playerSpectator->setWorldPosition(Math::dvec3(-1.6f, -1.7f, 1.7f));

	// set the Player to the Game singleton instance
	Game::setPlayer(playerSpectator);

	return 1;
}

/* ... */

int AppWorldLogic::shutdown() {

	// clear the pointer to Player
	playerSpectator.clear();

	return 1;
}

```


## Camera Class

### Enums

## PROJECTION_MODE

| Name | Description |
|---|---|
| **PROJECTION_MODE_PERSPECTIVE** = 0 | Perspective projection. |
| **PROJECTION_MODE_ORTHOGRAPHIC** = 1 | Orthographic projection. |

## FOV_FIXED

| Name | Description |
|---|---|
| **FOV_FIXED_VERTICAL** = 0 | Vertical FOV component is fixed. |
| **FOV_FIXED_HORIZONTAL** = 1 | Horizontal FOV component is fixed. |

## FOV_MODE

| Name | Description |
|---|---|
| **FOV_MODE_VERTICAL** = 0 | Vertical FOV mode. Vertical FOV of the camera is determined by the [FOV](#setFov_float_void) value. |
| **FOV_MODE_PHYSICALLY_BASED_CAMERA** = 1 | Physically based mode. Horizontal FOV of the physically-based camera is calculated using the [focal length](#setFocalLength_float_void) and [film gate](#setFilmGate_float_void) values according to the following formula: **FOV_h = 2 * atan(film_gate / (2 * focal_length)) * Consts::RAD2DEG** |

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
## void setObliqueFrustum ( bool frustum )

Sets a new value indicating if the viewing frustum is oblique.
> **Notice:** It is recommended to set oblique viewing frustum using this method, as it doesn't affect the projection matrix. To specify the near clipping plane use the *[setObliqueFrustumPlane()](#setObliqueFrustumPlane_Vec4_void)* method.


### Arguments

- *bool* **frustum** - Set **true** to enable oblique viewing frustum; **false** - to disable it.

## bool isObliqueFrustum () const

Returns the current value indicating if the viewing frustum is oblique.
> **Notice:** It is recommended to set oblique viewing frustum using this method, as it doesn't affect the projection matrix. To specify the near clipping plane use the *[setObliqueFrustumPlane()](#setObliqueFrustumPlane_Vec4_void)* method.


### Return value

**true** if oblique viewing frustum is enabled ; otherwise **false**.
## void setObliqueFrustumPlane ( const Math:: Vec4 & plane )

Sets a new oblique near clipping plane of the viewing frustum.
> **Notice:** This method does not affect the projection matrix. To enable the oblique frustum use the *[setObliqueFrustum()](#setObliqueFrustum_int_void)* method.


```cpp
// AppWorldLogic.cpp
#include <UnigineGame.h>
using namespace Unigine;

/* .. */

int AppWorldLogic::update() {
	// Write here code to be called before updating each render frame: specify all graphics-related functions you want to be called every frame while your application executes.
	float time = Game::getTime();

	// initializing a plane to be set as a near clipping plane
	Math::Vec4 plane = Math::Vec4(1.0f, 1.0f, 1.0f, 1.0f + Math::sin(time) * 4.0f);

	// getting a camera
	CameraPtr camera = Game::getPlayer()->getCamera();
	if (camera)
	{
		// enabling oblique frustum
		camera->setObliqueFrustum(1);

		// setting our plane as an oblique near clipping plane
		camera->setObliqueFrustumPlane(plane);
	}

	return 1;
}

/* .. */

```


### Arguments

- *const  Math::[Vec4](../../../api/library/math/class.vec4_cpp.md)&* **plane** - The world coordinates of the oblique near clipping plane (Nx, Ny, Nz, D), where Nx, Ny, Nz - coordinates of the plane normal, D - distance from the origin to the plane.

## Math:: Vec4 getObliqueFrustumPlane () const

Returns the current oblique near clipping plane of the viewing frustum.
> **Notice:** This method does not affect the projection matrix. To enable the oblique frustum use the *[setObliqueFrustum()](#setObliqueFrustum_int_void)* method.


```cpp
// AppWorldLogic.cpp
#include <UnigineGame.h>
using namespace Unigine;

/* .. */

int AppWorldLogic::update() {
	// Write here code to be called before updating each render frame: specify all graphics-related functions you want to be called every frame while your application executes.
	float time = Game::getTime();

	// initializing a plane to be set as a near clipping plane
	Math::Vec4 plane = Math::Vec4(1.0f, 1.0f, 1.0f, 1.0f + Math::sin(time) * 4.0f);

	// getting a camera
	CameraPtr camera = Game::getPlayer()->getCamera();
	if (camera)
	{
		// enabling oblique frustum
		camera->setObliqueFrustum(1);

		// setting our plane as an oblique near clipping plane
		camera->setObliqueFrustumPlane(plane);
	}

	return 1;
}

/* .. */

```


### Return value

Current world coordinates of the oblique near clipping plane (Nx, Ny, Nz, D), where Nx, Ny, Nz - coordinates of the plane normal, D - distance from the origin to the plane.
## void setUp ( const Math:: vec3 & up )

Sets a new up direction of the camera's viewport (i.e. tilt of the camera's viewport).
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **up** - The upward direction vector. The vector is normalized to 1.

## Math:: vec3 getUp () const

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
## Camera::FOV_FIXED getFovFixed () const

Returns the current value indicating which fov component (horizontal or vertical) is currently fixed.
### Return value

Current fixed FOV component, one of the *[FOV_FIXED_*](#FOV_FIXED_HORIZONTAL)* values.
## void setFovMode ( Camera::FOV_MODE mode )

Sets a new value indicating the type of FOV that is used for the camera:
- For the classic camera, the vertical FOV should be set. In this case, FOV is directly set in [degrees](#setFov_float_void).
- For the physically-based camera, the horizontal FOV should be set. In this case, FOV is calculated depending on the [film gate](#setFilmGate_float_void) and [focal length](#setFocalLength_float_void) of the camera.


### Arguments

- *[Camera::FOV_MODE](../../../api/library/rendering/class.camera_cpp.md#FOV_MODE)* **mode** - The value indicating the type of FOV that is used for the camera. 0 if the camera with the vertical FOV is used; 1 if the physically-based camera with the horizontal FOV is used.

## Camera::FOV_MODE getFovMode () const

Returns the current value indicating the type of FOV that is used for the camera:
- For the classic camera, the vertical FOV should be set. In this case, FOV is directly set in [degrees](#setFov_float_void).
- For the physically-based camera, the horizontal FOV should be set. In this case, FOV is calculated depending on the [film gate](#setFilmGate_float_void) and [focal length](#setFocalLength_float_void) of the camera.


### Return value

Current value indicating the type of FOV that is used for the camera. 0 if the camera with the vertical FOV is used; 1 if the physically-based camera with the horizontal FOV is used.
## void setProjection ( const Math:: mat4 & projection )

Sets a new projection matrix with unit (1.0) aspect ratio.
> **Notice:** It is not recommended to use this method for setting obliqueness of the near clipping plane of the frustum, as in this case a number of features (such as clouds, shadows, TAA, a number of engine optimizations, etc.) will not function properly. Please, use the [setObliqueFrustum()](#setObliqueFrustum_int_void) method instead.


This method allows you to set your camera to use [perspective](../../../principles/world_management/index.md#camera_perspective) or [orthographic](../../../principles/world_management/index.md#camera_orthographic) projection, depending on your project's requirements.


For example, you can use the following code to set up **orthographic projection** or **perspective projection** for your camera depending on a flag value:


```cpp
// AppWorldLogic.cpp

/* ... */
#include <UnigineCamera.h>
#include <UnigineGame.h>

// inject Unigine namespace names to global namespace
using namespace Unigine;

/* ... */

// ortho flag - change this value to switch projection type
int ortho = 0;

int AppWorldLogic::init() {

	// getting the camera of the current player
	CameraPtr camera = Game::getPlayer()->getCamera();

	// setting up near and far clipping planes and aspect ratio
	float znear = 0.001f;
	float zfar = 10000.0f;
	float aspect = 16.0f / 9.0f;

	if (ortho)
	{
		// setting up orthographic projection
		camera->setProjection(Math::ortho(-1.0f, 1.0f, -1.0f, 1.0f, znear, zfar));
	}
	else
	{
		// setting up perspective projection
		camera->setProjection(Math::perspective(60.0f, aspect, znear, zfar));
	}

	// setting player's camera
	Game::getPlayer()->setCamera(camera);

	return 1;
}

/* ... */

```


### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md)&* **projection** - The projection matrix.

## Math:: mat4 getProjection () const

Returns the current projection matrix with unit (1.0) aspect ratio.
> **Notice:** It is not recommended to use this method for setting obliqueness of the near clipping plane of the frustum, as in this case a number of features (such as clouds, shadows, TAA, a number of engine optimizations, etc.) will not function properly. Please, use the [setObliqueFrustum()](#setObliqueFrustum_int_void) method instead.


This method allows you to set your camera to use [perspective](../../../principles/world_management/index.md#camera_perspective) or [orthographic](../../../principles/world_management/index.md#camera_orthographic) projection, depending on your project's requirements.


For example, you can use the following code to set up **orthographic projection** or **perspective projection** for your camera depending on a flag value:


```cpp
// AppWorldLogic.cpp

/* ... */
#include <UnigineCamera.h>
#include <UnigineGame.h>

// inject Unigine namespace names to global namespace
using namespace Unigine;

/* ... */

// ortho flag - change this value to switch projection type
int ortho = 0;

int AppWorldLogic::init() {

	// getting the camera of the current player
	CameraPtr camera = Game::getPlayer()->getCamera();

	// setting up near and far clipping planes and aspect ratio
	float znear = 0.001f;
	float zfar = 10000.0f;
	float aspect = 16.0f / 9.0f;

	if (ortho)
	{
		// setting up orthographic projection
		camera->setProjection(Math::ortho(-1.0f, 1.0f, -1.0f, 1.0f, znear, zfar));
	}
	else
	{
		// setting up perspective projection
		camera->setProjection(Math::perspective(60.0f, aspect, znear, zfar));
	}

	// setting player's camera
	Game::getPlayer()->setCamera(camera);

	return 1;
}

/* ... */

```


### Return value

Current projection matrix.
## void setOffset ( const Math:: mat4 & offset )

Sets a new additional transformation (an offset matrix) set for the camera. This transformation is applied after modelview transformation. The offset matrix does not affect the view matrix or the position of the camera. For example, it can be used to simulate camera shake from an explosion.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md)&* **offset** - The offset matrix.

## Math:: mat4 getOffset () const

Returns the current additional transformation (an offset matrix) set for the camera. This transformation is applied after modelview transformation. The offset matrix does not affect the view matrix or the position of the camera. For example, it can be used to simulate camera shake from an explosion.
### Return value

Current offset matrix.
## void setPosition ( const Math:: Vec3 & position )

Sets a new position of the camera. The position vector is stored in the 3rd column of the view matrix (modelview and inverse modelview).
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md)&* **position** - The camera position in the world space.

## Math:: Vec3 getPosition () const

Returns the current position of the camera. The position vector is stored in the 3rd column of the view matrix (modelview and inverse modelview).
### Return value

Current camera position in the world space.
## Math:: Mat4 getIModelview () const

inverted view matrix of the camera.
### Return value

Inverted view matrix.
## void setModelview ( const Math:: Mat4 & modelview )

Sets a new view matrix of the camera.
### Arguments

- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md)&* **modelview** - The view matrix.

## Math:: Mat4 getModelview () const

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
## void setProjectionMode ( Camera::PROJECTION_MODE mode )

Sets a new projection mode: orthographic or perspective.
### Arguments

- *[Camera::PROJECTION_MODE](../../../api/library/rendering/class.camera_cpp.md#PROJECTION_MODE)* **mode** - The projection mode, *[PROJECTION_MODE_ORTHOGRAPHIC](#PROJECTION_MODE_ORTHOGRAPHIC)* for the orthographic mode; *[PROJECTION_MODE_PERSPECTIVE](#PROJECTION_MODE_PERSPECTIVE)* for the perspective mode.

## Camera::PROJECTION_MODE getProjectionMode () const

Returns the current projection mode: orthographic or perspective.
### Return value

Current projection mode, *[PROJECTION_MODE_ORTHOGRAPHIC](#PROJECTION_MODE_ORTHOGRAPHIC)* for the orthographic mode; *[PROJECTION_MODE_PERSPECTIVE](#PROJECTION_MODE_PERSPECTIVE)* for the perspective mode.
---

## static CameraPtr create ( )

Constructor. Creates a new camera with default settings:
- [Modelview](#setModelview_Mat4_void), [inverse modelview](#getIModelview_Mat4) and [offset matrices](#setOffset_mat4_void) are 4�4 identity matrices.
- FOV is 60 degrees.
- [Distance to the near clipping plane](#setZNear_float_void) is 0.1 unit.
- [Distance to the far clipping plane](#setZFar_float_void) is 10000 units.
- [Up direction vector](#setUp_vec3_void) is (0,0,1).
- Viewport, reflection, source and reverb masks are set to 00000001.


## void getDirectionFromScreen ( Math:: Vec3 & p0 , Math:: Vec3 & p1 , float screen_x , float screen_y , float aspect ) const

Casts the ray from a certain position on the screen.
### Arguments

- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start coordinate of the ray.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End coordinate of the ray.
- *float* **screen_x** - X-coordinate of screen, in the [0;1] range, where 0 is the left upper point, 1 is the right lower point.
- *float* **screen_y** - Y-coordinate of screen, in the [0;1] range, where 0 is the left upper point, 1 is the right lower point.
- *float* **aspect** - Screen's aspect ratio (height to width).

## Math:: vec3 getDirectionFromScreen ( float screen_x , float screen_y , float aspect ) const

Casts the ray from a certain position on the screen.
### Arguments

- *float* **screen_x** - X-coordinate of screen, in the [0;1] range, where 0 is the left upper point, 1 is the right lower point.
- *float* **screen_y** - Y-coordinate of screen, in the [0;1] range, where 0 is the left upper point, 1 is the right lower point.
- *float* **aspect** - Screen's aspect ratio (height to width).

### Return value

Point coordinate.
## Math:: mat4 getProjectionFromScreen ( float screen_x0 , float screen_y0 , float screen_x1 , float screen_y1 , float aspect ) const

Creates a projection matrix out of 2 screen positions. This is required for the frame selection.
### Arguments

- *float* **screen_x0** - X-coordinate of the first screen position, in the [0;1] range, where 0 is the left upper point, 1 is the right lower point.
- *float* **screen_y0** - Y-coordinate of the first screen position, in the [0;1] range, where 0 is the left upper point, 1 is the right lower point.
- *float* **screen_x1** - X-coordinate of the second screen position, in the [0;1] range, where 0 is the left upper point, 1 is the right lower point.
- *float* **screen_y1** - Y-coordinate of the second screen position, in the [0;1] range, where 0 is the left upper point, 1 is the right lower point.
- *float* **aspect** - Screen's aspect ratio (height to width).

### Return value

Projection matrix.
## int getScreenPosition ( float & screen_x , float & screen_y , const Math:: Vec3 & point , float aspect ) const

Projects the point in world coordinates to the screen. Screen coordinates are written into the first 2 variables passed to the method.
### Arguments

- *float &* **screen_x** - X-coordinate of the screen position.
- *float &* **screen_y** - Y-coordinate of the screen position.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point coordinates.
- *float* **aspect** - Aspect ratio (screen height to width).

### Return value

**1** if the point has been projected successfully; otherwise, **0**.
## Ptr < Camera > clone ( ) const

Clones the current camera and saves it to the given camera instance.
### Return value

Copy of the camera.
## Math:: mat4 getAspectCorrectedProjection ( float aspect ) const

Returns projection matrix after correction for the specified aspect ratio. [Currently fixed FOV component](#getFovFixed_int) is taken into account.
### Arguments

- *float* **aspect** - Aspect ratio.

### Return value

Projection matrix after correction for the specified aspect ratio.
## void addScriptableMaterial ( const Ptr < Material > & material )

Attaches a new [scriptable material](../../../content/materials/scriptable.md) to the camera.
To apply a scriptable material globally, use the *[addScriptableMaterial()](../../../api/library/rendering/class.render_cpp.md#addScriptableMaterial_Material_void)* method of the *Render* class. The order of execution for scripts assigned to scriptable materials is defined by material's number in the list of the camera.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cpp.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-camera.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Scriptable material to be attached to the camera.

## void insertScriptableMaterial ( int num , const Ptr < Material > & material )

Inserts a new [scriptable material](../../../content/materials/scriptable.md) into the list of the ones assigned to the camera.
To apply a scriptable material globally, use the [*insertScriptableMaterial()*](../../../api/library/rendering/class.render_cpp.md#insertScriptableMaterial_int_Material_void) method of the *Render* class. The order of execution for scripts assigned to scriptable materials is defined by material's number in the camera's list.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cpp.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-camera.


### Arguments

- *int* **num** - Position at which a new scriptable material is to be inserted.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Scriptable material to be inserted.

## void removeScriptableMaterial ( int num )

Removes the [scriptable material](../../../content/materials/scriptable.md) with the specified number from the camera.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

## int findScriptableMaterial ( const Ptr < Material > & material ) const

 Returns the number of the specified [scriptable material](../../../content/materials/scriptable.md) for the camera.
This number is camera-specific (valid for this camera only) and determines the order in which the assigned expressions are executed.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cpp.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-camera.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Scriptable material for which a number is to be found.

### Return value

Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int), or -1 if the specified material was not found.
## void setScriptableMaterial ( int num , const Ptr < Material > & material )

Replaces the [scriptable material](../../../content/materials/scriptable.md) with the specified number with the new scriptable material specified.
The number of material determines the order in which the expressions assigned to it are executed. This number is camera-specific (valid for this camera only).


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cpp.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-camera.


### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - New scriptable material to replace the one with the specified number.

## Ptr < Material > getScriptableMaterial ( int num ) const

Returns a [scriptable material](../../../content/materials/scriptable.md) attached to the camera by its number.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

### Return value

Scriptable material attached to the camera with the specified number.
## void setScriptableMaterialEnabled ( int num , bool enabled )

Enables or disables the [scriptable material](../../../content/materials/scriptable.md) with the specified number. When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *bool* **enabled** - true to enable the scriptable material with the specified number, false to disable it.

## bool getScriptableMaterialEnabled ( int num ) const

Returns a value indicating if the [scriptable material](../../../content/materials/scriptable.md) with the specified number attached to the camera is enabled (active). When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

### Return value

true if the scriptable material with the specified number is enabled; otherwise, false.
## void swapScriptableMaterials ( int num_0 , int num_1 )

Swaps two [scriptable materials](../../../content/materials/scriptable.md) with specified numbers.
The number of material determines the order in which the expressions assigned to it are executed.


> **Notice:** The number is camera-specific (valid for this camera only).


### Arguments

- *int* **num_0** - Number of the first scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *int* **num_1** - Number of the second scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

## void clearScriptableMaterials ( )

Clears all [scriptable materials](../../../content/materials/scriptable.md) attached to the camera.
## Ptr < Camera > copy ( const Ptr < Camera > & camera ) const

Copies the parameters from the source camera to this camera instance.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Smart pointer to the source camera.

### Return value

Smart pointer to this camera.
## void swap ( const Ptr < Camera > & camera )

Swaps the parameters between the specified camera and this camera instance.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Camera smart pointer.
