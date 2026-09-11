# FlightModelBase

**Inherits from:** ComponentBase


FlightModelBase is an abstract interface for drone flight models. It provides methods to initialize, reset, check state, and retrieve telemetry data (position, rotation, velocity, acceleration).


### See Also


- **[FlightModel](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.flightmodel.md)**
- **[FlightModelConfigBase](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.flightmodelconfigbase.md)**
- **[FlightModelBasicInput](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.flightmodelbasicinput.md)**
- **[MultirotorPhysical](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.multirotorphysical.md)**
- **[MultirotorLinear](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.multirotorlinear.md)**
- **[FixedWing](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.fixedwing.md)**
- **[Drone](../../../../../api/templates/template_aviation_uav/drone/class.drone.md)**


## FlightModelBase Class

---

## virtual void init ( )

Initializes the flight model with its parent drone.
### Arguments

## virtual void reset ( )

Resets the flight model to the specified transform.
### Arguments

## virtual getType ( )

Returns the flight model type (TYPE_MULTIROTOR_PHYSICAL, TYPE_MULTIROTOR_LINEAR, or TYPE_FIXED_WING).
### Return value

Flight model type.
## virtual isArmed ( )

Returns whether the flight model is armed (motors active).
### Return value

True if armed.
## virtual getState ( )

Returns the current flight state.
### Return value

Current state (GROUND, FLIGHT, or CRASHED).
## virtual getPosition ( )

Returns the drone's world position.
### Return value

World position.
## virtual getRotation ( )

Returns the drone's world rotation.
### Return value

World rotation.
## virtual getTransform ( )

Returns the drone's world transform.
### Return value

World transform.
## virtual getLinearVelocity ( )

Returns the drone's linear velocity.
### Return value

Linear velocity vector.
## virtual getAngularVelocity ( )

Returns the drone's angular velocity.
### Return value

Angular velocity vector.
## virtual void setActiveConfig ( ) =0

Sets the active flight configuration.
### Arguments

## virtual getActiveConfigIdx ( ) =0

Returns the index of the active configuration.
### Return value

Active config index.
## virtual getNumConfigs ( ) =0

Returns the number of available configurations.
### Return value

Number of configurations.
## virtual getRPMIntensity ( ) =0

Returns the current RPM intensity for propeller animation.
### Return value

RPM intensity 0-1.
## virtual getConfigName ( ) =0

Returns the name of the configuration at the specified index.
### Arguments

### Return value

Configuration name.
## virtual getDefaultConfigIdx ( ) =0

Returns the index of the default configuration.
### Return value

Default config index.
## virtual isMain ( )

Returns whether this is the main flight model (used for VTOL with multiple submodels).
### Return value

True if this is the main flight model.
## virtual getTransformUpdateMode ( )

Returns whether the flight model manages the drone's transform (MANAGED) or if manual updates are required (MANUAL).
### Return value

Transform update mode.
## virtual getEulerAngles ( )

Returns the drone's euler angles (decomposed from rotation).
### Return value

Euler angles in radians.
## virtual getLinearAcceleration ( )

Returns the drone's linear acceleration.
### Return value

Linear acceleration vector.
## virtual getAngularAcceleration ( )

Returns the drone's angular acceleration.
### Return value

Angular acceleration vector.
## static getTypeName ( )

Returns the human-readable name for a flight model type.
### Arguments

### Return value

Type name string.
## static getStateName ( )

Returns the human-readable name for a flight state.
### Arguments

### Return value

State name string.
