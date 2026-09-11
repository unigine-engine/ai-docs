# MultirotorLinear

**Inherits from:** FlightModel<MultirotorLinearConfig>


MultirotorLinear implements a simplified linear flight model for multirotor drones. It provides basic flight physics with configurable speed, angle limits, and crash detection without complex aerodynamic simulation.


### Component Parameters


| MultirotorLinearConfig Group |  |  |  |
|---|---|---|---|
| Name | Type | Default | Description |
| Linear Rate | *Float* | 4 | Linear acceleration rate. |
| Angular Rate | *Float* | 5 | Angular acceleration rate. |
| Max Speed | *Float* | 10 | Maximum horizontal speed in m/s. |
| Max Ascent Speed | *Float* | 10 | Maximum ascent speed in m/s. |
| Max Descent Speed | *Float* | 6 | Maximum descent speed in m/s. |
| Max Angular Velocity | *Float* | 180 | Maximum yaw rate in deg/s. |
| Max Pitch Angle | *Float* | 40 | Maximum pitch angle in degrees. |
| Max Roll Angle | *Float* | 40 | Maximum roll angle in degrees. |
| Crash Group |  |  |  |
| Leg Shape Name | *String* | Leg | Name pattern for landing leg collision shapes. |
| Physical Mask | *Mask* | 1 | Physical intersection mask for landing detection. |
| Max Crash Impulse | *Float* | 2.0 | Maximum impulse before crash. |
| Hovering Height | *Float* | 1.2 | Target hovering height above ground. |


### See Also


- **[MultirotorLinearConfig](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.multirotorlinearconfig.md)**
- **[FlightModelBase](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.flightmodelbase.md)**
- **[MultirotorPhysical](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.multirotorphysical.md)**
- **[Drone](../../../../../api/templates/template_aviation_uav/drone/class.drone.md)**


## MultirotorLinear Class

---

## void init ( )

Initializes the flight model with the parent drone.
### Arguments

## void reset ( )

Resets the flight model to the specified transform.
### Arguments

## getType ( )

Returns TYPE_MULTIROTOR_LINEAR.
## getState ( )

Returns current flight state (GROUND, TAKEOFF, FLIGHT, LANDING, HOVERING, CRASHED).
## getRPMIntensity ( )

Returns the current RPM intensity for propeller animation.
## getPosition ( )

Returns current world position.
## getRotation ( )

Returns current rotation quaternion.
## getTransform ( )

Returns current transformation matrix.
## getLinearVelocity ( )

Returns current linear velocity.
## getAngularVelocity ( )

Returns current angular velocity.
