# Requirements To 3D Models


This article describes the recommended methods of importing 3D geometry (3D models) to UNIGINE by means of [UnigineEditor](../../editor2/index.md).


## Geometry


The [FBX](https://en.wikipedia.org/wiki/FBX) file format is recommended for working with 3D geometry. Export to `*.fbx` is supported by the most popular 3D editors: *Autodesk Maya, Autodesk 3ds Max, Blender, Modo*, etc.


After [importing](../../editor2/fbx/index.md) the `*.fbx` file into UNIGINE, a so-called [**runtime**](../../editor2/assets_workflow/assets_runtimes.md) file is generated in an internal [MESH](../../code/formats/file_formats.md) file format for the source file. The created `*.mesh` file is saved to the `data/.runtimes` folder created in the same directory as the source `*.fbx` file in the `data` root folder.


In terms of UnigineEditor, the imported file becomes an [Asset](../../editor2/assets_workflow/index.md), a "unit of work" used in world building. After the asset is added to the virtual world, its geometry (same as any object in the scene) becomes the [node](../../start/index.md#node) and can be seen in the [World Hierarchy](../../editor2/interface/index.md#world_hierarchy) window. Any material, assigned to this geometry, becomes the single [surface](../../start/index.md#surface) of this node (surfaces can be found in the *Surfaces* section on the *Node* tab of the [Parameters](../../editor2/interface/index.md#parameters) window).


The **mesh limitations** set in UNIGINE:


| Maximum number of **vertices** per mesh | 4,294,967,295 |
|---|---|
| Maximum number of **surfaces** per mesh | 32,768 |


For example, in the 3D editor we have the car model consisting of five parts (the frame and four wheels). Two materials (car paint and glass) are assigned to the frame, one material (rubber) is assigned to each wheel. After the model has been exported to `*.fbx` and then imported to UNIGINE, five `*.mesh` files will be created (according to the amount of car parts in the 3D editor):


- Each of the four wheels will have one surface, as one material has been assigned.
- The frame will have two surfaces (as two materials have been assigned).
- The names of the surfaces will correspond to the names of materials assigned in the 3D editor.
- UNIGINE [materials](../../content/materials/index.md) will be created automatically on the `*.fbx` file import; their names will also correspond to the names of the 3D editor materials.


## Texture Coordinates


UNIGINE supports two UV channels for geometry. To specify whether to use the first or the second channel, use [materials settings](../../content/materials/library/mesh_base/index.md#uv_mapping). For example, you can use the first channel for tiling, and the second channel for the light map.


## Level of Details


If you want to create several variations of one object with different [levels of detail](../../principles/world_management/index.md#lods) (LOD), it is recommended to create them as individual surfaces. This will allow you to reduce the amount of nodes in the [hierarchy](../../principles/world_structure/index.md#nodes_hierarchy) and simplify the settings of the LODs visibility. The amount of polygons in the neighbouring LODs should differ at least 2-3 times. The recommended amount of LODs is 2 or 3 (more LODs will cause big CPU load).


To import LODs (different objects) to UNIGINE as different surfaces of one node, choose the *[Combine by Postfixes](../../editor2/fbx/index.md#lods)* option on FBX import.


## Textures


UNIGINE supports the most popular bitmap texture formats: `*.png, *.jpg, *.tiff, *.dds, *.tga, *.rgb, *.rgba, *.psd, *.hdr, *.pgm, *.ppm, *.sgi` with support for:


- **8**, **16** and **32** bit precision per channel
- Alpha channel
- Baked MIP-levels


You can [import texture](../../editor2/assets_workflow/texture_import.md) of any type listed above: the runtime `*.texture` file will be generated automatically, if necessary.


Texture resolution should be power of two, for example: **128�128, 256�256, 512�512, 1024�1024, 2048�2048**, etc. Both square and rectangular textures are supported (for example, **256�1024** pixels).


Texture resolution should not exceed **16384�16384**.


The texture postfix is important as it defines the compression algorithms and used color channels. For example, the postfix **_alb** is for [albedo](../../content/materials/library/mesh_base/index.md#texture_albedo) textures, **_n** and **_nrgb** for [normal](../../content/materials/library/mesh_base/index.md#texture_normal) textures, etc. The full list of postfixes is available [here](../../editor2/assets_workflow/texture_import.md#postfix).


## Animation


UNIGINE supports skeletal animation (3D model vertices have corresponding bones and their weights). An animated 3D model consists of the following files:


- `*.mesh_skinned` - bind pose and geometry (surfaces with skinning weights for all vertices).
- `*.anim` - animation frames (per-joint transforms for each frame).
- `*.skeleton` - shared skeleton that can be referenced by multiple meshes and animations.


To export animation to `*.fbx` from a 3D editor, choose *Animation* and *Bake Animation* and specify which frames should be exported. When importing the animated `*.fbx` file to UNIGINE, separate `*.mesh_skinned`, `*.anim`, and `*.skeleton` files will be created.


The **limitations** set in UNIGINE:


- Maximum amount of **weights** per vertex: 4


A skinned mesh is displayed in the scene via an [ObjectMeshSkinned](../../objects/objects/mesh_skinned/index.md) node controlled by a [Skeleton Pose](../../objects/animations/nodeskeletonpose/index.md) node. For legacy projects, [ObjectMeshSkinnedLegacy](../../objects/objects/mesh_skinned_legacy/index.md) is also available.


See [Preparing Animation Assets](../../content/animations/animation_assets/index.md) for details.


## Names


For file and surface names it is recommended to use English, lower case, without spaces.


## See Also


- [Mesh class](../../api/library/rendering/class.mesh_cpp.md) API
- [MeshSkinnedAnimation class](../../api/library/rendering/class.meshskinnedanimation_cpp.md) API
- Article on [Mesh File Formats](../../code/formats/file_formats.md)
