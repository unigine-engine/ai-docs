# TelemetryUI Component

**Inherits from:** ComponentBase


TelemetryUI displays real-time flight telemetry data as an on-screen overlay. It shows drone name, configuration, vertical speed, ground speed, air speed, heading, height, home distance, battery voltage, signal strength, and GPS status.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Position Offset | *Vec2* | (350, 180) | Screen position offset. |
| Font Name | *String* | � | Font file for telemetry text. |
| Font Outline | *Toggle* | true | Enable text outline. |
| Font Color | *Color* | (0.9, 0.9, 0.9, 1.0) | Text color. |
| Font Size | *Int* | 18 | Text size in pixels. |


### See Also


- **[Drone](../../../../api/templates/template_aviation_uav/drone/class.drone.md)**
- **[MinimapUI](../../../../api/templates/template_aviation_uav/ui/class.minimapui.md)**
