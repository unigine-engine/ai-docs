# Unigine::Visualizer Class (CS)

> **Notice:** This class is a singleton.


Controls visualizer-related settings. The visualizer is used to render mesh wireframe, object bounding boxes, and all sorts of visual helpers (such as physical collision shapes, joints, etc.).


### Usage Example


To render the world origin, do the following:


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#region Math Variables
#if UNIGINE_DOUBLE
using Scalar = System.Double;
using Vec3 = Unigine.dvec3;
#else
using Scalar = System.Single;
using Vec3 = Unigine.vec3;
#endif
#endregion

public partial class VisualizerClass : Component
{

	private void Init()
	{
		// enable the visualizer
		Visualizer.Enabled = true;

	}
	private void Update()
	{

		// render world origin
		Visualizer.RenderVector(new Vec3(0.0f, 0.0f, 0.1f), new Vec3(1.0f, 0.0f, 0.1f), vec4.RED);
		Visualizer.RenderVector(new Vec3(0.0f, 0.0f, 0.1f), new Vec3(0.0f, 1.0f, 0.1f), vec4.GREEN);
		Visualizer.RenderVector(new Vec3(0.0f, 0.0f, 0.1f), new Vec3(0.0f, 0.0f, 1.1f), vec4.BLUE);
	}

}


```


To render a trace from the camera movement, use the following:


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

#region Math Variables
#if UNIGINE_DOUBLE
using Scalar = System.Double;
using Vec3 = Unigine.dvec3;
#else
using Scalar = System.Single;
using Vec3 = Unigine.vec3;
#endif
#endregion

public partial class VisualizerClass : Component
{
	Vec3 last_pos; // stores the camera position

	private void Init()
	{
		// enable the visualizer
		Visualizer.Enabled = true;

		// save the camera position
		last_pos = Game.Player.WorldPosition;
	}
	private void Update()
	{

		// Tracking of camera movement
		var current_pos = Game.Player.WorldPosition;

		if ((current_pos - last_pos).Length2 >= 0.1f)
		{
			Visualizer.RenderPoint3D(last_pos, 0.05f, vec4.GREEN, false, 2.0f);
			last_pos = current_pos;
		}
	}

}


```


You'll be able to see green squares as you move backwards or turn around to watch your trace.


## Visualizer Class

### Enums

## MODE

Visualizer mode. Controls the way all visual helpers are displayed.
| Name | Description |
|---|---|
| **DISABLED** = 0 | Do not display the Visualizer at all. |
| **ENABLED_DEPTH_TEST_ENABLED** = 1 | Display the Visualizer with depth testing enabled. |
| **ENABLED_DEPTH_TEST_DISABLED** = 2 | Display the Visualizer without depth testing. |

### Properties

## string TextureName

