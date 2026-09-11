# Migrating to UNIGINE from Unreal Engine


This section gives a brief overview of UNIGINE from an *Unreal Engine* user's perspective and provides basic information to help you transfer your *Unreal Engine* experience to UNIGINE.


> **Notice:** Please consider [hardware requirements](../../start/requirements.md) first.


## Quick Glossary


This chapter matches common *Unreal Engine* terms on the left and their UNIGINE equivalents (or rough equivalent) on the right. UNIGINE keywords are linked directly to related articles to provide you with more in-depth information.


| Category | Unreal Engine | UNIGINE |
|---|---|---|
| **Editor UI** | World Outliner | [World Nodes](../../editor2/interface/index.md#world_hierarchy) Hierarchy window |
| Details Panel | [Parameters window](../../editor2/interface/index.md#parameters) |  |
| Content Browser | [Asset Browser window](../../editor2/assets_workflow/index.md#asset_browser) |  |
| Viewport | [Editor Viewport](../../editor2/interface/index.md#viewports) |  |
| **Scene** | Level | [World](../../principles/world_structure/index.md) |
| **Gameplay Types** | Actor, Pawn | [Node](../../objects/nodes/index.md) |
| Blueprint Class | [NodeReference](../../objects/nodes/reference/index.md) + [Component System](../../principles/component_system/index.md) |  |
| **Meshes** | Static Mesh | [Static Mesh](../../objects/objects/mesh/index.md), [Dynamic Mesh](../../objects/objects/mesh_dynamic/index.md) |
| Skeletal Mesh | [Skinned Mesh](../../objects/objects/mesh_skinned_legacy/index.md) |  |
| **Effects** | Effect, Particle, Cascade | [Particle System](../../objects/effects/particles/index.md) |
| **Game UI** | UMG (Unreal Motion Graphics) | [GUI](../../objects/objects/gui/index.md) |
| **Materials** | Material, Material Editor | [Base Material](../../content/materials/index.md#base_materials) |
| Material Instance | [User Material](../../content/materials/index.md#user_materials) |  |
| **Programming** | C++ | [C++](../../code/cpp/index.md) / [C#](../../code/csharp/index.md) |
| Blueprint | [UnigineScript](../../code/uniginescript/index.md) |  |
| **Physics** | Line Trace | [getIntersection](../../code/usage/intersections/index_cpp.md) |
| Primitive Component | [Rigid Body](../../principles/physics/bodies/rigid/index.md) |  |
| Collision | [Shape](../../principles/physics/shapes/index.md) |  |
| Physics Constraint | [Joint](../../principles/physics/joints/index.md) |  |
| **Animation** | Sequencer | [Tracker](../../editor2/tools/tracker/index.md) |


## Project and SDK Management


As an *Unreal Engine* user, you are accustomed to use **Epic Games Launcher** � the application that streamlines the way you find, download and manage your projects and installations. In addition to it, you can manage your projects directly via *Unreal Editor*: create a new project and switch between the existing ones.


**[UNIGINE SDK Browser](../../sdk/index.md)** is the first step to start working with UNIGINE Engine. This application incorporates all project-related tasks and enables you to manage your projects and installed SDKs, as well as gives you access to the samples and the knowledge base.


[![Epic Games Launcher and UNIGINE SDK Browser Comparison (click to enlarge)](unreal_unigine_sdk.png)](unreal_unigine_sdk.png)

*Epic Games Launcher and UNIGINE SDK Browser Comparison*


UNIGINE provides several [programming workflows](../../code/fundamentals/programming_overview/index.md), to easily adapt your programming experience in *Unreal Engine* it is recommended for you to use the [C++ Component System](../../migration/from_ue/code.md). [Creating a project](../../sdk/projects/index_cpp.md#creation) using this workflow in SDK Browser is done as follows:


1. Click *Create Project* on the *C++ Empty* template card in the *Templates* tab. ![](../../sdk/projects/create_project_cpp.png) > **Notice:** If you want to make a project compatible with one of the supported VR headsets, use the **VR C++** template instead. This will enable required plugins, add template assets and components (more about [VR-compatibility](../../vr_development/vr_template/index.md)).
2. Choose **C++ (Visual Studio 2022)** project type in the *API + IDE* field.
3. Click *Create New Project*.
4. Once the new project is created, it will appear in the *My Projects* tab. Click ***Open Editor*** to open it in UnigineEditor; click **Open Code IDE** to open the project's source code via the default IDE.


> **Notice:** UNIGINE Editor instances run per project. You will have to launch another instance of UNIGINE Editor for another project.


## Editor Interface


Below you can see interfaces of the *Unreal Editor* and *UnigineEditor*. Interface elements in the images are color-coded to indicate common functionality. Each element has a label to show UNIGINE's equivalent. The layout of UnigineEditor is fully [customizable](../../editor2/interface/customize/index.md) by resizing, dragging and dropping the tabbed windows.


[![Unreal and UNIGINE Editor UI Comparison (click to enlarge)](unreal_unigine_editor.png)](unreal_unigine_editor.png)

*Unreal and UNIGINE Editor UI Comparison*


To learn more about the UnigineEditor interface, read [this article](../../editor2/interface/index.md).


### Viewports


*Unreal Editor Viewports* and *Editor Viewports* in UnigineEditor are very much alike. You can use as [many *Editor* Viewports](../../editor2/camera_settings/index.md#camera_viewport) as you need.


By default, an *Editor* Viewport renders its own *Editor Camera* view, and you can switch to another [camera](#scene_players) present in the scene and control it the same way as you pilot a **CameraActor** in UE.


Navigation inside Editor Viewports is pretty much the same as in UE Viewports. However, get familiar with [Scene Navigation](../../editor2/navigation/index.md) so as not to miss details.


| ![](ue_viewport.png) | ![](unigine_editor_viewport.png) |
|---|---|
| *Unreal Editor Viewport* | *UNIGINE Editor Viewport* |
| ![](unigine_editor_viewport_2.png) |  |


You can use:


- **Camera panel** to switch between [cameras](#scene_players) and configure the current one.
- **Rendering Debug** to display the contents of rendering buffers the same way as using the *Buffer Visualization Mode* in UE4.
- **Navigation panel** to quickly set up and switch between camera speed presets and change the camera position.
- **ViewCube** to switch between the *perspective*/*orthographic* projections and control orientation of the camera.


Also, a set of switchers is available globally in the top toolbar:


![](unigine_toolbar.png)


- **[Helpers](../../editor2/using_visual_helpers/index.md)** panel provides quick access to auxiliary visualizers, such as icons, *gizmos* and wireframes.
- **Precompile All Shaders** toggle is used for [Forced Shaders Compilation](../../editor2/shaders_precompile/index.md)
- **[Animation](../../objects/objects/mesh_skinned_legacy/index.md)** toggle
- **[Physics](../../principles/physics/index.md)** toggle
- **[Audio](../../objects/sounds/index.md)** toggle


### Playing and Simulating


You are accustomed that *Unreal Editor* has the *Play In Editor (PIE)* mode launching the game in the current Viewport and being representative of your final build. You can also play in other modes and use the *Simulate In Editor (SIE)* mode to preview blueprints logic, animation and physics simulation.


![](ue_play_controls.png)


In UNIGINE, you can enable animation and [physics](../../principles/physics/index.md) simulation using the [toggles](#toolbar_toggles) in the top toolbar. You can open the *Engine* viewport (menu: *Windows -> Engine Viewport*) where you can pilot the current **[Main Player](#scene_players)**.


To check application logic you will need to run an instance of the current compiled binary of the application via any of the following ways:


- [Via SDK Browser](../../sdk/projects/index_cpp.md#run) by clicking **Run**: ![](../../sdk/projects/run_level.png) You can also [run the application with custom settings](../../sdk/projects/index_cpp.md#custom_run) by clicking an ellipsis under the *Run* button (e.g. choose the Debug binaries).
- By using the corresponding **launcher** created by default in the project folder:

  - ![](../../sdk/projects/file.png) `launch_debug` � the launcher of the project's debug version.
  - ![](../../sdk/projects/file.png) `launch_release` � the launcher of the project's release version.
- By running the project directly from the IDE used.


By default, the mouse cursor is grabbed when clicked at run time, providing camera movement control, press **Esc** to free the cursor. There are two ways to setup default Input Bindings (key states and the mouse behaviour):


- In the [Controls](../../editor2/settings/controls/index.md) settings of the Editor.
- Via [code](../../start/quick_start/pqr/index_cpp.md#inputs).


### Output Log


As well as UE4, UNIGINE has the [Console](../../code/console/index.md) used for standard input, output and error logging. A set of [console commands](../../code/console/index.md#meta) is provided.


It is available both in UnigineEditor and a running application. To open the Console window in the Editor, go to *Windows -> Console* menu:


![](unigine_console.png)


A built-in console is called by pressing the **F1** key:


![](../../code/console/console_sm.jpg)


You can use it to [print user messages from code](../../start/quick_start/pqr/index_cpp.md#logging).


### Packing a Final Build for Publishing


In *Unreal Engine*, you got used to building your projects via the Editor. In UNIGINE, [packing a final build](../../editor2/projects/build_project.md) is also done via UnigineEditor.


## Projects and Files


### Directories and Files


A project in UNIGINE, just like a UE project, is stored in its own folder, project settings are stored in the `*.project` file. There are various subfolders inside the project's folder, where your content and source files as well as various configuration files and binaries are stored. The most important are the `data` and `source` sub-folders.


In UNIGINE, each project has a `data` folder. Similar to a UE project's `Content` folder, this is where your project's assets are stored. To import assets into your project, simply drop files into your project's `data` directory and they will be automatically imported and appear in the [Asset Browser](../../editor2/assets_workflow/index.md#asset_browser). The assets in the editor will update automatically as you make changes to the files using an external program.


![](../../editor2/assets_workflow/file_system.png)

*Relationship between the contents of thedatafolder in your project's root on your computer, and the Project folder in the Asset Browser window*


The `core` folder contains the built-in core assets. These assets are read-only and available for every project by default.


### Supported File Types


UNIGINE, like UE, supports the [most commonly used file types and some specific ones](../../editor2/assets_workflow/asset_types.md):


| Asset Types | Supported Formats |
|---|---|
| Geometry | .fbx, .obj, .3ds, .dae, .glb/.gltf, .stp/.step, .igs/.iges, .brep, .stl |
| Textures | .png, .jpeg, .tif, .tga, .rgba, .psd, .hdr, .dds, and more |
| Sound and Video | .wav, .mp3, .oga/.ogg, .ogv |
| Fonts | .ttf |


### Bringing Your Assets from Unreal Engine


*Unreal Engine* assets (`.uasset`) are not supported for import by UNIGINE. Use the source content files you have used in your UE projects or export assets in one of formats supported by UNIGINE.


**Meshes**


You can import assets you used in UE to UNIGINE: export your mesh as an FBX model and [import it](../../editor2/fbx/index.md) to UNIGINE checking the required import options depending on the model.


> **Notice:** Make note that the primary unit of measurement is one meter in UNIGINE, while UE4 operates on centimeters. It's recommended to scale down the geometry by 100 times by setting the geometry **Scale** multiplier to 0.01 value when importing.


**Materials**


Similar to other engines, UNIGINE works with [PBR materials](../../content/materials/library/mesh_base/pbr.md). Moreover, UNIGINE supports both [Metalness and Specular workflows](../../content/materials/library/mesh_base/index.md#workflow) and has a rich out-of-the-box library of materials that can be used to create almost any material. Therefore, materials created for the model in UE can be re-created in UNIGINE using [mesh_base](../../content/materials/library/mesh_base/index.md) material, the base material in UNIGINE used for physically based materials.


**Textures**


Textures can be imported as a part of a model or separately and then applied to a mesh. To [import textures](../../editor2/assets_workflow/texture_import.md), you might have to do some adjustments in advance. For example, the *[Shading](../../content/materials/library/mesh_base/index.md#texture_shading)* texture in UNIGINE stores the metalness, roughness, specular, and microfiber maps in its corresponding channels (RGBA), so you need to modify the texture using third-party software, such as GIMP or Photoshop, and then import it to UNIGINE.


*[Normal](../../content/materials/library/mesh_base/index.md#texture_normal)* texture used in UE is compatible with UNIGINE, therefore you can import your normal textures to UNIGINE without any changes.


**Animations**


If you want to import a bone-animated model, export it from UE as an FBX file and enable the *[Import Animations](../../editor2/fbx/index.md#options_animations_import)* option during the import to UNIGINE. You will also have additional options to finetune the import.


For more details, see [import recommendations](../../editor2/assets_workflow/assets_create_import.md#import).


## Levels


The concept of 3D scene in both engines is the same. However, *Unreal Engine* and UNIGINE use different coordinate systems.


| Unreal Engine | UNIGINE |
|---|---|
| ![Unreal Engine Coordinate System (left-handed)](ue_cs.png) Separate 3D scenes are called **Levels** (also referred to as *Maps*). UE uses a **left-handed** coordinate system where the vertical direction is usually represented by the **+Z** axis. **Axes and Directions:** - **X** � forwards (+), backwards (-) - **Y** � right (+), left (-) - **Z** � up (+), down (-) Positive rotation angle sets the rotation clockwise. File format: `*.umap` | ![UNIGINE Coordinate System (right-handed)](unigine_cs.png) Separate 3D scenes are called **Worlds**. UNIGINE uses a **right-handed** coordinate system where the vertical direction is usually represented by the **+Z** axis. **Axes and Directions:** - **X** � right (+), left (-) - **Y** � forwards (+), backwards (-) - **Z** � up (+), down (-) Positive rotation angle sets the rotation counterclockwise. File format: `*.world` |


To change the **starting map** of your project in UE4, you open *Project Settings -> Maps & Modes* and specify the default map for game and editor. In UNIGINE you specify the **Default World** of the project when creating a build (*File -> Create Build*). As for UnigineEditor and development builds, you can override the default world explicitly by [running the project or the editor with custom settings](../../sdk/projects/index_cpp.md#custom_run):


1. In SDK Browser, click an ellipsis under the **Run** or **Open Editor** button;
2. In the Customize Run Options form that opens, specify the following [startup command-line option](../../code/command_line.md) in the *Arguments* field: ```bash -console_command "world_load your_world_name" ```


### Scene Objects


This section gives a brief description of basic scene objects in both engines as well as their basic similarities and differences.


| Unreal Engine | UNIGINE |
|---|---|
| ![](ue_hierarchy.png) *World Outliner* Basic scene object � **Actor**. It is the base object that can be placed in or spawned into the world. Actors can be organized into a hierarchy (parent-child relation). *Actor* is a container for *Components* that define its functionality. The Actor's position, rotation and scale are stored in a *Scene Component*. Usually *Actors*have a root component, which can be any subclass of *Scene Component*, by default. Programmers can inherit from the default *UActorComponent* to create a custom component using C++ or *Blueprint Script*. | ![](unigine_world_hierarchy.png) *World Hierarchy window* **Node** is a basic type from which all types of scene objects are inherited. Some of them appear visually: [Objects](../../objects/objects/index.md), [Decals](../../objects/decals/index.md), and [Effects](../../objects/effects/index.md) � they all have [surfaces](../../start/index.md#surface) to represent their geometry (mesh), while others ([Light Sources](../../objects/lights/index.md), [Players](../../objects/players/index.md), etc.) are invisible. Nodes can be organized into a hierarchy (parent-child relation). Basic functionality of a node is determined by its type. Additional functionality can be added using [properties](../../principles/properties/index.md) and the [component system](../../principles/component_system/component_system_cpp/index.md). Each node has a transformation matrix, which encodes its position, rotation, and scale in the world. > **Notice:** All scene objects added to the scene regardless of their type are called nodes. |


#### Blueprint Classes


The workflow in UE is based on *Blueprint Classes*. It is usual for you to build a complex object (*Actor*) from components, select it, and click the *Blueprint / Add Script* button (in the Details panel). Then you choose a place to save your *Blueprint Class* and click *Create Blueprint* to save your new *Blueprint Class*.


In UNIGINE, you [build the desired hierarchy](../../editor2/organizing_nodes/index.md) from nodes of different types, assign the required materials and properties to them. You can use [Dummy](../../objects/nodes/dummy/index.md) nodes to group multiple nodes.


In order to make a complex object to be [instanced](../../editor2/instancing_nodes/index.md) in your world, you save the node or the hierarchy of nodes as a [Node Reference](../../objects/nodes/reference/index.md), which can be instantiated and [edited](../../editor2/instancing_nodes/index.md#edit) in the Editor or at run time afterwards as many times as necessary.


![](../../editor2/instancing_nodes/drag_hierarchy.gif)


To learn more about creating *Node References* and managing them please follow the link below:


- [Instancing Nodes](../../editor2/instancing_nodes/index.md).
- Video tutorial: [Instancing Nodes](../../videotutorials/essentials/instancing.md)


#### How to Collaborate?


*Unreal Editor* provides the *Source Control* feature out of the box. Also, its Multi-User Editing workflow is built on a server-client model, supporting a number of sessions inside a shared environment for collaborative work.


In UNIGINE, all native file formats are text-based by default, so you can use any VCS you are used to and merge worlds, nodes and other assets. You can extend the file system to keep the shared assets by using **[Mount Points](../../principles/filesystem/index_cpp.md#mount_points)**. Also, a normal workflow is to split work of different team members using separate *[Node Layers](../../objects/nodes/layer/index.md)*, so there will be no need to match the conflicted files when merging the project modifications.


Check out the related article for more details:


- Configuring [Version Control](../../editor2/assets_workflow/version_control/index.md)


### Cameras


*Cameras*, the entities essential for rendering, are treated slightly differently in both engines.


In UE4, the *CameraComponent* is responsible for capturing a view and sending it to render. You usually set a *Pawn* actor with a *CameraComponent* attached as a default character by specifying it in a *GameMode* settings.


In UNIGINE, the *Camera* is a rendering-related object and implemented by the *[Player](../../objects/players/index.md)* nodes in the world. There are several player types with different behaviour provided in order to simplify creation of the most commonly used cameras controlled via the input devices (keyboard, mouse, joystick):


- **[Dummy](../../objects/players/dummy/index.md)** is a simple camera wrapper. You can use it for static cameras or enhance with custom logic.
- **[Spectator](../../objects/players/spectator/index.md)** is a free flying camera.
- **[Persecutor](../../objects/players/persecutor/index.md)** is a flying camera that has the target and orbits it at the specified distance. It is a ready-to-use simple solution for a third-person camera.
- **[Actor](../../objects/players/actor/index.md)** is a player that is capable of providing physical interaction with scenery. It has a rigid physical body, which is approximated with a capsule shape. It is a ready-to-use simple solution for a first-person character.


Only one *player* can be rendered into the viewport at a moment. To switch between cameras in the *Editor* Viewport of the UnigineEditor, use the *Camera* panel:


![](../../editor2/camera_settings/open_camera_settings.png)


By checking the **[Main Player](../../objects/players/index.md#main_player)** flag of a player you set the default player, which will be rendered in the Editor's *Engine* viewport and on world startup when running the application.


## Project Settings


Overall project settings adjustment in *Unreal Editor* is usually done via the **Project Settings** window. The Audio, Rendering, Physics, Input levels and other settings affect the whole project. Also, the **World Settings** panel provides settings for the current Level.


In UNIGINE, the Common [Settings and Preferences](../../editor2/settings/index.md) are available via **Windows -> Settings** menu at the **Runtime** section. The **World** settings are set for each world separately.


### Saved Configurations


You use *Export* and *Import* buttons in the project settings of the *Unreal Editor* to save the values of the settings to an external configuration file (`.ini`) and load them when necessary.


![](ue_settings_config.png)


In UNIGINE, you can [save and load](../../editor2/settings/index.md#save_load_settings) general physics, sound and render settings the same way. The presets are stored as assets with the `*.physics`, `*.sound` and `*.render` extensions respectively. Use **Load** and **Save .* asset** buttons of the *Settings* window to work with presets of the corresponding settings section.


![](unigine_settings_presets.png)


Saved assets appear in the Asset Browser. You can load the render settings by double-clicking the required `.render` asset.


> **Notice:** By default, a UNIGINE project provides settings for *low, medium, high, ultra* and *virtual reality* quality presets stored in the `data/template_render_settings` folder.


![](unigine_render_presets.png)


Presets are not an Editor-only feature in UNIGINE. You can use *[Physics](../../api/library/physics/class.physics_cpp.md)*, *[Sound](../../api/library/engine/class.sound_cpp.md)* and *[Render](../../api/library/rendering/class.render_cpp.md)* classes to manage presets for corresponding settings, for example, to switch between quality levels at run time.


### Graphics


In UE4, settings for graphics quality are mostly gathered in the *Engine - Rendering* section.


In UNIGINE, the [rendering settings](../../editor2/settings/render_settings/index.md) of the world can be found in the **Render** section of the *Settings* window. You can also toggle on and off the most common render features by using the *Rendering* menu:


![](unigine_menu_render_features.png)


There is no platform-dependent quiality adjustments in UNIGINE, you should write your own logic to control the quality levels. You can use [Render Presets](#settings_presets) for this purpose.


#### Deferred and Forward Shading


By default, *Unreal Engine* uses a **Deferred Renderer**. You can switch to **Forward Shading Renderer**, which would provide better performance in some cases, in the *Project Setting -> Rendering* section.


UNIGINE has the fixed **[Rendering Sequence](../../principles/render/sequence/index.md)** represented by a combination of a full deferred renderer with forward rendering techniques:


- All [opaque](../../editor2/materials_settings/index.md#blending) (non-transparent) geometry is rendered in the deferred pass.
- [Transparent](../../editor2/materials_settings/index.md#blending) geometry is rendered in the forward pass.


You can reduce computational load by skipping certain rendering stages. Watch the dedicated video tutorial on using the *[Microprofile](../../tools/profiling/microprofile/index_cpp.md)* tool to optimize rendering:


- Video tutorial: [*Microprofile* for Artists](../../videotutorials/advanced/microprofile_for_artists.md)


#### Post Processing


*Unreal Engine* uses *PostProcessVolume* to define the volumes where post-processing parameters and effects are locally (or globally) overridden, parameters are blended using linear interpolation. In UNIGINE, you will have to write your own logic to smoothly interpolate between settings at different spaces (if such a requirement appears).


This section lists all common UE4 post-processing techniques that can be achieved in UNIGINE as well.


| Unreal Engine | UNIGINE |
|---|---|
| Anti-aliasing methods: - FXAA - MSAA - TAA | [Anti-aliasing](../../principles/render/antialiasing/index.md) methods: - [Fast approximate anti-aliasing (FXAA)](../../principles/render/antialiasing/fxaa.md) - [Temporal anti-aliasing (TAA)](../../principles/render/antialiasing/taa.md). - [Subpixel Reconstruction Anti-Aliasing (SRAA)](../../principles/render/antialiasing/sraa.md). - [Supersampling](../../principles/render/antialiasing/supersampling.md). |
| Eye Adaptation (Auto-Exposure) | Camera Effects: - [Adaptive Exposure](../../editor2/settings/render_settings/camera_effects/index.md#exposure) - [Bloom](../../editor2/settings/render_settings/camera_effects/index.md#bloom) - [Tone mapping](../../editor2/settings/render_settings/color/index.md#filmic) - [White Balance](../../editor2/settings/render_settings/camera_effects/index.md#white_balance) - [Lens Dirt](../../editor2/settings/render_settings/camera_effects/index.md#lens_dirt) - [Lens Flares](../../objects/lights/parameters/index.md#lens_flares_settings) |
| Bloom |  |
| Filmic Tonemapper |  |
| White Balance |  |
| Dirt Mask |  |
| Lens Flare |  |
| Color Grading LUT (Lookup Texture) | - [Color Correction](../../editor2/settings/render_settings/color/index.md) - [Color Correction LUT](../../editor2/settings/render_settings/color/index.md#color_lut) |
| Depth of Field | [Depth of Field](../../editor2/settings/render_settings/camera_effects/index.md#dof) |
| Post Process Materials | [Postprocess Materials](../../content/materials/library/postprocess/index.md) |
| Chromatic Aberration | The *post_color_correction*[postprocess material](../../content/materials/library/postprocess/index.md) |
| Film Grain |  |
| Screen Space Reflections | [SSR](../../editor2/settings/render_settings/ssr/index.md) |
| Screen-Space Ambient Occlusion | [Screen-Space Ambient Occlusion](../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssao/index.md) |
| Screen Space Global Illumination | [SSRTGI](../../editor2/settings/render_settings/global_illumination/index.md) |
| Contact Shadows | [Screen Space Shadows](../../objects/lights/parameters/index.md#ss_shadow_settings) |
| Motion Blur | [Motion Blur](../../editor2/settings/render_settings/camera_effects/index.md#motion_blur) |
| Screen Percentage | [Supersampling](../../principles/render/antialiasing/supersampling.md) |


## What's Next?


**Where to go from here?**


Make sure you don't miss the subtopics of this guide:


- **[Content Creation](../../migration/from_ue/content.md)**
- **[Programming](../../migration/from_ue/code.md)**
- **[Physics](../../migration/from_ue/physics.md)**


Thank you for reading the guide! You can proceed to the following sections for further learning:


- [Principles of Operation](../../principles/index.md)
- [Video Tutorials](../../videotutorials/index.md)
- [Programming Quick Start](../../start/quick_start/intro_cpp.md)
- [API](../../api/index.md)
