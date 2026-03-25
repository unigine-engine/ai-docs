# Textures


This section contains texture-related settings.


![Textures settings](textures.png)

*Textures Settings*


### Common Settings


> **Notice:** Settings listed below affect all textures except for reflection cubemaps, depth textures used for shadows, and 3D textures used by voxel probes.


| Quality | The resolution of textures. One of the following values: - *Low* - low quality - *Medium* - medium quality - *High* - high quality (by default) `Console access:render_textures_quality` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_textures_quality)) |
|---|---|
| Min Resolution | The minimum resolution of all textures. The Engine doesn't compress existing textures: it uses specified mip maps of `*.dds` textures. One of the following values: - 128x128 (by default) - 256x256 - 512x512 - 1024x1024 - 2048x2048 - 4096x4096 - 8192x8192 - 16384x16384 `Console access:render_textures_min_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_textures_min_resolution)) |
| Max Resolution | The maximum resolution of all textures. the engine doesn't compress existing textures: it uses specified mipmaps of `*.dds` textures. One of the following values: - 128x128 - 256x256 - 512x512 - 1024x1024 - 2048x2048 - 4096x4096 - 8192x8192 (by default) - 16384x16384 `Console access:render_textures_max_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_textures_max_resolution)) |
| Filter | The texture filtering mode. One of the following values: - Bilinear - Trilinear (by default) `Console access:render_textures_filter` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_textures_filter)) |
| Anisotropy | The anisotropy level for textures (degree of anisotropic filtering). One of the following values: - level 1 - level 2 - level 4 - level 8 (by default) - level 16 `Console access:render_textures_anisotropy` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_textures_anisotropy)) |
