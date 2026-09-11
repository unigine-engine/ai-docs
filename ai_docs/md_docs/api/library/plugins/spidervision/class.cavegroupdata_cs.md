# Unigine::Plugins::SpiderVision::CAVEGroupData Class (CS)


This class stores the parameters of a CAVE viewport group, the programmatic counterpart of the CAVE generator available in the *SpiderVision* setup window. The CAVE (Cave Automatic Virtual Environment) generator creates a CAVE room made of display-type viewports: the left, back, and right walls and the bottom (floor) are always created, while the front wall and the top (ceiling) are optional.


Generating the group (see the *[GroupData](../../../../api/library/plugins/spidervision/class.groupdata_cs.md)* base class) creates the member viewports and applies the group parameters to them. All parameters, except **[UseFrontSide](../../../...md#isUseFrontSide_int)** and **[UseTopSide](../../../...md#isUseTopSide_int)**, may be changed later: for a generated group each setter automatically refreshes the derived parameters of every member viewport.


## CAVEGroupData Class

### Properties

## vec2 CenterOffset

The offset of the center of the generated CAVE group relative to its default position, in meters.
## vec2 WallSize

The dimensions (width and height) of the generated CAVE walls, in meters.
## vec2 FloorSize

The dimensions (width and depth) of the generated CAVE floor and ceiling, in meters.
## float PixelDensity

The pixel density assigned to the viewports of the generated CAVE group, in pixels per meter: the render texture size is calculated automatically from the physical screen dimensions and the specified pixel density, preserving the correct aspect ratio. The default value is 1200.
## ivec2 WindowSize

The size of the generated application windows, in pixels. The default value is 1920x1080.
## bool ExclusiveFullscreen

The value indicating if all generated windows use the exclusive fullscreen mode. When disabled (default), the windows are created in the borderless windowed mode.
## bool Stereo

The value indicating if the generated viewports use stereo (side-by-side stereo image) rendering instead of mono (single image). Disabled by default.
## bool Inverse

The value indicating if the viewports are configured for rear-projection systems (the walls are flipped). Enable this option when the image is projected onto the back side of the screen. Disabled by default.
## bool UseTopSide

The value indicating if the top (ceiling) viewport is created when the CAVE is generated. Unlike the other parameters, it cannot be changed after the group has been generated. Disabled by default.
## bool UseFrontSide

The value indicating if the front wall viewport is created when the CAVE is generated. Unlike the other parameters, it cannot be changed after the group has been generated. Disabled by default.
