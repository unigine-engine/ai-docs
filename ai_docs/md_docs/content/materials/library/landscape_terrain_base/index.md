# landscape_terrain_base


The *landscape_terrain_base* material is a default material for [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) objects. Via this material, you can manage different options for terrain optimization and control the post processing for terrains.


Terrain textures are assigned via the [landscape_terrain_detail_base](../../../../content/materials/library/landscape_terrain_detail_base/index.md) material used by [Landscape Layer Maps](../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md).


To adjust the landscape_terrain_base material, open the Surfaces tab of the Parameters window:


![Surfaces Tab](surfaces_tab.png)

*Parameters window,Surfacestab.*


## Surface Material Parameters


### Common


[Common](../../../../editor2/materials_settings/index.md#common_tab) material settings.


### Base


**Material Mask** is a [bit mask](../../../../principles/bit_masking/index.md#material_mask) used for decal projection onto the Landscape Terrain surface.


### Post Processing


- **Material SSAO** � enables Screen-Space Ambient Occlusion post for Landscape Terrain.
- **Material SSR** � enables Screen-Space Reflections post for Landscape Terrain.
- **Material SSSSS** � enables Screen-Space Sub-Surface Scattering post for Landscape Terrain.
- **Material DOF** � enables the Depth of Field post effect for Landscape Terrain.
- **Material Motion Blur** � enables the Motion Blur effect for Landscape Terrain.
- **Material Screen-Space Shadows** � enables the Screen-Space Shadows effect for Landscape Terrain.
