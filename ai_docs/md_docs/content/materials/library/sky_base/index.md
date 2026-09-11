# sky_base


A *sky_base* material is used for the [sky objects](../../../../objects/objects/sky/index.md).


## States


![](states.png)


### Options


#### Background


Enables a [cube map](../../../../editor2/assets_workflow/texture_import.md#image_type) texturing of the sky sphere. This option allows using sky dome environment maps, for example, to create a night sky with stars.


The following values are available:

- **None** � a background texture is not used.
- **Single** � one background texture is used.
- **Double** � two background textures are used.


#### Clouds


Specifies if the procedural clouds will be rendered.


## Textures


![](textures.png)


### Clouds Textures


The following textures create textured sky sphere clouds and are modified in the **Clouds** section of the Textures tab.


#### Mask 0


Mask for the 1st upper cloud layer. The texture is 4-channelled (RGBA).


#### Mask 1


Mask for the 2nd lower cloud layer. The texture is 4-channelled (RGBA).


#### Clouds 01


Noise texture for the 1st upper cloud layer. The texture is 4-channelled (RGBA).


#### Clouds 23


Noise texture for the 2nd lower cloud layer. The texture is 4-channelled (RGBA).


#### Sky Sphere Color Calculation


The color of the textured sky sphere is calculated in three steps:

1. The upper layer of the clouds, **[Clouds�01](#texture_clouds_01)**, is computed:

  1. For the first layer, two texture transformations ([**Clouds 0**](#parameter_clouds_0) and [**Clouds 1**](#parameter_clouds_1)) are summed.
  2. [**Mask 0**](#parameter_mask_0) is multiplied by the [**Threshold 01**](#parameter_threshold_01), modulating the strength of masking.
  3. The mask is subtracted from the textures transformation sum.
  4. The color intensity of the resulting **Clouds�01** layer is computed by multiplying it by the [**Clouds�01**](#parameter_clouds_01) parameter value.
2. The lower layer of the clouds, **[**Clouds�23**](#texture_clouds_23)**, is computed in the same way:

  1. For the second layer, two texture transformations ([**Clouds 2**](#parameter_clouds_2) and [**Clouds 3**](#parameter_clouds_3)) are summed.
  2. [**Mask 1**](#parameter_mask_1) is multiplied by the [**Threshold 23**](#parameter_threshold_23), modulating the strength of masking.
  3. The mask is subtracted from the textures transformation sum.
  4. The color intensity of the resulting **Clouds�23** layer is computed by multiplying it by the [Clouds�23](#parameter_clouds_23) parameter value.
3. The rendered clouds are adjusted by the [**Sphere**](#parameter_sphere) value that controls the influence of atmospheric scattering on the clouds.


### Background Textures


These textures are present if the [Background](#option_background) option selected in the *States* tab.


#### Background 0


A cube map for texturing the sky sphere with a static texture. The texture is 4-channelled (RGBA).


#### Background 1


A second cube map for texturing the sky sphere with a static texture. The texture is 4-channelled (RGBA).


## Parameters


In the *Parameters* tab you can set or modify base and additional parameters.


![](parameters.png)


### Transformation Parameters


Textures transformation parameters are modified in the **Transform** section of the *Parameters* tab.


#### Sphere


Transformation of the sky sphere:

- The first two components scale the sphere by *X* and *Y*, respectively. They affect the circle of a horizon.
- The third component scales the sphere by *Z*, making the sky look higher or lower.
- The fourth component offsets the sphere vertically. Positive values move the sphere down, negative values move it up. This can be used to remove cloud artefacts near the horizon.


#### Mask 0


Transformation of the mask texture *mask_0*.


#### Mask 1


Transformation of the mask texture *mask_1*.


#### Clouds 0


First transformation of the cloud texture *clouds_01*.


#### Clouds 1


Second transformation of the cloud texture *clouds_01*.


#### Clouds 2


First transformation of the cloud texture *clouds_23*.


#### Clouds 3


Second transformation of the cloud texture *clouds_23*.


### Clouds Parameters


Clouds parameters control the appearance of textured sphere clouds. They are modified in the **Clouds** section of the *Parameters* tab.


#### Color


Color of the clouds (applied for both clouds layers).


#### Clouds 01


Color intensity of the first cloud layer:

- Decreasing the value results in cloud color fading.
- Increasing the value results in cloud color intensification.


#### Clouds 23


Color intensity of the second cloud layer:

- Decreasing the value results in cloud color fading.
- Increasing the value results in cloud color intensification.


#### Threshold 01


Coefficient modulating the strength of masking of the first mask:

- Decreasing the value determines a weakened attenuation by the mask and abundant clouds.
- Increasing the value determines an intensive attenuation by the mask and sparse clouds.


#### Threshold 23


Coefficient modulating the strength of masking of the second mask:

- Decreasing the value determines a weakened attenuation by the mask and abundant clouds.
- Increasing the value determines an intensive attenuation by the mask and sparse clouds.


### Sphere Parameters


Sphere parameters are modified in the **Sphere** section of the *Parameters* tab. **Background 0** and **Background 1** parameters are present only if **[Background](#option_background)** option is set to **Single** or **Double** mode respectively.


#### Background 0


Color multiplier for the first background texture:

- Decreasing the value results in dark and unsaturated color.
- Increasing the value results in light and very saturated color.


#### Background 1


Color multiplier for the second background texture.
