# Unigine::Plugins::SpiderVision::WallGroupData Class (CS)


The object of this class represents a group of viewports arranged in a defined number of rows and columns with a specified distance between the viewports and orientation of viewports thus creating a [wall](../../../../principles/render/output/multi_monitor/spidervision_plugin/presets.md#wall).


## WallGroupData Class

### Properties

## ivec2 Size

The size of the wall, number of columns and rows.
## vec2 Offset

The horizontal and vertical distances between the edges of the neighboring viewports in the wall.
## vec2 DisplaySize

The actual width and height of the display in the Wall group. It is assumed that the wall consists of identical displays. If sizes of displays differ, you may consider creating a configuration with several Wall groups.
## ivec2 WindowSize

The width and height of the window on the display screen.
## float DistanceToViewer

The distance from the viewer point to the center of the group.
## float Angle

The angle between the neighboring displays in the XY plane (i.e. around the Z axis).
## bool AutoArrange

The value indicating if automatic positioning of windows on the displays is enabled. If disabled, all windows are created with the position (0, 0) at the same place and are to be positioned manually.
## float Aspect

The
## float VFov

The
## ViewportData.DISPLAY_TRANSFORM_TYPE TransformType

The
### Members

---

## void Generate ( )

Generates a group of viewports using the [createViewport()](../../../../api/library/plugins/spidervision/class.displaysconfig_cs.md#createViewport_int_ViewportData) method.
## void Refresh ( )

Updates the viewports' position and orientation based on the specified [size](#setSize_ivec2_void), [offset](#setOffset_vec2_void), [distance to viewer](#setDistanceToViewer_float_void), and [angle](#setAngle_float_void) values.
