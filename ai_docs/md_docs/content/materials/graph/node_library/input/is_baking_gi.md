# Is Baking GI Node


![](../img/is_baking_gi.png)

### Description

Outputs a boolean value indicating that [baking](../../../../../editor2/lighting/gi/index.md#light_baking) Global Illumination (GI) is currently in progress. You can pass this value to a [Branch](../../../../../content/materials/graph/node_library/logical/branch.md) node to change the look of your material when baking Global Illumination ([lightmaps](../../../../../editor2/lighting/gi/lightmaps.md), [Voxel Probes](../../../../../editor2/lighting/gi/voxel_probes.md), and [Environment Probes](../../../../../editor2/lighting/gi/env_probes.md)).


In case you want to change material colors after light baking, you can temporarily set the Albedo color to gray for such materials while baking lights. Simply connect gray color node to the True input of the [Branch](../../../../../content/materials/graph/node_library/logical/branch.md) node, and initial Albedo to the False input.
