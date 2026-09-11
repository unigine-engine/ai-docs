# Virtual World Structure


A UNIGINE-based virtual **world** is a scene that contains a set of different built-in objects with certain properties assigned to them. Almost all objects are visible in the virtual world. However, some of them are pseudo-objects, which cannot be seen in a normal mode (such as [physicals](../../objects/effects/physicals/index.md), [occluders](../../objects/worlds/world_occluders/index.md), and so on).


In general, a world includes:


- [Built-in objects](#objects) called **nodes**, which may refer to other nodes (`*.node`), meshes ([`*.mesh`](../../code/formats/file_formats.md)), audio files ([`*.oga`](../../objects/sounds/index.md)), paths (`*.path`), or scripts ([`*.h`](../../api/library/worlds/class.worldexpression_cpp.md)) > **Notice:** A world can store both nodes themselves and/or [references](../../objects/nodes/reference/index.md) to nodes stored in external `*.node` files. A `*.node` file can also store both nodes and references to other external `*.node` files.
- [Materials](#materials) and [properties](#properties)
- Shaders and textures to which materials refer
- General rendering, physics, sound and game settings


A new world can be created via the Menu bar of [UnigineEditor](../../editor2/worlds/index.md#create_world) or via [UNIGINE SDK Browser](../../sdk/projects/index_cpp.md#creation) when creating a new project.


Each world is stored on the disk in a separate file in the XML format with the `.world` extension. The world content is generated and managed via UnigineEditor.


You can also generate and manage content via [world logic](../../code/fundamentals/execution_sequence/app_logic_system.md#world_script): UnigineScript file (`*.usc`) for projects that use UnigineScript only, `AppWorldLogic.cpp` for C++ applications, or `AppWorldLogic.cs` for C# applications.


![](world_struct.png)

*Relationship between the main components of the world*


Worlds can be as large as a level designer wishes, because UNIGINE supports data streaming, and required resources � meshes, textures, animations, sounds � are dynamically loaded at run time. Resources that are no longer needed are unloaded from memory.


> **Notice:** Coordinates of objects in a world are stored as *floats*, therefore accuracy of the float data type may be insufficient. However, visual artifacts are noticeable for small objects starting from the distance of 50 thousand units.
>  For common outdoor scenes, we recommend you to use the scale *1 unit = 1 meter*, when you export objects from 3D modeling software.


To make the large-world designing and editing process easier, you can split your world into several parts.


## Coordinate System


UNIGINE uses the right-handed Cartesian coordinate system: **X** and **Y** axes form a horizontal plane, **Z** axis points up. When exporting animation from 3D editors, **Y** is considered a forward direction.


![](coordinates.gif)

*Coordinate system*


Positive rotation angle sets rotation counterclockwise. The right-hand rule applies: if you set the right hand thumb along the axis, other fingers wrapped will show the rotation direction.


![](coordinates_rotation.gif)

*Rotation directions*


## Built-in Objects


UNIGINE provides a set of [built-in objects](../../objects/index.md) that allow adding to a world practically all objects existing in real life. For convenience, they are divided into several groups according to the type of operation.


> **Notice:** In terms of UNIGINE, all objects added into a scene are called [**nodes**](../../objects/nodes/node/index.md). They are listed in the [*World Nodes*](../../editor2/interface/index.md#world_hierarchy) hierarchy window of [UnigineEditor](../../editor2/index.md).


A world can store both nodes themselves and/or [references](../../objects/nodes/reference/index.md) to nodes stored in external files with the `.node` extension.

> **Notice:** No matter how a node is stored � in a world or in an external file, it consists of the same entities.

 A node can refer to a mesh (`*.mesh`), an audio file (`*.oga`), or a path (`*.path`) depending on the node type.
Nodes of [object-related types](../../api/library/objects/index.md) may have **surfaces** and physical [bodies](../../principles/physics/bodies/index.md) (including collision [shapes](../../principles/physics/shapes/index.md) connected using [joints](../../principles/physics/joints/index.md)). Surfaces contain references to particular materials and properties. Such references are created automatically when you assign a material or a property to a surface.

> **Notice:** A single surface can have a reference only to one material and one property.


A **surface** serves as an atomic rendering unit and can represent:


- A part of the object that has its own separate [material](#materials).
- Different [levels of details (LODs)](../../principles/world_management/index.md#lods) (including reflection LODs and shadow LODs). In this case surfaces represent the same object or its part in a more and a less detailed variants (a high-polygonal and a low-polygonal model). Which of these surfaces is visible is determined by the surface properties.


Each surface can also have several morph targets (blend shapes).


Taking into account the information given above, [the scheme of the world components](#world_struct) can be extended as follows:


[![](virtual_world_structure.png)](virtual_world_structure.png)

*Interaction between the main components of the world*


### Nodes Hierarchy


All nodes are organized into a [hierarchy](../../editor2/organizing_nodes/index.md). Each node can have multiple children.


![](nodes_hierarchy.png)

*Nodes hierarchy list in theWorld Nodeshierarchy window*


Usually coordinates and orientation of the first-level nodes are set in the *global (world)* coordinate system, while coordinates and orientation of their child nodes are in *local* coordinate systems of their parents (if not chosen [otherwise](../../editor2/select_position_nodes/index.md#pivot_point)). So you can transform and rotate the whole hierarchy tree branch only by transforming and rotating its root node.


The origin of the *global (world)* coordinate system is located at *the scene center*. The origin of the local coordinate system is at *the pivot point* of the parent node.


### Surfaces


As mentioned above, nodes of object-related types can have surfaces. By default, such a node added via UnigineEditor has **one** surface.


![Surfaces](node_surfaces.png)

*Surfaces*


The *number* of surfaces depends on how a mesh was [imported](../../editor2/fbx/index.md) into UNIGINE and cannot be changed dynamically at run time. However, you can reimport it via [UnigineEditor](../../editor2/index.md), if necessary. Each surface may add a separate DIP call to the GPU.


> **Notice:** Identical surfaces of identical meshes with the same material are automatically instanced and drawn in one DIP call.


Surfaces also participate in [culling](../../principles/world_management/index.md#occlusion_culling) of invisible parts of the object when the object is hidden behind other objects. Moreover, surfaces are used to calculate collision detection with [physically simulated objects](#physical_objects).


> **Notice:** It is strongly recommended to keep the number of surfaces in exported art assets as **low** as reasonably possible to reduce the amount of computations.


Nodes share common options for their surfaces. Each surface can be **enabled** or **disabled** for rendering, as needed. Surfaces cannot be added, deleted, or otherwise altered in UnigineEditor. The reason is that surfaces are formed during the object creation in an external 3D editor. To change them, you should re-import the object.


You can assign a separate [**material**](../../principles/world_structure/index.md#materials) and [**property**](../../principles/world_structure/index.md#properties) to each surface.


Surfaces often represent [LODs](../../principles/world_management/index.md#lods) of the same object.  For more details about [Min parent](../../principles/world_management/index.md#parents), [Max parent](../../principles/world_management/index.md#parents), [Visibility](../../principles/world_management/index.md#visible) and [Fade](../../principles/world_management/index.md#fading) distance parameters, see [Levels of details](../../principles/world_management/index.md#lods).


## Physical Simulation of Objects


Objects can either be just non-interactive environment or take part in [physical simulation](../../principles/physics/index.md). The built-in engine physics is a very rough approximation of the real world that is designed to be effective and at the same time keep the overall framerate high. Its main aim is to [detect collisions](../../principles/physics/collision/index.md) between the objects.


To participate in collisions, an object should have a [body](../../principles/physics/bodies/index.md) that describes how it can behave and what physical properties it possesses. For example, an object with a [rigid body](../../principles/physics/bodies/rigid/index.md) always stays solid and undeformed, and an object with a [cloth](../../principles/physics/bodies/cloth/index.md) body can be folded and torn.


However, the body is not enough for an object to start interacting. Its volume should be approximated using some kind of a physical primitive (or a set of them) � a *shape*. UNIGINE provides several types of such primitives: [box](../../principles/physics/shapes/index.md#box), [sphere](../../principles/physics/shapes/index.md#sphere), [capsule](../../principles/physics/shapes/index.md#capsule), [cylinder](../../principles/physics/shapes/index.md#cylinder), [convex hull](../../principles/physics/shapes/index.md#convex), or an arbitrary mesh shape. The shape is used to compute collisions between objects.


Two shapes can be connected with one of the [joints](../../principles/physics/joints/index.md): fixed, ball, hinge, prismatic, cylindrical, wheel or suspension. Joints define how two shapes can move relative to each other.


## Materials


Nodes without materials are rendered red in the scene. The **material** stores information on how a node is to be rendered; it is in fact a set of properties (states, options, parameters) and assets (2D, 3D textures), based on which surfaces are rendered. The material should be assigned to the node surface.


| ![](no_material.jpg) | ![](mesh_base_applied.jpg) |
|---|---|
| *Material ball with no material assigned* | *Material ball with themesh_basematerial assigned* |


Even if no material is assigned to the node surfaces, the node can still participate in collisions and intersections.


To manage rendering of surfaces with no materials assigned, use the [viewport mask](../../principles/bit_masking/index.md#viewport) for these surfaces.


In UNIGINE, there are two types of materials:


- Read-only **base materials** created by programmers and stored in `*.basemat` files. A UNIGINE-based project includes a set of default base materials.
- Editable **user materials** inherited from the base materials or from other user materials and stored in `*.mat` files. Such materials are created by 3D artists and override properties of parent materials.


A set of base material properties may include:


- **[Options](../../code/formats/materials_formats/ulon_materials/options.md)**. The set of options is pre-defined and invariable for all materials. Each option either enables or disables some kind of behavior. Option values for base materials are hard-coded.
- **[States](../../code/formats/materials_formats/ulon_materials/states.md)**. Conditions based on which UNIGINE selects appropriate shaders, textures, and parameters. For example, one can define a state that turns on and off rendering of foam in water simulation and provide different shaders for both states (with and without foam).
- **[Textures](../../code/formats/materials_formats/ulon_materials/textures.md)**. Usually, the base material has several textures defined. The common reasons for that are the following:

  - A shader may need more than one texture for processing.
  - Different textures can be used in different [rendering passes](../../principles/render/sequence/index.md).
  - States may influence the number of textures, for example, each state may require its own texture.
- **[Parameters](../../code/formats/materials_formats/ulon_materials/parameters.md)**. The values passed as arguments to relevant shaders.
- **[Shaders](../../code/formats/materials_formats/ulon_materials/shaders.md)**. The programs that actually draw the material based on different conditions. > **Notice:** Only base materials can refer to shaders. Each base material is usually equipped with several shaders, and the appropriate one is chosen according to the current rendering pass and state.


A set of user material properties cannot differ from the base material ones: the user material inherited from the base material only overrides all its options, states, textures and parameters.


> **Notice:** The user material cannot refer to a shader � it can only override properties sent to shaders used by the base material from which the user material is inherited.


UNIGINE allows creating **manual materials**. These materials are created and edited manually: changes made via UnigineEditor at run time won't be saved. All base materials (both built-in and custom ones) are manual. However, not every manual material is the base one: user materials can be manual, too.


> **Notice:** You can use the same name for the base (`*.basemat`), user (`*.mat`) and manual (`*.basemat` or `*.mat`) materials within one project: it won't create any conflict.


### Material Hierarchy


In UNIGINE, *[materials](../../content/materials/index.md)* are organized into a hierarchy, like nodes, but are completely independent from the node hierarchy.


A parent material passes its properties to the inherited material so that they can be overridden.


> **Notice:** All inherited and non-overridden properties will be updated automatically, if they are updated in the parent material.


Base materials cannot be organized into a hierarchy: no base material can be inherited from another base material. However, if you need to modify properties of a base material, you can create a new user material by [inheriting](../../content/materials/inheritance.md#inherit) from the required base material: the base material will pass its properties to the inherited material and you can override them. Thus, the base materials are always on the top of the material hierarchy.


Materials hierarchy is based on *[GUIDs](../../content/materials/inheritance.md#material_guid)*. For base and manual materials, GUIDs are generated at run time by using their names stored in materials files. As for user materials, they are also generated at run time on materials' creation and stored in the `*.mat` files. However in materials files, references to materials can be [name-based or GUID-based](../../content/materials/inheritance.md#inheritance_types).


> **Notice:** Surfaces refer to materials by GUIDs only.


At cloning or inheriting a material, each new material becomes **internal** until a name is assigned to it.


The loading order of materials doesn't matter: on the engine start-up, all materials of the project are loaded, base materials are loaded first. And since each `*.mat` material refers to both the parent and the base materials, the base material is used as the parent one until the parent is loaded. So, when the application is loaded, all materials existing in the project are presented in the materials hierarchy.


![](materials_hierarchy.png)

*Hierarchy of materials in theMaterials Hierarchywindow*


Here is an example:


| ![](mesh_base.jpg) | ![](mesh_base_modified.jpg) |
|---|---|
| *Material ball withmesh_basematerial assigned* | *Material ball with a user material inherited frommesh_base* |


The left material ball is rendered using [one of the built-in base materials](../../content/materials/library/mesh_base/index.md). The right material ball inherits its material from that base and simply changes 2 textures (the [albedo](../../content/materials/library/mesh_base/index.md#texture_albedo) and [normal](../../content/materials/library/mesh_base/index.md#texture_normal) textures). There is no need to set other properties, as they are inherited. However, if necessary, you may change any property, just like we've changed the texture for the material ball.


All material properties (except shaders) can be easily overridden in UnigineEditor. However, if you need to extend a set of existing properties or override shaders, you need to create a [custom material](../../content/materials/custom.md). In this case also check the [Materials Files](../../code/formats/materials_formats/index.md) section for a detailed description of material declarations in XML.


## Properties


Just defining the object's position, inherent characteristics, and outside appearance is not enough to integrate the object into the world correctly. **Properties** specify the way the object will behave and interact with other objects and the scene environment.


A property is a "material" for application logic represented by a set of logic-related **[parameters](../../code/formats/property_format.md#element_parameter)**. Properties can be used to build [**components**](../../principles/component_system/index.md) to extend the functionality of nodes.


You can define [conditions](../../code/formats/property_format.md#parameter_conditions) for parameters of the property to be available/unavailable in UnigineEditor.


UNIGINE's Properties system includes:


- [**Manual**](../../principles/properties/index.md#manual) properties implemented and modified manually by programmers. A manual property at the top of the hierarchy is called a [base](../../principles/properties/index.md#base) property. There are **two** built-in read-only base properties: **node_base** and **surface_base**.
- [**User**](../../principles/properties/index.md#user) properties inherited from the manual ones and [adjusted via the UnigineEditor](../../editor2/properties_settings/index.md) by 3D artists.


Properties can be assigned to both the whole [node](../../start/index.md#node) and a single [surface](../../start/index.md#surface):


- If assigned to a node, properties can specify additional settings that extend the built-in ones (e.g., they can be used to specify if a node is interactive and whether it is a switch). For a character, properties can be used to specify health points or gold amount. > **Notice:** You can assign multiple properties to a single node.
- If assigned to a surface, a property can specify certain parameters that can be used during physical interaction with the surface. For example, the property can indicate the type of material assigned to the surface (wood, metal, plastic, etc.). > **Notice:** Only one property can be assigned to a surface.


Thus, properties make nodes follow the game/application logic.


If you need to assign a property to a [single surface](../../editor2/node_parameters/properties/index.md#surface_property), it is recommended to inherit it from the **surface_base** property.
We also recommend inheriting properties that will be assigned to [nodes](../../editor2/node_parameters/properties/index.md#node_property) from the **node_base** property. However, you can also assign any custom base property or its children to a node.


To assign a property, use one of the [available ways](../../editor2/properties_settings/organizing_properties/index.md#assign_property).


Each property is stored in a separate [`*.prop` file](../../code/formats/property_format.md), except for the [internal properties](../../principles/properties/index.md#internal).


### Property Hierarchy


Properties in UNIGINE, just like materials, are organized into their own independent [hierarchy](../../principles/properties/inheritance.md). This hierarchy is formed by inheriting one property from another. A parent property passes all its parameters to its children so that they can be overridden, much like in the object-oriented programming.

> **Notice:** All inherited and non-overridden parameters will be updated automatically, if they are updated in the parent property.


![](property_hierarchy.png)

*Hierarchy of properties*


The Properties hierarchy is based on [GUIDs](../../principles/properties/inheritance.md#property_guid): all properties are referred to using GUIDs, even the [base](../../principles/properties/index.md#base) and [manual](../../principles/properties/index.md#manual) ones (the GUIDs for such properties are generated at run time and are uniquely determined by their names). However, only [user properties](../../principles/properties/index.md#user) store their GUIDs explicitly: a GUID is generated automatically at the user property creation and is written to the corresponding `*.prop` file.


Properties in the hierarchy can be reparented, [renamed](../../editor2/properties_settings/organizing_properties/index.md#rename_property), [cloned](../../editor2/properties_settings/organizing_properties/index.md#clone_property), [inherited](../../editor2/properties_settings/organizing_properties/index.md#inherit_property), or [removed](../../editor2/properties_settings/organizing_properties/index.md#delete_property) in a single click.


> **Notice:** Reparenting and renaming of [manual properties](../../principles/properties/index.md#manual) in UnigineEditor is not supported. To change a parent or a name of a manual property, edit the [`*.prop` file](../../code/formats/property_format.md#property_parent_name) manually.
