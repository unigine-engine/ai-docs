# FlightLogic Component

**Inherits from:** ComponentBase


FlightLogic is the main flight simulation controller for rotary-wing aircraft (helicopters). It integrates the **JSBSim** flight dynamics model with Unigine's **IG** plugin to create a complete helicopter flight simulation.


The component handles flight dynamics simulation using **[FDMJSBSim](../../../api/modules/jsbsim/class.fdmjsbsim.md)**, helicopter control inputs (collective, cyclic, rudder), **AFCS** (Automatic Flight Control System) with SAS and altitude hold, crash detection and physics handoff via **[Crasher](../../../api/modules/jsbsim/class.crasher.md)**, camera management through **[CameraManager](../../../api/modules/cameras/class.cameramanager.md)**, rotor blade animation with flapping dynamics, sensor integration for **IR/NVG** modes, and avionics **HUD** updates.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Model | *String* | ah1s | **JSBSim** aircraft model name to load. |
| JSBSim Root Dir | *String* | modules/jsbsim | Path to the **JSBSim** root directory containing aircraft, engine, and systems folders. |
| Spawn Point | *Node* | � | Node defining the initial spawn position and orientation. |
| Engine Start Speed | *Float* | 0.2 | Rate of engine spool-up/down. |


### Default Controls


| Action | Keyboard | Joystick |
|---|---|---|
| Restart | *R* | - |
| Switch Camera | *N* | - |
| Start/Stop Engine | *T* | Button 9 |
| Enable/Disable SAS | *Y* | Button 11 |
| Enable/Disable Alt Hold | *U* | Button 13 |
| Landing Lights | *G* | Button 11 |
| Collective (Throttle) | *L.Shift / L.Ctrl* | Axis 2 |
| Cyclic Pitch (Elevator) | *W / S* | Axis 1 |
| Tail Rotor (Rudder) | *Q / E* | Axis 5 |
| Cyclic Roll (Aileron) | *A / D* | Axis 0 |
| View | *Mouse* | POV Hat |


### See Also


- **[AFCS](../../../api/templates/template_aviation_rotarywing/class.afcs.md)**
- **[FDMJSBSim](../../../api/modules/jsbsim/class.fdmjsbsim.md)**
- **[Crasher](../../../api/modules/jsbsim/class.crasher.md)**
- **[CameraManager](../../../api/modules/cameras/class.cameramanager.md)**


## FlightLogic Class

---

## void setSasEnabled ( )

Enables or disables the Stability Augmentation System (SAS) for pitch and roll stabilization.
### Arguments

## isSASEnabled ( )

Returns whether the Stability Augmentation System is currently enabled.
### Return value

true if SAS is active; otherwise, false.
## void setAltHoldEnabled ( )

Enables or disables the altitude hold autopilot function.
### Arguments

## isAltHoldEnabled ( )

Returns whether altitude hold is currently enabled.
### Return value

true if altitude hold is active; otherwise, false.
