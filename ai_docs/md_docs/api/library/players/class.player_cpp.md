# Unigine.Player Class (CPP)

**Header:** #include <UniginePlayers.h>

**Inherits from:** Node


This class is used to create cameras that view the world. When you create a new player, it creates a [camera](../../../api/library/rendering/class.camera_cpp.md) and specifies controls, [masks](#player_masks), postprocess materials for this camera.


Players' viewing frustum is defined by a [near clipping plane](#setZNear_float_void), [far clipping plane](#setZFar_float_void) and the [field of view](#setFov_float_void). Note that if you set up a custom [projection](#setProjection_mat4_void) matrix and after that call any of these functions:


- [*setFov()*](#setFov_float_void)
- [*setZFar()*](#setZFar_float_void)
- [*setZNear()*](#setZNear_float_void)


your custom matrices will be overwritten.


Players cannot have a parent node; they always use the world coordinates for their transformations. The only exception is [PlayerDummy](../../../api/library/players/class.playerdummy_cpp.md).


### Player Masks


Objects, decals and lights can be selectively displayed in the player viewport. To be displayed, their viewport mask should be matching with the player's [viewport mask](#setViewportMask_int_void) (one matching bit is enough):


- Object [surface viewport mask](../../../api/library/objects/class.object_cpp.md#setViewportMask_int_int_void) or [decal viewport mask](../../../api/library/decals/class.decal_cpp.md#setViewportMask_int_void)
- [Light viewport mask](../../../api/library/lights/class.light_cpp.md#setViewportMask_int_void) to light the object/decal
- [Material viewport mask](../../../api/library/rendering/class.material_cpp.md#setViewportMask_int_void) to render the object/decal material


Reflections can also be selectively rendered into the viewport: an object can be rendered without reflection or reflection without an object. For that, the player's [reflection viewport mask](#setReflectionViewportMask_int_void) should match:


- Reflection mask of the reflecting material
- [Viewport mask](../../../api/library/rendering/class.material_cpp.md#setViewportMask_int_void) of the reflecting material
- Object [surface viewport mask](../../../api/library/objects/class.object_cpp.md#setViewportMask_int_int_void)
- [Material viewport mask](../../../api/library/rendering/class.material_cpp.md#setViewportMask_int_void) of the reflected material
- [Light viewport mask](../../../api/library/lights/class.light_cpp.md#setViewportMask_int_void)


That is enough to render reflection from the object without an object itself. If an object needs to be present as well, all these conditions should simply go together with above mentioned ones.


To render an object without reflection, simply either its [material viewport mask](../../../api/library/rendering/class.material_cpp.md#setViewportMask_int_void) or object [surface viewport mask](../../../api/library/objects/class.object_cpp.md#setViewportMask_int_int_void) should not match the player's [reflection viewport mask](#setReflectionViewportMask_int_void).


Players also can have sound source and sound reverberation masks. As well as for viewports, corresponding masks of the *Player* object should match with [SoundReverb](../../../api/library/sounds/class.soundreverb_cpp.md#setReverbMask_int_void) and [SoundSource](../../../api/library/sounds/class.soundsource_cpp.md#setSourceMask_int_void) masks.


### Perspective and Orthographic Projection


Depending on your project's requirements you can set your player to use [perspective](../../../principles/world_management/index.md#camera_perspective) or [orthographic](../../../principles/world_management/index.md#camera_orthographic) projection. This can be done via the [*setProjection()*](#setProjection_mat4_void) method.


For example, you can use the following code to set up **orthographic projection** or **perspective projection** for your current game player depending on a flag value:


```cpp
#include "AppWorldLogic.h"
#include <UnigineGame.h>
#include <UniginePlayers.h>

using namespace Unigine;
using namespace Math;

/* ... */

// calculates a projection matrix for the specified parameters (angles for left, right, top, and bottom are in degrees)
Unigine::Math::mat4 calculateProjection(double left, double right, double bottom, double top, double zNear, double zFar, double zoom)
{
	left = zNear * Unigine::Math::tan(Unigine::Math::Consts::DEG2RAD*(left * zoom));
	right = zNear * Unigine::Math::tan(Unigine::Math::Consts::DEG2RAD*(right * zoom));
	top = zNear * Unigine::Math::tan(Unigine::Math::Consts::DEG2RAD*(top * zoom));
	bottom = zNear * Unigine::Math::tan(Unigine::Math::Consts::DEG2RAD*(bottom * zoom));

	return Unigine::Math::frustum(static_cast<float>(left), static_cast<float>(right), static_cast<float>(bottom), static_cast<float>(top), static_cast<float>(zNear), static_cast<float>(zFar));
}

	/* ... */

	// ortho flag - change this value to switch projection type
	int ortho_proj = 0;

int AppWorldLogic::init()
{
	// disabling default aspect correction for the main window
	// to ensure that the custom projection is applied properly
	Unigine::WindowManager::getMainWindow()->setAspectCorrection(false);

	// getting the current player
	PlayerPtr player = Game::getPlayer();

	// setting up near and far clipping planes and aspect ratio
	float znear = 0.001f;
	float zfar = 10000.0f;
	float aspect = 16.0f / 9.0f;

	float fov = 60.0f;
	float ortho_height = 2.0f;

	player->setZNear(znear);
	player->setZFar(zfar);
	player->setFov(fov);
	player->setOrthoHeight(ortho_height);

	if (ortho_proj)
	{
		// setting up orthographic projection
		player->setProjectionMode(Camera::PROJECTION_MODE_ORTHOGRAPHIC);

		// or setting up orthographic projection manually
		player->setProjection(Math::ortho(-ortho_height / 2.0f, ortho_height / 2.0f, -ortho_height / 2.0f, ortho_height / 2.0f, znear, zfar));
	}
	else
	{
		// setting up perspective projection
		player->setProjectionMode(Camera::PROJECTION_MODE_PERSPECTIVE);

		// or setting up a projection matrix manually
		player->setProjection(Math::perspective(fov, aspect, znear, zfar));

		// or calculating a projection matrix for FullfHD/4K resolution
		auto projection = calculateProjection(-22.5f, 22.5f, -13.1f, 13.1f, 1.0f, 200000.0f, 1.0f);
		// and setting up custom calculated projection manually
		player->setProjection(projection);
	}

	return 1;
}


```


### Getting Euler Angles for an Active Camera


Sometimes it might be necessary to get current rotation of the active camera as a set of Euler angles. When we talk about axes in UNIGINE we assume that:


|  |  |
|---|---|
| - **X** axis points to the *right* giving us a **pitch** angle. - **Y** axis points *forward* giving us a **roll** angle. - **Z** axis points *up* giving us a **yaw** (heading) angle. | ![](../../../code/fundamentals/matrices/object_directions.png) *Object Direction Vectors* |


To get the Euler angles we should use [*decomposeRotationZXY()*](../../../api/library/math/math.matrix_cpp.md#decomposeRotationZXY_const_mat3_ref_vec3) also known as Cardan angles (**yaw** is independent, then we get **pitch** and in the end, **roll**). But, there is one thing to be taken into account - cameras have a different system:


|  |  |
|---|---|
| - **X** axis points to the *right* giving us a **pitch** angle. - **Y** axis points *up* giving us a **yaw** (heading) angle. - **Z** axis points *backward* giving us a **-roll** angle. | ![](../../../code/fundamentals/matrices/camera_directions.png) *Camera Direction Vectors* |


To compensate it, we need to rotate our camera **-90** degrees around **X** axis.


```cpp
#include "AppWorldLogic.h"
#include <UnigineGame.h>
#include <UniginePlayers.h>

using namespace Unigine;
using namespace Math;

/* ... */

	// getting the current view matrix of the current camera
	Mat4 currentModelview = Game::getPlayer()->getCamera()->getIModelview();

	// decomposing rotation matrix of the camera (with compensation)
	vec3 euler = decomposeRotationZXY(mat3(currentModelview * Mat4(rotateX(-90.0f))));
	euler.x += 90.0f;

	// perform correction for negative angle values
	if (euler.x < 0) euler.x += 360.0f;
	if (euler.y < 0) euler.y += 360.0f;
	if (euler.z < 0) euler.z += 360.0f;

	// Euler angles for the camera
	float pitch = euler.x;
	float roll = euler.y;
	float yaw = euler.z;


```


### Usage Example


In this example we create a [PlayerSpectator](../../../objects/players/spectator/index.md) player, specify its parameters and set it as current game player.


In the `AppWorldLogic.h` header file include the `UniginePlayers.h` header and declare a [PlayerSpectator](../../../api/library/players/class.playerspectator_cpp.md) smart pointer.


```cpp
#include <UnigineLogic.h>
#include <UnigineStreams.h>
#include <UniginePlayers.h>

class AppWorldLogic : public Unigine::WorldLogic
{

public:

	/* public methods */

private:
	Unigine::PlayerSpectatorPtr playerSpectator;

};


```


In the `AppWorldLogic.cpp` implementation file do the following:


- Include the `UnigineGame.h` header to set a new player by using *[setPlayer()](../../../api/library/engine/class.game_cpp.md#setPlayer_Player_void)* method.
- Use **using namespace Unigine** directive: names of the Unigine namespace will be injected into global namespace.
- Specify the necessary parameters of the created *Player* instance.
- Set our recently created *Player* as a current game player.
- Clear the pointer to the *PlayerSpectator* to avoid memory leaks.


Here are the necessary parts of code:


```cpp
#include "AppWorldLogic.h"
#include <UnigineGame.h>
#include <UniginePlayers.h>

using namespace Unigine;
using namespace Math;

/* ... */

int AppWorldLogic::init()
{

	// create a new PlayerSpectator instance
	playerSpectator = PlayerSpectator::create();

	// specify the necessary parameters: FOV, ZNear, ZFar, view direction vector and PlayerSpectator position.
	playerSpectator->setFov(90.0f);
	playerSpectator->setZNear(0.1f);
	playerSpectator->setZFar(10000.0f);
	playerSpectator->setViewDirection(Math::vec3(0.0f, 1.0f, 0.0f));
	playerSpectator->setWorldPosition(Math::Vec3(-1.6f, -1.7f, 1.7f));

	// set the Player to the Game singleton instance
	Game::setPlayer(playerSpectator);

	return 1;
}

int AppWorldLogic::shutdown()
{

	// clear the pointer to Player
	playerSpectator.clear();

	return 1;
}


```


## Player Class

### Members

---

## void setCamera ( const Ptr < Camera > & camera )

Sets given Camera instance to the Player.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Camera](../../../api/library/rendering/class.camera_cpp.md)> &* **camera** - Smart pointer to a Camera to be set.

## Ptr < Camera > getCamera ( ) const

Returns the Camera instance of the Player node.
### Return value

The camera of the player.
## void setControlled ( bool controlled )

Disables or enables the player controls.
### Arguments

- *bool* **controlled** - true to enable player controls, false to disable (player stops responding to them).

## bool isControlled ( ) const

Returns a value indicating whether player controls are disabled (player does not respond to them) or enabled.
### Return value

true if player controls are enabled; otherwise, false.
## void setControls ( const Ptr < Controls > & controls )

Sets a *[Controls](../../../api/library/controls/class.controls_cpp.md)* object that will hold settings of input controls relevant to the player.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Controls](../../../api/library/controls/class.controls_cpp.md)> &* **controls** - [Controls](../../../api/library/controls/class.controls_cpp.md) object used to handle input controls.

## Ptr < Controls > getControls ( ) const

Returns a [Controls](../../../api/library/controls/class.controls_cpp.md) object that holds settings of input controls relevant to the player.
### Return value

*[Controls](../../../api/library/controls/class.controls_cpp.md)* object used to handle input controls.
## void getDirectionFromScreen ( Math:: Vec3 & p0 , Math:: Vec3 & p1 , int mouse_x , int mouse_y , int screen_x , int screen_y , int screen_width , int screen_height ) const


Casts the ray to a certain position on the screen and returns coordinates of the start (p0) and end (p1) points of the ray.


```cpp
Vec3 p0, p1;

// get the current player (camera)
PlayerPtr player = Game::getPlayer();

if (player.get() == NULL)
	return 0;

// get width and height of the current application window's client area
Math::ivec2 winsize = WindowManager::getMainWindow()->getClientSize();
int width = winsize.x;
int height = winsize.y;

// get the current X and Y coordinates of the mouse pointer
int mouse_x = Gui::getCurrent()->getMouseX();
int mouse_y = Gui::getCurrent()->getMouseY();

// get the mouse direction from the player's position (p0) to the mouse cursor pointer (p1)
player->getDirectionFromScreen(p0, p1, mouse_x, mouse_y, 0, 0, width, height);


```


### Arguments

- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start coordinates of the ray.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End coordinates of the ray.
- *int* **mouse_x** - X-coordinate of the mouse position.
- *int* **mouse_y** - Y-coordinate of the mouse position.
- *int* **screen_x** - X-coordinate of the screen position.
- *int* **screen_y** - Y-coordinate of the screen position.
- *int* **screen_width** - Screen width.
- *int* **screen_height** - Screen height.

## Math:: vec3 getDirectionFromScreen ( int mouse_x , int mouse_y , int screen_x , int screen_y , int screen_width , int screen_height ) const


Casts the ray to a certain position on the screen and returns a vector in the direction of this position.


```cpp
// get width and height of the current application window's client area
Math::ivec2 winsize = WindowManager::getMainWindow()->getClientSize();
int width = winsize.x;
int height = winsize.y;

// initializing points of the ray from player's position in the direction pointed by the mouse cursor
Vec3 p0 = player->getWorldPosition();
Vec3 p1 = p0 + Vec3(player->getDirectionFromScreen(Gui::getCurrent()->getMouseX(), Gui::getCurrent()->getMouseY(), 0, 0, width, height)) * 100;


```


### Arguments

- *int* **mouse_x** - X-coordinate of the mouse position.
- *int* **mouse_y** - Y-coordinate of the mouse position.
- *int* **screen_x** - X-coordinate of the screen position.
- *int* **screen_y** - Y-coordinate of the screen position.
- *int* **screen_width** - Screen width.
- *int* **screen_height** - Screen height.

### Return value

Vector coordinates.
## void setFov ( float fov )


Sets a vertical field of view of the player.


> **Notice:** Horizontal FOV cannot be used since it varies depending on the viewport's aspect ratio. Setting FOV recalculates projection matrix with aspect ratio = 1.


You can use the following formula to calculate horizontal FOV from the vertical one for the given aspect ratio (width/height): FOV_h = 2 � atan ( (width / height) � tan(FOV_v / 2)).


### Arguments

- *float* **fov** - New vertical field of view in degrees. The provided value will be saturated in the range [0; 180]. The default is 60 degrees.

## float getFov ( ) const


Returns the current vertical field of view of the player.


> **Notice:** Horizontal FOV cannot be used since it varies depending on the viewport's aspect ratio.


You can use the following formula to calculate horizontal FOV from the vertical one for the given aspect ratio (width/height): FOV_h = 2 � atan ( (width / height) � tan(FOV_v / 2)).


### Return value

Vertical field of view in degrees. The default is 60 degrees.
## void setObliqueFrustum ( bool frustum )


Enables or disables obliqueness of the viewing frustum.


> **Notice:** It is recommended to set oblique viewing frustum using this method, as it doesn't affect the projection matrix. To specify the near clipping plane use the *[setObliqueFrustumPlane()](#setObliqueFrustumPlane_Vec4_void)* method.


### Arguments

- *bool* **frustum** - true to enable oblique viewing frustum; false to disable it.

## bool isObliqueFrustum ( ) const

Returns a value indicating if the viewing frustum is oblique.
### Return value

true if the viewing frustum is oblique; otherwise, false.
## void setObliqueFrustumPlane ( const Math:: Vec4 & plane )


Sets the oblique near clipping plane of the viewing frustum.


> **Notice:** This method does not affect the projection matrix. To enable the oblique frustum use the *[setObliqueFrustum()](#setObliqueFrustum_int_void)* method.


```cpp
#include "AppWorldLogic.h"
#include <UnigineGame.h>
#include <UniginePlayers.h>

using namespace Unigine;
using namespace Math;

/* ... */

int AppWorldLogic::update()
{

	float time = Game::getTime();

	// initializing a plane to be set as a near clipping plane
	Math::Vec4 plane = Math::Vec4(1.0f, 1.0f, 1.0f, 1.0f + Math::sin(time) * 4.0f);

	// getting a player
	PlayerPtr player = Game::getPlayer();
	if (player != nullptr)
	{
		// enabling oblique frustum
		player->setObliqueFrustum(1);

		// setting our plane as an oblique near clipping plane
		player->setObliqueFrustumPlane(plane);
	}

	return 1;
}


```


### Arguments

- *const  Math::[Vec4](../../../api/library/math/class.vec4_cpp.md) &* **plane** - World coordinates of the oblique near clipping plane to set (Nx, Ny, Nz, D), where Nx, Ny, Nz - coordinates of the plane normal, D - distance from the origin to the plane.

## Math:: Vec4 getObliqueFrustumPlane ( ) const

Returns the oblique near clipping plane of the viewing frustum.
### Return value

World coordinates of the oblique near clipping plane to set (Nx, Ny, Nz, D), where Nx, Ny, Nz - coordinates of the plane normal, D - distance from the origin to the plane.
## void setProjection ( const Math:: mat4 & projection )


Updates the current projection matrix.


> **Notice:** It is not recommended to use this method for setting obliqueness of the near clipping plane of the frustum, as in this case a number of features (such as clouds, shadows, TAA, a number of engine optimizations, etc.) will not function properly. Please, use the [setObliqueFrustum()](#setObliqueFrustum_int_void) method instead.


### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **projection** - New projection matrix.

## Math:: mat4 getProjection ( ) const

Returns the current projection matrix with unit (1.0) aspect ratio.
### Return value

Current projection matrix.
## Math:: mat4 getProjectionFromScreen ( int x0 , int y0 , int x1 , int y1 , int screen_width , int screen_height ) const

Creates a projection matrix out of 2 screen positions . This is required for the frame selection.
### Arguments

- *int* **x0** - X-coordinate of the first screen position.
- *int* **y0** - Y-coordinate of the first screen position.
- *int* **x1** - X-coordinate of the second screen position.
- *int* **y1** - Y-coordinate of the second screen position.
- *int* **screen_width** - Screen width.
- *int* **screen_height** - Screen height.

### Return value

Projection matrix.
## void setReflectionViewportMask ( int mask )

Sets a bit mask for rendering reflections into the viewport. Reflections are rendered in the viewport if masks of reflective materials match this one (one bit at least).
### Arguments

- *int* **mask** - Reflection viewport mask (an integer, each bit of which is a mask).

## int getReflectionViewportMask ( ) const

Returns the current bit mask for rendering reflections into the viewport. Reflections are rendered in the viewport if masks of reflective materials match this one (one bit at least).
### Return value

Reflection viewport mask (an integer, each bit of which is a mask).
## void setReverbMask ( int mask )

Sets a bit mask that determines what [reverberation zones](../../../api/library/sounds/class.soundreverb_cpp.md) can be heard. For sound to reverberate, at least one bit of this mask should match with a [reverb mask of the sound source](../../../api/library/sounds/class.soundsource_cpp.md#setReverbMask_int_void) and a [reverb mask of the reverberation zone](../../../api/library/sounds/class.soundreverb_cpp.md#setReverbMask_int_void). (Masks of a sound source and reverberation zone can match with the player's one in different bits, not necessarily one).
### Arguments

- *int* **mask** - Integer, each bit of which is a mask for reverberating sound sources and reverberation zones.

## int getReverbMask ( ) const

Returns the current bit mask that determines what [reverberation zones](../../../api/library/sounds/class.soundreverb_cpp.md) can be heard. For sound to reverberate, at least one bit of this mask should match with a [reverb mask of the sound source](../../../api/library/sounds/class.soundsource_cpp.md#setReverbMask_int_void) and a [reverb mask of the reverberation zone](../../../api/library/sounds/class.soundreverb_cpp.md#setReverbMask_int_void). (Masks of a sound source and reverberation zone can match with the player's one in different bits, not necessarily one).
### Return value

Integer, each bit of which is a mask for reverberating sound sources and reverberation zones.
## int getScreenPosition ( int & x , int & y , const Math:: Vec3 & point , int screen_width , int screen_height ) const

Projects the point in world coordinates to the screen. Screen coordinates are written into the first 2 variables passed to the method (in pixels).


```cpp
// get relative screen position of a world-space point (world_point_position)
EngineWindowViewportPtr main_window = WindowManager::getMainWindow();
ivec2 client_render_size = main_window->getClientRenderSize();
int screen_x, screen_y;
Game::getPlayer()->getScreenPosition(screen_x, screen_y, world_point_position, client_render_size.x, client_render_size.y);
vec2 relative_pos = vec2(screen_x, screen_y) / client_render_size;

```


### Arguments

- *int &* **x** - X-coordinate of the screen position (in pixels).
- *int &* **y** - Y-coordinate of the screen position (in pixels).
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point coordinates.
- *int* **screen_width** - Screen width.
- *int* **screen_height** - Screen height.

### Return value

1 if the point has been projected successfully; otherwise, 0.
## void setSourceMask ( int mask )

Sets a bit mask that determines what sound sources can be heard. For a sound source to be heard, [its mask](../../../api/library/sounds/class.soundsource_cpp.md#setSourceMask_int_void) should match with this one in at least one bit. Plus, the volume of [sound channel](../../../api/library/engine/class.sound_cpp.md#setSourceVolume_int_float_void) in which the sound plays (its number also depends on this mask) should not be equal to 0.
### Arguments

- *int* **mask** - Source mask (integer, each bit of which specifies a sound channel).

## int getSourceMask ( ) const

Returns a bit mask that determines what [sound channels](../../../api/library/engine/class.sound_cpp.md#setSourceVolume_int_float_void) can be heard. For a sound source to be heard, [its mask](../../../api/library/sounds/class.soundsource_cpp.md#setSourceMask_int_void) should match with this one in at least one bit. Plus, the volume of [sound channel](../../../api/library/engine/class.sound_cpp.md#setSourceVolume_int_float_void) in which the sound plays (its number also depends on this mask) should not be equal to 0.
### Return value

Source mask (integer, each bit of which specifies a sound channel).
## void setUp ( const Math:: vec3 & up )


Sets an up direction of the player's viewport (i.e. tilt of the player's viewport).


> **Notice:** In case of [PlayerActor](../../../api/library/players/class.playeractor_cpp.md), its transformation forces it to recalculate its inner state (position, direction, angles and so on), so the up direction of the player's viewport may become "negative forward". And then transformation will be recalculated by using this direction, causing flip of the basis of the player actor. To avoid such flipping, the theta and phi angles should be [recalculated](../../../api/library/players/class.playeractor_cpp.md#setViewDirection_vec3_void) by using the [current viewing orientation](../../../api/library/players/class.playeractor_cpp.md#getViewDirection_vec3) of the player.


### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **up** - New upward direction vector. The vector is normalized to 1.

## Math:: vec3 getUp ( ) const

Returns the current up direction of the player's viewport (i.e. tilt of the player's viewport).
### Return value

Upward direction vector.
## void setVelocity ( const Math:: vec3 & velocity )


Sets a player's velocity.


> **Notice:** In case of [PlayerActor](../../../api/library/players/class.playeractor_cpp.md), this function is valid only when the player is not simulated physically ([*setPhysical()*](../../../api/library/players/class.playeractor_cpp.md#setPhysical_int_void) is set to 0). If it is, moving PlayerActor is done via accessing its body.


### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **velocity** - New velocity in units per second.

## Math:: vec3 getVelocity ( ) const

Returns the current velocity of the player.
### Return value

Velocity in units per second.
## void setViewDirection ( const Math:: vec3 & direction )

Sets given view direction vector to the Player instance.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **direction** - A view direction vector.

## Math:: vec3 getViewDirection ( ) const

Returns Player's view direction vector.
### Return value

A view direction vector.
## void setViewportMask ( int mask )

Sets a bit mask for rendering into the viewport. Object surfaces, materials, decals, lights and GUI objects will be rendered into the viewport only if their viewport mask matches the player's one (one matching bit is enough).
### Arguments

- *int* **mask** - Viewport mask (integer, each bit of which is a mask).

## int getViewportMask ( ) const

Returns the current bit mask for rendering into the viewport. Object surfaces, materials, decals, lights and GUI objects will be rendered into the viewport only if their viewport mask matches the player's one (one matching bit is enough).
### Return value

Viewport mask (integer, each bit of which is a mask).
## void setZFar ( float zfar )

Sets a distance to the far clipping plane of the player's viewing frustum. The default is 10000 units.
### Arguments

- *float* **zfar** - Distance to the far clipping plane in units. The minimum value is 0.

## float getZFar ( ) const

Returns the current distance to the far clipping plane of the player's viewing frustum. The default is 10000 units.
### Return value

Distance to the far clipping plane in units.
## void setZNear ( float znear )

Sets a distance to the near clipping plane of the player's viewing frustum. The default is 0.1 units.
### Arguments

- *float* **znear** - Distance to the near clipping plane in units. The minimum value is 0.

## float getZNear ( ) const

Returns the distance to the near clipping plane of the player's viewing frustum. The default is 0.1 units.
### Return value

Distance to the near clipping plane in units.
## void flushTransform ( ) const

Forces to immediately set transformations to the player. This function should be called manually after user input has been updated via *updateControls()*.
## void updateControls ( float ifps ) const

Gets the current player's parameters (impulse, direction, velocity etc) according to user input. After the input has been updated, *flushTransform()* should be called manually to apply it to the player.
### Arguments

- *float* **ifps** - Frame duration in seconds.

## void setFovMode ( Camera::FOV_MODE mode )


Sets the value indicating the type of FOV that is used for the player:


- For the standard player, the vertical FOV should be set. In this case, FOV is directly set in [degrees](#setFov_float_void).
- For the physically-based player, the horizontal FOV should be set. In this case, FOV is calculated depending on the [film gate](#setFilmGate_float_void) and [focal length](#setFocalLength_float_void) of the player.


### Arguments

- *[Camera::FOV_MODE](../../../api/library/rendering/class.camera_cpp.md#FOV_MODE)* **mode** - *[FOV_MODE_VERTICAL](../../../api/library/rendering/class.camera_cpp.md#FOV_MODE_VERTICAL)* for the player with the vertical FOV; *[FOV_MODE_PHYSICALLY_BASED_CAMERA](../../../api/library/rendering/class.camera_cpp.md#FOV_MODE_PHYSICALLY_BASED_CAMERA)* for the physically-based player with the horizontal FOV.

## Camera::FOV_MODE getFovMode ( ) const

Returns the value indicating the type of FOV that is used for the player.
### Return value

0 if the player with the vertical FOV is used; 1 if the physically-based player with the horizontal FOV is used.
## void setFilmGate ( float gate )

Sets a film gate for the physically-based camera with horizontal FOV.
### Arguments

- *float* **gate** - Film gate.

## float getFilmGate ( ) const

Returns a film gate for the physically-based camera with horizontal FOV.
### Return value

Film gate.
## void setFocalLength ( float length )

Sets a focal length of the physically-based camera lens.
### Arguments

- *float* **length** - Camera lens focal length.

## float getFocalLength ( ) const

Returns the focal length of the physically-based camera lens.
### Return value

Camera lens focal length.
## Math:: mat4 getAspectCorrectedProjection ( int width = -1 , int height = -1 ) const

Returns projection matrix after correction for the specified aspect ratio (**screen width** / **screen height**). [Currently fixed FOV component](#getFovFixed_int) is taken into account.
### Arguments

- *int* **width** - Screen width.
- *int* **height** - Screen height.

### Return value

Projection matrix after correction for the specified aspect ratio (**screen width** / **screen height**).
## Camera::FOV_FIXED getFovFixed ( ) const

Returns a value indicating which FOV component (horizontal or vertical) is currently fixed.
### Return value

Current fixed FOV component, one of the [Camera::FOV_FIXED_*](../../../api/library/rendering/class.camera_cpp.md#FOV_FIXED_HORIZONTAL) values.
## void addScriptableMaterial ( const Ptr < Material > & material )


Attaches a new [scriptable material](../../../content/materials/scriptable.md) to the player. To apply a scriptable material globally, use the **[addScriptableMaterial()](../../../api/library/rendering/class.render_cpp.md#addScriptableMaterial_Material_void)** method of the *Render* class. The order of execution for scripts assigned to scriptable materials is defined by material's number in the list of the player.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cpp.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-player.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Scriptable material to be attached to the player.

## void insertScriptableMaterial ( int num , const Ptr < Material > & material )


Inserts a new [scriptable material](../../../content/materials/scriptable.md) into the list of the ones assigned to the player. To apply a scriptable material globally, use the [*insertScriptableMaterial()*](../../../api/library/rendering/class.render_cpp.md#insertScriptableMaterial_int_Material_void) method of the *Render* class. The order of execution for scripts assigned to scriptable materials is defined by material's number in the player's list.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cpp.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-player.

### Arguments

- *int* **num** - Position at which a new scriptable material is to be inserted.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Scriptable material to be inserted.

## void removeScriptableMaterial ( int num )

Removes the [scriptable material](../../../content/materials/scriptable.md) with the specified number from the player.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

## int getNumScriptableMaterials ( ) const

Returns the total number of [scriptable materials](../../../content/materials/scriptable.md) attached to the player.
### Return value

Total number of scriptable materials attached to the player.
## int findScriptableMaterial ( const Ptr < Material > & material ) const


Returns the number of the specified [scriptable material](../../../content/materials/scriptable.md) for the player. This number is player-specific (valid for this player only) and determines the order in which the assigned expressions are executed.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cpp.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-player.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - Scriptable material for which a number is to be found.

### Return value

Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int), or -1 if the specified material was not found.
## void setScriptableMaterial ( int num , const Ptr < Material > & material )


Replaces the [scriptable material](../../../content/materials/scriptable.md) with the specified number with the new scriptable material specified. The number of material determines the order in which the expressions assigned to it are executed. This number is player-specific (valid for this player only).


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cpp.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-player.


### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Material](../../../api/library/rendering/class.material_cpp.md)> &* **material** - New scriptable material to replace the one with the specified number.

## Ptr < Material > getScriptableMaterial ( int num ) const

Returns a [scriptable material](../../../content/materials/scriptable.md) attached to the player by its number.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

### Return value

Scriptable material attached to the player with the specified number.
## void setScriptableMaterialEnabled ( int num , bool enabled )

Enables or disables the [scriptable material](../../../content/materials/scriptable.md) with the specified number. When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *bool* **enabled** - true to enable the scriptable material with the specified number, false to disable it.

## bool getScriptableMaterialEnabled ( int num ) const

Returns a value indicating if the [scriptable material](../../../content/materials/scriptable.md) with the specified number attached to the player is enabled (active). When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

### Return value

true if the scriptable material with the specified number is enabled; otherwise, false.
## void swapScriptableMaterials ( int num_0 , int num_1 )


Swaps two [scriptable materials](../../../content/materials/scriptable.md) with specified numbers. The number of material determines the order in which the expressions assigned to it are executed.


> **Notice:** The number is player-specific (valid for this player only).


### Arguments

- *int* **num_0** - Number of the first scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *int* **num_1** - Number of the second scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

## void clearScriptableMaterials ( )

Clears all [scriptable materials](../../../content/materials/scriptable.md) attached to the player.
## void setMainPlayer ( bool player )

Sets a player as a [main player](../../../objects/players/index.md#main_player).
### Arguments

- *bool* **player** - true to set the player as the main player, false to unset it.

## bool isMainPlayer ( ) const

Checks if the player is a [main player](../../../objects/players/index.md#main_player).
### Return value

true if the player is a main player; otherwise, false.
## void setListener ( bool listener )

Sets the player as the listener.
### Arguments

- *bool* **listener** - true to set the player as the listener, false to unset it.

## bool isListener ( ) const

Checks if the player is a [listener](../../../objects/players/index.md#listener).
### Return value

true if the player is a listener; otherwise, false.
## void getDirectionFromMainWindow ( Math:: Vec3 & p0 , Math:: Vec3 & p1 , int mouse_x , int mouse_y ) const

Casts the ray to a certain position on the screen and returns coordinates of the start (p0) and end (p1) points of the ray relative to the current main window.
### Arguments

- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start coordinates of the ray.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End coordinates of the ray.
- *int* **mouse_x** - X-coordinate of the mouse position in world coordinates.
- *int* **mouse_y** - Y-coordinate of the mouse position in world coordinates.

## Math:: vec3 getDirectionFromMainWindow ( int mouse_x , int mouse_y ) const

Casts the ray to a certain position on the screen and returns a vector in the direction of this position relative to the current main window.
### Arguments

- *int* **mouse_x** - X-coordinate of the mouse position in world coordinates.
- *int* **mouse_y** - Y-coordinate of the mouse position in world coordinates.

### Return value

Vector coordinates.
## void getDirectionFromWindow ( Math:: Vec3 & p0 , Math:: Vec3 & p1 , int mouse_x , int mouse_y , const Ptr < EngineWindowViewport > & window ) const

Casts the ray to a certain position on the screen and returns coordinates of the start (p0) and end (p1) points of the ray relative to the specified window viewport.
### Arguments

- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start coordinates of the ray.
- *Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End coordinates of the ray.
- *int* **mouse_x** - X-coordinate of the mouse position in world coordinates.
- *int* **mouse_y** - Y-coordinate of the mouse position in world coordinates.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cpp.md)> &* **window** - Window viewport relative to which the directon is returned.

## Math:: vec3 getDirectionFromWindow ( int mouse_x , int mouse_y , const Ptr < EngineWindowViewport > & window ) const

Casts the ray to a certain position on the screen and returns a vector in the direction of this position relative to the specified window viewport.
### Arguments

- *int* **mouse_x** - X-coordinate of the mouse position in world coordinates.
- *int* **mouse_y** - Y-coordinate of the mouse position in world coordinates.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cpp.md)> &* **window** - Window viewport relative to which the directon is returned.

### Return value

Vector coordinates.
## Math:: mat4 getProjectionFromMainWindow ( int x0 , int y0 , int x1 , int y1 ) const

Creates a projection matrix out of 2 screen positions relative to the current main window. This is required for the frame selection.
### Arguments

- *int* **x0** - X-coordinate of the first screen position.
- *int* **y0** - Y-coordinate of the first screen position.
- *int* **x1** - X-coordinate of the second screen position.
- *int* **y1** - Y-coordinate of the second screen position.

### Return value

Projection matrix.
## Math:: mat4 getProjectionFromWindow ( int x0 , int y0 , int x1 , int y1 , const Ptr < EngineWindowViewport > & window ) const

Creates a projection matrix out of 2 screen positions relative to the specified window viewport. This is required for the frame selection.
### Arguments

- *int* **x0** - X-coordinate of the first screen position.
- *int* **y0** - Y-coordinate of the first screen position.
- *int* **x1** - X-coordinate of the second screen position.
- *int* **y1** - Y-coordinate of the second screen position.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cpp.md)> &* **window** - Window viewport relative to which the projection is returned.

### Return value

Projection matrix.
## int getMainWindowPosition ( int & x , int & y , const Math:: Vec3 & point ) const


Projects the point in world coordinates relative to the main window. The coordinates are written into the first 2 variables passed to the method (in pixels).


```cpp

// get relative screen position of a world-space point (world_point_position)
ivec2 client_render_size = WindowManager::getMainWindow()->getClientRenderSize();
int screen_x, screen_y;
Game::getPlayer()->getMainWindowPosition(screen_x, screen_y, world_point_position);
vec2 relative_pos = vec2(screen_x, screen_y) / client_render_size;

```


### Arguments

- *int &* **x** - X-coordinate of the screen position (in pixels).
- *int &* **y** - Y-coordinate of the screen position (in pixels).
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point coordinates.

### Return value

1 if the point has been projected successfully; otherwise, 0.
## int getWindowPosition ( int & x , int & y , const Math:: Vec3 & point , const Ptr < EngineWindowViewport > & window ) const


Projects the point in world coordinates relative to the specified window viewport. The coordinates are written into the first 2 variables passed to the method (in pixels).


```cpp

// get relative screen position of a world-space point (world_point_position)
EngineWindowViewportPtr main_window = WindowManager::getMainWindow();
ivec2 client_render_size = main_window->getClientRenderSize();
int screen_x, screen_y;
Game::getPlayer()->getWindowPosition(screen_x, screen_y, world_point_position, main_window);
vec2 relative_pos = vec2(screen_x, screen_y) / client_render_size;

```


### Arguments

- *int &* **x** - X-coordinate of the screen position (in pixels).
- *int &* **y** - Y-coordinate of the screen position (in pixels).
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **point** - Point coordinates.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cpp.md)> &* **window** - Window viewport relative to which the projection is returned.

### Return value

1 if the point has been projected successfully; otherwise, 0.
## void setProjectionMode ( Camera::PROJECTION_MODE mode )

Sets the projection mode: orthographic or perspective.
### Arguments

- *[Camera::PROJECTION_MODE](../../../api/library/rendering/class.camera_cpp.md#PROJECTION_MODE)* **mode** - The projection mode, *[PROJECTION_MODE_ORTHOGRAPHIC](../../../api/library/rendering/class.camera_cpp.md#PROJECTION_MODE_ORTHOGRAPHIC)* for the orthographic mode; *[PROJECTION_MODE_PERSPECTIVE](../../../api/library/rendering/class.camera_cpp.md#PROJECTION_MODE_PERSPECTIVE)* for the perspective mode.

## Camera::PROJECTION_MODE getProjectionMode ( ) const

Returns the current projection mode: orthographic or perspective.
### Return value

The projection mode, *[PROJECTION_MODE_ORTHOGRAPHIC](../../../api/library/rendering/class.camera_cpp.md#PROJECTION_MODE_ORTHOGRAPHIC)* for the orthographic mode; *[PROJECTION_MODE_PERSPECTIVE](../../../api/library/rendering/class.camera_cpp.md#PROJECTION_MODE_PERSPECTIVE)* for the perspective mode.
## void setOrthoHeight ( float height )

Sets the height of the camera with the orthographic [projection mode](#getProjectionMode_int) enabled.
### Arguments

- *float* **height** - The orthographic camera height.

## float getOrthoHeight ( ) const

Returns the current height of the camera with the orthographic [projection mode](#getProjectionMode_int) enabled.
### Return value

The orthographic camera height.
