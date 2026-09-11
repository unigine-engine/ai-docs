# UAV Flight Simulator Template


![](../uav/img/vtol.png)


A configurable flight simulation template featuring manual operation of unmanned aerial vehicles.


- Flight dynamics
- Support for multiple UAV types
- Support for multiple control and input devices
- Camera zoom control and other effects
- On-screen indicators and UI
- Weather system


The template supports multiple UAV types, control devices, and camera modes, on-screen instruments and sensor simulation, ground traffic and obstacles, as well as environmental interaction including weather effects and lighting.


## Features


The template features unmanned aerial vehicles (UAVs) designed to demonstrate key features that can be configured to meet the requirements of a wide range of simulation applications.


**Key features:**


- Flight dynamics:

  - Simplified quadcopter aerodynamics
  - VTOL flight model
  - Fixed-wing aircraft flight model
  - Wind simulation model affecting UAV dynamics
- Manual UAV flight simulation with support for multiple aircraft types:

  - FPV quadcopter
  - VTOL quadcopter
  - Fixed-wing UAV
  - Fixed-wing UAV launched from a catapult
- Switchable UAV models during simulation
- Support for multiple control and input devices:

  - Keyboard + mouse
  - Gamepads
  - Real UAV remote controllers
- Multiple camera modes:

  - First-person (FPV) view
  - Third-person (external) view
  - Free camera mode
- On-screen indicators and UI:

  - Airspeed indicator
  - Battery charge indicator
  - Mini-map
  - Camera zoom control
- Sensor systems:

  - Thermal sensor (thermal imaging)
  - Electronic interference / jamming simulation
- Camera effects:

  - Rolling shutter effect simulation
- Dynamic environment interaction:

  - Collision with power line poles and wires
  - Ground vehicle traffic
- Weather system:

  - Time-of-day control
  - Weather condition control
  - Windsock
  - Signal smoke reacting to wind
- UAV engine and propeller sound effects
- Simplified scene content (replaceable)
- Immersive visualization:

  - Multi-monitor rendering support
  - VR mode
  - XR mode with chroma key support


## Main Menu


At runtime, click the ***Windows*** button in the top-left corner to open the main menu, from which the following configuration panels can be accessed:


![](../modules/main_desc/img/uav_menu.png)


- **[Weather Configurator](../../../sdk/templates/uav/weather.md)** - adjust time of day, weather conditions, and wind.
- **[Input Configurator](../../../sdk/templates/uav/controls.md)** - set up controls and device bindings.
- **[Profile Configurator](../../../sdk/templates/uav/controls.md#input_profile)** - manage input profiles for different devices and controller models.
- **Tutorial** - follow the step-by-step template training tool.
- **VR Options** - configure VR (available when a headset is connected).
- **Quality Settings** - switch between rendering presets *(Low / Medium / High)*.
- **[Sensor Configurator](../../../sdk/templates/uav/sensors.md)** - enable and configure available sensors.
- **[Picture-in-Picture Display](../../../sdk/templates/uav/sensors.md#widgetpictureinpicture_component)** - adjust PiP window layout in third-person mode.


## Template Tutorial


![](../modules/main_desc/img/tutorial.png)


On application startup, you will see the *Tutorial* window, which guides you through the core template features. By following its steps, you can try basic vehicle controls using default input bindings, switch between UAVs and camera modes to explore the environment from different perspectives.


![](../modules/main_desc/img/tutorial_ui.png)


## UAV Types


The template provides several ready-to-use UAVs, each with its own flight model. Switching respawns the selected vehicle at the spawn point, so you can compare how differently they behave in the same conditions.


![](../modules/main_desc/img/uav_models.png)


- **FPV quadcopter** - a multirotor with simplified quadcopter aerodynamics, taking off vertically from the ground.
- **Fixed-wing UAV** - an aircraft with control surfaces (rudders and ailerons), taking off from the runway.
- **Fixed-wing UAV on a catapult** - the same flight model launched from a *[catapult](#catapult_launch)* instead of the runway.
- **VTOL quadcopter** - a hybrid vehicle that takes off vertically and then transitions to wing-borne flight.


The vehicles are flown over an island environment that combines an airport setup - a runway and the related assets - with an urban area of road networks and background traffic, so that both open-space flight and flight among obstacles can be practiced in the same scene.


### Catapult Launch


Along with taking off from the ground, a fixed-wing UAV can be launched from a **catapult** - a rail-and-platform rig that accelerates the aircraft along a straight track and releases it in the air at flight speed. This reproduces the way lightweight fixed-wing drones are deployed in the field, where no runway is available.


![](../modules/main_desc/img/uav_launch.png)


The catapult is a separate UAV preset, selected the same way as the other vehicles. Once it is active, the aircraft is locked onto the platform and the launch sequence is as follows:


1. Arm the aircraft (the *Arm* action).
2. Trigger the launch (the *Launch* action). The platform accelerates the UAV along the rail.
3. At the end of the track the aircraft is released with the accumulated speed and continues under your control.


While the platform is moving, the engine is at full throttle and your pitch, yaw, and roll input is already applied, so the control surfaces can be set up in advance, before the aircraft leaves the rail. After the release, control returns to the regular fixed-wing flight model.


> **Notice:** If the UAV is flown by an autopilot via *[ArduPilot SITL](../../../sdk/templates/uav/sitl.md)*, the catapult unlocks the aircraft as soon as the autopilot takes over the controls, and takeoff is performed by ArduPilot instead.


## Using the Template For Project Creation


The template is designed as a ***flexible foundation for [customization](../../../sdk/templates/uav/custom.md)***, enabling the use of different flight models and real-world locations. Dynamic interaction with the environment makes crashes feel impactful, supports practicing realistic scenarios, and simplifies onboarding for a vehicle control, making it suitable for both professional simulators and game development.
