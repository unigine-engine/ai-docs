# Unigine::Visualizer Class (CPP)

**Header:** #include <UnigineVisualizer.h>

> **Notice:** This class is a singleton.


Controls visualizer-related settings. The visualizer is used to render mesh wireframe, object bounding boxes, and all sorts of visual helpers (such as physical collision shapes, joints, etc.).


### Usage Example


To render a world origin, do the following:


```cpp
#include "AppWorldLogic.h"
#include "UnigineVisualizer.h"

using namespace Unigine;
using namespace Math;

AppWorldLogic::AppWorldLogic()
{}

AppWorldLogic::~AppWorldLogic()
{}

int AppWorldLogic::init()
{
	// enable the visualizer
	Visualizer::setEnabled(true);

	return 1;
}

int AppWorldLogic::update()
{

	// render world origin
	Visualizer::renderVector(Vec3(0.0f, 0.0f, 0.1f), Vec3(1.0f, 0.0f, 0.1f), vec4_red);
	Visualizer::renderVector(Vec3(0.0f, 0.0f, 0.1f), Vec3(0.0f, 1.0f, 0.1f), vec4_green);
	Visualizer::renderVector(Vec3(0.0f, 0.0f, 0.1f), Vec3(0.0f, 0.0f, 1.1f), vec4_blue);

	return 1;
}


```


To render a trace from the camera movement, use the following:


```cpp
#include "AppWorldLogic.h"
#include "UnigineVisualizer.h"
#include "UnigineGame.h"

using namespace Unigine;
using namespace Math;

AppWorldLogic::AppWorldLogic()
{}

AppWorldLogic::~AppWorldLogic()
{}

int AppWorldLogic::init()
{
	// enable the visualizer
	Visualizer::setEnabled(true);

	return 1;
}

int AppWorldLogic::update()
{

	static auto last_pos = Game::getPlayer()->getWorldPosition();

	// Tracking of camera movement
	const auto current_pos = Game::getPlayer()->getWorldPosition();
	if (length2(current_pos - last_pos) >= 0.1f)
	{
		Visualizer::renderPoint3D(last_pos, 0.05f, vec4_green, false, 2.0f);
		last_pos = current_pos;
	}

	return 1;
}


```


You'll be able to see green squares as you move backwards or turn around to watch your trace.


## Visualizer Class

### Enums

## MODE

Visualizer mode. Controls the way all visual helpers are displayed.
| Name | Description |
|---|---|
| **MODE_DISABLED** = 0 | Do not display the Visualizer at all. |
| **MODE_ENABLED_DEPTH_TEST_ENABLED** = 1 | Display the Visualizer with depth testing enabled. |
| **MODE_ENABLED_DEPTH_TEST_DISABLED** = 2 | Display the Visualizer without depth testing. |

### Members

## void setTextureName ( const char * name )

