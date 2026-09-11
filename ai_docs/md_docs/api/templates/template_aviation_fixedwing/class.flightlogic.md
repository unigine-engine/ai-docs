# FlightLogic Component

**Inherits from:** ComponentBase


FlightLogic is the main flight simulation controller for fixed-wing aircraft. It integrates the **JSBSim** flight dynamics model with Unigine's **IG** plugin to create a complete flight simulation experience.


The component handles flight dynamics simulation using **[FDMJSBSim](../../../api/modules/jsbsim/class.fdmjsbsim.md)**, aircraft control inputs (throttle, elevator, rudder, aileron, flaps, gear, brakes), crash detection and physics handoff via **[Crasher](../../../api/modules/jsbsim/class.crasher.md)**, camera management through **[CameraManager](../../../api/modules/cameras/class.cameramanager.md)**, sensor integration for **IR/NVG** modes, avionics **HUD** updates, and interactive tutorial system.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Model | *String* | **JSBSim** aircraft model name to load (*default: "pc7"*). |
| JSBSim Root Dir | *String* | Path to the **JSBSim** root directory containing aircraft, engine, and systems folders (*default: "modules/jsbsim"*). |
| Spawn Point | *Node* | Node defining the spawn position and orientation for the aircraft. |


### Default Controls


| Action | Keyboard | Joystick |
|---|---|---|
| Restart | *R* | - |
| Switch Camera | *N* | - |
| Start/Stop Engine | *T* | Button 9 |
| Gear | *G* | Button 11 |
| Flaps Up | *Page Up* | Button 12 |
| Flaps Down | *Page Down* | Button 13 |
| Throttle | *L.Shift / L.Ctrl* | Axis 2 |
| Elevator | *W / S* | Axis 1 |
| Rudder | *Q / E* | Axis 5 |
| Aileron | *A / D* | Axis 0 |
| Brakes | *Space* | Axis 6 |
| View | *Mouse* | POV Hat |


### See Also


- **[FDMJSBSim](../../../api/modules/jsbsim/class.fdmjsbsim.md)**
- **[Crasher](../../../api/modules/jsbsim/class.crasher.md)**
- **[GearController](../../../api/templates/template_aviation_fixedwing/class.gearcontroller.md)**
- **[RotorController](../../../api/templates/template_aviation_fixedwing/class.rotorcontroller.md)**
- **[CameraManager](../../../api/modules/cameras/class.cameramanager.md)**
