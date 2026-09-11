# Variometer Component

**Inherits from:** ComponentBase


Variometer (vertical speed indicator, **VSI**) shows the aircraft's rate of climb or descent. This component renders an analog variometer to a texture for display on cockpit instrument panels.


The instrument displays vertical speed with a non-linear scale typical of real variometers. Scale ranges from -20 to +20 (units depend on your flight model, typically 100s of feet per minute), the arrow points up for climb, down for descent, and horizontal for level flight. Non-linear scaling provides finer resolution at lower climb/descent rates where precision matters most.


To use this component, attach it to a mesh object with a surface that has an albedo texture slot, configure the render settings and provide scale/arrow images, and feed the In Speed parameter with your aircraft's vertical speed.


For managing multiple analog indicators together, consider using **[AvionicsIndicatorsController](../../../api/modules/avionics/class.avionicsindicatorscontroller.md)**.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Render Settings Group |  |  |
| Size | *IVec2* | Render target size in pixels (*default: (400, 400)*). |
| Surface Name | *String* | Name of the surface to render to (*default: "plane"*). |
| Texture Name | *String* | Name of the texture slot (*default: "albedo"*). |
| Settings Group |  |  |
| Scale Image | *File* | Path to the background scale image (*default: "modules/avionics/variometer/background.png"*). |
| Arrow Image | *File* | Path to the arrow image (*default: "modules/avionics/variometer/arrow.png"*). |
| Runtime Group |  |  |
| In Speed | *Float* | Input vertical speed value. |


### See Also


- **[AvionicsIndicatorsController](../../../api/modules/avionics/class.avionicsindicatorscontroller.md)**
