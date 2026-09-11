# Objects


Objects are the major building blocks that construct the world. They are a stage settings for representing the visual idea and should be carefully placed to provide compositional coherence and deliver the holistic experience from the scene. Objects can be of the following types:


- [![](dummy.png)](../../objects/objects/dummy/index.md) � **[Dummy object](../../objects/objects/dummy/index.md)** is an invisible object that can have a body assigned. It is usually used as a root object or a connecting object.
- [![](mesh.png)](../../objects/objects/mesh/index.md) � **[Static mesh](../../objects/objects/mesh/index.md)** is an object that represents a collection of vertices, edges and faces defining the object's geometry. It is usually used to add non-animated meshes to the world.
- [![](mesh.png)](../../objects/objects/mesh_skinned/index.md) � **[Skinned mesh](../../objects/objects/mesh_skinned/index.md)** is an object that can contain both mesh geometry (vertices, edges and triangular faces organized in polygons) and animation data. It is usually used for rendering characters with a bone-based animation or a morph target animation (also known as blend shapes).
- [![](dynamic.png)](../../objects/objects/mesh_dynamic/index.md) � **[Dynamic mesh](../../objects/objects/mesh_dynamic/index.md)** is an object that represents a collection of vertices, edges and triangular faces (organized in polygons) defining the object's geometry that can be modified procedurally.
- [![](cluster.png)](../../objects/objects/mesh_cluster/index.md) � **[Mesh cluster](../../objects/objects/mesh_cluster/index.md)** is an object that can contain a great number of identical meshes, which can be scattered either automatically or each mesh can have custom position, rotation and scale.
- [![](clutter.png)](../../objects/objects/mesh_clutter/index.md) � **[Mesh clutter](../../objects/objects/mesh_clutter/index.md)** is an object that can contain a great number of identical meshes. Unlike cluster meshes, clutter meshes are always positioned, oriented and scaled randomly and cannot be managed manually.
- [![](terrain.png)](../../objects/objects/terrain/index.md) � **[Terrain](../../objects/objects/terrain/index.md)** is a 2D grid based on height data. It is used to create complex and naturally diverse landscapes such as planes, hills and mountains or reproduce fragments of the Earth's surface. (For such relief features as overhangs and caves use static meshes).
- [![](water.png)](../../objects/objects/water/index.md) � **[Water](../../objects/objects/water/index.md)** is a prepared object simulating different liquids.
- [![](sky.png)](../../objects/objects/sky/index.md) � **[Sky](../../objects/objects/sky/index.md)** is an object represented as an upper hemisphere, tiled with a texture producing realistic dynamic clouds.
- [![](sky.png)](../../objects/objects/cloud_layer/index.md) � **[Cloud Layer](../../objects/objects/cloud_layer/index.md)** is an object representing a layer of realistic dynamic clouds.
- [![](grass.png)](../../objects/objects/grass/index.md) � **[Grass](../../objects/objects/grass/index.md)** is a common object for vegetation simulation.
- [![](billboard.png)](../../objects/objects/billboards/index.md) � **[Billboards](../../objects/objects/billboards/index.md)** are rectangular flat objects that always face the camera.
- [![](gui.png)](../../objects/objects/gui/index.md) � **[GUI objects](../../objects/objects/gui/index.md)** are flat or mesh-based graphical elements, which can have various [widgets](../../code/gui/index.md) assigned.
