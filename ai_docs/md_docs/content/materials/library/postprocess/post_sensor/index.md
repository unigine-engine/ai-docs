# post_sensor


> **Warning:** This article is under development.


This postprocess material allows you to create the effects for real-time sensor simulation of optical sensors in the EO or IR passband.


The *post_sensor* material has 4 built-in child materials with predefined settings:

- *post_sensor_green* - material that is used to amplify near and far infrared emission.
- *post_sensor_heat*, *post_sensor_red* - material that is used for simulation of industrial thermal imagers.
- *post_sensor_white* - material that is used for simulation of military thermal imagers.


To apply the postprocess material, choose *Windows -> Rendering settings* (or press **Alt+R**) and specify the material name in the *Post* field.


> **Notice:** For all objects that should be visible in the IR spectrum the **Auxiliary** pass should be enabled.


![](sensors_enhanced_sm.jpg)

*post_sensor_green*


![](sensors_infrared_sm.jpg)

*post_sensor_heat*


## Main Concepts


All objects that should be visible after applying the material should have a *thermal map* specified as the **Auxiliary** texture in the object's material.


![](auxiliary_texture.png)

*Thermal map*


In case of the *post_sensor_green* material, the auxiliary texture will be used as a *glow texture*.


The **Auxiliary** texture is a 3-channel texture (RGB). Each channel stores a temperature value in range [0;255]. In the *post_sensor* material, this range is represented as [0;1]. So, the white texture stores a temperature value in range [0;3].


If the object's temperature is low (in range [0;1]), the auxiliary texture with 1 channel will be enough. For higher temperature, you should add the other channels.


### Reading Temperature from Thermal Map


The temperature value is obtained from the thermal map (the auxiliary texture) by adding the temperature values stored in the texture's channels. In parallel, the temperature value stored in each channel is multiplied by the corresponding channel of the **Auxiliary color** specified in the object's material.


*At = Rt � Ra + Gt � Ga + Bt � Ba*


However, the resulting temperature that will be rendered after applying the *post_sensor* material is calculated as follows:


*Tt = AtApower � Ascale + AOheat + ScolorSpower � Ascale + Tglobal*


Here:


| *At* | Temperature [obtained](#read_temperature) from the thermal map |
|---|---|
| *Apower* | [Auxiliary buffer power](#aux_buffer_power) |
| *Ascale* | [Auxiliary buffer scale](#aux_buffer_scale) |
| *AOheat* | [Ambient heat occlusion](#ambient_heat_occlusion) |
| *Scolor* | Scene color |
| *Spower* | [Influence scene power](#influence_scene_power) |
| *Sscale* | [Influence scene scale](#influence_scene_scale) |
| *Tglobal* | [Global temperature](#global_temperature) |


## Textures


### Vision LUT Texture


**Vision LUT** texture is used to map the sensor temperature (its values vary in range [0;1]) to the color familiar to human eyes. For example, objects with high temperature can be represented by using different gradations of the red color.


| ![](lut_green.png) | ![](lut_heat.png) |
|---|---|
| *Vision LUT texture forpost_sensor_greenmaterial* | *Vision LUT texture forpost_sensor_heatmaterial* |


The texture is 4-channeled:

1. *RGB* values store color information.
2. An *alpha (A)* value is not used.


## Parameters


### Base Parameters


#### Ambient Heat Occlusion


**Ambient heat occlusion** is a value that shows influence of SSAO on the temperature obtained from the thermal map.

- The *higher* the value, the higher the temperature in the shadowed areas (these areas will get cold more slowly).
- The *lower* the value, the lower the temperature in the shadowed areas (these areas will get cold faster).


| ![](ao_heat_low.png) | ![](ao_heat_high.png) |
|---|---|
| *Ambient heat occlusion = -0.5* | *Ambient heat occlusion = 0.5* |


#### Influence Scene Power


**Influence scene power** is a degree of impact of the scene color on the resulting temperature.

- By the value of 0, the scene color won't affect the resulting temperature.


#### Influence Scene Scale


**Influence scene scale** is a coefficient for increasing intensity of the scene color.


| ![](influence_default.png) | ![](influence_custom.png) |
|---|---|
| *Influence scene power = 2; Influence scene scale = 0.5* | *Influence scene power = 4; Influence scene scale = 1.5* |


#### Global Temperature


**Global temperature** is a global temperature of the scene that increases or decreases the resulting temperature displayed by the sensor.


| ![](global_temp_0.png) | ![](global_temp_05.png) |
|---|---|
| *Global temperature = 0* | *Global temperature = 0.5* |


#### Sensor Blur Power


**Sensor blur power** is a radius of the blur effect applied to the temperature displayed by the sensor.


| ![](blur_power_low.png) | ![](blur_power_high.png) |
|---|---|
| *Sensor blur power = 1; Sensor blur detail = 0.7* | *Sensor blur power = 4; Sensor blur detail = 0.7* |


#### Sensor Blur Detail


**Sensor blur detail** is a coefficient that allows adjusting sharpness of the blur effect.


| ![](blur_detail_low.png) | ![](blur_detail_high.png) |
|---|---|
| *Sensor blur detail = 0.3; Sensor blur power = 4* | *Sensor blur detail = 1; Sensor blur power = 4* |


#### Motion Blur Strength


**Motion blur strength** is a coefficient that controls blurring in motion (how blurred the displayed temperature will be when the camera moves).


#### Noise Count


**Noise count** is a level of the color noise.

- The *lower* the temperature in a specific area, the higher the color noise level will be.


| ![](noise_count_0.png) | ![](noise_count_03.png) |
|---|---|
| *Noise count = 0* | *Noise count = 0.3* |


#### Noise Granule Size


**Noise granule size** is a size of the color noise.


| ![](noise_count_03.png) | ![](noise_size_high.png) |
|---|---|
| *Noise granule size = 400* | *Noise granule size = 1000* |


#### Auxiliary Buffer Power


**Auxiliary buffer power** is a degree of impact of the temperature obtained from the thermal map on the resulting temperature displayed by the sensor.


| ![](aux_power_2.png) | ![](aux_power_10.png) |
|---|---|
| *Auxiliary buffer power = 2; Auxiliary buffer scale = 2* | *Auxiliary buffer power = 10; Auxiliary buffer scale = 2* |


#### Auxiliary Buffer Scale


**Auxiliary buffer scale** is a coefficient to scale the temperature obtained from the thermal map.


| ![](aux_power_2.png) | ![](aux_scale_3.png) |
|---|---|
| *Auxiliary buffer scale = 2; Auxiliary buffer power = 2* | *Auxiliary buffer scale = 3; Auxiliary buffer power = 2* |


#### Sensor LUT Shift


**Sensor LUT shift** is an offset of the resulting temperature in the vision LUT texture. This value can be used to correct mapping of the temperature to the color.


#### Sensor LUT Scale


**Sensor LUT scale** is a coefficient to scale the resulting temperature when mapping the temperature to the color.
