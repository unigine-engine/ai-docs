# Texture Import Guide


You can import textures in convenient formats (such as `.tga, .jpg, .png, .hdr,` etc.). As you import a texture via the *[Asset Browser](../../editor2/assets_workflow/index.md#asset_browser)*, using drag and drop or the **Import** button, the following import settings are displayed. These settings can also be changed later via the *[Parameters](../../editor2/interface/index.md#parameters)* window.


![](import_texture.png)

*Import settings for a texture asset*


## Common Parameters


| Unchanged | Defines whether the texture is to be used "as is" or a [runtime](../../editor2/assets_workflow/assets_runtimes.md) will be created for it in accordance with the specified import options. > **Notice:** When this option is enabled, the texture is used by the Engine and added to the final build "as is". E.g., you can use this option for your custom HDR texture. |  |  |  |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Texture Preset | This preset determines what sort of texture is to be generated, it defines compression algorithms and color channels to be used. The list of available presets includes the following: - **Albedo (RGB)** � for 3-channel [albedo](../../content/materials/library/mesh_base/index.md#texture_albedo) textures ([postfix](#postfix): **_alb**) - **Albedo (*RGB* � color, *A* � opacity)** � for 4-channel [albedo](../../content/materials/library/mesh_base/index.md#texture_albedo) textures ([postfix](#postfix): **_alb**) - **Diffuse (RGB)** � for 3-channel [diffuse](../../content/materials/library/mesh_base/index.md#texture_diffuse) textures ([postfix](#postfix): **_d**) - **Diffuse (*RGB* � color, *A* � opacity)** � for 4-channel [diffuse](../../content/materials/library/mesh_base/index.md#texture_diffuse) textures ([postfix](#postfix): **_d**) - **Shading (*R* � metalness, *G* � roughness, *B* � specular)** � for 3-channel [shading](../../content/materials/library/mesh_base/index.md#texture_shading) textures ([postfix](#postfix): **_sh**) - **Shading (*R* � metalness, *G* � roughness, *B* � specular, *A* � microfiber)** � for 4-channel [shading](../../content/materials/library/mesh_base/index.md#texture_shading) textures ([postfix](#postfix): **_sh**) - **Specular (*RGB* � specular, *A* � gloss)** � for 4-channel [specular](../../content/materials/library/mesh_base/index.md#texture_specular) textures ([postfix](#postfix): **_s**) - **Normal Map (RG)** � for 2-channel [normal](../../content/materials/library/mesh_base/index.md#texture_normal) textures ([postfix](#postfix): **_n**) - **Normal Map (*RG* � normals, *B* � opacity)** � for 3-channel [normal](../../content/materials/library/mesh_base/index.md#texture_normal) textures ([postfix](#postfix): **_nrgb**) > **Notice:** **Unigine Engine** expects a normal map in *DirectX* format. If your normal map is in *OpenGL* format, tick *[Invert G Channel](#invert_g)* in the import menu. As a general rule, if the lighting seems weird, try inverting the G Channel and see if it gets better. - **Ambient Occlusion** � for [ambient occlusion](../../content/materials/library/mesh_base/index.md#texture_ao) textures ([postfix](#postfix): **_a**) - **Emission** � for [emission](../../content/materials/library/mesh_base/index.md#texture_emission) textures ([postfix](#postfix): **_e**) - **Parallax** � for [parallax height maps](../../content/materials/library/mesh_base/index.md#texture_parallax) ([postfix](#postfix): **_h**) - **Mask (R)** � for 1-channel mask textures ([postfix](#postfix): **_m**) - **Mask (RG)** � for 2-channel mask textures ([postfix](#postfix): **_m**) - **Mask (RGB)** � for 3-channel mask textures ([postfix](#postfix): **_m**) - **Mask (RGBA)** � for 4-channel mask textures ([postfix](#postfix): **_m**) - **Mask For Vegetation (R)** � for 1-channel textures used as masks to distribute vegetation added as a *Grass* or *Mesh Clutter* object across the area ([postfix](#postfix): **_m**). Using the standard *Mask* preset for vegetation instead of this one may lead to incorrect results. If no preset is selected, the *Mask (R)* preset is set by default. - **Mask For Vegetation (RG)** � for 2-channel textures used as masks to distribute vegetation added as a *Grass* or *Mesh Clutter* object across the area ([postfix](#postfix): **_m**). Using the standard *Mask* preset for vegetation instead of this one may lead to incorrect results. If no preset is selected, the *Mask (RG)* preset is set by default. - **Mask For Vegetation (RGB)** � for 3-channel textures used as masks to distribute vegetation added as a *Grass* or *Mesh Clutter* object across the area ([postfix](#postfix): **_m**). Using the standard *Mask* preset for vegetation instead of this one may lead to incorrect results. If no preset is selected, the *Mask (RGB)* preset is set by default. - **Mask For Vegetation (RGBA)** � for 4-channel textures used as masks to distribute vegetation added as a *Grass* or *Mesh Clutter* object across the area ([postfix](#postfix): **_m**). Using the standard *Mask* preset for vegetation instead of this one may lead to incorrect results. If no preset is selected, the *Mask (RGBA)* preset is set by default. - **Cube Map** � for cubemap textures, that can be used for your world's [environment](../../editor2/settings/render_settings/environment/index.md#environment_settings) or for [Environment Probes](../../objects/lights/envprobe/index.md) ([postfix](#postfix): **_c**) - **Voxel Probe** � for 3D [lighting textures](../../objects/lights/voxelprobe/index.md#texture_param) used for Voxel Probes ([postfix](#postfix): **_vp**) - **Volume** � for 3D textures, that can be used for volumetric effects or color variations ([postfix](#postfix): **_v**) - **Light Map** � for 3-channel [light maps](../../editor2/node_parameters/visual_representation/index.md#surface_lightmaps) ([postfix](#postfix): **_l**) - **IES** � for IES light profile textures ([postfix](#postfix): **_ies**) - **3D LUT** � for [color correction](../../editor2/settings/render_settings/color/index.md#color_lut) textures |  |  |  |  |  |  |  |  |  |  |  |  |
| Image Type | Type of the texture to be generated. Available options are: - **2D** � 2D texture. This is the most commonly used type of texture. These textures are used in various [materials](../../content/materials/index.md) and be mapped to 3D meshes, GUI elements, etc. - **3D** � 3D texture. This type of textures can be used for volumetric effects or color variations. - **Cube** � cubemap texture. It can be used for your world's [environment](../../editor2/settings/render_settings/environment/index.md#environment_settings), [sky dome](../../content/materials/library/sky_base/index.md#option_background) or *[Environment Probe](../../objects/lights/envprobe/index.md)*. The imported cubemap will be oriented the following way: ![](cube_faces.png) The following layouts of source cubemaps are supported: \| ![](cube_faces_horizontal.png) \| ![](cube_faces_vertical.png) \| ![](cube_faces_panorama.png) \| \|---\|---\|---\| \| Horizontal cross layout \| Vertical cross layout \| Cylindrical Panorama \| - **2D Array** � array of 2D textures. These textures can be used for terrain details, etc. | ![](cube_faces_horizontal.png) | ![](cube_faces_vertical.png) | ![](cube_faces_panorama.png) | Horizontal cross layout | Vertical cross layout | Cylindrical Panorama |  |  |  |  |  |  |
| ![](cube_faces_horizontal.png) | ![](cube_faces_vertical.png) | ![](cube_faces_panorama.png) |  |  |  |  |  |  |  |  |  |  |  |
| Horizontal cross layout | Vertical cross layout | Cylindrical Panorama |  |  |  |  |  |  |  |  |  |  |  |
| Image Format | Defines the image pixel format: bit depth and channels used. Compressed formats are supported. The default format is **RGB8**. The drop-down menu contains all possible formats. However, if an unsuitable format is selected for the texture, the image would not be imported properly. For example, the normal texture accepts ATI2 files only. For more details on formats, see the description of the [texture asset format](../../editor2/assets_workflow/asset_types.md#texture). |  |  |  |  |  |  |  |  |  |  |  |  |
| Mipmap Type | Type of filtering to be used for mipmap generation. Available options are: - **Box** � choose this type to use simple box filter for mipmap generation. ![](mipmap_type_box.png) > **Notice:** If a texture contains very narrow features (e.g., lines), then aliasing artifacts may be very pronounced. In this case it might be better to choose the **Combined** option. - **Point** � choose this type to use point filtration for mipmap generation. ![](mipmap_type_point.png) - **Combine** � choose this type to get mipmaps from the source image. ![](mipmap_type_combined.png) > **Notice:** If the width and/or height of the source image are not power of 2, set the corresponding [resolution parameter](#params_resolution) to **Original**. - **Sharpen** � sharpness is applied for generated mipmaps. To configure the extent of sharpness, the following parameters are available: \| [![Click to enlarge](source_bricks.jpg)](source_bricks.jpg) \| [![Click to enlarge](mipmap_sharp_0_4.png)](mipmap_sharp_0_4.png) \| [![Click to enlarge](mipmap_sharp_1_0.png)](mipmap_sharp_1_0.png) \| \|---\|---\|---\| \| Source image 1024x1024 \| Mipmap 256x256, Intensity 0.4, Radius 1 \| Mipmap 256x256, Intensity 1.0, Radius 1 \| - **Sharpness Intensity** � intensity of the sharpness effect. - **Sharpness Radius** � radius to which the effect is applied, with sub-texel accuracy. - **Sharp Only Lightness** � only the HSL lightness value is affected by the sharpness effect. - **Blur** � blurring is applied for generated mipmaps. To configure the extent of blurring, the following parameter is available: \| [![Click to enlarge](source_bricks.jpg)](source_bricks.jpg) \| [![Click to enlarge](mipmap_blur_1.png)](mipmap_blur_1.png) \| [![Click to enlarge](mipmap_blur_3.png)](mipmap_blur_3.png) \| \|---\|---\|---\| \| Source image 1024x1024 \| Mipmap 256x256, Blur Radius 1 \| Mipmap 256x256, Blur Radius 3 \| - **Blur Radius** � radius, in texels, to which the effect is applied. | [![Click to enlarge](source_bricks.jpg)](source_bricks.jpg) | [![Click to enlarge](mipmap_sharp_0_4.png)](mipmap_sharp_0_4.png) | [![Click to enlarge](mipmap_sharp_1_0.png)](mipmap_sharp_1_0.png) | Source image 1024x1024 | Mipmap 256x256, Intensity 0.4, Radius 1 | Mipmap 256x256, Intensity 1.0, Radius 1 | [![Click to enlarge](source_bricks.jpg)](source_bricks.jpg) | [![Click to enlarge](mipmap_blur_1.png)](mipmap_blur_1.png) | [![Click to enlarge](mipmap_blur_3.png)](mipmap_blur_3.png) | Source image 1024x1024 | Mipmap 256x256, Blur Radius 1 | Mipmap 256x256, Blur Radius 3 |
| [![Click to enlarge](source_bricks.jpg)](source_bricks.jpg) | [![Click to enlarge](mipmap_sharp_0_4.png)](mipmap_sharp_0_4.png) | [![Click to enlarge](mipmap_sharp_1_0.png)](mipmap_sharp_1_0.png) |  |  |  |  |  |  |  |  |  |  |  |
| Source image 1024x1024 | Mipmap 256x256, Intensity 0.4, Radius 1 | Mipmap 256x256, Intensity 1.0, Radius 1 |  |  |  |  |  |  |  |  |  |  |  |
| [![Click to enlarge](source_bricks.jpg)](source_bricks.jpg) | [![Click to enlarge](mipmap_blur_1.png)](mipmap_blur_1.png) | [![Click to enlarge](mipmap_blur_3.png)](mipmap_blur_3.png) |  |  |  |  |  |  |  |  |  |  |  |
| Source image 1024x1024 | Mipmap 256x256, Blur Radius 1 | Mipmap 256x256, Blur Radius 3 |  |  |  |  |  |  |  |  |  |  |  |
| Mipmaps SRGB Correction | Enables sRGB gamma correction for mipmaps. |  |  |  |  |  |  |  |  |  |  |  |  |


## Resolution Parameters


| Width | Texture width (a power of 2). - **Original** � source image width is used. - **Auto** (default) � the power of 2 value closest to the source image width is used. |
|---|---|
| Height | Texture height (a power of 2). - **Original** � source image height is used. - **Auto** (default) � the power of 2 value closest to the source image height is used. |


> **Notice:** If the original width or height is not equal to a power of 2 and is selected as an import setting, the imported texture would fail to be compressed.


## Other Parameters


| Invert G Channel | Enable inversion of the green channel of the imported image. Depending on the game engine or 3D software package you use, normal maps can be handled differently. This option is used to simplify conversion of normal maps from different source platforms. ![](invert_green.jpg) |
|---|---|


## Texture Postfixes


Texture postfix is important, as it defines compression algorithms and color channels to be used. Postfixes correspond to certain [texture presets](#texture_preset). The list of available postfixes includes the following ones:


- texture_**alb** for [albedo](../../content/materials/library/mesh_base/index.md#texture_albedo) textures (*RGB* � color, *A* � opacity). Other possible postfixes are: *_al, _albedo, _albedomap, _albedo_map, _albedotexture, _albedo_texture, _col, _color, _colormap, _color_map, _colortexture, _color_texture*.
- texture_**d** for [diffuse](../../content/materials/library/mesh_base/index.md#texture_diffuse) textures (*RGB* � color, *A* � opacity). Other possible postfixes are: *_d, _dif, _diff, _diffuse, _diffusemap, _diffuse_map, _diffusetexture, _diffuse_texture*.
- texture_**n** for [normal](../../content/materials/library/mesh_base/index.md#texture_normal) textures (*RG* � surface normal components). Other possible postfixes are: *_nrm, _norm, _nrml, _normal, _normalmap, _normal_map, _normaltexture, _normal_texture*.
- texture_**nrgb** for [normal](../../content/materials/library/mesh_base/index.md#texture_normal) textures that store opacity in the B channel (*RG* � normals, *B* � opacity).
- texture_**s** for [specular](../../content/materials/library/mesh_base/index.md#texture_specular) textures (*RGB* � specular, *A* � gloss). Other possible postfixes are: *_sp,_ spec, _specular, _specularmap, _specular_map, _speculartexture, _specular_texture*.
- texture_**sh** for [shading](../../content/materials/library/mesh_base/index.md#texture_shading) textures (*R* � metalness, *G* � roughness, *B* � specular, *A* � microfiber).
- texture_**a** for [ambient occlusion](../../content/materials/library/mesh_base/index.md#texture_ao) textures (*R* � AO map). Other possible postfixes are: *_ao, _oc, _aomap, _ao_map, _aotexture, _ao_texture, _ambient, _occlusion, _aocclusion, _occlusionmap, _occlusion_map, _occlusiontexture, _occlusion_texture, _ambientocclusion, _ambient_occlusion*.
- texture_**h** for [parallax height maps](../../content/materials/library/mesh_base/index.md#texture_parallax) (parallax effect) (*R* � height map). Other possible postfixes are: *_p, _pa, _par, _parallax, _parallaxmap, _parallax_map, _parallaxtexture, _parallax_texture, _height, _heightmap, _height_map, _heighttexture, _height_texture, _dis, _disp, _displacement, _displacementmap, _displacement_map, _displacementtexture, _displacement_texture*.
- texture_**l** for [light](../../editor2/node_parameters/visual_representation/index.md#surface_lightmaps) maps (*RGB* � light color).
- texture_**e** for [emission](../../content/materials/library/mesh_base/index.md#texture_emission) textures (*RGB* � glow color). Other possible postfixes are: *_em, _emis, _emission, _emmap, _em_map, _emtexture, _em_texture, _emissionmap, _emission_map, _emissiontexture, _emission_texture*.
- texture_**m** for image mask textures, including those used to distribute vegetation across the area.
- texture_**c** for cubemap textures used as the world [environment](../../editor2/settings/render_settings/environment/index.md#environment_settings) or [environment probe](../../objects/lights/envprobe/index.md).
- texture_**vp** for 3D [lighting textures](../../objects/lights/voxelprobe/index.md#texture_param) used for voxel probes.
- texture_**v** for 3D textures used for volumetric effects or color variations.
- texture_**ies** for IES light profile textures.


You can define default import options for a texture by simply adding a postfix to its name.


> **Notice:** When you import a texture with a postfix, make sure that it corresponds to the texture's type and purpose. E.g. if you name an albedo texture as "`color_n.jpg`", it will be imported as a 2-channel normal map by default.


## Assigning Imported Texture


To assign the imported texture to a material, you can choose one of the following ways:


- Drag the icon of the texture asset from the *Asset Browser* window to the destination field in the *[Parameters](../../editor2/interface/index.md#parameters)* window. ![](drag_image.png)
- Use the button next to the destination field in the *Parameters* window to select the desired asset. ![](texture_select_asset.png)
- Type the name of the asset to the destination field in the *Parameters* window manually. If an asset with the specified name exists in the project it will be shown while you type. ![](typing_asset_name.gif)


## Texture Conversion


Texture Conversion is a feature that allows optimizing a texture at a later stage of the project without changing the asset GUID, thus preserving all necessary links. Any texture asset used in your project can be converted to one of the available formats.


To convert a texture, right-click the texture in the *Asset Browser* to open the context menu, and select **Convert To** and the required file format. The file immediately will be converted to a selected format.


![](texture_conversion.png)
