# EntitySplineMovement Component

**Inherits from:** ComponentBase


EntitySplineMovement provides automated movement of **IG** entities along a closed spline path, with optional water surface interaction. This is particularly useful for simulating ships, boats, or other watercraft that need to follow predefined routes while responding to wave motion.


The component works by building a cubic Hermite spline from child nodes of the component's node, moving an **IG** entity along this spline at a configurable speed, and optionally adjusting the entity's height and rotation to match wave surfaces.


The spline is automatically closed (looped), so the entity continuously travels around the path. The component uses geodetic coordinates for **IG** compatibility, making it suitable for large-scale geographic simulations.


To set up entity movement, create a parent node with EntitySplineMovement component, add child nodes as waypoints (their positions define the spline path), configure the entity type and ID to match your **IG** entity database, and adjust speed and inertia for smooth movement.


For water vessels, the component automatically finds ObjectWaterGlobal in the scene and uses it to sample wave heights at three points around the entity, creating realistic pitch and roll as the vessel rides the waves.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Entity Group |  |  |  |
| Entity Type | *Int* |  | IG entity type identifier. |
| Entity Id | *Int* |  | IG entity instance identifier. |
| Movement Group |  |  |  |
| Speed | *Float* | 30.0 | Movement speed along the spline. |
| Inertion | *Float* | 2.0 | Inertia factor for smooth rotation and height changes on water. Higher values mean faster response. |
| Z Offset | *Float* | 0.0 | Vertical offset from the water surface. |
| Radius Factor | *Float* | 0.5 | Multiplier for the entity's bounding sphere radius, used for wave sampling. |


### See Also


- **[SplinePath](../../../api/modules/entity_spline_movement/class.splinepath.md)**
