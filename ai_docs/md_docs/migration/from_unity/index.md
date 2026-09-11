# Migrating to UNIGINE from Unity


This section gives a brief overview of UNIGINE from a *Unity* user's perspective and provides basic information to help you transfer your *Unity* experience to UNIGINE.


> **Notice:** Please consider [hardware requirements](../../start/requirements.md) first.


## Overview


> **Notice:** You can transfer your *Unity* project to UNIGINE using a free community-generated UNIGINEEditor Plugin (*Unity Importer*), available from our [Add-On Store](https://store.unigine.com/en-US/add-on/1eefdaff-41c4-6b10-ace6-6b87a2ef1d21/).


## Quick Glossary


This chapter matches common *Unity* software terms on the left and their UNIGINE equivalents (or rough equivalent) on the right. UNIGINE keywords are linked directly to related articles to provide you with more in-depth information.


| Category | Unity software | UNIGINE |
|---|---|---|
| **Project and SDK management** | Hub | [SDK Browser](#sdk) |
| **Editor UI** | Hierarchy Panel | [World Nodes](../../editor2/interface/index.md#world_hierarchy) Hierarchy window |
| Inspector | [Parameters window](../../editor2/interface/index.md#parameters) |  |
| Project Browser | [Asset Browser window](../../editor2/assets_workflow/index.md#asset_browser) |  |
| Scene View | [Editor Viewport](#editor_scene) |  |
| **Scene** | Scene | [World](#scene) |
| **Gameplay Types** | Component | [Component System](../../migration/from_unity/code.md) |
| GameObject | [Node](#scene_objects) |  |
| Prefab | [NodeReference](#prefabs) |  |
| **Meshes** | Mesh Renderer | [Static Mesh](../../migration/from_unity/content.md#content_meshes), [Dynamic Mesh](../../objects/objects/mesh_dynamic/index.md) |
| Skinned Mesh Renderer | [Skinned Mesh](../../migration/from_unity/content.md#skinned) |  |
| Blendshapes | [Morph Targets](../../migration/from_unity/content.md#morphing) |  |
| **Effects** | Particle System | [Particle System](../../objects/effects/particles/index.md) |
| Halo | [Volumetric Objects](../../objects/effects/volumetrics/index.md) |  |
| Lens Flares | [Lens Flares](../../objects/lights/parameters/index.md#lens_flares_settings) |  |
| Billboard Renderer | [Billboards](../../migration/from_unity/content.md#optimize_billboards) |  |
| Projector / Decal Projector (HDRP) | [Decals](../../objects/decals/index.md) |  |
| **Exteriors** | Terrain | [Terrain systems](../../objects/objects/terrain/index.md) |
| Trees / Grass | [Mesh Clutter](../../objects/objects/mesh_clutter/index.md), [Grass](../../objects/objects/grass/index.md), [Vegetation Add-On](../../sdk/addons/vegetation/index.md) |  |
| Wind Zones | [Animation Field](../../objects/effects/fields/field_animation/index.md) |  |
| **Game UI** | UI | [GUI](../../objects/objects/gui/index.md) |
| **Lighting** | Light Sources | [Light Sources](../../migration/from_unity/content.md#lighting_light_sources) |
| Environment | [Environment](../../migration/from_unity/content.md#lighting_environment) |  |
| Lightmapping | [Voxel GI](../../migration/from_unity/content.md#lighting_gi) |  |
| Reflection Probes | [Environment Probes](../../migration/from_unity/content.md#lighting_reflection_probes) |  |
| **Rendering** | Shader | [Base Material](../../migration/from_unity/content.md#materials) |
| Material | [User Material](../../content/materials/index.md#user_materials) |  |
| Custom Shaders: HLSL | HLSL / [UUSL](../../code/uusl/index.md) |  |
| Custom Shaders: Shader Graph | [Material Graphs](../../content/materials/graph/index.md) |  |
| Compute Shaders | [UUSL Compute Shaders](../../code/uusl/compute.md) |  |
| Rendering Paths | [Rendering Sequence](#graphics_render_paths) |  |
| Multi-Display Rendering | [Multi-Monitor Rendering plugins](../../principles/render/output/multi_monitor/index.md), [Syncker Plugin](../../code/plugins/syncker/index.md) for Multi-Node Rendering |  |
| **Programming** | C# | [C++](../../code/cpp/index.md) / [C#](../../code/csharp/index.md) |
| Scriptable Render Pipeline (URP / HDRP) | Rendering Sequence is fully accessible from [API](../../api/library/rendering/index.md) / [Scriptable Materials](../../content/materials/scriptable.md) |  |
| **Physics** | Raycast | [Intersections](../../code/usage/intersections/index_cpp.md) |
| Rigid Body | [Rigid Body](../../principles/physics/bodies/rigid/index.md) |  |
| Collider | [Shape](../../principles/physics/shapes/index.md) |  |
| Joint | [Joint](../../principles/physics/joints/index.md) |  |
| Cloth | [Cloth Body](../../principles/physics/bodies/cloth/index.md) |  |
| **Animation** | Timeline | [Tracker](../../editor2/tools/tracker/index.md) |
| **Navigation and Pathfinding** | NavMesh, NavMeshAgent, Off-Mesh Link, NavMesh Obstacle | [Navigation Areas](../../objects/navigations/navigation/index.md), [Obstacles](../../objects/navigations/obstacle/index.md) |


## Project and SDK Management


As a *Unity* software user, you are accustomed to use **Unity Hub** � the application that streamlines the way you find, download and manage your projects and installations.


**[UNIGINE SDK Browser](../../sdk/index.md)** is the first step to start working with UNIGINE Engine. This application enables you to manage your projects and installed SDKs, as well as gives you access to the samples and the knowledge base.


[![Unity Hub and UNIGINE SDK Browser Comparison (click to enlarge)](unity_unigine_sdk.png)](unity_unigine_sdk.png)

*Unity Hub and UNIGINE SDK Browser Comparison*


UNIGINE provides several [programming workflows](../../code/fundamentals/programming_overview/index.md), to easily adapt your experience of scripting in *Unity* software, it is recommended to use [C# Component System](../../migration/from_unity/code.md). [Creating a project](../../sdk/projects/index_cpp.md#creation) using this workflow in SDK Browser is done as follows:


1. Click *Create Project* on the *C++ Empty* template card in the *Templates* tab. ![](../../sdk/projects/create_project_cs.png) > **Notice:** If you want to make a project compatible with one of the supported VR headsets, use the **VR C#** template instead. This will enable required plugins, add template assets and components (more about [VR-compatibility](../../vr_development/vr_template/index.md)).
2. Click *Create New Project*.
3. Once the new project is created, it will appear in the *My Projects* tab. Click ***Open Editor*** to open it in UnigineEditor.


> **Notice:** **C# API** section available in the **Samples** showcases traditional programming workflow in C#. For samples that use [C# Component System](../../migration/from_unity/code.md), take a look at the `Data ->C# Component Samples`.


## Editor Interface


Below you can see interfaces of *Unity Editor* and UnigineEditor. Interface elements in the images are color-coded to indicate common functionality. Each element has a label to show UNIGINE's equivalent. The layout of UnigineEditor is fully [customizable](../../editor2/interface/customize/index.md) by resizing, dragging and dropping the tabbed windows. UnigineEditor adopts a dark color scheme.


[![Unity and UNIGINE Editor UI Comparison (click to enlarge)](unity_unigine_editor.png)](unity_unigine_editor.png)

*Unity Editor and UnigineEditor UI Comparison*


To learn more about the UnigineEditor interface, read [this article](../../editor2/interface/index.md).


### Scene View


You may find the *Scene View* and the *Editor Viewport* controls looking very much alike.


| ![](unity_scene_view.png) | ![](unigine_editor_viewport.png) |
|---|---|
| *Unity Scene View* | *UNIGINE Editor Viewport* |
| ![](../from_ue/unigine_editor_viewport_2.png) |  |


You can use:


- **Camera panel** to switch between [cameras](#scene_players) and configure the current one.
- **Rendering Debug** to display the contents of rendering buffers the same way as using the *Draw Mode* in *Unity Editor*.
- **Navigation panel** to quickly set up and switch between camera speed presets and change the camera position.


*Navigation* inside the *Editor Viewport* is pretty much the same as in *Unity Scene View*. However, get familiar with [Scene Navigation](../../editor2/navigation/index.md) so as not to miss details.


Also, a set of global switchers is available in the top toolbar:


![](unigine_toolbar.png)


- **[Helpers](../../editor2/using_visual_helpers/index.md)** panel provides quick access to auxiliary visualizers, such as icons, *gizmos* and wireframes.
- **Precompile All Shaders** toggle is used for [Forced Shaders Compilation](../../editor2/shaders_precompile/index.md)
- **[Animation](../../migration/from_unity/content.md#skinned)** toggle
- **[Physics](../../migration/from_unity/physics.md)** toggle
- **[Audio](../../migration/from_unity/content.md#audio_video)** toggle
- **[Play controls](#editor_game)**


You can use as [many Editor Viewports](../../editor2/camera_settings/index.md#camera_viewport) as you need.


### Game View and Play Mode


You are accustomed that *Unity* Editor has the *Play* mode inside the *Game View* which is rendered from the camera(s) in your scene, being representative of your final build.


![](unity_play_controls.png)


In UNIGINE, the *Play* button is used to [run an instance](../../principles/component_system/component_system_cs/index.md#run) of the application in a separate window. You can switch between *Play* presets to change essential parameters of the play mode, such as **VR Mode** to enable compatibility with one of supported VR headsets, as an example.


![](../../principles/component_system/component_system_cs/run.png)


By default, the mouse cursor is grabbed when clicked in the *Play* mode. There are two ways to setup default Input Bindings (key states and the mouse behaviour):


- In the [Controls](../../editor2/settings/controls/index.md) settings of the Editor.
- Via [code](../../migration/from_unity/code.md#code_input).


> **Notice:** The *Engine Viewport*, the *Game View's* counterpart in UNIGINE used for debugging and profiling, is considered excessive for projects using C# .NET programming workflow (however, it is still available for other workflows).


### Console


As well as *Unity* software, UNIGINE has the [Console](../../code/console/index.md) used for standard input, output and error logging. A set of [console commands](../../code/console/index.md#meta) is provided.


It is available both in UnigineEditor and a running application. To open the Console window in the Editor, go to *Windows -> Console* menu:


![](unigine_console.png)


A built-in console is called by pressing the **F1** key:


![](../../code/console/console_sm.jpg)


You can use it to [print user messages from code](../../migration/from_unity/code.md#code_log).


### Packing a Final Build for Publishing


You got used to building your projects via *Unity* Editor. In UNIGINE, [packing a final build](../../editor2/projects/build_project.md) is also done via UnigineEditor.


## Projects and Files


### Directories and Files


A project in UNIGINE, just like a *Unity* project, is stored in its own folder, project settings are stored in the `*.project` file. There are various subfolders inside the project's folder, where your content and source files as well as various configuration files and binaries are stored. The most important are the **data** and **source** sub-folders.


In UNIGINE, each project has a `data` folder. Similar to a *Unity* project's `Assets` folder, this is where your project's assets are stored. To import assets into your project, simply drop files into your project's `data` directory and they will be automatically imported and appear in the [Asset Browser](../../editor2/assets_workflow/index.md#asset_browser). The assets in the editor will update automatically as you make changes to the files using an external program.


![](../../editor2/assets_workflow/file_system.png)

*Relationship between the contents of thedatafolder in your project's root on your computer, and the Project folder in the Asset Browser window*


### Supported File Types


*Unity* software supports a wide range of file formats, while UNIGINE supports [the most commonly used and some specific ones](../../editor2/assets_workflow/asset_types.md):


| Asset Types | Supported Formats |
|---|---|
| Geometry | .fbx, .obj, .3ds, .dae, .glb/.gltf, .stp/.step, .igs/.iges, .brep, .stl |
| Textures | .png, .jpeg, .tif, .tga, .rgba, .psd, .hdr, .dds, and more |
| Sound and Video | .wav, .mp3, .oga/.ogg, .ogv |
| Fonts | .ttf |


### Bringing Your Assets from Unity Software


> **Notice:** If you import a group of assets containing `.meta` description files (for example, from a *Unity* project), there might be warnings in the [Console](#editor_console) due to unsupported file format. Upon import completion, all contents in `.meta` files in the UNIGINE project folder will be replaced with UNIGINE native asset metadata. Source files will not be affected.


**Meshes**


You can import an asset you used in *Unity* software to UNIGINE if you have it as an FBX model. When importing the [FBX model](../../editor2/fbx/index.md) to UNIGINE, check the required [import options](../../editor2/fbx/index.md) depending on the model.


UNIGINE uses the same units (meters) as *Unity* software, so you don't need to rescale meshes.


**Materials**


Similar to *Unity* software, UNIGINE works with [PBR materials](../../content/materials/library/mesh_base/pbr.md) and supports both [Metalness and Specular workflows](../../content/materials/library/mesh_base/index.md#workflow) (similar to *Unity* materials based on the *Standard* and *Standard (Specular Setup)* shaders), a rich out-of-the-box library of materials enables to create almost any material. Similar to *Shader Graph* in *Unity* software you can use UNIGINE's [Material Graph Editor](../../content/materials/graph/index.md) to create your own materials visually simply by adding and connecting nodes and building a graph!  Materials created for your model in *Unity* software can be re-created in UNIGINE using [Material Graphs](../../content/materials/graph/index.md) or a sort of PBR uber-material called *[mesh_base](../../content/materials/library/mesh_base/index.md)* material.


When importing your models, UnigineEditor will try to automatically recreate materials for them along with the textures they use. This works good in majority of cases, however, sophisticated materials may have to be re-assembled using the [Material Graphs](../../content/materials/graph/index.md), but that won't take much time!


**Textures**


Textures can be imported as a part of a model or separately and then applied to a mesh. To [import textures](../../editor2/assets_workflow/texture_import.md), you might have to do some adjustments in advance. For example, the *[Shading](../../content/materials/library/mesh_base/index.md#texture_shading)* texture in UNIGINE stores the metalness, roughness, specular, and microfiber maps in its corresponding channels, so you need to modify the texture using third-party software, such as GIMP or Photoshop, and then import it to UNIGINE.


To import the *[Normal](../../content/materials/library/mesh_base/index.md#texture_normal)* texture, you should invert the G channel. This can be done while importing the texture (or even later) by using the *[Invert G Channel](../../editor2/assets_workflow/texture_import.md#invert_g)* setting.


**Animations**


You can import a bone-animated model you used in *Unity* software to UNIGINE if you have it as an FBX model. While importing the FBX model, enable the [Import Animations](../../editor2/fbx/index.md#options_animations_import) option and fine-tune the import using additional options.


For more details, see [import recommendations](../../editor2/assets_workflow/assets_create_import.md#import).


## Scene


The concept of the Scene in both engines is the same. However, *Unity* software and UNIGINE use different coordinate systems.


| Unity software | UNIGINE |
|---|---|
| ![Unity Coordinate System (left-handed)](unity_cs.png) *Unity* software uses a **left-handed** coordinate system where the vertical direction is usually represented by the **+Y** axis. One unit is one meter. **Axes and Directions:** - **X** � right (+), left (-) - **Y** � up (+), down (-) - **Z** � forwards (+), backwards (-) Positive rotation angle sets the rotation clockwise. File format: `*.scene` | ![UNIGINE Coordinate System (right-handed)](unigine_cs.png) UNIGINE uses a **right-handed** coordinate system where the vertical direction is usually represented by the **+Z** axis. One unit is one meter. **Axes and Directions:** - **X** � right (+), left (-) - **Y** � forwards (+), backwards (-) - **Z** � up (+), down (-) Positive rotation angle sets the rotation counterclockwise. File format: `*.world` |


### Scene Objects


This section gives a brief description of basic scene objects in both engines as well as their basic similarities and differences.


| Unity software | UNIGINE |
|---|---|
| ![](unity_hierarchy.png) *Hierarchy window* Basic scene object � **GameObject**. GameObjects are containers for all other Components. Components add functionality to the GameObject. Every GameObject has the *Transform* component by default. GameObjects can be organized into a hierarchy (parent-child relation). | ![](unigine_world_hierarchy.png) *World Nodes Hierarchy window* **Node** is a basic type from which all types of scene objects are inherited. Some of them appear visually: [Objects](../../objects/objects/index.md), [Decals](../../objects/decals/index.md), and [Effects](../../objects/effects/index.md) � they all have [surfaces](../../start/index.md#surface) to represent their geometry (mesh), while others ([Light Sources](../../objects/lights/index.md), [Players](../../objects/players/index.md), etc.) are invisible. Basic functionality of a node is determined by its type. Additional functionality can be added using [properties](../../principles/properties/index.md) and a [component system](../../principles/component_system/index.md). Each node has a transformation matrix, which encodes its position, rotation, and scale in the world. Nodes can be organized into a hierarchy (parent-child relation). > **Notice:** All scene objects added to the scene regardless of their type are called nodes. |


#### Prefabs


The workflow in *Unity* software is based on prefabs. It is usual for you to assemble a complex object from *GameObjects* with certain components and properties and create a prefab from such object. Prefabs can then be placed in your world via Editor, or instantiated at run time.


UNIGINE's workflow is based on [Node References](../../objects/nodes/reference/index.md) that are very similar to prefabs. In order to make a complex object to be [instanced](../../editor2/instancing_nodes/index.md) in your world, you just build the desired hierarchy from nodes, assign materials and properties to them, and save it as a *[Node Reference](../../objects/nodes/reference/index.md)*. Then you can use this *node reference* as many times as necessary and, just like with the prefabs, modify the *node reference* by changing any of its instances.


> **Notice:** Node References support nesting as well, so you can build complex hierarchies easily.


To learn more about creating Node References and managing them, please follow the link below:


- [Instancing Nodes](../../editor2/instancing_nodes/index.md)
- Video tutorial: [Instancing Nodes](../../videotutorials/essentials/instancing.md)


#### How to Collaborate?


*Unity* Editor provides the *Smart Merge* tool and support for custom tools for resolving conflicts when merging results of teamwork. Scenes and other files should use the YAML format in order to be merged.


In UNIGINE, all native file formats are text-based by default, so you can use [VCSIntegration Plugin](../../editor2/assets_workflow/version_control/vcs_plugin/index.md) that serves to simplify work with the version control system (SVN, Git) as well as any VCS you got used to and merge worlds, nodes, and other assets. You can extend the file system to keep the shared assets by using **[Mount Points](../../principles/filesystem/index_cpp.md#mount_points)**. Also, a normal workflow is to split work of different team members using separate *[Node Layers](../../objects/nodes/layer/index.md)*, so there will be no need to match the conflicted files when merging the project modifications.


Check out the following articles for more details:


- Configuring [Version Control](../../editor2/assets_workflow/version_control/index.md)
- [VCSIntegration Plugin](../../editor2/assets_workflow/version_control/vcs_plugin/index.md)


### Cameras


*Cameras*, the entities essential for rendering, are treated slightly differently in both engines.


In *Unity* software, *Camera* component is responsible for capturing a view and sending it to render. All enabled cameras present in the scene are rendered in the viewport (Game View) and may overlap each other. To switch between cameras, one usually needs to toggle off the current camera and enable the other one.


In UNIGINE, the *Camera* is a rendering-related object and implemented by the [Player](../../objects/players/index.md) nodes in the world. There are several player types with different behaviour provided in order to simplify creation of the most commonly used cameras controlled via the input devices (keyboard, mouse, joystick):


- **[Dummy](../../objects/players/dummy/index.md)** is a simple camera wrapper. You can use it for static cameras or enhance with custom logic.
- **[Spectator](../../objects/players/spectator/index.md)** is a free flying camera.
- **[Persecutor](../../objects/players/persecutor/index.md)** is a flying camera that has the target and orbits it at the specified distance. It is a ready-to-use simple solution for a third-person camera.
- **[Actor](../../objects/players/actor/index.md)** is a player that is capable of providing [physical interaction](../../migration/from_unity/physics.md#physics_players) with scenery. It has a rigid physical body, which is approximated with a capsule shape. It is a ready-to-use simple solution for a first-person character similar to *Unity* *Character Controller*.


Only one player can be rendered into the viewport at a moment. To switch between cameras in the Editor Viewport of the UnigineEditor, use the *Camera* panel:


![](../../editor2/camera_settings/open_camera_settings.png)


By checking the **[Main Player](../../objects/players/index.md#main_player)** flag of a player you set the default player, which will be rendered when the scene is loaded in the *[Play](#editor_game)* mode.


## Project Settings


Overall project settings adjustment in *Unity* Editor is usually done via the **Project Settings** window (menu: **Edit > Project Settings**). The Audio, Graphics, Physics, Quality levels and other settings affect the whole project.


In UNIGINE, the Common [Settings and Preferences](../../editor2/settings/index.md) are available via **Windows -> Settings** menu in the **Runtime** section. The **World** settings are set for each world separately.


### Shader Compilation


In *Unity* Editor, **Asynchronous Shader compilation** is toggled on and off in the Editor settings (menu: **Edit > Project Settings > Editor > Shader Compilation**).


In UNIGINE, a similar editor feature, **[Forced Shader Compilation](../../editor2/shaders_precompile/index.md)**, is available via both the toolbar and the *Editor* section of the *Settings* window.


![](../from_ue/unigine_shader_compilation.png)


### Presets


You use Presets in *Unity* Editor when you need to reuse property settings that have bearing to different tasks, be it component settings, import settings or especially *Project Settings*. You can save the settings preset for a certain section of the Project Settings as a `.preset` asset and reuse in development later.


![](unity_settings_presets.png)


Presets are an Editor-only feature in *Unity* software.


In UNIGINE, you can [save and load presets](../../editor2/settings/index.md#save_load_settings) for general physics, sound and render settings. The presets are stored as assets with the `*.physics`, `*.sound` and `*.render` extensions respectively. Use **Load** and **Save .* asset** buttons of the *Settings* window to work with presets of the corresponding settings section.


![](unigine_settings_presets.png)


Saved assets appear in the Asset Browser. You can load the render settings by double-clicking the required `.render` asset.


> **Notice:** By default, a UNIGINE project provides settings for *low, medium, high, ultra* and *virtual reality* quality presets stored in the `data/template_render_settings` folder.


![](unigine_render_presets.png)


Presets are not an Editor-only feature in UNIGINE. You can use *[Physics](../../api/library/physics/class.physics_cpp.md)*, *[Sound](../../api/library/engine/class.sound_cpp.md)* and *[Render](../../api/library/rendering/class.render_cpp.md)* classes to manage presets for corresponding settings, for example, to switch between quality levels at run time.


### Graphics


In *Unity* Editor, settings for graphics quality are mostly gathered in the following sections:


- The **Graphics** section contains global settings for graphics. The **Tier Settings** provide platform-specific adjustments to rendering and shader compilation. One of the three Tier levels to be applied is defined automatically based on the platform used.
- The **Quality** section handles levels of graphical quality defined for each platform.


In UNIGINE, the rendering settings of the world can be found in the **Render** section of the *Settings* window. You can also toggle on and off the most common render features by using the *Rendering* menu:


![](unigine_menu_render_features.png)


There is no platform-dependent quiality adjustments in UNIGINE, you should write your own logic to control the quality levels. You can use [Render Presets](#settings_presets) for this purpose.


Let's consider the most commonly used rendering settings in *Unity* software and their corresponding analogs in UNIGINE:


| Unity software | UNIGINE |
|---|---|
| HDR Mode | *Render -> Buffers ->*[**Color 16F**](../../editor2/settings/render_settings/buffers/index.md) |
| Rendering Path | [see below](#graphics_render_paths) |
| Shaders Preloading | [`shaders_preload`](../../code/console/index.md#shaders_preload) console command |
| Pixel Light Count | [Forward Per-Object Limits](../../editor2/settings/render_settings/lights/index.md#forward_limits) |
| Texture Quality | *Render -> Textures ->* **[Quality](../../editor2/settings/render_settings/textures/index.md)** |
| Anisotropic Textures | *Render -> Textures ->* **[Anisotropy](../../editor2/settings/render_settings/textures/index.md)** |
| Anti Aliasing | *Render -> Antialiasing ->* **[Supersampling](../../principles/render/antialiasing/supersampling.md)** |
| Soft Particles | *particles_base ->* **[Soft Interaction](../../content/materials/library/particles_base/index.md#soft_interaction)** |
| Realtime Reflection Probes | Menu: *Rendering -> Dynamic Reflections ->***Enabled** |
| Texture Streaming | *Render ->***[Streaming Settings](../../editor2/settings/render_settings/streaming/index.md)** |
| Shadows | *Render ->***[Shadows Settings](../../editor2/settings/render_settings/shadows/index.md)** |
| Shadow Cascades | set per each **[World Light](../../objects/lights/world/index.md#shadow_settings)** source |
| VSync Count | *Runtime -> Video* settings |


#### Rendering Paths


*Unity* software provides two non-legacy lighting and shading workflows: *Deferred* and *Forward* **Rendering Paths** defining the shading fidelity, as well as the rendering consumption and required hardware. You can choose the **rendering path** that your Project uses in the *Graphics* window, and you can override that path for each *Camera*.


UNIGINE has the fixed **[Rendering Sequence](../../principles/render/sequence/index.md)** represented by a combination of a full deferred renderer with forward rendering techniques:


- All [opaque](../../editor2/materials_settings/index.md#blending) (non-transparent) geometry is rendered in the deferred pass.
- [Transparent](../../editor2/materials_settings/index.md#blending) geometry is rendered in the forward pass.


You can reduce computational load by skipping certain rendering stages. Watch the dedicated video tutorial on using the *[Microprofile](../../tools/profiling/microprofile/index_cpp.md)* tool to optimize rendering:


- Video tutorial: [*Microprofile* for Artists](../../videotutorials/advanced/microprofile_for_artists.md)


#### Post-Processing


In *Unity* software, availability of post-processing effects is determined by the *render pipeline* used. In UNIGINE, similar effects are not a part of Post-processing but are integrated into the [Rendering Sequence](../../principles/render/sequence/index.md). Thus, *Unity* *High Definition Render Pipeline (HDRP)* is much closer to the rendering workflow in UNIGINE, than other render pipelines.


In *Unity* software the *Volume* framework is used to define the volumes where post-processing parameters and effects are locally (or globally) overridden. In UNIGINE you will have to write your own logic to smoothly interpolate between settings at different spaces (if such a requirement appears).


> **Notice:** UNIGINE offers a number of materials to create image [postprocessing effects](../../content/materials/library/postprocess/index.md) out of the box. They can be applied both globally and per camera.


This section lists all common *Unity* post-processing techniques that can be achieved in UNIGINE as well regardless of render pipeline.


##### Post-Processing Effects


| Unity software | UNIGINE |
|---|---|
| Anti-aliasing methods: - FXAA - TAA - SMAA - MSAA | [Anti-aliasing](../../principles/render/antialiasing/index.md) methods: - [Fast approximate anti-aliasing (FXAA)](../../principles/render/antialiasing/fxaa.md) - [Temporal anti-aliasing (TAA)](../../principles/render/antialiasing/taa.md). - [Subpixel Reconstruction Anti-Aliasing (SRAA)](../../principles/render/antialiasing/sraa.md). - [Supersampling](../../principles/render/antialiasing/supersampling.md). |
| Ambient Occlusion | [Screen-Space Ambient Occlusion](../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssao/index.md) |
| Auto Exposure | Camera Effects: - [Adaptive Exposure](../../editor2/settings/render_settings/camera_effects/index.md#exposure) - [White Balance](../../editor2/settings/render_settings/camera_effects/index.md#white_balance) - [Tone mapping](../../editor2/settings/render_settings/color/index.md#filmic) - [Bloom](../../editor2/settings/render_settings/camera_effects/index.md#bloom) - [Lens Dirt](../../editor2/settings/render_settings/camera_effects/index.md#lens_dirt) - [Chromatic Aberration](../../editor2/settings/render_settings/camera_effects/index.md#post_chromatic_aberration) - [Noise](../../editor2/settings/render_settings/camera_effects/index.md#post_noise) - [Vignette](../../editor2/settings/render_settings/camera_effects/index.md#post_vignette) |
| White Balance |  |
| Tonemapping |  |
| Bloom |  |
| Chromatic Aberration |  |
| Grain |  |
| Vignette |  |
| Color Grading: - Tone - Lookup Texture | - [Color Correction](../../editor2/settings/render_settings/color/index.md) - [Color Correction LUT](../../editor2/settings/render_settings/color/index.md#color_lut) |
| Deferred Fog | [Haze](../../editor2/settings/render_settings/environment/index.md#haze) |
| Depth of Field | [Depth of Field](../../editor2/settings/render_settings/camera_effects/index.md#dof) |
| Motion Blur | [Motion Blur](../../editor2/settings/render_settings/camera_effects/index.md#motion_blur) |
| Screen Space Reflection | [SSR](../../editor2/settings/render_settings/ssr/index.md) |
| Contact Shadows | [Screen Space Shadows](../../objects/lights/parameters/index.md#ss_shadow_settings) |
| Micro Shadows | [Cavity of SSAO](../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssao/index.md#ssao_cavity) |


## What's Next?


**Where to go from here?**


Make sure you don't miss the subtopics of this guide:


- **[Content Creation](../../migration/from_unity/content.md)**
- **[Programming](../../migration/from_unity/code.md)**
- **[Physics](../../migration/from_unity/physics.md)**


Thank you for reading the guide! You can proceed to the following sections for further learning:


- [Principles of Operation](../../principles/index.md)
- [Video Tutorials](../../videotutorials/index.md)
- [Programming Quick Start](../../start/quick_start/intro_cpp.md)
- [API](../../api/index.md)
