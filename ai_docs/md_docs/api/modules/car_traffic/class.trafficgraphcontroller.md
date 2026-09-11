# TrafficGraphController Component

**Inherits from:** ComponentBase


TrafficGraphController manages an AI-driven traffic simulation system where vehicles move along a road network defined by a WorldSplineGraph. It handles vehicle spawning, movement, collision avoidance, and synchronization in multi-display (**Syncker**) setups.


The system uses a road network defined by a WorldSplineGraph node (the component must be attached to this node), converts spline segments into a navigation graph (**JSON** format) with waypoints and connections, dynamically spawns vehicles within visibility distance of the player and despawns when too far, implements collision avoidance where vehicles slow down when approaching others in the same direction, and supports **Syncker** for synchronized traffic across multiple render nodes.


To set up traffic simulation, create a WorldSplineGraph defining your road network, attach this component to the spline graph node, create vehicle types using **[TrafficVehicleType](../../../api/modules/car_traffic/class.trafficvehicletype.md)** components on ObjectMeshCluster nodes, add vehicle types to the Spawn Types array with desired spawn probabilities, and either provide a pre-generated graph JSON file or enable Generate Graph On Init.


The traffic controller uses multithreaded updates via CPUShader for performance, and integrates with **Syncker** for master/slave synchronization in multi-channel setups.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Traffic Settings Group |  |  |
| Visibility Distance | *Double* | Maximum distance at which vehicles are visible and active (*default: 5000.0*). |
| Spawn Distance Min | *Double* | Minimum distance from player for spawning new vehicles (*default: 1000.0*). |
| Traffic Density | *Float* | Controls how many vehicles spawn relative to available spawn points (*default: 0.2*). |
| Max Vehicle Count | *Int* | Maximum number of simultaneous vehicles (*default: 200*). |
| Vehicle Reach Target Distance | *Double* | Distance threshold for considering a waypoint reached (*default: 5.0*). |
| Check Collision Distance | *Double* | Distance at which vehicles check for collisions ahead (*default: 5.0*). |
| Max Speed Kmph | *Float* | Maximum vehicle speed in km/h (*default: 80.0*). |
| Start Timer Delay | *Float* | Delay before traffic starts for Syncker sync (*default: 3.0*). |
| Normalized Dot Threshold For Same Direction | *Float* | Threshold for detecting same-direction vehicles (*default: 0.95*). |
| Road Center Offset | *Float* | Offset from the road center line for vehicle positioning (*default: 2*). |
| Graph Settings Group |  |  |
| Generate Graph On Init | *Toggle* | Generate navigation graph from spline on initialization (*default: false*). |
| Output File Path | *String* | Path for generated graph JSON file (*default: "/init_graph_test.json"*). |
| Traffic Graph File | *File* | Pre-generated graph JSON file to load. |
| Segment Split Length | *Float* | Distance between waypoints when splitting spline segments (*default: 5.0*). |
| Spawn Types Group |  |  |
| Traffic Vehicle Type | *Node* | Reference to a TrafficVehicleType component node. |
| Spawn Chance | *Float* | Relative probability of spawning this type (*default: 0.5*). |
| Features Group |  |  |
| Debug | *Toggle* | Enable debug visualization of graph and vehicles (*default: false*). |


### See Also


- **[TrafficVehicleType](../../../api/modules/car_traffic/class.trafficvehicletype.md)**


## TrafficGraphController Class

---

## void load_graph_json ( )

Loads a navigation graph from a JSON file. The graph defines waypoints and their connections for vehicle movement.
### Arguments

## void setDebug ( bool value )

Enables or disables debug visualization showing the navigation graph and vehicle positions.
### Arguments

- *bool* **value** - Enable or disable debug mode.

## void addSpawner ( float chance )

Registers a vehicle type with the controller. Usually called automatically based on the Spawn Types array, but can be used for dynamic registration.
### Arguments

- *float* **chance** - Spawn probability for this vehicle type.
