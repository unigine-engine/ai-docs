# Drone Component

**Inherits from:** ComponentBase


Drone is the main controller for UAV (Unmanned Aerial Vehicle) entities. It manages drone components, flight models, and lifecycle events. Each drone aggregates various subcomponents (battery, propellers, cameras, radio) and a flight model for physics simulation. The drone can be activated/deactivated and reset to spawn points.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Name | *String* | � | Display name of the drone. |


### Nested Classes


- **Drone::Component** - base class for all drone subcomponents (Battery, Camera, Propeller, Home, RadioModule, etc.). Components inheriting from this class are automatically registered with their parent Drone and receive a pointer to it via the *init(Drone *)* method.


### See Also


- **[Simulation](../../../../api/templates/template_aviation_uav/simulation/class.simulation.md)**
- **[FlightModelBase](../../../../api/templates/template_aviation_uav/drone/flightmodel/class.flightmodelbase.md)**
- **[Battery](../../../../api/templates/template_aviation_uav/drone/components/class.battery.md)**
- **[Propeller](../../../../api/templates/template_aviation_uav/drone/components/class.propeller.md)**


## Drone Class

---

## void reset ( )

Resets the drone to the specified transform and reinitializes all components.
### Arguments

## void setActive ( )

Activates or deactivates the drone.
### Arguments

## isActive ( )

Returns whether the drone is currently active.
### Return value

True if active.
## getComponent ( )

Returns the first drone component of the specified type.
### Return value

Component pointer or nullptr.
## void getComponents ( )

Returns all drone components of the specified type.
### Arguments

## getFlightModel ( )

Returns the drone's flight model.
### Return value

Flight model pointer.
## getEventActive ( )

Returns the event triggered when the drone's active state changes.
### Return value

Active state change event.
## getEventReset ( )

Returns the event triggered when the drone is reset.
### Return value

Reset event.