The path to auxiliary visualizer texture. This texture is applied to **[billboards](#renderBillboard3D_Vec3_float_vec4_int_float_int_void)** and **[handlers](#renderNodeHandler_Node_float_void)** (rendered via *[RenderBillboard3D()](../../...md#renderBillboard3D_Vec3_float_vec4_int_float_int_void)* and *[RenderNodeHandler()](../../...md#renderNodeHandler_Node_float_void)*). To restore the default texture, pass an empty string **("")**.
## int Size

The handler size. All handlers have the same size.
## bool Enabled

The value indicating if the visualizer (rendering of helper objects like handlers and bound boxes) is enabled.
## Visualizer.MODE Mode

The [visualizer mode](#MODE) controlling the way all visual helpers are displayed. You can choose to display Visualizer with or without depth testing, or turn it off completely.
## 🔒︎ int NumHandlers

The total number of handlers.
> **Notice:** The total number of handlers may change every frame depending on the camera transforms (i.e. how many handlers are visible in the current frame), therefore it is not recommended to save and reuse this value.


### Members

---

## void Clear ( )


Clears all internal primitives created by calls to *renderSmth* functions. These primitives are accumulated in the internal buffer and then rendered together.


> **Notice:** This method can be used to render several viewports with visualizer.


## void RenderPoint2D ( vec2 v , float size , vec4 color , float order = 0.0f , float duration = 0.0f )

Renders a 2D point of a given size and color. 2D points are rendered in the screen plane; coordinates of the upper left corner are (0; 0), of the lower right corner�(1; 1).
### Arguments

- *vec2* **v** - Point coordinates.
- *float* **size** - Point size.
- *vec4* **color** - Color, in which the point will be rendered.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void RenderPoint3D ( vec3 v , float size , vec4 color , bool screen_space = false , float duration = 0.0f , bool depth_test = true )

Renders a 3D point of a given size and color. 3D points are rendered in the world space.
### Arguments

- *vec3* **v** - Point coordinates.
- *float* **size** - Point size in range [0;1]. The point size is set in proportion to the screen resolution.
- *vec4* **color** - Point color.
- *bool* **screen_space** - Flag indicating the type of dimensions to be used:

  - **false** - use the world space dimensions
  - **true** - use the screen space dimensions
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderLine2D ( vec2 v0 , vec2 v1 , vec4 color , float order = 0.0f , float duration = 0.0f )

Renders a 2D line of a given color. 2D lines are rendered in the screen plane; coordinates of the upper left corner are **(0; 0)**, of the lower right corner � **(1; 1)**.
### Arguments

- *vec2* **v0** - Starting point of the line.
- *vec2* **v1** - Ending point of the line.
- *vec4* **color** - Line color.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void RenderLine3D ( vec3 v0 , vec3 v1 , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a 3D line of a given color. 3D lines are rendered in the world space.
### Arguments

- *vec3* **v0** - Starting point of the line.
- *vec3* **v1** - Ending point of the line.
- *vec4* **color** - Line color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderLine2D ( vec2 v0 , vec2 v1 , vec2 v2 , vec4 color , float order = 0.0f , float duration = 0.0f )

Renders a 2D line of a given color by using 3 points. 2D lines are rendered in the screen plane; coordinates of the upper left corner are **(0; 0)**, of the lower right corner � **(1; 1)**.
### Arguments

- *vec2* **v0** - Coordinates of the starting point of the line.
- *vec2* **v1** - Coordinates of the intermediate point of the line.
- *vec2* **v2** - Coordinates of the ending point of the line.
- *vec4* **color** - Ending point of the line.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void RenderLine3D ( vec3 v0 , vec3 v1 , vec3 v2 , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a 3D line of a given color. 3D lines are rendered in the world space.
### Arguments

- *vec3* **v0** - Coordinates of the starting point of the line.
- *vec3* **v1** - Coordinates of the intermediate point of the line.
- *vec3* **v2** - Coordinates of the ending point of the line.
- *vec4* **color** - Line color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderLine2D ( vec2 v0 , vec2 v1 , vec2 v2 , vec2 v3 , vec4 color , float order = 0.0f , float duration = 0.0f )

Renders a 2D line of a given color. 2D lines are rendered in the screen plane; coordinates of the upper left corner are **(0; 0)**, of the lower right corner � **(1; 1)**.
### Arguments

- *vec2* **v0** - Coordinates of the starting point of the line.
- *vec2* **v1** - Coordinates of the first intermediate point of the line.
- *vec2* **v2** - Coordinates of the second intermediate point of the line.
- *vec2* **v3** - Coordinates of the ending point of the line.
- *vec4* **color** - Color, in which the line will be rendered.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void RenderLine3D ( vec3 v0 , vec3 v1 , vec3 v2 , vec3 v3 , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a 3D line of a given color. 3D lines are rendered in the world space.
### Arguments

- *vec3* **v0** - Coordinates of the starting point of the line.
- *vec3* **v1** - Coordinates of the first intermediate point of the line.
- *vec3* **v2** - Coordinates of the second intermediate point of the line.
- *vec3* **v3** - Coordinates of the ending point of the line.
- *vec4* **color** - Color, in which the line will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderTriangle2D ( vec2 v0 , vec2 v1 , vec2 v2 , vec4 color , float order = 0.0f , float duration = 0.0f )

Renders a 2D triangle of a given color. 2D triangles are rendered in the screen plane; coordinates of the upper left corner are **(0; 0)**, of the lower right corner�**(1; 1)**.
### Arguments

- *vec2* **v0** - Coordinates of the first vertex.
- *vec2* **v1** - Coordinates of the second vertex.
- *vec2* **v2** - Coordinates of the third vertex.
- *vec4* **color** - Triangle color.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void RenderTriangle3D ( vec3 v0 , vec3 v1 , vec3 v2 , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a 3D triangle of a given color. 3D triangles are rendered in the world space.
### Arguments

- *vec3* **v0** - Coordinates of the first vertex.
- *vec3* **v1** - Coordinates of the second vertex.
- *vec3* **v2** - Coordinates of the third vertex.
- *vec4* **color** - Triangle color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderQuad2D ( vec2 v0 , vec2 v1 , vec2 v2 , vec2 v3 , vec4 color , float order = 0.0f , float duration = 0.0f )

Renders a 2D quad of a given color. 2D quads are rendered in the screen plane; coordinates of the upper left corner are **(0; 0)**, of the lower right corner�**(1; 1)**.
### Arguments

- *vec2* **v0** - Coordinates of the first vertex.
- *vec2* **v1** - Coordinates of the second vertex.
- *vec2* **v2** - Coordinates of the third vertex.
- *vec2* **v3** - Coordinates of the fourth vertex.
- *vec4* **color** - Color, in which the quad will be rendered.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void RenderQuad3D ( vec3 v0 , vec3 v1 , vec3 v2 , vec3 v3 , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a 3D quad of a given color. 3D quads are rendered in the world space.
### Arguments

- *vec3* **v0** - Coordinates of the first vertex.
- *vec3* **v1** - Coordinates of the second vertex.
- *vec3* **v2** - Coordinates of the third vertex.
- *vec3* **v3** - Coordinates of the fourth vertex.
- *vec4* **color** - Color, in which the quad will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderBillboard3D ( vec3 v , float size , vec4 texcoord , bool screen_space = false , float duration = 0.0f , bool depth_test = true )

Renders a 3D billboard of the specified size. You can customize billboard image via **[TextureName](../../...md#setTextureName_cstr_void)**.
### Arguments

- *vec3* **v** - Coordinates of the billboard.
- *float* **size** - The billboard size in units (meters).
- *vec4* **texcoord** - The billboard texture coordinates, consisting of two pairs of vector elements (x, y, z, w):

  - x - texture size along the X axis in range [0.0f; 1.0f]
  - y - texture size along the Y axis in range [0.0f; 1.0f]
  - z - offset of the texture's starting position along the X axis in range [0.0f; 1.0f]
  - w - offset of the texture's starting position along the Y axis [0.0f; 1.0f]
- *bool* **screen_space** - Flag indicating the type of dimensions to be used:

  - **false** - use the world space dimensions
  - **true** - use the screen space dimensions
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderVector ( vec3 position_start , vec3 position_end , vec4 color , float arrow_size = 0.25f , bool screen_space = false , float duration = 0.0f , bool depth_test = true )

Renders a vector of a given color.
### Arguments

- *vec3* **position_start** - Coordinates of the vector origin.
- *vec3* **position_end** - Coordinates of the vector target.
- *vec4* **color** - Vector color.
- *float* **arrow_size** - Relative length of the arrowhead (cone) with respect to the total vector length. For example, the default value of 0.25f means that the arrowhead occupies 25% of the overall arrow length.
- *bool* **screen_space** - Flag indicating the type of dimensions to be used:

  - **false** - use the world space dimensions
  - **true** - use the screen space dimensions
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderDirection ( vec3 position , vec3 direction , vec4 color , float arrow_size = 0.25f , bool screen_space = true , float duration = 0.0f , bool depth_test = true )

Renders a direction vector of a given color.
### Arguments

- *vec3* **position** - Coordinates of the vector origin.
- *vec3* **direction** - Target vector direction.
- *vec4* **color** - Vector color.
- *float* **arrow_size** - Relative length of the arrowhead (cone) with respect to the total vector length. For example, the default value of 0.25f means that the arrowhead occupies 25% of the overall arrow length.
- *bool* **screen_space** - Flag indicating the type of dimensions to be used:

  - **false** - use the world space dimensions
  - **true** - use the screen space dimensions
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderBox ( vec3 size , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a box of a given color.
### Arguments

- *vec3* **size** - Dimensions of the box.
- *mat4* **transform** - Transformation matrix, which is used to position the box.
- *vec4* **color** - Color, in which the box will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderFrustum ( mat4 projection , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a wireframe frustum of a given color.
### Arguments

- *mat4* **projection** - Projection matrix used to transform the coordinates.
- *mat4* **transform** - Transformation matrix used to position the frustum.
- *vec4* **color** - Color, in which the frustum will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderCircle ( float radius , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a wireframe circle of a given color.
### Arguments

- *float* **radius** - Radius of the circle.
- *mat4* **transform** - Transformation matrix used to position the circle.
- *vec4* **color** - Circle color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderSector ( float radius , float angle , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a wireframe sector of a given color.
### Arguments

- *float* **radius** - Radius of the circle from which a sector is cut.
- *float* **angle** - Angle of the sector.
- *mat4* **transform** - Transformation matrix used to position the sector.
- *vec4* **color** - Sector color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderCone ( float radius , float angle , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a wireframe cone of a given color.
### Arguments

- *float* **radius** - Radius of the cone.
- *float* **angle** - Angle of the cone.
- *mat4* **transform** - Transformation matrix used to position the cone.
- *vec4* **color** - Color, in which the cone will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderSphere ( float radius , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a wireframe sphere of a given color.
### Arguments

- *float* **radius** - Radius of the sphere.
- *mat4* **transform** - Transformation matrix used to position the sphere.
- *vec4* **color** - Color, in which the sphere will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderCapsule ( float radius , float height , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a wireframe capsule (capped cylinder) of a given color.
### Arguments

- *float* **radius** - Radius of the capsule.
- *float* **height** - Height of the capsule.
- *mat4* **transform** - Transformation matrix used to position the capsule.
- *vec4* **color** - Capsule color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderCylinder ( float radius , float height , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a wireframe cylinder of a given color.
### Arguments

- *float* **radius** - Radius of the cylinder.
- *float* **height** - Height of the cylinder.
- *mat4* **transform** - Transformation matrix used to position the cylinder.
- *vec4* **color** - Cylinder color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderEllipse ( vec3 radius , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a wireframe ellipse of a given color.
### Arguments

- *vec3* **radius** - Ellipse radius values along three axes.
- *mat4* **transform** - Transformation matrix for the ellipse.
- *vec4* **color** - Ellipse color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderSolidBox ( vec3 size , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a solid box of a given color.
### Arguments

- *vec3* **size** - Size of the solid box.
- *mat4* **transform** - Transformation matrix used to position the solid box.
- *vec4* **color** - Box color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderSolidSphere ( float radius , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a solid sphere of a given color.
### Arguments

- *float* **radius** - Radius of the solid sphere.
- *mat4* **transform** - Transformation matrix used to position the solid sphere.
- *vec4* **color** - Sphere color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderSolidCapsule ( float radius , float height , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a solid capsule af a given color.
### Arguments

- *float* **radius** - Radius of the capsule.
- *float* **height** - Height of the capsule.
- *mat4* **transform** - Transformation matrix used to position the capsule.
- *vec4* **color** - Capsule color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderSolidCylinder ( float radius , float height , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a solid cylinder of a given color.
### Arguments

- *float* **radius** - Radius of the cylinder.
- *float* **height** - Height of the cylinder.
- *mat4* **transform** - Transformation matrix used to position the cylinder.
- *vec4* **color** - Cylinder color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderSolidEllipse ( vec3 radius , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a solid ellipse of a given color.
### Arguments

- *vec3* **radius** - Ellipse radius values along three axes.
- *mat4* **transform** - Transformation matrix used to position the ellipse.
- *vec4* **color** - Ellipse color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderRectangle ( vec4 rectangle , vec4 color , float duration = 0.0f )

Renders a 2D wireframe rectangle of a given color.
### Arguments

- *vec4* **rectangle** - Four-component vector containing the coordinates of the upper-left (first two components) and bottom-right (second two components) corners of the rectangle.
- *vec4* **color** - Rectangle color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void RenderBoundBox ( BoundBox bb , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders the bounding box of a given color.
### Arguments

- *[BoundBox](../../../api/library/math/cs/bounds/boundbox_cs.md)* **bb** - The bounding box.
- *mat4* **transform** - Transformation matrix for the bounding box.
- *vec4* **color** - Color, in which the box will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderBoundSphere ( BoundSphere bs , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders the bounding sphere of a given color.
### Arguments

- *[BoundSphere](../../../api/library/math/cs/bounds/boundsphere_cs.md)* **bs** - The bounding sphere.
- *mat4* **transform** - Transformation matrix for the bounding sphere.
- *vec4* **color** - Color, in which the sphere will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderNodeBoundBox ( Node node , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders an axis-aligned bound box of a given node.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Node, for which the bound box is rendered.
- *vec4* **color** - Color, in which the box will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderNodeBoundSphere ( Node node , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a bound sphere of a given node.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Node, for which the bound sphere is rendered.
- *vec4* **color** - Color, in which the sphere will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderObjectSurfaceBoundBox ( Object object , int surface , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a bound box of a given object surface.
### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object, which contains the target surface.
- *int* **surface** - The number of the target surface in the object.
- *vec4* **color** - Color, in which the box will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderObjectSurfaceBoundSphere ( Object object , int surface , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a bound sphere of a given object surface.
### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object, which contains the target surface.
- *int* **surface** - The number of the target surface in the object.
- *vec4* **color** - Color, in which the sphere will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void RenderNodeHandler ( Node node , float duration = 0.0f )

Renders a handler for the specified node. You can customize handler image via **[TextureName](../../...md#setTextureName_cstr_void)**.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Node, for which the handler is to be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void RenderObject ( Object object , vec4 color , float duration = 0.0f )

Renders an object wireframe.
### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object, which wireframe will be rendered.
- *vec4* **color** - Color, in which the wireframe will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void RenderObjectSurface ( Object object , int surface , vec4 color , float duration = 0.0f )

Renders borders of a given object surface.
### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object, which contains the target surface.
- *int* **surface** - The number of the target surface in the object.
- *vec4* **color** - Color, in which the borders will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void RenderSolidObject ( Object object , vec4 color , float duration = 0.0f )

Renders a solid-colored object.
### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object that will be rendered.
- *vec4* **color** - Color in which the object will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void RenderSolidObjectSurface ( Object object , int surface , vec4 color , float duration = 0.0f )

Renders a solid-colored surface of a given object.
### Arguments

- *[Object](../../../api/library/objects/class.object_cs.md)* **object** - Object that will be rendered.
- *int* **surface** - The number of the object's surface.
- *vec4* **color** - Color, in which the object's surface will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void RenderMessage2D ( vec3 position , vec3 center , string str , vec4 color , int outline , int font_size = -1 , float duration = 0.0f )

Renders a message in a given color. Message position is specified in screen coordinates.
### Arguments

- *vec3* **position** - Coordinates of the anchor point of the message, each in **[0;1]** range.
- *vec3* **center** - Message alignment. The first two values in the vector set the offset, the third one is ignored. For example, vec3(-1,-1,0) sets the offset of the center of the message to its upper left edge. vec3(1,1,0) - to the lower right corner.
- *string* **str** - Message text to display.
- *vec4* **color** - Color, in which the message will be rendered.
- *int* **outline** - **1** to use font outlining, **0** not to use.
- *int* **font_size** - Font size.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void RenderMessage3D ( vec3 position , vec3 center , string str , vec4 color , int outline , int font_size = -1 , float duration = 0.0f )

Renders a message in a given color. Message position is specified in world coordinates.
### Arguments

- *vec3* **position** - Coordinates of the anchor point of the message (in world coordinates).
- *vec3* **center** - Message alignment. The first two values in the vector set the offset, the third one is ignored. For example, vec3(-1,-1,0) sets the offset of the center of the message to its upper left edge. vec3(1,1,0) - to the lower right corner.
- *string* **str** - Message text to display.
- *vec4* **color** - Color, in which the message will be rendered.
- *int* **outline** - **1** to use font outlining, **0** not to use.
- *int* **font_size** - Font size.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## Node GetHandlerNode ( int num )


Returns the handler node by its index.


> **Notice:** The handler index may change every frame depending on the camera transforms (i.e. how many handlers are visible in the current frame), therefore it is not recommended to save and reuse this value.


### Arguments

- *int* **num** - Handler node index in the range from 0 to the [total number of handlers](#getNumHandlers_int).

### Return value

The node for which the handler is rendered.
## float GetHandlerSize ( int num )

Returns the handler icon size in units by its index. This value may be affected by the icon size (set by the [setSize()](#setSize_int_void) method) and by the 3D option ([world_handler_3d](../../../code/console/index.md#world_handler_3d) console command).
### Arguments

- *int* **num** - Handler node index in the range from 0 to the [total number of handlers](#getNumHandlers_int).

### Return value

The handler icon size, in units.
## void RenderMesh ( MeshRender mesh , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a wireframe of the specified mesh in the given color.
### Arguments

- *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)* **mesh** - The mesh to be rendered.
- *mat4* **transform** - Transformation matrix for the mesh.
- *vec4* **color** - Color, in which the mesh's wireframe will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false - to disable it.

## void RenderMesh ( UGUID mesh_guid , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a wireframe of the mesh loaded by the specified asset GUID in a given color.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **mesh_guid** - GUID of the mesh asset to be rendered.
- *mat4* **transform** - Transformation matrix for the mesh.
- *vec4* **color** - Color, in which the mesh's wireframe will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false - to disable it.

## void RenderMesh ( string path , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a wireframe of the mesh loaded from the specified file path in the given color.
### Arguments

- *string* **path** - File path to the mesh to be rendered.
- *mat4* **transform** - Transformation matrix for the mesh.
- *vec4* **color** - Color, in which the mesh's wireframe will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false - to disable it.

## void RenderSolidMesh ( MeshRender mesh , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a solid version of the specified mesh in the given color.
### Arguments

- *[MeshRender](../../../api/library/rendering/class.meshrender_cs.md)* **mesh** - The mesh to be rendered.
- *mat4* **transform** - Transformation matrix for the mesh.
- *vec4* **color** - Color, in which the mesh will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false - to disable it.

## void RenderSolidMesh ( UGUID mesh_guid , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a solid version of the mesh loaded by the specified asset GUID in a given color.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **mesh_guid** - GUID of the mesh asset to be rendered.
- *mat4* **transform** - Transformation matrix for the mesh.
- *vec4* **color** - Color, in which the mesh will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false - to disable it.

## void RenderSolidMesh ( string path , mat4 transform , vec4 color , float duration = 0.0f , bool depth_test = true )

Renders a solid version of the mesh loaded from the specified file path in the given color.
### Arguments

- *string* **path** - File path to the mesh to be rendered.
- *mat4* **transform** - Transformation matrix for the mesh.
- *vec4* **color** - Color, in which the mesh's wireframe will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false - to disable it.

## void ClearNodeTypeIcons ( )

Removes all custom per-node-type handler icons set via **[SetNodeTypeIcon()](../../...md#setNodeTypeIcon_int_cstr_int)**, so all node handlers revert to the default icon.
## bool SetNodeTypeIcon ( Node.TYPE type , string path )

Replaces the billboard icon the visualizer draws for node handlers of the given node type (the per-node icons shown when visualizer node handlers are enabled). Node types without a custom icon keep the default handler icon.
### Arguments

- *[Node.TYPE](../../../api/library/nodes/class.node_cs.md#TYPE)* **type** - Node type, one of the *Node::TYPE* values.
- *string* **path** - Path to the icon image file.

### Return value

true if the icon is set successfully; otherwise, false (the type is out of range or the image cannot be loaded).
