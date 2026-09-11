# Attitude Component

**Inherits from:** ComponentBase


Attitude indicator (also known as artificial horizon) is arguably the most important instrument for flight in conditions without visual reference to the ground. This component renders a fully functional attitude indicator to a texture for display on cockpit instrument panels.


The instrument displays pitch (aircraft nose position relative to the horizon, clamped to +/-90 degrees), roll (aircraft bank angle shown by rotation of the horizon line), and a slip/skid ball that indicates whether the aircraft is in coordinated flight by showing lateral acceleration.


The slip/skid indicator uses a low-pass filter for smooth, realistic ball movement based on lateral (Y) and vertical (Z) acceleration inputs, simulating the inertia of a real inclinometer ball.


To use this component, attach it to a mesh object with a surface that has an albedo texture slot, provide the required texture and material assets, and connect your flight model's pitch, roll, and acceleration outputs to the runtime parameters.


For managing multiple analog indicators together, consider using **[AvionicsIndicatorsController](../../../api/modules/avionics/class.avionicsindicatorscontroller.md)**.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Render Settings Group |  |  |
| Size | *IVec2* | Render target size in pixels (*default: (400, 400)*). |
| Surface Name | *String* | Name of the surface to render to (*default: "plane"*). |
| Texture Name | *String* | Name of the texture slot (*default: "albedo"*). |
| Settings Group |  |  |
| Frame Image | *File* | Path to the frame image (*default: "modules/avionics/frame.png"*). |
| Attitude Material | *File* | Path to the attitude material (*default: "modules/avionics/attitude/attitude.basemat"*). |
| At Image | *File* | Path to the attitude image (*default: "modules/avionics/attitude/attitude.png"*). |
| At Mask Image | *File* | Path to the attitude mask image (*default: "modules/avionics/attitude/attitude_mask.png"*). |
| At Overlay Static Image | *File* | Path to the static overlay image (*default: "modules/avionics/attitude/attitude_overlay_static.png"*). |
| At Overlay Dynamic Image | *File* | Path to the dynamic overlay image (*default: "modules/avionics/attitude/attitude_overlay_dynamic.png"*). |
| Ssb Bg Image | *File* | Path to the slip/skid ball background image (*default: "modules/avionics/attitude/skid_slip_background.png"*). |
| Ssb Ball Image | *File* | Path to the slip/skid ball image (*default: "modules/avionics/attitude/ball.png"*). |
| Ssb Fg Image | *File* | Path to the slip/skid ball foreground image (*default: "modules/avionics/attitude/skid_slip_foreground.png"*). |
| Runtime Group |  |  |
| In Pitch | *Float* | Input pitch angle in degrees. |
| In Roll | *Float* | Input roll angle in degrees. |
| In Y Acceleration Fps | *Float* | Input lateral acceleration in feet per second squared. |
| In Z Acceleration Fps | *Float* | Input vertical acceleration in feet per second squared. |


### See Also


- **[AvionicsIndicatorsController](../../../api/modules/avionics/class.avionicsindicatorscontroller.md)**
