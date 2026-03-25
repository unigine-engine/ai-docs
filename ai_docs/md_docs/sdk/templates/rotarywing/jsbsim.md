# Rotary-Wing Template - JSBSim


The template has the [JSBSim library](https://jsbsim.sourceforge.net/) integrated into it.


JSBSim is a mature, open-source flight dynamics library used to simulate the physical behavior of aircraft and helicopters, as well as other airborne entities. It provides realistic modeling of aerodynamics, propulsion, and onboard systems, while UNIGINE handles visualization, input, collisions, and overall application logic.


In addition to its C++ codebase, JSBSim relies on XML configuration files that describe:


- Aircraft models (`aircraft`)
- Engines and propulsion systems (`engine`)
- Onboard systems and subsystems (`systems`)


> **Notice:** The template uses **JSBSim version 1.2.2**.
>
>
> Although newer versions are available, starting from version 1.2.3 JSBSim requires **C++17**, which is currently not used by the templates. Version 1.2.2 is therefore selected for compatibility and stability.


## Building JSBSim


This section describes how to build JSBSim to obtain the required binaries and prepare the development environment, including the headers and interface libraries needed to successfully rebuild the project template locally.


To build the JSBSim library, do the following:


1. Clone the [JSBSim](https://github.com/JSBSim-Team/jsbsim) repository. For compatibility with **C++14**, use tag **1.2.2**.
2. Build the library: place the provided **build script** (for your OS) into the root of the JSBSim repository and run it. The script will create a directory `artifacts` with the following structure: ```text artifacts/ ├ include   # headers ├ lib       # .lib (Windows) or .so (Linux) └ bin       # .dll (Windows only) ```
3. Link the library: the repository already contains **FindJSBSim.cmake**. This module expects the environment variable JSBSIM_ROOT to point to the JSBSim build artifacts directory. Once the variable is set, the library can be located in CMake with: ```text find_package(JSBSim REQUIRED) ```
4. Run the application:

  - Windows: copy `*.dll` files from `artifacts/bin` into your application's binary directory.
  - Linux: Either copy `*.so` from `artifacts/lib` into your binary directory, or set LD_LIBRARY_PATH.


## Setting Flight Model


The template includes the FlightLogic node with a corresponding FlightLogic component/property that contains two JSBSim-related parameters:


![](../modules/jsbsim/flightlogic_component.png)


| Model | Flight model used by JSBSim. The value must match the name of a directory inside the aircraft folder. |
|---|---|
| Jsbsim Root Dir | Path to the directory containing the required JSBSim folders (`aircraft, engine, systems`). The path can be absolute or relative to the application binary. |


## Data Exchange via JSBSim Properties


JSBSim connects its internal subsystems using a property-based data model. This mechanism is conceptually similar to ROS topics or UNIGINE DataBridge variables.


Each subsystem reads from and writes to named properties. For example:


- Control systems write throttle or control input values
- Engine systems read those values and compute engine state
- Other systems consume the updated results (RPM, forces, etc.)


The template interacts with JSBSim by reading and writing to these property values.


The property is addressed in code by its name in the following way:


```cpp
avionics_hud->in_throttle = fdm->getNodeValue<float>("fcs/throttle-cmd-norm[0]");

```


Otherwise, you can introduce a variable:


```cpp
struct JSBSimPropertyNodes
    {
        const char *throttle = "fcs/throttle-cmd-norm[0]";
		// … other properties
    } property_nodes;

```


And use it further in code for more convenience:


```cpp
avionics_hud->in_throttle = fdm->getNodeValue<float>(property_nodes.throttle);

```


To check or find the name, a dedicated *JSBSim Properties* window is available at runtime. It displays all properties of the currently loaded model.


![](../modules/jsbsim/prop_window.png)


This window allows you to:


1. Browse all available properties.
2. Search by name and use it in code. For example: ![](../modules/jsbsim/prop_by_name.png)
3. Inspect current values.
4. Modify writable properties interactively.


This is useful for debugging, experimentation, and adapting JSBSim to custom aircraft models or alternative control logic.


## Scope and Responsibility


Flight behavior and controllability are fully defined by the JSBSim model and its XML configuration.


The template does not directly influence aerodynamic behavior.


The template logic is responsible only for:


- Wheel-to-ground collision detection
- Aircraft body collision detection
- Post-crash behavior handling
- Wind (updated every frame using values from the UNIGINE Weather system)


## Helicopter Stabilization Features


For helicopters, two stabilization features are available:


### Stability Augmentation System (SAS)


SAS assists the pilot by stabilizing pitch and roll.


Controlled via JSBSim properties:


- `ap/afcs/pitch-channel-active-norm`
- `ap/afcs/roll-channel-active-norm`


### Altitude Hold


*Altitude Hold* maintains a constant altitude.


Controlled via `ap/afcs/altitude-channel-active-norm`


You can find both properties in the *JSBSim Properties* window and check the helicopter behavior when changing their values.
