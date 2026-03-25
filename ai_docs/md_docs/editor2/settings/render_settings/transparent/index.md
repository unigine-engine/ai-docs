# Transparent


This section contains rendering settings of transparent materials.


![](transparent.png)

*Transparent settings*


| Enabled | The value indicating if the transparent pass is rendered. > **Notice:** This option takes effect only when the forward rendering pass is used for transparent objects rendering. **enabled** by default. `Console access:render_transparent_enabled` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_transparent_enabled)) |
|---|---|
| Deferred | The value indicating if the deferred pass for transparent objects is enabled. > **Notice:** This option takes effect only when the forward rendering pass is used for transparent objects rendering. **enabled** by default. `Console access:render_transparent_deferred` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_transparent_deferred)) |
| Blur | The value indicating if transparent blur is enabled for materials. This option makes it possible to render matte transparent materials like matte glass. **enabled** by default. `Console access:render_transparent_blur` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_transparent_blur)) |


## Refraction


| Enabled | The value indicating if refraction is enabled. **enabled** by default. `Console access:render_refraction` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_refraction)) |  |  |
|---|---|---|---|
| Warp Background Transparent Surfaces | The value indicating if refraction affects background transparent surfaces (except for water and clouds). The following values are available: - Never - no refraction distortion is applied to transparent surfaces. - Behind Farthest Refractive Surface - apply refraction distortion to all transparent surfaces behind the farthest refractive surface. This method takes effect only when rendering of refractions*[Refraction](#render_refraction)* is enabled. Option **#1** is selected by default (see above). `Console access:render_refraction_warp_background_transparent_surfaces` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_refraction_warp_background_transparent_surfaces)) |  |  |
| Refraction Red | Refraction displacement for red channel (based on the refraction texture of [refractive materials](../../../../content/materials/library/mesh_base/index.md#option_refraction)). It can be used to create light dispersion (chromatic aberrations). - By the value of **0**, there is no dispersion for refracted light in red channel. \| ![No refraction dispersion](refraction0.jpg) *No Refraction Dispersion* \| ![Refraction Red and Green](refraction1.jpg) *Dispersion Per Channel: Red = 0.8, Green = 0.9, Blue = 1* \| \|---\|---\| | ![No refraction dispersion](refraction0.jpg) *No Refraction Dispersion* | ![Refraction Red and Green](refraction1.jpg) *Dispersion Per Channel: Red = 0.8, Green = 0.9, Blue = 1* |
| ![No refraction dispersion](refraction0.jpg) *No Refraction Dispersion* | ![Refraction Red and Green](refraction1.jpg) *Dispersion Per Channel: Red = 0.8, Green = 0.9, Blue = 1* |  |  |
| Refraction Green | Refraction displacement for green channel (based on the refraction texture of [refractive materials](../../../../content/materials/library/mesh_base/index.md#option_refraction)). It can be used to create light dispersion (chromatic aberrations). - By the value of **0**, there is no dispersion for refracted light in green channel. |  |  |
| Refraction Blue | Refraction displacement for blue channel (based on the refraction texture of [refractive materials](../../../../content/materials/library/mesh_base/index.md#option_refraction)). It can be used to create light dispersion (chromatic aberrations). - By the value of **0**, there is no dispersion for refracted light in blue channel. |  |  |
