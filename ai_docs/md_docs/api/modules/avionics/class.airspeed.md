# Airspeed Component

**Inherits from:** ComponentBase


Airspeed indicator is a classic round-dial instrument found in every aircraft cockpit. This component renders an analog airspeed gauge to a texture, allowing you to display it on 3D surfaces in your scene - instrument panels, cockpit dashboards, or training simulators.


The indicator uses a non-linear scale typical of real airspeed indicators, where the spacing between markings varies across the speed range (0-140 knots). The arrow rotates to point at the current speed value, with smooth interpolation between marked values.


To use this component, attach it to a mesh object with a surface that has an albedo texture slot, configure the render settings (size, surface name, texture name), and feed the In Speed parameter with your aircraft's current airspeed in knots.


For managing multiple analog indicators together, consider using **[AvionicsIndicatorsController](../../../api/modules/avionics/class.avionicsindicatorscontroller.md)** which can update all indicators from a single set of flight data inputs.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Render Settings Group |  |  |
| Size | *IVec2* | Render target size in pixels (*default: (400, 400)*). |
| Surface Name | *String* | Name of the surface to render to (*default: "plane"*). |
| Texture Name | *String* | Name of the texture slot (*default: "albedo"*). |
| Settings Group |  |  |
| Scale Image | *File* | Path to the background scale image (*default: "modules/avionics/airspeed/background.png"*). |
| Arrow Image | *File* | Path to the arrow image (*default: "modules/avionics/airspeed/arrow.png"*). |
| Runtime Group |  |  |
| In Speed | *Float* | Input speed value in knots. |


### See Also


- **[AvionicsIndicatorsController](../../../api/modules/avionics/class.avionicsindicatorscontroller.md)**
