# Getting Started


This article covers UNIGINE-specific terminology and concepts and is highly recommended for all new users.


> **Notice:** Please consider [hardware requirements](../start/requirements.md).


## How Are Virtual Worlds Organized?


### Project


When you create an application in UNIGINE, it is represented by a [project](../sdk/projects/index_cpp.md). A **project** is a "container" for the application's [code](../code/index.md), [content](../content/index.md), and meta-data.


A project can consist of one or several complex 3D scenes, which are called [worlds](#world).


All projects are [managed](../start/workflow.md) via the [UNIGINE SDK browser](../sdk/index.md).


![](project_concept.png)


### World


A UNIGINE-based virtual [**world**](../editor2/worlds/index.md) is a 3D scene that contains a set of different scene graph [**nodes**](#node) (e.g. static meshes, lights, cameras, etc.) placed into specified positions, and global **settings** ([rendering](#rendering), [physics](#global_physics_settings), etc.) applied to the whole scene.


![](structure.png)


A scene graph in UNIGINE is a [multi-root tree](../principles/world_structure/index.md#nodes_hierarchy) (hierarchy) of nodes.


Each world is represented by an XML file with the `.world` extension.


When you create a new [project](#project) via the SDK Browser, a new world is also created with the same name as your project.


To edit your existing worlds and create new ones, use [UnigineEditor](#unigineeditor). You can create and use as many worlds as you need.


[![](world_editor.png)](world_editor.png)

*A world with nodes in it viewed in UnigineEditor*


### Node


In terms of UNIGINE, all objects added to the scene are called **nodes**. Nodes can be of different types, determining their visual representation and behavior.


There is a rich set of [built-in node types](../objects/index.md). Though the set covers almost all of required cases, it can be manually extended by the user.


You can also extend basic functionality of any node by adding [**components**](../principles/component_system/index.md) to it.


Every node has a [transformation matrix](../code/fundamentals/matrix_transformations/index_cpp.md), which encodes position, rotation, and scale of the node in the world.


There are node types that appear visually: [Objects](../objects/objects/index.md), [Decals](../objects/decals/index.md), and [Effects](../objects/effects/index.md). Other node types ([Light Sources](../objects/lights/index.md), [Players](../objects/players/index.md), etc.) are invisible.


Node parameters are regularly stored in the `.world` file, but also can be saved into a separate XML file with the `.node` extension (and later be referenced from the `.world` file via the special nodes called [Node References](../objects/nodes/reference/index.md), which is used for [node instancing](../editor2/instancing_nodes/index.md)).


#### Object


One of the most important node types is [Object](../objects/objects/index.md). Objects represent imitations of entities existing in the real world: objects (people, trees, cars, planes, etc.), sky, terrains, water, and so on. Objects have a single [surface](#surface) or a set of surfaces defining their visual appearance. They can have a [shape](#shape) to represent the volume they occupy in 3D space and a [body](#body) to participate in physical interactions.


### Mesh


A **mesh** is a collection of polygons defining object's geometry. It has the following properties:


- Each mesh has one or several [surfaces](#surface).
- Maximum number of polygons per surface is **2,147,483,647** ([ObjectMeshStatic](../objects/objects/mesh/index.md), [ObjectMeshSkinned](../objects/objects/mesh_skinned_legacy/index.md)) or **65,535** ([ObjectMeshDynamic](../objects/objects/mesh_dynamic/index.md)).
- There are 2 UV channels for texturing.
- Mesh supports vertex colors.


Animation in UNIGINE can be performed by [skinned meshes](../objects/objects/mesh_skinned_legacy/index.md) (bone-based), [morph targets](../content/tutorials/morph/index_cpp.md) (keyframe) or [dynamic meshes](../objects/objects/mesh_dynamic/index.md) (code-controlled).


At run time, meshes are stored in proprietary UNIGINE [formats](../code/formats/file_formats.md) with `.mesh` (static mesh + optional animation data) and `.anim` (external animation data) extensions.


![](mesh_asset_browser.jpg)


When [importing an FBX model](../editor2/fbx/index.md) to the Engine, it is automatically converted to the `.mesh` format.


> **Notice:** If you want parts of your object to have different materials (e.g. transparent / opaque, shiny metal / human skin), you should split your mesh into surfaces. However, if you want parts of your geometry to move separately (e.g. spinning wheels of a car), you would need several separate meshes.


### Surface


A **surface** is a named non-overlapping subset of the object geometry (i.e. object mesh). Each surface can have its own [material](#materials) or [property](#properties) assigned. It is also possible to enable/disable surfaces independently from each other.


Surfaces can be organized in a [hierarchy](../principles/world_structure/index.md#surfaces_hierarchy) within a mesh (it can be used for [LOD](#lod) switching).


At the picture below, a soldier 3D mesh consists of 4 surfaces: eyes, skin, bags (body armor, radio set, bag), and body (overalls, shoes, hard hat, gloves).


![](surfaces.jpg)


### Material


In terms of UNIGINE, a [**material**](../editor2/materials_settings/index.md) is a rule defining how the surface will look like: its interaction with lights, reflection parameters, etc. It is based on:


- Vertex, fragment and geometry **shaders** that actually draw the material based on different conditions.
- User-defined **textures** passed to shaders.
- **States** that specify conditions, based on which the appropriate shaders will be applied.
- **Parameters** defining how shaders will be used.


![](materials.png)


UNIGINE provides a rich set of [**built-in base materials**](../content/materials/index.md) out of the box. The recommended way is to inherit a new user material from a base one and tweak it. However, a custom material can be created as well:

- Using the [**Material Editor**](#material_editor) for graph materials: by assembling and configuring the required blocks in the visual editor.
- Using [**Abstract Materials**](../code/materials_shaders/abstract_materials/index.md) for custom base materials: by inheriting a base material from an existing abstract prototype (or your own custom prototype) and adding the desired functions to it.


You can also create a custom shader via UnigineEditor and then implement the required logic using UUSL API ([Unified UNIGINE Shader Language](../code/uusl/index.md)). If you prefer, you can use HLSL for custom shaders creation, but in this case you will have to manually migrate them with every SDK release.


In addition to regular materials applied to certain surfaces, there is a special type of materials called [**post materials**](../content/materials/library/postprocess/index.md), that are applied above the final screen composition (e.g. to create a night or thermal vision effect). You can also create your own post-effects using the [**Scriptable Materials**](../content/materials/scriptable.md) workflow.


![](post_sensors.jpg)


#### Material Hierarchy


Materials are organized in [hierarchy](../content/materials/inheritance.md) with parameters inheritance and overloading (much like in object-oriented programming). When a material is inherited, all its parameters are inherited from the parent. If a parameter value is changed for the parent, it will be automatically changed for the child as well, unless it was overridden (set to a different value) for the child before that.


Example: a material A has two parameters (color: blue and specular power of 1.4), a material B is inherited from the material A and has color parameter overridden (red). If we change specular power to 2.0 in the material A, then the material B will have the following parameters: red color (overridden) and 2.0 value of specular power (inherited).


By using parameter inheritance it is very convenient to mass control values of multiple materials parameters.


![](hierarchy.jpg)


#### Material Editor


UNIGINE provides the node-based [Material Editor](../content/materials/graph/index.md) that enables creating custom materials without writing code. You simply connect nodes to build an easy-to-read graph: use basic pre-configured nodes (200+ are available) or create custom ones.


[![](material_editor_sm.png)](material_editor.png)


Also the Material Editor allows:

- Creating custom base materials (`.mgraph`) that can be directly assigned to objects or used as parent materials to avoid reassembling the whole graph repeatedly.
- Creating custom graph nodes using [subgraphs](../content/materials/graph/index.md#subgraphs) or your [custom code](../content/materials/graph/index.md#custom_code).
- Switching between material types (*Mesh Opaque PBR*, *Mesh Alpha Test PBR*, *Mesh Transparent PBR*, *Mesh Transparent Unlit*, *Decal PBR* types are available).
- Toggling performance-affecting features on and off.
- Constructing the final material's UI.
- Using textures from the Asset Browser or a file manager. The textures will be automatically imported with the corresponding nodes added to the graph.
- Writing code in a special [Function](../content/materials/graph/index.md#custom_code) node, if necessary.


The key features of the Material Editor include the following:

- [**Loops**](../content/materials/graph/index.md#loops) that allow repeating an arbitrary sequence of actions multiple times. UNIGINE provides the implementation of graph loops that is almost on par with loops in code and much easier to use.
- [**Portals**](../content/materials/graph/index.md#node_portal) that help keeping visual clarity even for complex or large graphs, avoiding situations when your connection wires are all over the place criss-crossing each other.
- [**Subgraphs**](../content/materials/graph/index.md#subgraphs) - custom nodes combining reusable parts of node graphs, that can be used in other material graphs. If you change anything in the subgraph, changes will apply to every material using it.
- **Connectors** - a special "collapsed" mode of a graph node: it occupies less space and can be attached right to an input of another graph node.
- **Expressions** - special nodes that enable writing simple arithmetic operations and use the UNIGINE Graphics API. They can be used as a swizzle in combination with the ability to change the number or order of data components.


You can [reparent](../content/materials/graph/materials_reparent/index.md) a material inherited from a built-in base material so that it is derived from a graph-based material. Or even [convert](../content/materials/graph/materials_reparent/index.md#unique_graph) it to a unique graph material.


### Property


A [**property**](../principles/properties/index.md) is a "material" for application logic. It specifies the way the object will behave and interact with other objects and the scene environment. Properties can have parameters of various types � from a simple *integer* representing your character's hit points, to *node, material, file* (for textures, meshes, sounds, etc.), or *property*, which simplifies access to various resources.


![](../code/fundamentals/file_access/assign_prop_params.gif)


Properties can be used to build [**components**](../principles/component_system/index.md) to extend the functionality of nodes.


Properties, like materials, are organized in a [hierarchy](../principles/properties/inheritance.md) with parameter inheritance. But, unlike materials, they can be applied either *per-surface* or *per-node*.


## How to Add Content to the Virtual World?


Every piece of content, that can be used in your world or project, is an **asset**. An asset may come from a file created using a third-party application, such as a 3D model, an audio file, an image, or any other type supported by the UNIGINE Engine.


The main front-end tool of the Asset System is the [**Asset Browser**](../editor2/assets_workflow/index.md#asset_browser) in [UnigineEditor](#unigineeditor). It is used to organize content in your project: create, import, view, rename your assets, move them between the folders and manage their hierarchy.


Each time an asset is [created or imported](../editor2/assets_workflow/assets_create_import.md), [UnigineEditor](../editor2/index.md) does all necessary job, including conversion of your assets (be it a JPG texture or and FBX model) to its native format (such as `.texture` textures, `.mesh` geometry, `.anim` animations, etc.) to be used by the Engine at run time. Such files, generated as a result of conversion, are called "**run-time files**", and they are updated by UnigineEditor each time you modify the corresponding asset.


It is recommended that you familiarize yourself with the [Assets Workflow](../editor2/assets_workflow/index.md) to learn all the details.


### UnigineEditor


[**UnigineEditor**](../editor2/index.md) allows you to assemble a virtual world: import and set nodes, assign materials and properties to them, setup lighting, adjust [global settings](../editor2/settings/index.md) (physics, rendering, etc.) and more. It features *What You See Is What You Get* approach: you can instantly see the scene with final quality (as at run time).


![](editor.jpg)


The UnigineEditor functionality can be extended by using the UnigineEditor's [Plugin System](../editor2/extensions/index.md#plugin_system).


Watch the tutorial below to learn how to import 3D models to UNIGINE:


## How Do We See the Virtual World?


For visual representation, UNIGINE uses a standard [perspective projection](../editor2/camera_settings/index.md#projection). The orthogonal projection is also available.


![](frustum.png)

*Perspective projection*


In UNIGINE, the way how the world is seen is based on the 3 entities:


- A [**camera**](../api/library/rendering/class.camera_cpp.md) is a structure containing 2 matrices: view and projection. Through this structure, you set the camera parameters: field of view, [masks](#bit_masking), near and far clipping planes, and [post materials](../content/materials/library/postprocess/index.md). Then, the camera is passed to a [Viewport](#viewport) that will render an image from this camera. The camera is assigned to a [Player](#player), that will further control its position.
- A [**viewport**](../api/library/rendering/class.viewport_cpp.md) receives a camera and renders an image from it on the screen. In addition, it provides all functions of the main renderer, for example, cube maps rendering, stereo rendering, panoramic rendering and so on.
- A [**player**](../api/library/players/index.md) is a node controlled via the input devices (keyboard, mouse, joystick). It has a [camera](#camera) assigned. Once a player has changed its position, its internal camera's view matrix will be changed as well. UNIGINE features several types of players: [Player Dummy](../objects/players/dummy/index.md), [Player Actor](../objects/players/actor/index.md), [Player Persecutor](../objects/players/persecutor/index.md) and [Player Spectator](../objects/players/spectator/index.md).


> **Notice:** The terms discussed above refer only to the API. The [Camera panel](../editor2/camera_settings/index.md) in UnigineEditor manages *cameras*, which in terms of API would be called *players*.


### Lighting


Lighting in your worlds is created by placing **Light Sources**. These nodes contain parameters, which determine various light characteristics, such as brightness, color, etc. You can also use physically-based parameters, like color temperature and illuminance, to set up your lights.


![](lighting.png)


There are different kinds of lights and they emit light in different ways. A light bulb, for example, emits light in all directions � in UNIGINE it is represented by the [**omni light**](../objects/lights/omni/index.md). A projector or car headlights emit a cone of light in a certain direction � [**projected light**](../objects/lights/proj/index.md). Light beams that come from the sun appear to be parallel, as their source is located so far away. To simulate this type of lighting in UNIGINE, the [**world light**](../objects/lights/world/index.md) is used.


To learn more about lighting in UNIGINE, see the [Lighting Video Tutorial](../videotutorials/essentials/lights.md).


### Rendering


UNIGINE has a combination of full deferred renderer with forward rendering techniques:


- All opaque (non-transparent) geometry is rendered in the [deferred pass](../principles/render/sequence/index.md#opaque_deferred).
- Transparent geometry is rendered in the [forward pass](../principles/render/sequence/index.md#transparent).


To learn more about the applied rendering techniques, see the [Rendering Sequence](../principles/render/sequence/index.md) article.


In *UnigineEditor* all rendering settings (such as global illumination, shadows, environment, anti-aliasing, post-effects, etc.) can be adjusted via the [*Rendering Settings*](../editor2/settings/render_settings/index.md) section and saved to a `*.render` file to be used later. Each new project contains settings for *low, medium, high*, and *ultra* quality presets as well as settings optimized for best performance in VR. You can now simply double-click on any of them in the *Asset Browser* to apply corresponding settings.


![](render_settings.png)


## How Do We Hear Sounds?


Next to the visual component, sound is a very important domain of real-time technologies. It is the key resource for creating the proper feeling of immersion in the virtual world. For example, rolling echo cues us to anticipate a scene to take place in a lofty dome. Soft tapping of a stone hit by an incautious foot or a car whooshing by with lightning speed � all that can be modelled aurally. UNIGINE offers a multi-channel sound system with support for binaural HRTF-based sound, various 3D effects, sound occlusion and multiple [reverberation zones](../objects/sounds/sound_reverb.md). You can assign any *MP3, WAV*, or *OGA* sound to be played by contact of the objects simulating their [physical properties](#physics) on the level of sound. For the moving sources, like a car, the [Doppler](../objects/sounds/sound_source.md#doppler) effect is applied so that the movement of the sound source relative to the listener is authentically imitated.


![](sound_system.png)


All sound settings can be adjusted via the [*Sound Settings*](../editor2/settings/sound_global/index.md) section in *UnigineEditor*. You can also save your presets to `*.sound` files to be used later.


## How Is Physical Behavior Defined?


UNIGINE features a built-in simplified game-like Newton [physics](../principles/physics/index.md). The use cases for physics properties (where physics is more preferable than hard-coding objects animation) are the following:


- [Collision detection](#collisions) (preventing moving through walls)
- Simulating perfectly elastic collisions (redistribution of kinetic energy)
- Simulation of simple mechanisms by rigid [bodies](#body) and destructible [joints](#joint)
- Simulation of basic physical phenomena: gravity, friction, buoyancy
- Procedural destruction of meshes
- Simulation of [cloth](../principles/physics/bodies/cloth/index.md) and [ropes](../principles/physics/bodies/rope/index.md) movement


> **Notice:** It is important to understand that the built-in physics module is very generic and works within the specific range of parameters: for precise simulation of mission-critical tasks (i.e. flight dynamics) it is highly recommended to use specialized solutions. As in any game-like physics, **you should not use real masses and extremely high velocity values**.


Physics is simulated with [its own update FPS](../code/fundamentals/execution_sequence/index.md#framerates) and is in effect within the [physics simulation distance](../editor2/settings/physics_global/index.md#physics_distance). Physical properties can be applied to the [objects](../objects/objects/index.md) only.


### Body


To assign some physical properties to an object, so that it could participate in interactions between objects or external physical forces, it should have a [**body**](../principles/physics/bodies/index.md). There are several types of bodies: *[Rigid](../principles/physics/bodies/rigid/index.md), [Rag Doll](../principles/physics/bodies/ragdoll/index.md), [Fracture](../principles/physics/bodies/fracture/index.md), [Rope](../principles/physics/bodies/rope/index.md), [Cloth](../principles/physics/bodies/cloth/index.md), [Water](../principles/physics/bodies/water/index.md), [Path](../principles/physics/bodies/path/index.md)*.


Almost like in the real world, virtual physics of the body follows the [concepts](../principles/physics/bodies/index.md#rigid_bodies_dynamics) of velocity, force, mass, density and so on.


![](body.png)


### Shape


While a [body](#body) simulates various types of physical behavior, a **shape** represents the volume (sphere, capsule, cylinder, box, convex hull) that a rigid [body](#body) occupies in space. A physically simulated object usually has a single body and one or several shapes which allow objects to [collide](#collisions) with each other.


> **Notice:** The maximum number of collision shapes for one body is limited to 32768.


#### Collision Detection


A [**collision detection**](../principles/physics/collision/index.md) algorithm detects contact points between [shapes](#shape) and prevents them from penetrating each other. Contact points and normals are accessible via API.


### Joint


[**Joints**](../principles/physics/joints/index.md) are used to connect several objects with respect to the mass balance and represent constraints removing certain degrees of freedom. There are different types of joints: *[Fixed](../principles/physics/joints/index.md#fixed), [Hinge](../principles/physics/joints/index.md#hinge), [Ball](../principles/physics/joints/index.md#ball), [Prismatic](../principles/physics/joints/index.md#prismatic), [Cylindrical](../principles/physics/joints/index.md#cylindrical), [Wheel](../principles/physics/joints/index.md#wheel)*.


![](joints.png)


### Global Physics Settings


There are [global physics settings](#global_physics_settings) (gravity, penetration factor, etc.) affecting all physical objects present in the world.


## How to Control the Virtual World?


### Programming Languages


To implement your project's logic in UNIGINE, you can use the following programming languages:


- [C#](../code/csharp/index.md) for a good balance between speed and ease of use. It allows using [C# Component System](../principles/component_system/component_system_cs/index.md) enabled by default and integrated into the UnigineEditor. It is the easiest way to implement your application logic in components and assign them to any node to be executed.
- [C++](../code/cpp/index.md) for maximum performance and seamless integration with the existing code base.
- [UnigineScript](../code/uniginescript/index.md), fast iterative scripting language featuring instant compilation and thousands of useful functions.


> **Notice:** All `*.usc` and `*.h` files inside of the data folder are scripts in UnigineScript language (they do not require compilation).


All the [APIs are unified](../api/index.md): every class, method, and constant are accessible via any API. However, there are minor language-specific differences.


To learn more, see the following usage examples articles:


- [UnigineScript API, C++ API and C# API usage examples](../code/usage/index.md)
- [Examples of UnigineScript extension using C++ API](../code/cpp/usage/index.md)
- [Examples of UnigineScript extension using C# API](../code/csharp/usage/index.md)


#### Mixing Languages


You can stick to a single language: C++ if maximum performance is a key factor, or C# for optimum balance. In case of *C# (.NET)*, UNIGINE provides the [C# Component System](../principles/component_system/component_system_cs/index.md) integrated into UnigineEditor. This approach is deemed to be the most convenient and ensuring good performance for complex applications with elaborate logic.


Alternatively, you can have different programming languages (C++, C#, and UnigineScript) for different pieces of your project: for example, you can use C++ for base classes and performance consuming operations; and implement some simple application logic in UnigineScript. You can also call methods from one API when using another, and manually expand API functionality.


### Run-Time Logic


Every UNIGINE-based application has its life cycle, that consists of certain stages, some of them are performed once, others are repeated each frame. In short, these stages are as follows:


![](engine_cycle.png)


UNIGINE has three **main logic components**, Each of them has a set of functions (named *init()*, *update()*, *postUpdate()*, etc.) that contain actions to be performed at corresponding stages of the Engine's working cycle. These components are:


- [**System Logic**](../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic) is the code that is run during the whole application life cycle (its scope exists even when switching between worlds).

  - For applications written using UnigineScript, the system logic is written to the [system script](../code/fundamentals/execution_sequence/app_logic_system.md#system_script) file (`unigine.usc`).
  - For applications that use C++ `AppSystemLogic.cpp` is created, and for C# applications � `AppSystemLogic.cs`. This file is stored in the `source/` folder of your project. It has [implemented methods](../api/library/common/logic/class.systemlogic_cpp.md) to put your logic code inside.
- [**World Logic**](../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic) is the logic of the [virtual world](#world). The logic takes effect only when the world is loaded.

  - For applications written using UnigineScript, the world logic is written to the [world script](../code/fundamentals/execution_sequence/app_logic_system.md#world_script) file (`*.usc` named after your project) and is loaded and unloaded together with the corresponding world.
  - For applications that use C++ `AppWorldLogic.cpp` is created, and for C# applications � `AppWorldLogic.cs`. This file is stored in the `source/` folder of your project and stays loaded during the whole engine runtime. It has [implemented methods](../api/library/common/logic/class.worldlogic_cpp.md) to put your logic code inside.
- [**Editor Logic**](../code/fundamentals/execution_sequence/app_logic_system.md#editorlogic). This component is to be used in case you need to implement your own Editor. It has more implemented methods providing you with clear understanding of the current Engine events (a node has been created, a property has been deleted, a material has been changed, etc.).


It is highly recommended that you familiarize yourself with the [execution sequence](../code/fundamentals/execution_sequence/index.md) to know the details, including the multi-threaded mode.


#### Component System


**Component System** enables you to implement your application's logic via a set of building blocks � **components**, and assign these blocks to [nodes](#node) extending their basic functionality. You can add a component to a node via code or via UnigineEditor.


![](../code/fundamentals/file_access/assign_prop_params.gif)


Each component's logic is implemented inside the following functions: *init(), update(), postUpdate()*, etc. Just like for the [main logic components](#main_logic_components), these functions are executed at corresponding stages of the Engine's [working cycle](../code/fundamentals/execution_sequence/code_update.md).


The logic of a certain component is active only when the corresponding node and property are enabled. Thus, you can enable/disable logic of each particular component at run time, when necessary.


You can assign several properties corresponding to different components to a single node. The order in which the logic of components is executed can be changed at run time to fit your needs, giving you an exceptional flexibility and freedom to implement any functionality you have in mind.


In UNIGINE, there are two implementations of the Component System:


- [C# Component System](../principles/component_system/component_system_cs/index.md) available for C# projects. In this case, a logic component integrates a node and a C# class, containing logic implementation (actions to be performed), defining a set of additional parameters to be used.
- [C++ Component System](../principles/component_system/component_system_cpp/index.md) available for C++ projects. In this case, a logic component integrates a node, a C++ class, containing logic implementation (actions to be performed), and a property, defining a set of additional parameters to be used.


### Intersection Detection


UNIGINE features a fast [**intersection** detection](../code/usage/intersections/index_cpp.md) algorithm. It can be used for ray-casting, calculating line of sight (LOS) or height above terrain (HOT), etc.


Intersections can also be found between the node's bounding volume and another bounding volume of the specified size.


### Samples and Demos


UNIGINE provides a rich set of [built-in samples](../sdk/api_samples/index.md) and [demo projects](../sdk/demos/index.md) covering the basic principles of working with the Engine (operations with built-in nodes, output rendering, GUI setting, etc.).


There are different samples for each of the three [programming languages](#languages). All samples come with the full source code. To check them out, click the **[Samples](../sdk/api_samples/index.md)** tab in SDK Browser.


![](../sdk/api_samples/cpp/index.jpg)


The **[Demos](../sdk/demos/index.md)** tab provides access to a set of demos that demonstrate various features available in UNIGINE and use cases where these features can be applied.


![](../sdk/demos/index.png)


An extended set of [**art samples**](../content/samples/index.md) available on the *Demos* tab illustrates various aspects of working with content: you can learn how to use [UNIGINE's built-in objects](../objects/index.md) with different settings, set up [LODs](../principles/world_management/index.md#lods) and [materials](../content/materials/index.md), adjust [rendering settings](../editor2/settings/render_settings/index.md), or work with [vegetation](../content/materials/library/mesh_base/index.md#option_vegetation).


## How to Optimize Your Project's Performance?


UNIGINE offers a wide range of various optimizations to ensure that your application runs at its best and fastest. But in order to enable them, you should do your part of the job: follow recommendations when preparing and setting up your project's content, e.g., use [LODs](#lod), [bit masking](#bit_masking), and other techniques.


### LODs


Smooth alpha-blended levels of details (LODs) are used to decrease geometry complexity of 3D objects, when these objects move away from the camera, making it possible to lighten the load on the renderer.


Usually, LODs are used for:


- Switching high-polygonal [surfaces](#surface) of the mesh to low-polygonal ones.
- Switching [surfaces](#surface) with complex materials to surfaces with simplified optimized ones.
- Switching several high-polygonal [surfaces](#surface) to a single simplified surface.
- Switching one [node](#node) type to the other (for example, switching a high-polygonal mesh to a billboard, a two-polygonal object that always faces the camera).


Switching between LODs can depend not only on the distance from the camera, but also on the distance from the certain object.


UNIGINE offers two mechanisms of [**LODs**](../principles/world_management/index.md#lods) switching:


- Disable one LOD and enable another at the specified [distance](../principles/world_management/index.md#visible) defined by two values: maximum visibility distance of the first LOD (**Max Visibility**) and minimum visibility distance of the second LOD (**Min Visibility**). ![](lods_switch.png)
- Smoothly [fade](../principles/world_management/index.md#fading) one LOD into another at the specified interval defined by two values: minimum fade distance of the first LOD (**Min Fade**) and maximum fade distance of the first LOD/minimum fade distance of the second LOD (**Max Fade**). ![](lods_fade.png)


See the [Setting up object LODs article](../content/optimization/geometry/lods/index.md) for the details.


### Bit Masking


Bit masking defines whether two entities affect each other or not. It can be used to:


- [Render](../principles/bit_masking/index.md#viewport) some objects to the viewport and not to render others.
- [Apply collision](../principles/bit_masking/index.md#collision_mask) to some bodies and not to apply to others.
- [Render shadows](../principles/bit_masking/index.md#shadow_mask) for some objects and not to render for others.
- [Apply physics interaction](../principles/bit_masking/index.md#physical_mask) for some objects and ignore others.


The [**bit masking**](../principles/bit_masking/index.md) algorithm compares 32-bit masks of each of two nodes using binary operator **and**. If masks match, one object will influence another object; if they don't, the objects won't interact.


If two masks have **at least one matching bit**, the masks match. E.g. the following two masks match, as they have **4** matching bits:


![](masks_match.png)


You can learn more about content optimization by watching the following tutorial:


Now you are prepared to start your experience with UNIGINE. Enjoy!
