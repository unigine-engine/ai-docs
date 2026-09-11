# Compass Component

**Inherits from:** ComponentBase


Compass (heading indicator) displays the aircraft's current magnetic heading. This component renders a classic rotating-disc compass to a texture for display on cockpit instrument panels.


The instrument consists of a rotating disc (compass card with degree markings that rotates based on heading) and a fixed lubber line (stationary reference mark at the top indicating the current heading). Unlike a magnetic compass, this is a gyroscopic heading indicator that shows heading without oscillation or turning errors, making it easier to read during flight maneuvers.


To use this component, attach it to a mesh object with a surface that has an albedo texture slot, configure the render settings and provide disc/background images, and feed the In Yaw parameter with your aircraft's current heading in degrees.


For managing multiple analog indicators together, consider using **[AvionicsIndicatorsController](../../../api/modules/avionics/class.avionicsindicatorscontroller.md)**.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Render Settings Group |  |  |
| Size | *IVec2* | Render target size in pixels (*default: (400, 400)*). |
| Surface Name | *String* | Name of the surface to render to (*default: "plane"*). |
| Texture Name | *String* | Name of the texture slot (*default: "albedo"*). |
| Settings Group |  |  |
| Background Image | *File* | Path to the background image (*default: "modules/avionics/background.png"*). |
| Disc Image | *File* | Path to the rotating disc image (*default: "modules/avionics/compass/disc.png"*). |
| Fixed Image | *File* | Path to the fixed overlay image (*default: "modules/avionics/compass/fixed.png"*). |
| Runtime Group |  |  |
| In Yaw | *Float* | Input yaw angle in degrees. |


### See Also


- **[AvionicsIndicatorsController](../../../api/modules/avionics/class.avionicsindicatorscontroller.md)**
