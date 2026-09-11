# Settings Nodes


Nodes with the *Settings* prefix provide access to global rendering settings from material graph.


#### Common Parameters

##### Settings Render Translucent Color

Outputs the current [Translucent Color](../../../../../editor2/settings/render_settings/sss/index.md#sss_translucent_color).

##### Settings Supersampling

Outputs the current [Number of samples per pixel](../../../../../principles/render/antialiasing/supersampling.md) used for supersampling.

##### Settings TAA

Outputs 1 if [Temporal Anti-Aliasing](../../../../../principles/render/antialiasing/taa.md) is enabled, otherwise � 0.


#### Scattering Parameters

##### Settings Environment Ambient Intensity

Outputs the [Environment ambient intensity](../../../../../editor2/settings/render_settings/environment/index.md#intensity_ambient) parameter.

##### Settings Environment Reflection Intensity

Outputs the [Environment reflection intensity](../../../../../editor2/settings/render_settings/environment/index.md#intensity_reflection) parameter.

##### Settings Environment Sky Intensity

Outputs the [Sky intensity](../../../../../editor2/settings/render_settings/environment/index.md#intensity_sky) parameter.

##### Settings Haze Color

Outputs the [color of the haze](../../../../../editor2/settings/render_settings/environment/index.md#haze_color).

##### Settings Haze Maximum Distance

Outputs the [Haze maximum visible distance](../../../../../editor2/settings/render_settings/environment/index.md#haze_max_distance).

##### Settings Haze Density

Outputs the [haze density](../../../../../editor2/settings/render_settings/environment/index.md#haze_density).

##### Settings Haze Solid

Outputs 1 if the [Environment Haze Mode](../../../../../editor2/settings/render_settings/environment/index.md#haze_mode) is set to Solid, otherwise � 0.

##### Settings Haze Visibility

Outputs 1 if haze is enabled, otherwise � 0.

##### Settings Haze Gradient

Outputs the [Environment haze gradient](../../../../../editor2/settings/render_settings/environment/index.md#haze_gradient_mode).

##### Settings Haze Physical

Outputs 1 if the [Environment Haze Mode](../../../../../editor2/settings/render_settings/environment/index.md#haze_physically_based) is set to Physical, otherwise � 0.

##### Settings Haze Physical Start Height

Outputs the [Reference height value](../../../../../editor2/settings/render_settings/environment/index.md#haze_start_height) for the two parameters ([Half Visibility Distance](../../../../../editor2/settings/render_settings/environment/index.md#haze_half_visibility_distance) and [Haze Physical Falloff](../../../../../editor2/settings/render_settings/environment/index.md#haze_half_faloff_height)).

##### Settings Haze Physical Density

Outputs the [Haze density](../../../../../editor2/settings/render_settings/environment/index.md#haze_density) for the *Physical* preset.

##### Settings Haze Physical Falloff

Outputs the [Height of the haze density gradient](../../../../../editor2/settings/render_settings/environment/index.md#haze_half_faloff_height).

##### Settings Haze Physical Zero Visibility Height

Outputs the height at which the haze completely overlaps the scene.

##### Settings Haze Physical Ambient Light Intensity

Outputs the [Intensity of the impact of the ambient lighting on haze](../../../../../editor2/settings/render_settings/environment/index.md#haze_ambient_light_intensity).

##### Settings Haze Physical Ambient Color Saturation

Outputs the [Intensity of the ambient color's contribution to the haze](../../../../../editor2/settings/render_settings/environment/index.md#haze_ambient_color_saturation).

##### Settings Haze Physical Sun Light Intensity

Outputs the [Intensity of the impact of the sunlight on haze](../../../../../editor2/settings/render_settings/environment/index.md#haze_sun_light_intensity).

##### Settings Haze Physical Sun Color Saturation

Outputs the [Intensity of the impact of the sunlight on haze](../../../../../editor2/settings/render_settings/environment/index.md#haze_sun_color_saturation).

##### Settings Haze Physical Screen Space Global Illumination

Outputs 1 if the [Screen-Space Haze Global Illumination (SSHGI)](../../../../../editor2/settings/render_settings/environment/index.md#sshgi) effect is enabled, otherwise � 0. SSHGI is a screen-space effect ensuring consistency of haze color with the current color of Global Illumination.

##### Settings Haze Scattering Mie Fresnel Power

Outputs the [Power of the Fresnel effect for Mie visibility](../../../../../editor2/settings/render_settings/environment/index.md#haze_mie_fresnel_power).

##### Settings Haze Scattering Mie Front Side Intensity

Outputs the [Falloff of the Fresnel effect for Mie intensity](../../../../../editor2/settings/render_settings/environment/index.md#haze_mie_fresnel_intensity).

##### Settings Haze Scattering Mie Intensity

Outputs the [Minimum Mie intensity value for geometry-occluded areas](../../../../../editor2/settings/render_settings/environment/index.md#haze_mie_intensity).

##### Settings Matrix Sky Transform

Outputs the sky transform matrix.

##### Settings Matrix Moon Rotation

Outputs the moon rotation matrix.

##### Settings Matrix Sun Rotation

Outputs the sun rotation matrix.

##### Settings Sky Up

Outputs the sky up vector. The coordinate space of the output value (*World, Object, Tangent, View*) can be selected with the Space dropdown parameter (double-click on the node to see the dropdown).

##### Settings Sun Color

Outputs the [Color multiplier for the Sun texture](../../../../../editor2/settings/render_settings/environment/index.md#sun_color).

##### Settings Sky Altitude

Outputs the sky altitude.


#### Tessellation Settings

##### Settings Tessellation Density Multiplier

Outputs the global [density multiplier for the adaptive hardware-accelerated tessellation](../../../../../editor2/settings/render_settings/tessellation/index.md#density).

##### Settings Tessellation Shadow Density Multiplier

Outputs the global [Shadow Density multiplier for the Tessellated Displacement effect](../../../../../editor2/settings/render_settings/tessellation/index.md#shadow_density).

##### Settings Tessellation Distance Multiplier

Outputs the global [multiplier for all distance parameters of the adaptive hardware-accelerated tessellation](../../../../../editor2/settings/render_settings/tessellation/index.md#distance) used for distance-dependent optimization.
