# Dynamic Reflections


This section contains rendering settings of dynamic reflections.


![](dynamic_reflections.png)

*Dynamic reflections settings*


| Enabled | The value indicating if dynamic reflections for materials are enabled. **enabled** by default. `Console access:render_reflection_dynamic` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_reflection_dynamic)) |
|---|---|
| Distance-Based Resolution | The value indicating if reduction of resolution of dynamic reflections when the camera moves away is enabled. **enabled** by default. `Console access:render_reflection_lods` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_reflection_lods)) |
| Roughness Offset | The value indicating whether roughness offset is enabled for dynamic reflections produced by *Environment Probes*. Sometimes, when specular highlights from glossy surfaces get into dynamic *Environment Probes* a very bright flickering of lighting from it may appear. This option makes surrounding materials look more matte for an *Environment Probe* than they actually are, reducing such flickering artefacts. **disabled** by default. `Console access:render_reflection_dynamic_roughness_offset` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_reflection_dynamic_roughness_offset)) |
| LOD Smooth Fading | The value indicating if [alpha-blend fading](../../../../principles/world_management/index.md#fading) (dithering) is enabled for surfaces inside the dynamic reflections when switching between LODs. This feature may be disabled to save performance, but in this case surfaces rendered in dynamic reflections will pop in and pop out. **disabled** by default. `Console access:render_reflection_dynamic_alpha_fade` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_reflection_dynamic_alpha_fade)) |
