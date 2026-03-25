# volume_shaft_base


A *volume_shaft_base* material is used to create beams of light falling into a dark room through windows or any other openings. In case colored glass is used for windows, beams also will be colored.


This material is applied only to [Volume boxes](../../../../objects/effects/volumetrics/volume_box.md).


![Volume shaft material](shaft.jpg)

*Volume shaft material*


## States


![States](states.png)

*Material Settings, States Tab*


### Height


This state determines if the intensity of light shafts reduces depending on height. By default this state is disabled. This state enables the [**Falloff**](#falloff) parameter.


### Camera position based


This state determines if light shafts are to be rendered relative to current camera position. By default this state is disabled. This state enables the [**Radius**](#radius) parameter.


## Textures


![](textures.png)

*Material Settings, Textures Tab*


### Noise Texture


Noise map. A texture to be rendered in the screen space and add a noise pattern to the beam. The texture is 1-channelled (R).


## Parameters


![Parameters](parameters.png)

*Material Editor,Parameterstab.*


### Base Parameters


- **Diffuse** - Determines the diffuse color multiplier for light shafts. ![](diffuse_white.jpg) ![](diffuse_green.jpg)


### Density Parameters


- **Power** - Determines the sharpness of volumetric bounds. By the minimum value of 1 the volumetric bounds are smoooth. The higher the value the sharper are the bounds. ![](power_1.jpg) ![](power_100.jpg)
- **Multiplier** - Determines the density scale of the environment. ![](multiplier_002.jpg) ![](multiplier_006.jpg)
- **Falloff** - Determines the reduction of intensity of light rays depending on height. > **Notice:** This parameter is available only when the [Height](#height) state is enabled. ![](falloff_002.jpg) ![](falloff_0044.jpg)
- **Radius** - Determines the visibility distance of the rays, measured from the camera position, in meters. > **Notice:** This parameter is available only when the [Camera position based](#camera_position_based) state is enabled. ![](radius_30.jpg) ![](radius_90.jpg)


### Other Parameters


- **Rays jitter** - Determines smoothness of light rays. The higher the value, the smoother the rays. ![](rays_jitter_0.jpg) ![](rays_jitter_1.jpg)
- **Step jitter** This parameter can be used to remove banding effect and make the rays look smoother. The higher the value, the smoother the rays. ![](step_jitter_0.jpg) ![](step_jitter_1.jpg)
- **Bias** This parameter shifts shadow in the light direction to remove banding effect in case of insufficient shadow resolution. ![](bias_0.jpg) ![](bias_1.jpg)
- **Samples** - Number of depth samples used. The more samples, the higher is the quality. > **Notice:** To increase performance, use low Sample values. ![](samples_16.jpg) ![](samples_64.jpg)
- **View intensity** - Determines the intensity of rays when view direction is the same as the direction of the light rays (looking away from the light source). The higher the value, the more pronounced the rays look. ![](view_intensity_06.jpg) ![](view_intensity_1.jpg)
- **View exponent** - Determines the rate of change of the intensity of rays when view direction is the same as the direction of the light rays (looking away from the light source). The higher the value, the smoother is the change of intensity. ![](view_exponent_0001.jpg) ![](view_exponent_1.jpg)
