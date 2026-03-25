# Tessellation


This section contains settings for tessellation. Mesh tessellation subdivides low-poly surfaces into finer meshes, to achieve higher visual quality (add more details) for a lower rendering cost.


![](tessellation.png)

*Tessellation Settings*


| Density Multiplier | The global [Density](../../../../content/materials/library/mesh_base/index.md#tessellation_density) multiplier for the adaptive hardware-accelerated tessellation. *Higher* values produce *denser* meshes. Range of values: **[0.0f, 10.0f]**. The default value is : **1.0f**. `Console access:render_tessellation_density_multiplier` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_tessellation_density_multiplier)) |
|---|---|
| Distance Multiplier | The global multiplier for all [distance](../../../../content/materials/library/mesh_base/index.md#tessellation_distance_falloff_near) parameters of the adaptive hardware-accelerated tessellation used for distance-dependent optimization. *Higher* values make tessellation visible at longer distances from the camera (consuming more resources). Range of values: **[0.0f, 10.0f]**. The default value is : **1.0f**. `Console access:render_tessellation_distance_multiplier` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_tessellation_distance_multiplier)) |
| Shadow Density Multiplier | The global [Shadow Density](../../../../content/materials/library/mesh_base/index.md#tessellation_density_shadow) multiplier for the Tessellated Displacement effect. *Higher* values produce more detailed shadows. You can make shadows from tessellated meshes simpler to save performance. Range of values: **[0.01f, 10.0f]**. The default value is : **1.0f**. `Console access:render_tessellation_shadow_density_multiplier` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_tessellation_shadow_density_multiplier)) |
