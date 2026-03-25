# SSAO


This section contains settings related to screen-space ambient occlusion (SSAO).


## Customizable Settings


The following settings are available when the [Custom](../../../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/index.md#ssrtgi_preset) preset is selected for SSRTGI.


![SSAO custom settings](ssao.png)

*Screen-Space Ambient Occlusion Settings*


| Enabled | The value indicating if the [SSAO](../../../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssao/index.md) (Screen Space Ambient Occlusion) effect is enabled. **enabled** by default. `Console access:render_ssao` ([API control](../../../../../../api/library/rendering/class.render_cpp.md#render_ssao)) |
|---|---|
| Intensity | The [intensity](../../../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssao/index.md#ssao_intensity) of the SSAO (Screen Space Ambient Occlusion) for the scene. The intensity value affects brightness of shadows: by the minimum value of 0.0f, the ambient occlusion shadowing is the lightest. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_ssao_intensity` ([API control](../../../../../../api/library/rendering/class.render_cpp.md#render_ssao_intensity)) |
| Intensity Reflection | The intensity of SSAO (Screen Space Ambient Occlusion) on reflections. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_ssao_intensity_reflection` ([API control](../../../../../../api/library/rendering/class.render_cpp.md#render_ssao_intensity_reflection)) |
| Cavity | The value indicating if the cavity option for the SSAO (Screen Space Ambient Occlusion) effect is enabled. This option improves (sharpens) the look of junction contours at low resolutions, so it should be used for detail enhancement (small stones, bolts and so on). > **Notice:** When checking the parameter value via API, you'll get the corresponding setting stored in the active preset (default or custom one). **enabled** by default. `Console access:render_ssao_cavity` ([API control](../../../../../../api/library/rendering/class.render_cpp.md#render_ssao_cavity)) |
| Cavity Intensity | The intensity of sharpening of contours for the cavity option*[SSAOCavity](#render_ssao_cavity)*. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_ssao_cavity_intensity` ([API control](../../../../../../api/library/rendering/class.render_cpp.md#render_ssao_cavity_intensity)) |
| Cavity Radius | The size of junction contours area for the cavity option for the SSAO (Screen Space Ambient Occlusion) effect*[SSAOCavity](#render_ssao_cavity)*. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_ssao_cavity_radius` ([API control](../../../../../../api/library/rendering/class.render_cpp.md#render_ssao_cavity_radius)) |
| Threshold | The threshold value for the SSAO (Screen Space Ambient Occlusion) effect. It limits SSAO in areas where information cannot be obtained. The *higher* the value, the less pronounced the effect is. Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**. `Console access:render_ssao_threshold` ([API control](../../../../../../api/library/rendering/class.render_cpp.md#render_ssao_threshold)) ![](ao_threshold_0.jpg) ![](ao_threshold_1.jpg) |
