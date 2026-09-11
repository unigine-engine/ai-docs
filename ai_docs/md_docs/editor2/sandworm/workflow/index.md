# Starting with Sandworm


This section is a newcomer's guide on how to create a terrain based on georeferenced data and generate various groups of objects.


### Preparation Steps


To follow this guide, you need to:


1. Download the *[Georeferenced Terrain Generation](../../../sdk/addons/terrain_geo/index.md)* and *[Procedural Generation](../../../sdk/addons/procedural_generation_assets/index.md)* add-ons.
2. [Create a new project](../../../sdk/projects/index_cpp.md#creation) and add the downloaded add-ons to it.
3. Open the project in *UnigineEditor* and open the *Sandworm* tool.
4. Create a new *Sandworm* project (*Tools -> Sandworm -> Create New*, type a project name, and click *Next*).


> **Notice:** For the sake of performance, check that *[Microprofile](../../../tools/profiling/microprofile/index_cpp.md)* is disabled.


### Generation Steps


In general, the process of generating the terrain in *Sandworm* is as follows:


1. Add the [terrain data](../../../editor2/sandworm/workflow/landscape/index.md): heights and imagery.
2. Add [masks](../../../editor2/sandworm/workflow/mask/index.md) for vegetation and details.
3. Add objects such as [roads](../../../editor2/sandworm/workflow/roads/index.md), [point objects](../../../editor2/sandworm/workflow/points/index.md), [spline objects](../../../editor2/sandworm/workflow/lines/index.md), [vegetation](../../../editor2/sandworm/workflow/vegetation/index.md), [rivers](../../../editor2/sandworm/sources/rivers/index.md), and [buildings](../../../editor2/sandworm/workflow/buildings/index.md), if any.
4. Define the generation settings: [quality of generated data](../../../editor2/sandworm/generation/quality/index.md), [projection](../../../editor2/sandworm/generation/projection/index.md), and the [world](../../../editor2/sandworm/generation/output_dir_files/index.md) that will store the generated result. The [terrain type](../../../editor2/sandworm/interface/index.md#terrain_type) was chosen when the *Sandworm* project was created and cannot be changed here.
5. [Generate](../../../editor2/sandworm/workflow/generate/index.md) the output.
6. Open the world with the output terrain in *UnigineEditor*.


Now let's review these steps in detail.
