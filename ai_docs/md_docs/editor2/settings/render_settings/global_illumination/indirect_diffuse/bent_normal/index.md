# Bent Normal


This section contains settings related to bent normals.


## Customizable Settings


The following settings are available when the [Custom](../../../../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/index.md#ssrtgi_preset) preset is selected for SSRTGI.


![Bent Normal custom settings](bent_normal.png)

*Bent Normal Settings*


| Enabled | The value indicating if ray-traced bent normals calculation is enabled. The use of SSRTGI for bent normals allows for smooth ambient lighting. > **Notice:** Ray-traced bent normals calculation available only when the SSRTGI technique*[SSRTGIPreset](#render_ssrtgi_preset)* is enabled. **disabled** by default. `Console access:render_bent_normal` ([API control](../../../../../../api/library/rendering/class.render_cpp.md#render_bent_normal)) ![](ssrtgi_bent_normals_off.jpg) ![](ssrtgi_bent_normals_on.jpg) |
|---|---|
| Threshold | The threshold value for the ray-traced bent normals calculation. > **Notice:** Ray-traced bent normals calculation is available only when the SSRTGI technique*[SSRTGIPreset](#render_ssrtgi_preset)* is enabled. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_bent_normal_threshold` ([API control](../../../../../../api/library/rendering/class.render_cpp.md#render_bent_normal_threshold)) ![](ssrtgi_bent_normals_threshold_0.jpg) ![](ssrtgi_bent_normals_denoise_on.jpg) |
| Fix Overlit Areas | The value indicating if correction of overlit areas for bent normals calculation is enabled. > **Notice:** - This option may significantly affect performance, so disable it when it's not necessary. > - Ray-traced bent normals calculation is available only when the SSRTGI technique*[SSRTGIPreset](#render_ssrtgi_preset)* is enabled. **disabled** by default. `Console access:render_bent_normal_fix_overlit_areas` ([API control](../../../../../../api/library/rendering/class.render_cpp.md#render_bent_normal_fix_overlit_areas)) ![](ssrtgi_bent_normals_fix_overlit_off.jpg) ![](ssrtgi_bent_normals_fix_overlit_on.jpg) |
