# TrafficVehicleType Component

**Inherits from:** ComponentBase


TrafficVehicleType defines a type of vehicle that can be spawned in the traffic simulation. Each vehicle type is associated with an ObjectMeshCluster, allowing efficient rendering of many identical vehicles using GPU instancing.


The traffic system uses this component to define what mesh is used for this vehicle type (the component must be attached to an ObjectMeshCluster node), set the movement speed for all vehicles of this type, and manage the collection of active vehicles and update their transforms each frame.


To set up a vehicle type, create an ObjectMeshCluster with your vehicle mesh, attach this component to the cluster node, set the Vehicle Speed parameter, and reference this node in **[TrafficGraphController](../../../api/modules/car_traffic/class.trafficgraphcontroller.md)**'s spawn types array.


The component automatically updates the mesh cluster each frame with the transforms of all active vehicles of this type, enabling efficient batch rendering.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Settings Group |  |  |
| Vehicle Speed | *Float* | Movement speed for vehicles of this type (*default: 1.0*). |


### See Also


- **[TrafficGraphController](../../../api/modules/car_traffic/class.trafficgraphcontroller.md)**


## TrafficVehicleType Class

---

## void addVehicle ( )

Adds a vehicle instance to this type's collection. Called internally by TrafficGraphController when spawning vehicles.
### Arguments

## void removeVehicle ( )

Removes a vehicle instance from this type's collection. Called internally when vehicles are despawned.
### Arguments

## float getSpeed ( )

Returns the configured speed for vehicles of this type.
### Return value

The speed value for this vehicle type.
