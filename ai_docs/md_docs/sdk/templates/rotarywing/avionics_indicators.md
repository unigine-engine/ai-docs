# Rotary-Wing Template - Flight Instruments Simulation


The template contains a framework for simulating the following flight instruments:


| Airspeed | Altimeter | Attitude | Variometer | Compass |
|---|---|---|---|---|
| ![](../modules/avionics_indicators/img/airspeed.png) | ![](../modules/avionics_indicators/img/altimeter.png) | ![](../modules/avionics_indicators/img/attitude.png) | ![](../modules/avionics_indicators/img/variometer.png) | ![](../modules/avionics_indicators/img/compass.png) |
| *Flight instruments at runtime* |  |  |  |  |


Each instrument is implemented through a separate component with a matching name, and updates its corresponding value in real time, reflecting the aircraft's changing transforms.


## Flight Instruments Configuration


The framework's functionality is implemented as follows:


- **In the Editor**, each *[instrument component](#component)* is attached to a dedicated *ObjectMeshStatic* node inside the aircraft/vehicle `*.node` file, exposing the following parameters for editing: ![](../modules/avionics_indicators/img/editor_prop.png) You can modify the property settings (such as textures, size, and other parameters) to *[customize the instrument appearance](../../../sdk/templates/rotarywing/custom.md#custom_indicators)* according to your project's needs. The `FlightLogic` and `AvionicsHUD` properties, attached to the `flight_logic` *Node Dummy*, are responsible for passing aircraft state data to the instruments. Note that **instrument readings are updated via code** at runtime and cannot be bound to fixed values directly in the Editor.
- **At runtime,** changes to the corresponding `in_*` parameters of the `AvionicsHUD` component (such as `in_speed, in_altitude`) dynamically drive the visual updates of the instruments. The parameters exposed by this component are updated by `FlightLogic` during simulation. In the template, their values are provided by *[JSBSim](../../../sdk/templates/fixedwing/jsbsim.md#prop_data_exchange)*. The complete list of **in_*** parameters is available in the *[AvionicsIndicatorsController](../../../api/modules/avionics/class.avionicsindicatorscontroller.md)* class.
