# What's Inside?


UNIGINE engine is a fully-featured 3D platform designed for creation of interactive virtual worlds with a photo-realistic quality. This powerful and extremely flexible solution is used for real-time simulation (transportation, military training, etc.), visualization (architecture, media installations, etc.) and game development.


However, UNIGINE is not some sort of application building constructor: it is a very robust, feature-rich, and optimized software library with a set of tools. So you will need some people in the team with programming skills (preferably C++) to utilize the UNIGINE power for your projects. Please also note that some features are optional, depending on the SDK edition (*Community / Engineering / Sim*).


![](slider_main.gif)


UNIGINE provides support for Windows and Linux.


![](logos.png)


For more details, see [hardware requirements](../../start/requirements.md).


## Renderer


The UNIGINE image generator provides a [near-photorealistic rendering](https://unigine.com/products/community/advantages/#photorealistic-graphics) of visual scenes based on sophisticated shading and lighting models, accurate atmosphere model, advanced special effects and lifelike post-processing.


| ![](ig.jpg) | - Physically based rendering (PBR) - GGX BRDF: realistic speck from light sources - Ultra-quality environment probes - Energy conservation model - Microfiber effect for fabric - Cinematic post-effects: SSAO, motion blur, chromatic aberrations, grain effect, sharpness filter, etc. |
|---|---|


- Atmospheric light scattering for realistic simulation of the atmosphere
- Excellent rendering of vast, detailed masses of vegetation
- Configurable forward and deferred rendering
- Support for HLSL and [UUSL](../../code/uusl/index.md) languages for shaders
- Support for DirectX 12 and Vulkan


## Image Output Schemas


| ![](output.jpg) | UNIGINE handles various image output schemas: - Multi-channel image generation (cluster rendering) via proprietary [Syncker](../../code/plugins/syncker/index.md) system or standard CIGI protocol - [Multi-projector setups](../../principles/render/output/multi_monitor/spidervision_plugin/index.md) with support for edge blending and image warping |
|---|---|


- Stereoscopic rendering in multiple modes, including native support for VR headsets:

  - Oculus Rift / Rift S / Quest / Quest 2 (with Oculus Link cable / Oculus Link wireless)
  - HTC Vive / Vive Pro / Focus / Cosmos
  - Varjo VR-1 / VR-2 / VR-3 / XR-3 (with extended mixed reality support)
  - Windows Mixed Reality (WMR)-compatible
  - OpenVR-compatible
- [Multi-monitor rendering](../../principles/render/output/multi_monitor/index.md) for video walls
- [Panoramic rendering](../../principles/render/output/apppanorama/index.md), including fisheye mode


## Scene Manager


Built-in advanced scene manager is designed for handling virtual worlds of unprecedented scale filled with thousands of objects.


| ![](scene.jpg) | - Support for 64-bit double precision of coordinates - Scene graph providing nodes hierarchy, easy control over nodes and branches relative object-space transformations, spatial multi-tree subdivision - Asynchronous data streaming - Advanced LOD system - Increased camera precision - Procedural placement of big amount of objects |
|---|---|


- Support for geo-coordinates
- Extremely fast intersection / line of sight tests
- Increased visibility distance


## Built-in Objects


UNIGINE provides a set of [built-in objects](../../objects/index.md) allowing you to create a complex, dynamic virtual world:


| ![](animation.jpg) | - [Nodes](../../objects/nodes/index.md) serve to organize other nodes into a hierarchy, create new pivot points and triggers - [Light sources](../../objects/lights/index.md) represent different kinds of the scene illumination: global, omni-directional, projected, etc. - [Objects](../../objects/objects/index.md) represent imitations of entities present in the real world: objects, sky, terrains, water, etc. - [Effects](../../objects/effects/index.md) contain particles systems, physical fields, volumetric objects, decals, etc. - [Players](../../objects/players/index.md) represent different kinds of cameras |
|---|---|


- [World nodes](../../objects/worlds/index.md) are invisible nodes used for world management
- [Sound objects](../../objects/sounds/index.md) represent sound sources and reverberations
- [Pathfinding objects](../../objects/navigations/navigation/index.md) represent objects used for pathfinding


## Physics Engine


There is a built-in [physics engine](../../principles/physics/index.md) available. Please take into the account that it is designed primarily for "game-level" physics simulation: for accurate simulation of physical processes (e.g.: flight dynamics model) it is recommended to use the specialized solutions.


| ![](physics.gif) | - Collision detection and rigid body physics - Ragdolls - Various joints, motors and springs - Deformable cloth and rope physics - Dynamic destruction of objects - Force fields - Fluid buoyancy and two-way interaction - Time reverse feature |
|---|---|


## Application Programming Interfaces


| ![](api.jpg) |
|---|
| You can choose among powerful UNIGINE APIs: - [C++ API](../../api/index.md) for maximum performance and seamless integration with the existing code base - [C# API](../../code/csharp/index.md) for a good balance between speed and ease of use with the [Component System](../../principles/component_system/component_system_cs/index.md) integrated into the UnigineEditor - Fast iterative scripting with [UnigineScript](../../code/uniginescript/index.md), featuring instant compilation |


## Input Systems


| ![](input.jpg) | UNIGINE handles various user input schemas: - Standard PC keyboards and mice - Multi-touch screens - Gamepads and joysticks - Head trackers - 6 DOF positioning devices - Motion capture systems We also offer our API for adding custom devices. |
|---|---|


## Audio System


| ![](sound.jpg) | Multi-channel audio system with support for: - 3D effects - Sound occlusion - Reverberation zones |
|---|---|


## Graphical User Interface


| ![](gui.jpg) | There are several ways to implement GUIs in UNIGINE-powered applications: - Integration into [Qt applications](../../code/cpp/usage/unigine_app/AppQt.md) - [Native GUI](../../code/gui/index.md) (rich set of widgets with 2D/3D effects and localization support) |
|---|---|


## Tools


| [![](editor.jpg)](../../tools/index.md) | - [UnigineEditor](../../editor2/index.md) provides the core functionality for creation and editing of virtual worlds for UNIGINE-based applications. It allows you to easily view and modify virtual worlds by adding, transforming and editing the nodes. - [SDK browser](../../sdk/index.md) for easy access to the SDK components and updates - [Performance profiling](../../tools/profiling/index.md) tools - A set of other utilities for data conversion and compression |
|---|---|
