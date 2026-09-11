# WheelTraceController Component

**Inherits from:** ComponentBase


WheelTraceController manages vehicle wheel tracks by detecting surface conditions and switching tire track textures accordingly. This allows realistic visualization of tire marks that adapt to different terrain types (asphalt, grass, mud, snow, etc.).


The component works with a tire track atlas texture, where different sections contain track patterns for different surface types. When the surface type changes, the component updates the texture coordinates to show the appropriate track pattern.


Surface detection can work in two modes: AUTO (automatically detects the surface type using raycasting) or MANUALY (uses the manually set Current Type parameter).


To set up wheel traces, prepare a texture atlas with tire track patterns for each surface type, add decal trails to your vehicle wheels, configure the Types array to map surface types to texture atlas indices, and set the detection mode and distance for surface checks.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Settings Group |  |  |
| Input Intensity | *Float* | Track visibility intensity (*default: 1.0*). |
| Detection Type | *Switch* | Surface detection mode: AUTO or MANUALY. |
| Current Type | *Int* | Manually set surface type index (when using MANUALY mode). |
| Distance Check | *Float* | Distance to check the surface type (*default: 2.0*). |
| Types | *Array* | Mapping of surface types to tire texture indices in the atlas. |


### See Also


- **[TerrainSurfaceComponent](../../../api/modules/ig_aviation/class.terrainsurfacecomponent.md)**
- **[TerrainInfo](../../../api/modules/ig_aviation/class.terraininfo.md)**
