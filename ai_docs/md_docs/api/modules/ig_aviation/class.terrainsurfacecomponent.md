# TerrainSurfaceComponent Component

**Inherits from:** ComponentBase


TerrainSurfaceComponent defines the mapping between landscape terrain masks and surface types. This allows systems like **[RotorWashController](../../../api/modules/ig_aviation/class.rotorwashcontroller.md)** and **[WheelTraceController](../../../api/modules/ig_aviation/class.wheeltracecontroller.md)** to determine what type of surface is at a given location.


Surface types include: UNKNOWN, GROUND, ASPHALT, GRASS, ICE, SNOW, WATER, MUD, and user-defined types (USER_1, USER_2, USER_3).


To configure surface detection, add this component to a node in your scene, configure the Types array to map each surface type to the corresponding landscape mask. The **[TerrainInfo](../../../api/modules/ig_aviation/class.terraininfo.md)** singleton will use this configuration for surface queries.


This component should initialize early (order -100) to be available for other components that depend on surface information.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Settings Group |  |  |
| Types | *Array* | Mapping of surface types to landscape masks. |


### See Also


- **[ObjectSurfaceComponent](../../../api/modules/ig_aviation/class.objectsurfacecomponent.md)**
- **[TerrainInfo](../../../api/modules/ig_aviation/class.terraininfo.md)**
