# Rotary-Wing Template - JSBSim


This template integrates ***[JSBSim](https://jsbsim.sourceforge.net/)*** - a lightweight, data-driven flight dynamics model for non-linear, six-degree-of-freedom aircraft behavior simulation. It provides realistic modeling of aerodynamics, propulsion, and onboard systems, while UNIGINE handles visualization, input, collisions, and overall application logic.

 ![](../modules/jsbsim/img/jsbsim_r_main.png)
In addition to its C++ codebase, *JSBSim* relies on **XML configuration files** that define:


- **Aircraft models** (*<project_name>\data\template_assets\jsbsim_configs\aircraft\*)
- **Engines and propulsion systems** (*<project_name>\data\template_assets\jsbsim_configs\aircraft\..\Engines\*)
- **Onboard systems and subsystems** (*<project_name>\data\template_assets\jsbsim_configs\aircraft\..\Systems\*)


> **Notice:** By default, the template uses **JSBSim 1.2.2** for compatibility with the **C++14** project setup, as starting from version 1.2.3 JSBSim requires C++17.


Any version other than **1.2.2** must be *[built manually](../../../sdk/templates/rotarywing/custom.md#custom_jsbsim)*.


## Data Exchange via JSBSim Properties


JSBSim connects its internal subsystems using a **property-based data model** - each subsystem reads from and writes to named properties. This mechanism is conceptually similar to *[ROS topics](https://docs.ros.org/en/jazzy/Concepts/Basic/About-Topics.html)* or UNIGINE *[*DataBridge* variables](../../../api/library/plugins/databridge/class.dbvariable_cpp.md)*.


For example:


- **Control systems** write throttle or control input values
- **Engine systems** read those values and compute engine state
- **Other systems** use the updated results (RPM, forces, etc.)


The template interacts with JSBSim by reading and writing to these property values.


In code, the property is addressed by its name in the following way:


```cpp
avionics_hud->in_throttle = fdm->getNodeValue<float>("fcs/throttle-cmd-norm[0]");

```


Alternatively, you can introduce a variable:


```cpp
struct JSBSimPropertyNodes
    {
        const char *throttle = "fcs/throttle-cmd-norm[0]";
		// � other properties
    } property_nodes;

```


And use it in code for your convenience:


```cpp
avionics_hud->in_throttle = fdm->getNodeValue<float>(property_nodes.throttle);

```


At runtime, the ***JSBSim Properties*** window displays the full list of all properties of the currently loaded aircraft model.


![](../modules/jsbsim/img/prop_window.png)


In this window you can:


1. Browse all available properties.
2. Find property names by keyword and use them in code. For example: ![](../modules/jsbsim/img/prop_by_name.png)
3. Inspect current values.
4. Modify writable properties interactively.


This is useful for debugging, experimentation, and adapting JSBSim to custom aircraft models or alternative control logic.


## Flight Model Configuration


In the Editor's *World Nodes* hierarchy, the `FlightLogic` property is assigned to the `flight_logic` node, and exposes the following JSBSim-related parameters:


![](../modules/jsbsim/img/flightlogic_component.png)


| Model | Flight model used by JSBSim. The value must match the name of a directory inside the `aircraft` folder (`pc7` by default). |
|---|---|
| Jsbsim Root Dir | Path to the directory containing the required JSBSim folders (`aircraft, Engines, Systems`). The path can be absolute or relative to the application binary. |


## Scope and Responsibility


Flight behavior and controllability are fully defined by the JSBSim model and its XML configuration - **the template does not directly affect aerodynamics**.


The template logic is responsible for:


- Wheel-to-ground collision detection
- Aircraft body collision detection
- Post-crash behavior handling
- Wind influence (updated every frame using values from the UNIGINE *[Weather system](../../../sdk/templates/rotarywing/weather.md)* and then smoothly interpolated by the JSBSim aerodynamic model to avoid abrupt changes).


## Helicopter Stabilization Features


For helicopters, the template provides two stabilization features:


![](../modules/jsbsim/img/jsbsim_heli.png)


### Stability Augmentation System (SAS)


SAS assists the pilot by stabilizing pitch and roll. It is controlled via the following JSBSim properties:


- `ap/afcs/pitch-channel-active-norm`
- `ap/afcs/roll-channel-active-norm`


When enabled, these property values are set to 0.5.


### Altitude Hold


*Altitude Hold* maintains a constant altitude. It is controlled via:


- `ap/afcs/altitude-channel-active-norm`


![](../modules/jsbsim/img/jsbsim_heli_stabilization.png)


These properties can be found in the *JSBSim Properties* window in the template menu at runtime. Try adjusting their values from 0 to 1 to observe how the helicopter behavior changes.
