# Adding Pipelines, Fences, Powerlines


Fences, pipes, and similar objects are placed along line segments selected from vector data sources (`*.shp` files). You can also simulate aircraft warning lights (in this case **Billboards** is used as the basic object).


In this chapter, let's perform two tasks:


- [Create lights](#create_lights) using the *Billboards* object.
- [Place a fence](#fences) along a road. The approach described here can be used for pipes, powerlines and other similar objects.


### See Also


Check this video from the series of [video tutorials on the terrain generation](../../../../videotutorials/essentials/sandworm.md) using Sandworm:


## Creating Lights


### Preparing Billboards


1. Create a *Billboards* object: click *Create -> Billboards -> Base* on the Menu bar.
2. Inherit the surface material and enable the *[Emission](../../../../content/materials/library/billboards_base/index.md#param_emission)* state. You can change the emission color and any other parameters in the *Parameters* panel. ![](billboards_primary.jpg)
3. [Export](../../../../editor2/exporting_nodes/index.md#export_to_noderef) the object to a `*.node` file.


> **Notice:** The `*.node` file should contain a single *[Billboards](../../../../objects/objects/billboards/index.md)* object.


Now that the primary node (the `*.node` asset) is ready for use, you can disable it or delete from the scene.


### Placing Billboards


1. Create the spline object: in the *Objects* list of the *Sources* panel, click *+* for *Spline Objects*. ![](add_spline_object.png)
2. In the *Parameters* panel, add a source: click the *Add Source(s)* button, select *Assets* and set the path to the file. As we are going to place billboards along the road, let's use `UnigineGeoreferencedTerrainGeneration/vector/roads.shp` as the vector data source.
3. Configure the billboards parameters: ![](billboards_parameters.png)

  - Set the created [node](#create_billboards) in the corresponding field.
  - Set 5 as the value for the **[Step](../../../../editor2/sandworm/sources/splines/index.md#step)** parameter that determines the distance (in units) between the two adjacent lights (*Billboards*) placed along the road.
4. Click the *Create Spline Object* button.


Now the spline object is ready for generation.


## Creating Fences


### Preparing Fence Node


An important issue about placing objects along the lines is the node's pivot point: it should be shifted, if you want a fence to be generated near the road, not in the middle of it. To do this, open the asset in a third-party Digital Content Creation software.


The road in this example was built from the 10-unit-wide plane prepared in [Adding Roads](../../../../editor2/sandworm/workflow/roads/index.md#create_primary_object), so the fence must sit more than 5 units from its pivot to keep it off the road. If your road mesh has a different width, offset the fence by more than half of it.


The reimported model will look as follows:


![Fence with a shifted pivot](shifted_fence.jpg)


[Export](../../../../editor2/exporting_nodes/index.md#export_to_noderef) the object to a `*.node` file.


Now that the primary node (the `*.node` asset) is ready for use, you can disable it or delete from the scene.


### Placing Fence


1. Create the spline object: in the *Objects* list of the *Sources* panel, click *+* for *Spline Objects*. ![](add_spline_object.png)
2. In the *Parameters* panel, add a source: click the *Add Source(s)* button, select *Assets* and set the path to the file. As we are going to place a fence along the road, let's use `UnigineGeoreferencedTerrainGeneration/vector/roads.shp` as the vector data source.
3. Placing fences along all roads might be not very performance-friendly, so let's set a [filter](../../../../editor2/sandworm/sources/index.md#filters). Let's use the same filter as for roads: ![](../roads/residential_road_filter.png)
4. Configure the object parameters: ![](fence_parameters.png)

  - Set the created [node](#create_fence) in the corresponding field.
  - Adjust the [maximum visibility distance](../../../../editor2/sandworm/sources/splines/index.md#max_visibility) and [fade](../../../../editor2/sandworm/sources/splines/index.md#max_fade) for the sake of performance.
  - You can also try out the *[Skew](../../../../editor2/sandworm/sources/splines/index.md#skew)* option if you want the fence to follow the slopes of the terrain surface.
5. Click the *Create Spline Object* button.


Now the spline object is ready for generation.


The [generated](../../../../editor2/sandworm/workflow/generate/index.md) fence will look as follows:


![](example_fence.jpg)


You can modify the cluster manually, but keep in mind that if you regenerate the object all manual changes will be lost. A solution may be to clone the edited object and move outside the *Terrain* hierarchy.


## What Else


- Read more about the [spline objects parameters](../../../../editor2/sandworm/sources/splines/index.md).
- Read more about the [filter settings](../../../../editor2/sandworm/sources/index.md#filters).
