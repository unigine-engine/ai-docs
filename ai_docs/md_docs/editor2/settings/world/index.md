# World Settings


This section contains all world-related settings.


![World settings](world.png)

*World Settings*


| World Distance | Distance from the camera, from which all nodes are not rendered or simulated (infinite by default). The distance is measured from the camera to the node's bound. |
|---|---|
| World Budget | World generation time budget for the Grass and Clutter objects in frames per second. |
| Update Grid Size | Size of the grid to be used for spatial tree update, in units. The default value is an average one, and can be adjusted when necessary depending on the scene. |
| Game Scale | Scale factor to speed up or slow down the game time. That includes both rendering rate (for example, particles spawn rate and material offsets) and [physics ticks](../../../editor2/settings/physics_global/index.md#physics_scale). |
| Async Load Node References | Toggles asynchronous loading of *Node References* at loading the world. |
