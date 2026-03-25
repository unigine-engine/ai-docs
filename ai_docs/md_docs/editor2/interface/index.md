# Interface Overview


**UnigineEditor** provides the core functionality for creation and editing of virtual worlds for UNIGINE-based applications. It allows you to easily view and modify virtual worlds by adding, transforming and editing the [nodes](../../start/index.md#node).


The main window of the UnigineEditor is made up of tabbed windows which can be easily rearranged, grouped, detached and docked.


You can [customize UI layout](../../editor2/interface/customize/index.md) to fit your preferences or a specific type of work.


The default layout (shown below) gives you access to the most commonly used windows.


[![](interface_sm.jpg)](interface.jpg)

*Main window of the Editor*


## Menu Bar


| ![](menu_bar.png) | A *Menu bar* provides access to general panels and commands that are used when creating virtual worlds. It has a batch of options that allows you to: - [Manage worlds](../../editor2/worlds/index.md) - Manage existing objects - [Create new objects](../../objects/index.md) - [Open windows and tools](#windows) - Select Rendering mode |
|---|---|


## Toolbar


[![](tools_panel.png)](tools_panel.png)


The Toolbar provides access to the most frequently used working features:


- placement tools available in the *Object Mode*;
- toggles that enable you to control animation, sound playback, and [physics](../../principles/physics/index.md) simulation;
- and the rightmost elements that enable you to access [light baking](../../editor2/lighting/gi/index.md#light_baking) and control [shader compilation](../../editor2/shaders_precompile/index.md).


> **Notice:** In projects using .NET API, the Toolbar has additional controls for [running applications](../../principles/component_system/component_system_cs/index.md#run).


On the left side, there is the mode switching button. It switches between the following modes:


| Object Mode | Enables basic tools for [selection and positioning](../../editor2/select_position_nodes/index.md) of objects on the scene (**Shift+1** hotkey). |
|---|---|
| Texture Paint Mode | Opens [Texture Editor](../../editor2/texture_editor/index.md) to edit and paint textures (**Shift+2** hotkey). |
| Landscape Paint Mode | Opens [Brush Editor](../../editor2/brush_editor/index.md) to edit *[Landscape Layer Map](../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md)* (**Shift+3** hotkey). |
| Clutter Mask Paint Mode | Opens [Mask Editor](../../editor2/mask_editor/index.md) for creating and editing mask images for *[Grass](../../objects/objects/grass/index.md), [Mesh Clutter](../../objects/objects/mesh_clutter/index.md)* or *[World Clutter](../../objects/worlds/world_clutter/index.md)* (**Shift+4** hotkey). |
| Cluster Paint Mode | Opens [Cluster Editor](../../editor2/cluster_editor/index.md) to edit *[Mesh Cluster](../../objects/objects/mesh_cluster/index.md)* objects (**Shift+5** hotkey). |
| Terrain Global Paint Mode | Opens [Brush Editor](../../editor2/terrain_editor/index.md) to edit [*Terrain Global*](../../objects/objects/terrain/terrain_global/index.md) (**Shift+6** hotkey). |


## Viewports


![](viewport_scene.jpg)


**Editor** viewport allows you to visually navigate and edit your virtual world. The number of *Editor* viewports that can be opened simultaneously is not limited. Parameters of each editor viewport can be adjusted separately. The window includes the following panels:


- *Camera Panel* that allows you to switch between cameras, add new cameras to the current world, open the *Camera Settings* window or lock the current camera
- *Helpers Panel* provides quick access to frequently used [helpers](../../editor2/using_visual_helpers/index.md) (ViewCube, FPS Counter, etc.)
- *Rendering Debug Panel* that enables fast visual debugging by displaying the contents of rendering buffers
- *Navigation Panel* that lets you quickly change camera speed and position.


**Engine** viewport is designed for application debugging and profiling - it renders the image from the Engine Camera.


### Fullscreen Viewport


You can maximize your viewport in the Editor with a keyboard shortcut using ***F11***. Pressing ***F11*** the second time will return the viewport to its original size and place.


![](viewport_maximize_new.gif)


## Main Windows


### Asset Browser


| ![](asset_browser.png) | [*Asset Browser*](../../editor2/assets_workflow/index.md#asset_browser) is a tool that is used to organize content in your project. The [Assets System](../../editor2/assets_workflow/index.md) keeps all links and dependencies between the resources when you edit, rename or move them within the project. It allows you to: - Create and import assets. - Organize yor assets: rename, move them between the folders and manage their hierarchy. - View assets and add them directly to the scene. |
|---|---|
| ![](asset_browser_windows.png) | To facilitate managing assets, you can create multiple Asset Browser windows via the menu bar: ***Windows -> Add Asset Browser*** and stack them anywhere. Each of the created windows is also listed in the *Windows* menu and can be hidden or removed, if required. Click on the lock sign ![](lock_sign.png) in the upper right corner of each Asset Browser window to prevent automatic switching of the [thumbnail view](../../editor2/assets_workflow/index.md#thumbnail_view) (the right side of the Asset Browser window) if an asset in another folder is selected. |


### World Hierarchy


| ![](world_hierarchy.png) | *World Nodes* window is a convenient tool for working with the hierarchy of [nodes](../../start/index.md#node) present in the scene. It allows you to: - Organize nodes into a hierarchy - Find a node by its name an quickly navigate to its location - Perform basic operations with the selected nodes (clone, remove, export, etc.) |
|---|---|


### Materials Hierarchy


| ![](materials_hierarchy.png) | *Materials* window serves for organizing and modifying UNIGINE [materials](../../content/materials/index.md). It allows you to: - Get instant access to built-in UNIGINE materials - Inherit materials and modify them - Organize materials into a hierarchy - Perform basic operations with the selected materials (clone, remove, etc.) |
|---|---|


Learn more about [materials hierarchy management](../../editor2/materials_settings/organizing_materials/index.md#materials_hierarchy).


### Properties Hierarchy


| ![](properties_hierarchy.png) | *Properties* window is used to modify and organize nodes properties (sets of custom options). It allows you to: - Organize properties into a hierarchy - Perform basic operations with the selected properties (clone, remove, etc.) - Enable property-specific options |
|---|---|


### Parameters


| ![](parameters.png) | A multi-purpose *Parameters* window allows you to modify parameters of any element selected in the *World Nodes, Materials*, or *Properties* window, as well as in the [*Asset Browser*](../../editor2/assets_workflow/index.md#asset_browser). It offers the following features: - Quick access to all parameters of the selected object - Simultaneous editing of multiple selected objects of the same type - Copying and pasting of [transformation parameters](../../editor2/node_parameters/transformation_common/index.md#transformation_params) and [surface parameters](../../editor2/node_parameters/visual_representation/index.md#copy_paste) by using the context menu |
|---|---|


## Search


[Search](../../editor2/search/index.md) in UnigineEditor is available in the *Propertes, Materials* and *World Nodes* hierarchy tabs, as well as in the *Parameters* and *Settings* tabs, various drop-downs and context menus. The search is limited to items within the currently active tab or menu.


![](search_in_editor.gif)


The search field in drop-down and context menus is displayed if the menu contains at least 5 items.


## Video Tutorial: Interface Overview
