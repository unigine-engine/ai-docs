# Rotary-Wing Flight Simulator Template


![](../rotarywing/img/rotarywing_template.png)


A configurable flight simulation template featuring a rotary-wing aircraft. It supports multi-monitor rendering as well as VR and XR modes.


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


The template features a rotary-wing aircraft designed to demonstrate key features that can be configured to meet the requirements of a wide range of simulation applications.


**Key features:**


- Flight dynamics simulated using the [JSBSim library](https://jsbsim.sourceforge.net/)
- Full aircraft control workflow:

  - Takeoff
  - En-route flight
  - Landing
  - Hovering
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

  - Equipped helicopter landing pads (helipads)
  - Multiple landing surface types:

    - Concrete
    - Soil
    - Grass
    - Snow
    - Water
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
- Rotor effects ([IG Aviation add-on](../../../sdk/addons/aircraft/index.md) content):

  - Rotor downwash and interaction effects
  - Rotor blade oscillations driven by wind-induced aerodynamic loads
  - Dynamic blade response during takeoff and landing phases
- Engine visual effects
- Simplified scene content (replaceable)
- Immersive visualization:

  - Multi-monitor rendering support
  - VR mode
  - XR mode with chroma key support


## Main Menu


At runtime, click the ***Windows*** button in the top-left corner to open the main menu, from which the following configuration panels can be accessed:


![](../modules/main_desc/img/rotary_menu.png)


- **[Weather Configurator](../../../sdk/templates/rotarywing/weather.md)** - adjust time of day, weather conditions, and wind.
- **[Input Configurator](../../../sdk/templates/rotarywing/controls.md)** - set up controls and device bindings.
- **[Profile Configurator](../../../sdk/templates/rotarywing/controls.md#input_profile)** - manage input profiles for different devices and controller models.
- **[JSBSim Properties](../../../sdk/templates/rotarywing/jsbsim.md)** - browse the list of JSBSim properties of the currently loaded aircraft model.
- **[HUD Configuration](../../../sdk/templates/rotarywing/avionics_hud.md)** - configure flight instrument data displayed in the viewport.
- **Tutorial** - follow the step-by-step template training tool.
- **VR Options** - configure VR (available when a headset is connected).
- **Quality Settings** - switch between rendering presets *(Low / Medium / High)*.
- **[Sensor Configurator](../../../sdk/templates/rotarywing/sensors.md)** - enable and configure available sensors.
- **[Picture-in-Picture Display](../../../sdk/templates/rotarywing/sensors.md#widgetpictureinpicture_component)** - adjust PiP window layout in third-person mode.


## Template Tutorial


![](../modules/main_desc/img/tutorial_r.png)


On application startup, you will see the *Tutorial* window, which guides you through the core template features. By following its steps, you can try basic vehicle controls using default input bindings, try flight model-specific systems and switch between camera modes to explore the environment from different perspectives.


![](../modules/main_desc/img/tutorial_ui_r.png)


## Using the Template For Project Creation


The template is designed as a ***flexible foundation for [customization](../../../sdk/templates/rotarywing/custom.md)***, enabling the use of different flight models and real-world locations. Dynamic interaction with the environment makes crashes feel impactful, supports practicing realistic scenarios, and simplifies onboarding for a vehicle control, making it suitable for both professional simulators and game development.
