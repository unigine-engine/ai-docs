# Image Generator Template (CPP)


A default C++ [Image Generator (IG)](../../../ig/index.md) project template designed for developing custom IG-based applications. It supports multi-monitor rendering as well as VR and XR modes.


- High-Level Image Generator (IG) functionality
- Support for CIGI, HLA, and DIS protocols
- Support for multiple control and input devices
- Weather system
- Lighting and airfield infrastructure


The template allows creating a real-time visual system rendering the scene based on data received from an external host, such as a simulator, training system, or control application. The IG manages scene visualization, camera control, environmental conditions, and entity state updates, while the host system provides simulation logic and control commands.


## Features


The template provides a clean environment with basic IG initialization and integration logic for further extension and host-side control. It is designed to demonstrate key features that can be configured to meet the requirements of a wide range of simulation applications.


**Key features:**


- High-Level [Image Generator (IG)](../../../ig/index.md) functionality:

  - Cross-platform host emulator for debugging
  - Entity creation, deletion, and control
  - Control of articulated entity parts
  - View and viewgroup management
  - HAT/HOT request support
- Support for CIGI, HLA, and DIS (Sim edition only)
- Support for multiple control and input devices:

  - Keyboard + mouse
  - Joysticks
  - HOTAS/HOSAS (throttles, flight sticks, and rudder pedals)
- Weather System:

  - Time-of-day control
  - Weather condition control
