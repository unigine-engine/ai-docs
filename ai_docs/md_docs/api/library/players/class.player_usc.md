# Unigine.Player Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


This class is used to create cameras that view the world. When you create a new player, it creates a [camera](../../../api/library/rendering/class.camera_usc.md) and specifies controls, [masks](#player_masks), postprocess materials for this camera.


Players' viewing frustum is defined by a [near clipping plane](#setZNear_float_void), [far clipping plane](#setZFar_float_void) and the [field of view](#setFov_float_void). Note that if you set up a custom [projection](#setProjection_mat4_void) matrix and after that call any of these functions:


- [*setFov()*](#setFov_float_void)
- [*setZFar()*](#setZFar_float_void)
- [*setZNear()*](#setZNear_float_void)


your custom matrices will be overwritten.


Players cannot have a parent node; they always use the world coordinates for their transformations. The only exception is [PlayerDummy](../../../api/library/players/class.playerdummy_usc.md).


### Player Masks


Objects, decals and lights can be selectively displayed in the player viewport. To be displayed, their viewport mask should be matching with the player's [viewport mask](#setViewportMask_int_void) (one matching bit is enough):


- Object [surface viewport mask](../../../api/library/objects/class.object_usc.md#setViewportMask_int_int_void) or [decal viewport mask](../../../api/library/decals/class.decal_usc.md#setViewportMask_int_void)
- [Light viewport mask](../../../api/library/lights/class.light_usc.md#setViewportMask_int_void) to light the object/decal
- [Material viewport mask](../../../api/library/rendering/class.material_usc.md#setViewportMask_int_void) to render the object/decal material


Reflections can also be selectively rendered into the viewport: an object can be rendered without reflection or reflection without an object. For that, the player's [reflection viewport mask](#setReflectionViewportMask_int_void) should match:


- Reflection mask of the reflecting material
- [Viewport mask](../../../api/library/rendering/class.material_usc.md#setViewportMask_int_void) of the reflecting material
- Object [surface viewport mask](../../../api/library/objects/class.object_usc.md#setViewportMask_int_int_void)
- [Material viewport mask](../../../api/library/rendering/class.material_usc.md#setViewportMask_int_void) of the reflected material
- [Light viewport mask](../../../api/library/lights/class.light_usc.md#setViewportMask_int_void)


That is enough to render reflection from the object without an object itself. If an object needs to be present as well, all these conditions should simply go together with above mentioned ones.


To render an object without reflection, simply either its [material viewport mask](../../../api/library/rendering/class.material_usc.md#setViewportMask_int_void) or object [surface viewport mask](../../../api/library/objects/class.object_usc.md#setViewportMask_int_int_void) should not match the player's [reflection viewport mask](#setReflectionViewportMask_int_void).


Players also can have sound source and sound reverberation masks. As well as for viewports, corresponding masks of the *Player* object should match with [SoundReverb](../../../api/library/sounds/class.soundreverb_usc.md#setReverbMask_int_void) and [SoundSource](../../../api/library/sounds/class.soundsource_usc.md#setSourceMask_int_void) masks.


### Perspective and Orthographic Projection


Depending on your project's requirements you can set your player to use [perspective](../../../principles/world_management/index.md#camera_perspective) or [orthographic](../../../principles/world_management/index.md#camera_orthographic) projection. This can be done via the [*setProjection()*](#setProjection_mat4_void) method.


For example, you can use the following code to set up **orthographic projection** or **perspective projection** for your current game player depending on a flag value:


```cpp
// world.usc

Player player;

/* ... */

// ortho flag - change this value to switch projection type
int ortho_flag = 0;

int init(){
	/* ... */

	// getting the current player
	player = engine.game.getPlayer();

	// setting up near and far clipping planes and aspect ratio
	float znear = 0.001f;
	float zfar = 10000.0f;
	float aspect = 16.0f / 9.0f;

	if (ortho_flag)
	{
		// setting up orthographic projection
		player.setProjection(ortho(-1.0f, 1.0f, -1.0f, 1.0f, znear, zfar));
	}
	else
	{
		// setting up perspective projection
		player.setProjection(perspective(60.0f, aspect, znear, zfar));
	}

	return 1;
}

```


### Getting Euler Angles for an Active Camera


Sometimes it might be necessary to get current rotation of the active camera as a set of Euler angles. When we talk about axes in UNIGINE we assume that:


|  |  |
|---|---|
| - **X** axis points to the *right* giving us a **pitch** angle. - **Y** axis points *forward* giving us a **roll** angle. - **Z** axis points *up* giving us a **yaw** (heading) angle. | ![](../../../code/fundamentals/matrices/object_directions.png) *Object Direction Vectors* |


To get the Euler angles we should use [*decomposeRotationZXY()*](../../../api/library/math/math.matrix_usc.md#decomposeRotationZXY_const_mat3_ref_vec3) also known as Cardan angles (**yaw** is independent, then we get **pitch** and in the end, **roll**). But, there is one thing to be taken into account - cameras have a different system:


|  |  |
|---|---|
| - **X** axis points to the *right* giving us a **pitch** angle. - **Y** axis points *up* giving us a **yaw** (heading) angle. - **Z** axis points *backward* giving us a **-roll** angle. | ![](../../../code/fundamentals/matrices/camera_directions.png) *Camera Direction Vectors* |


To compensate it, we need to rotate our camera **-90** degrees around **X** axis.


## Player Class

### Members

---

## void setCamera ( )

Sets given Camera instance to the Player.
### Arguments

## getCamera ( )

Returns the Camera instance of the Player node.
### Return value

The camera of the player.
## void setControlled ( int controlled )

Disables or enables the player controls.
### Arguments

- *int* **controlled** - **1** to enable player controls, **0** to disable (player stops responding to them).

## int isControlled ( )

Returns a value indicating whether player controls are disabled (player does not respond to them) or enabled.
### Return value

**1** if player controls are enabled; otherwise, **0**.
## void setControls ( Controls controls )

Sets a *[Controls](../../../api/library/controls/class.controls_usc.md)* object that will hold settings of input controls relevant to the player.
### Arguments

- *[Controls](../../../api/library/controls/class.controls_usc.md)* **controls** - [Controls](../../../api/library/controls/class.controls_usc.md) object used to handle input controls.

## Controls getControls ( )

Returns a [Controls](../../../api/library/controls/class.controls_usc.md) object that holds settings of input controls relevant to the player.
### Return value

*[Controls](../../../api/library/controls/class.controls_usc.md)* object used to handle input controls.
## void setFov ( float fov )


Sets a vertical field of view of the player.


> **Notice:** Horizontal FOV cannot be used since it varies depending on the viewport's aspect ratio. Setting FOV recalculates projection matrix with aspect ratio = 1.


You can use the following formula to calculate horizontal FOV from the vertical one for the given aspect ratio (width/height): FOV_h = 2 � atan ( (width / height) � tan(FOV_v / 2)).


### Arguments

- *float* **fov** - New vertical field of view in degrees. The provided value will be saturated in the range [0; 180]. The default is 60 degrees.

## float getFov ( )


Returns the current vertical field of view of the player.


> **Notice:** Horizontal FOV cannot be used since it varies depending on the viewport's aspect ratio.


You can use the following formula to calculate horizontal FOV from the vertical one for the given aspect ratio (width/height): FOV_h = 2 � atan ( (width / height) � tan(FOV_v / 2)).


### Return value

Vertical field of view in degrees. The default is 60 degrees.
## void setObliqueFrustum ( int frustum )


Enables or disables obliqueness of the viewing frustum.


> **Notice:** It is recommended to set oblique viewing frustum using this method, as it doesn't affect the projection matrix. To specify the near clipping plane use the *[setObliqueFrustumPlane()](#setObliqueFrustumPlane_Vec4_void)* method.


### Arguments

- *int* **frustum** - **1** to enable oblique viewing frustum; **0** to disable it.

## int isObliqueFrustum ( )

Returns a value indicating if the viewing frustum is oblique.
### Return value

**1** if the viewing frustum is oblique; otherwise, **0**.
## void setObliqueFrustumPlane ( Vec4 plane )


Sets the oblique near clipping plane of the viewing frustum.


> **Notice:** This method does not affect the projection matrix. To enable the oblique frustum use the *[setObliqueFrustum()](#setObliqueFrustum_int_void)* method.


```cpp
/* .. */

int update() {
	// Write here code to be called before updating each render frame: specify all graphics-related functions you want to be called every frame while your application executes.
            float time = engine.game.getTime();

				// initializing a plane to be set as a near clipping plane
                Vec4 plane = Vec4(1.0f, 1.0f, 1.0f, 1.0f + sin(time) * 4.0f);

				// getting a player
                Player player = engine.game.getPlayer();
                if (player != NULL)
                {
					// enabling oblique frustum
                    player.setObliqueFrustum(1);

					// setting our plane as an oblique near clipping plane
                    player.setObliqueFrustumPlane(plane);
                }

	return 1;
}

/* .. */

```


### Arguments

- *Vec4* **plane** - World coordinates of the oblique near clipping plane to set (Nx, Ny, Nz, D), where Nx, Ny, Nz - coordinates of the plane normal, D - distance from the origin to the plane.

## Vec4 getObliqueFrustumPlane ( )

Returns the oblique near clipping plane of the viewing frustum.
### Return value

World coordinates of the oblique near clipping plane to set (Nx, Ny, Nz, D), where Nx, Ny, Nz - coordinates of the plane normal, D - distance from the origin to the plane.
## void setProjection ( mat4 projection )


Updates the current projection matrix.


> **Notice:** It is not recommended to use this method for setting obliqueness of the near clipping plane of the frustum, as in this case a number of features (such as clouds, shadows, TAA, a number of engine optimizations, etc.) will not function properly. Please, use the [setObliqueFrustum()](#setObliqueFrustum_int_void) method instead.


### Arguments

- *mat4* **projection** - New projection matrix.

## mat4 getProjection ( )

Returns the current projection matrix with unit (1.0) aspect ratio.
### Return value

Current projection matrix.
## void setReflectionViewportMask ( int mask )

Sets a bit mask for rendering reflections into the viewport. Reflections are rendered in the viewport if masks of reflective materials match this one (one bit at least).
### Arguments

- *int* **mask** - Reflection viewport mask (an integer, each bit of which is a mask).

## int getReflectionViewportMask ( )

Returns the current bit mask for rendering reflections into the viewport. Reflections are rendered in the viewport if masks of reflective materials match this one (one bit at least).
### Return value

Reflection viewport mask (an integer, each bit of which is a mask).
## void setReverbMask ( int mask )

Sets a bit mask that determines what [reverberation zones](../../../api/library/sounds/class.soundreverb_usc.md) can be heard. For sound to reverberate, at least one bit of this mask should match with a [reverb mask of the sound source](../../../api/library/sounds/class.soundsource_usc.md#setReverbMask_int_void) and a [reverb mask of the reverberation zone](../../../api/library/sounds/class.soundreverb_usc.md#setReverbMask_int_void). (Masks of a sound source and reverberation zone can match with the player's one in different bits, not necessarily one).
### Arguments

- *int* **mask** - Integer, each bit of which is a mask for reverberating sound sources and reverberation zones.

## int getReverbMask ( )

Returns the current bit mask that determines what [reverberation zones](../../../api/library/sounds/class.soundreverb_usc.md) can be heard. For sound to reverberate, at least one bit of this mask should match with a [reverb mask of the sound source](../../../api/library/sounds/class.soundsource_usc.md#setReverbMask_int_void) and a [reverb mask of the reverberation zone](../../../api/library/sounds/class.soundreverb_usc.md#setReverbMask_int_void). (Masks of a sound source and reverberation zone can match with the player's one in different bits, not necessarily one).
### Return value

Integer, each bit of which is a mask for reverberating sound sources and reverberation zones.
## void setSourceMask ( int mask )

Sets a bit mask that determines what sound sources can be heard. For a sound source to be heard, [its mask](../../../api/library/sounds/class.soundsource_usc.md#setSourceMask_int_void) should match with this one in at least one bit. Plus, the volume of [sound channel](../../../api/library/engine/class.sound_usc.md#setSourceVolume_int_float_void) in which the sound plays (its number also depends on this mask) should not be equal to 0.
### Arguments

- *int* **mask** - Source mask (integer, each bit of which specifies a sound channel).

## int getSourceMask ( )

Returns a bit mask that determines what [sound channels](../../../api/library/engine/class.sound_usc.md#setSourceVolume_int_float_void) can be heard. For a sound source to be heard, [its mask](../../../api/library/sounds/class.soundsource_usc.md#setSourceMask_int_void) should match with this one in at least one bit. Plus, the volume of [sound channel](../../../api/library/engine/class.sound_usc.md#setSourceVolume_int_float_void) in which the sound plays (its number also depends on this mask) should not be equal to 0.
### Return value

Integer, each bit of which specifies a sound channel.
## void setUp ( vec3 up )


Sets an up direction of the player's viewport (i.e. tilt of the player's viewport).


> **Notice:** In case of [PlayerActor](../../../api/library/players/class.playeractor_usc.md), its transformation forces it to recalculate its inner state (position, direction, angles and so on), so the up direction of the player's viewport may become "negative forward". And then transformation will be recalculated by using this direction, causing flip of the basis of the player actor. To avoid such flipping, the theta and phi angles should be [recalculated](../../../api/library/players/class.playeractor_usc.md#setViewDirection_vec3_void) by using the [current viewing orientation](../../../api/library/players/class.playeractor_usc.md#getViewDirection_vec3) of the player.


### Arguments

- *vec3* **up** - New upward direction vector. The vector is normalized to 1.

## vec3 getUp ( )

Returns the current up direction of the player's viewport (i.e. tilt of the player's viewport).
### Return value

Upward direction vector.
## void setVelocity ( vec3 velocity )


Sets a player's velocity.


> **Notice:** In case of [PlayerActor](../../../api/library/players/class.playeractor_usc.md), this function is valid only when the player is not simulated physically ([*setPhysical()*](../../../api/library/players/class.playeractor_usc.md#setPhysical_int_void) is set to 0). If it is, moving PlayerActor is done via accessing its body.


### Arguments

- *vec3* **velocity** - New velocity in units per second.

## vec3 getVelocity ( )

Returns the current velocity of the player.
### Return value

Velocity in units per second.
## void setViewDirection ( vec3 direction )

Sets given view direction vector to the Player instance.
### Arguments

- *vec3* **direction** - A view direction vector.

## vec3 getViewDirection ( )

Returns Player's view direction vector.
### Return value

A view direction vector.
## void setViewportMask ( int mask )

Sets a bit mask for rendering into the viewport. Object surfaces, materials, decals, lights and GUI objects will be rendered into the viewport only if their viewport mask matches the player's one (one matching bit is enough).
### Arguments

- *int* **mask** - Integer, each bit of which is a mask.

## int getViewportMask ( )

Returns the current bit mask for rendering into the viewport. Object surfaces, materials, decals, lights and GUI objects will be rendered into the viewport only if their viewport mask matches the player's one (one matching bit is enough).
### Return value

Viewport mask (integer, each bit of which is a mask).
## void setZFar ( float zfar )

Sets a distance to the far clipping plane of the player's viewing frustum. The default is 10000 units.
### Arguments

- *float* **zfar** - New distance in units. If a negative value is provided, 0 will be used instead.

## float getZFar ( )

Returns the current distance to the far clipping plane of the player's viewing frustum. The default is 10000 units.
### Return value

Distance in units.
## void setZNear ( float znear )

Sets a distance to the near clipping plane of the player's viewing frustum. The default is 0.1 units.
### Arguments

- *float* **znear** - New distance in units. If a negative value is provided, 0 will be used instead.

## float getZNear ( )

Returns the distance to the near clipping plane of the player's viewing frustum. The default is 0.1 units.
### Return value

Distance in units.
## void flushTransform ( )

Forces to immediately set transformations to the player. This function should be called manually after user input has been updated via *updateControls()*.
## void updateControls ( float ifps )

Gets the current player's parameters (impulse, direction, velocity etc) according to user input. After the input has been updated, *flushTransform()* should be called manually to apply it to the player.
### Arguments

- *float* **ifps** - Frame duration in seconds.

## void setFovMode ( int mode )


Sets the value indicating the type of FOV that is used for the player:


- For the standard player, the vertical FOV should be set. In this case, FOV is directly set in [degrees](#setFov_float_void).
- For the physically-based player, the horizontal FOV should be set. In this case, FOV is calculated depending on the [film gate](#setFilmGate_float_void) and [focal length](#setFocalLength_float_void) of the player.


### Arguments

- *int* **mode** - *[FOV_MODE_VERTICAL](../../../api/library/rendering/class.camera_usc.md#FOV_MODE_VERTICAL)* for the player with the vertical FOV; *[FOV_MODE_PHYSICALLY_BASED_CAMERA](../../../api/library/rendering/class.camera_usc.md#FOV_MODE_PHYSICALLY_BASED_CAMERA)* for the physically-based player with the horizontal FOV.

## int getFovMode ( )

Returns the value indicating the type of FOV that is used for the player.
### Return value

0 if the player with the vertical FOV is used; 1 if the physically-based player with the horizontal FOV is used.
## void setFilmGate ( float gate )

Sets a film gate for the physically-based camera with horizontal FOV.
### Arguments

- *float* **gate** - Film gate.

## float getFilmGate ( )

Returns a film gate for the physically-based camera with horizontal FOV.
### Return value

Film gate.
## void setFocalLength ( float length )

Sets a focal length of the physically-based camera lens.
### Arguments

- *float* **length** - Camera lens focal length.

## float getFocalLength ( )

Returns the focal length of the physically-based camera lens.
### Return value

Camera lens focal length.
## mat4 getAspectCorrectedProjection ( int width = -1 , int height = -1 )

Returns projection matrix after correction for the specified aspect ratio (**screen width** / **screen height**). [Currently fixed FOV component](#getFovFixed_int) is taken into account.
### Arguments

- *int* **width** - Screen width.
- *int* **height** - Screen height.

### Return value

Projection matrix after correction for the specified aspect ratio (**screen width** / **screen height**).
## int getFovFixed ( )

Returns a value indicating which FOV component (horizontal or vertical) is currently fixed.
### Return value

Current fixed FOV component, one of the [CAMERA_FOV_FIXED_*](../../../api/library/rendering/class.camera_usc.md#FOV_FIXED_HORIZONTAL) values.
## void addScriptableMaterial ( Material material )


Attaches a new [scriptable material](../../../content/materials/scriptable.md) to the player. To apply a scriptable material globally, use the **[addScriptableMaterial()()](../../../api/library/rendering/class.render_usc.md#addScriptableMaterial_Material_void)** method of the *Render* class. The order of execution for scripts assigned to scriptable materials is defined by material's number in the list of the player.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_usc.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-player.


### Arguments

- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - Scriptable material to be attached to the player.

## void insertScriptableMaterial ( int num , Material material )


Inserts a new [scriptable material](../../../content/materials/scriptable.md) into the list of the ones assigned to the player. To apply a scriptable material globally, use the [*insertScriptableMaterial()*](../../../api/library/rendering/class.render_usc.md#insertScriptableMaterial_int_Material_void) method of the *Render* class. The order of execution for scripts assigned to scriptable materials is defined by material's number in the player's list.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_usc.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-player.

### Arguments

- *int* **num** - Position at which a new scriptable material is to be inserted.
- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - Scriptable material to be inserted.

## void removeScriptableMaterial ( int num )

Removes the [scriptable material](../../../content/materials/scriptable.md) with the specified number from the player.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

## int getNumScriptableMaterials ( )

Returns the total number of [scriptable materials](../../../content/materials/scriptable.md) attached to the player.
### Return value

Total number of scriptable materials attached to the player.
## int findScriptableMaterial ( Material material )


Returns the number of the specified [scriptable material](../../../content/materials/scriptable.md) for the player. This number is player-specific (valid for this player only) and determines the order in which the assigned expressions are executed.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_usc.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-player.


### Arguments

- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - Scriptable material for which a number is to be found.

### Return value

Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int), or -1 if the specified material was not found.
## void setScriptableMaterial ( int num , Material material )


Replaces the [scriptable material](../../../content/materials/scriptable.md) with the specified number with the new scriptable material specified. The number of material determines the order in which the expressions assigned to it are executed. This number is player-specific (valid for this player only).


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_usc.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-player.


### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *[Material](../../../api/library/rendering/class.material_usc.md)* **material** - New scriptable material to replace the one with the specified number.

## Material getScriptableMaterial ( int num )

Returns a [scriptable material](../../../content/materials/scriptable.md) attached to the player by its number.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

### Return value

Scriptable material attached to the player with the specified number.
## void setScriptableMaterialEnabled ( int num , int enabled )

Enables or disables the [scriptable material](../../../content/materials/scriptable.md) with the specified number. When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *int* **enabled** - true to enable the scriptable material with the specified number, false to disable it.

## int getScriptableMaterialEnabled ( int num )

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
## void setMainPlayer ( int player )

Sets a player as a [main player](../../../objects/players/index.md#main_player).
### Arguments

- *int* **player** - true to set the player as the main player, false to unset it.

## int isMainPlayer ( )

Checks if the player is a [main player](../../../objects/players/index.md#main_player).
### Return value

true if the player is a main player; otherwise, false.
## void setListener ( int listener )

Sets the player as the listener.
### Arguments

- *int* **listener** - true to set the player as the listener, false to unset it.

## int isListener ( )

Checks if the player is a [listener](../../../objects/players/index.md#listener).
### Return value

true if the player is a listener; otherwise, false.
## void setProjectionMode ( int mode )

Sets the projection mode: orthographic or perspective.
### Arguments

- *int* **mode** - The projection mode, 1 for the orthographic mode; 0 for the perspective mode.

## int getProjectionMode ( )

Returns the current projection mode: orthographic or perspective.
### Return value

The projection mode, 1 for the orthographic mode; 0 for the perspective mode.
## void setOrthoHeight ( float height )

Sets the height of the camera with the orthographic [projection mode](#getProjectionMode_int) enabled.
### Arguments

- *float* **height** - The orthographic camera height.

## float getOrthoHeight ( )

Returns the current height of the camera with the orthographic [projection mode](#getProjectionMode_int) enabled.
### Return value

The orthographic camera height.
