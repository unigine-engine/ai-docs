# Adding Buildings


Sandworm allows the procedural generation of buildings based on shapes stored in the vector data sources.


The [Procedural Generation Assets](../../../../sdk/addons/procedural_generation_assets/index.md) add-on contains additional building materials to add a variety to the city view. You can use your own materials as long as they are created following the [rules](../../../../editor2/sandworm/sources/buildings/index.md#materials_naming).


### See Also


Check this video from the series of [video tutorials on the terrain generation](../../../../videotutorials/essentials/sandworm.md) using Sandworm:


## Setting the Building Object


1. Create the object: in the *Objects* list of the *Sources* panel, click *+* for *Buildings*. ![](add_object.png)
2. In the *Parameters* panel, add a source: click the *Add Source(s)* button, select *Assets* and set the path to the `UnigineGeoreferencedTerrainGeneration/vector/buildings.shp` file. As the source is added, we can click the *Preview* button below to see the building data preview on the map. ![](preview.png)
3. Add a [filter](../../../../editor2/sandworm/sources/index.md#filters) if you want to pick specific data from the source. Open the Attributes Table (the ![](../../sources/table_sign.png) button) to look through all available data and set any filter you want. If you add no filters, all buildings will be generated.
4. In fact, we can already generate the buildings with Auto settings. However, if you do that, you'll notice several skyscrapers not typical for such towns. This is due to the data provided in the floor column of the Attributes table: some values are irrelevant. Filters also can't help in this case as the data is in the string format. To solve this problem, let's switch to the *[Manual](../../../../editor2/sandworm/sources/buildings/index.md#parameters)* mode and set the *Floor Number* parameter to Random: ![](floor_parameters.png) In this case *Sandworm* will disregard any floor number values from the data source and generate buildings with a random number of floors from 1 to 5 as set in *Floor Number Range*.
5. Click the *Create Building Object* button.


## Generated Buildings


The [generated](../../../../editor2/sandworm/workflow/generate/index.md) buildings will look as follows:


![](example.jpg)

*Generated buildings*


## What Else


- Check the article on [Buildings Customization](../../../../editor2/sandworm/sources/buildings/index.md).
