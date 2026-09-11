# MeteoRadar Component

**Inherits from:** ComponentBase


MeteoRadar simulates a weather radar (**WXR**) that scans the environment for cloud formations and terrain. It generates a real-time image showing precipitation intensity and terrain shadows, similar to cockpit weather radar displays.


The radar works by casting rays in a fan pattern defined by the FOV parameter, sampling cloud density at each point along the ray, mapping density to color (green for light, yellow for moderate, red for heavy precipitation), and detecting terrain intersections to show ground shadows.


The radar integrates with the **IG** weather system, using cloud layer humidity values to determine reflectivity. Unknown clouds use a default reflectivity factor.


For performance, the radar processes one column at a time per frame, sweeping left-to-right and then right-to-left continuously. Multi-threaded processing is used via CPUShader for efficiency.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Radar Group |  |  |
| Orientation Euler | *Vec3* | Radar antenna orientation offset in degrees. |
| Fixed Rotation | *Toggle* | Fix radar rotation relative to aircraft. |
| Gain | *Float* | Sensitivity threshold for display (*default: 0.1*). |
| Shadow Gain | *Float* | Maximum reflection sum before shadow effect starts (*default: 10.0*). |
| FOV | *Float* | Field of view angle in degrees (*default: 90*). |
| Range Group |  |  |
| Min Range | *Float* | Minimum scan distance in meters (*default: 0*). |
| Max Range | *Float* | Maximum scan distance in meters (*default: 20000*). |
| Width | *Int* | Horizontal resolution (number of rays) (*default: 500*). |
| Height | *Int* | Vertical resolution (distance samples per ray) (*default: 500*). |


## MeteoRadar Class

---

## getImage ( )

Returns the current radar display image. Update this image to a texture for display.
### Return value

The radar display image.
## void resize ( )

Resizes the radar display image.
### Arguments
