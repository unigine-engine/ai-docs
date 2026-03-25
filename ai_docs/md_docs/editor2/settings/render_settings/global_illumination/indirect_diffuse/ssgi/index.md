# SSGI


This section contains settings related to Screen-Space Global Illumination (SSGI).


## Customizable Settings


The following settings are available when the [Custom](../../../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/index.md#ssrtgi_preset) preset is selected for SSRTGI.


![SSGI custom settings](ssgi.png)

*Screen-Space Global Illumination Settings*


| Enabled | The value indicating if the [SSGI](../../../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssgi/index.md) (Screen Space Global Illumination) effect is enabled. **disabled** by default. `Console access:render_ssgi` ([API control](../../../../../../api/library/rendering/class.render_cpp.md#render_ssgi)) |  |  |
|---|---|---|---|
| Intensity | The [intensity](../../../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssgi/index.md#ssgi_intensity) of the SSGI (Screen Space Global Illumination) for the scene. By the minimum value of 0.0f, the global illumination is the darkest. Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**. `Console access:render_ssgi_intensity` ([API control](../../../../../../api/library/rendering/class.render_cpp.md#render_ssgi_intensity)) \| ![Intensity = 0.2](intensity02.png) *Intensity = 0.2* \| ![Intensity = 1](intensity1.png) *Intensity = 1* \| \|---\|---\| | ![Intensity = 0.2](intensity02.png) *Intensity = 0.2* | ![Intensity = 1](intensity1.png) *Intensity = 1* |
| ![Intensity = 0.2](intensity02.png) *Intensity = 0.2* | ![Intensity = 1](intensity1.png) *Intensity = 1* |  |  |
| Intensity Boost | The boost intensity value. Increases the SSGI intensity by raising the value to the specified power. One of the following values: - power of 1 (by default) - power of 2 - power of 3 - power of 4 `Console access:render_ssgi_intensity_boost` ([API control](../../../../../../api/library/rendering/class.render_cpp.md#render_ssgi_intensity_boost)) |  |  |
| Threshold | The threshold value for the ray-traced SSGI (Screen Space Global Illumination). > **Notice:** Ray-traced SSGI calculation available only when the SSRTGI technique*[SSRTGIPreset](#render_ssrtgi_preset)* is enabled. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_ssgi_threshold` ([API control](../../../../../../api/library/rendering/class.render_cpp.md#render_ssgi_threshold)) |  |  |
| Information Lost Fix | The value indicating if the information lost fix option is enabled for the ray-traced SSGI (Screen Space Global Illumination). This option removes artifacts in the information lost areas around moving objects. **disabled** by default. `Console access:render_ssgi_information_lost_fix` ([API control](../../../../../../api/library/rendering/class.render_cpp.md#render_ssgi_information_lost_fix)) |  |  |
