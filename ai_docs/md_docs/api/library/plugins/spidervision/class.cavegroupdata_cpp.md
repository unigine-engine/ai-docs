# Unigine::Plugins::SpiderVision::CAVEGroupData Class (CPP)

**Header:** #include <plugins/Unigine/SpiderVision/UnigineSpiderVision.h>


This class stores the parameters of a CAVE viewport group, the programmatic counterpart of the CAVE generator available in the *SpiderVision* setup window. The CAVE (Cave Automatic Virtual Environment) generator creates a CAVE room made of display-type viewports: the left, back, and right walls and the bottom (floor) are always created, while the front wall and the top (ceiling) are optional.


Generating the group (see the *[GroupData](../../../../api/library/plugins/spidervision/class.groupdata_cpp.md)* base class) creates the member viewports and applies the group parameters to them. All parameters, except **[isUseFrontSide()](../../../...md#isUseFrontSide_int)** and **[isUseTopSide()](../../../...md#isUseTopSide_int)**, may be changed later: for a generated group each setter automatically refreshes the derived parameters of every member viewport.


## CAVEGroupData Class

### Members

## void setCenterOffset ( const Math:: vec2 & offset )

Sets a new offset of the center of the generated CAVE group relative to its default position, in meters.
### Arguments

- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md)&* **offset** - The offset of the CAVE group center, in meters

## Math:: vec2 getCenterOffset () const

Returns the current offset of the center of the generated CAVE group relative to its default position, in meters.
### Return value

Current offset of the CAVE group center, in meters
## void setWallSize ( const Math:: vec2 & size )

Sets a new dimensions (width and height) of the generated CAVE walls, in meters.
### Arguments

- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md)&* **size** - The dimensions of the CAVE walls, in meters

## Math:: vec2 getWallSize () const

Returns the current dimensions (width and height) of the generated CAVE walls, in meters.
### Return value

Current dimensions of the CAVE walls, in meters
## void setFloorSize ( const Math:: vec2 & size )

Sets a new dimensions (width and depth) of the generated CAVE floor and ceiling, in meters.
### Arguments

- *const  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md)&* **size** - The dimensions of the CAVE floor and ceiling, in meters

## Math:: vec2 getFloorSize () const

Returns the current dimensions (width and depth) of the generated CAVE floor and ceiling, in meters.
### Return value

Current dimensions of the CAVE floor and ceiling, in meters
## void setPixelDensity ( float density )

Sets a new pixel density assigned to the viewports of the generated CAVE group, in pixels per meter: the render texture size is calculated automatically from the physical screen dimensions and the specified pixel density, preserving the correct aspect ratio. The default value is 1200.
### Arguments

- *float* **density** - The pixel density of the generated group, in pixels per meter

## float getPixelDensity () const

Returns the current pixel density assigned to the viewports of the generated CAVE group, in pixels per meter: the render texture size is calculated automatically from the physical screen dimensions and the specified pixel density, preserving the correct aspect ratio. The default value is 1200.
### Return value

Current pixel density of the generated group, in pixels per meter
## void setWindowSize ( const Math:: ivec2 & size )

Sets a new size of the generated application windows, in pixels. The default value is 1920x1080.
### Arguments

- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md)&* **size** - The size of the generated application windows, in pixels

## Math:: ivec2 getWindowSize () const

Returns the current size of the generated application windows, in pixels. The default value is 1920x1080.
### Return value

Current size of the generated application windows, in pixels
## void setExclusiveFullscreen ( bool fullscreen )

Sets a new value indicating if all generated windows use the exclusive fullscreen mode. When disabled (default), the windows are created in the borderless windowed mode.
### Arguments

- *bool* **fullscreen** - Set **true** to enable exclusive fullscreen mode for the generated windows; **false** - to disable it.

## bool isExclusiveFullscreen () const

Returns the current value indicating if all generated windows use the exclusive fullscreen mode. When disabled (default), the windows are created in the borderless windowed mode.
### Return value

**true** if exclusive fullscreen mode for the generated windows is enabled ; otherwise **false**.
## void setStereo ( bool stereo )

Sets a new value indicating if the generated viewports use stereo (side-by-side stereo image) rendering instead of mono (single image). Disabled by default.
### Arguments

- *bool* **stereo** - Set **true** to enable stereo rendering of the generated viewports; **false** - to disable it.

## bool isStereo () const

Returns the current value indicating if the generated viewports use stereo (side-by-side stereo image) rendering instead of mono (single image). Disabled by default.
### Return value

**true** if stereo rendering of the generated viewports is enabled ; otherwise **false**.
## void setInverse ( bool inverse )

Sets a new value indicating if the viewports are configured for rear-projection systems (the walls are flipped). Enable this option when the image is projected onto the back side of the screen. Disabled by default.
### Arguments

- *bool* **inverse** - Set **true** to enable rear-projection configuration of the generated viewports; **false** - to disable it.

## bool isInverse () const

Returns the current value indicating if the viewports are configured for rear-projection systems (the walls are flipped). Enable this option when the image is projected onto the back side of the screen. Disabled by default.
### Return value

**true** if rear-projection configuration of the generated viewports is enabled ; otherwise **false**.
## void setUseTopSide ( bool side )

Sets a new value indicating if the top (ceiling) viewport is created when the CAVE is generated. Unlike the other parameters, it cannot be changed after the group has been generated. Disabled by default.
### Arguments

- *bool* **side** - Set **true** to enable adding the ceiling when generating the CAVE; **false** - to disable it.

## bool isUseTopSide () const

Returns the current value indicating if the top (ceiling) viewport is created when the CAVE is generated. Unlike the other parameters, it cannot be changed after the group has been generated. Disabled by default.
### Return value

**true** if adding the ceiling when generating the CAVE is enabled ; otherwise **false**.
## void setUseFrontSide ( bool side )

Sets a new value indicating if the front wall viewport is created when the CAVE is generated. Unlike the other parameters, it cannot be changed after the group has been generated. Disabled by default.
### Arguments

- *bool* **side** - Set **true** to enable adding the front wall when generating the CAVE; **false** - to disable it.

## bool isUseFrontSide () const

Returns the current value indicating if the front wall viewport is created when the CAVE is generated. Unlike the other parameters, it cannot be changed after the group has been generated. Disabled by default.
### Return value

**true** if adding the front wall when generating the CAVE is enabled ; otherwise **false**.
