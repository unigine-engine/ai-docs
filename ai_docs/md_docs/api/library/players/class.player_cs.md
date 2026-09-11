# Unigine.Player Class (CS)

**Inherits from:** Node


This class is used to create cameras that view the world. When you create a new player, it creates a [camera](../../../api/library/rendering/class.camera_cs.md) and specifies controls, [masks](#player_masks), postprocess materials for this camera.


Players' viewing frustum is defined by a [near clipping plane](#setZNear_float_void), [far clipping plane](#setZFar_float_void) and the [field of view](#setFov_float_void). Note that if you set up a custom [projection](#setProjection_mat4_void) matrix and after that call any of these functions:


- [*setFov()*](#setFov_float_void)
- [*setZFar()*](#setZFar_float_void)
- [*setZNear()*](#setZNear_float_void)


your custom matrices will be overwritten.


Players cannot have a parent node; they always use the world coordinates for their transformations. The only exception is [PlayerDummy](../../../api/library/players/class.playerdummy_cs.md).


### Player Masks


Objects, decals and lights can be selectively displayed in the player viewport. To be displayed, their viewport mask should be matching with the player's [viewport mask](#setViewportMask_int_void) (one matching bit is enough):


- Object [surface viewport mask](../../../api/library/objects/class.object_cs.md#setViewportMask_int_int_void) or [decal viewport mask](../../../api/library/decals/class.decal_cs.md#setViewportMask_int_void)
- [Light viewport mask](../../../api/library/lights/class.light_cs.md#setViewportMask_int_void) to light the object/decal
- [Material viewport mask](../../../api/library/rendering/class.material_cs.md#setViewportMask_int_void) to render the object/decal material


Reflections can also be selectively rendered into the viewport: an object can be rendered without reflection or reflection without an object. For that, the player's [reflection viewport mask](#setReflectionViewportMask_int_void) should match:


- Reflection mask of the reflecting material
- [Viewport mask](../../../api/library/rendering/class.material_cs.md#setViewportMask_int_void) of the reflecting material
- Object [surface viewport mask](../../../api/library/objects/class.object_cs.md#setViewportMask_int_int_void)
- [Material viewport mask](../../../api/library/rendering/class.material_cs.md#setViewportMask_int_void) of the reflected material
- [Light viewport mask](../../../api/library/lights/class.light_cs.md#setViewportMask_int_void)


That is enough to render reflection from the object without an object itself. If an object needs to be present as well, all these conditions should simply go together with above mentioned ones.


To render an object without reflection, simply either its [material viewport mask](../../../api/library/rendering/class.material_cs.md#setViewportMask_int_void) or object [surface viewport mask](../../../api/library/objects/class.object_cs.md#setViewportMask_int_int_void) should not match the player's [reflection viewport mask](#setReflectionViewportMask_int_void).


Players also can have sound source and sound reverberation masks. As well as for viewports, corresponding masks of the *Player* object should match with [SoundReverb](../../../api/library/sounds/class.soundreverb_cs.md#setReverbMask_int_void) and [SoundSource](../../../api/library/sounds/class.soundsource_cs.md#setSourceMask_int_void) masks.


### Perspective and Orthographic Projection


Depending on your project's requirements you can set your player to use [perspective](../../../principles/world_management/index.md#camera_perspective) or [orthographic](../../../principles/world_management/index.md#camera_orthographic) projection. This can be done via the [*setProjection()*](#setProjection_mat4_void) method.


For example, you can use the following code to set up **orthographic projection** or **perspective projection** for your current game player depending on a flag value:


```csharp
// calculates a projection matrix for the specified parameters (angles for left, right, top, and bottom are in degrees)
mat4 calculateProjection(float left, float right, float bottom, float top, float zNear, float zFar, float zoom)
{
	left = zNear * MathLib.Tan(MathLib.DEG2RAD * (left * zoom));
	right = zNear * MathLib.Tan(MathLib.DEG2RAD * (right * zoom));
	top = zNear * MathLib.Tan(MathLib.DEG2RAD * (top * zoom));
	bottom = zNear * MathLib.Tan(MathLib.DEG2RAD * (bottom * zoom));

	return MathLib.Frustum(left, right, bottom, top, zNear, zFar);
}

/* ... */
Player player;

// ortho flag - change this value to switch projection type
bool ortho = false;

private void Init()
{

	/* ... */

	// disabling default aspect correction for the main window
	// to ensure that the custom projection is applied properly
	WindowManager.MainWindow.AspectCorrection = false;

	// getting the current player
	player = Game.Player;

	// setting up near and far clipping planes and aspect ratio
	float znear = 0.001f;
	float zfar = 10000.0f;
	float aspect = 16.0f / 9.0f;

	float fov = 60.0f;
	float ortho_height = 2.0f;

	player.ZNear = znear;
	player.ZFar = zfar;
	player.Fov = fov;
	player.OrthoHeight = ortho_height;

	if (ortho)
	{
		// setting up orthographic projection
		player.ProjectionMode = Camera.PROJECTION_MODE.ORTHOGRAPHIC;

		// or setting up orthographic projection manually
		player.Projection = MathLib.Ortho(-ortho_height / 2.0f, ortho_height / 2.0f, -ortho_height / 2.0f, ortho_height / 2.0f, znear, zfar);
	}
	else
	{
		// setting up perspective projection
		player.ProjectionMode = Camera.PROJECTION_MODE.PERSPECTIVE;

		// or setting up a projection matrix manually
		player.Projection = MathLib.Perspective(fov, aspect, znear, zfar);

		// or calculating a projection matrix for FullfHD/4K resolution
		mat4 projection = calculateProjection(-22.5f, 22.5f, -13.1f, 13.1f, 1.0f, 200000.0f, 1.0f);
		// and setting up custom calculated projection manually
		player.Projection = projection;
	}
}


```


### Getting Euler Angles for an Active Camera


Sometimes it might be necessary to get current rotation of the active camera as a set of Euler angles. When we talk about axes in UNIGINE we assume that:


|  |  |
|---|---|
| - **X** axis points to the *right* giving us a **pitch** angle. - **Y** axis points *forward* giving us a **roll** angle. - **Z** axis points *up* giving us a **yaw** (heading) angle. | ![](../../../code/fundamentals/matrices/object_directions.png) *Object Direction Vectors* |


To get the Euler angles we should use [*decomposeRotationZXY()*](../../../api/library/math/math.matrix_cs.md#decomposeRotationZXY_const_mat3_ref_vec3) also known as Cardan angles (**yaw** is independent, then we get **pitch** and in the end, **roll**). But, there is one thing to be taken into account - cameras have a different system:


|  |  |
|---|---|
| - **X** axis points to the *right* giving us a **pitch** angle. - **Y** axis points *up* giving us a **yaw** (heading) angle. - **Z** axis points *backward* giving us a **-roll** angle. | ![](../../../code/fundamentals/matrices/camera_directions.png) *Camera Direction Vectors* |


To compensate it, we need to rotate our camera **-90** degrees around **X** axis.


```csharp
#if UNIGINE_DOUBLE
using Mat4 = Unigine.dmat4;
#else
	using Mat4 = Unigine.mat4;
#endif

		// getting the current view matrix of the current camera
		Mat4 currentModelview = Game.Player.Camera.IModelview;

		// decomposing rotation matrix of the camera (with compensation)
		vec3 euler = MathLib.DecomposeRotationZXY(new mat3(currentModelview * new Mat4(MathLib.RotateX(-90.0f))));
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


In this example a [PlayerSpectator class](../../../api/library/players/class.playerspectator_cs.md) instance (which inherited from Player class) created and added to the current scene. Here is a code from the `AppWorldLogic.cs` file.


```csharp
#if UNIGINE_DOUBLE
using Vec3 = Unigine.dvec3;
#else
using Vec3 = Unigine.vec3;
#endif

{

		PlayerSpectator playerSpectator;

		/* ... */

	private void Init()
	{

		/* ... */
		playerSpectator = new PlayerSpectator();

		// specify the necessary parameters: FOV, ZNear, ZFar, view direction vector and PlayerSpectator position.
		playerSpectator.Fov = 90.0f;
		playerSpectator.ZNear = 0.1f;
		playerSpectator.ZFar = 10000.0f;
		playerSpectator.ViewDirection = new vec3(0.0f, 1.0f, 0.0f);
		playerSpectator.WorldPosition = new Vec3(-1.6f, -1.7f, 1.7f);

		// set the Player to the Game singleton instance
		Game.Player = playerSpectator;
	}

}


```


## Player Class

### Properties

## Camera Camera

The camera instance of the player node.
## 🔒︎ int NumScriptableMaterials

The total number of [scriptable materials](../../../content/materials/scriptable.md) attached to the player.
## bool MainPlayer

The A value indicating indicating if the player is a [main player](../../../objects/players/index.md#main_player).
## Controls Controls

The A controls smart pointer that holds settings of input controls relevant to the player.
## bool Controlled

The A value indicating whether player controls are disabled (player does not respond to them) or enabled.
## vec3 Velocity

The current velocity of the player.
## vec3 ViewDirection

The Player's view direction vector.
## int ReverbMask

The current bit mask that determines what [reverberation zones](../../../api/library/sounds/class.soundreverb_cs.md) can be heard. For sound to reverberate, at least one bit of this mask should match with a [reverb mask of the sound source](../../../api/library/sounds/class.soundsource_cs.md#setReverbMask_int_void) and a [reverb mask of the reverberation zone](../../../api/library/sounds/class.soundreverb_cs.md#setReverbMask_int_void). (Masks of a sound source and reverberation zone can match with the player's one in different bits, not necessarily one).
## int SourceMask

The source mask that determines sound sources, which can be heard. for a sound source to be heard, its mask should match with this one in at least one bit. plus, the volume of sound channel in which the sound plays (its number also depends on this mask) should not be equal to 0.
## int ReflectionViewportMask

The current bit mask for rendering reflections into the viewport. reflections are rendered in the viewport if masks of reflective materials match this one (one bit at least).
## int ViewportMask

The current viewport mask. object surfaces, materials, decals, lights and gui objects will be rendered into the viewport only if their viewport mask matches the player's one (one matching bit is enough).
## bool ObliqueFrustum

The A value indicating if the viewing frustum is oblique.
## vec4 ObliqueFrustumPlane

The
The oblique near clipping plane of the viewing frustum.


```csharp
#if UNIGINE_DOUBLE
using Vec4 = Unigine.dvec4;
#else
using Vec4 = Unigine.vec4;
#endif

{

	private void Update()
	{

 		float time = Game.Time;

		// initializing a plane to be set as a near clipping plane
		Vec4 plane = new Vec4(1.0f, 1.0f, 1.0f, 1.0f + MathLib.Sin(time) * 4.0f);

		// getting a player
		Player player = Game.Player;
		if (player != null)
		{
			// enabling oblique frustum
			player.ObliqueFrustum = true;

			// setting our plane as an oblique near clipping plane
			player.ObliqueFrustumPlane = plane;
		}
	}

}


```


## vec3 Up

The current up direction of the player's viewport (i.e. tilt of the player's viewport).
## float ZFar

The current distance to the far clipping plane of the player's viewing frustum. the default is 10000 units.
## float ZNear

The distance to the near clipping plane of the player's viewing frustum. the default is 0.1 units.
## float FocalLength

The focal length of the physically-based camera lens.
## float FilmGate

The A film gate for the physically-based camera with horizontal fov.
## float Fov

The
Current vertical field of view of the player.


> **Notice:** Horizontal FOV cannot be used since it varies depending on the viewport's aspect ratio. Setting FOV recalculates projection matrix with **aspect ratio = 1**.


You can use the following formula to calculate horizontal FOV from the vertical one for the given aspect ratio (width/height): **FOV_h = 2 � atan ( (width / height) � tan(FOV_v / 2))**.


## 🔒︎ Camera.FOV_FIXED FovFixed

The A value indicating which fov component (horizontal or vertical) is currently fixed.
## Camera.FOV_MODE FovMode

The Sets the value indicating the type of FOV that is used for the player.
## mat4 Projection

The current projection matrix with unit (1.0) aspect ratio.
## bool Listener

The Checks if the player is a [listener](../../../objects/players/index.md#listener).
## float OrthoHeight

The height of the camera with the orthographic [projection mode](#getProjectionMode_int) enabled.
## Camera.PROJECTION_MODE ProjectionMode

The projection mode, *[PROJECTION_MODE.ORTHOGRAPHIC](../../../api/library/rendering/class.camera_cs.md#PROJECTION_MODE_ORTHOGRAPHIC)* for the orthographic mode; *[PROJECTION_MODE.PERSPECTIVE](../../../api/library/rendering/class.camera_cs.md#PROJECTION_MODE_PERSPECTIVE)* for the perspective mode.
### Members

---

## void GetDirectionFromScreen ( out Vec3 p0 , out Vec3 p1 , int mouse_x , int mouse_y , int screen_x , int screen_y , int screen_width , int screen_height )


Casts the ray to a certain position on the screen and returns coordinates of the start (p0) and end (p1) points of the ray.


```csharp
Vec3 p0, p1;

// get the current player (camera)
Player player = Game.Player;
if (player == null)
	return;

// get width and height of the current application window
EngineWindow main_window = WindowManager.MainWindow;
if (!main_window)
{
	Engine.Quit();
	return;
}

ivec2 main_size = main_window.ClientSize;

// get the current X and Y coordinates of the mouse pointer
int mouse_x = Gui.GetCurrent().MouseX;
int mouse_y = Gui.GetCurrent().MouseY;

// get the mouse direction from the player's position (p0) to the mouse cursor pointer (p1)
player.GetDirectionFromScreen(out p0, out p1, mouse_x, mouse_y, 0, 0, main_size.x, main_size.y);


```


### Arguments

- *out Vec3* **p0** - Start coordinates of the ray.
- *out Vec3* **p1** - End coordinates of the ray.
- *int* **mouse_x** - X-coordinate of the mouse position.
- *int* **mouse_y** - Y-coordinate of the mouse position.
- *int* **screen_x** - X-coordinate of the screen position.
- *int* **screen_y** - Y-coordinate of the screen position.
- *int* **screen_width** - Screen width.
- *int* **screen_height** - Screen height.

## vec3 GetDirectionFromScreen ( int mouse_x , int mouse_y , int screen_x , int screen_y , int screen_width , int screen_height )


Casts the ray to a certain position on the screen and returns a vector in the direction of this position.


```csharp
// get width and height of the current application window
EngineWindow main_window = WindowManager.MainWindow;
if (!main_window)
{
	Engine.Quit();
	return;
}

ivec2 main_size = main_window.ClientSize;
// initializing points of the ray from player's position in the direction pointed by the mouse cursor
Vec3 p0 = player.WorldPosition;
Vec3 p1 = p0 + new Vec3(player.GetDirectionFromScreen(Gui.GetCurrent().MouseX, Gui.GetCurrent().MouseY, 0, 0, main_size.x, main_size.y)) * 100;


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
## mat4 GetProjectionFromScreen ( int x0 , int y0 , int x1 , int y1 , int screen_width , int screen_height )

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
## int GetScreenPosition ( out int x , out int y , vec3 point , int screen_width , int screen_height )

Projects the point in world coordinates to the screen. Screen coordinates are written into the first 2 variables passed to the method (in pixels).


```csharp
// get relative screen position of a world-space point (world_point_position)
EngineWindowViewport mainWindow = WindowManager.MainWindow;
ivec2 clientRenderSize = mainWindow.ClientRenderSize;
Game.Player.GetScreenPosition(out int screenX, out int screenY, worldPointPosition, clientRenderSize.x, clientRenderSize.y);
vec2 relative_pos = new vec2(screenX, screenY) / clientRenderSize;

```


### Arguments

- *out int* **x** - X-coordinate of the screen position (in pixels).
- *out int* **y** - Y-coordinate of the screen position (in pixels).
- *vec3* **point** - Point coordinates.
- *int* **screen_width** - Screen width.
- *int* **screen_height** - Screen height.

### Return value

1 if the point has been projected successfully; otherwise, 0.
## void FlushTransform ( )

Forces to immediately set transformations to the player. This function should be called manually after user input has been updated via *updateControls()*.
## void UpdateControls ( float ifps )

Gets the current player's parameters (impulse, direction, velocity etc) according to user input. After the input has been updated, *flushTransform()* should be called manually to apply it to the player.
### Arguments

- *float* **ifps** - Frame duration in seconds.

## mat4 GetAspectCorrectedProjection ( int width = -1 , int height = -1 )

Returns projection matrix after correction for the specified aspect ratio (**screen width** / **screen height**). [Currently fixed FOV component](#getFovFixed_int) is taken into account.
### Arguments

- *int* **width** - Screen width.
- *int* **height** - Screen height.

### Return value

Projection matrix after correction for the specified aspect ratio (**screen width** / **screen height**).
## void AddScriptableMaterial ( Material material )


Attaches a new [scriptable material](../../../content/materials/scriptable.md) to the player. To apply a scriptable material globally, use the **[AddScriptableMaterial()](../../../api/library/rendering/class.render_cs.md#addScriptableMaterial_Material_void)** method of the *Render* class. The order of execution for scripts assigned to scriptable materials is defined by material's number in the list of the player.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cs.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-player.


### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Scriptable material to be attached to the player.

## void InsertScriptableMaterial ( int num , Material material )


Inserts a new [scriptable material](../../../content/materials/scriptable.md) into the list of the ones assigned to the player. To apply a scriptable material globally, use the [*insertScriptableMaterial()*](../../../api/library/rendering/class.render_cs.md#insertScriptableMaterial_int_Material_void) method of the *Render* class. The order of execution for scripts assigned to scriptable materials is defined by material's number in the player's list.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cs.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-player.

### Arguments

- *int* **num** - Position at which a new scriptable material is to be inserted.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Scriptable material to be inserted.

## void RemoveScriptableMaterial ( int num )

Removes the [scriptable material](../../../content/materials/scriptable.md) with the specified number from the player.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

## int FindScriptableMaterial ( Material material )


Returns the number of the specified [scriptable material](../../../content/materials/scriptable.md) for the player. This number is player-specific (valid for this player only) and determines the order in which the assigned expressions are executed.


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cs.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-player.


### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Scriptable material for which a number is to be found.

### Return value

Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int), or -1 if the specified material was not found.
## void SetScriptableMaterial ( int num , Material material )


Replaces the [scriptable material](../../../content/materials/scriptable.md) with the specified number with the new scriptable material specified. The number of material determines the order in which the expressions assigned to it are executed. This number is player-specific (valid for this player only).


> **Notice:** Scriptable materials [applied globally](../../../api/library/rendering/class.render_cs.md#addScriptableMaterial_Material_void) have their expressions executed before the ones that are applied per-player.


### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - New scriptable material to replace the one with the specified number.

## Material GetScriptableMaterial ( int num )

Returns a [scriptable material](../../../content/materials/scriptable.md) attached to the player by its number.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

### Return value

Scriptable material attached to the player with the specified number.
## void SetScriptableMaterialEnabled ( int num , bool enabled )

Enables or disables the [scriptable material](../../../content/materials/scriptable.md) with the specified number. When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *bool* **enabled** - true to enable the scriptable material with the specified number, false to disable it.

## bool GetScriptableMaterialEnabled ( int num )

Returns a value indicating if the [scriptable material](../../../content/materials/scriptable.md) with the specified number attached to the player is enabled (active). When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

### Return value

true if the scriptable material with the specified number is enabled; otherwise, false.
## void SwapScriptableMaterials ( int num_0 , int num_1 )


Swaps two [scriptable materials](../../../content/materials/scriptable.md) with specified numbers. The number of material determines the order in which the expressions assigned to it are executed.


> **Notice:** The number is player-specific (valid for this player only).


### Arguments

- *int* **num_0** - Number of the first scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *int* **num_1** - Number of the second scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

## void ClearScriptableMaterials ( )

Clears all [scriptable materials](../../../content/materials/scriptable.md) attached to the player.
## void GetDirectionFromMainWindow ( out Vec3 p0 , out Vec3 p1 , int mouse_x , int mouse_y )

Casts the ray to a certain position on the screen and returns coordinates of the start (p0) and end (p1) points of the ray relative to the current main window.
### Arguments

- *out Vec3* **p0** - Start coordinates of the ray.
- *out Vec3* **p1** - End coordinates of the ray.
- *int* **mouse_x** - X-coordinate of the mouse position in world coordinates.
- *int* **mouse_y** - Y-coordinate of the mouse position in world coordinates.

## vec3 GetDirectionFromMainWindow ( int mouse_x , int mouse_y )

Casts the ray to a certain position on the screen and returns a vector in the direction of this position relative to the current main window.
### Arguments

- *int* **mouse_x** - X-coordinate of the mouse position in world coordinates.
- *int* **mouse_y** - Y-coordinate of the mouse position in world coordinates.

### Return value

Vector coordinates.
## void GetDirectionFromWindow ( out Vec3 p0 , out Vec3 p1 , int mouse_x , int mouse_y , EngineWindowViewport window )

Casts the ray to a certain position on the screen and returns coordinates of the start (p0) and end (p1) points of the ray relative to the specified window viewport.
### Arguments

- *out Vec3* **p0** - Start coordinates of the ray.
- *out Vec3* **p1** - End coordinates of the ray.
- *int* **mouse_x** - X-coordinate of the mouse position in world coordinates.
- *int* **mouse_y** - Y-coordinate of the mouse position in world coordinates.
- *[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cs.md)* **window** - Window viewport relative to which the directon is returned.

## vec3 GetDirectionFromWindow ( int mouse_x , int mouse_y , EngineWindowViewport window )

Casts the ray to a certain position on the screen and returns a vector in the direction of this position relative to the specified window viewport.
### Arguments

- *int* **mouse_x** - X-coordinate of the mouse position in world coordinates.
- *int* **mouse_y** - Y-coordinate of the mouse position in world coordinates.
- *[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cs.md)* **window** - Window viewport relative to which the directon is returned.

### Return value

Vector coordinates.
## mat4 GetProjectionFromMainWindow ( int x0 , int y0 , int x1 , int y1 )

Creates a projection matrix out of 2 screen positions relative to the current main window. This is required for the frame selection.
### Arguments

- *int* **x0** - X-coordinate of the first screen position.
- *int* **y0** - Y-coordinate of the first screen position.
- *int* **x1** - X-coordinate of the second screen position.
- *int* **y1** - Y-coordinate of the second screen position.

### Return value

Projection matrix.
## mat4 GetProjectionFromWindow ( int x0 , int y0 , int x1 , int y1 , EngineWindowViewport window )

Creates a projection matrix out of 2 screen positions relative to the specified window viewport. This is required for the frame selection.
### Arguments

- *int* **x0** - X-coordinate of the first screen position.
- *int* **y0** - Y-coordinate of the first screen position.
- *int* **x1** - X-coordinate of the second screen position.
- *int* **y1** - Y-coordinate of the second screen position.
- *[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cs.md)* **window** - Window viewport relative to which the projection is returned.

### Return value

Projection matrix.
## int GetMainWindowPosition ( out int x , out int y , vec3 point )


Projects the point in world coordinates relative to the main window. The coordinates are written into the first 2 variables passed to the method (in pixels).


```csharp
// get relative screen position of a world-space point (worldPointPosition)
ivec2 clientRenderSize = WindowManager.MainWindow.ClientRenderSize;
Game.Player.GetMainWindowPosition(out int screenX, out int screenY, worldPointPosition);
vec2 relative_pos = new vec2(screenX, screenY) / clientRenderSize;

```


### Arguments

- *out int* **x** - X-coordinate of the screen position (in pixels).
- *out int* **y** - Y-coordinate of the screen position (in pixels).
- *vec3* **point** - Point coordinates.

### Return value

1 if the point has been projected successfully; otherwise, 0.
## int GetWindowPosition ( out int x , out int y , vec3 point , EngineWindowViewport window )


Projects the point in world coordinates relative to the specified window viewport. The coordinates are written into the first 2 variables passed to the method (in pixels).


```csharp
// get relative screen position of a world-space point (world_point_position)
EngineWindowViewport mainWindow = WindowManager.MainWindow;
ivec2 clientRenderSize = mainWindow.ClientRenderSize;
Game.Player.GetWindowPosition(out int screenX, out int screenY, worldPointPosition, mainWindow);
vec2 relativePos = new vec2(screenX, screenY) / clientRenderSize;

```


### Arguments

- *out int* **x** - X-coordinate of the screen position (in pixels).
- *out int* **y** - Y-coordinate of the screen position (in pixels).
- *vec3* **point** - Point coordinates.
- *[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cs.md)* **window** - Window viewport relative to which the projection is returned.

### Return value

1 if the point has been projected successfully; otherwise, 0.
