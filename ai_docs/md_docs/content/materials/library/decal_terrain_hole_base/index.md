# decal_terrain_hole_base


A *decal_terrain_hole_base* material creates holes in [Global Terrain](../../../../objects/objects/terrain/terrain_global/index.md#decal_holes) and [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md#decal_holes) using [decals](../../../../objects/decals/index.md).

 Prior KnowledgeThis article assumes you have prior knowledge of the following topics. Please read them before proceeding:
- *[Materials settings](../../../../editor2/materials_settings/index.md)*
- *[mesh_base](../../../../content/materials/library/mesh_base/index.md)* material states, textures, parameters
- *[decal_base](../../../../content/materials/library/decal_base/index.md)* material states, textures, parameters


### See Also


- Samples located in `decals` folder.


## States


![States](states.png)

*Materials editor,Statestab.*


### Options


#### Jitter Transparency


**Jitter transparency** enables creating deferred transparency by using jittering. When enabled, a dither pattern is used for transparency imitation.


| ![](jitter_off_scheme.png) | ![](jitter_on_scheme.png) |
|---|---|
| *Jitter Transparency disabled* | *Jitter Transparency enabled* |


#### Only Touched Lods


**Only touched Lods** indicates whether the decal cuts out the surface of all LODs of the Terrain Global or of only those ones with which it intersects.


### UV Mapping


#### Base


Base option specifies which UV coordinates of the mesh will be used for base texture.


> **Notice:** **World** mapping option described below works properly only within the distance range of 10000 units from the origin.


- UV - map the texture using the UV coordinates of the mesh.
- World - map the texture using world transformation (the texture is always projected atop).


## Textures


![Textures](textures.png)

*Materials editor,Texturestab.*


### Base Textures


#### Mask


**Mask** texture defines areas of holes in a terrain object. Only R channel is used:


- **White** pixels indicate that the area will be transparent.
- **Black** pixels indicate that the area will be visible.


| ![](terrain_hole.png) | ![](noise_texture.png) |
|---|---|
| *Mask texture applied* | *Mask texture* |


## Parameters


All of the parameters have set default values, which can be replaced by your own ones.


### Base Parameters


![](parameters.png)

*Materials editor,Parameterstab.*


#### UV Transform


**[Base](#textures_base)** texture coordinates transformation.


#### Transparent Multiplier


**Transparent multiplier** is a multiplier of mask's colors. The higher the value, the darker pixels of mask are holes.


![](mask_texture.png)


For this mask texture, results of Transparent multiplier usage with the [Jitter Transparency](#option_jitter) disabled are the following:


| ![](transparent_multiplier_2.png) | ![](transparent_multiplier_1.png) | ![](transparent_multiplier_3.png) |
|---|---|---|
| *Transparent multiplier = 0.5; Transparent pow = 1.0* | *Transparent multiplier = 1.0; Transparent pow = 1.0* | *Transparent multiplier = 1.5; Transparent pow = 1.0* |


With the [Jitter Transparency](#option_jitter) enabled:


| ![](transparent_multiplier_jitter_3.png) | ![](transparent_multiplier_jitter_1.png) | ![](transparent_multiplier_jitter_2.png) |
|---|---|---|
| *Transparent multiplier = 0.5; Transparent pow = 1.0* | *Transparent multiplier = 1.0; Transparent pow = 1.0* | *Transparent multiplier = 1.5; Transparent pow = 1.0* |


#### Transparent Pow


**Transparent pow** is a power of mask's colors. The higher the value, the less contrast the mask.


| ![](transparent_pow_jitter_1.png) | ![](transparent_pow_jitter_2.png) | ![](transparent_pow_jitter_3.png) |
|---|---|---|
| *Transparent pow = 0.01; Transparent multiplier = 1.0* | *Transparent pow = 1.0; Transparent multiplier = 1.0* | *Transparent pow = 2.0; Transparent multiplier = 1.0* |
