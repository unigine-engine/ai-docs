# Textures Optimization


Textures are often the most frequently used and the most memory-consuming assets. Big projects with a huge number of assets have to face the optimization stage to improve performance and have acceptable FPS.


An overview of the project's bottlenecks is given by *[Performance Profiler](../../../tools/profiling/profiler/index.md#render)*. By using the *Rendering Performance Profiler*, you can estimate the amount of video memory consumed by textures.


![](profiler.png)

*The output ofRendering Profiler*


Adjust the global **[Textures Settings](../../../editor2/settings/render_settings/textures/index.md)** to quickly choose the desired **Quality** or **Maximum Resolution** of all textures in the project and thus decrease the video memory consumption. Mipmaps of lower resolution are used for rendering textures of lower quality.


![](../../../editor2/settings/render_settings/textures/textures.png)


## Asynchronous Streaming


[Asynchronous Data Streaming](../../../principles/data_streaming/index.md) of graphic resources ensures smooth texture loading without spikes and other impacts on performance at the first moments of run time.


> **Notice:** Make sure asynchronous texture streaming is enabled for your world:
> - In **UnigineEditor**, open the [*Settings*](../../../editor2/settings/render_settings/index.md) window and go to the [*Streaming*](../../../editor2/settings/render_settings/streaming/index.md) section. Here you can check and switch the streaming mode for textures, if necessary.
> - In the **console**, run the [`render_streaming_textures_mode`](../../../code/console/index.md) command.


For the texture streaming optimization, you can enable texture mipmap loading, which significantly improves performance by reducing the memory consumption of texture streaming. This feature allows for the correct mipmap to be loaded at the current moment. When mipmaps loading is enabled, the textures that are not currently in use are unloaded.


To enable and configure mipmaps loading via UnigineEditor, do the following:


1. Open the *Settings* window and go to the *Streaming* section.
2. Toggle on the *Mipmaps* flag and specify the required *Mipmaps Density*.


> **Notice:** You can do the same via the console using the `render_streaming_textures_mipmaps` and `render_streaming_textures_mipmaps_density` commands.


*Mipmaps Density* sets the density of mipmaps relative to the screen resolution and helps to define which mipmap should be loaded at the current moment. You can specify different values for different quality presets. For example, you can set the density to less than 1 for the low-quality preset. In this case, the engine will load the low-resolution mipmaps, and the textures will look blurry.


Additionally, you may need to configure the *[Texture Streaming Density Multiplier](../../../editor2/materials_settings/index.md#texture_streaming_density_multiplier)* for each texture in some materials to achieve the desired visual effect.


## Texture Formats


You can control each texture asset in its [Import Parameters](../../../editor2/assets_workflow/texture_import.md).


![](../../../editor2/assets_workflow/import_texture.png)


It is usually inappropriate to use textures with the **[Unchanged](../../../editor2/assets_workflow/texture_import.md#unchanged)** option enabled unless they have the `*.dds` or `*.texture` format. Otherwise, compression may affect the color data a lot (like with custom *hdri* textures).


It is crucial to use the correct [Texture Preset](../../../editor2/assets_workflow/texture_import.md#texture_preset) for every texture, depending on its applicability. Thus, you ensure to use only needed channels and apply a proper compression algorithm. If the list does not provide a required preset, you can select the ***Custom*** option and choose the needed options.


You can also manually select the desired resolution of the texture in the [Import Options](../../../editor2/assets_workflow/texture_import.md#params_resolution).


## Texture Profiler


To clearly understand which assets can be optimized or deleted, **[Texture Profiler](../../../editor2/assets_optimize/content_profiler/texture_profiler.md)** is used. Using this tool, you can see how much memory every texture used in the project takes, easily find it in Asset Browser, and delete or resize it.


To open the *Texture Profiler* window, choose *Tools -> Content Profiler* on the Menu Bar of UnigineEditor and switch to the *Textures* tab. By using the ***Location*** switch, you can choose to inspect the textures either from the entire video memory or only the ones displayed in the Editor viewport at the moment.


![](../../../editor2/assets_optimize/content_profiler/texture_profiler.png)


*Texture Profiler* allows sorting by path, extension, occupied RAM or Video Memory size, format, or resolution.


## Visual Debugging


Find more tools for texture optimization in the *[Rendering Debug](../../../editor2/rendering_debug/index.md) Panel*. *[Texture Max Pixel Count](../../../content/optimization/textures/index.md#texture_pixel_count)* and *[Texture Screen Density](../../../content/optimization/textures/index.md#texture_screen_density)* visualizers help you quickly assess and balance texture usage in your scenes.


### Texture Max Pixel Count


Paints surfaces depending on maximum resolution of textures used in materials assigned to them applying colors in accordance with the scale.


![](pixel_count_1_off.jpg) ![](pixel_count_1_on.jpg)


![](pixel_count_2_off.jpg) ![](pixel_count_2_on.jpg)


### Texture Screen Density


Enables you to estimate the relationship between maximum texture resolution of the material to the size of triangles on the screen to which it is applied:


- **Blue areas** indicate insufficient texture resolution.
- **Green areas** - the texture density is optimal.
- **Yellow areas** highlight excessive resolution.

     Sorry, your browser does not support embedded videos.
