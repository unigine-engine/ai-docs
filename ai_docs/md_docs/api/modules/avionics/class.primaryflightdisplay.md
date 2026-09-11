# PrimaryFlightDisplay Component

**Inherits from:** ComponentBase


**Primary Flight Display** (**PFD**) is the main instrument for pilots in modern glass cockpits. This component renders a fully functional PFD to a texture, which can then be displayed on any 3D surface in your scene - such as a cockpit screen, MFD panel, or in-game monitor.


The display combines several critical flight instruments into a single view: artificial horizon (shows aircraft pitch and roll relative to the horizon with pitch ladder markings every 10 degrees and roll indicator arc), heading tape (horizontal compass strip at the top showing current heading with tick marks), airspeed tape (vertical speed indicator on the left side with color-coded ranges for flap operating, normal, and caution ranges), altitude tape (vertical altitude indicator on the right side), vertical speed indicator (shows rate of climb or descent), and slip/skid indicator (shows lateral acceleration for coordinated flight).


To use this component, attach it to an ObjectMeshStatic that has a surface with an albedo texture slot. The component will render the PFD to that texture each frame. Connect your flight model outputs (pitch, roll, airspeed, altitude, etc.) to the runtime parameters to drive the display.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Runtime Group |  |  |
| In Yaw | *Float* | Input yaw angle. |
| In Pitch | *Float* | Input pitch angle. |
| In Roll | *Float* | Input roll angle. |
| In Altitude | *Float* | Input altitude value. |
| In Airspeed | *Float* | Input airspeed value. |
| In Vertical Speed | *Float* | Input vertical speed value. |
| In Skid Slip | *Float* | Input skid/slip value in [-1, 1] range. |
| In Flap Operating Range | *Vec2* | Flap operating speed range. |
| In Normal Operating Range | *Vec2* | Normal operating speed range. |
| In Caution Range | *Vec2* | Caution speed range. |
| Settings Group |  |  |
| Width | *Int* | Display width in pixels (*default: 400*). |
| Height | *Int* | Display height in pixels (*default: 300*). |
| Surface Name | *String* | Name of the surface to render to (*default: "surface"*). |
| Texture Name | *String* | Name of the texture slot (*default: "albedo"*). |
| Horizon Image | *File* | Path to the horizon background image. |
| Pixels Per Pitch Deg | *Float* | Pixels per degree of pitch (*default: 2.2*). |
| Heading Bg Height | *Float* | Height of heading background (*default: 35*). |
| Airspeed Bg Width | *Float* | Width of airspeed background (*default: 64*). |
| Altitude Bg Width | *Float* | Width of altitude background (*default: 60*). |
| Vertical Speed Bg Width | *Float* | Width of vertical speed background (*default: 25*). |
| Horizon Pitch Tick Step | *Int* | Pitch tick step in degrees (*default: 10*). |
| Horizon Roll Tick Step | *Int* | Roll tick step in degrees (*default: 5*). |
| Heading Tick Step | *Int* | Heading tick step in degrees (*default: 5*). |
| Airspeed Tick Step | *Int* | Airspeed tick step (*default: 10*). |
| Altitude Tick Step | *Int* | Altitude tick step (*default: 100*). |


### See Also


- **[AvionicsHUD](../../../api/modules/avionics/class.avionicshud.md)**
