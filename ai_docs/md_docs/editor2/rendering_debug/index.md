# Using Visual Debugging


The *Rendering Debug* panel provides quick access to the rendering buffers. Visual Debugging helps artists to adjust various elements of the final image (albedo, depth, ambient occlusion, baked lightmaps, etc.).


![](rendering_debug_panel.png)


| Albedo | Toggles rendering of the albedo color buffer. |
|---|---|
| Roughness | Toggles rendering of the roughness value visualized as a grey-scale color from black (the roughness value equal to 0) to white (the roughness value equal to 1). |
| Metalness | Toggles rendering of the metalness value visualized as a grey-scale color from black (the metalness value equal to 0) to white (the metalness value equal to 1). |
| Specular | Toggles rendering of the specular value visualized as a grey-scale color from black (the specular value equal to 0) to white (the specular value equal to 1). |
| Microfiber | Toggles rendering of the microfiber value visualized as a grey-scale color from black (the microfiber value equal to 0) to white (the microfiber value equal to 1). |
| Opacity World Normal | Toggles rendering of the opacity normal buffer. |
| Bent Normal | Toggles rendering of the [bent normal texture](../../principles/render/sequence/index.md#ssrtgi). |
| Water World Normal | Toggles rendering of the [water normal buffer](../../principles/render/sequence/index.md#wbuffer_global_water). |
| Diffuse Lighting | Toggles rendering of the diffuse light buffer. |
| Direct Lighting | Toggles rendering of the direct light buffer. |
| Indirect Lighting | Toggles rendering of the indirect light buffer. |
| Baked Lightmap | Toggles rendering of the baked lightmaps. |
| Baked Lightmap Checker | Toggles rendering of the baked lightmaps as checked areas. |
| SSAO | Toggles rendering of the [SSAO buffer](../../principles/render/sequence/index.md#ssao). |
| SSGI | Toggles rendering of the [SSGI buffer](../../principles/render/sequence/index.md#ssgi). |
| Reflections | Toggles rendering of Reflections. |
| Highlights | Toggles rendering of highlights. |
| Cubemaps | Toggles rendering of cubemaps. |
| SSR | Toggles rendering of the [Screen-Space Reflections buffer](../../principles/render/sequence/index.md#ssr). |
| Baked Occlusion | Toggles rendering of baked occlusion. |
| Lighting Information Lost | Toggles rendering of the buffer that stores the data on the pixels that are missing from the previous frame (i.e. are new). |
| Diffuse Denoise Mask | Toggles rendering of the diffuse denoise mask buffer. |
| Specular Denoise Mask | Toggles rendering of the specular denoise mask buffer. |
| Distance | Toggles rendering of the buffer that stores the information about the distance to the nearest surface at every point of the screen. Only *Environment Probe* with the [Raymarching projection](../../objects/lights/envprobe/index.md#box_projection) renders to this buffer. |
| Light Meter | Toggles rendering of the [Light Meter](../../editor2/lighting/light_meter.md), a visual debugging tool used to simplify lighting adjustment. |
| Translucent | Toggles rendering of the translucent buffer. |
| Curvature | Toggles rendering of the curvature texture encoding the surface cavity and convexity pattern. |
| Bevel | Toggles displaying the contents of the Bevel buffer. |
| Opacity Depth | Toggles displaying the contents of the Opacity Depth buffer. |
| Scene Depth | Toggles displaying the contents of the Scene Depth buffer. |
| Velocity | Toggles rendering of the [Velocity](../../principles/render/sequence/index.md#velocity) buffer. |
| DOF Mask | Toggles rendering of the DOF Mask buffer. |
| Metering Mask | Toggles rendering of the [Metering Mask](../../editor2/settings/render_settings/camera_effects/index.md#metering_mask) buffer. |
| Auxiliary | Toggles rendering of the [Auxiliary](../../principles/render/sequence/index.md#auxiliary) buffer. |
| Vertex Color | Toggles rendering of geometry that uses the selected vertex color (channel). |
| Surface ID | A submenu of five modes that paint every surface with a unique color derived from its *[Surface ID](../../content/materials/custom_parameters/ids_and_buffers.md#ids)* - the number the renderer gives each surface it draws. Useful to check whether a surface writes its ID at all before debugging a shader that reads it, and to tell instances of a *[Mesh Cluster](../../objects/objects/mesh_cluster/index.md)* or *[Mesh Clutter](../../objects/objects/mesh_clutter/index.md)* apart. - *Surface ID Opaque* - opaque geometry, which always writes its ID. - *Surface ID Decal* - decals whose material has *Write Surface ID* enabled. - *Surface ID Transparent* - alpha-blend geometry and particles with the *Surface ID* state of their material enabled. - *Surface ID Water* - water surfaces. - *Surface ID All* - the modes above combined: decals over transparent geometry over opaque. > **Notice:** The *Transparent* and *Water* modes are available only while *[Multilayered](../../content/materials/custom_parameters/ids_and_buffers.md#modes)* Surface ID is enabled, because there is no separate buffer behind them otherwise. The other three always work. |
| Material ID | The same five modes - *Opaque*, *Decal*, *Transparent*, *Water* and *All* - for the *[Material ID](../../content/materials/custom_parameters/ids_and_buffers.md#ids)*: a unique color per material rather than per surface, so everything sharing one material comes out the same color. Availability follows the same rule as for [Surface ID](#surface_id). |
| Texture Max Pixel Count | Toggles rendering of the *[Texture Max Pixel Count](../../content/optimization/textures/index.md#texture_pixel_count)* visualizer, which shows the maximum texture resolution for materials using a color scale. > **Notice:** Only available for **Development and Debug builds** of the Engine: not compiled for *Release* builds. |
| Texture Screen Density | Toggles rendering of the *[Texture Screen Density](../../content/optimization/textures/index.md#texture_screen_density)* visualizer, which shows how the maximum texture resolution of the material corresponds to the triangle size of the screen. > **Notice:** Only available for **Development and Debug builds** of the Engine: not compiled for *Release* builds. |
| Vertex Density | Toggles rendering of the *[Vertex Density](../../content/optimization/geometry/vertex_density/index.md#tool_overview)* visualizer - a color-coded heatmap that visualizes vertex concentration hotspots across scene geometry. > **Notice:** Only available for **Development and Debug builds** of the Engine: not compiled for *Release* builds. |
| Quad Overdraw | Toggles rendering of the *[Quad Overdraw](../../content/optimization/geometry/quad_overdraw/index.md#tool_overview)* visualizer - a color-coded overlay that visualizes screen pixels that are shaded multiple times per frame. > **Notice:** Only available for **Development and Debug builds** of the Engine: not compiled for *Release* builds. |
| Gamma Space | Toggles display of the rendered frame in Linear Space. |
