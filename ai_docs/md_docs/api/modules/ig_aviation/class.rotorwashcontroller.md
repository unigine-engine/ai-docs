# RotorWashController Component

**Inherits from:** ComponentBase


RotorWashController manages multiple **[RotorWash](../../../api/modules/ig_aviation/class.rotorwash.md)** effects, automatically switching between them based on the underlying surface type. This allows different particle effects for different terrain - dust over dry ground, water spray over water, snow over snow-covered areas, etc.


The controller periodically samples the terrain to detect surface type changes and activates the appropriate RotorWash effect. Surface detection uses the **[TerrainInfo](../../../api/modules/ig_aviation/class.terraininfo.md)** system and considers both landscape masks and object surface components.


To set up surface-dependent rotor wash, create separate NodeReference files containing RotorWash effects for each surface type, configure the Types array to map surface types to effect files, and set up **[TerrainSurfaceComponent](../../../api/modules/ig_aviation/class.terrainsurfacecomponent.md)** to define surface types on the landscape.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Settings Group |  |  |
| Intensity | *Float* | Overall effect intensity 0-1 (*default: 1.0*). |
| Rpm Intensity | *Float* | Intensity based on rotor RPM 0-1 (*default: 1.0*). |
| Xy Distance Check | *Float* | Distance for surface type checks (*default: 1.0*). |
| Types | *Array* | Mapping of surface types to RotorWash node references. |


### See Also


- **[RotorWash](../../../api/modules/ig_aviation/class.rotorwash.md)**
- **[TerrainSurfaceComponent](../../../api/modules/ig_aviation/class.terrainsurfacecomponent.md)**
- **[TerrainInfo](../../../api/modules/ig_aviation/class.terraininfo.md)**


## RotorWashController Class

---

## getCurrentWash ( )

Returns the currently active rotor wash effect based on surface type.
### Return value

The currently active RotorWash component.
