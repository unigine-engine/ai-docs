# Adding Point Objects


The *Points* object type in *Sandworm* is designed to place houses, landmarks, and other such objects at specific points of the terrain based on the vector source data.


### See Also


Check this video from the series of [video tutorials on the terrain generation](../../../../videotutorials/essentials/sandworm.md) using Sandworm:


## Preparing a Primary Object


A primary object to be used for the generation should be a `*.node` file (*Node Reference*) containing a single root node with any hierarchy.


Let's use the `UnigineGeoreferencedTerrainGeneration/nodes/gsm_tower/gsm_tower.node`.


![](gsm_tower.jpg)


## Setting the Point Object


1. Create the object: in the *Objects* panel, click *+* for *Points*. ![](add_object.png)
2. In the *Parameters* tab, add a source: click the *Add Source(s)* button, select *Assets* and set the path to the `UnigineGeoreferencedTerrainGeneration\vector\unique_buildings\unique_buildings.shp` file. As the source is added, we can click the *Preview* button below to see the point data preview on the map. ![](preview.jpg)
3. Set the prepared [primary object](#create_primary_object) as *Node* and keep other settings as they are. ![](node_settings.png)
4. Click the *Create Point Object* button.


## Generated Point Objects


The [generated](../../../../editor2/sandworm/workflow/generate/index.md) points will look as follows:


![](example.jpg)

*Generated point objects*


## What Else


- Read more about the [points parameters](../../../../editor2/sandworm/sources/points/index.md).
- Read more about the [filter settings](../../../../editor2/sandworm/sources/index.md#filters).
