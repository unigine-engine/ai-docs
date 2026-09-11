# Fixed-Wing Flight Simulator Template


![](ig_sm.jpg)


A configurable flight simulation template featuring a fixed-wing aircraft. It supports multi-monitor rendering as well as VR and XR modes.


- Flight dynamics
- Full aircraft control workflow
- Avionics systems
- Support for multiple control and input devices
- Heads-up display (HUD)
- Weather system
- Lighting and airfield infrastructure


The template supports the full aircraft operation cycle from takeoff to landing, multiple control devices and camera modes, a HUD and basic avionics, ground and water traffic, as well as environmental interaction including weather effects and lighting.


> **Warning:** The [IG Aviation Add-on](../../../sdk/addons/aircraft/index.md) is already included in this template. Do not add it again, as duplicating the add-on may cause conflicts.


## Features


The template features a fixed-wing aircraft and is designed to demonstrate key features that can be configured to meet the requirements of a wide range of simulation applications.


**Key features:**


- Flight dynamics simulated using the [JSBSim library](https://jsbsim.sourceforge.net/)
- Full aircraft control workflow:

  - Takeoff
  - En-route flight
  - Landing
- Avionics systems:

  - Airspeed indicator
  - Altimeter
  - Attitude indicator
  - Variometer
  - Compass
- Support for multiple control and input devices:

  - Keyboard + mouse
  - Joysticks
  - Gamepads
  - HOTAS/HOSAS (throttles, flight sticks, and rudder pedals)
  - Step-by-step controls tutorial
- Multiple camera modes:

  - First-person (cockpit) view
  - Third-person (external) view
  - Free camera mode
- Heads-up display (HUD)
- Sensors:

  - Thermal sensor (thermal imaging)
  - Electronic interference / jamming simulation
- Lighting and airfield infrastructure:

  - Runway lighting
  - Approach and taxiway lights
  - PAPI / VASI visual approach guidance systems
- Dynamic environment interaction:

  - Collision with power line poles and wires
  - Ground vehicle traffic
  - Water traffic:

    - Small and large vessels
    - Wake (ship trail) simulation
- Weather system:

  - Time-of-day control
  - Weather condition control
  - Windsock
  - Signal smoke reacting to wind
- High-Level [Image Generator (IG)](../../../ig/index.md) functionality:

  - Cross-platform host emulator for debugging
  - Entity creation, deletion, and control
  - Control of articulated entity parts
  - View and viewgroup management
  - HAT/HOT request support
- Engine sound simulation
- Simplified scene content (replaceable)
- Immersive visualization:

  - Multi-monitor rendering support
  - VR mode
  - XR mode with chroma key support


## Main Menu


At runtime, click the ***Windows*** button in the top-left corner to open the main menu, from which the following configuration panels can be accessed:


![](../modules/main_desc/img/fixed_menu.png)


- **Light Controls** - toggle airfield lighting presets (*Runway, Approach, Taxiway*).
- **[Weather Configurator](../../../sdk/templates/fixedwing/weather.md)** - adjust time of day, weather conditions, and wind.
- **[Input Configurator](../../../sdk/templates/fixedwing/controls.md)** - set up controls and device bindings.
- **[Profile Configurator](../../../sdk/templates/fixedwing/controls.md#input_profile)** - manage input profiles for different devices and controller models.
- **[JSBSim Properties](../../../sdk/templates/fixedwing/jsbsim.md)** - browse the list of JSBSim properties of the currently loaded aircraft model.
- **[HUD Configuration](../../../sdk/templates/fixedwing/avionics_hud.md)** - configure flight instrument data displayed in the viewport.
- **Tutorial** - follow the step-by-step template training tool.
- **VR Options** - configure VR (available when a headset is connected).
- **Quality Settings** - switch between rendering presets *(Low / Medium / High)*.
- **[Sensor Configurator](../../../sdk/templates/fixedwing/sensors.md)** - enable and configure available sensors.
- **[Picture-in-Picture Display](../../../sdk/templates/fixedwing/sensors.md#widgetpictureinpicture_component)** - adjust PiP window layout in third-person mode.


## Template Tutorial


![](../modules/main_desc/img/tutorial_f.png)


On application startup, you will see the *Tutorial* window, which guides you through the core template features. By following its steps, you can try basic vehicle controls using default input bindings, try flight model-specific systems and switch between camera modes to explore the environment from different perspectives.


![](../modules/main_desc/img/tutorial_ui_f.png)


## Using the Template For Project Creation


The template is designed as a ***flexible foundation for [customization](../../../sdk/templates/fixedwing/custom.md)***, enabling the use of different flight models and real-world locations. Dynamic interaction with the environment makes crashes feel impactful, supports practicing realistic scenarios, and simplifies onboarding for a vehicle control, making it suitable for both professional simulators and game development.
