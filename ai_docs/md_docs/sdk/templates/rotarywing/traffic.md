# Rotary-Wing Template - Background Traffic Simulation


This framework simulates **background vehicle movement along roads**, providing a **lightweight approximation of traffic** intended for scenarios where detailed simulation is not required - for example, when viewed from a cockpit at altitude.


![](../modules/traffic/img/intro.jpg)


Traffic simulation is implemented using a ***[WorldSplineGraph](../../../objects/worlds/world_spline_graph/index.md)*** node. This graph lets you visually arrange points (graph vertices), connected with curved edges to form the road network to be used by vehicles.


**Key Features:**


- **Low performance cost**. The traffic approximation minimizes CPU workload, allowing resources to be prioritized for critical gameplay or simulation logic.
- **Synchronization support**. The traffic system works with the *[Syncker](../../../code/plugins/syncker/index.md)* plugin, enabling simulation across multiple machines or across several application instances running on a single machine.


## Framework Structure


The node structure of the framework is organized as follows:


![](../modules/traffic/img/clusters.png)


The `car_traffic` *NodeDummy* is the top-level parent node, containing the following hierarchy:


- `WorldSplineGraph` node with the `TrafficGraphController` component property attached. This is the core framework component that handles traffic graph generation and provides access to the main configuration parameters.
- Vehicle ***[Mesh Cluster](../../../objects/objects/mesh_cluster/index.md)*** nodes under *[WorldSplineGraph](#worldsplinegraph)*, representing different vehicle types. Each cluster has the `TrafficVehicleType` component property assigned, to control vehicle type settings per cluster.


## Graph Generation


The traffic system transforms the native *WorldSplineGraph* `.spl` file data into a more lightweight adjacency-based structure, stored in a `.json` file. This conversion is performed by the `TrafficGraphController` component, which then produces the final traffic graph based on this data.


You can *[change the file location](#graph_gen_on_init)* or *[use an existing `.json` file](#graph_reuse)* when *[configuring traffic simulation for your project](../../../sdk/templates/rotarywing/custom.md#custom_traffic)*.


### Graph Segmentation


During graph generation, each edge is internally subdivided into smaller segments using the configurable *[Segment Split Distance](#graph_gen_on_init)* parameter of the `TrafficGraphController` component. These segments form traffic graph vertices (points) that approximate the curvature of the original spline. Edges are split into segments regardless of whether they are curved or straight.


## Traffic Control


### Vehicle Configuration


Vehicles in the template move along the spline-based trajectory in the following manner:


- A vehicle travels from vertex to vertex of the *[generated graph](#create_graph)*, not exactly following an exact spline path.
- When a vehicle approaches a target within a *[defined threshold](#reach_target_distance)*, it starts turning toward the next vertex in line.
- Movement is continuous and approximate, rather than realistically accurate.


This approach keeps computation lightweight while producing visually convincing results at a distance.


Vehicle visuals (mesh and material) configured per vehicle type through the parameters of the *[Mesh Cluster](#vehicle_clusters)* nodes.


![](../modules/traffic/img/vehicle_mesh_cluster.png)


### Framework Logic


The framework logic is implemented via the following components:


#### TrafficVehicleType component


The *TrafficVehicleType* component property is assigned to vehicle *Mesh Cluster* nodes. This component:


- Provides access to the vehicle speed setting. ![](../modules/traffic/img/trafficvehicletype.png)
- During the *update()* stage, sets the current transforms of vehicles as calculated by *[TrafficGraphController](#trafficgraphcontroller_component)*.


#### TrafficGraphController component


*TrafficGraphController* is the main framework component. It exposes the following groups of traffic system configuration parameters:


- **Traffic Settings** ![](../modules/traffic/img/trafficgraphcontroller_component.png) | **Visibility Distance** | The maximum distance at which vehicles are visible. | |---|---| | **Spawn Distance Min** | Vehicles are spawned at graph vertices around the player limited by this distance. | | **Traffic Density** | Defines traffic density as the number of vehicles per visible graph vertex. | | **Max Vehicle Count** | Upper limit on the total number of vehicles. | | **Vehicle Reach Target Distance** | Distance at which a vehicle considers a target vertex reached and begins steering toward the next one. This controls how early the vehicle starts turning. | | **Check Collision Distance** | Distance at which a vehicle stops if another vehicle ahead is moving toward the same target vertex. | | **Max Speed (km/h)** | Maximum possible velocity of a vehicle. | | **Start Timer Delay** | Ensures traffic starts simultaneously across all synchronized instances, accounting for cases where a *Slave* instance loads significantly later than the *Master* (only for IG-based templates). | | **Normalized Dot Threshold for Same Direction** | When checking for a vehicle ahead, the system verifies that both vehicles are moving in the same direction using the dot product of their movement vectors. The value must be within [-1, 1]. Higher values indicate a smaller angle between vectors and better directional alignment. | | **Road Center Offset** | Controls lateral vehicle placement relative to the traffic graph. Vehicles are spawned with a sideways offset from the graph vertex, allowing them to occupy separate lanes instead of driving directly toward each other. |
- **Graph Settings** Since a *WorldSplineGraph*-generated `.spl` file contains significantly more information than is necessary for the framework operation, the `TrafficGraphController` component transforms it into a simplified adjacency matrix stored in a `.json` file. **To generate a new graph:** ![](../modules/traffic/img/graph_settings_json_generation.png) *Generating the JSON file to be used for graph creation* **To reuse an existing graph:** ![](../modules/traffic/img/graph_settings_json_use.png) *Using the available JSON file*

  1. Enable *Generate Graph On Init*.
  2. Specify the output location in the *Generation Output Path* field.
  3. Configure the *Segment Split Distance* parameter, which determines the length of the *[generated graph segments](#graph_segmentation)*.

  1. Disable *Generate Graph On Init*.
  2. Select the desired `.json` file in the *Graph JSON File To Use* field.
  3. Configure the *Segment Split Distance* parameter, which determines the length of the *[generated graph segments](#graph_segmentation)*.
- **Spawn Types** ![](../modules/traffic/img/spawn_settings.png) *Three vehicle types with equal weights will have the same spawn probability of33%* | **Spawn Types** | Total number of vehicle types. | |---|---| | **Traffic Vehicle Type** | Reference to a vehicle type *Mesh Cluster* node. | | **Spawn Chance** | Raw spawn chance for each vehicle type. Values are normalized across all vehicle types to determine the final spawn probability. |
- **Features** When the **Debug** parameter is enabled, the actual traffic graph and the target vertices currently assigned to vehicles are rendered by the Engine visualizer. ![](../modules/traffic/img/debug.png)


## Limitations


1. The system works best when the **frame rate is stable** on both *Master* and *Slave* instances. If the *Slave* experiences frame drops, traffic may temporarily desynchronize, but should gradually re-sync over time.
2. Vehicles do **not follow graph edges precisely**. They move directly between the points generated by the *[segmentation process](#graph_segmentation)*, without taking into account the turn curvature. Proper behavior requires careful tuning using: For example, a crossroads (two roads crossing perpendicularly) can be implemented in either of the following ways: | ![](../modules/traffic/img/point_crossroads.jpg) | **Simply placing points in the Editor** - quicker to implement, but requires additional parameter tuning to ensure vehicles navigate turns correctly. This approach is applied uniformly to all turns, which may be beneficial if turn geometry is relatively consistent, but less suitable when turn types vary significantly. | |---|---| | ![](../modules/traffic/img/spline_crossroads.jpg) | **Using spline curves for each lane** - offers greater control over vehicle movement. This method requires finer graph segmentation so that vehicle motion more accurately follows the curvature of the graph. |

  - *[Vehicle speed](#trafficvehicletype_component)*
  - Graph *[segmentation length](#graph_gen_on_init)*
  - Placement of *[*WorldSplineGraph* control points](../../../objects/worlds/world_spline_graph/index.md#point_add)*
  - Turn angle logic (the `max_acceleration_angle` parameter in `TrafficComponent.h`, 5 by default).
3. If vehicle speed is too high, graph segmentation too coarse, and *[Vehicle Reach Target Distance](#reach_target_distance)* (*TrafficGraphController* component setting) too large, vehicles may overshoot sharp turns and begin circling around a single vertex. This can be resolved by:

  - Increasing graph segmentation density
  - Reducing vehicle speed
  - Increasing turn angle limits (the `max_acceleration_angle` parameter in `TrafficComponent.h`, 5 by default).
