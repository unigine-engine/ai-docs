# Adding Vegetation


Trees and grass are placed on the terrain based on the [Mask](../../../../editor2/sandworm/workflow/mask/index.md) data.


### See Also


Check this video from the series of [video tutorials on the terrain generation](../../../../videotutorials/essentials/sandworm.md) using Sandworm:


## Preparing a Primary Object


We need to create a primary object that will be used as a building block to generate vegetation (grass, trees, etc.). The following types of primary objects are supported:


- *[Grass](../../../../objects/objects/grass/index.md)* object
- *[Mesh Clutter](../../../../objects/objects/mesh_clutter/index.md)* object
- *[World Clutter](../../../../objects/worlds/world_clutter/index.md)* object (generated only if ***Object Terrain Global*** is selected as the [Terrain Type](../../../../editor2/sandworm/interface/index.md#terrain_type))
- A **group** of the objects above, exported to a single *[Node Reference](../../../../editor2/exporting_nodes/index.md#export_to_noderef)* � all of them are then planted over the same area, so one vegetation object produces a mixed cover


Let's create a *Mesh Clutter* object with a tree.


> **Notice:** You can omit the creation process and use a ready-made *Node Reference* `UnigineGeoreferencedTerrainGeneration/nodes/vegetation/pine/pine_clutter.node`.


1. In the scene, click *Create -> Clutter -> Mesh*. In the window that opens, select a mesh: `UnigineGeoreferencedTerrainGeneration/nodes/vegetation/pine/fbx/pine_01_2.FBX/pine_01_2.mesh` and place it somewhere in the scene.
2. Specify parameters of the primary object in the *Parameters* panel: assign the materials from the `UnigineGeoreferencedTerrainGeneration/nodes/vegetation/pine/materials/` folder to the corresponding surfaces, increase the visibility distance of the Mesh Clutter, etc. For more details, see [this article](../../../../content/tutorials/vegetation/index.md). > **Notice:** Intersections with the parent object **must be enabled** for all types of primary objects. The *Intersection* flag can be found on the *Parameters* panel of the object. ![](intersections_enabled.png)
3. Open the folder in the Asset Browser where you want the primary object be stored, right-click on the created *ObjectMeshClutter* and [create a *Node Reference*](../../../../editor2/exporting_nodes/index.md#export_to_noderef) from it.


The primary object is ready � we will use this *Node Reference* to generate vegetation.


![Created primary object](primary_object.jpg)


You can remove it from the scene at all or disable if you'll require it later for further adjustments.


### Impostors


Considering that there'll be many trees generated, you may come across some performance issues. To optimize vegetation, create the *[Impostor](../../../../content/optimization/geometry/impostors/index.md)* object that will be rendered at a farther distance.


If you created the primary object from scratch, be sure that all settings of the *Impostor* object [are the same as](../../../../objects/objects/grass/index.md#low_poly_grass) in the primary object, except *Visibility Distance*.


You may also use the *Impostor* asset `UnigineGeoreferencedTerrainGeneration/nodes/vegetation/pine/pine_clutter_impostor.node` from the pack in pair with the `UnigineGeoreferencedTerrainGeneration/nodes/vegetation/pine/pine_clutter.node` asset.


## Adding the Vegetation Object


1. In the *Objects* list of the *Sources* panel, click *+* for *Vegetation*. ![](add_object.png)
2. Set the following parameters for the object: ![](vegetation_object_set.png)

  - The object name is set for convenience. This name will be displayed in the Objects list in Sandworm and in the *World Nodes* hierarchy after generation.
  - As you have only one mask, it is selected by default in the *Parameters* panel.
  - Set the prepared [primary object](#create_primary_object) as *Node* (or use an asset from the pack).
3. Click the *Create Vegetation Object* button.


You can edit any parameters of the created vegetation object in *Sandworm* � changes are saved automatically.


If you plan to use an *[Impostor](#impostors)* object, add it as one more *Vegetation* object.


![List of Created Objects](created_objects.png)


## Generated Vegetation


The [generated](../../../../editor2/sandworm/workflow/generate/index.md) trees:


![](example.jpg)

*Generated trees*


## What Else


- Add grass the same way using the *Grass* node instead of *Mesh Clutter*. Use the same mask and grass will be spread under the trees.
- Check the information on how to [generate](../../../../editor2/tools/impostors_creator/index.md) and [use](../../../../content/optimization/geometry/impostors/index.md) *Impostors*.
- Read the tips on [vegetation optimization](../../../../content/tutorials/vegetation/index.md#billboards).
- Check the article on the *Sandworm* [vegetation parameters](../../../../editor2/sandworm/sources/vegetation/index.md) for a more detailed description.
