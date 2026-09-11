# TerrainInfo Class


TerrainInfo is a singleton class that provides surface type queries at specific world positions. It combines information from landscape terrain masks (via **[TerrainSurfaceComponent](../../../api/modules/ig_aviation/class.terrainsurfacecomponent.md)**) and object surface components (via **[ObjectSurfaceComponent](../../../api/modules/ig_aviation/class.objectsurfacecomponent.md)**) to determine the surface type.


The class performs intersection tests and landscape mask fetches to determine what type of surface exists at a given position. This information is used by systems like **[RotorWashController](../../../api/modules/ig_aviation/class.rotorwashcontroller.md)** and **[WheelTraceController](../../../api/modules/ig_aviation/class.wheeltracecontroller.md)** to select appropriate visual effects.


Query results include the surface type (GROUND, ASPHALT, GRASS, etc.), intersection point position, surface normal, and intersected object.


### See Also


- **[TerrainSurfaceComponent](../../../api/modules/ig_aviation/class.terrainsurfacecomponent.md)**
- **[ObjectSurfaceComponent](../../../api/modules/ig_aviation/class.objectsurfacecomponent.md)**


## TerrainInfo Class

---

## static get ( )

Returns the singleton instance of TerrainInfo.
### Return value

The singleton instance.
## fetch ( )

Queries the surface type at the specified world position.
### Arguments

### Return value

The surface type at the specified position.
## getIntersectionMask ( )

Returns the intersection mask used for surface queries.
### Return value

The intersection mask.
