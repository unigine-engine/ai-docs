# Altimeter Component

**Inherits from:** ComponentBase


Altimeter is a critical flight instrument that displays the aircraft's altitude. This component renders a classic two-pointer analog altimeter to a texture for display on 3D surfaces in cockpits and instrument panels.


The instrument uses two arrows like a traditional altimeter: the fat arrow indicates thousands of feet (one full rotation = 1000 ft), and the thin arrow indicates hundreds of feet (one full rotation = 100 ft). This dual-arrow design allows pilots to quickly read altitude at a glance, a proven interface used in aviation for decades.


To use this component, attach it to a mesh object with a surface that has an albedo texture slot, configure the render settings, and feed the In Altitude parameter with your aircraft's current altitude.


For managing multiple analog indicators together, consider using **[AvionicsIndicatorsController](../../../api/modules/avionics/class.avionicsindicatorscontroller.md)**.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Render Settings Group |  |  |
| Size | *IVec2* | Render target size in pixels (*default: (400, 400)*). |
| Surface Name | *String* | Name of the surface to render to (*default: "plane"*). |
| Texture Name | *String* | Name of the texture slot (*default: "albedo"*). |
| Settings Group |  |  |
| Scale Image | *File* | Path to the background scale image (*default: "modules/avionics/altimeter/background.png"*). |
| Arrow Fat Image | *File* | Path to the fat arrow image (*default: "modules/avionics/altimeter/arrow_fat.png"*). |
| Arrow Thin Image | *File* | Path to the thin arrow image (*default: "modules/avionics/altimeter/arrow_thin.png"*). |
| Runtime Group |  |  |
| In Altitude | *Float* | Input altitude value (*default: 0.0*). |


### See Also


- **[AvionicsIndicatorsController](../../../api/modules/avionics/class.avionicsindicatorscontroller.md)**
