# landscape_terrain_detail_base


The *landscape_terrain_detail_base* material is a default material for [details](../../../../objects/objects/terrain/landscape_terrain/index.md#details) of a *Landscape Terrain* object. Via this material you can manage albedo, roughness and height data and apply additional masking for terrain enrichment.


## Parameters


The *landscape_terrain_detail_base* material has the following states and parameters.


### Base


![Base Parameters](base.png)

*Base parameters.*


| Triplanar | Triplanar texture mapping for the detail. |
|---|---|
| Size | Texture tile size. |
| Rotation | Rotation of the detail's textures around the Z axis, in degrees. |
| Offset | Offset of the detail's textures along the X and Y axes, in units. |
| Contrast | Sharp or smooth transition of the detail with other details. |
| Blend Triplanar | The value of blending between triplanar texture projections (available only when the **Triplanar** mapping for the detail is enabled). |


### Albedo


![Albedo Parameters](albedo.png)

*Albedo parameters*


| Opacity | Albedo opacity. |
|---|---|
| Color | Color multiplier for the albedo texture. |
| Texture | Texture used to specify the color information (how the detail looks like). |


### Roughness


![Roughness Parameters](roughness.png)

*Roughness parameters*


| Opacity | Opacity of the roughness effect. |
|---|---|
| Roughness | Roughness multiplier for the roughness texture. |
| Texture | Roughness texture of the detail. |


### Height


![Height Parameters](height.png)

*Height parameters*


| Opacity | Opacity of the height texture. |
|---|---|
| Scale | Displacement height of the detail. > **Notice:** - Maximum possible value is 1.0, but it is not recommended to set it higher than 0.2; > - Detail displacement is clamped to [**Detail Max Height**](../../../../editor2/settings/render_settings/landscape/index.md#detail_max_height) but normals are preserved. |
| Texture | Texture used to specify the height of the detail (for rocks, pits, etc.). |


### Additional Mask


![Additional Mask Parameters](additional_mask.png)

*Additional mask parameters*


| Blend Mode | Blending mode between the additional detail mask and the corresponding mask of a landscape layer map. \| ![](mask_blending_mask.png) *Mask of a landscape layer map* \| ![](mask_blending_add_mask.png) *Additional detail mask* \| \|---\|---\| As an example, for two masks presented above ([Albedo](#albedo) color is set to red color) the available blending modes provide the following results: - **Multiplicative** � the base mask color is multiplied by the additional detail mask color, resulting in darker colors. ![](mask_blending_multiplicative.png) - **Overlay** � the base and additional detail mask colors are multiplied for dark color pixels and screened for light color pixels, which leads to the contrast increase while preserving highlights and shadows. Grey pixels are not effected at all. ![](mask_blending_overlay.png) - **Additive** � the additional detail mask color is added to the base mask color. ![](mask_blending_additive.png) - **Vivid Light** � the additional detail mask colors are darkened for dark color pixels and lightened for light color pixels, which leads to preserving mask details on semi-transparent pixels. ![](mask_blending_vivid_light.png) | ![](mask_blending_mask.png) *Mask of a landscape layer map* | ![](mask_blending_add_mask.png) *Additional detail mask* |
|---|---|---|---|
| ![](mask_blending_mask.png) *Mask of a landscape layer map* | ![](mask_blending_add_mask.png) *Additional detail mask* |  |  |
| Intensity | Mask intensity. |  |  |
| Size | Tile size. |  |  |
| Mask | Additional mask texture (only red channel is taken into account). |  |  |
