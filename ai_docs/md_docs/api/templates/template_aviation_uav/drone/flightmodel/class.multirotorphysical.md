# MultirotorPhysical

**Inherits from:** FlightModel<MultirotorPhysicalConfig>


MultirotorPhysical implements a physics-based multirotor (quadcopter) flight model. It uses rigid body physics with configurable control rates, damping, and flight assists (altitude hold, position hold). The model simulates realistic multirotor behavior including weather effects and crash detection.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Mass | *Float* | 0.5 | Drone mass in kg. |
| Weather Affect | *Float* | 0.2 | Wind influence factor. |
| Max Crash Impulse | *Float* | 2.0 | Collision impulse threshold for crash. |


### Configuration Parameters (MultirotorPhysicalConfig)


| Name | Type | Default | Description |
|---|---|---|---|
| Hold Altitude | *Toggle* | true | Enable altitude hold. |
| Hold Position | *Toggle* | false | Enable position hold. |
| Limit Angles | *Toggle* | true | Limit pitch and roll angles. |
| Yaw Rate | *Float* | 10.0 | Maximum yaw rotation rate. |
| Pitch Rate | *Float* | 5.0 | Maximum pitch rotation rate. |
| Roll Rate | *Float* | 5.0 | Maximum roll rotation rate. |
| Max Throttle | *Float* | 40.0 | Maximum throttle force. |
| Max Pitch | *Float* | 25.0 | Maximum pitch angle in degrees. |
| Max Roll | *Float* | 25.0 | Maximum roll angle in degrees. |
| Linear Damping | *Float* | 0.6 | Linear velocity damping. |
| Angular Damping | *Float* | 10.0 | Angular velocity damping. |
| Max Linear Velocity | *Float* | 50.0 | Maximum linear velocity. |
| Max Angular Velocity | *Float* | 1.5 | Maximum angular velocity. |


### See Also


- **[MultirotorPhysicalConfig](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.multirotorphysicalconfig.md)**
- **[FlightModelBase](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.flightmodelbase.md)**
- **[MultirotorLinear](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.multirotorlinear.md)**
- **[Drone](../../../../../api/templates/template_aviation_uav/drone/class.drone.md)**


## MultirotorPhysical Class

---

## void init ( )

Initializes the flight model with the parent drone.
### Arguments

## void reset ( )

Resets the flight model to the specified transform.
### Arguments

## getType ( )

Returns TYPE_MULTIROTOR_PHYSICAL.
## getState ( )

Returns current flight state.
## getRPMIntensity ( )

Returns the current RPM intensity for propeller animation.
## void setActiveConfig ( )

Sets the active configuration by index.
### Arguments
