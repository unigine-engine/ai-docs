# AvionicsHUD Component

**Inherits from:** ComponentBase


**Head-Up Display** (**HUD**) is a transparent display that presents flight data directly in the pilot's field of view, eliminating the need to look down at instruments. This component renders a fully configurable aviation HUD as a screen overlay using WidgetCanvas.


Unlike **[PrimaryFlightDisplay](../../../api/modules/avionics/class.primaryflightdisplay.md)** which renders to a texture for cockpit screens, AvionicsHUD draws directly on the main window, making it ideal for fighter jet or military aircraft simulations, debug/development overlay to monitor flight parameters, or simplified cockpit setups where separate instrument textures aren't needed.


The HUD displays comprehensive flight information including speed tapes (true airspeed and ground speed), altitude (above ground and above sea level), heading with compass tape, attitude with pitch ladder and roll indication, control surfaces positions (aileron, elevator, rudder and their trim), plus throttle, G-load, and geographic coordinates in DMS format.


Each element can be individually enabled/disabled via component parameters. The HUD color is configurable (default green, typical for aviation HUDs).


### Component Parameters


| Name | Type | Description |
|---|---|---|
| HUD Settings Group |  |  |
| Default Unit Speed Label | *String* | Label for speed units (*default: "kts"*). |
| Geocoords Enabled | *Toggle* | Show geographic coordinates (*default: true*). |
| Throttle Enabled | *Toggle* | Show throttle indicator (*default: true*). |
| G Load Enabled | *Toggle* | Show G-load indicator (*default: true*). |
| True Speed Enabled | *Toggle* | Show true airspeed (*default: true*). |
| Ground Speed Enabled | *Toggle* | Show ground speed (*default: true*). |
| Ground Altitude Enabled | *Toggle* | Show altitude above ground (*default: true*). |
| Sea Altitude Enabled | *Toggle* | Show altitude above sea level (*default: true*). |
| Heading Enabled | *Toggle* | Show heading indicator (*default: true*). |
| Control Surfaces Enabled | *Toggle* | Show control surfaces state (*default: true*). |
| Attitude Motion Enabled | *Toggle* | Enable attitude motion display (*default: true*). |
| Turn Bank Enabled | *Toggle* | Show turn and bank indicator (*default: true*). |
| Runtime Group |  |  |
| In Hud Color | *Color* | HUD elements color (*default: green*). |
| In Lat | *Double* | Input latitude (*default: 0*). |
| In Lon | *Double* | Input longitude (*default: 0*). |
| In Throttle | *Float* | Input throttle value (*default: 0*). |
| In G Load | *Float* | Input G-load value (*default: 0*). |
| In True Speed | *Float* | Input true airspeed (*default: 0*). |
| In Ground Speed | *Float* | Input ground speed (*default: 0*). |
| In Ground Altitude | *Float* | Input altitude above ground (*default: 0*). |
| In Sea Altitude | *Float* | Input altitude above sea level (*default: 0*). |
| In Gyrocompass | *Float* | Input heading from gyrocompass (*default: 0*). |
| In Pitch | *Float* | Input pitch angle (*default: 0*). |
| In Roll | *Float* | Input roll angle (*default: 0*). |
| In Aileron | *Float* | Input aileron position (*default: 0*). |
| In Aileron Trim | *Float* | Input aileron trim (*default: 0*). |
| In Elevator | *Float* | Input elevator position (*default: 0*). |
| In Elevator Trim | *Float* | Input elevator trim (*default: 0*). |
| In Rudder | *Float* | Input rudder position (*default: 0*). |
| In Rudder Trim | *Float* | Input rudder trim (*default: 0*). |
| In Turn Bank | *Float* | Input turn and bank value (*default: 0.0*). |


### See Also


- **[PrimaryFlightDisplay](../../../api/modules/avionics/class.primaryflightdisplay.md)**


## AvionicsHUD Class
