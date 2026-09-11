# FixedWing

**Inherits from:** FlightModel<FixedWingConfig, FixedWingInput>


FixedWing implements a physics-based fixed-wing aircraft flight model. It simulates aerodynamic forces including lift, drag, and control surface effects. The model supports flaps, angle-of-attack calculations, stall behavior, and various steering curves.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Rudder Node | *Node* | � | Node for rudder visualization. |
| Mass | *Float* | 0.5 | Aircraft mass in kg. |
| Weather Affect | *Float* | 0.2 | Wind influence factor. |
| Max Crash Impulse | *Float* | 8.0 | Collision impulse threshold for crash. |


### Configuration Parameters (FixedWingConfig)


| Name | Type | Default | Description |
|---|---|---|---|
| Max Thrust | *Float* | 150.0 | Maximum engine thrust. |
| Thrust Rate | *Float* | 2.0 | Throttle response rate. |
| Stall Angle | *Float* | 15.0 | Angle of attack for stall. |
| Lift Group |  |  |  |
| Lift AOA Curve | *Curve2d* | � | Lift coefficient vs angle of attack curve. |
| Induced Drag Curve | *Curve2d* | � | Induced drag coefficient curve. |
| Lift S | *Float* | 8.0 | Wing reference area. |
| Common S | *Float* | 0.61 | Common reference area. |
| Induced Drag | *Float* | 0.3 | Induced drag coefficient. |
| Ambient Throttle Air K | *Float* | 0.3 | Ambient throttle coefficient in air. |
| Ambient Throttle Ground K | *Float* | 0.1 | Ambient throttle coefficient on ground. |
| Rudder Group |  |  |  |
| Rudder AOA Curve | *Curve2d* | � | Rudder effectiveness curve. |
| Rudder Induced Drag Curve | *Curve2d* | � | Rudder induced drag curve. |
| Rudder S | *Float* | 0 | Rudder reference area. |
| Rudder Power | *Float* | 2.0 | Rudder control authority. |
| Rudder AOA Bias | *Float* | 1.0 | Rudder angle of attack bias. |
| Flaps Group |  |  |  |
| Flaps Lift Power | *Float* | 3.0 | Additional lift from flaps. |
| Flaps AOA Bias | *Float* | 0.35 | Flaps angle of attack bias. |
| Flaps Drag | *Float* | 0.3 | Additional drag from flaps. |
| Flaps Retract Speed | *Float* | 29.0 | Speed for automatic flap retraction. |
| Steering Group |  |  |  |
| Steering Curve | *Curve2d* | � | Steering response curve. |
| Angle Curve | *Curve2d* | � | Angle response curve. |
| Turn Speed | *Vec3* | � | Maximum turn rates for each axis. |
| Turn Acceleration | *Vec3* | � | Turn acceleration rates. |
| Max Roll | *Float* | 20.0 | Maximum roll angle. |
| Max Pitch | *Float* | 20.0 | Maximum pitch angle. |
| Drag Group |  |  |  |
| Front Drag AOA Curve | *Curve2d* | � | Front drag vs angle of attack curve. |
| Right Drag | *Float* | 1.0 | Right-side drag coefficient. |
| Top Drag | *Float* | 1.0 | Top drag coefficient. |
| Angular Drag | *Vec3* | � | Angular drag coefficients. |
| Physics Group |  |  |  |
| Linear Damping | *Float* | 1.0 | Linear velocity damping. |
| Angular Damping | *Float* | 1.0 | Angular velocity damping. |
| Max Linear Velocity | *Float* | 80.0 | Maximum linear velocity. |
| Max Angular Velocity | *Float* | 20.0 | Maximum angular velocity. |


### See Also


- **[FixedWingConfig](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.fixedwingconfig.md)**
- **[FixedWingInput](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.fixedwinginput.md)**
- **[FlightModelBase](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.flightmodelbase.md)**
- **[ControlSurface](../../../../../api/templates/template_aviation_uav/drone/components/class.controlsurface.md)**
- **[Drone](../../../../../api/templates/template_aviation_uav/drone/class.drone.md)**


## FixedWing Class

---

## void init ( )

Initializes the flight model with the parent drone.
### Arguments

## void reset ( )

Resets the flight model to the specified transform.
### Arguments

## getType ( )

Returns TYPE_FIXED_WING.
## getState ( )

Returns current flight state (GROUND, FLIGHT, CRASHED).
## getRPMIntensity ( )

Returns the current RPM intensity for propeller animation.
## void setActiveConfig ( )

Sets the active configuration by index.
### Arguments
