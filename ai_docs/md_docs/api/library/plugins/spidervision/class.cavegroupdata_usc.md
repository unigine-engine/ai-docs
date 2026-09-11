# Unigine::Plugins::SpiderVision::CAVEGroupData Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class stores the parameters of a CAVE viewport group, the programmatic counterpart of the CAVE generator available in the *SpiderVision* setup window. The CAVE (Cave Automatic Virtual Environment) generator creates a CAVE room made of display-type viewports: the left, back, and right walls and the bottom (floor) are always created, while the front wall and the top (ceiling) are optional.


Generating the group (see the *[GroupData](../../../../api/library/plugins/spidervision/class.groupdata_usc.md)* base class) creates the member viewports and applies the group parameters to them. All parameters, except **[isUseFrontSide()()](../../../...md#isUseFrontSide_int)** and **[isUseTopSide()()](../../../...md#isUseTopSide_int)**, may be changed later: for a generated group each setter automatically refreshes the derived parameters of every member viewport.


## CAVEGroupData Class

### Members

## void setCenterOffset ( vec2 offset )

Sets a new offset of the center of the generated CAVE group relative to its default position, in meters.
### Arguments

- *vec2* **offset** - The offset of the CAVE group center, in meters

## vec2 getCenterOffset () const

Returns the current offset of the center of the generated CAVE group relative to its default position, in meters.
### Return value

Current offset of the CAVE group center, in meters
## void setWallSize ( vec2 size )

Sets a new dimensions (width and height) of the generated CAVE walls, in meters.
### Arguments

- *vec2* **size** - The dimensions of the CAVE walls, in meters

## vec2 getWallSize () const

Returns the current dimensions (width and height) of the generated CAVE walls, in meters.
### Return value

Current dimensions of the CAVE walls, in meters
## void setFloorSize ( vec2 size )

Sets a new dimensions (width and depth) of the generated CAVE floor and ceiling, in meters.
### Arguments

- *vec2* **size** - The dimensions of the CAVE floor and ceiling, in meters

## vec2 getFloorSize () const

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
## void setWindowSize ( ivec2 size )

Sets a new size of the generated application windows, in pixels. The default value is 1920x1080.
### Arguments

- *ivec2* **size** - The size of the generated application windows, in pixels

## ivec2 getWindowSize () const

Returns the current size of the generated application windows, in pixels. The default value is 1920x1080.
### Return value

Current size of the generated application windows, in pixels
## void setExclusiveFullscreen ( int fullscreen )

Sets a new value indicating if all generated windows use the exclusive fullscreen mode. When disabled (default), the windows are created in the borderless windowed mode.
### Arguments

- *int* **fullscreen** - The exclusive fullscreen mode for the generated windows

## int isExclusiveFullscreen () const

Returns the current value indicating if all generated windows use the exclusive fullscreen mode. When disabled (default), the windows are created in the borderless windowed mode.
### Return value

Current exclusive fullscreen mode for the generated windows
## void setStereo ( int stereo )

Sets a new value indicating if the generated viewports use stereo (side-by-side stereo image) rendering instead of mono (single image). Disabled by default.
### Arguments

- *int* **stereo** - The stereo rendering of the generated viewports

## int isStereo () const

Returns the current value indicating if the generated viewports use stereo (side-by-side stereo image) rendering instead of mono (single image). Disabled by default.
### Return value

Current stereo rendering of the generated viewports
## void setInverse ( int inverse )

Sets a new value indicating if the viewports are configured for rear-projection systems (the walls are flipped). Enable this option when the image is projected onto the back side of the screen. Disabled by default.
### Arguments

- *int* **inverse** - The rear-projection configuration of the generated viewports

## int isInverse () const

Returns the current value indicating if the viewports are configured for rear-projection systems (the walls are flipped). Enable this option when the image is projected onto the back side of the screen. Disabled by default.
### Return value

Current rear-projection configuration of the generated viewports
## void setUseTopSide ( int side )

Sets a new value indicating if the top (ceiling) viewport is created when the CAVE is generated. Unlike the other parameters, it cannot be changed after the group has been generated. Disabled by default.
### Arguments

- *int* **side** - The adding the ceiling when generating the CAVE

## int isUseTopSide () const

Returns the current value indicating if the top (ceiling) viewport is created when the CAVE is generated. Unlike the other parameters, it cannot be changed after the group has been generated. Disabled by default.
### Return value

Current adding the ceiling when generating the CAVE
## void setUseFrontSide ( int side )

Sets a new value indicating if the front wall viewport is created when the CAVE is generated. Unlike the other parameters, it cannot be changed after the group has been generated. Disabled by default.
### Arguments

- *int* **side** - The adding the front wall when generating the CAVE

## int isUseFrontSide () const

Returns the current value indicating if the front wall viewport is created when the CAVE is generated. Unlike the other parameters, it cannot be changed after the group has been generated. Disabled by default.
### Return value

Current adding the front wall when generating the CAVE
