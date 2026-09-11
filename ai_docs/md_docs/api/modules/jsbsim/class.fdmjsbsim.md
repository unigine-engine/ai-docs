# JSBSim::FDMJSBSim Class


FDMJSBSim provides integration with the **JSBSim** Flight Dynamics Model library. **JSBSim** is an open-source, high-fidelity flight dynamics model used in many professional flight simulators.


This wrapper handles loading **JSBSim** aircraft models from configuration files, coordinating between Unigine's coordinate system and **JSBSim**'s geodetic coordinates, ground contact callbacks using Unigine's intersection system, wind integration with the **IG** meteorological system, and property access for reading and writing **JSBSim** internal values.


Usage pattern: create FDMJSBSim with the root directory containing aircraft/engine/systems folders, call **loadModel()** with the aircraft name, call **start()** with initial conditions, call **update()** every frame with delta time, read position/rotation using getter methods, and control the aircraft via **JSBSim** property nodes.


### See Also


- **[JSBSim::GroundCallback](../../../api/modules/jsbsim/class.groundcallback.md)**
- **[JSBSim::Crasher](../../../api/modules/jsbsim/class.crasher.md)**
- **[JSBSim::WidgetJSBSimProperties](../../../api/modules/jsbsim/class.widgetjsbsimproperties.md)**


## FDMJSBSim Class

---

## FDMJSBSim ( )

Constructs a JSBSim FDM instance with the specified root directory.
### Arguments

## loadModel ( )

Loads a JSBSim aircraft model.
### Arguments

### Return value

True if model loaded successfully.
## isModelLoaded ( )

Returns whether an aircraft model is currently loaded.
### Return value

True if a model is loaded.
## isCrashed ( )

Returns whether the aircraft is in a crashed state.
### Return value

True if the aircraft has crashed.
## void freeze ( )

Freezes or unfreezes the simulation.
### Arguments

## isFreeze ( )

Returns whether the simulation is frozen.
### Return value

True if frozen.
## void start ( )

Starts the simulation with the specified initial conditions.
### Arguments

## void update ( )

Advances the simulation by the specified time step.
### Arguments

## getGeoPosition ( )

Returns the current geodetic position of the aircraft.
### Return value

Geodetic position (latitude, longitude, altitude).
## getRotationEulerNEDDeg ( )

Returns the aircraft orientation as Euler angles in NED frame.
### Return value

Euler angles in NED frame (degrees).
## getBodyLinearVelocity ( )

Returns the linear velocity in body-frame coordinates.
### Return value

Body-frame linear velocity.
## getBodyAngularVelocity ( )

Returns the angular velocity in body-frame coordinates.
### Return value

Body-frame angular velocity.
## getAirSpeed ( )

Returns the current airspeed.
### Return value

Airspeed value.
## void setWind ( )

Sets the wind velocity affecting the aircraft.
### Arguments

## void setNodeValue ( )

Sets a JSBSim property value by path.
### Arguments

## getNodeValue ( )

Gets a JSBSim property value by path.
### Arguments

### Return value

Property value.
## hasNode ( )

Checks if a JSBSim property exists.
### Arguments

### Return value

True if the property exists.
## getWheelPositions ( )

Returns the geodetic positions of all landing gear contact points.
### Return value

Vector of wheel geodetic positions.
## getProperties ( )

Returns a list of all available JSBSim property names.
### Return value

Vector of property names.
