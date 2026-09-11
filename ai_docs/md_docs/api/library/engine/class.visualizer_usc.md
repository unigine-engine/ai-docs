# Unigine::Visualizer Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


Controls visualizer-related settings. The visualizer is used to render mesh wireframe, object bounding boxes, and all sorts of visual helpers (such as physical collision shapes, joints, etc.).


- 3D visualizer (engine.visualizer.render*3D()) is rendered based on scene depth.
- 2D visualizer (engine.visualizer.render*2D()) is rendered atop of everything else.


To render 3D objects atop of the scene, you can transform 3D space coordinates into screen space and render lines and triangles using 2D visualizer functions.


#### Usage Example


To render a vector, do the following:


```cpp
// my_world.usc

Player player;  // In-game camera.

int init() {

player = new PlayerSpectator();   // Create a new player
engine.game.setPlayer(player);	// used in the game.

...

return 1;
}

int update() {

// The player position is updated

...

// Call a rendering function
engine.visualizer.renderVector(vec3_zero, vec3(1.0f,0.0f,0.0f), vec4_one, 0.25f, 0);

return 1;
}

```


## Visualizer Class

### Members

## void setTextureName ( string name )

Sets a new path to auxiliary visualizer texture. This texture is applied to **[billboards](#renderBillboard3D_Vec3_float_vec4_int_float_int_void)** and **[handlers](#renderNodeHandler_Node_float_void)** (rendered via *[renderBillboard3D()()](../../...md#renderBillboard3D_Vec3_float_vec4_int_float_int_void)* and *[renderNodeHandler()()](../../...md#renderNodeHandler_Node_float_void)*). To restore the default texture, pass an empty string **("")**.
### Arguments

- *string* **name** - The path to the texture.

## const char * getTextureName () const

Returns the current path to auxiliary visualizer texture. This texture is applied to **[billboards](#renderBillboard3D_Vec3_float_vec4_int_float_int_void)** and **[handlers](#renderNodeHandler_Node_float_void)** (rendered via *[renderBillboard3D()()](../../...md#renderBillboard3D_Vec3_float_vec4_int_float_int_void)* and *[renderNodeHandler()()](../../...md#renderNodeHandler_Node_float_void)*). To restore the default texture, pass an empty string **("")**.
### Return value

Current path to the texture.
## void setSize ( )

Sets a new handler size. All handlers have the same size.
### Arguments

- **size** - The handler size, in pixels.

## getSize () const

Returns the current handler size. All handlers have the same size.
### Return value

Current handler size, in pixels.
## void setEnabled ( int enabled )

Sets a new value indicating if the visualizer (rendering of helper objects like handlers and bound boxes) is enabled.
### Arguments

- *int* **enabled** - The value indicating if the visualizer is enabled

## int isEnabled () const

Returns the current value indicating if the visualizer (rendering of helper objects like handlers and bound boxes) is enabled.
### Return value

Current value indicating if the visualizer is enabled
## void setMode ( int mode )

Sets a new [visualizer mode](#MODE) controlling the way all visual helpers are displayed. You can choose to display Visualizer with or without depth testing, or turn it off completely.
### Arguments

- *int* **mode** - The visualizer mode.

## int getMode () const

Returns the current [visualizer mode](#MODE) controlling the way all visual helpers are displayed. You can choose to display Visualizer with or without depth testing, or turn it off completely.
### Return value

Current visualizer mode.
## int getNumHandlers () const

Returns the current total number of handlers.
> **Notice:** The total number of handlers may change every frame depending on the camera transforms (i.e. how many handlers are visible in the current frame), therefore it is not recommended to save and reuse this value.


### Return value

Current total number of handlers.
---

## void engine.visualizer. clear ( )


Clears all internal primitives created by calls to *renderSmth* functions. These primitives are accumulated in the internal buffer and then rendered together.


> **Notice:** This method can be used to render several viewports with visualizer.


## void engine.visualizer. renderPoint2D ( vec2 v , float size , vec4 color , float order = 0.0f , float duration = 0.0f )

Renders a 2D point of a given size and color. 2D points are rendered in the screen plane; coordinates of the upper left corner are (0; 0), of the lower right corner�(1; 1).
### Arguments

- *vec2* **v** - Point coordinates.
- *float* **size** - Point size.
- *vec4* **color** - Color, in which the point will be rendered.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void engine.visualizer. renderPoint3D ( Vec3 v , float size , vec4 color , int screen_space = false , float duration = 0.0f , int depth_test = true )

Renders a 3D point of a given size and color. 3D points are rendered in the world space.
### Arguments

- *Vec3* **v** - Point coordinates.
- *float* **size** - Point size in range [0;1]. The point size is set in proportion to the screen resolution.
- *vec4* **color** - Point color.
- *int* **screen_space** - Flag indicating the type of dimensions to be used:

  - **false** - use the world space dimensions
  - **true** - use the screen space dimensions
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderLine2D ( vec2 v0 , vec2 v1 , vec4 color , float order = 0.0f , float duration = 0.0f )

Renders a 2D line of a given color. 2D lines are rendered in the screen plane; coordinates of the upper left corner are **(0; 0)**, of the lower right corner � **(1; 1)**.
### Arguments

- *vec2* **v0** - Starting point of the line.
- *vec2* **v1** - Ending point of the line.
- *vec4* **color** - Line color.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void engine.visualizer. renderLine3D ( Vec3 v0 , Vec3 v1 , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a 3D line of a given color. 3D lines are rendered in the world space.
### Arguments

- *Vec3* **v0** - Starting point of the line.
- *Vec3* **v1** - Ending point of the line.
- *vec4* **color** - Line color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderLine2D ( vec2 v0 , vec2 v1 , vec2 v2 , vec4 color , float order = 0.0f , float duration = 0.0f )

Renders a 2D line of a given color by using 3 points. 2D lines are rendered in the screen plane; coordinates of the upper left corner are **(0; 0)**, of the lower right corner � **(1; 1)**.
### Arguments

- *vec2* **v0** - Coordinates of the starting point of the line.
- *vec2* **v1** - Coordinates of the intermediate point of the line.
- *vec2* **v2** - Coordinates of the ending point of the line.
- *vec4* **color** - Ending point of the line.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void engine.visualizer. renderLine3D ( Vec3 v0 , Vec3 v1 , Vec3 v2 , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a 3D line of a given color. 3D lines are rendered in the world space.
### Arguments

- *Vec3* **v0** - Coordinates of the starting point of the line.
- *Vec3* **v1** - Coordinates of the intermediate point of the line.
- *Vec3* **v2** - Coordinates of the ending point of the line.
- *vec4* **color** - Line color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderLine2D ( vec2 v0 , vec2 v1 , vec2 v2 , vec2 v3 , vec4 color , float order = 0.0f , float duration = 0.0f )

Renders a 2D line of a given color. 2D lines are rendered in the screen plane; coordinates of the upper left corner are **(0; 0)**, of the lower right corner � **(1; 1)**.
### Arguments

- *vec2* **v0** - Coordinates of the starting point of the line.
- *vec2* **v1** - Coordinates of the first intermediate point of the line.
- *vec2* **v2** - Coordinates of the second intermediate point of the line.
- *vec2* **v3** - Coordinates of the ending point of the line.
- *vec4* **color** - Color, in which the line will be rendered.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void engine.visualizer. renderLine3D ( Vec3 v0 , Vec3 v1 , Vec3 v2 , Vec3 v3 , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a 3D line of a given color. 3D lines are rendered in the world space.
### Arguments

- *Vec3* **v0** - Coordinates of the starting point of the line.
- *Vec3* **v1** - Coordinates of the first intermediate point of the line.
- *Vec3* **v2** - Coordinates of the second intermediate point of the line.
- *Vec3* **v3** - Coordinates of the ending point of the line.
- *vec4* **color** - Color, in which the line will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderTriangle2D ( vec2 v0 , vec2 v1 , vec2 v2 , vec4 color , float order = 0.0f , float duration = 0.0f )

Renders a 2D triangle of a given color. 2D triangles are rendered in the screen plane; coordinates of the upper left corner are **(0; 0)**, of the lower right corner�**(1; 1)**.
### Arguments

- *vec2* **v0** - Coordinates of the first vertex.
- *vec2* **v1** - Coordinates of the second vertex.
- *vec2* **v2** - Coordinates of the third vertex.
- *vec4* **color** - Triangle color.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void engine.visualizer. renderTriangle3D ( Vec3 v0 , Vec3 v1 , Vec3 v2 , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a 3D triangle of a given color. 3D triangles are rendered in the world space.
### Arguments

- *Vec3* **v0** - Coordinates of the first vertex.
- *Vec3* **v1** - Coordinates of the second vertex.
- *Vec3* **v2** - Coordinates of the third vertex.
- *vec4* **color** - Triangle color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderQuad2D ( vec2 v0 , vec2 v1 , vec2 v2 , vec2 v3 , vec4 color , float order = 0.0f , float duration = 0.0f )

Renders a 2D quad of a given color. 2D quads are rendered in the screen plane; coordinates of the upper left corner are **(0; 0)**, of the lower right corner�**(1; 1)**.
### Arguments

- *vec2* **v0** - Coordinates of the first vertex.
- *vec2* **v1** - Coordinates of the second vertex.
- *vec2* **v2** - Coordinates of the third vertex.
- *vec2* **v3** - Coordinates of the fourth vertex.
- *vec4* **color** - Color, in which the quad will be rendered.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void engine.visualizer. renderQuad3D ( Vec3 v0 , Vec3 v1 , Vec3 v2 , Vec3 v3 , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a 3D quad of a given color. 3D quads are rendered in the world space.
### Arguments

- *Vec3* **v0** - Coordinates of the first vertex.
- *Vec3* **v1** - Coordinates of the second vertex.
- *Vec3* **v2** - Coordinates of the third vertex.
- *Vec3* **v3** - Coordinates of the fourth vertex.
- *vec4* **color** - Color, in which the quad will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderBillboard3D ( Vec3 v , float size , vec4 texcoord , int screen_space = false , float duration = 0.0f , int depth_test = true )

Renders a 3D billboard of the specified size. You can customize billboard image via **[setTextureName()()](../../...md#setTextureName_cstr_void)**.
### Arguments

- *Vec3* **v** - Coordinates of the billboard.
- *float* **size** - The billboard size in units (meters).
- *vec4* **texcoord** - The billboard texture coordinates, consisting of two pairs of vector elements (x, y, z, w):

  - x - texture size along the X axis in range [0.0f; 1.0f]
  - y - texture size along the Y axis in range [0.0f; 1.0f]
  - z - offset of the texture's starting position along the X axis in range [0.0f; 1.0f]
  - w - offset of the texture's starting position along the Y axis [0.0f; 1.0f]
- *int* **screen_space** - Flag indicating the type of dimensions to be used:

  - **false** - use the world space dimensions
  - **true** - use the screen space dimensions
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderVector ( Vec3 position_start , Vec3 position_end , vec4 color , float arrow_size = 0.25f , int screen_space = false , float duration = 0.0f , int depth_test = true )

Renders a vector of a given color.
### Arguments

- *Vec3* **position_start** - Coordinates of the vector origin.
- *Vec3* **position_end** - Coordinates of the vector target.
- *vec4* **color** - Vector color.
- *float* **arrow_size** - Relative length of the arrowhead (cone) with respect to the total vector length. For example, the default value of 0.25f means that the arrowhead occupies 25% of the overall arrow length.
- *int* **screen_space** - Flag indicating the type of dimensions to be used:

  - **false** - use the world space dimensions
  - **true** - use the screen space dimensions
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderDirection ( Vec3 position , vec3 direction , vec4 color , float arrow_size = 0.25f , int screen_space = true , float duration = 0.0f , int depth_test = true )

Renders a direction vector of a given color.
### Arguments

- *Vec3* **position** - Coordinates of the vector origin.
- *vec3* **direction** - Target vector direction.
- *vec4* **color** - Vector color.
- *float* **arrow_size** - Relative length of the arrowhead (cone) with respect to the total vector length. For example, the default value of 0.25f means that the arrowhead occupies 25% of the overall arrow length.
- *int* **screen_space** - Flag indicating the type of dimensions to be used:

  - **false** - use the world space dimensions
  - **true** - use the screen space dimensions
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderBox ( vec3 size , Mat4 transform , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a box of a given color.
### Arguments

- *vec3* **size** - Dimensions of the box.
- *Mat4* **transform** - Transformation matrix, which is used to position the box.
- *vec4* **color** - Color, in which the box will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderFrustum ( mat4 projection , Mat4 transform , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a wireframe frustum of a given color.
### Arguments

- *mat4* **projection** - Projection matrix used to transform the coordinates.
- *Mat4* **transform** - Transformation matrix used to position the frustum.
- *vec4* **color** - Color, in which the frustum will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderCircle ( float radius , Mat4 transform , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a wireframe circle of a given color.
### Arguments

- *float* **radius** - Radius of the circle.
- *Mat4* **transform** - Transformation matrix used to position the circle.
- *vec4* **color** - Circle color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderSector ( float radius , float angle , Mat4 transform , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a wireframe sector of a given color.
### Arguments

- *float* **radius** - Radius of the circle from which a sector is cut.
- *float* **angle** - Angle of the sector.
- *Mat4* **transform** - Transformation matrix used to position the sector.
- *vec4* **color** - Sector color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderCone ( float radius , float angle , Mat4 transform , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a wireframe cone of a given color.
### Arguments

- *float* **radius** - Radius of the cone.
- *float* **angle** - Angle of the cone.
- *Mat4* **transform** - Transformation matrix used to position the cone.
- *vec4* **color** - Color, in which the cone will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderSphere ( float radius , Mat4 transform , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a sphere in a given color.
### Arguments

- *float* **radius** - Radius of the sphere.
- *Mat4* **transform** - Transformation matrix used to position the sphere.
- *vec4* **color** - Color, in which the sphere will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderCapsule ( float radius , float height , Mat4 transform , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a wireframe capsule (capped cylinder) of a given color.
### Arguments

- *float* **radius** - Radius of the capsule.
- *float* **height** - Height of the capsule.
- *Mat4* **transform** - Transformation matrix used to position the capsule.
- *vec4* **color** - Capsule color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderCylinder ( float radius , float height , Mat4 transform , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a wireframe cylinder of a given color.
### Arguments

- *float* **radius** - Radius of the cylinder.
- *float* **height** - Height of the cylinder.
- *Mat4* **transform** - Transformation matrix used to position the cylinder.
- *vec4* **color** - Cylinder color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderEllipse ( vec3 radius , Mat4 transform , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a wireframe ellipse of a given color.
### Arguments

- *vec3* **radius** - Ellipse radius values along three axes.
- *Mat4* **transform** - Transformation matrix for the ellipse.
- *vec4* **color** - Ellipse color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderSolidBox ( vec3 size , Mat4 transform , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a solid box of a given color.
### Arguments

- *vec3* **size** - Size of the solid box.
- *Mat4* **transform** - Transformation matrix used to position the solid box.
- *vec4* **color** - Box color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderSolidSphere ( float radius , Mat4 transform , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a solid sphere of a given color.
### Arguments

- *float* **radius** - Radius of the solid sphere.
- *Mat4* **transform** - Transformation matrix used to position the solid sphere.
- *vec4* **color** - Sphere color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderSolidCapsule ( float radius , float height , Mat4 transform , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a solid capsule af a given color.
### Arguments

- *float* **radius** - Radius of the capsule.
- *float* **height** - Height of the capsule.
- *Mat4* **transform** - Transformation matrix used to position the capsule.
- *vec4* **color** - Capsule color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderSolidCylinder ( float radius , float height , Mat4 transform , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a solid cylinder of a given color.
### Arguments

- *float* **radius** - Radius of the cylinder.
- *float* **height** - Height of the cylinder.
- *Mat4* **transform** - Transformation matrix used to position the cylinder.
- *vec4* **color** - Cylinder color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderSolidEllipse ( vec3 radius , Mat4 transform , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a solid ellipse of a given color.
### Arguments

- *vec3* **radius** - Ellipse radius values along three axes.
- *Mat4* **transform** - Transformation matrix used to position the ellipse.
- *vec4* **color** - Ellipse color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderRectangle ( vec4 rectangle , vec4 color , float duration = 0.0f )

Renders a 2D wireframe rectangle of a given color.
### Arguments

- *vec4* **rectangle** - Four-component vector containing the coordinates of the upper-left (first two components) and bottom-right (second two components) corners of the rectangle.
- *vec4* **color** - Rectangle color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void engine.visualizer. renderBoundBox ( BoundBox bb , Mat4 transform , vec4 color , float duration = 0.0f , int depth_test = true )

Renders the bounding box of a given color.
### Arguments

- *BoundBox* **bb** - The bounding box.
- *Mat4* **transform** - Transformation matrix for the bounding box.
- *vec4* **color** - Color, in which the box will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderBoundSphere ( BoundSphere bs , Mat4 transform , vec4 color , float duration = 0.0f , int depth_test = true )

Renders the bounding sphere of a given color.
### Arguments

- *BoundSphere* **bs** - The bounding sphere.
- *Mat4* **transform** - Transformation matrix for the bounding sphere.
- *vec4* **color** - Color, in which the sphere will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderNodeBoundBox ( Node node , vec4 color , float duration = 0.0f , int depth_test = true )

Renders an axis-aligned bound box of a given node.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - Node, for which the bound box is rendered.
- *vec4* **color** - Color, in which the box will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderNodeBoundSphere ( Node node , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a bound sphere of a given node.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - Node, for which the bound sphere is rendered.
- *vec4* **color** - Color, in which the sphere will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderObjectSurfaceBoundBox ( Object object , int surface , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a bound box of a given object surface.
### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Object, which contains the target surface.
- *int* **surface** - The number of the target surface in the object.
- *vec4* **color** - Color, in which the box will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderObjectSurfaceBoundSphere ( Object object , int surface , vec4 color , float duration = 0.0f , int depth_test = true )

Renders a bound sphere of a given object surface.
### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Object, which contains the target surface.
- *int* **surface** - The number of the target surface in the object.
- *vec4* **color** - Color, in which the sphere will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *int* **depth_test** - **1** to enable depth testing for the element (if it should be obscured by elements closer to the camera); **0** � to disable it.

## void engine.visualizer. renderNodeHandler ( Node node , float duration = 0.0f )

Renders a handler for the specified node. You can customize handler image via **[setTextureName()()](../../...md#setTextureName_cstr_void)**.
### Arguments

- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - Node, for which the handler is to be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void engine.visualizer. renderObject ( Object object , vec4 color , float duration = 0.0f )

Renders an object wireframe.
### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Object, which wireframe will be rendered.
- *vec4* **color** - Color, in which the wireframe will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void engine.visualizer. renderObjectSurface ( Object object , int surface , vec4 color , float duration = 0.0f )

Renders borders of a given object surface.
### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Object, which contains the target surface.
- *int* **surface** - The number of the target surface in the object.
- *vec4* **color** - Color, in which the borders will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void engine.visualizer. renderSolidObject ( Object object , vec4 color , float duration = 0.0f )

Renders a solid-colored object.
### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Object that will be rendered.
- *vec4* **color** - Color in which the object will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void engine.visualizer. renderSolidObjectSurface ( Object object , int surface , vec4 color , float duration = 0.0f )

Renders a solid-colored surface of a given object.
### Arguments

- *[Object](../../../api/library/objects/class.object_usc.md)* **object** - Object that will be rendered.
- *int* **surface** - The number of the object's surface.
- *vec4* **color** - Color, in which the object's surface will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void engine.visualizer. renderMessage2D ( vec3 position , vec3 center , string str , vec4 color , int outline , int font_size = -1 , float duration = 0.0f )

Renders a message in a given color. Message position is specified in screen coordinates.
### Arguments

- *vec3* **position** - Coordinates of the anchor point of the message, each in **[0;1]** range.
- *vec3* **center** - Message alignment. The first two values in the vector set the offset, the third one is ignored. For example, vec3(-1,-1,0) sets the offset of the center of the message to its upper left edge. vec3(1,1,0) - to the lower right corner.
- *string* **str** - Message text to display.
- *vec4* **color** - Color, in which the message will be rendered.
- *int* **outline** - **1** to use font outlining, **0** not to use.
- *int* **font_size** - Font size.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void engine.visualizer. renderMessage3D ( Vec3 position , vec3 center , string str , vec4 color , int outline , int font_size = -1 , float duration = 0.0f )

Renders a message in a given color. Message position is specified in world coordinates.
### Arguments

- *Vec3* **position** - Coordinates of the anchor point of the message (in world coordinates).
- *vec3* **center** - Message alignment. The first two values in the vector set the offset, the third one is ignored. For example, vec3(-1,-1,0) sets the offset of the center of the message to its upper left edge. vec3(1,1,0) - to the lower right corner.
- *string* **str** - Message text to display.
- *vec4* **color** - Color, in which the message will be rendered.
- *int* **outline** - **1** to use font outlining, **0** not to use.
- *int* **font_size** - Font size.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## Node engine.visualizer. getHandlerNode ( int num )


Returns the handler node by its index.


> **Notice:** The handler index may change every frame depending on the camera transforms (i.e. how many handlers are visible in the current frame), therefore it is not recommended to save and reuse this value.


### Arguments

- *int* **num** - Handler node index in the range from 0 to the [total number of handlers](#getNumHandlers_int).

### Return value

The node for which the handler is rendered.
## float engine.visualizer. getHandlerSize ( int num )

Returns the handler icon size in units by its index. This value may be affected by the icon size (set by the [setSize()](#setSize_int_void) method) and by the 3D option ([world_handler_3d](../../../code/console/index.md#world_handler_3d) console command).
### Arguments

- *int* **num** - Handler node index in the range from 0 to the [total number of handlers](#getNumHandlers_int).

### Return value

The handler icon size, in units.
## void engine.visualizer. clearNodeTypeIcons ( )

Removes all custom per-node-type handler icons set via **[setNodeTypeIcon()()](../../...md#setNodeTypeIcon_int_cstr_int)**, so all node handlers revert to the default icon.
## int engine.visualizer. setNodeTypeIcon ( int type , string path )

Replaces the billboard icon the visualizer draws for node handlers of the given node type (the per-node icons shown when visualizer node handlers are enabled). Node types without a custom icon keep the default handler icon.
### Arguments

- *int* **type** - Node type, one of the *Node::TYPE* values.
- *string* **path** - Path to the icon image file.

### Return value

true if the icon is set successfully; otherwise, false (the type is out of range or the image cannot be loaded).
