# Indirect Diffuse


This tab contains global illumination indirect diffuse settings known as Screen-Space Ray-Traced Global Illumination (SSRTGI).


![Screen Space Ray-Traced Global Illumination Settings](indirect_diffuse.png)


## SSRTGI Parameters


The **SSRTGI** technology is a set of screen-space ray tracing techniques with the real-time performance level. The technology doesn't require light baking, so every object can be freely moved. In other words, SSRTGI is real-time global illumination in the screen space.


The technique implements real ray-tracing through each pixel of the screen, with a given number of rays and a specified accuracy of obstacle detection (the accuracy is set by using [steps](#ssrtgi_num_steps)). Such ray-tracing is used for Ambient Occlusion (*[SSAO](../../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssao/index.md)*) to make more realistic shadows between objects, for *[Bent Normals](../../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/bent_normal/index.md)* to smooth ambient lighting on edges, and for *[SSGI](../../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssgi/index.md)* to recreate light reflections from the object's surfaces.


> **Notice:** For the technique to take an effect, the *SSRTGI* (Screen Space Ray-Traced Global Illumination) feature must be enabled (*Rendering -> Features -> SSRTGI*).


| Preset | The index of the SSRTGI (Screen-Space Ray-Traced Global Illumination) preset used at the moment. To customize the SSRTGI effect options at run time you should activate the **Custom** preset: One of the following values: - Disabled (by default) - Low - Medium - High - Ultra - Extreme - Custom `Console access:render_ssrtgi_preset` ([API control](../../../../../api/library/rendering/class.render_cpp.md#render_ssrtgi_preset)) |
|---|---|


> **Notice:** Presets override user-defined custom settings. When any preset other than Custom is active, modification of the parameters via [API](../../../../../api/library/rendering/class.render_cpp.md) has no effect. The parameter value set via the last API call shall be used only when the Custom preset is active. When checking the current parameter value via API you'll get the corresponding setting stored in the active preset (default or custom one).


### Customizable Settings


The following settings are available when the [Custom](#ssrtgi_preset) preset is selected.


![SSRTGI custom settings](ssrtgi_custom.png)

*SSRTGI Settings*


| Fast Tracing | The value indicating if fast tracing is enabled for the SSRTGI (Screen Space Ray-Traced Global Illumination). This option dynamically changes step size to obtain indirect illumination bounces using low number of steps while keeping performance high. Disabling this option improves quality, but significantly reduces performance. SSRTGI must be enabled*[SSRTGIPreset](#render_ssrtgi_preset)*. **enabled** by default. `Console access:render_ssrtgi_fast_tracing` ([API control](../../../../../api/library/rendering/class.render_cpp.md#render_ssrtgi_fast_tracing)) |
|---|---|
| Increased Accuracy | The value indicating if increased accuracy is enabled for the SSRTGI (Screen Space Ray-Traced Global Illumination). This option reduces visual artifacts by increasing accuracy of the last step. SSRTGI must be enabled*[SSRTGIPreset](#render_ssrtgi_preset)*. **enabled** by default. `Console access:render_ssrtgi_increased_accuracy` ([API control](../../../../../api/library/rendering/class.render_cpp.md#render_ssrtgi_increased_accuracy)) |
| Resolution | The resolution of the SSRTGI (screen space ray-traced global illumination) effect. This option significantly affects performance. At low values, edges of objects become blurred. SSRTGI must be enabled*[SSRTGIPreset](#render_ssrtgi_preset)*. One of the following values: - *Quarter* - quarter resolution - *Half* - half resolution (by default) - *Full* - full resolution `Console access:render_ssrtgi_resolution` ([API control](../../../../../api/library/rendering/class.render_cpp.md#render_ssrtgi_resolution)) |
| Resolution Depth | The resolution of the depth buffer used for SSRTGI (screen space ray-traced global illumination) calculation. This option significantly affects performance. To gain performance this option can be set to lower values while enabling the increased accuracy*[SSRTGIIncreasedAccuracy](#render_ssrtgi_increased_accuracy)*. SSRTGI must be enabled*[SSRTGIPreset](#render_ssrtgi_preset)*. One of the following values: - *Quarter* - quarter resolution (by default) - *Half* - half resolution - *Full* - full resolution `Console access:render_ssrtgi_resolution_depth` ([API control](../../../../../api/library/rendering/class.render_cpp.md#render_ssrtgi_resolution_depth)) |
| Num Rays | The number of rays of SSRTGI per pixel that are used to calculate the final image. Using more rays provides more precise SSRTGI calculation, however, it is more expensive. SSRTGI must be enabled*[SSRTGIPreset](#render_ssrtgi_preset)*. Range of values: **[1, 1024]**. The default value is : **8**. `Console access:render_ssrtgi_num_rays` ([API control](../../../../../api/library/rendering/class.render_cpp.md#render_ssrtgi_num_rays)) |
| Num Steps | The number of steps of SSRTGI per ray that are used for trace calculation. The higher the value, the more accurate obstacles between objects are accounted. However, this option significantly affects performance. SSRTGI must be enabled*[SSRTGIPreset](#render_ssrtgi_preset)*. Range of values: **[1, 256]**. The default value is : **8**. `Console access:render_ssrtgi_num_steps` ([API control](../../../../../api/library/rendering/class.render_cpp.md#render_ssrtgi_num_steps)) |
| Step Size | The size of the trace step used for SSRTGI calculation. The higher the value, the longer the trace. However, tiny objects may be missed. The lower the value, the more detailed will be the tiny objects. The SSRTGI effect must be enabled*[SSRTGIPreset](#render_ssrtgi_preset)*. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_ssrtgi_step_size` ([API control](../../../../../api/library/rendering/class.render_cpp.md#render_ssrtgi_step_size)) |
