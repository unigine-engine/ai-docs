# ObjectSurfaceComponent Component

**Inherits from:** ComponentBase


ObjectSurfaceComponent allows specifying the surface type for individual mesh objects. While **[TerrainSurfaceComponent](../../../api/modules/ig_aviation/class.terrainsurfacecomponent.md)** handles landscape terrain, this component is used for standalone objects like runways, roads, or water surfaces.


When the **[TerrainInfo](../../../api/modules/ig_aviation/class.terraininfo.md)** system queries a location, it checks both landscape masks (via **[TerrainSurfaceComponent](../../../api/modules/ig_aviation/class.terrainsurfacecomponent.md)**) and object intersections (via ObjectSurfaceComponent) to determine the surface type.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Settings Group |  |  |
| Type | *Switch* | The surface type: UNKNOWN, GROUND, ASPHALT, GRASS, ICE, SNOW, WATER, MUD, USER_1, USER_2, or USER_3. |


### See Also


- **[TerrainSurfaceComponent](../../../api/modules/ig_aviation/class.terrainsurfacecomponent.md)**
- **[TerrainInfo](../../../api/modules/ig_aviation/class.terraininfo.md)**
