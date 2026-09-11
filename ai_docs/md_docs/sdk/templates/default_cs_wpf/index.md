# C# (WPF) Empty Template


A C# template for **embedding UNIGINE real-time 3D rendering into a [WPF](https://learn.microsoft.com/en-us/dotnet/desktop/wpf/overview/) desktop application** (Windows only). It is intended for cases where you already have an existing software framework and need UNIGINE primarily for real-time 3D visualization inside it - for example, a simulation, training, or visualization application built around its own interface, tools, and workflows. Here the 3D view is a component of a larger Windows application rather than a standalone application occupying the entire screen.


In this setup the WPF application owns the window and the user interface, while the Engine renders into a viewport placed among regular WPF interface elements: panels, toolbars, docked windows, and dialogs. This makes the template suitable for adding a 3D viewport to an existing product without restructuring its user interface, toolchain, or build process around the Engine.


The Engine runs on a dedicated thread, separate from the WPF UI thread. This is essential for this type of integration: on a single thread the Engine loop and the WPF dispatcher compete for it, resulting in either a reduced frame rate or an unresponsive interface. With the Engine on its own thread, the application keeps a responsive interface and a full frame rate at the same time.


The integration layer required for correct operation within a host Windows application is provided out of the box: mouse and keyboard input, window management and resizing, fullscreen mode, multi-monitor and DPI handling, clipboard access, and system dialogs. It is implemented as a *[CustomSystemProxy](../../../api/library/engine/class.customsystemproxy_cpp.md)* - the approach used when the host application has its own windowing and input systems, described in *[Embedding UNIGINE in Third-Party Application](../../../code/integration/index.md#unigine_embedding)*. Mouse handling accounts for the mixed interface: the cursor remains free so that WPF controls stay clickable, and the Engine captures it for camera control only when a click occurs within the 3D viewport. Custom interface elements are added following the same pattern as the ones already present in the project.


The template includes a basic scene with a first-person controller, so that the viewport displays meaningful content immediately. The scene content can be removed without affecting the integration.


> **Notice:** The boot (splash) screen is disabled, preventing a second window and flicker at startup.


For a detailed description of the integration and instructions on bringing it into an existing project, refer to the *[Integrating with Frameworks](../../../code/csharp/usage/unigine_app/proxy.md)* article.


## Features


- UNIGINE rendering viewport hosted inside a WPF application
- 3D view coexisting with regular WPF interface elements
- Engine running on a dedicated thread: full frame rate without blocking the interface
- Input support: keyboard + mouse, with mouse capture limited to the 3D viewport so that WPF controls stay clickable
- Window management: resizing, fullscreen mode, icons, and window styles
- Multi-monitor and DPI handling
- Clipboard access and system dialogs
- Basic character movement
- Physics-based interaction with simple rigid body objects
- Default scene content for interaction and testing purposes
- Pre-baked lighting