Sets a new path to auxiliary visualizer texture. This texture is applied to **[billboards](#renderBillboard3D_Vec3_float_vec4_int_float_int_void)** and **[handlers](#renderNodeHandler_Node_float_void)** (rendered via *[renderBillboard3D()](../../...md#renderBillboard3D_Vec3_float_vec4_int_float_int_void)* and *[renderNodeHandler()](../../...md#renderNodeHandler_Node_float_void)*). To restore the default texture, pass an empty string **("")**.
### Arguments

- *const char ** **name** - The path to the texture.

## const char * getTextureName () const

Returns the current path to auxiliary visualizer texture. This texture is applied to **[billboards](#renderBillboard3D_Vec3_float_vec4_int_float_int_void)** and **[handlers](#renderNodeHandler_Node_float_void)** (rendered via *[renderBillboard3D()](../../...md#renderBillboard3D_Vec3_float_vec4_int_float_int_void)* and *[renderNodeHandler()](../../...md#renderNodeHandler_Node_float_void)*). To restore the default texture, pass an empty string **("")**.
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
## void setEnabled ( bool enabled )

Sets a new value indicating if the visualizer (rendering of helper objects like handlers and bound boxes) is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable value indicating if the visualizer is enabled; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if the visualizer (rendering of helper objects like handlers and bound boxes) is enabled.
### Return value

**true** if value indicating if the visualizer is enabled is enabled ; otherwise **false**.
## void setMode ( Visualizer::MODE mode )

Sets a new [visualizer mode](#MODE) controlling the way all visual helpers are displayed. You can choose to display Visualizer with or without depth testing, or turn it off completely.
### Arguments

- *[Visualizer::MODE](../../../api/library/engine/class.visualizer_cpp.md#MODE)* **mode** - The visualizer mode.

## Visualizer::MODE getMode () const

Returns the current [visualizer mode](#MODE) controlling the way all visual helpers are displayed. You can choose to display Visualizer with or without depth testing, or turn it off completely.
### Return value

Current visualizer mode.
## int getNumHandlers () const

Returns the current total number of handlers.
> **Notice:** The total number of handlers may change every frame depending on the camera transforms (i.e. how many handlers are visible in the current frame), therefore it is not recommended to save and reuse this value.


### Return value

Current total number of handlers.
---

## void clear ( )


Clears all internal primitives created by calls to *renderSmth* functions. These primitives are accumulated in the internal buffer and then rendered together.


> **Notice:** This method can be used to render several viewports with visualizer.


## void renderPoint2D ( const Math:: vec2 & v , float size , const Math:: vec4 & color , float order = 0.0f , float duration = 0.0f ) const

Renders a 2D point of a given size and color. 2D points are rendered in the screen plane; coordinates of the upper left corner are (0; 0), of the lower right corner�(1; 1).
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v** - Point coordinates.
- *float* **size** - Point size in range [0;1]. The point size is set in proportion to the screen resolution.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Point color.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void renderPoint3D ( const Math:: Vec3 & v , float size , const Math:: vec4 & color , bool screen_space = false , float duration = 0.0f , bool depth_test = true ) const

Renders a 3D point of a given size and color. 3D points are rendered in the world space.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Point coordinates.
- *float* **size** - Point size in range [0;1]. The point size is set in proportion to the screen resolution.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Point color.
- *bool* **screen_space** - Flag indicating the type of dimensions to be used:

  - **false** - use the world space dimensions
  - **true** - use the screen space dimensions
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderLine2D ( const Math:: vec2 & v0 , const Math:: vec2 & v1 , const Math:: vec4 & color , float order = 0.0f , float duration = 0.0f )

Renders a 2D line of a given color. 2D lines are rendered in the screen plane; coordinates of the upper left corner are **(0; 0)**, of the lower right corner � **(1; 1)**.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - Starting point of the line.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Ending point of the line.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Line color.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void renderLine3D ( const Math:: Vec3 & v0 , const Math:: Vec3 & v1 , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true )

Renders a 3D line of a given color. 3D lines are rendered in the world space.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - Starting point of the line.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Ending point of the line.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Line color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderLine2D ( const Math:: vec2 & v0 , const Math:: vec2 & v1 , const Math:: vec2 & v2 , const Math:: vec4 & color , float order = 0.0f , float duration = 0.0f )

Renders a 2D line of a given color by using 3 points. 2D lines are rendered in the screen plane; coordinates of the upper left corner are **(0; 0)**, of the lower right corner � **(1; 1)**.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - Coordinates of the starting point of the line.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Coordinates of the intermediate point of the line.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v2** - Coordinates of the ending point of the line.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Line color.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void renderLine3D ( const Math:: Vec3 & v0 , const Math:: Vec3 & v1 , const Math:: Vec3 & v2 , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true )

Renders a 3D line of a given color. 3D lines are rendered in the world space.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - Coordinates of the starting point of the line.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Coordinates of the intermediate point of the line.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v2** - Coordinates of the ending point of the line.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Line color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderLine2D ( const Math:: vec2 & v0 , const Math:: vec2 & v1 , const Math:: vec2 & v2 , const Math:: vec2 & v3 , const Math:: vec4 & color , float order = 0.0f , float duration = 0.0f )

Renders a 2D line of a given color. 2D lines are rendered in the screen plane; coordinates of the upper left corner are **(0; 0)**, of the lower right corner � **(1; 1)**.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - Coordinates of the starting point of the line.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Coordinates of the first intermediate point of the line.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v2** - Coordinates of the second intermediate point of the line.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v3** - Coordinates of the ending point of the line.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the line will be rendered.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void renderLine3D ( const Math:: Vec3 & v0 , const Math:: Vec3 & v1 , const Math:: Vec3 & v2 , const Math:: Vec3 & v3 , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true )

Renders a 3D line of a given color. 3D lines are rendered in the world space.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - Coordinates of the starting point of the line.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Coordinates of the first intermediate point of the line.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v2** - Coordinates of the second intermediate point of the line.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v3** - Coordinates of the ending point of the line.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the line will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderTriangle2D ( const Math:: vec2 & v0 , const Math:: vec2 & v1 , const Math:: vec2 & v2 , const Math:: vec4 & color , float order = 0.0f , float duration = 0.0f ) const

Renders a 2D triangle of a given color. 2D triangles are rendered in the screen plane; coordinates of the upper left corner are **(0; 0)**, of the lower right corner�**(1; 1)**.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - Coordinates of the first vertex.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Coordinates of the second vertex.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v2** - Coordinates of the third vertex.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Triangle color.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void renderTriangle3D ( const Math:: Vec3 & v0 , const Math:: Vec3 & v1 , const Math:: Vec3 & v2 , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true ) const

Renders a 3D triangle of a given color. 3D triangles are rendered in the world space.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - Coordinates of the first vertex.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Coordinates of the second vertex.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v2** - Coordinates of the third vertex.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Triangle color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderQuad2D ( const Math:: vec2 & v0 , const Math:: vec2 & v1 , const Math:: vec2 & v2 , const Math:: vec2 & v3 , const Math:: vec4 & color , float order = 0.0f , float duration = 0.0f ) const

Renders a 2D quad of a given color. 2D quads are rendered in the screen plane; coordinates of the upper left corner are **(0; 0)**, of the lower right corner�**(1; 1)**.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v0** - Coordinates of the first vertex.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v1** - Coordinates of the second vertex.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v2** - Coordinates of the third vertex.
- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **v3** - Coordinates of the fourth vertex.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the quad will be rendered.
- *float* **order** - Z-order value for the rendered element. An element having a *lower* order shall be rendered *over* the one having a *higher* one.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void renderQuad3D ( const Math:: Vec3 & v0 , const Math:: Vec3 & v1 , const Math:: Vec3 & v2 , const Math:: Vec3 & v3 , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true ) const

Renders a 3D quad of a given color. 3D quads are rendered in the world space.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v0** - Coordinates of the first vertex.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v1** - Coordinates of the second vertex.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v2** - Coordinates of the third vertex.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v3** - Coordinates of the fourth vertex.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the quad will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderBillboard3D ( const Math:: Vec3 & v , float size , const Math:: vec4 & texcoord , bool screen_space = false , float duration = 0.0f , bool depth_test = true ) const

Renders a 3D billboard of the specified size. You can customize billboard image via **[setTextureName()](../../...md#setTextureName_cstr_void)**.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **v** - Coordinates of the billboard.
- *float* **size** - The billboard size in units (meters).
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **texcoord** - The billboard texture coordinates, consisting of two pairs of vector elements (x, y, z, w):

  - x - texture size along the X axis in range [0.0f; 1.0f]
  - y - texture size along the Y axis in range [0.0f; 1.0f]
  - z - offset of the texture's starting position along the X axis in range [0.0f; 1.0f]
  - w - offset of the texture's starting position along the Y axis [0.0f; 1.0f]
- *bool* **screen_space** - Flag indicating the type of dimensions to be used:

  - **false** - use the world space dimensions
  - **true** - use the screen space dimensions
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderVector ( const Math:: Vec3 & position_start , const Math:: Vec3 & position_end , const Math:: vec4 & color , float arrow_size = 0.25f , bool screen_space = false , float duration = 0.0f , bool depth_test = true ) const

Renders a vector of a given color.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position_start** - Coordinates of the vector origin.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position_end** - Coordinates of the vector target.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Vector color.
- *float* **arrow_size** - Relative length of the arrowhead (cone) with respect to the total vector length. For example, the default value of 0.25f means that the arrowhead occupies 25% of the overall arrow length.
- *bool* **screen_space** - Flag indicating the type of dimensions to be used:

  - **false** - use the world space dimensions
  - **true** - use the screen space dimensions
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderDirection ( const Math:: Vec3 & position , const Math:: vec3 & direction , const Math:: vec4 & color , float arrow_size = 0.25f , bool screen_space = true , float duration = 0.0f , bool depth_test = true ) const

Renders a direction vector of a given color.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - Coordinates of the vector origin.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **direction** - Target vector direction.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Vector color.
- *float* **arrow_size** - Relative length of the arrowhead (cone) with respect to the total vector length. For example, the default value of 0.25f means that the arrowhead occupies 25% of the overall arrow length.
- *bool* **screen_space** - Flag indicating the type of dimensions to be used:

  - **false** - use the world space dimensions
  - **true** - use the screen space dimensions
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderBox ( const Math:: vec3 & size , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true ) const

Renders a box of a given color.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Dimensions of the box.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix, which is used to position the box.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the box will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderFrustum ( const Math:: mat4 & projection , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true ) const

Renders a wireframe frustum of a given color.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **projection** - Projection matrix used to transform the coordinates.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix used to position the frustum.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the frustum will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderCircle ( float radius , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true ) const

Renders a wireframe circle of a given color.
### Arguments

- *float* **radius** - Radius of the circle.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix used to position the circle.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Circle color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderSector ( float radius , float angle , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true ) const

Renders a wireframe sector of a given color.
### Arguments

- *float* **radius** - Radius of the circle from which a sector is cut.
- *float* **angle** - Angle of the sector.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix used to position the sector.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Sector color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderCone ( float radius , float angle , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true ) const

Renders a wireframe cone of a given color.
### Arguments

- *float* **radius** - Radius of the cone.
- *float* **angle** - Angle of the cone.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix used to position the cone.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the cone will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderSphere ( float radius , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true ) const

Renders a wireframe sphere of a given color.
### Arguments

- *float* **radius** - Radius of the sphere.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix used to position the sphere.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Sphere color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderCapsule ( float radius , float height , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true ) const

Renders a wireframe capsule (capped cylinder) of a given color.
### Arguments

- *float* **radius** - Radius of the capsule.
- *float* **height** - Height of the capsule.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix used to position the capsule.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Capsule color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderCylinder ( float radius , float height , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true ) const

Renders a wireframe cylinder of a given color.
### Arguments

- *float* **radius** - Radius of the cylinder.
- *float* **height** - Height of the cylinder.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix used to position the cylinder.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Cylinder color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderEllipse ( const Math:: vec3 & radius , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true ) const

Renders a wireframe ellipse of a given color.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **radius** - Ellipse radius values along three axes.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix for the ellipse.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Ellipse color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderSolidBox ( const Math:: vec3 & size , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true ) const

Renders a solid box of a given color.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **size** - Size of the solid box.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix used to position the solid box.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Box color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderSolidSphere ( float radius , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true ) const

Renders a solid sphere of a given color.
### Arguments

- *float* **radius** - Radius of the solid sphere.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix used to position the solid sphere.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Sphere color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderSolidCapsule ( float radius , float height , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true ) const

Renders a solid capsule af a given color.
### Arguments

- *float* **radius** - Radius of the capsule.
- *float* **height** - Height of the capsule.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix used to position the capsule.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Capsule color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderSolidCylinder ( float radius , float height , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true ) const

Renders a solid cylinder of a given color.
### Arguments

- *float* **radius** - Radius of the cylinder.
- *float* **height** - Height of the cylinder.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix used to position the cylinder.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Cylinder color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderSolidEllipse ( const Math:: vec3 & radius , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true ) const

Renders a solid ellipse of a given color.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **radius** - Ellipse radius values along three axes.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix used to position the ellipse.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Ellipse color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderRectangle ( const Math:: vec4 & rectangle , const Math:: vec4 & color , float duration = 0.0f )

Renders a 2D wireframe rectangle of a given color.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **rectangle** - Four-component vector containing the coordinates of the upper-left (first two components) and bottom-right (second two components) corners of the rectangle.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Rectangle color.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void renderBoundBox ( const Math:: BoundBox & bb , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true )

Renders the bounding box of a given color.
### Arguments

- *const  Math::[BoundBox](../../../api/library/math/bounds/class.boundbox_cpp.md) &* **bb** - The bounding box.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix for the bounding box.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the box will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderBoundSphere ( const Math:: BoundSphere & bs , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true )

Renders the bounding sphere of a given color.
### Arguments

- *const  Math::[BoundSphere](../../../api/library/math/bounds/class.boundsphere_cpp.md) &* **bs** - The bounding sphere.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix for the bounding sphere.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the sphere will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderNodeBoundBox ( const Ptr < Node > & node , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true )

Renders an axis-aligned bound box of a given node.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node, for which the bound box is rendered.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the box will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderNodeBoundSphere ( const Ptr < Node > & node , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true )

Renders a bound sphere of a given node.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node, for which the bound sphere is rendered.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the sphere will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderObjectSurfaceBoundBox ( const Ptr < Object > & object , int surface , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true )

Renders a bound box of a given object surface.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)> &* **object** - Object, which contains the target surface.
- *int* **surface** - The number of the target surface in the object.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the box will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderObjectSurfaceBoundSphere ( const Ptr < Object > & object , int surface , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true )

Renders a bound sphere of a given object surface.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)> &* **object** - Object, which contains the target surface.
- *int* **surface** - The number of the target surface in the object.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the sphere will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false � to disable it.

## void renderNodeHandler ( const Ptr < Node > & node , float duration = 0.0f ) const

Renders a handler for the specified node. You can customize handler image via **[setTextureName()](../../...md#setTextureName_cstr_void)**.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node, for which the handler is to be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void renderObject ( const Ptr < Object > & object , const Math:: vec4 & color , float duration = 0.0f ) const

Renders an object wireframe.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)> &* **object** - Object, which wireframe will be rendered.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the wireframe will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void renderObjectSurface ( const Ptr < Object > & object , int surface , const Math:: vec4 & color , float duration = 0.0f ) const

Renders borders of a given object surface.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)> &* **object** - Object, which contains the target surface.
- *int* **surface** - The number of the target surface in the object.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the borders will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void renderSolidObject ( const Ptr < Object > & object , const Math:: vec4 & color , float duration = 0.0f ) const

Renders a solid-colored object.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)> &* **object** - Object smart pointer.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color in which the object will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void renderSolidObjectSurface ( const Ptr < Object > & object , int surface , const Math:: vec4 & color , float duration = 0.0f ) const

Renders a solid-colored surface of a given object.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)> &* **object** - Object smart pointer.
- *int* **surface** - The number of the object's surface.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the object's surface will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void renderMessage2D ( const Math:: vec3 & position , const Math:: vec3 & center , const char * str , const Math:: vec4 & color , int outline , int font_size = -1 , float duration = 0.0f )

Renders a message in a given color. Message position is specified in screen coordinates.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - Coordinates of the anchor point of the message, each in **[0;1]** range.
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **center** - Message alignment. The first two values in the vector set the offset, the third one is ignored. For example, vec3(-1,-1,0) sets the offset of the center of the message to its upper left edge. vec3(1,1,0) - to the lower right corner.
- *const char ** **str** - Message text to display.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the message will be rendered.
- *int* **outline** - **1** to use font outlining, **0** not to use.
- *int* **font_size** - Font size.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## void renderMessage3D ( const Math:: Vec3 & position , const Math:: vec3 & center , const char * str , const Math:: vec4 & color , int outline , int font_size = -1 , float duration = 0.0f )

Renders a message in a given color. Message position is specified in world coordinates.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **position** - Coordinates of the anchor point of the message (in world coordinates).
- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **center** - Message alignment. The first two values in the vector set the offset, the third one is ignored. For example, vec3(-1,-1,0) sets the offset of the center of the message to its upper left edge. vec3(1,1,0) - to the lower right corner.
- *const char ** **str** - Message text to display.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the message will be rendered.
- *int* **outline** - **1** to use font outlining, **0** not to use.
- *int* **font_size** - Font size.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.

## Ptr < Node > getHandlerNode ( int num ) const


Returns the handler node by its index.


> **Notice:** The handler index may change every frame depending on the camera transforms (i.e. how many handlers are visible in the current frame), therefore it is not recommended to save and reuse this value.


### Arguments

- *int* **num** - Handler node index in the range from 0 to the [total number of handlers](#getNumHandlers_int).

### Return value

The node for which the handler is rendered.
## float getHandlerSize ( int num ) const

Returns the handler icon size in units by its index. This value may be affected by the icon size (set by the [setSize()](#setSize_int_void) method) and by the 3D option ([world_handler_3d](../../../code/console/index.md#world_handler_3d) console command).
### Arguments

- *int* **num** - Handler node index in the range from 0 to the [total number of handlers](#getNumHandlers_int).

### Return value

The handler icon size, in units.
## void renderMesh ( const Ptr < MeshRender > & mesh , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true )

Renders a wireframe of the specified mesh in the given color.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)> &* **mesh** - The mesh to be rendered.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix for the mesh.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the mesh's wireframe will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false - to disable it.

## void renderMesh ( const UGUID & mesh_guid , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true )

Renders a wireframe of the mesh loaded by the specified asset GUID in a given color.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **mesh_guid** - GUID of the mesh asset to be rendered.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix for the mesh.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the mesh's wireframe will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false - to disable it.

## void renderMesh ( const char * path , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true )

Renders a wireframe of the mesh loaded from the specified file path in the given color.
### Arguments

- *const char ** **path** - File path to the mesh to be rendered.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix for the mesh.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the mesh's wireframe will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false - to disable it.

## void renderSolidMesh ( const Ptr < MeshRender > & mesh , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true )

Renders a solid version of the specified mesh in the given color.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[MeshRender](../../../api/library/rendering/class.meshrender_cpp.md)> &* **mesh** - The mesh to be rendered.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix for the mesh.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the mesh will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false - to disable it.

## void renderSolidMesh ( const UGUID & mesh_guid , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true )

Renders a solid version of the mesh loaded by the specified asset GUID in a given color.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **mesh_guid** - GUID of the mesh asset to be rendered.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix for the mesh.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the mesh will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false - to disable it.

## void renderSolidMesh ( const char * path , const Math:: Mat4 & transform , const Math:: vec4 & color , float duration = 0.0f , bool depth_test = true )

Renders a solid version of the mesh loaded from the specified file path in the given color.
### Arguments

- *const char ** **path** - File path to the mesh to be rendered.
- *const  Math::[Mat4](../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation matrix for the mesh.
- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **color** - Color, in which the mesh's wireframe will be rendered.
- *float* **duration** - Time period (in seconds) during which the rendered element shall be displayed. The default value of 0 means that the visualizer is rendered for 1 frame only.
- *bool* **depth_test** - true to enable depth testing for the element (if it should be obscured by elements closer to the camera); false - to disable it.

## void clearNodeTypeIcons ( )

Removes all custom per-node-type handler icons set via **[setNodeTypeIcon()](../../...md#setNodeTypeIcon_int_cstr_int)**, so all node handlers revert to the default icon.
## bool setNodeTypeIcon ( Node::TYPE type , const char * path )

Replaces the billboard icon the visualizer draws for node handlers of the given node type (the per-node icons shown when visualizer node handlers are enabled). Node types without a custom icon keep the default handler icon.
### Arguments

- *[Node::TYPE](../../../api/library/nodes/class.node_cpp.md#TYPE)* **type** - Node type, one of the *Node::TYPE* values.
- *const char ** **path** - Path to the icon image file.

### Return value

true if the icon is set successfully; otherwise, false (the type is out of range or the image cannot be loaded).
