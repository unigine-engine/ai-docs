# Rotary-Wing Flight Simulator Template


A configurable flight simulation template featuring a rotary-wing aircraft. It supports multi-monitor rendering as well as VR and XR modes.


- Flight dynamics
- Full aircraft control workflow
- Avionics systems
- Support for multiple control and input devices
- Heads-up display (HUD)
- Weather system
- Lighting and airfield infrastructure


The template supports the full aircraft operation cycle from takeoff to landing, multiple control devices and camera modes, a HUD and basic avionics, ground and water traffic, as well as environmental interaction including weather effects and lighting.


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
