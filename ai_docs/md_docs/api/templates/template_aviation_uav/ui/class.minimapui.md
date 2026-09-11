# MinimapUI Component

**Inherits from:** ComponentBase


MinimapUI displays a minimap overlay showing drone position, home location, flight path, north indicator, and distance circles. The map can be zoomed and shows a rendered path trail of the drone's flight history.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Markers Group |  |  |  |
| Home Marker | *File* | � | Image for home location marker. |
| Player Marker | *File* | � | Image for drone position marker. |
| North Marker | *File* | � | Image for north indicator. |
| Markers Size | *Float* | 25.0 | Size of marker icons. |
| Map Group |  |  |  |
| Map Image | *File* | � | Background map image (1:1 ratio). |
| Distance Circle Radius | *Float* | 25.0 | Radius of distance circles. |
| Distance Circle Font Size | *Float* | 14.0 | Font size for distance labels. |
| Distance Circles Color | *Color* | #ffffff | Color of distance circles. |
| Path Thickness | *Float* | 10.0 | Flight path line thickness. |
| Path Smoothness | *Float* | 1.0 | Path edge anti-aliasing width. |
| Path Color | *Color* | #4a5564 | Flight path line color. |
| Horizon Color | *Color* | #a4c0ff60 | Horizon indicator color. |
| Pixel To Unit Ratio | *Float* | 1.0 | Map scale ratio. |
| Origin Offset | *Vec2* | � | Map center offset. |
| Map Zoom | *Float* | 1.0 | Initial zoom level. |
| Zoom Curve | *Curve2d* | � | Zoom interpolation curve. |
| Widget Group |  |  |  |
| Widget Padding | *Vec2* | (20, 20) | Screen edge padding. |
| Widget Size | *Float* | 200.0 | Minimap widget size. |


### See Also


- **[TelemetryUI](../../../../api/templates/template_aviation_uav/ui/class.telemetryui.md)**
- **[Drone](../../../../api/templates/template_aviation_uav/drone/class.drone.md)**
