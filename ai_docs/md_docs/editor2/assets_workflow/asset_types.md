# Asset Types


There are a number of file types supported by the UNIGINE [assets system](../../editor2/assets_workflow/index.md). This page contains a categorized list of these file types along with a brief description.


## Geometry and Animation


**Mesh** is the basic unit, that consists of a set of polygons and is used to create geometry for worlds in a UNIGINE project.


Some meshes can be animated, apart from a set of polygons representing its surfaces, such mesh has a hierarchical set of interconnected bones (a skeleton or a rig) which can be used to animate the vertices of the polygons. Another way to animate a model is to create morph targets (or blend shapes), these are "deformed" versions of a mesh, stored as a series of vertex positions. In each key frame of an animation, the vertices are interpolated between these stored positions.


![](3d_model.png)

*Exported 3D model*


You can create 3D models, rigs, and animations in an external modeling application (3DSMax, Maya, Softimage, etc.), and then import them to your UNIGINE project via the [Asset Browser](../../editor2/assets_workflow/index.md#asset_browser).


> **Notice:** It is recommended to use **FBX** as an intermediate file format to bring your 3D models to UNIGINE. This format is supported by the most popular 3D editors: Autodesk Maya, Autodesk 3ds Max, Blender, Modo, etc.


| Format | Description |
|---|---|
| **.fbx** | A 3D model or a scene created in an external 3D modeling application. It can contain static meshes, skeletal meshes, animations, morph targets, light sources, and cameras. [Learn more about FBX import.](../../editor2/fbx/index.md) |
| **.dae** | A 3D model or a scene created in an external 3D modeling application and stored in DAE format (COLLADA). It can contain static meshes, skeletal meshes, animations, morph targets, light sources, and cameras. Import settings for DAE files are the same as the ones used for [FBX import.](../../editor2/fbx/index.md) |
| **.3ds** | A 3D model or a scene created in an external 3D modeling application and stored in 3DS format (3D MAX). It can contain static meshes, skeletal meshes, animations, morph targets, light sources, and cameras. Import settings for 3DS files are the same as the ones used for [FBX import.](../../editor2/fbx/index.md) |
| **.obj** | Static polygonal geometry stored in OBJ format � namely, the position of each vertex, the UV position of each texture coordinate vertex, vertex normals, and the faces that make each polygon defined as a list of vertices, and texture vertices. The file format is open and has been adopted by other 3D graphics application vendors. > **Notice:** If you want to import your 3d model with all materials assigned, you should import all corresponding material library assets (`*.mtl` files) either prior to importing the `*.obj` file or together with it. |
| **.glTF** | glTF (GL Transmission Format) is a royalty-free specification for the efficient transmission and loading of 3D scenes and models by engines and applications. > **Notice:** Limited experimental support. |
| **.usd, .usda, .usdc** | [Universal Scene Description](https://openusd.org/release/intro.html#what-is-usd) (USD) format is used for storing hierarchical 3D scenes that may be composed from many elemental assets (textures, materials, meshes, skinned geometry, skeletons and animations, blend shapes, lights, and more) and exchanging this data with third-party applications. |
| **.stp, .step** | A 3D CAD file based on the Standard for the Exchange of Product Data (STEP) format. Is used mostly for solid models. |
| **.igs, .iges** | A CAD file format based on the Initial Graphics Exchange Specification (IGES) 2D/3D vector format. It can contain wireframes, freedom surface or solid modeling representations, or circuit diagrams. |
| **.brep** | Boundary Representation file format. Used for representing shapes by defining boundary limits. |
| **.stl** | A format for storage of stereolithography CAD models. STL files contain only the surface geometry of a 3D object described by triangles. This format is used for 3D printing, rapid prototyping, and computer-aided manufacturing. |
| **.mesh** | Built-in [file format](../../code/formats/file_formats.md#mesh), that describes static and skinned geometry. It supports multiple surfaces and variable number of morph targets (blend shapes) for each surface, as well as multiple named animations stored in the single file. |
| **.anim** | Built-in [file format](../../code/formats/animations_formats.md#anim), that describes skinned animation. It is used together with `*.mesh` file that contains a bind pose. Thus, you can have a single skinned mesh (`*.mesh`) and multiple animations for it. |


## Textures


**Textures** are images that are commonly used in [materials](../../content/materials/index.md). When a material is applied to a surface, textures are mapped to it. They can be either applied directly, as albedo textures, for instance, used as masks, or the values of the texture's pixels can be used for other calculations. Textures can also be used directly, e.g., as environment cubemaps, or to draw a projection of a [Projected Light Source](../../objects/lights/proj/index.md).


![](texture_assigned.png)

*A texture mapped to a 3D mesh*


Textures are generally created using an external image-editing application, such as GIMP or Photoshop, and then imported via the *[Asset Browser](../../editor2/assets_workflow/index.md#asset_browser)*. Some textures, such as render textures, are generated by the UNIGINE Engine. They generally take some information from the scene and render it to a texture to be used elsewhere.


Several textures can be used in a single material for different purposes. For instance, a material may have an albedo texture, an ambient occlusion texture, a normal map, etc. In addition, there may be a map for the *Emission* and *Roughness* stored in the alpha channels of one or more of these textures.


UNIGINE supports the most popular bitmap texture formats (see the table below) along with the following features:


- 8, 16, and 32 bit precision per channel
- *Alpha* channel
- Baked MIP-levels


| Format | Description |
|---|---|
| **.png** | Image file stored in the Portable Network Graphic (PNG) format; contains a bitmap of indexed colors under a lossless compression; commonly used to store graphics for Web images. |
| `.jpg, .jpeg, .jpe, .jif, .jfif, .jfi` | Image file stored in the Joint Photographic Experts Group format using lossy compression. |
| `.tiff` | Image file stored in the TIFF (Tagged Image File Format) format using losless compression. |
| `.tga` | Image in raster graphic file format designed by Truevision; supports 8, 16, 24, or 32 bits per pixel at a maximum of 24 bits for RGB colors and 8-bit alpha channel. |
| `.rgb, .rgba` | Bitmap in RGB/RGBA format. |
| `.psd` | Image file created by Adobe Photoshop, a professional image-editing program; may include image layers, adjustment layers, layer masks, annotation notes, file information, keywords, and other Photoshop-specific elements. |
| `.hdr` | High Dynamic Range image. These are most commonly used for environment maps. |
| `.exr` | Image file stored in the high-dynamic range image file format created by the Industrial Light & Magic visual effects company. > **Notice:** Three types of lossy compression that `*.exr` files can use � **B44, B44A, PIX24** � are not supported. To avoid any related issues, please, consider using either uncompressed `*.exr` files or `*.hdr` files instead. Keep also in mind that the engine applies compression where necessary, thus using a compressed source image may lead to the output image quality deterioration. |
| `.pgm` | Netpbm grayscale image. |
| `.ppm` | Image file stored in the PPM (Portable Pixmap) format. |
| `.sgi` | Image file stored in the SGI (Silicon Graphics Image) format. |
| `.ies` | IES Profile format defined by the Illuminating Engineering Society (IES). Used to make *[Omni](../../objects/lights/omni/index.md#light_settings)* and *[Projected](../../objects/lights/proj/index.md#light_settings_texture)* light sources cast light realistically based on real-world measured data. |
| **.dds** | File in DirectDraw Surface format, contains compressed or uncompressed image data, which is optimal for GPUs. The following types of compression are available: - **DXT1 (BC1/S3TC)** to compress RGB8 data without the alpha channel or 1-bit alpha. It gives the best compression ratio � 1:6, resulting in an image that uses 0.5 bpp (bits per pixel). - **DXT3 (BC2)** to compress RGBA8. It allows encoding the alpha channel, but the file would be twice as large as DXT1. The alpha channel is encoded without compression, which makes this format fit for images with varying alpha values. Compression ratio � 1:4; 1 bpp. > **Warning:** Although the engine supports DXT3(BC2), it is recommended to use DXT5(BC3) instead in order to have textures of a good quality. - **DXT5 (BC3)** to compress RGBA8. This format is in fact a modification of DXT3. The alpha channel is stored in compressed form and fits for cases with more or less homogeneous alpha. This format is suitable for the **shading texture**. - **ATI1 (BC4/3Dc+)** to compress R8, which means it fits for compression of single-channel textures, such as the **height map**. Compression ratio � 1:2; 0.5 bpp. - **ATI2 (BC5/3Dc)** to compress RG8. This format was developed specially for **normal maps**, because it provides a quality better than DXT1 thanks to storing two channels only with reconstruction of the trird one. But this format is also suitable for any other two-channel textures. Compression ratio � 1:2; 1 bpp. - **ZLC1, ZLC2, LZ4** � ZLIB compressed formats that allow for a smaller memory footprint for textures stored in the system memory (these formats are not supported by graphics cards). They are useful for images that cannot be compressed using quality-loss algorithms (DXT, JPG, etc.), for example, GUI textures with thin lines that need to be rendered with pixel precision. |
| `.texture` | Native format of **RGB32F** textures used for [lightmapping](../../editor2/lighting/gi/lightmaps.md). |


To learn more about importing textures, see the [Texture Import Guide](../../editor2/assets_workflow/texture_import.md).


## Materials


**Material** defines how the surface, to which it is assigned, will look like: its interaction with lights, reflection parameters, etc. A material asset is generally linked to several [texture assets](#texture).


The list of supported material assets includes the following:


| Format | Description |
|---|---|
| `.basemat` | Built-in type representing a [base material](../../content/materials/index.md#base_materials), from which other materials can be inherited. [Learn more about the base material file format.](../../code/formats/materials_formats/ulon_base_material_format.md) |
| `.mat` | Built-in type representing a [user material](../../content/materials/index.md#user_materials) inherited from the base one. [Learn more about the user material file format.](../../code/formats/materials_formats/user_material_format.md) |
| `.mtl` | Material template library MTL file, that stores description of materials for [3D models in OBJ format](#obj). > **Notice:** An `*.mtl` file should be imported together with a corresponding `*.obj` file referring to it. |
| `.mgraph` | Built-in type representing Material Graph assets. It stores a node-based graph defining a material created with the **[Visual Material Graph editor](../../content/materials/graph/index.md)**. [Learn more about the Material Graph asset.](../../content/materials/graph/index.md#graph_create) |


When materials are imported along with a 3D model, only the following source data will be used (if defined):


- Textures:

  - Diffuse (albedo) texture
  - Normal map or bump map
  - Specular texture
  - Light map
- Parameters:

  - Diffuse color
  - Specular color and power
  - Emission color


> **Notice:** As UNIGINE uses its own [material system](../../content/materials/index.md), you should [adjust other material settings](../../editor2/materials_settings/index.md) manually.


## Sound and Video Files


**Sound** assets � are the key resources for creating the proper feeling of immersion in the virtual world. UNIGINE supports virtually the unlimited number of sound sources


Either as mono or stereo files, compressed or not, they can be quickly imported into your project.


In the table below you'll find types of sound and video assets supported by UNIGINE.


| Format | Description |
|---|---|
| `.wav` | Waveform audio file (mono and stereo). |
| `.mp3` | MP3 file type storing compressed audio data. |
| `.oga, .ogg` | Ogg Vorbis (or oga, Ogg Audio Profile) storing compressed audio data. |
| `.ogv` | Video file that uses the open source Ogg container format; may contain video streams that use one or more different codecs, such as Theora; can be played using a variety of media players. |


## Scripts


**Scripts** are an essential part of your project representing application logic. UNIGINE supports two scripting approaches: [C#](../../code/csharp/index.md) and [UnigineScript](../../code/uniginescript/index.md) (proprietary scripting language).


- **C#** is supported through `.cs` files, which appear as C# Components (used in the [C# Component System](../../principles/component_system/component_system_cs/index.md)) and [C# Files](../../code/csharp/interfaces_and_abstract_classes.md), containing supporting code such as interfaces, abstract classes, or helper classes.
- **UnigineScript** is designed to make coding easy-to-use even for junior programmers and at the same time provide the most optimal Engine usage. Scripts are platform-independent and do not require compilation.


![](script.jpg)


Both asset types can be created and edited in a plain text-editor. You can add scripts to your project via the [Asset Browser](../../editor2/assets_workflow/index.md#asset_browser).


| Format | Description |
|---|---|
| `.cs` | A C# source code file containing implementation of your application's logic. It can either represent a [C# component](../../principles/component_system/component_system_cs/index.md) or contain [supporting code](../../code/csharp/interfaces_and_abstract_classes.md) such as interfaces, abstract or helper classes. |
| `.h` | Built-in type representing a header-file for a script written in [UnigineScript](../../code/uniginescript/index.md). |
| `.usc` | Built-in type representing a script written in [UnigineScript](../../code/uniginescript/index.md). |
| `.cpp (deprecated)` | Built-in type representing a script written in [UnigineScript](../../code/uniginescript/index.md). |


## Presets


UnigineEditor allows saving various **presets** � configurations of different settings (e.g. rendering settings, gravity, sound velocity, volumes of sound sources, etc.). This type of assets can be used to configure worlds within your project.


| Format | Description |
|---|---|
| `.render` | Built-in type that determines a configuration of [rendering settings](../../editor2/settings/render_settings/index.md) for a world. |
| `.physics` | Built-in type that determines a configuration of [physics simulation settings](../../editor2/settings/physics_global/index.md) for a world. |
| `.sound` | Built-in type that determines a configuration of sound settings for a world. |
| `.navigation` | Built-in type that determines a configuration of [navigation settings](../../editor2/settings/navigation/index.md) for a world: the budgets of the experimental navigation system and the list of areas the ground can be marked with. |
| `.launch` | Built-in type that determines a configuration of [custom run options](../../principles/component_system/component_system_cs/index.md#run) for C# (.NET) projects. |


## Other Asset Types


| Format | Description |
|---|---|
| `.world` | Built-in type describing a UNIGINE [world](../../start/index.md#world) (scene). One project can include several worlds. So, there is no need to create a separate project for each world. Created in the UnigineEditor. [Learn more about the creating and managing worlds.](../../editor2/worlds/index.md) |
| `.node` | Built-in type describing any [Node](../../start/index.md#node) (or a hierarchy of Nodes) of the UNIGINE's virtual world. Created in the UnigineEditor or [at runtime via the code](../../api/library/nodes/class.node_cpp.md#export_import_node). |
| `.prop` | Built-in type describing a property. A property is a "material" for application logic. It specifies the way how the object will behave and interact with other objects and the scene environment. |
| `.sworm` | Built-in type that stores generation parameters used by the *[Sandworm](../../editor2/sandworm/index.md)* Tool to generate a *[LandscapeTerrain](../../objects/objects/terrain/landscape_terrain/index.md)* or *[TerrainGlobal](../../objects/objects/terrain/terrain_global/index.md)* object. Created in the *Sandworm* Tool. > **Warning:** The functionality described in this paragraph is not available in the Community SDK edition. > You should upgrade to [**Engineering**](https://l.unigine.com/kNeoPJV1j) / [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it. |
| `.track` | Built-in type, that contains the sequence of the parameters animated with keyframes along the timeline. Created in the [Tracker Tool](../../editor2/tools/tracker/index.md). |
| `.ttf` | The font in TTF (True Type Font) format. As a raster font, it can be scaled to any size without quality loss or pixelation, and the stored image appears the same when printed as it does on-screen. You can use any existing TTF font or create a new one. |
| `.path` | The path is a spline along which an object can be moved. Such splines can be created, for example, in 3ds Max or via the API, using the *[Path](../../api/library/common/class.path_cpp.md)* class and then saved to the `*.path` file. |
| `.spl` | Built-in type to store [world spline graphs](../../objects/worlds/world_spline_graph/index.md). This is a text file based on the *[json](http://www.json.org/)* format. A [spline file](../../code/formats/spline_format.md) contains all necessary information to define a spline graph consisting of points in 3D space connected by cubic Bezier spline segments. |
| `.lmap` | Built-in type to store *[Landscape Layer Map](../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md)*. This is a binary file containing albedo, height and mask textures and settings. |
| `.navmesh` | Built-in type to store a baked *[Navigation Mesh (Experimental)](../../objects/navigations/experimental/navigation_mesh/index.md)*. This is a binary file holding the tiles the bake produced, so that a world does not pay for a bake every time it is loaded. Written by the *Bake* button of the node. |
| `.sv` | Built-in type used by the *[SpiderVision](../../principles/render/output/multi_monitor/spidervision_plugin/displays_setup.md#config_file)* plugin to define multi-display and projection setups. It stores viewport arrangements, projection parameters, color correction, blend zones, masks, wall groups, configuration names, and hotkeys. |
| `.ply (experimental)` | A file in `.ply` (Polygon File Format) format stores 3D Gaussian Splat data, such as point clouds and polygonal meshes. It supports vertex positions, colors, normals, and other attributes and is commonly used for point-based rendering and geometry exchange. |
