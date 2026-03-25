# Unigine.Render Class (CS)

> **Notice:** This class is a singleton.


Provides access to Unigine rendering functions. For example, it is used by Wall application to render onto multiple monitors.


### See Also


- A set of UnigineScript API samples located in the `<UnigineSDK>/data/samples/rendering/` folder


## Render Class

### Enums

## PASS

| Name | Description |
|---|---|
| **WIREFRAME** = 0 | Wireframe pass. |
| **VISUALIZER_SOLID** = 1 | Visualizer pass. |
| **VISUALIZER_QUAD_OVERDRAW** = 2 | *[Quad Overdraw](../../../content/optimization/geometry/quad_overdraw/index.md#tool_overview)* visualizer pass. |
| **VISUALIZER_QUAD_OVERDRAW_NO_DEPTH_PREPASS** = 3 | *[Quad Overdraw](../../../content/optimization/geometry/quad_overdraw/index.md#tool_overview)* visualizer pass (without depth pre-pass). |
| **DEFERRED** = 4 | Deferred pass. |
| **AUXILIARY** = 5 | Auxiliary pass. |
| **EMISSION** = 6 | Emission pass. |
| **REFRACTION** = 7 | Refraction pass. |
| **TRANSPARENT_BLUR** = 8 | Transparent blur pass. |
| **AMBIENT** = 9 | Ambient pass. |
| **LIGHT_VOXEL_PROBE** = 10 | Light voxel probe pass. |
| **LIGHT_ENVIRONMENT_PROBE** = 11 | Light environment probe pass. |
| **LIGHT_PLANAR_PROBE** = 12 | Light planar probe pass. |
| **LIGHT_OMNI** = 11 | Omni light pass. |
| **LIGHT_PROJ** = 12 | Proj light pass. |
| **LIGHT_WORLD** = 13 | World light pass. |
| **SHADOW** = 13 | Shadow pass. |
| **DEPTH_PRE_PASS** = 14 | Depth pre-pass. |
| **MS_DEPTH** = 15 | MS depth pass. |
| **POST** = 16 | Post materials pass. |
| **LIGHTMAP_DATA** = 17 | Lightmap data rendering pass. |
| **PROCEDURAL_DECALS** = 18 | Pass for rendering of particles into procedural textures to be used by orthographic decals. |
| **PROCEDURAL_FIELDS** = 19 | Pass for rendering of particles into procedural textures to be used by height fields. |
| **MIXED_REALITY_BLEND_MASK_COLOR** = 20 | Pass for rendering the blend mask for mixed reality. |
| **CUSTOM_0** = 21 | Custom pass (unassigned). |
| **CUSTOM_1** = 22 | Custom pass (unassigned). |
| **CUSTOM_2** = 23 | Custom pass (unassigned). |
| **CUSTOM_3** = 24 | Custom pass (unassigned). |
| **CUSTOM_4** = 25 | Custom pass (unassigned). |
| **CUSTOM_5** = 26 | Custom pass (unassigned). |
| **CUSTOM_6** = 27 | Custom pass (unassigned). |
| **CUSTOM_7** = 28 | Custom pass (unassigned). |
| **CUSTOM_8** = 29 | Custom pass (unassigned). |
| **CUSTOM_9** = 30 | Custom pass (unassigned). |
| **CUSTOM_10** = 31 | Custom pass (unassigned). |
| **CUSTOM_11** = 32 | Custom pass (unassigned). |
| **CUSTOM_12** = 33 | Custom pass (unassigned). |
| **CUSTOM_13** = 34 | Custom pass (unassigned). |
| **CUSTOM_14** = 35 | Custom pass (unassigned). |
| **CUSTOM_15** = 36 | Custom pass (unassigned). |
| **CUSTOM_16** = 37 | Custom pass (unassigned). |
| **CUSTOM_17** = 38 | Custom pass (unassigned). |
| **CUSTOM_18** = 39 | Custom pass (unassigned). |
| **CUSTOM_19** = 40 | Custom pass (unassigned). |
| **CUSTOM_20** = 41 | Custom pass (unassigned). |
| **CUSTOM_21** = 42 | Custom pass (unassigned). |
| **CUSTOM_22** = 43 | Custom pass (unassigned). |
| **CUSTOM_23** = 44 | Custom pass (unassigned). |
| **CUSTOM_24** = 45 | Custom pass (unassigned). |
| **CUSTOM_25** = 46 | Custom pass (unassigned). |
| **CUSTOM_26** = 47 | Custom pass (unassigned). |
| **CUSTOM_27** = 48 | Custom pass (unassigned). |
| **CUSTOM_28** = 49 | Custom pass (unassigned). |
| **CUSTOM_29** = 50 | Custom pass (unassigned). |
| **CUSTOM_30** = 51 | Custom pass (unassigned). |
| **CUSTOM_31** = 52 | Custom pass (unassigned). |
| **CUSTOM_32** = 53 | Custom pass (unassigned). |
| **NUM_PASSES** = 54 | Total number of rendering passes. |

## GGX_MIPMAPS_QUALITY

Quality of GGX mipmaps for environment reflections on rough surfaces.
| Name | Description |
|---|---|
| **LOW** = 0 | Low quality of GGX mipmaps. |
| **MEDIUM** = 1 | Medium quality of GGX mipmaps. |
| **HIGH** = 2 | High quality of GGX mipmaps. |
| **ULTRA** = 3 | Ultra quality of GGX mipmaps. |

## STREAMING_MESHES_PREFETCH

| Name | Description |
|---|---|
| **DISABLE** = 0 | Asynchronous pre-loading of meshes is disabled. |
| **RADIUS** = 1 | Asynchronous pre-loading of meshes is enabled within a certain radius. |
| **FULL** = 2 | Asynchronous pre-loading of all meshes is enabled. |

## STREAMING_IGPU_VRAM_MODE

VRAM size modes for integrated GPUs (iGPU). Since integrated graphics share system RAM instead of having dedicated video memory, this mode determines how the Engine calculates the available VRAM budget for the streaming system.
| Name | Description |
|---|---|
| **SYSTEM** = 0 | Use the VRAM size reported by the system (default). |
| **SIZE** = 1 | Use a custom VRAM size specified via the [StreamingIGpuVRAMSize](#StreamingIGpuVRAMSize) property. |
| **BALANCE** = 2 | Calculate VRAM as a percentage of total system RAM, specified via the [StreamingIGpuVRAMBalance](#StreamingIGpuVRAMBalance) property. |

## SHOW_TEXTURE_RESOLUTION_UV

| Name | Description |
|---|---|
| **MODE_0** = 0 | UV Channel 0 is used for visualization of the texture resolution. |
| **MODE_1** = 1 | UV Channel 1 is used for visualization of the texture resolution. |

## SHOW_TEXTURE_RESOLUTION

| Name | Description |
|---|---|
| **DISABLED** = 0 | Texture resolution rendering mode is disabled. |
| **BY_MAX_PIXEL_COUNT** = 1 | Surfaces are colored depending on maximum resolution of textures used in materials assigned to them in accordance with the scale. |
| **BY_SCREEN_SIZE** = 2 | Surfaces are colored to display the relationship between maximum texture resolution of the material to the size of triangles on the screen to which it is applied: blue indicates insufficient texture resolution, while yellow tells that it is excessive, if the color is green - everything is ok. |

## SHOW_IMMOVABLE

| Name | Description |
|---|---|
| **DISABLED** = 0 | Do not display geometry with or without the Immovable option. |
| **OPTION_ENABLED** = 1 | Display geometry with the Immovable option enabled. |
| **OPTION_DISABLED** = 2 | Display geometry with the Immovable option disabled. |

## SHOW_VERTEX_COLOR

| Name | Description |
|---|---|
| **DISABLED** = 0 | Displaying of vertex colors is disabled. |
| **RED** = 1 | Display geometry that uses the red vertex color channel. |
| **GREEN** = 2 | Display geometry that uses the green vertex color channel. |
| **BLUE** = 3 | Display geometry that uses the blue vertex color channel. |
| **ALPHA** = 4 | Display geometry that uses the alpha vertex color channel. |
| **RGB** = 5 | Display geometry that uses RGB vertex color channels. |

## TONEMAPPER

Tone mapping mode.
| Name | Description |
|---|---|
| **FILMIC** = 0 | *Filmic* - basic customizable filmic tone mapping mode. |
| **ACES** = 1 | *ACES* - tone mapping in accordance with the industry standard set by the Academy Color Encoding System (ACES) for television and film. |
| **MIX_ACES_WITH_REINHARD** = 2 | *Mix ACES With Reinhard* - Combination of ACES and Reinhard tone mapping. |
| **REINHARD** = 3 | *Reinhard* - Simple Reinhard. C/(1+C) formula applied to each of the channels. May cause slight desaturation. |
| **REINHARD_LUMA_BASED** = 4 | *Reinhard Luma-Based* - Luma-based Reinhard tone mapping, applied to luminance only. More accurate representation of colors. |

## VIEWPORT_MODE

| Name | Description |
|---|---|
| **DEFAULT** = 0 | Enables the default stereo mode - no stereo and panoramic rendering in the current viewport is available. This mode is set by default for [a new viewport](#Viewport). |
| **PANORAMA_CURVED_180** = 1 | Enables rendering of the viewport as a panorama with curved edges with an angle of 180 degrees. |
| **PANORAMA_CURVED_360** = 2 | Enables rendering of the viewport as a panorama with curved edges with an angle of 360 degrees. |
| **PANORAMA_LINEAR_180** = 3 | Enables rendering of the viewport as a linear panorama without distortion at the edges with an angle of 180 degrees. |
| **PANORAMA_LINEAR_360** = 4 | Enables rendering of the viewport as a linear panorama without distortion at the edges with an angle of 360 degrees. |
| **PANORAMA_FISHEYE_ORTHOGRAPHIC** = 5 | Enables rendering of the viewport as an orthographic spherical panorama (fisheye). |
| **PANORAMA_FISHEYE_EQUDISTANT** = 6 | Enables rendering of the viewport as an equidistant spherical panorama (fisheye). |
| **PANORAMA_FISHEYE_STEREOGRAPHIC** = 7 | Enables rendering of the viewport as an stereographic spherical panorama (fisheye). |
| **PANORAMA_FISHEYE_EQUISOLID** = 8 | Enables rendering of the viewport as an equisolid spherical panorama (fisheye). |
| **STEREO_ANAGLYPH** = 9 | Enables the anaglyph stereo mode that is viewed with red-cyan anaglyph glasses. |
| **STEREO_INTERLACED** = 10 | Enables the interlaced stereo mode that is used with interlaced stereo monitors and polarized 3D glasses. |
| **STEREO_HORIZONTAL** = 11 | Enables the horizontal stereo mode that is supported on mobile devices. |
| **STEREO_VERTICAL** = 12 | Enables the vertical stereo mode that is supported on mobile devices. |
| **STEREO_SEPARATE** = 13 | Enables the replicate images stereo mode. |
| **STEREO_REPLICATE** = 14 | Enables the separate images stereo mode. This mode serves to output two separate images for each of the eye. It can be used with any VR/AR output devices that support separate images output, e.g. for 3D video glasses or helmets (HMD). |

## VSYNC

| Name | Description |
|---|---|
| **DISABLE** = 0 | Vertical FPS synchronization is disabled. |
| **STRICT** = 1 | Strict vertical FPS synchronization. |
| **ADAPTIVE** = 2 | Adaptive vertical FPS synchronization (OpenGL only). |

## SHOW_LIGHTING_MODE

| Name | Description |
|---|---|
| **DISABLED** = 0 | Displaying of lighting mode is disabled. |
| **STATIC** = 1 | Displaying of surfaces for which [static lighting mode](../../../api/library/objects/class.object_cs.md#SURFACE_LIGHTING_MODE_STATIC) is enabled. |
| **DYNAMIC** = 2 | Displaying of surfaces for which [dynamic lighting mode](../../../api/library/objects/class.object_cs.md#SURFACE_LIGHTING_MODE_DYNAMIC) is enabled. |
| **ADVANCED** = 3 | Displaying of surfaces for which [advanced lighting mode](../../../api/library/objects/class.object_cs.md#SURFACE_LIGHTING_MODE_ADVANCED) is enabled. |

## SHADERS_COMPILE_MODE

| Name | Description |
|---|---|
| **ASYNC** = 0 | Asynchronous shaders compilation mode. |
| **FORCE** = 1 | Forced shaders compilation mode. |

## EXPOSURE_MODE

| Name | Description |
|---|---|
| **DISABLED** = 0 | Static exposure mode. The amount of luminance is determined by the Exposure*[Exposure](../../...md#render_exposure)* depending on the Camera Mode*[CameraMode](../../...md#render_camera_mode)* parameter. |
| **LOGARITHMIC** = 1 | Exposure mode based on the adaptive logarithmic mapping technique. |
| **QUADRATIC** = 2 | Exposure mode based on the adaptive quadratic mapping technique. |
| **CURVE_BASED** = 3 | Exposure mode based on the adaptive curve mapping technique. |

## CAMERA_MODE

| Name | Description |
|---|---|
| **CLASSIC** = 0 | Camera mode with the exposure set by the Exposure value*[Exposure](../../...md#render_exposure)*. |
| **PHYSICALLY_BASED** = 1 | Camera mode with the real-world values used to set up lighting and camera exposure: ISO*[ISO](../../...md#render_iso)*, shutter speed*[ShutterSpeed](../../...md#render_shutter_speed)*, F-stop*[FStop](../../...md#render_f_stop)*. With the default values of these parameters, the static exposure value is near 1. The exposure mode*[ExposureMode](../../...md#render_exposure_mode)* should be set to *Static* to avoid exposure issues. |

## RENDER_API

| Name | Description |
|---|---|
| **API_NULL** = 0 | Null API name. |
| **API_DIRECT3D12** = 1 | DIRECT3D 12 API. |
| **API_VULKAN** = 2 | VULKAN API. |

## RENDER_FSR_MODE

Quality modes of FSR (FidelityFX Super Resolution upsampling technique).
| Name | Description |
|---|---|
| **ULTRA_PERFORMANCE** = 0 | Offers the highest performance gain while still retaining image quality close to native. Scale factor: 3.0x per dimension (≈33.3% of output resolution) |
| **PERFORMANCE** = 1 | Delivers a substantial performance boost with image quality similar to native rendering. Scale factor: 2.0x per dimension (≈50.0% of output resolution) |
| **BALANCED** = 2 | Balances performance gains and image quality effectively. Scale factor: 1.7x per dimension (≈58.8% of output resolution) |
| **QUALITY** = 3 | Provides image quality equal to or better than native with a meaningful performance improvement. Scale factor: 1.5x per dimension (≈66.6% of output resolution) |
| **NATIVE_AA** = 4 | Renders at native resolution (no upscaling, scale factor 1.0x) and applies FSR anti-aliasing only. |
| **CUSTOM** = 5 | Uses a custom resolution scale set via the [FSRCustomResolutionScale](#FSRCustomResolutionScale) property (range: 0.1 to 1.0). |
| **RENDER_FSR_NUM_MODES** = 6 | Total number of FSR quality modes. |

## RENDER_DLSS_PRESET

Presets of DLSS (Deep Learning Super Sampling technique).
| Name | Description |
|---|---|
| **DEFAULT** = 0 | DLSS *Default Preset*. Automatically selects the recommended configuration (Preset D for Performance/Balanced/Quality, Preset F for Ultra Performance/DLAA) and may be updated over-the-air by NVIDIA. |
| **A** = 1 | DLSS *Preset A*. Legacy preset designed to mitigate ghosting artifacts, particularly in cases where input data (e.g., motion vectors) may be missing. **Intended modes:** Performance, Balanced, Quality |
| **B** = 2 | DLSS *Preset B*. Variant of Preset A, optimized specifically for Ultra Performance mode. **Intended modes:** Ultra Performance |
| **C** = 3 | DLSS *Preset C*. Prefers current-frame information, making it well-suited for fast-paced, high-motion content. **Intended modes:** Performance, Balanced, Quality |
| **D** = 4 | DLSS *Preset D*. Functionally similar to Preset E but less commonly recommended. Preset E is preferred in most cases. **Intended modes:** Performance, Balanced, Quality |
| **E** = 5 | DLSS *Preset E*. General-purpose preset prioritizing both performance and image stability. **Intended modes:** Performance, Balanced, Quality |
| **F** = 6 | DLSS *Preset F*. Default preset for Ultra Performance and DLAA modes. Provides stable results across these configurations. **Intended modes:** Ultra Performance, DLAA |
| **G** = 7 | DLSS *Preset G*: Unused. Reverts to default preset behavior. |
| **H** = 8 | DLSS *Preset H*: Unused. Reverts to default preset behavior. |
| **I** = 9 | DLSS *Preset I*: Unused. Reverts to default preset behavior. |
| **J** = 10 | DLSS *Preset J*. Transformer-based model similar to Preset K. May exhibit slightly less ghosting, but at the cost of additional flickering. Generally superseded by Preset K. **Intended modes:** DLAA, Performance, Balanced, Quality |
| **K** = 11 | DLSS *Preset K*. Default transformer-based preset delivering the highest image quality. Reduces ghosting and shimmering compared to other presets, though at a higher performance cost. Recommended over Preset J. **Intended modes:** DLAA, Performance, Balanced, Quality |
| **RENDER_DLSS_NUM_PRESETS** = 12 | Total number of DLSS presets. |

## RENDER_DLSS_MODE

Quality modes of DLSS (Deep Learning Super Sampling technique).
| Name | Description |
|---|---|
| **ULTRA_PERFORMANCE** = 0 | *Ultra Performance* provides the highest performance boost by rendering at ~33.3% of the target resolution and upscaling to the output resolution. This mode is recommended only for 8K output resolution due to the significant reduction in internal image quality. |
| **MAX_PERFORMANCE** = 1 | *Max Performance* provides a higher performance boost than *Balanced* by rendering at ~50% of the target resolution. Use when frame-rate is prioritized but some internal detail should be preserved. It is recommended for users with 1440p/2K monitors, providing better performance with minimal effort. |
| **BALANCED** = 2 | *Balanced* offers both optimized performance and image quality by rendering at approximately ~58% of the target resolution. Recommended as the general-purpose preset for users who want a compromise between frame-rate and visual fidelity. |
| **MAX_QUALITY** = 3 | *Max Quality* offers higher image quality than *Balanced* by rendering at approximately ~66.7% of the target resolution. Prioritizes visual fidelity while still delivering a meaningful performance improvement over native rendering. |
| **DLAA** = 4 | *DLAA* (**Deep Learning Anti-Aliasing**) is an AI-powered tool to eliminate jagged edges in video apps, by rendering at native (100%) resolution. It improves image quality with less performance cost than traditional anti-aliasing methods. |
| **RENDER_DLSS_NUM_MODES** = 5 | Total number of DLSS modes. |

## RENDER_UPSCALE_MODE

| Name | Description |
|---|---|
| **NONE** = 0 | No upscaling - 1.0x per dimension, the final image has 100% rendered resolution. |
| **FSR** = 1 | The Fidelity FX Super Resolution upscaling mode. |
| **DLSS** = 2 | The Deep Learning Super Sampling upscaling mode. |
| **RENDER_UPSCALE_NUM_MODES** = 3 | Total number of upscaling modes. |

## RENDER_UPSCALE_ORDER

Determines at which stage of the rendering pipeline the upscaling is applied.
| Name | Description |
|---|---|
| **BEFORE_POST_EFFECTS** = 0 | Upscale is applied before post-effects (default). |
| **AFTER_ADAPTATION_COLOR** = 1 | Upscale is applied after color adaptation. |
| **BEFORE_TAA** = 2 | Upscale is applied before TAA. |
| **AFTER_POST_EFFECTS** = 3 | Upscale is applied after post-effects, before the Sharpen effect. |
| **RENDER_UPSCALE_ORDER.AFTER_POST_EFFECTS** = 3 | Total number of upscale order modes. |

## MATERIALS_QUALITY

| Name | Description |
|---|---|
| **LOW** = 0 | Low quality of materails. |
| **MEDIUM** = 1 | Medium quality of materails. |
| **HIGH** = 2 | High quality of materails. |

## TEXTURE_LIFETIME

Lifetime of a temporary render texture that defines when the allocated resource should be released. UNIGINE maintains an internal pool of temporary render textures - including 2D, 3D, and texture arrays - that can be used for temporary calculations. These textures are retrieved from the pool using the appropriate *getTemporaryTexture*()* methods and are automatically released once the specified lifetime expires.
| Name | Description |
|---|---|
| **FRAME_VIEWPORT** = 0 | The temporary render texture resource will be released when the viewport in which it was used is removed. |
| **FRAME_APPLICATION** = 1 | The temporary render texture resource will be released at the end of the current frame after the frame is rendered. |
| **APPLICATION** = 2 | The temporary render texture resource will be released on application shutdown. |

## SHOW_TEXTURE_RESOLUTION_STREAMING_ACCOUNTING

| Name | Description |
|---|---|
| **MODE_ACTUAL** = 0 | Actual resolution. |
| **MODE_REQUESTED** = 1 | Requested texture resolution. |
| **MODE_SOURCE** = 2 | Source texture resolution. |

## STREAMING_VRAM_BUDGET

| Name | Description |
|---|---|
| **SYSTEM** = 0 | The available VRAM size is obtained from the operating system. |
| **DRIVER** = 1 | The VRAM available for the application is determined by the video driver. |
| **FULL_GPU_MEMORY** = 2 | All VRAM is available for the application. |

## STREAMING_MODE

| Name | Description |
|---|---|
| **ASYNC** = 0 | Asyncronous data streaming mode. |
| **FORCE** = 1 | Forced data streaming mode. |

## TEXTURE_ACCESSORY

| Name | Description |
|---|---|
| **NONE** = 0 | Ordinary non-accessory textures. |
| **GBUFFER** = 1 | GBuffer textures (**gbuffer_albedo, gbuffer_shading, gbuffer_normal**, etc.). |
| **WBUFFER** = 2 | Water buffer (WBuffer) textures (**wbuffer_diffuse, wbuffer_normal**, etc.). |
| **RENDER** = 3 | Render textures (**clouds, scene depth**, etc.). |
| **OCCLUDERS** = 4 | Textures used for occluders (**occluders, occluder shadows**, etc.). |
| **EXTERNAL** = 5 | External textures. |

## RENDER_VR_EMULATION_MODE

| Name | Description |
|---|---|
| **DISABLED** = 0 | VR emulation is disabled. Standard rendering is used. |
| **VIVE** = 1 | Emulates the HTC Vive headset rendering parameters. |
| **VIVE_PRO** = 2 | Emulates the HTC Vive Pro headset rendering parameters. |
| **VIVE_PRO_2** = 3 | Emulates the HTC Vive Pro 2 headset rendering parameters. |
| **VIVE_FOCUS_3** = 4 | Emulates the HTC Vive Focus 3 headset rendering parameters. |
| **VIVE_FOCUS_VISION** = 5 | Emulates the HTC Vive Focus Vision headset rendering parameters. |
| **VIVE_XR_ELITE** = 6 | Emulates the HTC Vive XR Elite headset rendering parameters. |
| **OCULUS_RIFT** = 7 | Emulates the Oculus Rift headset rendering parameters. |
| **QUEST_2** = 8 | Emulates the Quest 2 headset rendering parameters. |
| **QUEST_3S** = 9 | Emulates the Quest 3S VR headset rendering parameters. |
| **QUEST_3** = 10 | Emulates the Quest 3 headset rendering parameters. |
| **QUEST_PRO** = 11 | Emulates the Quest Pro headset rendering parameters. |
| **PICO_4** = 12 | Emulates the Pico 4 headset rendering parameters. |
| **VALVE_INDEX** = 13 | Emulates the Valve Index headset rendering parameters. |
| **VARJO_VR_3** = 14 | Emulates the Varjo VR-3 headset rendering parameters. |
| **VARJO_VR_4** = 15 | Emulates the Varjo VR-4 headset rendering parameters. |
| **RENDER_VR_EMULATION_NUM_MODES** = 16 | The total number of emulation modes. |

## SHOW_QUAD_OVERDRAW_PASSES

| Name | Description |
|---|---|
| **ALL** = 0 | Displays the total number of overdraws, including all passes (Auxiliary, Emission, Ambient, Light, and others), and depth pre-passes. |
| **GEOMETRY** = 1 | Displays the number of overdraws for the primary rendering pass of the content after applying the depth pre-pass. Separate passes (such as Auxiliary or Lighting) are not counted in this mode. |
| **GEOMETRY_WITHOUT_DEPTH_PRE_PASS** = 2 | Displays the number of content overdraws without using depth pre-pass (before any early depth rejection is applied). |

## SHOW_QUAD_OVERDRAW_DISPLAY_MODE

| Name | Description |
|---|---|
| **GRADIENT** = 0 | Displays a color gradient representing overdraw intensity from black (0) to white (threshold value). |
| **DISCRETE_THRESHOLD** = 1 | Displays only the areas where the overdraw exceeds the specified threshold. |

## SHOW_VERTEX_DENSITY_MODE

| Name | Description |
|---|---|
| **DISCRETE_THRESHOLD** = 0 | Displays only the areas where the vertex density exceeds the specified threshold within the defined area. |
| **GRADIENT** = 1 | Displays a color gradient representing vertex density from black (0) to white (threshold value) within the defined area. |

## SHADING_QUALITY

Quality levels of shading. In graph-based materials, this corresponds to the input of a [Shading Quality Switch](../../../content/materials/graph/node_library/misc/shading_quality_switch.md) node.
| Name | Description |
|---|---|
| **LOW** = 0 | Low shading quality level. |
| **MEDIUM** = 1 | Medium shading quality level. |
| **HIGH** = 2 | High shading quality level (default). |

### Properties

## bool Enabled

The a value indicating if the render is enabled.
## 🔒︎ int NumTriangles

The number of rendered per frame triangles that can be seen in the viewport. See [Rendering Profiler](../../../tools/profiling/profiler/index.md#rtriangles) article for details.
## 🔒︎ int NumSurfaces

The number of rendered per frame surfaces that can be seen in the viewport (in all rendering passes). See [Rendering Profiler](../../../tools/profiling/profiler/index.md#rshaders) article for details.
## 🔒︎ int NumShadows

The number of shadow passes rendered per frame. See [Rendering Profiler](../../../tools/profiling/profiler/index.md#rshadows) article for details.
## 🔒︎ long NumShaders

The number of shaders set per frame. See [Rendering Profiler](../../../tools/profiling/profiler/index.md#rshaders) article for details.
## 🔒︎ int NumReflections

The number of reflections drawn per frame that can be seen in the viewport. In case of cubemap reflections, if all six faces are updated, six reflections are rendered per each frame.
## 🔒︎ int NumPrimitives

The number of geometric rendered per frame primitives that can be seen in the viewport. See [Rendering Profiler](../../../tools/profiling/profiler/index.md#rprimitives) article for details.
## 🔒︎ int NumMaterials

The number of materials set per frame (during all of the rendering passes) in the current scene.
## 🔒︎ int NumLights

The number of light passes rendered per frame. It means that the value contains the number of all light sources that are currently seen illuminating something in the viewport and also includes additional passes for rendering lights in the reflecting surfaces (if dynamical reflections are used). See [Rendering Profiler](../../../tools/profiling/profiler/index.md#rlights) article for details.
## 🔒︎ int NumDips

The number of draw calls used in the current scene. See [Rendering Profiler](../../../tools/profiling/profiler/index.md#rdips) article for details.
## 🔒︎ int NumDecals

The number of rendered per frame decals that can be seen in the viewport (during all of the rendering passes).
## 🔒︎ int HDRTextureFormat

The HDR texture format to be used.
## bool ShowFieldMask

***Console*:**`render_show_field_mask`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is enabled to highlight the surfaces that use the [specified bits](#render_show_field_mask_bits) of the [field mask](../../../principles/bit_masking/index.md#field_mask). The default value is **false**.
## int ShowFieldMaskBits

***Console*:**`render_show_field_mask_bits`The value indicating which bit or bits of the [field mask](../../../principles/bit_masking/index.md#field_mask) are used for visualization. The surfaces that use the specified bits of the field mask will be highlighted. To use this option, rendering of the relevant visualizer *[ShowFieldMask](../../...md#render_show_field_mask)* should be enabled.
> **Notice:** Please note that the argument is an integer value, so the bit mask has to be represented accordingly.



## bool ShowShadowMask

***Console*:**`render_show_shadow_mask`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is enabled to highlight the surfaces that use the [specified bits](#render_show_shadow_mask_bits) of the [shadow mask](../../../principles/bit_masking/index.md#shadow_mask). The default value is **false**.
## int ShowShadowMaskBits

***Console*:**`render_show_shadow_mask_bits`The value indicating which bit or bits of the [shadow mask](../../../principles/bit_masking/index.md#shadow_mask) are used for visualization. The surfaces that use the specified bits of the shadow mask will be highlighted. To use this option, rendering of the relevant visualizer *[ShowShadowMask](../../...md#render_show_shadow_mask)* should be enabled.
> **Notice:** Please note that the argument is an integer value, so the bit mask has to be represented accordingly.



## bool ShowObstacleMask

***Console*:**`render_show_obstacle_mask`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is enabled to highlight the surfaces that use the [specified bits](#render_show_obstacle_mask_bits) of the [obstacle mask](../../../principles/bit_masking/index.md#obstacle_mask). The default value is **false**.
## int ShowObstacleMaskBits

***Console*:**`render_show_obstacle_mask_bits`The value indicating which bit or bits of the [obstacle mask](../../../principles/bit_masking/index.md#obstacle_mask) are used for visualization. The surfaces that use the specified bits of the obstacle mask will be highlighted. To use this option, rendering of the relevant visualizer *[ShowObstacleMask](../../...md#render_show_obstacle_mask)* should be enabled.
> **Notice:** Please note that the argument is an integer value, so the bit mask has to be represented accordingly.



## bool ShowMaterialMask

***Console*:**`render_show_material_mask`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is enabled to highlight the surfaces that use the [specified bits](#render_show_material_mask_bits) of the [material mask](../../../principles/bit_masking/index.md#material_mask). The default value is **false**.
## int ShowMaterialMaskBits

***Console*:**`render_show_material_mask_bits`The value indicating which bit or bits of the [material mask](../../../principles/bit_masking/index.md#material_mask) are used for visualization. The surfaces that use the specified bits of the material mask will be highlighted. To use this option, rendering of the relevant visualizer *[ShowMaterialMask](../../...md#render_show_material_mask)* should be enabled.
> **Notice:** Please note that the argument is an integer value, so the bit mask has to be represented accordingly.



## bool ShowViewportMask

***Console*:**`render_show_viewport_mask`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is enabled to highlight the surfaces that use the [specified bits](#render_show_viewport_mask_bits) of the [viewport mask](../../../principles/bit_masking/index.md#viewport). The default value is **false**.
## int ShowViewportMaskBits

***Console*:**`render_show_viewport_mask_bits`The value indicating which bit or bits of the [viewport mask](../../../principles/bit_masking/index.md#viewport) are used for visualization. The surfaces that use the specified bits of the viewport mask will be highlighted. To use this option, rendering of the relevant visualizer *[ShowViewportMask](../../...md#render_show_viewport_mask)* should be enabled.
> **Notice:** Please note that the argument is an integer value, so the bit mask has to be represented accordingly.



## bool ShowPhysicalMask

***Console*:**`render_show_physical_mask`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is enabled to highlight the surfaces that use the [specified bits](#render_show_physical_mask_bits) of the [physical mask](../../../principles/bit_masking/index.md#physical_mask). The default value is **false**.
## int ShowPhysicalMaskBits

***Console*:**`render_show_physical_mask_bits`The value indicating which bit or bits of the [physical mask](../../../principles/bit_masking/index.md#physical_mask) are used for visualization. The surfaces that use the specified bits of the physical mask will be highlighted. To use this option, rendering of the relevant visualizer *[ShowPhysicalMask](../../...md#render_show_physical_mask)* should be enabled.
> **Notice:** Please note that the argument is an integer value, so the bit mask has to be represented accordingly.



## bool ShowCollisionMask

***Console*:**`render_show_collision_mask`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is enabled to highlight the surfaces that use the [specified bits](#render_show_collision_mask_bits) of the [collision mask](../../../principles/bit_masking/index.md#collision_mask). The default value is **false**.
## int ShowCollisionMaskBits

***Console*:**`render_show_collision_mask_bits`The value indicating which bit or bits of the [collision mask](../../../principles/bit_masking/index.md#collision_mask) are used for visualization. The surfaces that use the specified bits of the collision mask will be highlighted. To use this option, rendering of the relevant visualizer *[ShowCollisionMask](../../...md#render_show_collision_mask)* should be enabled.
> **Notice:** Please note that the argument is an integer value, so the bit mask has to be represented accordingly.



## bool ShowNavigationMask

***Console*:**`render_show_navigation_mask`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is enabled to highlight the surfaces that use the [specified bits](#render_show_navigation_mask_bits) of the [navigation mask](../../../principles/bit_masking/index.md#navigation_mask). The default value is **false**.
## int ShowNavigationMaskBits

***Console*:**`render_show_navigation_mask_bits`The value indicating which bit or bits of the [navigation mask](../../../principles/bit_masking/index.md#navigation_mask) are used for visualization. The surfaces that use the specified bits of the navigation mask will be highlighted. To use this option, rendering of the relevant visualizer *[ShowNavigationMask](../../...md#render_show_navigation_mask)* should be enabled.
> **Notice:** Please note that the argument is an integer value, so the bit mask has to be represented accordingly.



## bool ShowIntersectionMask

***Console*:**`render_show_intersection_mask`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is enabled to highlight the surfaces that use the [specified bits](#render_show_intersection_mask_bits) of the [intersection mask](../../../principles/bit_masking/index.md#intersection_mask). The default value is **false**.
## int ShowIntersectionMaskBits

***Console*:**`render_show_intersection_mask_bits`The value indicating which bit or bits of the [intersection mask](../../../principles/bit_masking/index.md#intersection_mask) are used for visualization. The surfaces that use the specified bits of the intersection mask will be highlighted. To use this option, rendering of the relevant visualizer *[ShowIntersectionMask](../../...md#render_show_intersection_mask)* should be enabled.
> **Notice:** Please note that the argument is an integer value, so the bit mask has to be represented accordingly.



## bool ShowSoundSourceMask

***Console*:**`render_show_sound_source_mask`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is enabled to highlight the surfaces that use the [specified bits](#render_show_sound_source_mask_bits) of the [sound source mask](../../../principles/bit_masking/index.md#source_mask). The default value is **false**.
## int ShowSoundSourceMaskBits

***Console*:**`render_show_sound_source_mask_bits`The value indicating which bit or bits of the [sound source mask](../../../principles/bit_masking/index.md#source_mask) are used for visualization. The surfaces that use the specified bits of the sound source mask will be highlighted. To use this option, rendering of the relevant visualizer *[ShowSoundSourceMask](../../...md#render_show_sound_source_mask)* should be enabled.
> **Notice:** Please note that the argument is an integer value, so the bit mask has to be represented accordingly.



## bool ShowSoundReverbMask

***Console*:**`render_show_sound_reverb_mask`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is enabled to highlight the surfaces that use the [specified bits](#render_show_sound_reverb_mask_bits) of the [reverberation mask](../../../principles/bit_masking/index.md#reverb_mask). The default value is **false**.
## int ShowSoundReverbMaskBits

***Console*:**`render_show_sound_reverb_mask_bits`The value indicating which bit or bits of the [reverberation mask](../../../principles/bit_masking/index.md#reverb_mask) are used for visualization. The surfaces that use the specified bits of the reverberation mask will be highlighted. To use this option, rendering of the relevant visualizer *[ShowSoundReverbMask](../../...md#render_show_sound_reverb_mask)* should be enabled.
> **Notice:** Please note that the argument is an integer value, so the bit mask has to be represented accordingly.



## bool ShowSoundOcclusionMask

***Console*:**`render_show_sound_occlusion_mask`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is enabled to highlight the surfaces that use the [specified bits](#render_show_sound_occlusion_mask_bits) of the [sound occlusion mask](../../../principles/bit_masking/index.md#sound_occlusion_mask). The default value is **false**.
## int ShowSoundOcclusionMaskBits

***Console*:**`render_show_sound_occlusion_mask_bits`The value indicating which bit or bits of the [sound occlusion mask](../../../principles/bit_masking/index.md#sound_occlusion_mask) are used for visualization. The surfaces that use the specified bits of the sound occlusion mask will be highlighted. To use this option, rendering of the relevant visualizer *[ShowSoundOcclusionMask](../../...md#render_show_sound_occlusion_mask)* should be enabled.
> **Notice:** Please note that the argument is an integer value, so the bit mask has to be represented accordingly.



## bool ShowPhysicalExclusionMask

***Console*:**`render_show_physical_exclusion_mask`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is enabled to highlight the surfaces that use the [specified bits](#render_show_physical_exclusion_mask_bits) of the [physical exclusion mask](../../../principles/bit_masking/index.md#exclusion_mask). The default value is **false**.
## int ShowPhysicalExclusionMaskBits

***Console*:**`render_show_physical_exclusion_mask_bits`The value indicating which bit or bits of the [physical exclusion mask](../../../principles/bit_masking/index.md#exclusion_mask) are used for visualization. The surfaces that use the specified bits of the physical exclusion mask will be highlighted. To use this option, rendering of the relevant visualizer *[ShowPhysicalExclusionMask](../../...md#render_show_physical_exclusion_mask)* should be enabled.
> **Notice:** Please note that the argument is an integer value, so the bit mask has to be represented accordingly.



## bool ShowPhysicsIntersectionMask

***Console*:**`render_show_physics_intersection_mask`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is enabled to highlight the surfaces that use the [specified bits](#render_show_physics_intersection_mask_bits) of the [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask). The default value is **false**.
## int ShowPhysicsIntersectionMaskBits

***Console*:**`render_show_physics_intersection_mask_bits`The value indicating which bit or bits of the [physics intersection mask](../../../principles/bit_masking/index.md#physics_intersection_mask) are used for visualization. The surfaces that use the specified bits of the physics intersection mask will be highlighted. To use this option, rendering of the relevant visualizer *[ShowPhysicsIntersectionMask](../../...md#render_show_physics_intersection_mask)* should be enabled.
> **Notice:** Please note that the argument is an integer value, so the bit mask has to be represented accordingly.



## bool ShowQueries

***Console*:**`render_show_queries`The value indicating whether occlusion query boxes are displayed in the viewport.
## bool ShowDecals

***Console*:**`render_show_decals`The value indicating whether the visualizer is displayed for decals.
## bool ShowScissors

***Console*:**`render_show_scissors`The value indicating if scissor rectangles are displayed. The default value is **false**.
## bool ShowLightmapChecker

***Console*:**`render_show_lightmap_checker`The value indicating whether the Baked Lightmap Checker debug mode is enabled. This mode maps the checker texture onto the baked lightmap polygons, which can be used to facilitate the process of comparing UV map texels on neighboring planes.
## bool ShowOccluder

***Console*:**`render_show_occluder`The value indicating whether the buffer used for occluders is displayed in the viewport.
## bool ShowCascades

***Console*:**`render_show_cascades`The value indicating whether Parallel Split Shadow Map - world shadow cascades are displayed.
## float ShowVisualizerDistance

***Console*:**`render_show_visualizer_distance`The distance from the camera within which the helpers are visualized.
Range of values: **[0, 100000]**. The default value is : **500**.
## bool ShowWorldShadowCasters

***Console*:**`render_show_world_shadow_casters`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for surfaces that are configured to cast shadows from the current *World Light*. The default value is **false**.
## bool ShowProjAndOmniShadowCasters

***Console*:**`render_show_proj_and_omni_shadow_casters`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for surfaces that are configured to cast shadows from *Proj* and *Omni* light sources. The default value is **false**.
## bool ShowAlphaTest

***Console*:**`render_show_alpha_test`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for transparent objects using alpha test. The default value is **false**.
## bool ShowDepthPrePass

***Console*:**`render_show_depth_pre_pass`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for surfaces that use depth pre-pass rendering. This includes surfaces with Alpha Test transparency and opaque surfaces with Force Depth Pre-Pass option enabled in the material. The default value is **false**.
## bool ShowEmission

***Console*:**`render_show_emission`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for materials with the *Emission* state enabled or connecting any data to the *Emission* input in the material graph. The default value is **false**.
## bool ShowMeshStatics

***Console*:**`render_show_mesh_statics`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for static meshes. The default value is **false**.
## bool ShowMeshDynamics

***Console*:**`render_show_mesh_dynamics`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for dynamic meshes. The default value is **false**.
## bool ShowComplexShadowShader

***Console*:**`render_show_complex_shadow_shader`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for objects that cast shadows in the following way: the pixels are cut out during the shadow pass, as it's done in Alpha Test or Alpha Blend materials, materials assigned to animated Mesh Skinned, opaque materials with the enabled Depth Offset or any other effects that affect shadows. The default value is **false**.
## bool ShowSurfaceCustomTextureNotAvailable

***Console*:**`render_show_surface_custom_texture_not_available`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for surfaces the materials of which use the [surface custom texture](../../../content/materials/graph/node_library/textures/surface_custom_texture.md) in the material graph, however the option is not enabled for the surface. The default value is **false**.
## bool ShowSurfaceCustomTextureNotUsed

***Console*:**`render_show_surface_custom_texture_not_used`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for surfaces with the [surface custom texture](../../../content/materials/graph/node_library/textures/surface_custom_texture.md) enabled and/or set, but not used in the material graph. The default value is **false**.
## bool ShowSurfaceCustomTexture

***Console*:**`render_show_surface_custom_texture`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for surfaces with the [surface custom texture](../../../content/materials/graph/node_library/textures/surface_custom_texture.md) enabled. The default value is **false**.
## bool ShowPhysicsIntersection

***Console*:**`render_show_physics_intersection`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for surfaces with the *[physics intersection](../../../editor2/node_parameters/physics/index.md#surface_physics_intersection)* enabled. The default value is **false**.
## bool ShowIntersection

***Console*:**`render_show_intersection`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for surfaces with the *[Intersection](../../../editor2/node_parameters/physics/index.md#surface_intersection)* enabled. The default value is **false**.
## bool ShowManualMaterials

***Console*:**`render_show_manual_materials`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for objects with manual materials. The default value is **false**.
## bool ShowNonManualMaterials

***Console*:**`render_show_non_manual_materials`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for objects with non-manual materials. The default value is **false**.
## bool ShowClusters

***Console*:**`render_show_clusters`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for *Mesh Cluster* objects. The default value is **false**.
## int ShowImmovable

***Console*:**`render_show_immovable`The value visualizing the state of the [Immovable](../../../editor2/node_parameters/transformation_common/index.md#clutter) option for objects. One of the following values:
- **0** - disabled (by default)
- **1** - show objects with *Immovable* option enabled
- **2** - show objects with *Immovable* option disabled

## bool ShowDynamic

***Console*:**`render_show_dynamic`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for dynamic objects. The default value is **false**.
## bool ShowTransparent

***Console*:**`render_show_transparent`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for transparent objects. The default value is **false**.
## bool ShowTransparentGBuffer

***Console*:**`render_show_transparent_gbuffer`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for transparent (blend) surfaces whose material is configured to render in the deferred pass (write to GBuffer). The default value is **false**.
## bool ShowTransparentLightingAmbient

***Console*:**`render_show_transparent_lighting_ambient`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for transparent (blend) surfaces whose material is configured to receive lighting from ambient sources. The default value is **false**.
## bool ShowTransparentLightingEnvironmentProbe

***Console*:**`render_show_transparent_lighting_environment_probe`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for transparent (blend) surfaces whose material is configured to receive lighting from Environment Probes. The default value is **false**.
## bool ShowTransparentLightingVoxelProbe

***Console*:**`render_show_transparent_lighting_voxel_probe`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for transparent (blend) surfaces whose material is configured to receive lighting from Voxel Probes. The default value is **false**.
## bool ShowTransparentLightingPlanarProbe

***Console*:**`render_show_transparent_lighting_planar_probe`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for transparent (blend) surfaces whose material is configured to receive lighting from Planar Probes. The default value is **false**.
## bool ShowTransparentLightingLightOmni

***Console*:**`render_show_transparent_lighting_light_omni`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for transparent (blend) surfaces whose material is configured to receive lighting from Omni lights. The default value is **false**.
## bool ShowTransparentLightingLightProj

***Console*:**`render_show_transparent_lighting_light_proj`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for transparent (blend) surfaces whose material is configured to receive lighting from Projected lights. The default value is **false**.
## bool ShowTransparentLightingLightWorld

***Console*:**`render_show_transparent_lighting_light_world`The value indicating whether the [visualizer](../../../api/library/engine/class.visualizer_cs.md) is displayed for transparent (blend) surfaces whose material is configured to receive lighting from World light (sun). The default value is **false**.
## bool ShowAmbient

***Console*:**`render_show_ambient`The value indicating whether the ambient pass buffer is displayed. The default value is **false**.
## bool ShowGeodeticPivot

***Console*:**`render_show_geodetic_pivot`The value indicating whether [geodetic pivots](../../../objects/geodetics/geodeticpivot/index.md) are displayed. The default value is **false**.
## int ShowLandscapeMask

***Console*:**`render_show_landscape_mask`The number of the [Landscape Terrain detail mask](../../../objects/objects/terrain/landscape_terrain/index.md#details) to be visualized. This method can be used for visual debugging to display the selected detail mask of the Landscape Terrain.
## bool ShowLandscapeAlbedo

***Console*:**`render_show_landscape_albedo`The value indicating if visualization of albedo data of the Landscape Terrain is enabled.
## bool ShowLandscapeTerrainVTStreaming

***Console*:**`render_show_landscape_terrain_vt_streaming`The value indicating if visualization is enabled for [streaming of tiles](../../../objects/objects/terrain/landscape_terrain/index.md#tiling) of the Landscape Terrain megatexture. In this mode colored areas show the tiles that are currently being rendered in a lower resolution until the highest MIP-level is loaded. This method can be used for visual adjustment of the streaming process.
## bool ShowVoxelProbeVisualizer

***Console*:**`render_show_voxel_probe_visualizer`The value indicating if the Voxel Probe visualizer is enabled. The visualizer shows only the selected probe with the grid size*[ShowVoxelProbeVisualizerGridSize](../../...md#render_show_voxel_probe_visualizer_grid_size)* from 7 to 40.
## int ShowVoxelProbeVisualizerGridSize

***Console*:**`render_show_voxel_probe_visualizer_grid_size`The size of the grid that is used to visualize Voxel Probes.
> **Notice:** For the probe to be visualized properly, the grid size should be from 7 to 40.


## float ShowVoxelProbeVisualizerSphereScale

***Console*:**`render_show_voxel_probe_visualizer_sphere_scale`The scale factor of the sphere that is used to visualize Voxel Probes. The sphere size depends on the scale factor and the voxel size.
## int ShowTextures

***Console*:**`render_show_textures`The display mode for texture buffers used by the renderer. The number of displayed buffers depends on the number of buffers in a row specified by the corresponding command*[ShowTexturesNumber](../../...md#render_show_textures_number)*. One of the following values:
- **0** - all buffers are hidden (by default)
- **1** - show render textures (compact)
- **2** - show render textures (full)

## int ShowTexturesOffset

***Console*:**`render_show_textures_offset`The number of the buffer to start displaying from in the full view mode*[ShowTextures](../../...md#render_show_textures)*.
Range of values: **[0, 256]**. The default value is : **0**.
## int ShowTexturesNumber

***Console*:**`render_show_textures_number`The number of buffers in a row and column displayed in the full view mode*[ShowTextures](../../...md#render_show_textures)*. Textures are displayed in the following manner, depending on the set value:
- **1** - a single texture per screen
- **2** - 2x2 textures per screen
- **3** - 3x3 textures per screen
- ... etc.


Range of values: **[0, 16]**. The default value is : **7**.
## float ShowTextureResolutionBlend

***Console*:**`render_show_texture_resolution_blend`The value used for blending the rendered image with the color displaying the texture resolution.
Range of values: **[0, 1]**. The default value is : **0.5**.
## Render.SHOW_TEXTURE_RESOLUTION_UV ShowTextureResolutionUVMode

***Console*:**`render_show_texture_resolution_uv_mode`The UV channel to be used for [visualization of the texture resolution](#ShowTextureResolution). One of the following values:
- **0** - UV0 (by default)
- **1** - UV1

## Render.SHOW_TEXTURE_RESOLUTION ShowTextureResolution

***Console*:**`render_show_texture_resolution`The display mode for texture resolution used by the renderer. One of the following values:
- **0** - disabled (by default)
- **1** - show surfaces depending on maximum resolution of textures used in materials assigned to them applying colors in accordance with the scale
- **2** - show the relationship between maximum texture resolution of the material to the size of triangles on the screen to which it is applied: blue indicates insufficient texture resolution, while yellow tells that it is excessive, if the color is green - everything is ok.

## int ShowTriangles

***Console*:**`render_show_triangles`The wireframe mode for scene triangles. One of the [TRIANGLES_*](#TRIANGLES_DISABLED) values. The default value is **false**.
## Render.SHOW_VERTEX_COLOR ShowVertexColor

***Console*:**`render_show_vertex_color`The value indicating whether displaying of geometry that uses the selected vertex color is enabled. One of the following values:
- **0** - disabled. (by default)
- **1** - Red color.
- **2** - Green color.
- **3** - Blue color.
- **4** - Alpha color.
- **5** - RGB color.

## bool ShowNodesInteractionGrass

***Console*:**`render_show_nodes_interaction_grass`The value indicating whether the visualizer is enabled for nodes with the *Grass Interaction* flag enabled. The default value is **false**.
## bool ShowNodesInteractionClutter

***Console*:**`render_show_nodes_interaction_clutter`The value indicating whether the visualizer is enabled for nodes with the *Clutter Interaction* flag enabled. The default value is **false**.
## bool ShowNodesInteractionTrigger

***Console*:**`render_show_nodes_interaction_trigger`The value indicating whether the visualizer is enabled for nodes with the *Trigger Interaction* flag enabled. The default value is **false**.
## bool TransparentMultipleEnvProbes

***Console*:**`render_transparent_multiple_env_probes`The value indicating if the transparent [multiple environment probes](../../../principles/render/sequence/index.md#transparent_multiple_env_probes) pass is rendered.
> **Notice:** This method takes effect only when the forward rendering pass is used for transparent objects rendering.

 The default value is **true**.
## bool TransparentDeferred

***Console*:**`render_transparent_deferred`The value indicating if the deferred pass for transparent objects is enabled.
> **Notice:** This option takes effect only when the forward rendering pass is used for transparent objects rendering.

  The default value is **true**.
## bool TransparentEnabled

***Console*:**`render_transparent_enabled`The value indicating if the transparent pass is rendered.
> **Notice:** This option takes effect only when the forward rendering pass is used for transparent objects rendering.

  The default value is **true**.
## bool ScreenSpaceEffects

***Console*:**`render_screen_space_effects`The value indicating if rendering of screen-space effects is enabled. The default value is **true**.
## int FieldShorelineResolution

***Console*:**`render_field_shoreline_resolution`The resolution of the texture into which all textures set for all *[FieldShoreline](../../../api/library/fields/class.fieldshoreline_cs.md)* objects are rendered.
> **Notice:** Increased resolution significantly affects performance.

 One of the following values:
- **0** - 128x128 (by default)
- **1** - 256x256
- **2** - 512x512
- **3** - 1024x1024
- **4** - 2048x2048
- **5** - 4096x4096
- **6** - 8192x8192

## bool FieldPrecision

***Console*:**`render_field_precision`The value indicating the precision of textures used for field objects. Either of the following:
- 16-bit precision R16 texture
- 32-bit precision R32F texture

  One of the following values:
- **0** - 16 bit (by default)
- **1** - 32 bit

## int FieldHeightResolution

***Console*:**`render_field_height_resolution`The resolution of the texture into which all textures set for all *[FieldHeight](../../../api/library/fields/class.fieldheight_cs.md)* objects are rendered.
> **Notice:** Increased resolution significantly affects performance.

 One of the following values:
- **0** - 128 x 128
- **1** - 256 x 256
- **2** - 512 x 512 (by default)
- **3** - 1024 x 1024
- **4** - 2048 x 2048
- **5** - 4096 x 4096
- **6** - 8192 x 8192

## float CloudsNoiseStepSkip

***Console*:**`render_clouds_noise_step_skip`The value of the *noise step skip* parameter for clouds. This parameter determines the amount of jitter in the areas between clouds, that is used to reduce banding effect due to insufficient number of steps.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[CloudsQualityPreset](/api/library/rendering/class.render_cs#render_clouds_quality_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float CloudsNoiseLighting

***Console*:**`render_clouds_noise_lighting`The value of the *noise lighting* parameter for the clouds. This parameter determines the amount of jitter for tracing steps of lighting calculation, that is used to reduce banding effect due to insufficient number of steps.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[CloudsQualityPreset](/api/library/rendering/class.render_cs#render_clouds_quality_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float CloudsNoiseIterations

***Console*:**`render_clouds_noise_iterations`The value of the *noise iterations* parameter for clouds. This parameter determines the amount of jitter in the areas within clouds, that is used to reduce banding effect due to insufficient number of steps.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.1f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[CloudsQualityPreset](/api/library/rendering/class.render_cs#render_clouds_quality_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float CloudsNoiseStep

***Console*:**`render_clouds_noise_step`The value of the *noise step* parameter for clouds. This parameter determines the amount of jitter in the areas within clouds, that is used to reduce banding effect due to insufficient number of steps.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[CloudsQualityPreset](/api/library/rendering/class.render_cs#render_clouds_quality_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float CloudsSoftIntersection

***Console*:**`render_clouds_soft_intersection`The [soft intersection distance](../../../editor2/settings/render_settings/clouds/index.md#soft_intersection) for clouds, in meters.
Range of values: **[0.0f, 100000.0f]**. The default value is : **100.0f**.
## int CloudsSamplesCount

***Console*:**`render_clouds_samples_count`The [number of samples](../../../editor2/settings/render_settings/clouds/index.md#samples_count) used for clouds rendering. The higher the value, the less noise in clouds rendering. The following values are available:
- **Low** - 1 sample, low quality
- **Medium** - 3 samples, medium quality
- **High** - 5 samples, high quality
- **Ultra** - 6 samples, ultra quality

  One of the following values:

- *Low* - low quality
- *Medium* - medium quality
- *High* - high quality (by default)
- *Ultra* - ultra quality

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[CloudsQualityPreset](/api/library/rendering/class.render_cs#render_clouds_quality_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int CloudsDownsamplingRendering

***Console*:**`render_clouds_downsampling_rendering`The downsampling rendering mode for clouds. This parameter determines clouds resolution based on current screen resolution.
> **Notice:** This parameter has a significant impact on performance.

 One of the following values:

- *Quarter* - quarter resolution
- *Half* - half resolution (by default)
- *Full* - full resolution

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[CloudsQualityPreset](/api/library/rendering/class.render_cs#render_clouds_quality_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int CloudsInterleavedRendering

***Console*:**`render_clouds_interleaved_rendering`The [interleaved rendering mode](../../../editor2/settings/render_settings/clouds/index.md#interleaved_rendering) for clouds. In cases when clouds are viewed from the ground, or from above (at significant distance) and viewer's velocities are less than 200 units per second, this parameter can be used to provide a significant gain in performance. One of the following values:
- **0** - Disabled (by default)
- **1** - 2×2
- **2** - 4×4
- **3** - 8×8

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[CloudsQualityPreset](/api/library/rendering/class.render_cs#render_clouds_quality_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int CloudsDynamicCoverageResolution

***Console*:**`render_clouds_dynamic_coverage_resolution`The the value defining the size of the square dynamic coverage resolution texture for clouds, in pixels. This parameter determines the quality of dynamic coverage texture for [FieldWeather](../../../objects/effects/fields/field_weather/index.md) objects. Higher values make it possible to preserve texture details at high distances.
> **Notice:** Increased resolution significantly affects performance.

Range of values: **[16, 8192]**. The default value is : **256**.
## float CloudsDynamicCoverageArea

***Console*:**`render_clouds_dynamic_coverage_area`The dynamic coverage area for clouds, in units. This parameter determines visibility distance for coverage of [FieldWeather](../../../objects/effects/fields/field_weather/index.md) objects.
> **Notice:** Increasing dynamic coverage area leads to reduction of quality of FieldWeather coverage texture and loss of details. This effect can be mitigated by increasing dynamic coverage resolution using the corresponding command*[CloudsDynamicCoverageResolution](../../...md#render_clouds_dynamic_coverage_resolution)*.


Range of values: **[10.0f, 400000.0f]**. The default value is : **10000.0f**.
## float CloudsLightingConeRadius

***Console*:**`render_clouds_lighting_cone_radius`The [lighting cone sampling radius](../../../editor2/settings/render_settings/clouds/index.md#lighting_cone_radius) for clouds lighting.
> **Notice:** Low values may result in unnatural behavior as the position of the sun changes.


Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**.
## float CloudsLightingTraceLength

***Console*:**`render_clouds_lighting_tracelength`The [lighting trace length](../../../editor2/settings/render_settings/clouds/index.md#lighting_trace_length) for clouds. This parameter determines the maximum length of a sun ray inside a cloud.
Range of values: **[1.0f, 2048.0f]**. The default value is : **230.0f**.
## int CloudsSamplingQuality

***Console*:**`render_clouds_sampling_quality`The [sampling quality](../../../editor2/settings/render_settings/clouds/index.md#sampling_quality) for clouds. This parameter sets the number of noise samples that affects the cloud shape processing quality. The higher the value, the less are visual artifacts. The following modes are available:
- **Low** - 1 sample, low quality (higher cloud density)
- **Medium** - 3 samples, medium quality
- **High** - 5 samples, high quality
- **Ultra** - 6 samples, ultra quality (lower density, the clouds are softer)


> **Notice:** Visual difference between low and ultra quality is not significant. Therefore, it is recommended to use low settings, when possible, to gain performance.

  One of the following values:

- *Low* - low quality
- *Medium* - medium quality (by default)
- *High* - high quality
- *Ultra* - ultra quality

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[CloudsQualityPreset](/api/library/rendering/class.render_cs#render_clouds_quality_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int CloudsLightingQuality

***Console*:**`render_clouds_lighting_quality`The [lighting quality](../../../editor2/settings/render_settings/clouds/index.md#lighting_quality) for clouds. This parameter determines the number of samples used to calculate lighting for clouds. The following values are available:
- **Low** - 1 sample, low quality
- **Medium** - 3 samples, medium quality
- **High** - 5 samples, high quality
- **Ultra** - 6 samples, ultra quality


> **Notice:** This parameter has a significant impact on performance. Therefore, it is recommended to use low settings, when possible.

  One of the following values:

- *Low* - low quality
- *Medium* - medium quality (by default)
- *High* - high quality
- *Ultra* - ultra quality

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[CloudsQualityPreset](/api/library/rendering/class.render_cs#render_clouds_quality_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool CloudsGroundShadows

***Console*:**`render_clouds_ground_shadows`The value indicating if rendering of shadows from the clouds on the ground is enabled. The default value is **true**.
## bool CloudsEnabled

***Console*:**`render_clouds_enabled`The value indicating if rendering of clouds is enabled. The default value is **true**.
## float CloudsStepAccuracy

***Console*:**`render_clouds_step_accuracy`The accuracy of ray marching steps. This parameter enables you to improve the visual look of clouds when viewed from inside a cloud layer. It reduces the noise of lighting and clouds shape for long ray marching distances, adds some noise-based blur to a sharp border at the bottom sphere of the cloud layer (rounded) and removes popping effect when leaving a rounded cloud layer. *Higher* values provide more accurate form and less noise, while *lower* ones gain more performance.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[CloudsQualityPreset](/api/library/rendering/class.render_cs#render_clouds_quality_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool CloudsAccurateLayersSorting

***Console*:**`render_clouds_accurate_layers_sorting`The value indicating if correct sorting of intersecting cloud layers is enabled.
> **Notice:** Enabling this feature may reduce raymarching quality as samples shall be distributed among all layers.

 The default value is **false**.
## int CloudDistortionTexture

***Console*:**`render_clouds_distortion_texture`The value indicating which texture type is used for clouds distortion at the moment. This parameter has a significant impact on performance:
- **2D Texture** - more performance-friendly, but may cause an excessive vertical extrusion of clouds.
- **3D Texture** - ensures homogeneous detail distortion and better image quality, but at a higher performance cost.

  One of the following values:
- **0** - 2D texture (by default)
- **1** - 3D texture

## bool CloudsInterleavedRenderingTemporal

***Console*:**`render_clouds_interleaved_rendering_temporal`The value indicating if temporal accumulation of noises for interleaved sampling for clouds is enabled.
> **Notice:** Works only when the clouds interleaved rendering mode*[CloudsInterleavedRendering](../../...md#render_clouds_interleaved_rendering)* is set to 2x2.

  The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[CloudsQualityPreset](/api/library/rendering/class.render_cs#render_clouds_quality_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float CloudsDepthBasedReconstructionThreshold

***Console*:**`render_clouds_depth_based_reconstruction_threshold`The depth threshold value for clouds depth-based reconstruction mode*[CloudsDepthBasedReconstruction](../../...md#render_clouds_depth_based_reconstruction)*. This value defines the depth difference starting from which pixels are considered to be related to different surfaces.
Range of values: **[0.0f, inf]**. The default value is : **100.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[CloudsQualityPreset](/api/library/rendering/class.render_cs#render_clouds_quality_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool CloudsDepthBasedReconstruction

***Console*:**`render_clouds_depth_based_reconstruction`The value indicating if clouds ray-marched depth is used for upsampling the downsampled clouds without obscuring the geometry and reprojection depending on the cloud depth. Recommended for flying through clouds.
> **Notice:** Works only with the clouds downsampling rendering mode*[CloudsDownsamplingRendering](../../...md#render_clouds_downsampling_rendering)* set to half and/or the clouds interleaved rendering mode*[CloudsInterleavedRendering](../../...md#render_clouds_interleaved_rendering)* set to 2x2.

  The default value is **false**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[CloudsQualityPreset](/api/library/rendering/class.render_cs#render_clouds_quality_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool CloudsFarClipping

***Console*:**`render_clouds_far_clipping`The value indicating if [far-plane clipping](../../../editor2/camera_settings/index.md#camera_settings) is used for clouds visibility.
Controlling clouds visibility by increasing the far-plane distance significantly affects performance in many aspects (dynamic Environment Probes, etc.). You can disable this option when necessary as an optimization.

 The default value is **true**.
## float CloudsRoundedPlanetRadius

***Console*:**`render_clouds_rounded_planet_radius`The radius of the planet to be used for clouds curving. Visual curving can be used to make clouds look more natural imitating planet's curvature.
Range of values: **[100.0f, inf]**. The default value is : **200000.0f**.
## bool CloudsRounded

***Console*:**`render_clouds_rounded`The value indicating if cloud layers are to be curved to make them look more natural imitating planet's curvature. The default value is **true**.
## int WaterAnisotropy

***Console*:**`render_water_anisotropy`The water texture anisotropy level. The following values are available:
- 1x - anisotropy level 1
- 2x - anisotropy level 2
- 4x - anisotropy level 4
- 8x - anisotropy level 8
- 16x - anisotropy level 16

  One of the following values:
- **0** - 1x
- **1** - 2x (by default)
- **2** - 4x
- **3** - 8x
- **4** - 16x

## int WaterRefractionQuality

***Console*:**`render_water_refraction_quality`The quality of water refraction. One of the following values:

- *Low* - low quality
- *Medium* - medium quality
- *High* - high quality (by default)
- *Ultra* - ultra quality

## int WaterSSRQuality

***Console*:**`render_water_ssr_quality`The resolution of water SSR (Screen Space Reflections). One of the following values:

- *Low* - low quality
- *Medium* - medium quality (by default)
- *High* - high quality
- *Ultra* - ultra quality

## bool WaterLights

***Console*:**`render_water_lights`The value indicating if rendering of lights on the water surface is enabled.
> **Notice:** The option doesn't affect the [World Light source](../../../objects/lights/world/index.md).

 The default value is **true**.
## bool WaterVoxelProbes

***Console*:**`render_water_voxel_probes`The value indicating if voxel probes are enabled for water rendering. The default value is **true**.
## bool WaterEnvironmentProbes

***Console*:**`render_water_environment_probes`The value indicating if rendering of environment probes on the water surface is enabled. The default value is **true**.
## bool WaterOpacityDepth

***Console*:**`render_water_opacity_depth`The value indicating if depth data for water is written to the opacity buffer. The default value is **true**.
## bool WaterShafts

***Console*:**`render_water_shafts`The value indicating if rendering of underwater shafts is enabled. The default value is **true**.
## bool WaterShorelineWetness

***Console*:**`render_water_shoreline_wetness`The value indicating if the wetness effect for objects near the shoreline is enabled. The default value is **true**.
## bool WaterSSRIncreasedAccuracy

***Console*:**`render_water_ssr_increased_accuracy`The value indicating if increased accuracy for the water SSR (Screen Space Reflections). This option reduces visual artifacts by increasing accuracy of the last step. The default value is **false**.
## bool WaterSSR

***Console*:**`render_water_ssr`The value indicating if the SSR (Screen Space Reflections) effect is enabled for water. The default value is **true**.
## bool WaterEnabled

***Console*:**`render_water_enabled`The value indicating if rendering of water is enabled. The default value is **true**.
## int TerrainGlobalAnisotropy

***Console*:**`render_terrain_global_anisotropy`The [global terrain](../../../objects/objects/terrain/terrain_global/index.md) texture anisotropy level (degree of anisotropic filtering). Anisotropy for the global terrain has a huge impact for the performance if terrain has a lot of tiled detail materials as anisotropy filtering for the terrain is much slower than for the other objects. One of the following values:
- **0** - anisotropy level 1
- **1** - anisotropy level 2
- **2** - anisotropy level 4 (by default)
- **3** - anisotropy level 8
- **4** - anisotropy level 16

## bool TerrainGlobalHoles

***Console*:**`render_terrain_global_holes`The value indicating if [decal-based holes](../../../objects/objects/terrain/terrain_global/index.md#decal_holes) are enabled for the [global terrain](../../../objects/objects/terrain/terrain_global/index.md). The default value is **false**.
## bool TerrainGlobalDisplacementNormal

***Console*:**`render_terrain_global_displacement_normal`The value indicating if displacement mapping for the [Global Terrain](../../../objects/objects/terrain/terrain_global/index.md) rendering uses normals. The default value is **false**.
## bool TerrainGlobalDisplacement

***Console*:**`render_terrain_global_displacement`The value indicating if displacement mapping is enabled for the [Global Terrain](../../../objects/objects/terrain/terrain_global/index.md). The default value is **false**.
## bool TerrainGlobalTriplanar

***Console*:**`render_terrain_global_triplanar`The value indicating if [triplanar texture mapping](../../../objects/objects/terrain/terrain_global/details/index.md#triplanar) is enabled for the [Global Terrain](../../../objects/objects/terrain/terrain_global/index.md). If disabled, planar UV-mapping is used. The default value is **false**.
## float SSDirtConvexityMetalnessVisibility

***Console*:**`render_ssdirt_convexity_metalness_visibility`The [metalness visibility](../../../editor2/settings/render_settings/ssdirt/index.md#convexity_metalness_visibility) value for convexities. A multiplier that determines the degree of impact of the effect on metalness buffer (the *higher* the value the more metalness buffer is affected. SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**.
## float SSDirtConvexityMetalness

***Console*:**`render_ssdirt_convexity_metalness`The [metalness](../../../editor2/settings/render_settings/ssdirt/index.md#convexity_metalness) value for convexities. When set to 0 (by default), the SSDirt effect does not modify metalness buffer in convex areas. SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**.
## float SSDirtConvexityExponent

***Console*:**`render_ssdirt_convexity_exponent`The [exponent](../../../editor2/settings/render_settings/ssdirt/index.md#convexity_exponent) value that determines the rate of gradual change of intensity along the radius for convexities. *Lower* values make gradual change of intensity smoother. SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## vec4 SSDirtConvexityColor

***Console*:**`render_ssdirt_convexity_color`The [color multiplier](../../../editor2/settings/render_settings/ssdirt/index.md#convexity_color) for the Albedo texture used for convexities (global wear and scratch color pattern). SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
**vec4(0.48f, 0.44f, 0.39f, 1.0f)** - default value
## float SSDirtConvexityTextureSize

***Console*:**`render_ssdirt_convexity_texture_size`The scaling factor for the textures used for convexities. SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float SSDirtCavityMetalnessVisibility

***Console*:**`render_ssdirt_cavity_metalness_visibility`The [metalness visibility](../../../editor2/settings/render_settings/ssdirt/index.md#cavity_metalness_visibility) value for cavities. A multiplier that determines the degree of impact of the effect on metalness buffer (the *higher* the value the more metalness buffer is affected. SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**.
## float SSDirtCavityMetalness

***Console*:**`render_ssdirt_cavity_metalness`The [metalness](../../../editor2/settings/render_settings/ssdirt/index.md#cavity_metalness) value for cavities. When set to 0 (by default), the SSDirt effect does not modify metalness buffer in cavities. SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**.
## float SSDirtCavityExponent

***Console*:**`render_ssdirt_cavity_exponent`The [exponent](../../../editor2/settings/render_settings/ssdirt/index.md#cavity_exponent) value that determines the rate of gradual change of intensity along the radius for cavities. *Lower* values make gradual change of intensity smoother. SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## vec4 SSDirtCavityColor

***Console*:**`render_ssdirt_cavity_color`The [color multiplier](../../../editor2/settings/render_settings/ssdirt/index.md#cavity_color) for the Albedo texture used for cavities (global dirt and dust color pattern). SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
**vec4(0.26f, 0.24f, 0.21f, 1.0f)** - default value
## float SSDirtCavityTextureSize

***Console*:**`render_ssdirt_cavity_texture_size`The scaling factor for the textures used for cavities. SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## string SSDirtConvexityShadingTextureName

The name of the shading texture to be used for convexities. *Red* channel of this texture defines metalness pattern for all convexities globally (other channels are ignored). SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
## string SSDirtConvexityAlbedoTextureName

The name of the albedo texture to be used for convexities. This texture defines wear and scratch color pattern for all convexities globally. SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
## string SSDirtCavityShadingTextureName

The name of the shading texture to be used for cavities. *Red* channel of this texture defines metalness pattern for all cavities globally (other channels are ignored). SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
## string SSDirtCavityAlbedoTextureName

The name of the albedo texture to be used for cavities. This texture defines wear and scratch color pattern for all cavities globally. SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
## bool SSDirtIncreaseAccuracy

***Console*:**`render_ssdirt_increase_accuracy`The value indicating if increased accuracy for the [SSDirt](../../../editor2/settings/render_settings/ssdirt/index.md) effect. This option should be used to remove visual artefacts along the screen edges, in case if they appear. Otherwise, it should be disabled. SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled. The default value is **false**.
## float SSDirtPerspective

***Console*:**`render_ssdirt_perspective`The [perspective](../../../editor2/settings/render_settings/ssdirt/index.md#perspective) value, that determines the degree of impact of distance from the camera on the radius of the Screen-Space Dirt effect.
- 0.0f - radius of the effect is bound to screen space (it remains constant relative to screen size, regardless of the distance to the camera).
- 1.0f - radius of the effect is bound to world space (it remains the same relative to objects, i.e. gets smaller as the camera moves away from them).

SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.02f**.
## float SSDirtAngleBias

***Console*:**`render_ssdirt_angle_bias`The angle bias value to limit the [SSDirt](../../../editor2/settings/render_settings/ssdirt/index.md) effect where information cannot be obtained. This parameter can be used to remove visual artefacts at the edges of polygons. SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
> **Notice:** This parameter affects both, concave and convex areas.


Range of values: **[0.0f, 1.0f]**. The default value is : **0.35f**.
## float SSDirtThreshold

***Console*:**`render_ssdirt_threshold`The [threshold](../../../editor2/settings/render_settings/ssdirt/index.md#threshold) of the SSDirt effect. It determines depth limit for the SSDirt effect in areas where information cannot be obtained. *Higher* values make the effect less pronounced. SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
## float SSDirtRadius

***Console*:**`render_ssdirt_radius`The [size](../../../editor2/settings/render_settings/ssdirt/index.md#radius) of the SSDirt effect. SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float SSDirtIntensity

***Console*:**`render_ssdirt_intensity`The [intensity](../../../editor2/settings/render_settings/ssdirt/index.md#intensity) of the SSDirt effect.
- By the minimum value of 0.0f, the effect is not visible.
- *Higher* values make the effect more pronounced.

 SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## int SSDirtResolution

***Console*:**`render_ssdirt_resolution`The [resolution](../../../editor2/settings/render_settings/ssdirt/index.md#resolution) of the SSDirt effect. SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled.
> **Notice:** This parameter significantly affects performance, so choose it reasonably.

 One of the following values:

- *Quarter* - quarter resolution
- *Half* - half resolution (by default)
- *Full* - full resolution

## int SSDirtQuality

***Console*:**`render_ssdirt_quality`The [quality](../../../editor2/settings/render_settings/ssdirt/index.md#quality) for the SSDirt effect. SSDirt*[SSDirt](../../...md#render_ssdirt)* must be enabled. Quality implies the number of samples used for the Screen-Space Dirt effect:
- Low - 4 samples
- Medium - 8 samples
- High - 16 samples
- Ultra - 32 samples


> **Notice:** This parameter significantly affects performance, so choose it reasonably.

  One of the following values:

- *Low* - low quality
- *Medium* - medium quality
- *High* - high quality (by default)
- *Ultra* - ultra quality

## bool SSDirt

***Console*:**`render_ssdirt`The value indicating if the [Screen-Space Dirt](../../../editor2/settings/render_settings/ssdirt/index.md) (SSDirt) effect is enabled. The default value is **false**.
## float SSBevelRadius

***Console*:**`render_ssbevel_radius`The [size](../../../editor2/settings/render_settings/ssbevel/index.md#radius) of the Screen-Space Bevel effect. To use this option, rendering of SSBevel *[SSBevel](../../...md#render_ssbevel)* should be enabled.
Range of values: **[0.0f, inf]**. The default value is : **0.01f**.
## bool SSBevelNoise

***Console*:**`render_ssbevel_noise`The value indicating if the [noise](../../../editor2/settings/render_settings/ssbevel/index.md#noise) is enabled for smoothing bevels. It is recommended to use the noise with TAA*[TAA](../../...md#render_taa)* enabled to avoid visual artifacts. The bevel noise is applied at a certain distance from the camera (i.e. if the camera is too far from the object with bevels, the noise won't be applied). To use this option, rendering of SSBevel*[SSBevel](../../...md#render_ssbevel)* should be enabled. The default value is **true**.
## int SSBevelQuality

***Console*:**`render_ssbevel_quality`The [quality mode](../../../editor2/settings/render_settings/ssbevel/index.md#quality) for the screen-space bevels. One of the following values:

- *Low* - low quality
- *Medium* - medium quality (by default)
- *High* - high quality
- *Ultra* - ultra quality

## int SSBevelVertexNormal

***Console*:**`render_ssbevel_vertex_normal`The rendering mode of the screen-space bevels. The following modes are available:
- **Better Edges** smoothes vertex and surface normals of the object. In this mode, the relief created by using Normal Mapping will be smoothed along with the mesh edges.
- **Better Normals** smoothes only vertex normals. In this mode, only edges of the mesh geometry will be bevelled. The mode may produce visual artifacts on the edges. However, they can be reduced by increasing quality settings of [anti-aliasing](../../../principles/render/antialiasing/taa.md).

 To use this option, rendering of SSBevel*[SSBevel](../../...md#render_ssbevel)* should be enabled.  One of the following values:
- **0** - Better Edges (by default)
- **1** - Better Normals

## bool SSBevel

***Console*:**`render_ssbevel`The value indicating if the Screen-Space Bevels (SSBevel effect) are enabled. The default value is **true**.
## bool ScreenPrecision

***Console*:**`render_screen_precision`The value indicating the current screen precision. This parameter determines the texture format used for screen HDR buffers. One of the following values:
- **0** - RG11B10F
- **1** - RGBA16F (by default)

## bool ShadowsFilterNoise

***Console*:**`render_shadows_filter_noise`The value indicating if noise for shadow filtering is enabled. This noise is used for smoothing. The default value is **true**.
## int ShadowsFilterMode

***Console*:**`render_shadows_filter_mode`The global filtering mode to be used for shadows from all light sources by default. This mode determines quality of soft shadows. *Higher* quality produces *smoother* shadow edges. When disabled, no filtering is performed and the stair-step effect is clearly seen at the edges of shadows.
> **Notice:** You can set filtering mode or disable filtering for each light source [individually](../../../api/library/lights/class.light_cs.md#setShadowFilterMode_int_void).

  One of the following values:
- **0** - Disabled
- **1** - Low
- **2** - Medium (by default)
- **3** - High
- **4** - Ultra

## bool ShadowsPenumbraNoise

***Console*:**`render_shadows_penumbra_noise`The value indicating if noise for penumbra rendering is enabled. This noise is used for smoothing. The default value is **true**.
## int ShadowsPenumbraMode

***Console*:**`render_shadows_penumbra_mode`The global quality mode to be used for rendering penumbra from all light sources by default. This mode enables simulation of real-world shadows by keeping sharp contact shadows closer to the base and softening the farther the shadow stretches away. *Higher* values produce *softer* shadows. When disabled, shadow edges are crisp and sharp (no shadow softness at all).
> **Notice:** You can set penumbra quality mode or disable penumbra rendering for each light source [individually](../../../api/library/lights/class.light_cs.md#setShadowPenumbraMode_int_void). But these per-light quality settings are ignored when global quality is set to *Disabled*.

  One of the following values:
- **0** - Disabled
- **1** - Low (by default)
- **2** - Medium
- **3** - High
- **4** - Ultra

## bool ShadowsScreenSpace

***Console*:**`render_shadows_screen_space`The value indicating if screen space shadows are enabled. They provide high-quality penumbra, per-light work, per-pixel detail at any zoom level and infinite visibility distance (when enabled, distant objects can cast shadows next to the horizon). Supports depth cutout parallax. Screen space shadows can be mixed with regular ones. The default value is **true**.
## bool ShadowsAlphaTest

***Console*:**`render_shadows_alpha_test`The value indicating if alpha test is enabled for shadows. The default value is **true**.
## bool ShadowsWorldLerpCascades

***Console*:**`render_shadows_world_lerp_cascades`The value indicating if [linear interpolation of shadow cascades](../../../editor2/settings/render_settings/shadows/index.md#lerp_shadow_cascades) is enabled, making transitions between cascades smoother. This option significantly affects performance, as two shadow maps are rendered in transition areas. The default value is **true**.
## float ShadowsTranslucentDepth

***Console*:**`render_shadows_translucent_depth`The global translucence depth value defining how deep the light goes through translucent objects shifting the shadow. The *higher* the value, the *deeper* the light penetrates translucent objects shifting the shadow.
Range of values: **[0.0f, inf]**. The default value is : **0.1f**.
## bool Shadows

***Console*:**`render_shadows`The value indicating whether shadows are rendered. The default value is **true**.
## bool LightsLensFlares

***Console*:**`render_lights_lens_flares`The value indicating if rendering of [per-light lens flares](../../../api/library/lights/class.light_cs.md#setLensFlaresEnabled_int_void) is enabled. The default value is **true**.
## int LightsForwardPerObjectVoxel

***Console*:**`render_lights_forward_per_object_voxel`The maximum number of Voxel Probes per object (available only for materials rendered in the [forward rendering pass](../../../principles/render/sequence/index.md#transparent)). You should set the nonzero value to increase performance: it is not recommended to use more than 4 Voxel Probes per object.
Range of values: **[0, 128]**. The default value is : **4**.
## int LightsForwardPerObjectEnv

***Console*:**`render_lights_forward_per_object_env`The maximum number of Environment Probes per object (available only for materials rendered in the [forward rendering pass](../../../principles/render/sequence/index.md#transparent)). You should set the nonzero value to increase performance: it is not recommended to use more than 4 Voxel Probes per object.
Range of values: **[0, 128]**. The default value is : **4**.
## int LightsForwardPerObjectPlanar

***Console*:**`render_lights_forward_per_object_planar`The maximum number of Planar Reflection Probes per object (available only for materials rendered in the [forward rendering pass](../../../principles/render/sequence/index.md#transparent)). You should set the nonzero value to increase performance: it is not recommended to use more than 4 Planar Reflection Probes per object.
Range of values: **[0, 128]**. The default value is : **4**.
## int LightsForwardPerObjectProj

***Console*:**`render_lights_forward_per_object_proj`The maximum number of Projected lights per object (available only for materials rendered in the [forward rendering pass](../../../principles/render/sequence/index.md#transparent)). You should set the nonzero value to increase performance: it is not recommended to use more than 4 Projected lights per object.
Range of values: **[0, 128]**. The default value is : **4**.
## int LightsForwardPerObjectOmni

***Console*:**`render_lights_forward_per_object_omni`The maximum number of Omni lights per object (available only for materials rendered in the [forward rendering pass](../../../principles/render/sequence/index.md#transparent)). You should set the nonzero value to increase performance: it is not recommended to use more than 4 Omni lights per object.
Range of values: **[0, 128]**. The default value is : **4**.
## int LightsForwardPerObjectWorld

***Console*:**`render_lights_forward_per_object_world`The maximum number of World lights per object (available only for materials rendered in the [forward rendering pass](../../../principles/render/sequence/index.md#transparent)). You should set the nonzero value to increase performance: it is not recommended to use more than 4 World lights per object.
Range of values: **[0, 128]**. The default value is : **4**.
## int DirectLightingInterleavedSamples

***Console*:**`render_direct_lighting_interleaved_samples`The number of samples for interleaved rendering of direct lighting defining the number of pixels to be skipped during interleaved rendering of direct lighting with subsequent reconstruction of neighboring pixels using the data from previous frames (defines the size of reduced lights buffer relative to original size).
- **1 x 2** - half of all pixels are rendered skipping each second line (1.0 * width x 0.5 * height)
- **2 x 2** - quarter of all pixels are rendered skipping each second line and row (0.5 * width x 0.5 * height)

  One of the following values:
- **0** - 1 x 2 (by default)
- **1** - 2 x 2

## int DirectLightingInterleavedColorClamping

***Console*:**`render_direct_lighting_interleaved_color_clamping`The color clamping mode to be used for interleaved rendering of direct lighting. This mode is used to reduce ghosting effect: higher values increase clamping intensity but may cause flickering on rippled reflective surfaces (as this mode is not so good at the object's edges). When disabled, shadows and reflections have a lag as they are several frames behind.  One of the following values:
- **0** - Disabled
- **1** - Low (by default)
- **2** - Medium
- **3** - High
- **4** - High + Velocity

## bool DirectLightingInterleavedCatmullResampling

***Console*:**`render_direct_lighting_interleaved_catmull_resampling`The value indicating if the Catmull-Rom resampling for interleaved rendering of direct lighting is enabled. This mode allows you to reduce image blurring when the camera moves forward/backward. The default value is **false**.
## bool DirectLightingInterleaved

***Console*:**`render_direct_lighting_interleaved`The value indicating if interleaved mode for rendering direct lighting is enabled. When enabled, lights are rendered in half resolution with subsequent reconstruction of neighboring pixels using the data from previous frames. This mode requires a high framerate (60+ FPS), otherwise anti-aliasing quality reduces and ghosting effect becomes more pronounced. Recommended for relatively static scenes which contain a lot of light sources and do not have a lot of reflective surfaces (in case of small number of light sources may reduce performance). The default value is **false**.
## bool IndirectLightingInterleaved

***Console*:**`render_indirect_lighting_interleaved`The value indicating if interleaved mode for rendering indirect lighting is enabled. When enabled, lights are rendered in half resolution with subsequent reconstruction of neighboring pixels using the data from previous frames. This mode requires a high framerate (60+ FPS), otherwise anti-aliasing quality reduces and ghosting effect becomes more pronounced. Recommended for relatively static scenes which contain a lot of light sources and do not have a lot of reflective surfaces (in case of small number of light sources may reduce performance). The default value is **false**.
## bool LightsEnabled

***Console*:**`render_lights_enabled`The value indicating if rendering of lights is enabled. The default value is **true**.
## vec2 OccludersShadowsResolution

***Console*:**`render_occluders_shadows_resolution`The resolution of the texture, to which occluders for shadows*[OccludersShadows](../../...md#render_occluders_shadows)* are rendered.
From **1x1** to **1024x1024** Default: **512x512**
## bool OccludersShadows

***Console*:**`render_occluders_shadows`The value indicating whether rendering of occluders for shadows is enabled. The default value is **false**.
## vec2 OccludersResolution

***Console*:**`render_occluders_resolution`The resolution of the texture, to which occluders*[Occluders](../../...md#render_occluders)* are rendered.
From **1x1** to **1024x1024** Default: **128x64**
## bool Occluders

***Console*:**`render_occluders`The value indicating if rendering of occluders is enabled. The default value is **true**.
## int OcclusionQueriesNumFrames

***Console*:**`render_occlusion_queries_num_frames`The number of frames for additional hardware occlusion query test performed before sending data to GPU. Make sure that the additional hardware occlusion query test*[OcclusionQueries](../../...md#render_occlusion_queries)* is enabled.
Range of values: **[0, 1024]**. The default value is : **5**.
## bool OcclusionQueries

***Console*:**`render_occlusion_queries`The value indicating if additional hardware occlusion query test before sending data to GPU is enabled. This test is performed for all objects with the *[Culled by occlusion query](../../../editor2/node_parameters/transformation_common/index.md#query)* flag set. The default value is **true**.
## quat SkyRotation

The sky rotation.
## 🔒︎ float EnvironmentSkyIntensity

The intensity of the environment sky set for the preset that overlays the other ones. To get the sky intensity for the specific preset, use *[RenderEnvironmentPreset.GetSkyIntensity()](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getSkyIntensity_float)*.
```csharp
// get a sky intensity for the preset that overlays the others
Render.GetEnvironmentSkyIntensity();
// get a sky intensity for the second environment preset
RenderEnvironmentPreset preset = Render.GetEnvironmentPreset(1);
preset.GetSkyIntensity();

```


## 🔒︎ float EnvironmentReflectionIntensity

The intensity of the environment reflections for the preset that overlays the other ones. 0 value means no environment reflections for the preset. To get the reflection intensity for the specific preset, use *[RenderEnvironmentPreset.getReflectionIntensity()](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getReflectionIntensity_float)*.
```csharp
// get a reflection intensity for the preset that overlays the others
Render.GetEnvironmentReflectionIntensity();
// get a reflection intensity for the second environment preset
RenderEnvironmentPreset preset = Render.GetEnvironmentPreset(1);
preset.GetReflectionIntensity();

```


## 🔒︎ float EnvironmentAmbientIntensity

The intensity of the environment ambient lighting for the preset that overlays the other ones. 0 value means no environment ambient lighting for the preset. The higher the value, the more ambient lighting affects environment. To get the ambient intensity for the specific preset, use *[RenderEnvironmentPreset.getAmbientIntensity()](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getAmbientIntensity_float)*.
```csharp
// get an ambient intensity for the preset that overlays the others
Render.GetEnvironmentAmbientIntensity();
// get an ambient intensity for the second environment preset
RenderEnvironmentPreset preset = Render.GetEnvironmentPreset(1);
preset.GetAmbientIntensity();

```


## 🔒︎ float EnvironmentHazeDensity

The [haze density](../../../editor2/settings/render_settings/environment/index.md#haze_density) set for the preset that overlays the other ones. To get the haze density for the specific preset, use *[RenderEnvironmentPreset.getHazeDensity()](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazeDensity_float)*.
```csharp
// get a haze density for the preset that overlays the others
Render.GetEnvironmentHazeDensity();
// get a haze density for the second environment preset
RenderEnvironmentPreset preset = Render.GetEnvironmentPreset(1);
preset.GetHazeDensity();

```


## 🔒︎ float EnvironmentHazeMaxDistance

The distance starting at which the haze becomes completely solid, so nothing will be seen behind. To get the haze maximum visibility distance for the specific preset, use *[RenderEnvironmentPreset.GetHazeMaxDistance()](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazeMaxDistance_float)*.
```csharp
// get a haze maximum visibility distance for the preset that overlays the others
Render.GetEnvironmentHazeMaxDistance();
// get a haze maximum visibility distance for the second environment preset
RenderEnvironmentPreset preset = Render.GetEnvironmentPreset(1);
preset.GetHazeMaxDistance();

```


## 🔒︎ vec4 EnvironmentHazeColor

The [haze color](../../../editor2/settings/render_settings/environment/index.md#haze_color) for the preset that overlays the other ones.
> **Notice:** This function will return color only if the [HAZE_SOLID](#HAZE_SOLID) mode is set via *[setEnvironmentHazeMode()](#setEnvironmentHazeMode_int_void)*.

To get the haze color for the specific preset, use *[RenderEnvironmentPreset.getHazeColor()](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazeColor_vec4)*.
```csharp
// get a haze color for the preset that overlays the others
Render.GetEnvironmentHazeColor();
// get a haze color for the second environment preset
RenderEnvironmentPreset preset = Render.GetEnvironmentPreset(1);
preset.GetHazeColor();

```


## int EnvironmentHazeResolution

***Console*:**`render_environment_haze_resolution`The resolution scale for rendering the environment haze effect (quarter, half, or full). Lower values improve performance at the cost of quality. One of the following values:

- *Quarter* - quarter resolution
- *Half* - half resolution
- *Full* - full resolution (by default)

## float EnvironmentHazeScreenSpaceGlobalIlluminationDistanceMax

***Console*:**`render_environment_haze_screen_space_global_illumination_distance_max`The maximum distance within which Screen Space Haze GI calculations are performed.
Range of values: **[0.0f, inf]**. The default value is : **100000.0f**.
## float EnvironmentHazeScreenSpaceGlobalIlluminationDistanceMin

***Console*:**`render_environment_haze_screen_space_global_illumination_distance_min`The minimum distance at which Screen Space Haze GI calculations start to take effect.
Range of values: **[0.0f, inf]**. The default value is : **98000.0f**.
## int EnvironmentCubemapBlendMode

***Console*:**`render_environment_cubemap_blend`The blending mode for the environment cubemap. One of the following values:
- **0** - alpha blend (by default)
- **1** - additive blend
- **2** - multiply
- **3** - overlay

## Render.GGX_MIPMAPS_QUALITY EnvironmentGGXMipmapsQuality

***Console*:**`render_environment_ggx_mipmaps_quality`The GGX Mipmap quality mode for environment reflections on rough surfaces. Quality modes differ in the number of rays used to create a reflection on a rough surface. One of the following values:

- *Low* - low quality (by default)
- *Medium* - medium quality
- *High* - high quality
- *Ultra* - ultra quality

## int EnvironmentHazeGradient

***Console*:**`render_environment_haze_gradient`The environment haze gradient mode. By using this option, you can make the haze look more realistic for a specific distance range.
- Short Distance Range - better suitable for near-surface haze
- Long Distance Range - better suitable for hazy mountains
- Physically Based - for physically based haze simulation

  One of the following values:
- **0** - Short Distance Range (by default)
- **1** - Long Distance Range
- **2** - Physically Based

## int EnvironmentHazeMode

***Console*:**`render_environment_haze`The [mode](../../../editor2/settings/render_settings/environment/index.md#haze) for the haze effect.
- If **Disabled**, no haze is applied.
- The **Solid** mode uses the solid color from the *[Color](../../../editor2/settings/render_settings/environment/index.md#haze_color)* parameter.
- The **Scattering** mode uses the color from the sky LUTs is blended with the *[Color](../../../editor2/settings/render_settings/environment/index.md#haze_color)* parameter. This value is recommended for better realism: objects will smoothly fade into the distance.

  One of the following values:
- **0** - haze disabled
- **1** - haze colored the specific color
- **2** - haze colored in accordance with the sky LUT (by default)

## bool Environment

***Console*:**`render_environment`The value indicating if rendering of environment of the scene is enabled. The default value is **true**.
## string ColorCorrectionLUTPath

The name of a new color transformation texture (LUT).
## vec4 ColorCorrectionWhite

***Console*:**`color_correction_white`The white balance of the scene.
**vec4_zero** - default value (black)
## float ColorCorrectionGamma

***Console*:**`color_correction_gamma`The Gamma correction value for the scene.
Range of values: **[0.5f, 1.5f]**. The default value is : **1.0f**.
## 🔒︎ TextureRamp ColorCorrectionRamp

The Color Correction ramp texture of the scene. An instance of the [TextureRamp](../../../api/library/rendering/class.textureramp_cs.md) class with 4 channels:
- Channels 0, 1, 2 - the Red, Green and Blue channels of the [Color Correction](../../../editor2/settings/render_settings/color/index.md#color_curve) ramp.
- Channel 3 - the [Saturation Correction](../../../editor2/settings/render_settings/color/index.md#saturation) ramp.


## Palette ColorCorrectionSaturation

***Console*:**`color_correction_saturation`The [saturation adjustment](../../../editor2/settings/render_settings/color/index.md#saturation_palette) values for the scene.List of palette colors: 0 - Red, 1 - Orange, 2 - Yellow, 3 - Chartreuse, 4 - Green, 5 - Spring green, 6 - Cyan, 7 - Azure, 8 - Blue, 9 - Violet, 10 - Magenta, 11 - Rose.
**(1,1,1,1,1,1,1,1,1,1,1,1)** - default value
## Palette ColorCorrectionHueShift

***Console*:**`color_correction_hue_shift`The [hue adjustment](../../../editor2/settings/render_settings/color/index.md#hue_palette) values for the scene. List of palette colors: 0 - Red, 1 - Orange, 2 - Yellow, 3 - Chartreuse, 4 - Green, 5 - Spring green, 6 - Cyan, 7 - Azure, 8 - Blue, 9 - Violet, 10 - Magenta, 11 - Rose.
**(0,0,0,0,0,0,0,0,0,0,0,0)** - default value
## float ColorCorrectionContrast

***Console*:**`color_correction_contrast`The overall contrast value for the scene.
Range of values: **[-1.0f, 1.0f]**. The default value is : **0.0f**.
## float ColorCorrectionBrightness

***Console*:**`color_correction_brightness`The overall brightness value for the scene.
Range of values: **[-1.0f, 1.0f]**. The default value is : **0.0f**.
## bool ColorCorrectionPreserveSaturation

***Console*:**`color_correction_preserve_saturation`The value indicating if initial scene color saturation is to be preserved after applying color correction. The default value is **false**.
## vec4 FadeColor

***Console*:**`render_fade_color`The fade color for the scene on the screen. By gradually changing this value it is possible to create "fade in" and "fade out" effects depending on the w component of the given vector. For example, when the following vectors are passed the result will be:
- vec4(1,1,1,1) - a fully white screen. Positive w results in additive blending.
- vec4(0.5,0.5,0.5,1) - light colors on the screen.
- vec4(1,0,0,1) - R channel for all screen colors is to its maximum; G and B without changes.
- vec4(0,0,0,0) - there is no fading (no color alterations are done to the screen).
- vec4(1,1,1,-1) - a fully black screen. Negative w results in scene colors * (1 - RGB), where RGB is the first three components of the passed vector.
- vec4(0.5,0.5,0.5,-1) - dark colors on the screen.


**vec4_zero** - default value (white)
## vec4 BackgroundColor

***Console*:**`render_background_color`The [background color](../../../editor2/settings/render_settings/environment/index.md#background_color) vector. The Alpha channel of this color sets background transparency: lower alpha channel values produce darker background color. This parameter allows creating colored transparent background instead of rendering an environment cubemap. However, if the environment cubemap is rendered, the background color will always be rendered over the environment.
**vec4_one** - default value (white)
## vec4 WireframeColor

***Console*:**`render_wireframe_color`The color of the wireframe.
**vec4_one** - default value (white)
## vec3 LensDispersion

***Console*:**`render_lens_dispersion`The color displacement for red, green, and blue channels of the lens flares. Can be used to create light dispersion (chromatic aberrations). If a negative value is set for a channel, 0 will be used instead. To use this option, rendering of lens flares*[Lens](../../...md#render_lens)* should be enabled.
**vec3_one** - default value
## vec4 LensColor

***Console*:**`render_lens_color`The color of HDR lens flares. To use this option, rendering of lens flares*[Lens](../../...md#render_lens)* should be enabled.
**vec4_one** - default value (white)
## float LensThreshold

***Console*:**`render_lens_threshold`The value of the brightness threshold for areas to produce lens flares. The *higher* the threshold value, *the brighter* the area should be to produce flares. To use this option, rendering of lens flares*[Lens](../../...md#render_lens)* should be enabled.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**.
## float LensRadius

***Console*:**`render_lens_radius`The radius of the spherical lens flares on the screen. **1.0f** corresponds to a screen-wide radius (a lens flare is not visible). To use this option, rendering of lens flares*[Lens](../../...md#render_lens)* should be enabled.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**.
## float LensLength

***Console*:**`render_lens_length`The length of the radial lens flare indicating if the whole radial lens flare is rendered on the screen or only a part of it. This option controls how lens flares pattern is distributed. To use this option, rendering of lens flares *[Lens](../../...md#render_lens)* should be enabled.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**.
## float LensScale

***Console*:**`render_lens_scale`The multiplier for color*[LensColor](../../...md#render_lens_color)* of HDR lens flares. To use this option, rendering of lens flares*[Lens](../../...md#render_lens)* should be enabled.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## bool Lens

***Console*:**`render_lens`The value indicating if lens flares are enabled. The default value is **false**.
## int ScreenSpaceShadowShaftsMode

***Console*:**`render_screen_space_shadow_shafts_mode`The rendering mode for volumetric [screen-space shadow shafts](../../../editor2/settings/render_settings/environment/index.md#ssss). Shadow shafts (aka light shafts) can be generated in screen space for the Sun and the Moon to simulate the real world effect of crepuscular rays, or atmospheric shadowing of atmospheric in-scattering. These rays add depth and realism to any scene.
> **Notice:** - This effect works for opaque geometry only.
> - It is recommended to use Screen-Space Shadow Shafts with relatively thick haze for visual consistency.
> - Disable this effect for indoor scenes as only world light sources are supported.

 One of the following values:
- **0** - Disabled
- **1** - Sun shadow shafts (by default)
- **2** - Moon shadow shafts
- **3** - Sun and Moon shadow shafts

## float ScreenSpaceShadowShaftsLength

***Console*:**`render_screen_space_shadow_shafts_length`The length of volumetric [screen-space shadow shafts](../../../editor2/settings/render_settings/environment/index.md#ssss).
Range of values: **[0.0f, 100.0f]**. The default value is : **3.0f**.
## int ScreenSpaceShadowShaftsQuality

***Console*:**`render_screen_space_shadow_shafts_quality`The [quality](../../../editor2/settings/render_settings/environment/index.md#ssss_quality) of screen-space shadow shafts. Defines the number of steps to be used when generating the texture for this effect. *Lower* quality values may result in noticeable banding effect especially in case of long shadow shafts. *Medium* quality is usually enough, but you can increase it if shafts are long enough and banding effect becomes noticeable. One of the following values:

- *Low* - low quality
- *Medium* - medium quality (by default)
- *High* - high quality
- *Ultra* - ultra quality

## int ScreenSpaceShadowShaftsResolution

***Console*:**`render_screen_space_shadow_shafts_resolution`The [resolution of the texture](../../../editor2/settings/render_settings/environment/index.md#ssss_resolution) to which screen-space shadows are rendered. One of the following values:

- *Quarter* - quarter resolution
- *Half* - half resolution (by default)
- *Full* - full resolution

## vec4 CrossColor

***Console*:**`render_cross_color`The [color](../../../editor2/settings/render_settings/camera_effects/index.md#cross_color) of the cross flares. To use this option, rendering of cross flares*[Cross](../../...md#render_cross)* should be enabled.
**vec4_one** - default value (white)
## float CrossThreshold

***Console*:**`render_cross_threshold`The brightness [threshold](../../../editor2/settings/render_settings/camera_effects/index.md#cross_threshold) for areas to produce flare. The *higher* the threshold value, the brighter the area should be to produce a flare. To use this option, rendering of cross flares*[Cross](../../...md#render_cross)* should be enabled.
Range of values: **[0.0f, inf]**. The default value is : **0.0f**.
## float CrossAngle

***Console*:**`render_cross_angle`The cross flares orientation [angle](../../../editor2/settings/render_settings/camera_effects/index.md#cross_angle). To use this option, rendering of cross flares*[Cross](../../...md#render_cross)* should be enabled.
Range of values: **[-inf, inf]**. The default value is : **45.0f**.
## float CrossScale

***Console*:**`render_cross_scale`The color multiplier.[cross color scale](../../../editor2/settings/render_settings/camera_effects/index.md#cross_scale) - a multiplier for the [color](#setCrossColor_vec4_void) of cross flares. *Higher* values produce *more pronounced* flares. To use this option, rendering of cross flares*[Cross](../../...md#render_cross)* should be enabled.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float CrossLength

***Console*:**`render_cross_length`The [length](../../../editor2/settings/render_settings/camera_effects/index.md#cross_length) of a cross flare relative to the screen width. *Increasing* this value also leads to fading of the shafts across their length. To use this option, rendering of cross flares*[Cross](../../...md#render_cross)* should be enabled.
Range of values: **[0.0f, 2.0f]**. The default value is : **0.2f**.
## int CrossShafts

***Console*:**`render_cross_shafts`The number of [shafts](../../../editor2/settings/render_settings/camera_effects/index.md#cross_shafts) in a cross flare. High number of flares can cause a FPS drop on low-performance hardware. To use this option, rendering of cross flares*[Cross](../../...md#render_cross)* should be enabled.
Range of values: **[2, 32]**. The default value is : **4**.
## bool Cross

***Console*:**`render_cross`The value indicating if [cross flares](../../../editor2/settings/render_settings/camera_effects/index.md#cross) are enabled. The default value is **false**.
## float FilmicSaturationRecovery

***Console*:**`render_filmic_saturation_recovery`The [color saturation recovery](../../../editor2/settings/render_settings/color/index.md#saturation_recovery) value for the filmic tonemapper. Filmic tonemapper desaturates image colors in bright areas making them look grayish. This parameter enables you to recover initial color saturation in such areas. Higher values make colors more saturated:
- 0.0f - standard filmic tonemapping, no saturation recovery is performed.
- 1.0f - color saturation is recovered to the full extent.


> **Notice:** When the 1.0f value is set specular highlights appear too saturated, so the recommended value is 0.75f (default)


Range of values: **[0.0f, 1.0f]**. The default value is : **0.75f**.
## float FilmicWhiteLevel

***Console*:**`render_filmic_white_level`The [Linear White Point](../../../editor2/settings/render_settings/color/index.md#white_level) tonemapping parameter value, which is mapped as pure white in the resulting image.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float FilmicToeDenominator

***Console*:**`render_filmic_toe_denominator`The [Toe Denominator](../../../editor2/settings/render_settings/color/index.md#toe_denominator) tonemapping parameter value.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**.
## float FilmicToeNumerator

***Console*:**`render_filmic_toe_numerator`The [Toe Numerator](../../../editor2/settings/render_settings/color/index.md#toe_numerator) tonemapping parameter value.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.01f**.
## float FilmicToeScale

***Console*:**`render_filmic_toe_scale`The [Toe Scale](../../../editor2/settings/render_settings/color/index.md#toe_scale) tonemapping parameter value that is used to change dark values. The Toe Scale controls the slope of the tone mapping curve toe (the area of underexposure).
Range of values: **[0.0f, 1.0f]**. The default value is : **0.2f**.
## float FilmicLinearAngle

***Console*:**`render_filmic_linear_angle`The [Linear Angle](../../../editor2/settings/render_settings/color/index.md#linear_angle) tone mapping parameter value. This parameter controls the slope of the linear part of the [tone mapping curve](../../../editor2/settings/render_settings/color/index.md#tonemapping_curve).
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
## float FilmicLinearScale

***Console*:**`render_filmic_linear_scale`The [Linear Strength](../../../editor2/settings/render_settings/color/index.md#linear_scale) tone mapping parameter value that is used to change gray values. The Linear Scale controls the length of the [tone mapping curve](../../../editor2/settings/render_settings/color/index.md#tonemapping_curve) linear part.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**.
## float FilmicShoulderScale

***Console*:**`render_filmic_shoulder_scale`The [Shoulder Strength](../../../editor2/settings/render_settings/color/index.md#shoulder_scale) tonemapping parameter value that is used to change bright values.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.2f**.
## float BloomPower

***Console*:**`render_bloom_power`The power of the Bloom effect.
- 0.0f (min) - the Bloom effect is blurred.
- 1.0f (max) - the Bloom effect is more contrast.


Range of values: **[0.0f, 1.0f]**. The default value is : **0.7f**.
## float BloomScale

***Console*:**`render_bloom_scale`The scale of the Bloom effect.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**.
## int BloomPasses

***Console*:**`render_bloom_passes`The number of passes for the bloom effect. During the pass a Bloom texture is generating. Up to 8 Bloom textures can be generated: each texture has lower resolution (original size, original size /2, original size /4, so forth) with Bloom effect. After that, all these Bloom textures with the different resolution form the final Bloom texture.
> **Notice:** The higher the value, the smoother the effect is. However, this option significantly affects performance.

Range of values: **[2, 8]**. The default value is : **6**.
## int BloomResolution

***Console*:**`render_bloom_resolution`The resolution of the Bloom effect. One of the following values:
- **0** - quarter
- **1** - half
- **2** - full (by default)

## bool Bloom

***Console*:**`render_bloom`The value indicating if the Bloom effect is enabled. The default value is **false**.
## float DOFNearFocalOffset

***Console*:**`render_dof_near_focal_offset`The [offset](../../../editor2/settings/render_settings/camera_effects/index.md#near_focal_offset) from the focal to the nearest blurred zone. In other words, the distance when foreground (near) is in focus.
Range of values: **[0.0f, inf]**. The default value is : **0.0f**.
## float DOFNearDistance

***Console*:**`render_dof_near_distance`The [near DOF limit](../../../editor2/settings/render_settings/camera_effects/index.md#near_distance) of the camera: the distance between the camera and the first element that is considered to be acceptably sharp. Black zone on the DOF mask means in-focus zone.
Range of values: **[0.0f, inf]**. The default value is : **10.0f**.
## float DOFFarFocalOffset

***Console*:**`render_dof_far_focal_offset`The Sets the [offset](../../../editor2/settings/render_settings/camera_effects/index.md#far_focal_offset) from the focal to the farthest blurred zone for the DOF effect. In other words, the distance when background (far) is in focus.
Range of values: **[0.0f, inf]**. The default value is : **0.0f**.
## float DOFFarDistance

***Console*:**`render_dof_far_distance`The [far DOF limit](../../../editor2/settings/render_settings/camera_effects/index.md#far_distance) of the camera: the distance between the camera and the furthest element that is considered to be acceptably sharp. Black zone on the DOF mask means in-focus zone.
Range of values: **[0.0f, inf]**. The default value is : **10.0f**.
## float DOFBlur

***Console*:**`render_dof_blur`The intensity of [blur](../../../editor2/settings/render_settings/camera_effects/index.md#blur) for the DOF (Depth Of Field) effect.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float DOFChromaticAberration

***Console*:**`render_dof_chromatic_aberration`The intensity of [chromatic aberration](../../../editor2/settings/render_settings/camera_effects/index.md#chromatic_aberration) for the DOF (Depth Of Field) effect.
Range of values: **[0.0f, inf]**. The default value is : **0.0f**.
## float DOFFocalDistance

***Console*:**`render_dof_focal_distance`The [focal distance](../../../editor2/settings/render_settings/camera_effects/index.md#focal_distance) of the camera, i.e. a point where objects are in-focus and visible clearly.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## int DOFBokehMode

***Console*:**`render_dof_bokeh_mode`The shape of the [Bokeh](../../../editor2/settings/render_settings/camera_effects/index.md#bokeh_shape) for the DOF effect. This parameter determines the way the lens renders out-of-focus points of light.
> **Notice:** For the DOF effect, the Bokeh effect is enabled by default.

 One of the following values:
- **0** - ring (by default)
- **1** - circle

## int DOFResolution

***Console*:**`render_dof_resolution`The [resolution](../../../editor2/settings/render_settings/camera_effects/index.md#resolution) of the DOF (Depth Of Field) effect. One of the following values:
- **0** - quarter
- **1** - half
- **2** - full (by default)

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DOFPreset](/api/library/rendering/class.render_cs#render_dof_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int DOFQuality

***Console*:**`render_dof_quality`The [quality](../../../editor2/settings/render_settings/camera_effects/index.md#quality) of the DOF (Depth Of Field) effect. One of the following values:

- *Low* - low quality
- *Medium* - medium quality (by default)
- *High* - high quality
- *Ultra* - ultra quality

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DOFPreset](/api/library/rendering/class.render_cs#render_dof_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool DOFFocusImprovement

***Console*:**`render_dof_focus_improvement`The value indicating if the [focus improvement](../../../editor2/settings/render_settings/camera_effects/index.md#focus_improvement) option is enabled for the DOF (Depth Of Field) effect. When enabled, transitions between the focused and unfocused parts of the scene become more accurate. The default value is **false**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DOFPreset](/api/library/rendering/class.render_cs#render_dof_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool DOFIncreasedAccuracy

***Console*:**`render_dof_increased_accuracy`The value indicating if the [increased accuracy](../../../editor2/settings/render_settings/camera_effects/index.md#increased_accuracy) option is enabled for the DOF (Depth Of Field) effect. When enabled, focusing calculation is performed with increased accuracy. The default value is **false**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DOFPreset](/api/library/rendering/class.render_cs#render_dof_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool DOF

***Console*:**`render_dof`The value indicating if the [DOF](../../../editor2/settings/render_settings/camera_effects/index.md) (Depth Of Field) effect is enabled. The default value is **false**.
## int MotionBlurNumSteps

***Console*:**`render_motion_blur_num_steps`The number of steps used in the [motion blur](../../../principles/render/sequence/index.md#motion_blur). The higher the value, the more correct the motion blur effect is. At low values, moving objects may look doubled, however, performance will increase. To use this option, rendering of the motion blur effect*[MotionBlur](../../...md#render_motion_blur)* should be enabled.
Range of values: **[2, 64]**. The default value is : **8**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[MotionBlurPreset](/api/library/rendering/class.render_cs#render_motion_blur_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float MotionBlurNoiseIntensity

***Console*:**`render_motion_blur_noise_intensity`The intensity of the noise used in the [motion blur](../../../principles/render/sequence/index.md#motion_blur). To use this option, rendering of the motion blur effect*[MotionBlur](../../...md#render_motion_blur)* should be enabled.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[MotionBlurPreset](/api/library/rendering/class.render_cs#render_motion_blur_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float MotionBlurMaxVelocity

***Console*:**`render_motion_blur_max_velocity`The [maximum possible amount](../../../editor2/settings/render_settings/camera_effects/index.md#max_velocity) of [motion blur](../../../principles/render/sequence/index.md#motion_blur) for moving physical objects. When their body velocity exceeds the set value, they will be blurred as if they have the maximum velocity set by the parameter.
This parameter should be used:


- To avoid excessive blurring of fast moving objects.
- To save performance, as increasing the object's velocity leads increasing the radius of the motion blur effect that drops performance at too high values.

 To use this option, rendering of the motion blur effect*[MotionBlur](../../...md#render_motion_blur)* should be enabled.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[MotionBlurPreset](/api/library/rendering/class.render_cs#render_motion_blur_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float MotionBlurVelocityScale

***Console*:**`render_motion_blur_velocity_scale`The [scale value](../../../editor2/settings/render_settings/camera_effects/index.md#velocity) of bodies' linear and angular velocities used for the motion blur. The *higher* the value, the more blurred the objects will appear when moving. To use this option, rendering of the motion blur effect*[MotionBlur](../../...md#render_motion_blur)* should be enabled.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[MotionBlurPreset](/api/library/rendering/class.render_cs#render_motion_blur_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool MotionBlurCameraVelocity

***Console*:**`render_motion_blur_camera_velocity`The value indicating if camera velocity contributes to the [motion blur](../../../principles/render/sequence/index.md#motion_blur) effect (false to take into account velocities of objects only). To use this option, rendering of the motion blur effect*[MotionBlur](../../...md#render_motion_blur)* should be enabled.
> **Notice:** Disabled in VR mode by default.

 The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[MotionBlurPreset](/api/library/rendering/class.render_cs#render_motion_blur_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float MotionBlurDepthThresholdFar

***Console*:**`render_motion_blur_depth_threshold_far`The value defining if the blur effect is applied to the background object. If the distance between the foreground object and the background object is less than this threshold value, the motion blur effect won't be applied to the background object. To use this option, rendering of the motion blur effect*[MotionBlur](../../...md#render_motion_blur)* should be enabled.
> **Notice:** Disabled in VR mode by default.

Range of values: **[0.0f, inf]**. The default value is : **0.5f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[MotionBlurPreset](/api/library/rendering/class.render_cs#render_motion_blur_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float MotionBlurDepthThresholdNear

***Console*:**`render_motion_blur_depth_threshold_near`The value defining if the blur effect is applied to the foreground object. If the distance between the foreground object and the background object is less than this threshold value, the motion blur effect won't be applied to the foreground object. To use this option, rendering of the motion blur effect*[MotionBlur](../../...md#render_motion_blur)* should be enabled.
> **Notice:** Disabled in VR mode by default.

Range of values: **[0.0f, inf]**. The default value is : **0.2f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[MotionBlurPreset](/api/library/rendering/class.render_cs#render_motion_blur_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float MotionBlurVelocityBlurRadius

***Console*:**`render_motion_blur_velocity_blur_radius`The radius of the [motion blur](../../../principles/render/sequence/index.md#motion_blur) effect for the boundary between moving and static objects.
Range of values: **[0.0f, inf]**. The default value is : **0.5f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[MotionBlurPreset](/api/library/rendering/class.render_cs#render_motion_blur_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int MotionBlurVelocityBlurSamples

***Console*:**`render_motion_blur_velocity_blur_samples`The number of iterations performed to blur the border between moving and static objects. Higher values ensure a higher quality of blurring, but affect the performance. To use this option, rendering of the motion blur effect*[MotionBlur](../../...md#render_motion_blur)* should be enabled.
> **Notice:** Disabled in VR mode by default.

Range of values: **[0, 512]**. The default value is : **32**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[MotionBlurPreset](/api/library/rendering/class.render_cs#render_motion_blur_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool MotionBlur

***Console*:**`render_motion_blur`The value indicating if the motion blur effect is enabled. The default value is **true**.
## float WhiteBalanceAdaptationTime

***Console*:**`render_white_balance_adaptation_time`The time period set for the camera to adjust white balance. During this time white balance correction is performed (0.0f - instant correction is to be used).
> **Notice:** It is recommended to use lower values, when possible, to make correction process unnoticeable, otherwise it'll be slow and will catch user's eye. However, setting too low values may result in abrupt switching of colors as the camera moves. So, adjust this parameter carefully to make transition smoooth. You can set it equal to the Exposure Adaptation value*[ExposureAdaptation](../../...md#render_exposure_adaptation)*.


Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float WhiteBalanceIntensity

***Console*:**`render_white_balance_intensity`The value of [white balance correction intensity](../../../editor2/settings/render_settings/camera_effects/index.md#white_balance_intensity).
- 0.0f - no white balance correction is performed.
- *higher* values result in stronger correction.


> **Notice:** Do not set too high values for night-time and dimly lit scenes, as it may lead to heavy color distortion making the scene look totally unnatural.


Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**.
## bool WhiteBalance

***Console*:**`render_white_balance`The value indicating if [automatic white balance correction](../../../editor2/settings/render_settings/camera_effects/index.md#white_balance) is enabled. The default value is **true**.
## float ExposureMaxLuminance

***Console*:**`render_exposure_max_luminance`The [maximum luminance](../../../editor2/settings/render_settings/camera_effects/index.md#max_luminance) offset relative to the default luminance of the scene used for rendering of adaptive exposure effect: the *lower* the value, the brighter the adapted image will be. The parameter can take on negative values.
> **Notice:** If the specified value is less than the current minimum luminance, the minimum luminance value will be changed to the specified maximum luminance so that they are equal.


Range of values: **[-10.0f, 10.0f]**. The default value is : **10.0f**.
## float ExposureMinLuminance

***Console*:**`render_exposure_min_luminance`The [minimum luminance](../../../editor2/settings/render_settings/camera_effects/index.md#min_luminance) offset relative to the default luminance of the scene used for rendering of adaptive exposure effect: the *higher* the value, the darker the adapted image will be. The parameter can take on negative values.
> **Notice:** If the specified value is greater than the current maximum luminance, the maximum luminance value will be changed to the specified minimum luminance so that they are equal.


Range of values: **[-10.0f, 10.0f]**. The default value is : **-5.0f**.
## float ExposureAdaptation

***Console*:**`render_exposure_adaptation`The time for the camera to adjust exposure, in seconds. 0.0f - means instant adaptation. If a too small or even negative value is provided, **1E-6** will be used instead.
Range of values: **[eps, inf]**. The default value is : **1.0f**.
## float Exposure

***Console*:**`render_exposure`The camera [exposure](../../../editor2/settings/render_settings/camera_effects/index.md#exposure) (a multiplier of the scene luminance and brightness).
It determines the resulting amount of luminance:


- By the minimum value of 0.0f, the image is rendered black.
- The *higher* the value, the more luminance and the brighter the scene lit.

 Available only when the Camera Mode*[CameraMode](../../...md#render_camera_mode)* is set to Classic.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## int ExposureMode

***Console*:**`render_exposure_mode`The [mode of the adaptive exposure effect](../../../editor2/settings/render_settings/camera_effects/index.md#mode).
- **Static** - a static exposure. The amount of luminance is determined by the Exposure*[Exposure](../../...md#render_exposure)* depending on the Camera Mode*[CameraMode](../../...md#render_camera_mode)* parameter.
- **Logarithmic** - adaptive logarithmic mapping technique.
- **Quadratic** - adaptive quadratic mapping technique.
- **Curve based** - adaptive curve based mapping technique.

  One of the following values:
- **0** - static (by default)
- **1** - logarithmic adaptive exposure
- **2** - quadratic adaptive exposure

## bool MeteringMaskEnabled

***Console*:**`render_metering_mask_enabled`The value indicating if metering mask for exposure and white balance correction is enabled. This option gives you an additional texture slot*[MeteringMaskTexture](../../...md#MeteringMaskTexture)* to control the effect of auto exposure and white balance correction on the whole screen, where each pixel is weighted in importance in accordance with the specified texture mask. The default value is **false**.
## 🔒︎ Texture MeteringMaskTexture

The Metering Mask texture used to control the influence of auto exposure and white balance correction for the whole screen, where each pixel is weighted in importance in accordance with the specified texture mask. Giving importance to pixels toward the center of the screen rather than along the edges helps stabilize auto exposure.
## string MeteringMaskTexturePath

The path to the Metering Mask texture to be used to control the influence of auto exposure and white balance correction for the whole screen, where each pixel is weighted in importance in accordance with the specified texture mask. After setting the path the texture is loaded automatically.
## Render.SHOW_LIGHTING_MODE ShowLightingMode

***Console*:**`render_show_lighting_mode`The visualization of surfaces with the selected lighting mode. One of the following values:
- **0** - disabled (by default)
- **1** - render objects using static lighting mode
- **2** - render objects using dynamic lighting mode
- **3** - render objects using advanced lighting mode

## bool CloudsPanoramaReuse

***Console*:**`render_clouds_panorama_reuse`The value indicating if the panorama cubemap texture is reused between several viewports. Available for *Render To Panorama* [clouds mode](#render_clouds_mode). The default value is **false**.
## int CloudsPanoramaResolution

***Console*:**`render_clouds_panorama_resolution`The resolution of the panorama cubemap texture. Available for *Render To Panorama* [clouds mode](#render_clouds_mode). One of the following values:
- **0** - 128x128
- **1** - 256x256
- **2** - 384x384
- **3** - 512x512
- **4** - 768x768 (by default)
- **5** - 1024x1024
- **6** - 1536x1536
- **7** - 2048x2048
- **8** - 4096x4096

## int CloudsMode

***Console*:**`render_clouds_mode`The clouds rendering mode. Rendering clouds into the panorama cubemap texture once per frame automatically makes the clouds seen in simple default environment-based reflections making them look more natural for a reduced cost. However, rendering views from inside the clouds is possible in *Volumetric* mode only. One of the following values:
- **0** - *Volumetric* - render volumetric clouds (by default)
- **1** - *Render To Panorama* - render clouds to panorama (environment cubemap)

## bool CloudsEnvironmentSky

***Console*:**`render_clouds_environment_sky`The value indicating whether the custom environment cubemap texture is automatically adjusted to match the current sky lighting. When enabled, the original sky color baked into the texture (specified via [CloudsEnvironmentSkyColor](#CloudsEnvironmentSkyColor)) is replaced with the actual sky color based on the current sun position. Only applies in Panorama clouds rendering mode. The default value is **true**.
## vec4 CloudsEnvironmentSkyColor

***Console*:**`render_clouds_environment_sky_color`The reference sky color that was baked into the custom environment cubemap texture. Used to remove the original sky lighting before applying the current sky color when [CloudsEnvironmentSky](#CloudsEnvironmentSky) is enabled. Only applies in Panorama clouds rendering mode.
**vec4(1.0f, 1.0f, 1.0f, 1.0f)** - default value (white)
## vec4 CloudsEnvironmentColor

***Console*:**`render_clouds_environment_color`The color multiplier for the custom environment cubemap texture specified via [CloudsEnvironmentTexturePath](#CloudsEnvironmentTexturePath). Only applies in Panorama clouds rendering mode.
**vec4(1.0f, 1.0f, 1.0f, 1.0f)** - default value (white)
## string CloudsEnvironmentTexturePath

The path to a custom cubemap texture that is blended into the environment cubemap when rendering clouds in Panorama mode. The resulting cubemap is used for sky reflections across the scene. If empty, no custom environment texture is applied.
## bool ShadowsSimplified

***Console*:**`render_shadows_simplified`The value indicating if the [static shadows](../../../code/materials_shaders/abstract_materials/mesh.md#static_shadow) are enabled for all materials in the scene. The default value is **false**.
## bool ShadowsReuse

***Console*:**`render_shadows_reuse`The value indicating if the shadow maps of the main viewport are reused for other viewports. Shadow maps are normally rendered separately for each viewport when multiple viewports render the scene. It is important as each camera that renders into the viewport has its unique transformation. However, in cases when cameras are close to each other, shadows appear very similar, so for certain viewport and camera configurations you can save resources by enabling this mode - the shadow maps will be rendered only for the main viewport and then used for the others. The default value is **false**.
## float DenoiseDenoiseMaskBias

***Console*:**`render_denoise_denoise_mask_bias`The threshold value for the brightness delta between frames below which the denoise mask becomes black. Denoise mask is based on the difference in brightness between the previous frame and the current one. Sometimes this difference is very small and can be neglected. This bias value is the threshold difference below which the denoise mask will be plain black. Since a zero value may cause a slight blur effect on the global illumination, this bias was added to avoid such effect.
Range of values: **[0.0f, inf]**. The default value is : **0.001f**.
## float DenoiseDenoiseMaskDenoiseThreshold

***Console*:**`render_denoise_denoise_mask_denoise_threshold`The threshold for the pixel brightness delta value of neighboring pixels, which defines if the pixels may be blurred together.
Range of values: **[0.0f, inf]**. The default value is : **0.05f**.
## float DenoiseDenoiseMaskFrameCount

***Console*:**`render_denoise_denoise_mask_frame_count`The number of frames stored to generate the denoise mask.
Range of values: **[0.0f, inf]**. The default value is : **15.0f**.
## float DenoiseDenoiseMaskInformationLostBoost

***Console*:**`render_denoise_denoise_mask_information_lost_boost`The value controlling the intensity of filling in the information lost areas with the white color and temporally accumulating the result between frames. This parameter reduces the effect of flickering pixels, but may add a ghosting effect.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**.
## float DenoiseDenoiseMaskVelocityThreshold

***Console*:**`render_denoise_denoise_mask_velocity_threshold`The threshold for the velocity intensity value at which the denoise mask becomes white. This parameter is used to remove ghosting and flickering pixels when the camera moves quickly.
Range of values: **[0.0f, inf]**. The default value is : **0.0f**.
## float DenoiseColorClampingBlurIntensityAO

***Console*:**`render_denoise_color_clamping_blur_intensity_ao`The intensity of using the blurred version of the current frame for color clamping in the areas where the Ambient Occlusion mask is black.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.1f**.
## float DenoiseColorClampingBlurIntensity

***Console*:**`render_denoise_color_clamping_blur_intensity`The intensity of using the blurred version of the current frame for color clamping.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.9f**.
## float DenoiseColorClampingBlurRadius

***Console*:**`render_denoise_color_clamping_blur_radius`The blur radius for the current frame. The blurred image is further used in color clamping. This setting helps reducing noise in dark indoor areas.
Range of values: **[0.0f, 64.0f]**. The default value is : **8.0f**.
## float DenoiseHotPixelsFixIntensity

***Console*:**`render_denoise_hot_pixels_fix_intensity`The value reducing the intensity of flickering pixels in the screen space. Adjusting this value may cause darkening of the global illumination.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**.
## float DenoiseInformationLostFixFlicker

***Console*:**`render_denoise_information_lost_fix_flicker`The value reducing the intensity of flickering pixels in the information lost areas. An excessive value may cause darkening of the areas behind objects when the camera is moving or when objects are moving in space.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.75f**.
## float DenoiseAOMaskRadius

***Console*:**`render_denoise_ao_mask_radius`The radius of the Ambient Occlusion Mask (the Distance buffer) that is used to additionally configure the Denoiser parameters. This parameter affects only the *Environment Probes* with the [Raymarching mode](../../../objects/lights/envprobe/index.md#box_projection) enabled.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float DenoiseInformationLostDepthThreshold

***Console*:**`render_denoise_information_lost_depth_threshold`The value defining starting from which depth the noise reduction effect is applied to the data in the "information lost" areas. This setting is aimed at reducing noise in areas where the ghosting effect commonly occurs.
Range of values: **[0.0f, inf]**. The default value is : **0.1f**.
## bool DenoiseInterleaved

***Console*:**`render_denoise_interleaved`The interleaved rendering for the Denoiser. The default value is **false**.
## bool IndirectSpecularNormalization

***Console*:**`render_indirect_specular_normalization`The  adjustment of indirect reflection color and brightness to match the indirect diffuse lighting. When this option is enabled, all indirect specular reflections will attempt to match the brightness and color of the indirect diffuse lighting. This affects both matte and glossy reflections.
**Example:** if there is dark indirect diffuse lighting under a table (set by a lightmap, voxel probe, or in another way), then the indirect specular reflection in that area will also appear dark.


This effect is physically inaccurate and implemented using a fake approach, so it should be used with caution. In some scenes, it may improve the visual quality, while in others, it may worsen it. Enable the option to observe whether it improves the result or not.


This feature is commonly used in many games, especially on consoles, because it's a performance-friendly way to eliminate overly bright reflections in dark areas of the scene.

  The default value is **false**.
## float IndirectSpecularDenoiseThresholdAO

***Console*:**`render_indirect_specular_denoise_threshold_ao`The threshold noise reduction value for the indirect specular lighting in the areas where the Ambient Occlusion mask is black.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.1f**.
## float IndirectSpecularTemporalFilteringFramesClampingVelocityThreshold

***Console*:**`render_indirect_specular_temporal_filtering_frames_clamping_velocity_threshold`The threshold velocity value exceeding which the number of accumulated frames will be equal to Frame Count Min *[IndirectSpecularTemporalFilteringFrameCountMin](../../...md#render_indirect_specular_temporal_filtering_frame_count_min)*.
Range of values: **[0.0f, inf]**. The default value is : **10.0f**.
## float IndirectSpecularTemporalFilteringColorClampingIntensityAO

***Console*:**`render_indirect_specular_temporal_filtering_color_clamping_intensity_ao`The intensity of temporal filtering color clamping at zero pixel velocity for Indirect Specular in the areas where the Ambient Occlusion mask is black (the Distance buffer).
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
## float IndirectSpecularTemporalFilteringFrameCountMin

***Console*:**`render_indirect_specular_temporal_filtering_frame_count_min`The number of accumulated frames in the information lost areas and if the Frames Clamping Velocity value *[IndirectSpecularTemporalFilteringFramesClampingVelocityThreshold](../../...md#render_indirect_specular_temporal_filtering_frames_clamping_velocity_threshold)* is exceeded.
Range of values: **[0.0f, inf]**. The default value is : **50.0f**.
## float IndirectDiffuseDenoiseThresholdAO

***Console*:**`render_indirect_diffuse_denoise_threshold_ao`The threshold of the noise reduction value for the indirect diffuse lighting in the areas where the Ambient Occlusion mask is black.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.1f**.
## float IndirectDiffuseTemporalFilteringFramesClampingVelocityThreshold

***Console*:**`render_indirect_diffuse_temporal_filtering_frames_clamping_velocity_threshold`The threshold velocity value exceeding which the number of accumulated frames will be equal to Frame Count Min *[IndirectDiffuseTemporalFilteringFrameCountMin](../../...md#render_indirect_diffuse_temporal_filtering_frame_count_min)*.
Range of values: **[0.0f, inf]**. The default value is : **10.0f**.
## float IndirectDiffuseTemporalFilteringColorClampingIntensityAO

***Console*:**`render_indirect_diffuse_temporal_filtering_color_clamping_intensity_ao`The intensity of temporal filtering color clamping at zero pixel velocity for Indirect Diffuse in the areas where the Ambient Occlusion mask is black (the Distance buffer).
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
## float IndirectDiffuseTemporalFilteringFrameCountMin

***Console*:**`render_indirect_diffuse_temporal_filtering_frame_count_min`The number of accumulated frames in the information lost areas and if the Frames Clamping Velocity value *[IndirectDiffuseTemporalFilteringFramesClampingVelocityThreshold](../../...md#render_indirect_diffuse_temporal_filtering_frames_clamping_velocity_threshold)* is exceeded.
Range of values: **[0.0f, inf]**. The default value is : **50.0f**.
## Render.SHADERS_COMPILE_MODE ShadersCompileMode

***Console*:**`render_shaders_compile_mode`The compilation mode for shaders that are used in the loaded world. The following modes are available:
- *Async* - shaders are compiled in a background thread. Objects whose shaders are not yet ready are not rendered (pop-in effect).
- *Force* - shaders are compiled synchronously on the main thread. The application freezes until the shader is ready, but objects are rendered immediately.


> **Notice:** This setting does not affect post-processing shaders, lightmap data shaders, and materials with forced compilation - these are always compiled synchronously regardless of this setting.

  One of the following values:
- **0** - Asynchronous compilation. Objects whose shaders are not yet ready are not rendered (pop-in). (by default)
- **1** - Forced synchronous compilation. The application freezes until the shader is ready.

## 🔒︎ int NumLoadedShaders

The number of shaders loaded to RAM.
## 🔒︎ int NumCompiledShaders

The number of shaders that are currently compiled.
## 🔒︎ int NumLoadedPSO

The number of loaded PSOs.
## 🔒︎ int NumCompiledPSO

The number of PSOs that are currently compiled.
## float FStop

***Console*:**`render_f_stop`The f-stop value used for static exposure calculation. This setting is available for the physically-based camera*[CameraMode](../../...md#render_camera_mode)* and represents the ratio of the focal length (f) and the diameter of the lens opening (D): **f / D**. It is the reciprocal of the relative aperture. The *higher* the value, the darker the image is.
Range of values: **[0, inf]**. The default value is : **11**.
## float ShutterSpeed

***Console*:**`render_shutter_speed`The shutter speed used for static exposure calculation. This setting is available for the physically-based camera*[CameraMode](../../...md#render_camera_mode)* and indicates how long the sensor of the camera is actively collecting light. *Higher* values make the shutter speed faster and the image - darker.
Range of values: **[0, inf]**. The default value is : **250**.
## float ISO

***Console*:**`render_iso`The ISO value used for static exposure calculation. This value is available for the physically-based camera*[CameraMode](../../...md#render_camera_mode)* and represents the sensitivity of the camera sensor. The *higher* the ISO number, the more light is collected and the brighter the image is.
Range of values: **[0, inf]**. The default value is : **100**.
## int CameraMode

***Console*:**`render_camera_mode`The camera mode, which determines the way the exposure is set. Either of the following:
- **Physically-Based** - the real-world values are used to set up lighting and camera exposure: ISO*[ISO](../../...md#render_iso)*, shutter speed*[ShutterSpeed](../../...md#render_shutter_speed)*, F-stop*[FStop](../../...md#render_f_stop)*. With the default values of these parameters, the static exposure value is near 1. > **Notice:** For the physically-based mode, the exposure mode*[ExposureMode](../../...md#render_exposure_mode)* should be set to *Static* to avoid exposure issues.
- **Classic** - the exposure is set by the Exposure value*[Exposure](../../...md#render_exposure)*.

  One of the following values:
- **0** - classic (by default)
- **1** - physically-based

## string DirtTextureName

The name of the texture that modulates the pattern of lens flares. For example, it can be used to create an effect of light reflections or unclean optics when the camera looks at the sun.
## float DirtScale

***Console*:**`render_dirt_scale`The intensity of lens dirt effect modulating the pattern of lens flares defined by the [Dirt Texture](../../../editor2/settings/render_settings/camera_effects/index.md#lens_dirt). For example, it can be used to create an effect of unclean optics when the camera looks at the sun.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**.
## bool CameraEffectsTemporalFiltering

***Console*:**`render_camera_effects_temporal_filtering`The value indicating if temporal filtering for camera effects is enabled. Temporal filtering reduces flickering of the bloom effect on the small bright objects (such flickering may appear when the camera moves). For example, it can be used in scenes with industrial pipes. The default value is **false**.
## float CameraEffectsTemporalFilteringColorClampingIntensity

***Console*:**`render_camera_effects_temporal_filtering_color_clamping_intensity`The intensity of TAA color clamping for the Bloom effect. *Lower* values result in more accumulated frames combined, which reduces noise flickering, but increases ghosting effect. To reduce ghosting in this case you can use Min Velocity Clamping*[CameraEffectsTemporalFilteringMinVelocityClamping](../../...md#render_camera_effects_temporal_filtering_min_velocity_clamping)* and Max Velocity Clamping*[CameraEffectsTemporalFilteringMaxVelocityClamping](../../...md#render_camera_effects_temporal_filtering_max_velocity_clamping)*, while *higher* values reduce ghosting effect, but increase flickering.
> **Notice:** This option is available only when the temporal filtering*[CameraEffectsTemporalFiltering](../../...md#render_camera_effects_temporal_filtering)* is enabled.


Range of values: **[1.0f, inf]**. The default value is : **3.0f**.
## float CameraEffectsTemporalFilteringMinVelocityClamping

***Console*:**`render_camera_effects_temporal_filtering_min_velocity_clamping`The sensitivity of TAA color clamping for the Bloom effect for static objects. This parameter is used to reduce ghosting effect for lower Color Clamping Intensity*[CameraEffectsTemporalFilteringColorClampingIntensity](../../...md#render_camera_effects_temporal_filtering_color_clamping_intensity)* values: higher values reduce ghosting, but at the same time reduce the temporal filter effect.
> **Notice:** This option is available only when the temporal filtering*[CameraEffectsTemporalFiltering](../../...md#render_camera_effects_temporal_filtering)* is enabled.


Range of values: **[0.0f, 1.0f]**. The default value is : **0.05f**.
## float CameraEffectsTemporalFilteringMaxVelocityClamping

***Console*:**`render_camera_effects_temporal_filtering_max_velocity_clamping`The sensitivity of TAA color clamping for the Bloom effect for moving objects. This parameter is used to reduce ghosting effect for lower Color Clamping Intensity*[CameraEffectsTemporalFilteringColorClampingIntensity](../../...md#render_camera_effects_temporal_filtering_color_clamping_intensity)* values: higher values reduce ghosting, but at the same time reduce the temporal filter effect.
> **Notice:** This option is available only when the temporal filtering*[CameraEffectsTemporalFiltering](../../...md#render_camera_effects_temporal_filtering)* is enabled.


Range of values: **[0.0f, 1.0f]**. The default value is : **0.1f**.
## float CameraEffectsThreshold

***Console*:**`render_camera_effects_threshold`The brightness threshold, which is used to detect if an object should be blurred in the HDR mode. By the minimum value of 0, the bright areas can become overexposed.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## vec4 TranslucentColor

***Console*:**`render_translucent_color`The color used for translucent objects globally. When light shines on one side of the object, the other side is partially illuminated with this color.
**vec4(1.0f, 1.0f, 1.0f, 1.0f)** - default value (white)
## bool IndirectDiffuseTemporalFilteringEnabled

***Console*:**`render_indirect_diffuse_temporal_filtering_enabled`The value indicating if temporal filtering for Indirect Diffuse is enabled. Temporal filtering reduces flickering of indirect diffuse light. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DenoisePreset](/api/library/rendering/class.render_cs#render_denoise_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float IndirectDiffuseTemporalFilteringFrameCount

***Console*:**`render_indirect_diffuse_temporal_filtering_frame_count`The [frame count](../../../principles/render/antialiasing/taa.md#taa_frame_count) of temporal filtering for the indirect diffuse effect. Specifies the number of frames for the velocity buffer. The higher the value, the more frames are combined into the final image and the better anti-aliasing.
Range of values: **[0.0f, inf]**. The default value is : **50.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DenoisePreset](/api/library/rendering/class.render_cs#render_denoise_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float IndirectDiffuseTemporalFilteringColorClampingIntensity

***Console*:**`render_indirect_diffuse_temporal_filtering_color_clamping_intensity`The intensity of temporal filtering color clamping at zero pixel velocity for Indirect Diffuse. *Lower* values result in more accumulated frames combined, which reduces noise flickering, but increases ghosting effect. To reduce ghosting in this case you can use Indirect Diffuse Color Clamping Velocity Threshold*[IndirectDiffuseTemporalFilteringColorClampingVelocityThreshold](../../...md#render_indirect_diffuse_temporal_filtering_color_clamping_velocity_threshold)*, while *higher* values reduce ghosting effect, but increase flickering.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DenoisePreset](/api/library/rendering/class.render_cs#render_denoise_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float IndirectDiffuseTemporalFilteringColorClampingVelocityThreshold

***Console*:**`render_indirect_diffuse_temporal_filtering_color_clamping_velocity_threshold`The sensitivity of temporal filtering color clamping for Indirect Diffuse to pixel velocity change. This parameter is used to reduce ghosting effect for lower Color Clamping Intensity*[IndirectDiffuseTemporalFilteringColorClampingIntensity](../../...md#render_indirect_diffuse_temporal_filtering_color_clamping_intensity)* values: it automatically increases clamping intensity for higher velocities, and disables clamping for low velocity values.
Range of values: **[0.0f, inf]**. The default value is : **100.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DenoisePreset](/api/library/rendering/class.render_cs#render_denoise_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool IndirectDiffuseDenoiseEnabled

***Console*:**`render_indirect_diffuse_denoise_enabled`The value indicating if noise reduction for Indirect Diffuse is enabled. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DenoisePreset](/api/library/rendering/class.render_cs#render_denoise_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool IndirectDiffuseDenoiseMaskEnabled

***Console*:**`render_indirect_diffuse_denoise_mask_enabled`The value indicating if the denoise mask for Indirect Diffuse is enabled. This mask identifies which portions of the screen should be denoised more, and which - less. This may ensure more detailed ambient lighting. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DenoisePreset](/api/library/rendering/class.render_cs#render_denoise_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float IndirectDiffuseDenoiseThreshold

***Console*:**`render_indirect_diffuse_denoise_threshold`The threshold value for color difference of neighboring pixels used for noise reduction for Indirect Diffuse. Blur is applied when the color difference is less than the threshold value.
> **Notice:** Setting too high values results in blurring the whole image.

Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DenoisePreset](/api/library/rendering/class.render_cs#render_denoise_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool IndirectSpecularTemporalFilteringEnabled

***Console*:**`render_indirect_specular_temporal_filtering_enabled`The value indicating if temporal filtering for Indirect Specular is enabled. Temporal filtering reduces flickering of Indirect Specular lighting. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DenoisePreset](/api/library/rendering/class.render_cs#render_denoise_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float IndirectSpecularTemporalFilteringFrameCount

***Console*:**`render_indirect_specular_temporal_filtering_frame_count`The [frame count](../../../principles/render/antialiasing/taa.md#taa_frame_count) of temporal filtering for Indirect Specular. Specifies the number of frames for the velocity buffer. The higher the value, the more frames are combined into the final image and the better anti-aliasing.
Range of values: **[0.0f, inf]**. The default value is : **50.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DenoisePreset](/api/library/rendering/class.render_cs#render_denoise_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float IndirectSpecularTemporalFilteringColorClampingIntensity

***Console*:**`render_indirect_specular_temporal_filtering_color_clamping_intensity`The intensity of temporal filtering color clamping at zero pixel velocity for Indirect Specular. *Lower* values result in more accumulated frames combined, which reduces noise flickering, but increases ghosting effect. To reduce ghosting in this case you can use Indirect Specular Temporal Filtering Color Clamping Velocity Threshold*[IndirectSpecularTemporalFilteringColorClampingVelocityThreshold](../../...md#render_indirect_specular_temporal_filtering_color_clamping_velocity_threshold)*, while *higher* values reduce ghosting effect, but increase flickering.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DenoisePreset](/api/library/rendering/class.render_cs#render_denoise_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float IndirectSpecularTemporalFilteringColorClampingVelocityThreshold

***Console*:**`render_indirect_specular_temporal_filtering_color_clamping_velocity_threshold`The sensitivity of temporal filtering color clamping for Indirect Specular to pixel velocity change. This parameter is used to reduce ghosting effect for lower Color Clamping Intensity*[IndirectSpecularTemporalFilteringColorClampingIntensity](../../...md#render_indirect_specular_temporal_filtering_color_clamping_intensity)* values: it automatically increases clamping intensity for higher velocities, and disables clamping for low velocity values.
Range of values: **[0.0f, inf]**. The default value is : **100.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DenoisePreset](/api/library/rendering/class.render_cs#render_denoise_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool IndirectSpecularDenoiseEnabled

***Console*:**`render_indirect_specular_denoise_enabled`The value indicating if noise reduction for Indirect Specular is enabled. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DenoisePreset](/api/library/rendering/class.render_cs#render_denoise_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool IndirectSpecularDenoiseMaskEnabled

***Console*:**`render_indirect_specular_denoise_mask_enabled`The value indicating if the denoise mask for Indirect Specular is enabled.This mask identifies which portions of the screen should be denoised more, and which - less. This may ensure more detailed ambient lighting. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DenoisePreset](/api/library/rendering/class.render_cs#render_denoise_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float IndirectSpecularDenoiseThreshold

***Console*:**`render_indirect_specular_denoise_threshold`The threshold value for color difference of neighboring pixels used for noise reduction for the Indirect Specular effect. Blur is applied when the color difference is less than the threshold value.
> **Notice:** Setting too high values results in blurring the whole image.

Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DenoisePreset](/api/library/rendering/class.render_cs#render_denoise_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int DenoisePreset

***Console*:**`render_denoise_preset`The Denoise preset used at the moment. ***Sharpest*** to ***Smoothest*** - intensity of applying the noise reduction temporal filter (smoother settings cause more ghosting, but provide a more credible and smooth effect in static scenes). ***Low*** to ***High*** - quality of blur processing in denoiser (higher values are more performance-consuming). To customize the Denoise effect options at run time, activate the **Custom** preset.
```csharp
// enabling the Custom preset (the last one) to customize the Denoise effect options at run time
Render.DenoisePreset = Render.DenoisePresetNumNames - 1;

// disabling the Indirect Diffuse Denoise option
Render.IndirectDiffuseDenoiseEnabled = false;

```

  One of the following values:
- **0** - Disabled (by default)
- **1** - Sharpest Low
- **2** - Sharpest High
- **3** - Sharp Low
- **4** - Sharp High
- **5** - Smooth Low
- **6** - Smooth High
- **7** - Smoothest Low
- **8** - Smoothest High
- **9** - Custom

## 🔒︎ int DenoisePresetNumNames

The number of Denoise presets.
## int DenoiseRadius

***Console*:**`render_denoise_radius`The radius of each blur iteration in noise reduction. This value allows simulating a higher number of blur iterations without affecting performance. However, this may cause such screen-space artefact as insufficiently smooth denoiser blur.
Range of values: **[1, 3]**. The default value is : **1**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DenoisePreset](/api/library/rendering/class.render_cs#render_denoise_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int DenoiseNumBlurIterations

***Console*:**`render_denoise_num_blur_iterations`The number of iterations performed for blurring. Higher values increase the blur radius, which helps to reduce noise even in areas with very intense noise. However this greatly affects performance. Recommended values are in range [3, 5].
Range of values: **[0, 10]**. The default value is : **5**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[DenoisePreset](/api/library/rendering/class.render_cs#render_denoise_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool SSSSS

***Console*:**`render_sssss`The  value indicating if the SSSSS (Screen-Space Subsurface Scattering) effect is enabled. This effect is used to imitate human skin, wax, etc.  The default value is **false**.
## int SSSSSPreset

***Console*:**`render_sssss_preset`The SSSSS (Screen-Space Subsurface Scattering) preset used at the moment. To customize the SSSSS effect options at run time you should activate the **Custom** preset:
```csharp
// enabling the Custom preset (the last one) to customize the SSSSS effect options at run time
Render.SSSSSPreset = Render.SSSSSPresetNumNames - 1;

// setting the SSSSS resolution mode
Render.SSSSSResolution = 2;

```

  One of the following values:
- **0** - Low (by default)
- **1** - Medium
- **2** - High
- **3** - Ultra
- **4** - Extreme
- **5** - Custom

## 🔒︎ int SSSSSPresetNumNames

The number of SSSSS (Screen-Space Subsurface Scattering) presets.
## int SSSSSQuality

***Console*:**`render_sssss_quality`The [quality](../../../editor2/settings/render_settings/sss/index.md#sss_quality) of the SSSSS (Screen-Space Subsurface Scattering) effect. One of the following values:

- *Low* - low quality
- *Medium* - medium quality (by default)
- *High* - high quality
- *Ultra* - ultra quality

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int SSSSSResolution

***Console*:**`render_sssss_resolution`The [resolution](../../../editor2/settings/render_settings/sss/index.md#sss_resolution) of the SSSSS (Screen-Space Subsurface Scattering) effect. One of the following values:

- *Quarter* - quarter resolution
- *Half* - half resolution (by default)
- *Full* - full resolution

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSSSSRadius

***Console*:**`render_sssss_radius`The  [subsurface scattering radius](../../../editor2/settings/render_settings/sss/index.md#sss_radius) - distance in the screen space, within which colors will be sampled.It controls how much wrinkles, pores and cavities will be blurred and highlighted. The higher the value, the farther subsurface scattering reaches. Too high values result in the ghosting effect. By the minimum value of 0, no subsurface scattering is rendered.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## vec4 SSSSSColor

***Console*:**`render_sssss_color`The  [subsurface scattering color](../../../editor2/settings/render_settings/sss/index.md#sss_color) used to simulate the subsurface component of skin lighting, i.e. the light that bounces inside of the subsurface tissue layers (epidermis and dermis) before exiting.For skin, subsurface color is reddish, due to blood circulating in skin tissues. To use this option, SSSSS effect *[SSSSS](../../...md#render_sssss)* should be enabled.
**vec4(1.0f, 0.0f, 0.0f, 1.0f)** - default value
## bool SSSSSDiffuse

***Console*:**`render_sssss_diffuse`The value indicating if the SSSSS (Screen-Space Subsurface Scattering) calculation for diffuse lighting (directional lights) is enabled. If this option is not required, disable it to save performance. To use this option, the SSSSS effect*[SSSSS](../../...md#render_sssss)* should be enabled. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool SSSSSAmbient

***Console*:**`render_sssss_ambient`The value indicating if the SSSSS (Screen-Space Subsurface Scattering) calculation for ambient lighting (environment) is enabled. If this option is not required, disable it to save performance. To use this option, the SSSSS effect*[SSSSS](../../...md#render_sssss)* should be enabled. The default value is **false**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSSSSMinThreshold

***Console*:**`render_sssss_min_threshold`The threshold of SSSSS (Screen-Space Subsurface Scattering) for the material's [Translucent](../../../content/materials/library/mesh_base/index.md#parameter_translucency) parameter equal to 0 (minimum translucency). To use this option, the SSSSS effect*[SSSSS](../../...md#render_sssss)* should be enabled.
Range of values: **[0.0f, inf]**. The default value is : **4.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSSSSMaxThreshold

***Console*:**`render_sssss_max_threshold`The threshold of SSSSS (Screen-Space Subsurface Scattering) for the material's [Translucent](../../../content/materials/library/mesh_base/index.md#parameter_translucency) parameter equal to 1 (maximum translucency). To use this option, the SSSSS effect*[SSSSS](../../...md#render_sssss)* should be enabled.
Range of values: **[0.0f, inf]**. The default value is : **10.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSSSSNoiseStep

***Console*:**`render_sssss_noise_step`The intensity of the step noise used for SSSSS (Screen-Space Subsurface Scattering) calculation to reduce banding artifacts of tracing. Higher values make banding less visible. To use this option, the SSSSS effect*[SSSSS](../../...md#render_sssss)* should be enabled.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSSSSNoiseRay

***Console*:**`render_sssss_noise_ray`The intensity of the ray noise used for SSSSS (Screen-Space Subsurface Scattering) calculation to reduce banding artifacts of tracing. Higher values make banding less visible. To use this option, the SSSSS effect*[SSSSS](../../...md#render_sssss)* should be enabled.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool SSSSSInterleaved

***Console*:**`render_sssss_interleaved`The value indicating if the [interleaved rendering mode](../../../editor2/settings/render_settings/sss/index.md#sss_interleaved) for SSSSS (Screen-Space Subsurface Scattering) is enabled. This option enables rendering of the effect in only half or quarter of all pixels with subsequent reconstruction of neighboring pixels using the data from previous frames, significantly improving performance.
The effect is cumulative and works best with *[Temporal Filter](../../../editor2/settings/render_settings/sss/index.md#taa)*, which reduces ghosting and noise artifacts.

 The default value is **false**.
## int SSSSSInterleavedColorClamping

***Console*:**`render_sssss_interleaved_color_clamping`The [color clamping mode](../../../editor2/settings/render_settings/sss/index.md#sss_interleaved_color_clamping) used to reduce ghosting effect. *Higher* values increase clamping intensity, but may cause flickering (to reduce flickering you can choose **High + Velocity**). When disabled, translucency has a lag as it is several frames behind. One of the following values:
- **0** - Disabled
- **1** - Low (by default)
- **2** - Medium
- **3** - High
- **4** - High + Velocity

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int SSSSSInterleavedSamples

***Console*:**`render_sssss_interleaved_samples`The number of pixels to be skipped when rendering the SSSSS (Screen-Space Subsurface Scattering) effect with subsequent reconstruction of neighboring pixels using the data from previous frames. The following options are available:
- **1 x 2** (1.0 * width x 0.5 * height) - a half of all pixels is rendered, skipping each second line
- **2 x 2** (0.5 * width x 0.5 * height) - a quarter of all pixels is rendered, skipping each second line and row

  One of the following values:
- **0** - 1 x 2 (by default)
- **1** - 2 x 2

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool SSSSSTAA

***Console*:**`render_sssss_taa`The value indicating if [TAA (Temporal Anti-Aliasing)](../../../principles/render/antialiasing/taa.md) for Screen-Space Subsurface Scattering is enabled. The default value is **true**.
## bool SSSSSTAAFixFlicker

***Console*:**`render_sssss_taa_fix_flicker`The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Fix Flicker](#render_taa_fix_flicker)*[TAAFixFlicker](../../...md#render_taa_fix_flicker)*. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool SSSSSTAAAntialiasingInMotion

***Console*:**`render_sssss_taa_antialiasing_in_motion`The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Antialiasing In Motion](#render_taa_antialiasing_in_motion)*[TAAAntialiasingInMotion](../../...md#render_taa_antialiasing_in_motion)*. The default value is **false**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool SSSSSTAAFramesByColor

***Console*:**`render_sssss_taa_frames_by_color`The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Frames By Color](#render_taa_frames_by_color)*[TAAFramesByColor](../../...md#render_taa_frames_by_color)*. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool SSSSSTAAFramesByVelocity

***Console*:**`render_sssss_taa_frames_by_velocity`The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Frames By Velocity](#render_taa_frames_by_velocity)*[TAAFramesByVelocity](../../...md#render_taa_frames_by_velocity)*. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSSSSTAAPreserveDetails

***Console*:**`render_sssss_taa_preserve_details`The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Preserve Details](#render_taa_preserve_details)*[TAAPreserveDetails](../../...md#render_taa_preserve_details)*.
Range of values: **[0.0f, inf]**. The default value is : **0.5f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSSSSTAAFrameCount

***Console*:**`render_sssss_taa_frame_count`The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Frame Count](#render_taa_frame_count)*[TAAFrameCount](../../...md#render_taa_frame_count)*.
Range of values: **[0.0f, inf]**. The default value is : **30.0f**.
## float SSSSSTAAFramesVelocityThreshold

***Console*:**`render_sssss_taa_frames_velocity_threshold`The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Frames Velocity Threshold](#render_taa_frames_velocity_threshold)*[TAAFramesVelocityThreshold](../../...md#render_taa_frames_velocity_threshold)*.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float SSSSSTAAPixelOffset

***Console*:**`render_sssss_taa_pixel_offset`The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Pixel Offset](#render_taa_pixel_offset)*[TAAPixelOffset](../../...md#render_taa_pixel_offset)*.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool SSSSSTAACatmullResampling

***Console*:**`render_sssss_taa_catmull_resampling`The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Catmull Resampling](#render_taa_catmull_resampling)*[TAACatmullResampling](../../...md#render_taa_catmull_resampling)*. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int SSSSSTAASamples

***Console*:**`render_sssss_taa_samples`The value of TAA parameter for Screen-Space Subsurface Scattering that is similar to [TAA Samples](#render_taa_samples)*[TAASamples](../../...md#render_taa_samples)*. One of the following values:
- **0** - 1 sample offset, no anti-aliasing
- **1** - 4 offsets (by default)
- **2** - 8 offsets
- **3** - 16 offsets

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSSSSPreset](/api/library/rendering/class.render_cs#render_sssss_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSRTonemappingGamma

***Console*:**`render_ssr_tonemapping_gamma`The tonemapping Gamma value for the SSR effect. Helps reducing noise for reflections from bright surfaces. 1.0f corresponds to the physically correct value. The recommended value is 2.0f - although it slightly reduces the reflection brightness, it also significantly reduces noise.
Range of values: **[0.0f, 10.0f]**. The default value is : **2.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSRRoughnessMipOffset

***Console*:**`render_ssr_roughness_mip_offset`The mip offset value for the SSR effect on rough surfaces. Enhances reading a color on rough surfaces on lower-resolution screens. This setting allows reducing the noise and improving performance.
Range of values: **[0.0f, 10.0f]**. The default value is : **4.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSRPerspectiveCompensation

***Console*:**`render_ssr_perspective_compensation`The perspective compensation value for the SSR effect. At 0.0f, the raymarching step size doesn't depend on the distance from the reflecting surface to the camera. At 1.0f, the raymarching step size linearly depends on the distance from the reflecting surface to the camera.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSRNonLinearStepSize

***Console*:**`render_ssr_non_linear_step_size`The linear step size for the SSR effect. At 0.0f, all raymarching steps are of the same size. At 1.0f, each raymarching step is longer than a preceding one, which allows increasing the ray length while keeping the same number of raymarching steps.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int SSRAlphaAccumulationMode

***Console*:**`render_ssr_alpha_accumulation_mode`The [accumulation mode](../../../editor2/settings/render_settings/sss/index.md#sss_interleaved_color_clamping) for Alpha values used when rendering screen-space reflections. Two modes are available:
- Correct - physically correct implementation.
- Boosted - artificial implementation that makes SSR more intense and adds additional contrast to some scenes.

  One of the following values:
- **0** - Correct
- **1** - Boosted (by default)

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSRThresholdOcclusion

***Console*:**`render_ssr_threshold_occlusion`The value that [limits](../../../editor2/settings/render_settings/ssr/index.md#ssr_threshold_occlusion) imitation of environment cubemap occlusion in areas where SSR (Screen-Space Reflections) cannot get information. *Higher* values make the effect less pronounced. This parameter is mainly used for indoor environment to correct false reflections on occluded areas (false reflections are replaced with black color). For outdoor environment, higher values of this parameter are recommended.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSRThreshold

***Console*:**`render_ssr_threshold`The threshold used for SSR (Screen-Space Reflections) calculation to limit imitation of reflections in areas where SSR cannot get information. *Higher* values make the effect less pronounced.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSRVisibilityRoughnessMax

***Console*:**`render_ssr_visibility_roughness_max`The [maximum roughness value](../../../editor2/settings/render_settings/ssr/index.md#ssr_visibility_roughness_max), starting from which the SSR (Screen-Space Reflections) effect is not rendered. It allows reducing noise of reflections on rough materials.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSRVisibilityRoughnessMin

***Console*:**`render_ssr_visibility_roughness_min`The [minimum roughness value](../../../editor2/settings/render_settings/ssr/index.md#ssr_visibility_roughness_min), starting from which the SSR (Screen-Space Reflections) effect begins to fade out. It allows reducing noise of reflections on rough materials.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool SSRInformationLostFix

***Console*:**`render_ssr_information_lost_fix`The value indicating if the information lost fix option is enabled for the SSR (Screen Space Reflections). This option removes artifacts in the information lost areas around moving objects. The default value is **false**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSRStepSize

***Console*:**`render_ssr_step_size`The [size of the trace step](../../../editor2/settings/render_settings/ssr/index.md#ssr_step_size) used for SSR calculation. *Higher* values result in longer traces (however, tiny objects may become missing), *lower* values produce more detailed reflections of tiny objects.
Range of values: **[0.0f, inf]**. The default value is : **0.5f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int SSRNumSteps

***Console*:**`render_ssr_num_steps`The [number of SSR steps](../../../editor2/settings/render_settings/ssr/index.md#ssr_num_steps) per ray that are used for trace calculation. The number of steps defines accuracy of reflections and causes a reasonable performance impact. The higher the value, the more accurate obstacles between objects are accounted.
Range of values: **[1, 64]**. The default value is : **16**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int SSRNumRays

***Console*:**`render_ssr_num_rays`The [number of SSR rays](../../../editor2/settings/render_settings/ssr/index.md#ssr_num_rays) per pixel that are used to calculate rough refrections. Using more rays provides more precise SSR roughness calculation, however, it is more expensive.
Range of values: **[1, 64]**. The default value is : **4**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int SSRResolutionColor

***Console*:**`render_ssr_resolution_color`The [resolution](../../../editor2/settings/render_settings/ssr/index.md#ssr_resolution_depth) of the color buffer used for SSR (Screen Space Reflections) calculation. It significantly affects performance. One of the following values:

- *Quarter* - quarter resolution (by default)
- *Half* - half resolution
- *Full* - full resolution

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int SSRResolutionDepth

***Console*:**`render_ssr_resolution_depth`The [resolution](../../../editor2/settings/render_settings/ssr/index.md#ssr_resolution_depth) of the depth buffer used for SSR (Screen Space Reflections) calculation. It affects detailing of reflections of tiny objects.
> **Notice:** To gain performance, this option can be set to lower values while enabling increased accuracy*[SSRIncreasedAccuracy](../../...md#render_ssr_increased_accuracy)*.

 One of the following values:

- *Quarter* - quarter resolution (by default)
- *Half* - half resolution
- *Full* - full resolution

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int SSRResolution

***Console*:**`render_ssr_resolution`The [resolution](../../../editor2/settings/render_settings/ssr/index.md#ssr_resolution) of SSR (Screen Space Reflections). One of the following values:

- *Quarter* - quarter resolution
- *Half* - half resolution (by default)
- *Full* - full resolution

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool SSRIncreasedAccuracy

***Console*:**`render_ssr_increased_accuracy`The value indicating if [increased accuracy](../../../editor2/settings/render_settings/ssr/index.md#ssr_increased_accuracy) option is enabled for the SSR (Screen Space Reflections). This option increases the accuracy of intersection detection between the ray and surfaces, which makes a reflection on smooth surfaces more detailed. The default value is **false**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool SSR

***Console*:**`render_ssr`The value indicating if the SSR (Screen Space Reflections) effect is enabled. The default value is **false**.
## bool BentNormal

***Console*:**`render_bent_normal`The value indicating if ray-traced bent normals calculation is enabled. The use of SSRTGI for bent normals allows for smooth ambient lighting.
> **Notice:** Ray-traced bent normals calculation available only when the SSRTGI technique*[SSRTGIPreset](../../...md#render_ssrtgi_preset)* is enabled.

  The default value is **false**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRTGIPreset](/api/library/rendering/class.render_cs#render_ssrtgi_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float BentNormalThreshold

***Console*:**`render_bent_normal_threshold`The threshold value for the ray-traced bent normals calculation.
> **Notice:** Ray-traced bent normals calculation is available only when the SSRTGI technique*[SSRTGIPreset](../../...md#render_ssrtgi_preset)* is enabled.

Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRTGIPreset](/api/library/rendering/class.render_cs#render_ssrtgi_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool BentNormalFixOverlitAreas

***Console*:**`render_bent_normal_fix_overlit_areas`The value indicating if correction of overlit areas for bent normals calculation is enabled.
> **Notice:** - This option may significantly affect performance, so disable it when it's not necessary.
> - Ray-traced bent normals calculation is available only when the SSRTGI technique*[SSRTGIPreset](../../...md#render_ssrtgi_preset)* is enabled.

  The default value is **false**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRTGIPreset](/api/library/rendering/class.render_cs#render_ssrtgi_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool SSGI

***Console*:**`render_ssgi`The value indicating if the [SSGI](../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssgi/index.md) (Screen Space Global Illumination) effect is enabled. The default value is **false**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via ). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSGIIntensity

***Console*:**`render_ssgi_intensity`The [intensity](../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssgi/index.md#ssgi_intensity) of the SSGI (Screen Space Global Illumination) for the scene. By the minimum value of 0.0f, the global illumination is the darkest.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRTGIPreset](/api/library/rendering/class.render_cs#render_ssrtgi_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool SSGIInformationLostFix

***Console*:**`render_ssgi_information_lost_fix`The value indicating if the information lost fix option is enabled for the ray-traced SSGI (Screen Space Global Illumination). This option removes artifacts in the information lost areas around moving objects. The default value is **false**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRTGIPreset](/api/library/rendering/class.render_cs#render_ssrtgi_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSGIThreshold

***Console*:**`render_ssgi_threshold`The threshold value for the ray-traced SSGI (Screen Space Global Illumination).
> **Notice:** Ray-traced SSGI calculation available only when the SSRTGI technique*[SSRTGIPreset](../../...md#render_ssrtgi_preset)* is enabled.


Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRTGIPreset](/api/library/rendering/class.render_cs#render_ssrtgi_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSAOThreshold

***Console*:**`render_ssao_threshold`The threshold value for the SSAO (Screen Space Ambient Occlusion) effect. It limits SSAO in areas where information cannot be obtained. The *higher* the value, the less pronounced the effect is.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**.
## float SSAOCavityRadius

***Console*:**`render_ssao_cavity_radius`The size of junction contours area for the cavity option for the SSAO (Screen Space Ambient Occlusion) effect*[SSAOCavity](../../...md#render_ssao_cavity)*.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float SSAOCavityIntensity

***Console*:**`render_ssao_cavity_intensity`The intensity of sharpening of contours for the cavity option*[SSAOCavity](../../...md#render_ssao_cavity)*.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float SSAOIntensityReflection

***Console*:**`render_ssao_intensity_reflection`The intensity of SSAO (Screen Space Ambient Occlusion) on reflections.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float SSAOIntensity

***Console*:**`render_ssao_intensity`The [intensity](../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssao/index.md#ssao_intensity) of the SSAO (Screen Space Ambient Occlusion) for the scene. The intensity value affects brightness of shadows: by the minimum value of 0.0f, the ambient occlusion shadowing is the lightest.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## bool SSAOCavity

***Console*:**`render_ssao_cavity`The value indicating if the cavity option for the SSAO (Screen Space Ambient Occlusion) effect is enabled. This option improves (sharpens) the look of junction contours at low resolutions, so it should be used for detail enhancement (small stones, bolts and so on).
> **Notice:** When checking the parameter value via API, you'll get the corresponding setting stored in the active preset (default or custom one).

  The default value is **true**.
## bool SSAO

***Console*:**`render_ssao`The value indicating if the [SSAO](../../../editor2/settings/render_settings/global_illumination/indirect_diffuse/ssao/index.md) (Screen Space Ambient Occlusion) effect is enabled. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via ). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSRTGIStepSize

***Console*:**`render_ssrtgi_step_size`The size of the trace step used for SSRTGI calculation. The higher the value, the longer the trace. However, tiny objects may be missed. The lower the value, the more detailed will be the tiny objects. The SSRTGI effect must be enabled*[SSRTGIPreset](../../...md#render_ssrtgi_preset)*.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRTGIPreset](/api/library/rendering/class.render_cs#render_ssrtgi_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int SSRTGINumSteps

***Console*:**`render_ssrtgi_num_steps`The number of steps of SSRTGI per ray that are used for trace calculation. The higher the value, the more accurate obstacles between objects are accounted. However, this option significantly affects performance. SSRTGI must be enabled*[SSRTGIPreset](../../...md#render_ssrtgi_preset)*.
Range of values: **[1, 256]**. The default value is : **8**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRTGIPreset](/api/library/rendering/class.render_cs#render_ssrtgi_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int SSRTGINumRays

***Console*:**`render_ssrtgi_num_rays`The number of rays of SSRTGI per pixel that are used to calculate the final image. Using more rays provides more precise SSRTGI calculation, however, it is more expensive. SSRTGI must be enabled*[SSRTGIPreset](../../...md#render_ssrtgi_preset)*.
Range of values: **[1, 1024]**. The default value is : **8**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRTGIPreset](/api/library/rendering/class.render_cs#render_ssrtgi_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int SSRTGIResolutionDepth

***Console*:**`render_ssrtgi_resolution_depth`The resolution of the depth buffer used for SSRTGI (screen space ray-traced global illumination) calculation. This option significantly affects performance. To gain performance this option can be set to lower values while enabling the increased accuracy*[SSRTGIIncreasedAccuracy](../../...md#render_ssrtgi_increased_accuracy)*. SSRTGI must be enabled*[SSRTGIPreset](../../...md#render_ssrtgi_preset)*. One of the following values:

- *Quarter* - quarter resolution (by default)
- *Half* - half resolution
- *Full* - full resolution

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRTGIPreset](/api/library/rendering/class.render_cs#render_ssrtgi_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int SSRTGIResolution

***Console*:**`render_ssrtgi_resolution`The resolution of the SSRTGI (screen space ray-traced global illumination) effect. This option significantly affects performance. At low values, edges of objects become blurred. SSRTGI must be enabled*[SSRTGIPreset](../../...md#render_ssrtgi_preset)*. One of the following values:

- *Quarter* - quarter resolution
- *Half* - half resolution (by default)
- *Full* - full resolution

## bool SSRTGIUpscaling

***Console*:**`render_ssrtgi_upscaling`The value indicating if upscaling is enabled for the SSRTGI (screen space ray-traced global illumination). This option makes the quality of edges in half and quarter resolution look closer to full. SSRTGI must be enabled*[SSRTGIPreset](../../...md#render_ssrtgi_preset)*. The default value is **true**.
## bool SSRTGIIncreasedAccuracy

***Console*:**`render_ssrtgi_increased_accuracy`The value indicating if increased accuracy is enabled for the SSRTGI (Screen Space Ray-Traced Global Illumination). This option reduces visual artifacts by increasing accuracy of the last step. SSRTGI must be enabled*[SSRTGIPreset](../../...md#render_ssrtgi_preset)*. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRTGIPreset](/api/library/rendering/class.render_cs#render_ssrtgi_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool SSRTGIFastTracing

***Console*:**`render_ssrtgi_fast_tracing`The value indicating if fast tracing is enabled for the SSRTGI (Screen Space Ray-Traced Global Illumination). This option dynamically changes step size to obtain indirect illumination bounces using low number of steps while keeping performance high. Disabling this option improves quality, but significantly reduces performance. SSRTGI must be enabled*[SSRTGIPreset](../../...md#render_ssrtgi_preset)*. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRTGIPreset](/api/library/rendering/class.render_cs#render_ssrtgi_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool ReflectionLods

***Console*:**`render_reflection_lods`The value indicating if reduction of resolution of dynamic reflections when the camera moves away is enabled. The default value is **true**.
## bool ReflectionDynamic

***Console*:**`render_reflection_dynamic`The value indicating if dynamic reflections for materials are enabled. The default value is **true**.
## bool TransparentBlur

***Console*:**`render_transparent_blur`The value indicating if transparent blur is enabled for materials. This option makes it possible to render matte transparent materials like matte glass. The default value is **true**.
## vec3 RefractionDispersion

***Console*:**`render_refraction_dispersion`The refraction displacement for red, green, and blue channels (according to the refraction texture of refractive materials). Can be used to create light dispersion (chromatic aberrations). To use this option, render_refraction*[Refraction](../../...md#render_refraction)* should be enabled.
vec3_one - default value
## bool Refraction

***Console*:**`render_refraction`The value indicating if refraction is enabled. The default value is **true**.
## bool Sharpen

***Console*:**`render_sharpen`The value indicating if the sharpening post-processing effect is enabled. The default value is **false**.
## float SharpenIntensity

***Console*:**`render_sharpen_intensity`The intensity of the sharpening effect. To use this option, sharpening post-processing effect should be enabled*[Sharpen](../../...md#render_sharpen)*.
Range of values: **[0.0f, inf]**. The default value is : **0.5f**.
## bool SharpenDiagonalSamples

***Console*:**`render_sharpen_diagonal_samples`The value indicating diagonal neighboring pixels are included in the blur calculation, which is a part of the [sharpening post-processing effect](#render_sharpen). When enabled, all eight surrounding pixels affect the blur, resulting in a more rounded and consistent blur shape, but may affect performance. Disabling it limits the effect to only horizontal and vertical neighbors (left, right, top, bottom). The default value is **true**.
## int SharpenResolution

***Console*:**`render_sharpen_resolution`The resolution of the [sharpening post-processing effect](#render_sharpen). One of the following values:

- *Quarter* - quarter resolution
- *Half* - half resolution
- *Full* - full resolution (by default)

## float SharpenBlurColorThreshold

***Console*:**`render_sharpen_blur_color_threshold`The brightness difference threshold between neighboring pixels to determine whether they should be blurred together when the [sharpening post-processing effect](#render_sharpen) is applied. If the brightness difference is below this threshold, the pixels will be blurred as a group. Lower values help avoid visual artifacts such as blooming around objects, harsh shadows, or thin details like wires against the sky.
Range of values: **[0.001f, inf]**. The default value is : **0.2f**.
## float SharpenBlurDarkColorThresholdBias

***Console*:**`render_sharpen_blur_dark_color_threshold_bias`The bias value applied to the sharpening blur in dark regions of the image. This value is used in the [sharpening post-processing effect](#render_sharpen) to reduce excessive noise that may occur when sharpening low-light areas during post-processing.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.05f**.
## int SharpenBlurRadius

***Console*:**`render_sharpen_blur_radius`The radius of the blur applied in the [sharpening post-processing effect](#render_sharpen). A radius greater than 1-2 pixels may cause an undesirable blooming effect and negatively affect performance.
Range of values: **[1, INT_MAX]**. The default value is : **1**.
## float SharpenBlurSigma

***Console*:**`render_sharpen_blur_sigma`The smoothing applied to the Gaussian blur used in the [sharpening post-processing effect](#render_sharpen). Lower values result in a smoother, less noticeable blur. Such values are effective when the [blur radius](#render_sharpen_blur_radius) is greater than 1 pixel. If the blur radius is set to 1 pixel, a value of 1 is typically sufficient.
Range of values: **[0.001f, inf]**. The default value is : **1.0f**.
## bool AlphaFade

***Console*:**`render_alpha_fade`The value indicating if [alpha-blend fading](../../../principles/world_management/index.md#fading) (dithering) is enabled for objects. When the feature is enabled, objects LODs are smoothly blended into each other over a [fade distance](../../../principles/world_management/index.md#fading). The default value is **true**.
## bool Auxiliary

***Console*:**`render_auxiliary`The value indicating if auxiliary render buffer is used. The buffer should be enabled for render and post post-processes to work. The default value is **true**.
## bool Decals

***Console*:**`render_decals`The value indicating if rendering of decals is enabled. The default value is **true**.
## bool TAA

***Console*:**`render_taa`The value indicating if [TAA (Temporal Anti-Aliasing)](../../../principles/render/antialiasing/taa.md) is enabled. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[AAPreset](/api/library/rendering/class.render_cs#render_aa_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int TAAPreset

***Console*:**`render_taa_preset`The TAA (Temporal Anti-Aliasing) preset used at the moment. To customize Anti-Aliasing options at run time you should activate the **Custom** preset:
```csharp
// enabling the Custom preset (the last one) to customize Temporal Anti-Aliasing options at run time
Render.TAAPreset = Render.TAAPresetNumNames - 1;

// disabling the velocity clamping option
Render.TAAFramesByVelocity = false;

```

  One of the following values:
- **0** - Sharpest (by default)
- **1** - Sharp
- **2** - Smooth
- **3** - Smoothest
- **4** - VR Mode
- **5** - Custom

## 🔒︎ int TAAPresetNumNames

The number of TAA (Temporal Anti-Aliasing) presets.
## bool TAAFixFlicker

***Console*:**`render_taa_fix_flicker`The value indicating if the taa [fix flicker](../../../principles/render/antialiasing/taa.md#taa_fix_flicker) option is enabled. This option fixes flickering edges caused by TAA: it removes bright pixels by using the pixel brightness information from the previous frame. It is recommended to enable the option for bright thin ropes, wires and lines. The option is available only when TAA*[TAA](../../...md#render_taa)* is enabled.
> **Notice:** Enabling this option may increase performance costs.

 The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[TAAPreset](/api/library/rendering/class.render_cs#render_taa_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool TAAAntialiasingInMotion

***Console*:**`render_taa_antialiasing_in_motion`The value indicating if improved anti-aliasing in motion (for moving camera and objects) is enabled. TAA*[TAA](../../...md#render_taa)* must be enabled. The default value is **false**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[TAAPreset](/api/library/rendering/class.render_cs#render_taa_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool TAAFramesByColor

***Console*:**`render_taa_frames_by_color`The value indicating if TAA [color clamping](../../../principles/render/antialiasing/taa.md#taa_color_clamping) option is enabled. This option clamps the color of the current and previous frame. The image becomes more sharp. TAA*[TAA](../../...md#render_taa)* must be enabled. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[TAAPreset](/api/library/rendering/class.render_cs#render_taa_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool TAAFramesByVelocity

***Console*:**`render_taa_frames_by_velocity`The value indicating if the TAA [velocity clamping](../../../principles/render/antialiasing/taa.md#taa_vc_enabled) option is enabled. This option controls the number of frames combined for pixels depending on the velocity in the fragment. It reduces blurring in dynamic scenes with a lot of moving objects. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[TAAPreset](/api/library/rendering/class.render_cs#render_taa_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool TAADiagonalNeighbors

***Console*:**`render_taa_diagonal_neighbors`The value indicating if diagonally neighboring pixels are to be taken into account in the process of color clamping for TAA. This mode can be used for relatively static scenes when improved antialiasing is required. In case of a dynamic scene, blurring artefacts near the screen borders may appear. The default value is **false**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[TAAPreset](/api/library/rendering/class.render_cs#render_taa_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float TAAPreserveDetails

***Console*:**`render_taa_preserve_details`The [detail level](../../../principles/render/antialiasing/taa.md#taa_preserve_details) of TAA (Temporal Anti-Aliasing). The higher the value, the more detailed the image is. Can produce additional flickering.
Range of values: **[0.0f, inf]**. The default value is : **0.5f**.
## float TAAFrameCount

***Console*:**`render_taa_frame_count`The [frame count](../../../principles/render/antialiasing/taa.md#taa_frame_count) of TAA (Temporal Anti-Aliasing). Specifies the number of frames combined for pixels. The higher the value, the more frames are combined into the final image and the better anti-aliasing. This value is used only when the Frames By Velocity option*[TAAFramesByVelocity](../../...md#render_taa_frames_by_velocity)* is disabled.
Range of values: **[0.0f, inf]**. The default value is : **30.0f**.
## float TAAFramesVelocityThreshold

***Console*:**`render_taa_frames_velocity_threshold`The [velocity threshold](../../../principles/render/antialiasing/taa.md#taa_vc_threshold) of TAA (Temporal Anti-Aliasing), at which pixels are treated as fast moving ones.This value specifies the intensity of velocity clamping. The following options must be enabled: TAA*[TAA](../../...md#render_taa)* and TAA velocity clamping*[TAAFramesByVelocity](../../...md#render_taa_frames_by_velocity)*.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float TAAPixelOffset

***Console*:**`render_taa_pixel_offset`The size of the sample offset performed during subpixel jittering. The offset can be less than a pixel: for example, if **0.5** is set, frames will shift to half a pixel.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[TAAPreset](/api/library/rendering/class.render_cs#render_taa_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool TAACatmullResampling

***Console*:**`render_taa_catmull_resampling`The value indicating if Catmull-Rom resampling is enabled. This option enables you to reduce image blurring when the camera moves forward/backward. It is recommended to disable resampling fow low-quality presets. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[TAAPreset](/api/library/rendering/class.render_cs#render_taa_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float TAACatmullResamplingSharpness

***Console*:**`render_taa_catmull_resampling_sharpness`The sharpness value for the [Catmull-Rom resampling](#TAACatmullResampling) option.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.7f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[TAAPreset](/api/library/rendering/class.render_cs#render_taa_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int TAASamples

***Console*:**`render_taa_samples`The number of the sample offsets performed during subpixel jittering. The parameter allows reducing image jittering and blurring. By the minimum value of 0 (1 sample offset), there will be no offsets, and, therefore, no anti-aliasing. TAA*[TAA](../../...md#render_taa)* must be enabled. One of the following values:
- **0** - 1 sample offset, no anti-aliasing
- **1** - 4 offsets (by default)
- **2** - 8 offsets
- **3** - 16 offsets

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[TAAPreset](/api/library/rendering/class.render_cs#render_taa_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float TAAEdgesFrameCountMultiplier

***Console*:**`render_taa_edges_frame_count_multiplier`The multiplier for the number of frames accumulated for TAA effect on the sharp edges of objects within the image.
Range of values: **[1.0f, inf]**. The default value is : **1.0f**.
## bool FXAA

***Console*:**`render_fxaa`The value indicating if FXAA (post-process anti-aliasing) is enabled. The default value is **true**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[AAPreset](/api/library/rendering/class.render_cs#render_aa_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float FXAAIntensity

***Console*:**`render_fxaa_intensity`The intensity of FXAA. Intensity specifies the sample offset of FXAA fragment. The higher the value, the more blurred image will be.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**.
## float Supersampling

***Console*:**`render_supersampling`The number of samples per pixel used for [supersampling](../../../principles/render/antialiasing/supersampling.md).
Range of values: **[1e-6f, 8.0f]**. The default value is : **1.0f**.
## float StereoFocusSupersampling

***Console*:**`render_stereo_focus_supersampling`The supersampling factor for focus viewports in the stereo video mode (number of samples per pixel used for adjusting supersampling for focus displays). The main supersampling factor *[Supersampling](../../...md#render_supersampling)* for focus viewports is multiplied by this value.
Range of values: **[1e-6f, 2.0f]**. The default value is : **1.0f**.
## vec4 StereoHiddenAreaExposureTransform

***Console*:**`render_stereo_hidden_area_exposure_transform`The area to be used for exposure calculation, when culling of pixels that are not visible in VR mode*[StereoHiddenArea](../../...md#render_stereo_hidden_area)* is enabled. Correction of this area is used to avoid visual artefacts when clipped pixels affect exposure in visible areas. A four-component vector (X, Y, Z, W):
- First two components **(X, Y)** - sizes along the X and Y axes respectively.
- Second two components **(Z, W)** - offset values along the X and Y axes respectively. > **Notice:** These components can be used only when the hidden area culling mode*[StereoHiddenArea](../../...md#render_stereo_hidden_area)* is set to 1 or 2.

 All components are specified within the **[0.0f, 1.0f]** range.
**(0.6f, 0.6f, 0.0f, 0.0f)** - default value
## vec4 StereoHiddenAreaTransform

***Console*:**`render_stereo_hidden_area_transform`The size and offset parameters for a new oval or circular mesh to be used for culling pixels, that are not visible in VR mode. A four-component vector (X, Y, Z, W), that determines an area to be used for exposure calculation, when culling of pixels, that are not visible in VR mode, is enabled:
- First two components **(X, Y)** - sizes along the X and Y axes respectively.
- Second two components **(Z, W)** - offset values along the X and Y axes respectively. > **Notice:** These components can be used only when the hidden area culling mode*[StereoHiddenArea](../../...md#render_stereo_hidden_area)* is set to 2.

 All components are specified within the **[0.0f, 1.0f]** range
**(1.0f, 1.0f, 0.0f, 0.0f)** - default value
## int StereoHiddenArea

***Console*:**`render_stereo_hidden_area`The culling mode for pixels that are not visible in VR mode. One of the following values:
- 0 - hidden area culling is disabled (by default).
- 1 - **OpenVR-based culling mode**. Culling is performed using meshes returned by OpenVR. > **Notice:** Culling result depends on HMD used.
- **2** - **Custom culling mode**. Culling is performed using meshes returned by OpenVR and an oval or circular mesh determined by custom adjustable parameters*[StereoHiddenAreaTransform](../../...md#render_stereo_hidden_area_transform)*.

 This parameter is used for performance optimization.  One of the following values:
- **0** - disabled (by default)
- **1** - OpenVR-based culling mode
- **2** - Custom culling mode

## float StereoOffset

The virtual camera offset (an offset after the perspective projection).
## float StereoRadius

The radius for stereo (the half of the separation distance between the cameras).
## float StereoDistance

The focal distance for stereo rendering (distance in the world space to the point where two views line up).
## Render.RENDER_VR_EMULATION_MODE VREmulation

***Console*:**`render_vr_emulation`The value indicating the current VR emulation mode. The FoV value in any selected mode is 110. One of the following values:
- **0** - Disabled (by default)
- **1** - HTC Vive (1512x1680)
- **2** - HTC Vive Pro (2016x2240)
- **3** - HTC Vive Pro 2 (3428x3428)
- **4** - HTC Vive Focus 3(3428x3428)
- **5** - HTC Vive Focus Vision (3428x3428)
- **6** - HTC Vive XR Elite (1920x1920)
- **7** - Oculus Rift (1332x1586)
- **8** - Quest 2 (2712x2746)
- **9** - Quest 3S VR (2712x2746)
- **10** - Quest 3 (2064x2242)
- **11** - Quest Pro (1800x1950)
- **12** - Pico 4 (2160x2160)
- **13** - Valve Index (2016x2240)
- **14** - Varjo VR-3 (2880x2720)
- **15** - Varjo VR-4 (3840x3744)

## 🔒︎ float AnimationOldTime

The previous render animation time for vegetation.
## float AnimationTime

The render animation time for vegetation.
## vec3 AnimationWind

***Console*:**`render_animation_wind`The direction of wind for all vegetation (grass and trees). It is a multiplier for the stem offset (in grass, stem and leaves materials).
**(0.0f, 0.0f, 0.0f)** - default value
## float AnimationScale

***Console*:**`render_animation_scale`The global scale for rotation speed of vegetation leaves.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float AnimationLeaf

***Console*:**`render_animation_leaf`The global scale for rotation angle of vegetation leaves.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float AnimationStem

***Console*:**`render_animation_stem`The global scale for movement amplitude of vegetation stems.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float ShadowDistance

***Console*:**`render_shadow_distance`The distance from the camera, beyond which shadows will not be rendered.
> **Notice:** If this value is greater than the [visibility distance for objects](../../../editor2/settings/render_settings/visibility_distances/index.md#objects_distance) the shadows will still be rendered even though the objects themselves are not. Please, pay attention to setting these parameters properly to avoid wasting performance on rendering unnecessary shadows.


Range of values: **[0.0f, inf]**. The default value is : **100.0f**.
## float ShadowDistanceScale

***Console*:**`render_shadow_distance_scale`The global scale multiplier for [shadow distances](#render_shadow_distance). This option enables you to easily increase or decrease shadows rendering performance by changing the scale.
> **Notice:** If this value is greater than the scale multiplier for objects*[DistanceScale](../../...md#render_distance_scale)*, the shadows will still be rendered even though the objects themselves are not. Please, make sure you set these parameters properly to avoid wasting performance on rendering unnecessary shadows.

Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float ReflectionDistance

***Console*:**`render_reflection_distance`The distance starting from which (and farther) reflections will not be rendered.
Range of values: **[0.0f, inf]**. The default value is : **inf**.
## float OccluderDistance

***Console*:**`render_occluder_distance`The distance starting from which (and farther) occluders will not be rendered.
Range of values: **[0.0f, inf]**. The default value is : **inf**.
## float ObjectDistance

***Console*:**`render_object_distance`The distance at which (and farther) objects will not be rendered.
> **Notice:** If this value is less than the scale multiplier for shadows*[ShadowDistanceScale](../../...md#render_shadow_distance_scale)*, the shadows will still be rendered even though the objects themselves are not. Please, make sure you set these parameters properly to avoid wasting performance on rendering unnecessary shadows.

Range of values: **[0.0f, inf]**. The default value is : **inf**.
## float DecalDistance

***Console*:**`render_decal_distance`The distance at which (and farther) decals will not be rendered. The distance is measured from the camera to the decal's bound. If the value is greater than the *[World Distance](../../../editor2/settings/world/index.md#world_distance)* value, the latter is used instead.
Range of values: **[0.0f, inf]**. The default value is : **inf**.
## float LightDistance

***Console*:**`render_light_distance`The distance at which (and farther) lights will not be rendered. The distance is measured from the camera to the light's bound. If the value is greater than the *[World Distance](../../../editor2/settings/world/index.md#world_distance)* value, the latter is used instead.
Range of values: **[0.0f, inf]**. The default value is : **inf**.
## float FieldDistance

***Console*:**`render_field_distance`The distance at which (and farther) [field](../../../objects/effects/fields/index.md) nodes will not be rendered. The distance is measured from the camera to the field's bound. If the value is greater than the *[World Distance](../../../editor2/settings/world/index.md#world_distance)* value, the latter is used instead.
Range of values: **[0.0f, inf]**. The default value is : **inf**.
## float DistanceScale

***Console*:**`render_distance_scale`The global distance multiplier for all distance parameters, such as the world rendering distance, [decal distance](#getDecalDistance_float), [field distance](#getFieldDistance_float), [light distance](#getLightDistance_float), [object distance](#getObjectDistance_float), [reflection distance](#getReflectionDistance_float), LODs, and surface visibility distances. This value enables you to easily increase or decrease rendering performance by changing the world extent. Distances are measured from the camera to the node's (surface's) bound. For example, if the maximum visibility distance of a LOD is 10 meters, and you set *Distance Scale = 2*, the LOD will disappear at the distance of 20 meters, not 10.
> **Notice:** Increasing the value leads to decreasing the performance. The maximum recommended value is 4.

Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## bool ForceStreaming

The value indicating if force-streaming is enabled for all resources.
## int StreamingAnimationsLifeTime

***Console*:**`render_streaming_animations_life_time`The lifetime of GPU cache used for animations rendering.
Range of values: **[-1, INT_MAX]**. The default value is : **-1**.
## int StreamingParticlesMemoryLimit

***Console*:**`render_streaming_particles_memory_limit`The cache memory limit for vertices of particle systems, in percentage of the total GPU memory.
> **Notice:** Setting a too low limit for a huge number of particle systems in the scene may lead to rendering only some of them. Works only with the **Vulkan** graphics API.

Range of values: **[0, 100]**. The default value is : **3**.
## int StreamingCacheRAM

***Console*:**`render_streaming_cache_ram`The  maximum size of RAM available for streaming caches. When set to -1, caches grow freely up to [engine limits](#render_streaming_usage_limit_ram). When limited, caches will grow only up to the defined value. If the limit is too low, not all resources will fit into the cache in time, which may cause streaming to stutter.
Range of values: **[-1, inf]**. The default value is : **-1**.
## int StreamingCacheVRAM

***Console*:**`render_streaming_cache_vram`The  maximum size of VRAM available for streaming caches. When set to -1, caches grow freely up to [engine limits](#render_streaming_usage_limit_vram). When limited, caches will grow only up to the defined value. If the limit is too low, not all resources will fit into the cache in time, which may cause streaming to stutter.
Range of values: **[-1, inf]**. The default value is : **-1**.
## Render.STREAMING_MODE StreamingTexturesMode

***Console*:**`render_streaming_textures_mode`The streaming mode for textures. The following modes are available:
- *Async* - asynchronous loading of textures.
- *Force* - force-loading of textures required for each frame at ones.

  One of the following values:
- **0** - asynchronous streaming (by default)
- **1** - force-loading of resources

## Render.STREAMING_MODE StreamingMeshesModeVRAM

***Console*:**`render_streaming_meshes_mode_vram`The streaming mode for loading meshes to video memory (VRAM). The following modes are available:
- *Async* - asynchronous loading of meshes.
- *Force* - force-loading of meshes required for the current frame at once.

 One of the following values:
- **0** - asynchronous streaming (by default)
- **1** - force-loading of resources

## Render.STREAMING_MODE StreamingMeshesModeRAM

***Console*:**`render_streaming_meshes_mode_ram`The streaming mode for loading meshes to memory (RAM). The following modes are available:
- *Async* - asychronous loading of meshes.
- *Force* - force-loading of meshes required for the current frame at once.

 One of the following values:
- **0** - asynchronous streaming (by default)
- **1** - force-loading of resources

## Render.STREAMING_MESHES_PREFETCH StreamingMeshesPrefetchCollision

***Console*:**`render_streaming_meshes_prefetch_collision`The mode of asynchronous pre-loading of meshes to memory before they are used. Pre-loading is available only for meshes, which have at least one surface with the *Collision* flag set. There are 2 modes of loading such meshes to RAM:
- *Disable* - loading is disabled.
- *Radius* - meshes within the prefetch radius are loaded.

 This method should be used when the *Async* streaming mode for meshes is set.  One of the following values:
- **0** - disable (by default)
- **1** - radius

## Render.STREAMING_MESHES_PREFETCH StreamingMeshesPrefetchIntersection

***Console*:**`render_streaming_meshes_prefetch_intersection`The mode of asynchronous pre-loading of meshes into memory before they are used. Pre-loading is available only for meshes, which have at least one surface with the *Intersection* flag set. There are 2 modes of loading such meshes to RAM:
- *Disable* - loading is disabled.
- *Radius* - all meshes within the prefetch radius are loaded.

 This method should be used when the *Async* streaming mode for meshes is set.  One of the following values:
- **0** - disable (by default)
- **1** - radius

## float StreamingMeshesPrefetchRadius

***Console*:**`render_streaming_meshes_prefetch_radius`The radius within which meshes are pre-loaded into memory. The value should exceed the physics radius (for collisions) and/or the radius within which intersections are calculated.
Range of values: **[0.0f, inf]**. The default value is : **0.0f**.
## int TexturesAnisotropy

***Console*:**`render_textures_anisotropy`The anisotropy level for textures (degree of anisotropic filtering). One of the following values:
- **0** - level 1
- **1** - level 2
- **2** - level 4
- **3** - level 8 (by default)
- **4** - level 16

## int TexturesFilter

***Console*:**`render_textures_filter`The texture filtering mode. One of the following values:
- **0** - Bilinear
- **1** - Trilinear (by default)

## int TexturesMinResolution

***Console*:**`render_textures_min_resolution`The minimum resolution of all textures. The Engine doesn't compress existing textures: it uses specified mip maps of `*.dds` textures. One of the following values:
- **0** - 128x128 (by default)
- **1** - 256x256
- **2** - 512x512
- **3** - 1024x1024
- **4** - 2048x2048
- **5** - 4096x4096
- **6** - 8192x8192
- **7** - 16384x16384

## int TexturesMaxResolution

***Console*:**`render_textures_max_resolution`The maximum resolution of all textures. the engine doesn't compress existing textures: it uses specified mipmaps of `*.dds` textures. One of the following values:
- **0** - 128x128
- **1** - 256x256
- **2** - 512x512
- **3** - 1024x1024
- **4** - 2048x2048
- **5** - 4096x4096
- **6** - 8192x8192 (by default)
- **7** - 16384x16384

## int TexturesQuality

***Console*:**`render_textures_quality`The resolution of textures. One of the following values:

- *Low* - low quality
- *Medium* - medium quality
- *High* - high quality (by default)

## int Latency

***Console*:**`render_latency`The maximum number of back buffer frames that a driver is allowed to queue for rendering. The buffers are used for GPU load optimization: in certain cases several command buffers (frames) can be processed by GPU at once increasing the [**Waiting GPU**](../../../tools/profiling/profiler/index.md#present) time for one frame and having zero **Waiting GPU** time for the next ones. Thus, GPU avoids rendering spikes, but increased **Waiting GPU** time will cause a spike in application logic, in case when the logic is bound to [duration of a single frame](../../../api/library/engine/class.game_cs.md#getIFps_float). **Frame latency** is the number of frames that are allowed to be stored in a queue before submission for rendering. Latency is often used to control how the CPU chooses between responding to user input and frames that are in the render queue. In certain cases (high GPU load, VSYNC usage) it may be required to queue more frames of data, it is also beneficial for applications with no user input (e.g., video playback).
> **Notice:** Values 1-3 are available for DirectX only.

 One of the following values:
- **0** - sequential rendering CPU-GPU-CPU-GPU...
- **1** - 1 buffer (by default)
- **2** - 2 buffers
- **3** - 3 buffers

## UGUID DeferredMaterialGUID

The material that will be used on the [Deferred Composite](../../../principles/render/sequence/index.md#deferred_composite) stage of rendering sequence. A [debug material](#addDebugMaterial_Material_void) can be put here in order to be added to the final image.
## bool Debug

***Console*:**`render_debug`The value indicating whether debug materials (the *debug_materials* material) are rendered. Debug materials can be used for debugging of image generation stages. For example, you can render only SSR, or only cubemaps and so on. The default value is **false**.
## bool GbufferLightmap

***Console*:**`render_gbuffer_lightmap`The value indicating if lightmap data is stored in the gbuffer. The default value is **true**.
## bool DepthPrePass

***Console*:**`render_depth_pre_pass`The value indicating if depth pre-pass rendering is enabled. When enabled, an additional depth buffer rendering pass is performed in the beginning of the rendering sequence.
> **Notice:** This option can be used to gain performance for well optimized scenes using LODs and having a low-to-medium number of triangles in case of GPU bottlenecks. In other cases (heavy CAD models, large number of triangles and CPU bottlenecks) it may reduce performance, so it is recommended to use [profiling tools](../../../tools/profiling/index.md) to make sure that a positive effect is obtained.

  The default value is **false**.
## vec2 VirtualResolution

***Console*:**`render_virtual_resolution`The virtual screen resolution. This option can be used to render video with high resolution (e.g. 8K) regardless of monitor's resolution.
**-1; -1** - default value
## float MaxFPS

***Console*:**`render_max_fps`The maximum FPS value, to which rendering FPS is to be clamped.
0 - disables FPS clamping. Both [VSync](../../../code/fundamentals/execution_sequence/index.md#waiting_gpu), and *Max FPS* are actually about an additional idle period at the end of the frame. In case of *VSync* the Engine shall wait for the monitor to draw the whole image, while *Max FPS* enables you to specify any value for the delay (even a fractional, like 24.5). This clamping limit can be used for both debugging purposes and in the final build as well enabling you to smooth an unstable "jigsaw" framerate. For example, in case FPS jumps between 45 and 90, setting *Max FPS* to 45 may significantly improve your application's response visually.
Range of values: **[0.0f, inf]**. The default value is : **0.0f**.
## Render.VSYNC VSync

***Console*:**`render_vsync`The vertical synchronization (vsync) mode. Prevents rendering more than *video_refresh* frames per second. The following modes are available: One of the following values:
- **0** - Disable (by default)
- **1** - Strict
- **2** - Adaptive

## vec2 Border

***Console*:**`render_border`The width and height of the image border (in pixels), to be rendered outside the horizontal bounds of the screen to reduce artefacts of post effects.
> **Notice:** Increasing the width of the border may increase performance costs.

**(0, 0)** - default value
## float Budget

***Console*:**`render_budget`The render budget value, in seconds, which limits the number of loaded/created graphics resources during a frame according to loading/creation time.
Range of values: **[0.0f, inf]**. The default value is : **1/60**.
## UGUID CompositeMaterialGUID

The GUID of a custom composite material that specifies a custom shader used for the final composition of the full-screen image instead of the default one.
## 🔒︎ int NumScriptableMaterials

The total number of [scriptable materials](../../../content/materials/scriptable.md) applied globally.
## Viewport Viewport

The custom [viewport](../../../api/library/rendering/class.viewport_cs.md). To get the main viewport regardless of whether it is a custom or default one use *[ViewportMain](../../...md#ViewportMain)*.
> **Notice:** In case the default viewport is used the return value will be nullptr

## 🔒︎ Viewport ViewportMain

The main [viewport](../../../api/library/rendering/class.viewport_cs.md). The return value is the main viewport, regardless of whether it is a custom or default one (unlike the *[Viewport](../../...md#getViewport_Viewport)*).
## Render.VIEWPORT_MODE ViewportMode

***Console*:**`render_viewport_mode`The viewport rendering mode. The following modes are available:
- *Default* - default rendering mode.
- *Curved Panorama 180* - 180-degree panorama with curved edges.
- *Curved Panorama 360* - 360-degree panorama with curved edges.
- *Linear Panorama 180* - 180-degree linear panorama without distortion at the edges.
- *Linear Panorama 360* - 360-degree linear panorama without distortion at the edges.
- *Panorama Fisheye Orthographic* - orthographic spherical panorama (fisheye) with an adjustable Field of View.
- *Panorama Fisheye Equidistant* - equidistant (tru-theta or f-theta) spherical panorama (fisheye) with an adjustable Field of View.
- *Panorama Fisheye Stereographic* - stereographic spherical panorama (fisheye) with an adjustable Field of View.
- *Panorama Fisheye Equisolid* - equisolid (equal-area) spherical panorama (fisheye) with an adjustable Field of View.
- *Anaglyph* - stereo mode that is viewed with red-cyan anaglyph glasses.
- *Interlaced* - stereo mode that is used with interlaced stereo monitors and polarized 3D glasses.
- *Horizontal* - horizontal stereo mode.
- *Vertical* - vertical stereo mode.


> **Notice:** If the panoramic rendering is enabled, underwater shafts and water line effects will be disabled.

  One of the following values:
- **0** - Default (by default)
- **1** - Curved Panorama 180
- **2** - Curved Panorama 360
- **3** - Linear Panorama 180
- **4** - Linear Panorama 360
- **5** - Panorama Fisheye Orthographic
- **6** - Panorama Fisheye Equidistant
- **7** - Panorama Fisheye Stereographic
- **8** - Panorama Fisheye Equisolid
- **9** - Anaglyph
- **10** - Interlaced
- **11** - Horizontal
- **12** - Vertical

## string ShaderDefines

***Console*:**`render_defines`The macros list related to the renderer (defines to make corresponding resources available in shaders).
## int ClearBufferMask

The buffer cleanup mask. This mask determines which buffers are to be cleared next time the [Engine::render()](../../../code/fundamentals/execution_sequence/index.md) is called. Thus, you can determine the contents of which buffers is to be kept, avoiding situations, when necessary data is cleared.
```csharp
Render.ClearBufferMask = RenderState.BUFFER_ALL;
// color, depth & stencil buffers will be cleared
Render.ClearBufferMask = RenderState.BUFFER_NONE;
// no buffers will be cleared (useful if you want to embed the engine somewhere)
Render.ClearBufferMask = RenderState.BUFFER_DEPTH;
// only the depth buffer will be cleared

// masks can be combined:
Render.ClearBufferMask = BUFFER_COLOR | BUFFER_STENCIL;
// color and stencil buffer will be cleared

// there is a separate BUFFER_DEPTH_STENCIL mask for convenience
Render.ClearBufferMask(BUFFER_DEPTH_STENCIL);

```


## bool FirstFrame

The value indicating if the first frame is enabled over the current frame.
## string Data

The user data associated with the render. This string is written directly into a `*.world` file. Namely, into the *data* child tag of the *render* tag, for example:
```xml
<world version="1.21">
	<render>
		<data>User data</data>
	</render>
</world>

```


## 🔒︎ int MaxFieldShorelines

The maximum limit of [FieldShoreline](../../../api/library/fields/class.fieldshoreline_cs.md) nodes allowed to be used in shaders.
> **Notice:** Higher values will affect shader compilation time and performance

## 🔒︎ int MaxFieldHeights

The maximum limit of [FieldHeight](../../../api/library/fields/class.fieldheight_cs.md) nodes allowed to be used in shaders.
> **Notice:** Higher values will affect shader compilation time and performance

## 🔒︎ int MaxFieldAnimations

The maximum limit of [FieldAnimation](../../../api/library/fields/class.fieldanimation_cs.md) nodes allowed to be used in shaders.
> **Notice:** Higher values will affect shader compilation time and performance

## 🔒︎ int MaxFieldSpacers

The maximum limit of [FieldSpacer](../../../api/library/fields/class.fieldspacer_cs.md) nodes allowed to be used in shaders.
> **Notice:** Higher values will affect shader compilation time and performance

## 🔒︎ int NumInstances

The maximum number of instances that can be rendered for each of the following node types:
- [Field Animation](../../../objects/effects/fields/field_animation/index.md)
- [Field Height](../../../objects/effects/fields/field_height/index.md)
- [Field Shoreline](../../../objects/effects/fields/field_shoreline/index.md)
- [Field Spacer](../../../objects/effects/fields/field_spacer/index.md)


> **Notice:** Returned value depends on the graphics API used.


## 🔒︎ bool IsFlipped

The value indicating render orientation.
```csharp
Texture texture;
Texture texture_2;
float uv_x, uv_y;
//...
float flip_sign = (Render.IsFlipped() == 1 ? -1.0f : 1.0f);
float translate_x = 2.0f * uv_x - 1.0f;
float translate_y = flip_sign * (2.0f * uv_y - 1.0f);
float scale_x = texture.GetWidth() / texture_2.GetWidth();
float scale_y = texture.GetHeight() / texture_2.GetHeight();

mat4 transform = MathLib.Translate(translate_x, translate_y, 0.0f) * MathLib.Scale(scale_x, scale_y, 1.0f);

```


## 🔒︎ int API

The Graphics API (see *[API_*](#API_DIRECT3D12)* variables).
## int LandscapeCacheCPUSize

***Console*:**`render_landscape_cache_cpu_size`The CPU cache size to be used for landscape terrain rendering, in percentage of the total memory. CPU cache size affects intersections, physics, streaming, etc. The size of CPU cache depends on the scene.
Range of values: **[1, 100]**. The default value is : **10**.
## float LandscapeCacheCPUPrefetchRadius

***Console*:**`render_landscape_cache_cpu_prefetch_radius`The radius within which heights data is pre-loaded into memory for correct calculation of collisions and intersections.
Range of values: **[0.0f, inf]**. The default value is : **0.0f**.
## int LandscapeCacheGPUSize

***Console*:**`render_landscape_cache_gpu_size`The GPU cache size to be used for landscape terrain rendering, in percentage of the total GPU memory. GPU cache is used to accumulate tiles, that are visible to the camera, before streaming them to the megatexture.
> **Notice:** High-resolution maps require larger cache capacity.

Range of values: **[1, 100]**. The default value is : **4**.
## int LandscapeCacheGPULifeTime

***Console*:**`render_landscape_cache_gpu_life_time`The lifetime of GPU cache used for Landscape Terrain rendering, in frames.
Range of values: **[1, 60]**. The default value is : **4**.
## float LandscapeTerrainGeometrySubpixelReduction

***Console*:**`render_landscape_terrain_geometry_subpixel_reduction`The minimum ratio between the polygon size (in screen space) to the size of an area in the viewport for [skipping polygons rendering](../../../objects/objects/terrain/landscape_terrain/settings.md#subpixel_reduction) (the ones having a lower ratio will be removed).
> **Notice:** Setting too high values may cause small but noticeable visual artifacts when the camera moves.

Range of values: **[0.0f, 50.0f]**. The default value is : **6.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[LandscapeTerrainGeometryPreset](/api/library/rendering/class.render_cs#render_landscape_terrain_geometry_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float LandscapeTerrainGeometryProgression

***Console*:**`render_landscape_terrain_geometry_progression`The progression of [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md) geometry tessellation.
> **Notice:** [Reloads Landscape Terrain graphic data](../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe).

Range of values: **[0.0f, 50.0f]**. The default value is : **1.5f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[LandscapeTerrainGeometryPreset](/api/library/rendering/class.render_cs#render_landscape_terrain_geometry_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float LandscapeTerrainGeometryPolygonSize

***Console*:**`render_landscape_terrain_geometry_polygon_size`The size of Landscape Terrain polygons defining the maximum allowed density of Landscape Terrain geometry.
> **Notice:** [Reloads Landscape Terrain graphic data](../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe).

Range of values: **[0.0f, 1000.0f]**. The default value is : **0.01f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[LandscapeTerrainGeometryPreset](/api/library/rendering/class.render_cs#render_landscape_terrain_geometry_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## bool LandscapeTerrainGeometryHoles

***Console*:**`render_landscape_terrain_geometry_holes`The value indicating if [decal-based holes](../../../objects/objects/terrain/landscape_terrain/index.md#decal_holes) for the [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md) are enabled. The default value is **true**.
## int LandscapeTerrainDetailResolutionAdditionalMask

***Console*:**`render_landscape_terrain_detail_resolution_additional_mask`The resolution of the additional mask texture for details of the [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md).
> **Notice:** [Reloads Landscape Terrain graphic data](../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe).

  One of the following values:
- **0** - 64×64
- **1** - 128×128
- **2** - 256×256
- **3** - 512×512
- **4** - 1024×1024 (by default)
- **5** - 2048×2048
- **6** - 4096×4096
- **7** - 8192×8192
- **8** - 16384×16384

## int LandscapeTerrainDetailResolutionHeight

***Console*:**`render_landscape_terrain_detail_resolution_height`The resolution of the height texture for details of the [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md).
> **Notice:** [Reloads Landscape Terrain graphic data](../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe).

  One of the following values:
- **0** - 64×64
- **1** - 128×128
- **2** - 256×256
- **3** - 512×512
- **4** - 1024×1024 (by default)
- **5** - 2048×2048
- **6** - 4096×4096
- **7** - 8192×8192
- **8** - 16384×16384

## int LandscapeTerrainDetailResolutionAlbedo

***Console*:**`render_landscape_terrain_detail_resolution_albedo`The resolution of the albedo texture for details of the [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md).
> **Notice:** [Reloads Landscape Terrain graphic data](../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe).

  One of the following values:
- **0** - 64×64
- **1** - 128×128
- **2** - 256×256
- **3** - 512×512
- **4** - 1024×1024 (by default)
- **5** - 2048×2048
- **6** - 4096×4096
- **7** - 8192×8192
- **8** - 16384×16384

## int LandscapeTerrainVTTilesReloadPerFrame

***Console*:**`render_landscape_terrain_vt_tiles_reload_per_frame`The number of tiles to be reloaded per frame after applying changes to the [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md) surface.
Range of values: **[1, 64]**. The default value is : **4**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[LandscapeTerrainStreamingPreset](/api/library/rendering/class.render_cs#render_landscape_terrain_streaming_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int LandscapeTerrainVTTilesLoadPerFrame

***Console*:**`render_landscape_terrain_vt_tiles_load_per_frame`The number of [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md) tiles loaded per frame. You can decrease the value of this parameter to reduce spikes, but in this case streaming becomes slower and more noticeable.
Range of values: **[1, 64]**. The default value is : **4**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[LandscapeTerrainStreamingPreset](/api/library/rendering/class.render_cs#render_landscape_terrain_streaming_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int LandscapeTerrainVTTilesUpdatePerFrame

***Console*:**`render_landscape_terrain_vt_tiles_update_per_frame`The number of tiles passed to the virtual texture of the [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md) each frame.
Range of values: **[1, 256]**. The default value is : **60**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[LandscapeTerrainStreamingPreset](/api/library/rendering/class.render_cs#render_landscape_terrain_streaming_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int LandscapeTerrainVTFiltering

***Console*:**`render_landscape_terrain_vt_filtering`The filtering mode for the [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md) textures. The following values are available:
- Low - use the lower mip-level
- Medium - use the higher mip-level
- High - linearly interpolate between adjacent mip-levels

  One of the following values:
- **0** - Low
- **1** - Medium (by default)
- **2** - High

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[LandscapeTerrainStreamingPreset](/api/library/rendering/class.render_cs#render_landscape_terrain_streaming_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float LandscapeTerrainVTDetailLevelByAngle

***Console*:**`render_landscape_terrain_vt_detail_level_by_angle`The value indicating detail level reduction depending on the inclination of the the Landscape Terrain polygons relative to viewing direction. Can be used to reduce streaming load and memory consumption. The value of 1 corresponds to the pixel-to-pixel quality, and lower values decrease it.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.95f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[LandscapeTerrainStreamingPreset](/api/library/rendering/class.render_cs#render_landscape_terrain_streaming_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## vec2 LandscapeTerrainVTTargetResolution

***Console*:**`render_landscape_terrain_vt_target_resolution`The [target resolution](../../../objects/objects/terrain/landscape_terrain/settings.md#target_resolution) (width x height) for the Landscape Terrain, in pixels.
 **1344 х 756** - (default)
## float LandscapeTerrainVTMemorySize

***Console*:**`render_landscape_terrain_vt_memory_size`The value defining memory consumption for the [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md) textures. The value is interpreted as follows:
- 0.0f - 3072×3072 (~200 MB of VRAM)
- 1.0f - 16384×16384 (~3.1 GB of VRAM)
- **0.4f** - 8192×8192 (~860 MB of VRAM)


> **Notice:** [Reloads Landscape Terrain graphic data](../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe).


Range of values: **[0.0f, 1.0f]**. The default value is : **0.4f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[LandscapeTerrainStreamingPreset](/api/library/rendering/class.render_cs#render_landscape_terrain_streaming_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float LandscapeTerrainTexelSize

***Console*:**`render_landscape_terrain_texel_size`The texel size of the [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md) render textures representing the maximum level of detail for the albedo, normal, and height components of the Landscape Terrain.
> **Notice:** [Reloads Landscape Terrain graphic data](../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe).

Range of values: **[0.0001f, 1.0f]**. The default value is : **0.001f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[LandscapeTerrainStreamingPreset](/api/library/rendering/class.render_cs#render_landscape_terrain_streaming_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float LandscapeTerrainVisibleDistance

***Console*:**`render_landscape_terrain_visible_distance`The maximum visibility distance for the [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md), in meters. The terrain is visible, as long as the distance between the camera and the terrain does not exceed this value.
> **Notice:** [Reloads Landscape Terrain graphic data](../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe).

Range of values: **[0.0f, inf]**. The default value is : **30000.0f**.
## float LandscapeTerrainMaskDithering

***Console*:**`render_landscape_terrain_mask_dithering`The global dither amount multiplier to be used for rendering details of the [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md). Dithering enables reduction of graphical artefacts in case of increased Mask Contrast values set for a detail. This is a global multiplier for dithering values set [for each detail mask](../../../api/library/objects/landscape_terrain/class.terraindetailmask_cs.md#setDithering_float_void).
> **Notice:** [Reloads Landscape Terrain graphic data](../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe).

Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
## bool FfpAntialiasingLines

***Console*:**`render_ffp_antialiasing_lines`The value indicating if antialiasing is enabled for rendering of the Visualizer and other FFP lines.
## bool WireframeAntialiasing

***Console*:**`render_wireframe_antialiasing`The value indicating if antialiasing is enabled for wireframe rendering.
## bool EnvironmentHazeScreenSpaceGlobalIllumination

***Console*:**`render_environment_haze_screen_space_global_illumination`The value indicating if the Screen-Space Haze Global Illumination effect is enabled. SSHGI - is a screen-space effect ensuring consistency of haze color with the current color of Global Illumination.
> **Notice:** Available for **Physically Based** [haze gradient mode](#render_environment_haze_gradient) only.

 The default value is **true**.
## bool EnvironmentHazeTemporalFilter

***Console*:**`render_environment_haze_temporal_filter`The value indicating if temporal filtering for the Screen-Space Haze Global Illumination effect is enabled. The default value is **true**.
## float EnvironmentHazeColorizationThreshold

***Console*:**`render_environment_haze_colorization_threshold`The treshold value for scene depth used when setting haze color for the SSHGI effect in "information lost" areas on the screen.
- 0 - haze color is defined only by surfaces currently visible on the screen.
- 1 - haze color is defined by surfaces everywhere, even in "information lost" areas.


Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**.
## float EnvironmentHazeColorizationIntensity

***Console*:**`render_environment_haze_colorization_intensity`The colorization intensity value that defines haze color in "information lost" areas on the screen.
- 0 - haze in "information lost" areas will have the initial color (same as it would be without SSHGI).
- 1 - haze in "information lost" areas will have the less bright color among the two, initial color and haze color with SSHGI correction.


This parameter is ignored when *[Colorization Threshold](#render_environment_haze_colorization_threshold)* is set to 1, as there will be no "information lost" areas not covered by SSHGI.

Range of values: **[0.0f, 1.0f]**. The default value is : **0.95f**.
## 🔒︎ float EnvironmentHazeScatteringMieFresnelPower

The power of the Fresnel effect for Mie visibility. *Higher* values will tighten up the areas affected, while *lower* ones will allow more areas to be affected by the Fresnel effect.
## 🔒︎ float EnvironmentHazeScatteringMieFrontSideIntensity

The falloff of the Fresnel effect for Mie intensity. This paremeter enables you to control light occlusion from *World* light sources by geometry.
## 🔒︎ float EnvironmentHazeScatteringMieIntensity

The minimum Mie intensity value for geometry-occluded areas. This value specifies the fraction of Mie intensity visible when the surface is viewed from straight on. Setting this value to 1 disables the Fresnel effect. You can use this parameter together with *Mie Frontside Intensity**[EnvironmentHazeScatteringMieFrontSideIntensity](../../...md#getEnvironmentHazeScatteringMieFrontSideIntensity_float)* and *Mie Fresnel Power**[EnvironmentHazeScatteringMieFresnelPower](../../...md#getEnvironmentHazeScatteringMieFresnelPower_float)* to control light occlusion from *World* light sources. Works for both opaque and transparent objects.
## 🔒︎ float EnvironmentHazePhysicalSunColorSaturation

The intensity of the impact of the sunlight on haze (how much the sunlight affects the haze).
## 🔒︎ float EnvironmentHazePhysicalSunLightIntensity

The intensity of the impact of the sunlight on haze defining how much the sunlight affects the haze.
## 🔒︎ float EnvironmentHazePhysicalAmbientColorSaturation

The intensity of the ambient color's contribution to the haze (how much the sunlight affects the haze).
## 🔒︎ float EnvironmentHazePhysicalAmbientLightIntensity

The intensity of the impact of the ambient lighting on haze (how much the ambient lighting affects the haze).
## 🔒︎ float EnvironmentHazePhysicalHalfFalloffHeight

The height of the haze density gradient. The *higher* the value, the *longer* the haze desity reduces as the height grows, making the transition between the clear sky and haze smoother.
## 🔒︎ float EnvironmentHazePhysicalHalfVisibilityDistance

The distance to the boundary at which the visibility comprises 50%. There is no zero-visibility in the real world, so the half-visibility boundary is used to adjust haze distance.
## 🔒︎ float EnvironmentHazePhysicalStartHeight

The reference height value for the two parameters ([Half Visibility Distance](#getEnvironmentHazePhysicalHalfVisibilityDistance_float) and [Half Faloff Height](#getEnvironmentHazePhysicalHalfFalloffHeight_float)). To get the current reference height value for the specific preset, use *[RenderEnvironmentPreset::getHazePhysicalStartHeight()](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazePhysicalStartHeight_float)*.
```cpp
// get a reference height value for the preset that overlays the others
Render::getEnvironmentHazePhysicalStartHeight();
// get a reference height value for the second environment preset
RenderEnvironmentPresetPtr preset = Render::getEnvironmentPreset(1);
preset->getHazePhysicalStartHeight();

```

 reference height value for the two parameters ([Half Visibility Distance](#getEnvironmentHazePhysicalHalfVisibilityDistance_float) and [Half Faloff Height](#getEnvironmentHazePhysicalHalfFalloffHeight_float)). To get the current reference height value for the specific preset, use *[RenderEnvironmentPreset.GetHazePhysicalStartHeight()](../../../api/library/rendering/class.renderenvironmentpreset_cs.md#getHazePhysicalStartHeight_float)*.
```csharp
// get a haze reference height value for the preset that overlays the others
Render.GetEnvironmentHazePhysicalStartHeight();
// get a reference height value for the second environment preset
RenderEnvironmentPreset preset = Render.GetEnvironmentPreset(1);
preset.GetHazePhysicalStartHeight();

```


## float TessellationDensityMultiplier

***Console*:**`render_tessellation_density_multiplier`The global [Density](../../../content/materials/library/mesh_base/index.md#tessellation_density) multiplier for the adaptive hardware-accelerated tessellation. *Higher* values produce *denser* meshes.
Range of values: **[0.0f, 10.0f]**. The default value is : **1.0f**.
## float TessellationShadowDensityMultiplier

***Console*:**`render_tessellation_shadow_density_multiplier`The global [Shadow Density](../../../content/materials/library/mesh_base/index.md#tessellation_density_shadow) multiplier for the Tessellated Displacement effect. *Higher* values produce more detailed shadows. You can make shadows from tessellated meshes simpler to save performance.
Range of values: **[0.01f, 10.0f]**. The default value is : **1.0f**.
## float TessellationDistanceMultiplier

***Console*:**`render_tessellation_distance_multiplier`The global multiplier for all [distance](../../../content/materials/library/mesh_base/index.md#tessellation_distance_falloff_near) parameters of the adaptive hardware-accelerated tessellation used for distance-dependent optimization. *Higher* values make tessellation visible at longer distances from the camera (consuming more resources).
Range of values: **[0.0f, 10.0f]**. The default value is : **1.0f**.
## vec4 LightmapColor

***Console*:**`render_lightmap_color`The color multiplier for lightmaps.
> **Notice:** Some light sources may be modified after the lightmap was baked. To make lighting in the scene consistent once again without any re-baking you can simply adjust the color multiplier for lightmaps. See the [How-To video tutorial](../../../videotutorials/how_to/how_to_rendering/lightmap_color.md) for additional information.

**vec4_one** - default value (white)
## float SSRViewBias

***Console*:**`render_ssr_view_bias`The bias value to which the ray starting position has been shifted along the view vector. This value is used for SSR (Screen-Space Reflections) calculation. Can be adjusted to fine-tune reflections of small objects at far distances. Recommended for narrow FOV angles. To use this option, SSR*[SSR](../../...md#render_ssr)* should be enabled.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SSRNormalBias

***Console*:**`render_ssr_normal_bias`The bias value to which the ray starting position has been shifted along the normal vector. This value is used for SSR (Screen-Space Reflections) calculation. Can be adjusted to fine-tune reflections of small objects at far distances. Recommended for narrow FOV angles. To use this option, SSR*[SSR](../../...md#render_ssr)* should be enabled.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRPreset](/api/library/rendering/class.render_cs#render_ssr_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## int SSGIIntensityBoost

***Console*:**`render_ssgi_intensity_boost`The boost intensity value. Increases the SSGI intensity by raising the value to the specified power. One of the following values:
- **0** - power of 1 (by default)
- **1** - power of 2
- **2** - power of 3
- **3** - power of 4

> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[SSRTGIPreset](/api/library/rendering/class.render_cs#render_ssrtgi_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float SRAADepthThreshold

***Console*:**`render_sraa_depth_threshold`The depth threshold value used for edges detection that specifies the area for the SRAA processing. Turn on the debug mode and adjust this parameter in such a way that covers the required edges but at the same time leaves out the unnecessary geometry in the scene.
Range of values: **[0.0f, inf]**. The default value is : **0.1f**.
## bool SRAADebug

***Console*:**`render_sraa_debug`The value indicating if the SRAA debug mode is enabled. This mode shows the geometry edges smoothed by the SRAA. The default value is **false**.
## bool SRAATemporal

***Console*:**`render_sraa_temporal`The value indicating if TAA integration is enabled. SRAA will use the shading sample from the previously rendered frame (TAA) to achieve correct anti-aliasing. Uses camera jittering, so it works only when the TAA*[TAA](../../...md#render_taa)* is enabled. It is recommended to use this option by default. The default value is **true**.
## int SRAASamples

***Console*:**`render_sraa_samples`The number of depth geometry samples per pixel. This value may significantly affect performance, so keep it low when the image quality differences are not apparent. One of the following values:
- **0** - 2
- **1** - 4 (by default)
- **2** - 8

## bool SRAA

***Console*:**`render_sraa`The value indicating if [Subpixel Reconstruction Anti-Aliasing (SRAA)](../../../principles/render/antialiasing/sraa.md) is enabled. The default value is **false**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[AAPreset](/api/library/rendering/class.render_cs#render_aa_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float PanoramaFisheyeFov

***Console*:**`render_panorama_fisheye_fov`The Field of View (in degrees) for the panoramic viewport mode selected at the moment.
> **Notice:** Available only when the viewport rendering mode*[ViewportMode](../../...md#render_viewport_mode)* is set to one of the fisheye panorama modes (5-8).

Range of values: **[0, 360]**. The default value is : **0**.
## bool ShadowsWorldCascadesCullingClusters

***Console*:**`render_shadows_world_cascades_culling_clusters`The value indicating whether culling of shadow cascades is enabled for *Mesh Cluster/Clutter* objects. If enabled, the *Mesh Cluster/Clutter* objects rendered in the nearest cascade won't be rendered again in farther cascades. If disabled, the *Mesh Cluster* objects rendered in the nearest cascade will also be rendered in all other cascades. In some cases performance may be better if this option is disabled. The default value is **false**.
## bool ReflectionDynamicAlphaFade

***Console*:**`render_reflection_dynamic_alpha_fade`The value indicating if [alpha-blend fading](../../../principles/world_management/index.md#fading) (dithering) is enabled for surfaces inside the dynamic reflections when switching between LODs. This feature may be disabled to save performance, but in this case surfaces rendered in dynamic reflections will pop in and pop out. The default value is **false**.
## bool ReflectionDynamicRoughnessOffset

***Console*:**`render_reflection_dynamic_roughness_offset`The value indicating whether roughness offset is enabled for dynamic reflections produced by *Environment Probes*. Sometimes, when specular highlights from glossy surfaces get into dynamic *Environment Probes* a very bright flickering of lighting from it may appear. This option makes surrounding materials look more matte for an *Environment Probe* than they actually are, reducing such flickering artefacts. The default value is **false**.
## int Clouds3dTextureVerticalResolution

***Console*:**`render_clouds_3d_texture_vertical_resolution`The vertical resolution for the 3D texture to be used for clouds rendering.
> **Notice:** Setting too high resolution may significantly affect performance, so adjust it wisely.

 One of the following values:
- **0** - 32
- **1** - 64
- **2** - 128
- **3** - 256 (by default)
- **4** - 512

## int Clouds3dTextureHorizontalResolution

***Console*:**`render_clouds_3d_texture_horizontal_resolution`The horizontal resolution for the 3D texture to be used for clouds rendering.
> **Notice:** Setting too high resolution may significantly affect performance, so adjust it wisely.

 One of the following values:
- **0** - 64
- **1** - 128
- **2** - 256 (by default)
- **3** - 512
- **4** - 1024
- **5** - 2048

## float CloudsLightingSamplesDistribution

***Console*:**`render_clouds_lighting_samples_distribution`The value that controls distribution of samples for clouds lighting. Can be used to keep small details for long shadows when the lighting trace length value*[CloudsLightingTraceLength](../../...md#render_clouds_lighting_tracelength)* is high.
Range of values: **[0.001f, 5.0f]**. The default value is : **1.0f**.
## int CloudsTransparentOrder

***Console*:**`render_clouds_transparent_order`The rendering order for clouds relative to transparent objects (except water).
- **Render Before Transparent** - render clouds before all [transparent objects](../../../principles/render/sequence/index.md#transparent) (except water).
- **Render After Transparent** - render clouds after all [transparent objects](../../../principles/render/sequence/index.md#transparent) (except water).
- **Sort Transparent** - enable rough sorting for [transparent objects](../../../principles/render/sequence/index.md#transparent) relative to clouds (*below the lowest cloud layer base -> inside the clouds -> above the highest cloud layer top*).

  One of the following values:
- **0** - Render Before Transparent (by default)
- **1** - Render After Transparent
- **2** - Sort Transparent

## 🔒︎ int CloudsQualityPresetNumNames

The number of clouds quality presets.
## int CloudsQualityPreset

***Console*:**`render_clouds_quality_preset`The index of the clouds quality preset used at the moment.
```csharp
// enabling the Custom preset (the last one) to customize clouds options at run time
Render.CloudsQualityPreset = Render.CloudsQualityPresetNumNames - 1;

// disabling depth-based reconstruction for clouds
Render.CloudsDepthBasedReconstruction = false;

```

  One of the following values:
- **0** - Low (by default)
- **1** - Medium
- **2** - High + Interleaved
- **3** - High
- **4** - Ultra + Interleaved
- **5** - Ultra
- **6** - Extreme + Interleaved
- **7** - Extreme
- **8** - Custom

## int LandscapeOperationsPerFrame

***Console*:**`render_landscape_operations_per_frame`The maximum number of Landscape texture draw operations (*[asyncTextureDraw](../../../api/library/objects/landscape_terrain/class.landscape_cs.md#asyncTextureDraw_int_UGUID_ivec2_ivec2_int_VECWorldBoundBox_void)*) that can be performed per frame.
Range of values: **[1, 1000]**. The default value is : **10**.
## 🔒︎ int LandscapeTerrainStreamingPresetNumNames

The number of Landscape Terrain streaming presets.
## int LandscapeTerrainStreamingPreset

***Console*:**`render_landscape_terrain_streaming_preset`The index of the Landscape Terrain streaming preset used at the moment.
> **Notice:** Presets override user-defined custom settings. When any preset other than Custom is active, modification of the parameters via [API](../../../api/library/rendering/class.render_cs.md) has no effect. The parameter value set via the last API call shall be used only when the Custom preset is active. When checking the current parameter value via API you'll get the corresponding setting stored in the active preset (default or custom one).


```csharp
// enabling the Custom preset (the last one) to customize Landscape Terrain streaming options at run time
Render.LandscapeTerrainStreamingPreset = Render.LandscapeTerrainStreamingPresetNumNames - 1;

// setting the number of tiles passed to the virtual texture per frame
Render.LandscapeTerrainVTTilesUpdatePerFrame = 64;

```

  One of the following values:
- **0** - Low (by default)
- **1** - Medium
- **2** - High
- **3** - Ultra
- **4** - Extreme
- **5** - Custom

## 🔒︎ int LandscapeTerrainGeometryPresetNumNames

The number of Landscape Terrain geometry presets.
## int LandscapeTerrainGeometryPreset

***Console*:**`render_landscape_terrain_geometry_preset`The index of the Landscape Terrain geometry preset used at the moment.
> **Notice:** Presets override user-defined custom settings. When any preset other than Custom is active, modification of the parameters via [API](../../../api/library/rendering/class.render_cs.md) has no effect. The parameter value set via the last API call shall be used only when the Custom preset is active. When checking the current parameter value via API you'll get the corresponding setting stored in the active preset (default or custom one).


```csharp
// enabling the Custom preset (the last one) to customize Landscape Terrain geometry options at run time
Render.LandscapeTerrainGeometryPreset = Render.LandscapeTerrainGeometryPresetNumNames - 1;

// setting the size of the Landscape Terrain polygons
Render.LandscapeTerrainGeometryPolygonSize = 100.0f;

```

  One of the following values:
- **0** - Low (by default)
- **1** - Medium
- **2** - High
- **3** - Ultra
- **4** - Extreme
- **5** - Custom

## 🔒︎ int WaterGeometryPresetNumNames

The number of Global Water geometry presets.
## int WaterGeometryPreset

***Console*:**`render_water_geometry_preset`The index of the Global Water geometry preset used at the moment. To customize the Global Water geometry preset options at run time you should activate the **Custom** preset:
```csharp
// enabling the Custom preset (the last one) to customize the Global Water options at run time
Render.WaterGeometryPreset = Render.WaterGeometryPresetNumNames - 1;

// setting the size of the Global Water polygons
Render.WaterGeometryPolygonSize = 100.0f;

```

  One of the following values:
- **0** - Low (by default)
- **1** - Medium
- **2** - High
- **3** - Ultra
- **4** - Extreme
- **5** - Custom

## 🔒︎ int DOFPresetNumNames

The number of DoF presets.
## int DOFPreset

***Console*:**`render_dof_preset`The DoF effect quality preset. To customize the DoF effect options at run time you should activate the **Custom** preset:
```csharp
// enabling the Custom preset (the last one) to customize the DoF effect options at run time
Render.DOFPreset = Render.DOFPresetNumNames - 1;

// disabling the increased accuracy
Render.DOFIncreasedAccuracy = false;

```

  One of the following values:
- **0** - Very Low (by default)
- **1** - Low
- **2** - Medium
- **3** - High
- **4** - Ultra
- **5** - Extreme
- **6** - Custom

## 🔒︎ int MotionBlurPresetNumNames

The number of Motion Blur presets.
## int MotionBlurPreset

***Console*:**`render_motion_blur_preset`The Motion Blur preset. To customize the Motion Blur effect options at run time you should activate the **Custom** preset:
```csharp
// enabling the Custom preset (the last one) to customize the Motion Blur effect options at run time
Render.MotionBlurPreset = Render.MotionBlurPresetNumNames - 1;

// disabling the neat silhouettes option
Render.MotionBlurNeatSilhouettes = false;

```

  One of the following values:
- **0** - Low (by default)
- **1** - Medium
- **2** - High
- **3** - Ultra
- **4** - Custom

## 🔒︎ int SSRPresetNumNames

The number of SSR (Screen-Space Reflections) presets.
## int SSRPreset

***Console*:**`render_ssr_preset`The SSR (Screen-Space Reflections) preset used at the moment. To customize the SSR effect options at run time you should activate the **Custom** preset:
```csharp
// enabling the Custom preset (the last one) to customize the SSR effect options at run time
Render.SSRPreset = Render.SSRPresetNumNames - 1;

// disabling the increased accuracy option
Render.SSRIncreasedAccuracy = false;

```

  One of the following values:
- **0** - Low (by default)
- **1** - Medium
- **2** - High
- **3** - Ultra
- **4** - Extreme
- **5** - Custom

## 🔒︎ int SSRTGIPresetNumNames

The number of SSRTGI (Screen-Space Ray-Traced Global Illumination) presets.
## int SSRTGIPreset

***Console*:**`render_ssrtgi_preset`The index of the SSRTGI (Screen-Space Ray-Traced Global Illumination) preset used at the moment. To customize the SSRTGI effect options at run time you should activate the **Custom** preset:
```csharp
// enabling the Custom preset (the last one) to customize the SSRTGI effect options at run time
Render.SSRTGIPreset = Render.SSRTGIPresetNumNames - 1;

// disabling the increased accuracy option
Render.SSRTGIIncreasedAccuracy = false;

```

  One of the following values:
- **0** - Disabled (by default)
- **1** - Low
- **2** - Medium
- **3** - High
- **4** - Ultra
- **5** - Extreme
- **6** - Custom

## int RefractionWarpBackgroundTransparentSurfaces

***Console*:**`render_refraction_warp_background_transparent_surfaces`The value indicating if refraction affects background transparent surfaces (except for water and clouds). The following values are available:
- Never - no refraction distortion is applied to transparent surfaces.
- Behind Farthest Refractive Surface - apply refraction distortion to all transparent surfaces behind the farthest refractive surface.

 This method takes effect only when rendering of refractions*[Refraction](../../...md#render_refraction)* is enabled. One of the following values:
- **0** - Never (by default)
- **1** - Behind Farthest Refractive Surface

## 🔒︎ int AAPresetNumNames

The number of AA (Anti-Aliasing) presets.
## int AAPreset

***Console*:**`render_aa_preset`The index of the AA (Anti-Aliasing) preset used at the moment. To customize Anti-Aliasing options at run time you should activate the **Custom** preset:
```csharp
// enabling the Custom preset (the last one) to customize Anti-Aliasing options at run time
Render.AAPreset = Render.AAPresetNumNames - 1;

// disabling TAA
Render.TAA = false;

```

  One of the following values:
- **0** - Sharpest (by default)
- **1** - Sharp
- **2** - Smooth
- **3** - Smooth + SRAA
- **4** - Smoothest
- **5** - Smoothest + SRAA
- **6** - VR Mode
- **7** - Custom

## float ACESWithReinhardShoulderLength

***Console*:**`render_aces_with_reinhard_shoulder_length`The [shoulder length](../../../editor2/settings/render_settings/color/index.md#shoulder_length) parameter for the ACES with Reinhard operator. Controls the amount of f-stops to add to the dynamic range of the curve. Defines how much of the highlights the curve takes into account.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.14f**.
## float ACESWithReinhardShoulderStrength

***Console*:**`render_aces_with_reinhard_shoulder_strength`The [shoulder strength](../../../editor2/settings/render_settings/color/index.md#shoulder_length) parameter for the ACES with Reinhard operator. Controls the strength of the transition between the curve's midsection and the curve's shoulder.
Range of values: **[0.0f, 10.0f]**. The default value is : **0.59f**.
## float ACESWithReinhardShoulderAngle

***Console*:**`render_aces_with_reinhard_shoulder_angle`The [shoulder angle](../../../editor2/settings/render_settings/color/index.md#shoulder_angle) parameter for the ACES with Reinhard operator. Controls how much overshoot should be added to the curve's shoulder.
Range of values: **[0.0f, 10.0f]**. The default value is : **2.43f**.
## float ACESWithReinhardToe

***Console*:**`render_aces_with_reinhard_toe`The [toe](../../../editor2/settings/render_settings/color/index.md#toe) parameter for the ACES with Reinhard operator. Controls the dark color. Higher values result in darker colors.
Range of values: **[0.0f, 10.0f]**. The default value is : **0.03f**.
## float ACESWithReinhardWhiteClip

***Console*:**`render_aces_with_reinhard_white_clip`The [white clip](../../../editor2/settings/render_settings/color/index.md#white_clip) parameter for the ACES with Reinhard operator. Controls the cut-off point for white.ACES with Reinhard operator's white clip.
Range of values: **[0.0f, 10.0f]**. The default value is : **2.51f**.
## float ACESShoulderLength

***Console*:**`render_aces_shoulder_length`The [shoulder length](../../../editor2/settings/render_settings/color/index.md#shoulder_length) parameter for the ACES operator. Controls the amount of f-stops to add to the dynamic range of the curve. Defines how much of the highlights the curve takes into account.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.59f**.
## float ACESShoulderStrength

***Console*:**`render_aces_shoulder_strength`The [shoulder strength](../../../editor2/settings/render_settings/color/index.md#shoulder_length) parameter for the ACES operator. Controls the strength of the transition between the curve's midsection and the curve's shoulder.
Range of values: **[0.0f, 10.0f]**. The default value is : **0.59f**.
## float ACESShoulderAngle

***Console*:**`render_aces_shoulder_angle`The [shoulder angle](../../../editor2/settings/render_settings/color/index.md#shoulder_angle) parameter for the ACES operator. Controls how much overshoot should be added to the curve's shoulder.
Range of values: **[0.0f, 10.0f]**. The default value is : **2.43f**.
## float ACESToe

***Console*:**`render_aces_toe`The [toe](../../../editor2/settings/render_settings/color/index.md#toe) parameter for the ACES operator. Controls the dark color. Higher values result in darker colors.
Range of values: **[0.0f, 10.0f]**. The default value is : **0.03f**.
## float ACESWhiteClip

***Console*:**`render_aces_white_clip`The [white clip](../../../editor2/settings/render_settings/color/index.md#white_clip) parameter for the ACES operator. Controls the cut-off point for white.
Range of values: **[0.0f, 10.0f]**. The default value is : **2.51f**.
## float ACESWithReinhardMix

***Console*:**`render_aces_with_reinhard_mix`The [ACES with Reinhard tonemapping](../../../editor2/settings/render_settings/color/index.md#mix_with_reinhard) operator contribution. If the value is closer to **0**, then ACES prevails. Otherwise, when the value is closer to **1**, the Reinhard has a grater impact.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**.
## float ReinhardLumaBasedContribution

***Console*:**`render_reinhard_luma_based_contribution`The [Reinhard Luma-Based tonemapping](../../../editor2/settings/render_settings/color/index.md#contribution_l) operator contribution. Controls the overall contribution that the Reinhard operator makes to the final color grading of the image. Higher values result in more tonemapping contribution to the final image.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
## float ReinhardContribution

***Console*:**`render_reinhard_contribution`The [Reinhard tonemapping](../../../editor2/settings/render_settings/color/index.md#contribution_r) operator contribution.
The value is calculated according to the following formula: **C / (1 + C)** It controls the overall contribution that the Reinhard operator makes to the final color grading of the image. The higher values result in more tonemapping contribution to the final image.

Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
## bool Tonemapper

***Console*:**`render_tonemapper`The value indicating if [tone mapping](../../../editor2/settings/render_settings/color/index.md#tonemapper) is enabled. The default value is **true**.
## Render.TONEMAPPER TonemapperMode

***Console*:**`render_tonemapper_mode`The mode of [tone mapping](../../../editor2/settings/render_settings/color/index.md#tonemapper). One of the following values:
- **0** - Filmic
- **1** - ACES (by default)
- **2** - ACES with Reinhard
- **3** - Reinhard
- **4** - Reinhard Luma-Based

## int WaterWaterlineAccuracy

***Console*:**`render_water_waterline_accuracy`The quality of underwater and waterline determination. Use high quality only if you need to submerge underwater (to see the waterline) and at medium and high Beaufort values. One of the following values:

- *Low* - low quality (by default)
- *Medium* - medium quality
- *High* - high quality
- *Ultra* - ultra quality

## float WaterCullingObliqueFrustum

***Console*:**`render_water_culling_oblique_frustum`The multiplier for the size of viewing frustum used for culling polygons of *[Global Water](../../../objects/objects/water/water_object.md)* object beyond the oblique frustum plane. The higher the value, the more patches will be culled.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.9f**.
## float WaterCullingFrustumPadding

***Console*:**`render_water_culling_frustum_padding`The value, by which the borders of the current frustum are increased. Frustum culling is performed for the frustum of the increased size. By the maximum value of 1, the frustum borders will be increased by the size of the current frustum.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.1f**.
## bool WaterCullingAggressive

***Console*:**`render_water_culling_aggressive`The value indicating if frustum culling optimization is enabled for the [Global Water](../../../objects/objects/water/water_object.md). When enabled, the number of culled polygons increases thereby increasing performance. In case of any issues with polygons rendering, try disabling this option (however, note that performance may drop). The default value is **true**.
## float WaterGeometrySubpixelReduction

***Console*:**`render_water_geometry_subpixel_reduction`The minimum ratio of a polygon size (in screen space) to the size of an area seen in the viewport. If the ratio calculated for the polygon is less than this value, such polygon will be removed.
Range of values: **[0.0f, 50.0f]**. The default value is : **6.0f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[WaterGeometryPreset](/api/library/rendering/class.render_cs#render_water_geometry_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float WaterGeometryFadeLods

***Console*:**`render_water_geometry_fade_lods`The intensity of fading between levels of [Global Water](../../../objects/objects/water/water_object.md) geometry tessellation. This value can be increased to remove sharp edges between areas with different geometry density.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[WaterGeometryPreset](/api/library/rendering/class.render_cs#render_water_geometry_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float WaterGeometryProgression

***Console*:**`render_water_geometry_progression`The progression of [Global Water](../../../objects/objects/water/water_object.md) geometry tessellation.
Range of values: **[0.0f, 50.0f]**. The default value is : **1.5f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[WaterGeometryPreset](/api/library/rendering/class.render_cs#render_water_geometry_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float WaterGeometryPolygonSize

***Console*:**`render_water_geometry_polygon_size`The size of [Global Water](../../../objects/objects/water/water_object.md) polygons. The value defines the maximum allowed density of Global Water geometry. If the polygon size is large, small waves will be lost. It is better to set this parameter to about 1/3 or 1/4 of the smallest wavelength.
Range of values: **[0.0f, 1000.0f]**. The default value is : **0.01f**.
> **Notice:** Setting the value via  API changes only the setting stored in the **Custom** preset, and will take effect only when this preset is active (change active preset via *[WaterGeometryPreset](/api/library/rendering/class.render_cs#render_water_geometry_preset)*). Checking the parameter returns the corresponding setting stored in the active preset (default or custom one).

## float WaterVisibleDistance

***Console*:**`render_water_visible_distance`The maximum visibility distance for the [Global Water](../../../objects/objects/water/water_object.md). The water is visible, as long as the distance between the camera and the water object does not exceed this value.
Range of values: **[0.0f, inf]**. The default value is : **30000.0f**.
## float DistanceOffset

***Console*:**`render_distance_offset`The global distance offset for all distance parameters: shadow distance, light distance, LOD distances, etc.
Range of values: **[0.0f, inf]**. The default value is : **0.0f**.
## bool EnvironmentHemisphere

***Console*:**`render_environment_hemisphere`The value indicating if rendering of environment only for the top (above-ground) hemisphere is enabled. The underground is rendered black. When disabled, environment for the whole sphere is rendered. The default value is **false**.
## bool WaterPlanarProbes

***Console*:**`render_water_planar_probes`The value indicating if rendering of [Planar Reflection Probes](../../../objects/lights/planar/index.md) on the water surface is enabled. The default value is **true**.
## 🔒︎ int NumDebugMaterials

The number of debug materials.
## bool ColorCorrectionHuePerColor

***Console*:**`color_correction_hue_per_color`The value indicating if fine-adjustment of hue (color shift) for each of the 12 major colors of the spectre is enabled. The default value is **true**.
## bool ColorCorrectionSaturationPerColor

***Console*:**`color_correction_saturation_per_color`The value indicating if fine-adjustment of saturation for each of the 12 major colors of the spectre is enabled. The default value is **true**.
## bool ColorCorrectionByCurves

***Console*:**`color_correction_by_curves`The value indicating if color correction via curves is enabled. The default value is **true**.
## bool VignetteMask

***Console*:**`render_vignette_mask`The value indicating if rendering of the *[Vignette Mask](../../../editor2/settings/render_settings/camera_effects/index.md#post_vignette)* post-effect is enabled. The effect applies darkening towards the edges of an image compared to the center usually caused by thick or stacked filters, secondary lenses, and lens hoods. It can be used for an artistic effect, to draw focus to the center of the image. The default value is **false**.
## float VignetteMaskIntensity

***Console*:**`render_vignette_mask_intensity`The intensity of the *[Vignette Mask](../../../editor2/settings/render_settings/camera_effects/index.md#post_vignette)*. Defines the amount of vignetting on the screen: *higher* values moke the vignette wider.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
## float VignetteMaskPower

***Console*:**`render_vignette_mask_power`The Power value that controls mask opacity for the *[Vignette Mask](../../../editor2/settings/render_settings/camera_effects/index.md#post_vignette)* post-effect.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## string VignetteMaskTexturePath

The path to the custom mask texture for the *[Vignette Mask](../../../editor2/settings/render_settings/camera_effects/index.md#post_vignette)* post-effect.
## bool Noise

***Console*:**`render_noise`The value indicating if rendering of the *[Noise](../../../editor2/settings/render_settings/camera_effects/index.md#post_noise)* post-effect is enabled. The default value is **false**.
## float NoiseIntensity

***Console*:**`render_noise_intensity`The intensity of the *[Noise](../../../editor2/settings/render_settings/camera_effects/index.md#post_noise)* post-effect. *Higher* values result in more noise applied to the image.
Range of values: **[0.0f, inf]**. The default value is : **0.03f**.
## bool ChromaticAberration

***Console*:**`render_chromatic_aberration`The value indicating if rendering of the *[Chromatic Aberration](../../../editor2/settings/render_settings/camera_effects/index.md#post_chromatic_aberration)* post-effect is enabled. This effect simulates color shifts in real-world camera lenses due to light rays entering a lens at different points causing separation of RGB colors. The default value is **false**.
## float ChromaticAberrationIntensity

***Console*:**`render_chromatic_aberration_intensity`The intensity (strength) of the *[Chromatic Aberration](../../../editor2/settings/render_settings/camera_effects/index.md#post_chromatic_aberration)* post-effect. Controls how much color shifting occurs.
Range of values: **[0.0f, inf]**. The default value is : **0.5f**.
## float ChromaticAberrationNoiseIntensity

***Console*:**`render_chromatic_aberration_noise_intensity`The intensity of noise applied for the *[Chromatic Aberration](../../../editor2/settings/render_settings/camera_effects/index.md#post_chromatic_aberration)* post-effect.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**.
## int ChromaticAberrationSamples

***Console*:**`render_chromatic_aberration_samples`The number of samples used for calculation of the *[Chromatic Aberration](../../../editor2/settings/render_settings/camera_effects/index.md#post_chromatic_aberration)* post-effect. *Higher* values reduce banding making the effect look smoother.
Range of values: **[1, 32]**. The default value is : **1**.
## float LandscapeTerrainCullingMap

***Console*:**`render_landscape_terrain_culling_map`The  extent of culling of [Landscape Layer Maps](../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md) with the distance. In case small Landscape Layer Maps disappear too soon with the distance, try increasing this value.
> **Notice:** [Reloads Landscape Terrain graphic data](../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe).


Range of values: **[0.0f, 1.0f]**. The default value is : **0.3f**.
## float LandscapeTerrainCullingObliqueFrustum

***Console*:**`render_landscape_terrain_culling_oblique_frustum`The multiplier for culling of tessellation patches of the [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md) beyond the oblique frustum plane. *Higher* values result in more patches culled.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.9f**.
## float LandscapeTerrainCullingPaddingPatchCPU

***Console*:**`render_landscape_terrain_culling_padding_patch_cpu`The  padding between LODs of patches culled on CPU.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float LandscapeTerrainCullingPaddingPatchGPU

***Console*:**`render_landscape_terrain_culling_padding_patch_gpu`The  padding between LODs of patches culled on GPU.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## float LandscapeTerrainCullingPaddingTriangles

***Console*:**`render_landscape_terrain_culling_padding_triangles`The  padding between LODs of tessellated polygons.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## int LandscapeTerrainCullingPatchBatching

***Console*:**`render_landscape_terrain_culling_patch_batching`The  number of culling patches of [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md) processed in a batch. The higher this value, the more patches will be checked for visibility on CPU at once.
Range of values: **[1, 64]**. The default value is : **16**.
## int LandscapeTerrainCullingPatchResolutionCPU

***Console*:**`render_landscape_terrain_culling_patch_resolution_cpu`The  number of subdivisions for patches of [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md) culled on the CPU side that are to be passed to GPU. The lowest value of 2 corresponds to no subdivisions at all, i.e. all patched will be culled on the CPU side. By increasing this value you can reduce the load on CPU as more patches will be checked for visibility on the GPU side.
Range of values: **[2, 64]**. The default value is : **2**.
## int LandscapeTerrainCullingPatchResolutionGPU

***Console*:**`render_landscape_terrain_culling_patch_resolution_gpu`The  number of subdivisions for patches of [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md) culled on the GPU side that are to be tessellated. By lowering this value you reduce the load on CPU, by increasing it you reduce the load on GPU. The point is to find a trade-off between loads in the given conditions on the target hardware.
Range of values: **[4, 64]**. The default value is : **32**.
## int LandscapeTerrainCullingDepthResolution

***Console*:**`render_landscape_terrain_culling_depth_resolution`The  resolution of the buffer used for culling by depth.
Range of values: **[4, 2048]**. The default value is : **64**.
## bool LandscapeTerrainCullingByDepth

***Console*:**`render_landscape_terrain_culling_by_depth`The  value indicating if culling by depth is enabled. Keep this option enabled to get the performance higher due to culling of tiles occluded by geometry and Landscape Terrain itself.  The default value is **true**.
## bool LandscapeTerrainCullingFrustumAggressive

***Console*:**`render_landscape_terrain_culling_frustum_aggressive`The value indicating if frustum culling optimization is enabled for the [Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md). When enabled, the number of culled polygons increases thereby increasing performance. In case of any issues with polygons rendering, try disabling this option (however, note that performance may drop). The default value is **true**.
## float LandscapeTerrainGeometryDetailMaxHeight

***Console*:**`render_landscape_terrain_geometry_detail_max_height`The maximum height for detail displacement clamping. Adjust this value to the highest height value used in details in case of artifacts of stepped geometry caused by insufficient bit depth.
> **Notice:** [Reloads Landscape Terrain graphic data](../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe).


Range of values: **[0.0f, 10.0f]**. The default value is : **0.5f**.
## int LandscapeTerrainDetailCompression

***Console*:**`render_landscape_terrain_detail_compression`The mode of detail textures compression. Compressed detail textures take less video memory.  One of the following values:
- **0** - Disabled
- **1** - Fast Compression (by default)
- **2** - High Quality

## bool LandscapeTerrainStreamingPerLods

***Console*:**`render_landscape_terrain_streaming_per_lods`The value indicating if streaming per LODs (MIP maps) is enabled. Disable this option to make streaming faster by skipping loading of intermediate MIP-levels for textures.  The default value is **true**.
## int LandscapeTerrainStreamingThreads

***Console*:**`render_landscape_terrain_streaming_threads`The  number of threads used for streaming.
Range of values: **[0, 32]**. The default value is : **1**.
## vec2 LandscapeTerrainVTSamplerFeedbackBufferResolution

***Console*:**`render_landscape_terrain_vt_sampler_feedback_buffer_resolution`The resolution of the buffer used to transfer data about tiles and what MIP-levels to be loaded.
> **Notice:** [Reloads Landscape Terrain graphic data](../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe).


From **1x1** to **1024x1024** Default: **80x60**
## int LandscapeTerrainVTSamplerFeedbackScreenResolution

***Console*:**`render_landscape_terrain_vt_sampler_feedback_screen_resolution`The resolution of the screen buffer used to detect visible tiles and what MIP-levels to be loaded.
> **Notice:** [Reloads Landscape Terrain graphic data](../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe).

  One of the following values:
- **0** - Quarter
- **1** - Half (by default)
- **2** - Full

## int LandscapeTerrainVTHashSize

***Console*:**`render_landscape_terrain_vt_hash_size`The upper limit for the hash function used to determine tiles of *Landscape Terrain*. The value must be high enough to cover all variety of world-space positions of tiles being used and streamed.
> **Notice:** [Reloads Landscape Terrain graphic data](../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe).


Range of values: **[1000, 5000000]**. The default value is : **1000000**.
## int LandscapeTerrainVTHashSizeNumberMistakes

***Console*:**`render_landscape_terrain_vt_hash_number_mistakes`The number of mistakes of the hash function used in *Landscape Terrain* data streaming. This value actually represents the number of iterations to compute a new unique hash value that determines a tile being streamed. Too low values may introduce collisions and, therefore, wrong terrain data at certain areas.
> **Notice:** [Reloads Landscape Terrain graphic data](../../../objects/objects/terrain/landscape_terrain/settings.md#runtime_safe).


Range of values: **[1, 32]**. The default value is : **2**.
## bool LocalTonemapper

***Console*:**`render_local_tonemapper`The value indicating if the local tonemapper is enabled. The default value is **false**.
## int LocalTonemapperNumBlurIterations

***Console*:**`render_local_tonemapper_num_blur_iterations`The number of blur iterations applied to the screen texture, which is used to define bright and dark portions of the screen. A higher number of iterations increases the blur radius and reduces halo artifacts around objects, but may affect performance.
Range of values: **[0, 10]**. The default value is : **5**.
## float LocalTonemapperDepthThreshold

***Console*:**`render_local_tonemapper_depth_threshold`The depth threshold value used to detect the areas affected by local tonemapping. A properly set value may help to reduce halo artifacts.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.9f**.
## float LocalTonemapperTonemappingIntensity

***Console*:**`render_local_tonemapper_tonemapping_intensity`The intensity of the local tonemapping effect.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**.
## float LocalTonemapperEffectOnDarkAreas

***Console*:**`render_local_tonemapper_effect_on_dark_areas`The extent of applying the local tonemapping effect on dark areas.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.1f**.
## float LocalTonemapperTargetMiddleGray

***Console*:**`render_local_tonemapper_target_middle_gray`The target middle gray value for tonemapping.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.4f**.
## float LocalTonemapperLumaBlurredIntensity

***Console*:**`render_local_tonemapper_luma_blurred_intensity`The intensity of blurring the luma values. It is recommended to keep the default value for this setting. With the value set to 0, a regular screen texture is used instead of a blurred screen texture. This might be required in a rare case of reducing the halo effect and increasing the tonemapping effect for small details.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
## 🔒︎ TextureRamp AutoExposureRamp

The correction curve for the overall scene saturation. The input luminance values are mapped to the vertical saturation values. Higher values make colors more saturated and vibrant, lower values make colors duller and less saturated.
## Render.RENDER_UPSCALE_MODE UpscaleMode

***Console*:**`render_upscale_mode`The Upscaling mode. Defines a technology to be used to render high-resolution images based on the lower resolution source, which may help preserve image quality while getting more fps. One of the following values:
- **0** - *Disabled* for no upscaling. 1.0x per dimension, the final image has 100% rendered resolution.
- **1** - *FSR* for Fidelity FX Super Resolution by AMD.
- **2** - *DLSS* for Deep Learning Super Sampling by NVIDIA. (by default)

## bool UpscaleFixFlicker

***Console*:**`render_upscale_fix_flicker`The value indicating whether a temporal filtering pass is applied when upscaling is active to reduce pixel flicker on bright thin details such as wires and lines. May increase rendering costs. The default value is **false**.
## Render.RENDER_DLSS_MODE DLSSMode

***Console*:**`render_upscale_dlss_mode`The DLSS quality.
- *Ultra Performance* provides the highest performance boost by rendering at ~33.3% of the target resolution and upscaling to the output resolution. This mode is recommended only for 8K output resolution due to the significant reduction in internal image quality.
- *Max Performance* provides a higher performance boost than *Balanced* by rendering at ~50% of the target resolution. Use when frame-rate is prioritized but some internal detail should be preserved. It is recommended for users with 1440p/2K monitors, providing better performance with minimal effort.
- *Balanced* offers both optimized performance and image quality by rendering at approximately ~58% of the target resolution. Recommended as the general-purpose preset for users who want a compromise between frame-rate and visual fidelity.
- *Max Quality* offers higher image quality than *Balanced* by rendering at approximately ~66.7% of the target resolution. Prioritizes visual fidelity while still delivering a meaningful performance improvement over native rendering.
- *DLAA* (**Deep Learning Anti-Aliasing**) is an AI-powered tool to eliminate jagged edges in video apps, by rendering at native (100%) resolution. It improves image quality with less performance cost than traditional anti-aliasing methods.

  One of the following values:
- **0** - Ultra Performance
- **1** - Max Performance
- **2** - Balanced
- **3** - Max Quality (by default)
- **4** - DLAA (Deep Learning Anti-Aliasing).

## float FSRCustomResolutionScale

***Console*:**`render_upscale_fsr_custom_resolution_scale`The custom resolution scale used when [FSRMode](#FSRMode) is set to *Custom*. The value directly multiplies the output resolution to determine the internal render resolution.
Range of values: **[0.1f, 1.0f]**. The default value is : **0.5f**.
## bool DLSSResolutionScaleEnabled

***Console*:**`render_upscale_dlss_resolution_scale_enabled`The value indicating whether a custom resolution scale is used instead of the default render resolution provided by DLSS for the current [DLSSMode](#DLSSMode). When enabled, the render resolution is adjusted within the allowed range for the current mode using the [DLSSResolutionScaleValue](#DLSSResolutionScaleValue). The default value is **false**.
## float DLSSResolutionScaleValue

***Console*:**`render_upscale_dlss_resolution_scale_value`The custom resolution scale for DLSS within the allowed range for the current [DLSSMode](#DLSSMode) and output resolution, where 0.0 is the minimum and 1.0 is the maximum render resolution. [DLSSResolutionScaleEnabled](#DLSSResolutionScaleEnabled) must be enabled for this value to take effect.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**.
## Render.RENDER_DLSS_PRESET DLSSPreset

***Console*:**`render_upscale_dlss_preset`The DLSS preset.
- *A* - Legacy preset designed to mitigate ghosting artifacts, particularly in cases where input data (e.g., motion vectors) may be missing. **Intended modes:** Performance, Balanced, Quality
- *B* - Variant of Preset A, optimized specifically for Ultra Performance mode. **Intended modes:** Ultra Performance
- *C* - Prefers current-frame information, making it well-suited for fast-paced, high-motion content. **Intended modes:** Performance, Balanced, Quality
- *D* - Functionally similar to Preset E but less commonly recommended. Preset E is preferred in most cases. **Intended modes:** Performance, Balanced, Quality
- *E* - General-purpose preset prioritizing both performance and image stability. **Intended modes:** Performance, Balanced, Quality
- *F* - Default preset for Ultra Performance and DLAA modes. Provides stable results across these configurations. **Intended modes:** Ultra Performance, DLAA
- *G* is unused. Reverts to default preset behavior.
- *H* is unused. Reverts to default preset behavior.
- *I* is unused. Reverts to default preset behavior.
- *J* - Transformer-based model similar to Preset K. May exhibit slightly less ghosting, but at the cost of additional flickering. Generally superseded by Preset K. **Intended modes:** DLAA, Performance, Balanced, Quality
- *K* - Default transformer-based preset delivering the highest image quality. Reduces ghosting and shimmering compared to other presets, though at a higher performance cost. Recommended over Preset J. **Intended modes:** DLAA, Performance, Balanced, Quality

  One of the following values:
- **0** - Default (by default)
- **1** - Preset A
- **2** - Preset B
- **3** - Preset C
- **4** - Preset D
- **5** - Preset E
- **6** - Preset F
- **7** - Preset G
- **8** - Preset H
- **9** - Preset I
- **10** - Preset J
- **11** - Preset K

## Render.RENDER_FSR_MODE FSRMode

***Console*:**`render_upscale_fsr_mode`The quality mode of FSR (FidelityFX Super Resolution upsampling technique).
- *Ultra Performance* that offers the highest performance gain while still retaining image quality close to native. Scale factor: 3.0x per dimension (≈33.3% of output resolution)
- *Performance* that delivers a substantial performance boost with image quality similar to native rendering. Scale factor: 2.0x per dimension (≈50.0% of output resolution)
- *Balanced* that balances performance gains and image quality effectively. Scale factor: 1.7x per dimension (≈58.8% of output resolution)
- *Quality* that provides image quality equal to or better than native with a meaningful performance improvement. Scale factor: 1.5x per dimension (≈66.6% of output resolution)
- *Native AA* that renders at native resolution (no upscaling, scale factor 1.0x) and applies FSR anti-aliasing only.
- *Custom* that uses a custom resolution scale set via the [FSRCustomResolutionScale](#FSRCustomResolutionScale) property (range: 0.1 to 1.0).

  One of the following values:
- **0** - Ultra Performance (by default)
- **1** - Performance
- **2** - Balanced
- **3** - Quality
- **4** - Native AA
- **5** - Custom

## bool FSREnableSharpness

***Console*:**`render_upscale_fsr_enable_sharpness`The value indicating if additional sharpness pass for FidelityFX Super Resolution upscaling is enabled. The default value is **false**.
## float FSRSharpness

***Console*:**`render_upscale_fsr_sharpness`The sharpness value, where 0 is no additional sharpness and 1 is maximum additional sharpness.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**.
## float FSRPreExposure

***Console*:**`render_upscale_fsr_pre_exposure`The pre-exposure value by which we divide the input signal to get back to the original signal produced by the game before any packing into lower precision render targets.
Range of values: **[0.0f, inf]**. The default value is : **1.0f**.
## 🔒︎ Event EventBegin

The event triggered when rendering of the frame begins. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the Begin event handler
void begin_event_handler()
{
	Log.Message("\Handling Begin event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begin_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBegin.Connect(begin_event_connections, begin_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBegin.Connect(begin_event_connections, () => {
		Log.Message("Handling Begin event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begin_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the Begin event with a handler function
Render.EventBegin.Connect(begin_event_handler);

// remove subscription to the Begin event later by the handler function
Render.EventBegin.Disconnect(begin_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begin_event_connection;

// subscribe to the Begin event with a lambda handler function and keeping the connection
begin_event_connection = Render.EventBegin.Connect(() => {
		Log.Message("Handling Begin event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begin_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begin_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begin_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring Begin events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBegin.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBegin.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginEnvironment

The event triggered before the Environment rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginEnvironment event handler
void beginenvironment_event_handler()
{
	Log.Message("\Handling BeginEnvironment event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginenvironment_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginEnvironment.Connect(beginenvironment_event_connections, beginenvironment_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginEnvironment.Connect(beginenvironment_event_connections, () => {
		Log.Message("Handling BeginEnvironment event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginenvironment_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginEnvironment event with a handler function
Render.EventBeginEnvironment.Connect(beginenvironment_event_handler);

// remove subscription to the BeginEnvironment event later by the handler function
Render.EventBeginEnvironment.Disconnect(beginenvironment_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginenvironment_event_connection;

// subscribe to the BeginEnvironment event with a lambda handler function and keeping the connection
beginenvironment_event_connection = Render.EventBeginEnvironment.Connect(() => {
		Log.Message("Handling BeginEnvironment event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginenvironment_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginenvironment_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginenvironment_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginEnvironment events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginEnvironment.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginEnvironment.Enabled = true;

```

</details>

## 🔒︎ Event EventEndEnvironment

The event triggered after the Environment rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndEnvironment event handler
void endenvironment_event_handler()
{
	Log.Message("\Handling EndEnvironment event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endenvironment_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndEnvironment.Connect(endenvironment_event_connections, endenvironment_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndEnvironment.Connect(endenvironment_event_connections, () => {
		Log.Message("Handling EndEnvironment event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endenvironment_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndEnvironment event with a handler function
Render.EventEndEnvironment.Connect(endenvironment_event_handler);

// remove subscription to the EndEnvironment event later by the handler function
Render.EventEndEnvironment.Disconnect(endenvironment_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endenvironment_event_connection;

// subscribe to the EndEnvironment event with a lambda handler function and keeping the connection
endenvironment_event_connection = Render.EventEndEnvironment.Connect(() => {
		Log.Message("Handling EndEnvironment event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endenvironment_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endenvironment_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endenvironment_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndEnvironment events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndEnvironment.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndEnvironment.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginShadows

The event triggered before the shadows rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginShadows event handler
void beginshadows_event_handler()
{
	Log.Message("\Handling BeginShadows event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginshadows_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginShadows.Connect(beginshadows_event_connections, beginshadows_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginShadows.Connect(beginshadows_event_connections, () => {
		Log.Message("Handling BeginShadows event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginshadows_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginShadows event with a handler function
Render.EventBeginShadows.Connect(beginshadows_event_handler);

// remove subscription to the BeginShadows event later by the handler function
Render.EventBeginShadows.Disconnect(beginshadows_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginshadows_event_connection;

// subscribe to the BeginShadows event with a lambda handler function and keeping the connection
beginshadows_event_connection = Render.EventBeginShadows.Connect(() => {
		Log.Message("Handling BeginShadows event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginshadows_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginshadows_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginshadows_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginShadows events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginShadows.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginShadows.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWorldShadow

The event triggered before the stage of rendering shadows from World light sources. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWorldShadow event handler
void beginworldshadow_event_handler()
{
	Log.Message("\Handling BeginWorldShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginworldshadow_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginWorldShadow.Connect(beginworldshadow_event_connections, beginworldshadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginWorldShadow.Connect(beginworldshadow_event_connections, () => {
		Log.Message("Handling BeginWorldShadow event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginworldshadow_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWorldShadow event with a handler function
Render.EventBeginWorldShadow.Connect(beginworldshadow_event_handler);

// remove subscription to the BeginWorldShadow event later by the handler function
Render.EventBeginWorldShadow.Disconnect(beginworldshadow_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginworldshadow_event_connection;

// subscribe to the BeginWorldShadow event with a lambda handler function and keeping the connection
beginworldshadow_event_connection = Render.EventBeginWorldShadow.Connect(() => {
		Log.Message("Handling BeginWorldShadow event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginworldshadow_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginworldshadow_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginworldshadow_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWorldShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginWorldShadow.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginWorldShadow.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWorldShadow

The event triggered after the stage of rendering shadows from World light sources. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWorldShadow event handler
void endworldshadow_event_handler()
{
	Log.Message("\Handling EndWorldShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endworldshadow_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndWorldShadow.Connect(endworldshadow_event_connections, endworldshadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndWorldShadow.Connect(endworldshadow_event_connections, () => {
		Log.Message("Handling EndWorldShadow event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endworldshadow_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWorldShadow event with a handler function
Render.EventEndWorldShadow.Connect(endworldshadow_event_handler);

// remove subscription to the EndWorldShadow event later by the handler function
Render.EventEndWorldShadow.Disconnect(endworldshadow_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endworldshadow_event_connection;

// subscribe to the EndWorldShadow event with a lambda handler function and keeping the connection
endworldshadow_event_connection = Render.EventEndWorldShadow.Connect(() => {
		Log.Message("Handling EndWorldShadow event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endworldshadow_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endworldshadow_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endworldshadow_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWorldShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndWorldShadow.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndWorldShadow.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginProjShadow

The event triggered before the stage of rendering shadows from Projected light sources. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginProjShadow event handler
void beginprojshadow_event_handler()
{
	Log.Message("\Handling BeginProjShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginprojshadow_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginProjShadow.Connect(beginprojshadow_event_connections, beginprojshadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginProjShadow.Connect(beginprojshadow_event_connections, () => {
		Log.Message("Handling BeginProjShadow event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginprojshadow_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginProjShadow event with a handler function
Render.EventBeginProjShadow.Connect(beginprojshadow_event_handler);

// remove subscription to the BeginProjShadow event later by the handler function
Render.EventBeginProjShadow.Disconnect(beginprojshadow_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginprojshadow_event_connection;

// subscribe to the BeginProjShadow event with a lambda handler function and keeping the connection
beginprojshadow_event_connection = Render.EventBeginProjShadow.Connect(() => {
		Log.Message("Handling BeginProjShadow event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginprojshadow_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginprojshadow_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginprojshadow_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginProjShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginProjShadow.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginProjShadow.Enabled = true;

```

</details>

## 🔒︎ Event EventEndProjShadow

The event triggered after the stage of rendering shadows from Projected light sources. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndProjShadow event handler
void endprojshadow_event_handler()
{
	Log.Message("\Handling EndProjShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endprojshadow_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndProjShadow.Connect(endprojshadow_event_connections, endprojshadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndProjShadow.Connect(endprojshadow_event_connections, () => {
		Log.Message("Handling EndProjShadow event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endprojshadow_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndProjShadow event with a handler function
Render.EventEndProjShadow.Connect(endprojshadow_event_handler);

// remove subscription to the EndProjShadow event later by the handler function
Render.EventEndProjShadow.Disconnect(endprojshadow_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endprojshadow_event_connection;

// subscribe to the EndProjShadow event with a lambda handler function and keeping the connection
endprojshadow_event_connection = Render.EventEndProjShadow.Connect(() => {
		Log.Message("Handling EndProjShadow event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endprojshadow_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endprojshadow_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endprojshadow_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndProjShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndProjShadow.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndProjShadow.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginOmniShadow

The event triggered before the stage of rendering shadows from Omni light sources. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginOmniShadow event handler
void beginomnishadow_event_handler()
{
	Log.Message("\Handling BeginOmniShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginomnishadow_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginOmniShadow.Connect(beginomnishadow_event_connections, beginomnishadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginOmniShadow.Connect(beginomnishadow_event_connections, () => {
		Log.Message("Handling BeginOmniShadow event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginomnishadow_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginOmniShadow event with a handler function
Render.EventBeginOmniShadow.Connect(beginomnishadow_event_handler);

// remove subscription to the BeginOmniShadow event later by the handler function
Render.EventBeginOmniShadow.Disconnect(beginomnishadow_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginomnishadow_event_connection;

// subscribe to the BeginOmniShadow event with a lambda handler function and keeping the connection
beginomnishadow_event_connection = Render.EventBeginOmniShadow.Connect(() => {
		Log.Message("Handling BeginOmniShadow event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginomnishadow_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginomnishadow_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginomnishadow_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginOmniShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginOmniShadow.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginOmniShadow.Enabled = true;

```

</details>

## 🔒︎ Event EventEndOmniShadow

The event triggered after the stage of rendering shadows from Omni light sources. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndOmniShadow event handler
void endomnishadow_event_handler()
{
	Log.Message("\Handling EndOmniShadow event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endomnishadow_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndOmniShadow.Connect(endomnishadow_event_connections, endomnishadow_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndOmniShadow.Connect(endomnishadow_event_connections, () => {
		Log.Message("Handling EndOmniShadow event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endomnishadow_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndOmniShadow event with a handler function
Render.EventEndOmniShadow.Connect(endomnishadow_event_handler);

// remove subscription to the EndOmniShadow event later by the handler function
Render.EventEndOmniShadow.Disconnect(endomnishadow_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endomnishadow_event_connection;

// subscribe to the EndOmniShadow event with a lambda handler function and keeping the connection
endomnishadow_event_connection = Render.EventEndOmniShadow.Connect(() => {
		Log.Message("Handling EndOmniShadow event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endomnishadow_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endomnishadow_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endomnishadow_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndOmniShadow events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndOmniShadow.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndOmniShadow.Enabled = true;

```

</details>

## 🔒︎ Event EventEndShadows

The event triggered after the shadows rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndShadows event handler
void endshadows_event_handler()
{
	Log.Message("\Handling EndShadows event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endshadows_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndShadows.Connect(endshadows_event_connections, endshadows_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndShadows.Connect(endshadows_event_connections, () => {
		Log.Message("Handling EndShadows event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endshadows_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndShadows event with a handler function
Render.EventEndShadows.Connect(endshadows_event_handler);

// remove subscription to the EndShadows event later by the handler function
Render.EventEndShadows.Disconnect(endshadows_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endshadows_event_connection;

// subscribe to the EndShadows event with a lambda handler function and keeping the connection
endshadows_event_connection = Render.EventEndShadows.Connect(() => {
		Log.Message("Handling EndShadows event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endshadows_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endshadows_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endshadows_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndShadows events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndShadows.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndShadows.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginScreen

The event triggered before the stage of rendering each screen (a stereo image has 2 screens, while a cubemap will have 6). You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginScreen event handler
void beginscreen_event_handler()
{
	Log.Message("\Handling BeginScreen event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginscreen_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginScreen.Connect(beginscreen_event_connections, beginscreen_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginScreen.Connect(beginscreen_event_connections, () => {
		Log.Message("Handling BeginScreen event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginscreen_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginScreen event with a handler function
Render.EventBeginScreen.Connect(beginscreen_event_handler);

// remove subscription to the BeginScreen event later by the handler function
Render.EventBeginScreen.Disconnect(beginscreen_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginscreen_event_connection;

// subscribe to the BeginScreen event with a lambda handler function and keeping the connection
beginscreen_event_connection = Render.EventBeginScreen.Connect(() => {
		Log.Message("Handling BeginScreen event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginscreen_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginscreen_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginscreen_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginScreen events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginScreen.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginScreen.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginMixedRealityBlendMaskColor

The event triggered before the mask for Mixed Reality is rendered. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginMixedRealityBlendMaskColor event handler
void beginmixedrealityblendmaskcolor_event_handler()
{
	Log.Message("\Handling BeginMixedRealityBlendMaskColor event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginmixedrealityblendmaskcolor_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginMixedRealityBlendMaskColor.Connect(beginmixedrealityblendmaskcolor_event_connections, beginmixedrealityblendmaskcolor_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginMixedRealityBlendMaskColor.Connect(beginmixedrealityblendmaskcolor_event_connections, () => {
		Log.Message("Handling BeginMixedRealityBlendMaskColor event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginmixedrealityblendmaskcolor_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginMixedRealityBlendMaskColor event with a handler function
Render.EventBeginMixedRealityBlendMaskColor.Connect(beginmixedrealityblendmaskcolor_event_handler);

// remove subscription to the BeginMixedRealityBlendMaskColor event later by the handler function
Render.EventBeginMixedRealityBlendMaskColor.Disconnect(beginmixedrealityblendmaskcolor_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginmixedrealityblendmaskcolor_event_connection;

// subscribe to the BeginMixedRealityBlendMaskColor event with a lambda handler function and keeping the connection
beginmixedrealityblendmaskcolor_event_connection = Render.EventBeginMixedRealityBlendMaskColor.Connect(() => {
		Log.Message("Handling BeginMixedRealityBlendMaskColor event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginmixedrealityblendmaskcolor_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginmixedrealityblendmaskcolor_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginmixedrealityblendmaskcolor_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginMixedRealityBlendMaskColor events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginMixedRealityBlendMaskColor.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginMixedRealityBlendMaskColor.Enabled = true;

```

</details>

## 🔒︎ Event EventEndMixedRealityBlendMaskColor

The event triggered after the mask for Mixed Reality is rendered. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndMixedRealityBlendMaskColor event handler
void endmixedrealityblendmaskcolor_event_handler()
{
	Log.Message("\Handling EndMixedRealityBlendMaskColor event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endmixedrealityblendmaskcolor_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndMixedRealityBlendMaskColor.Connect(endmixedrealityblendmaskcolor_event_connections, endmixedrealityblendmaskcolor_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndMixedRealityBlendMaskColor.Connect(endmixedrealityblendmaskcolor_event_connections, () => {
		Log.Message("Handling EndMixedRealityBlendMaskColor event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endmixedrealityblendmaskcolor_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndMixedRealityBlendMaskColor event with a handler function
Render.EventEndMixedRealityBlendMaskColor.Connect(endmixedrealityblendmaskcolor_event_handler);

// remove subscription to the EndMixedRealityBlendMaskColor event later by the handler function
Render.EventEndMixedRealityBlendMaskColor.Disconnect(endmixedrealityblendmaskcolor_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endmixedrealityblendmaskcolor_event_connection;

// subscribe to the EndMixedRealityBlendMaskColor event with a lambda handler function and keeping the connection
endmixedrealityblendmaskcolor_event_connection = Render.EventEndMixedRealityBlendMaskColor.Connect(() => {
		Log.Message("Handling EndMixedRealityBlendMaskColor event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endmixedrealityblendmaskcolor_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endmixedrealityblendmaskcolor_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endmixedrealityblendmaskcolor_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndMixedRealityBlendMaskColor events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndMixedRealityBlendMaskColor.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndMixedRealityBlendMaskColor.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginVisualizerQuadOverdraw

The event triggered before *[Quad Overdraw](../../../content/optimization/geometry/quad_overdraw/index.md#tool_overview)* visualizer rendering. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginVisualizerQuadOverdraw event handler
void beginvisualizerquadoverdraw_event_handler()
{
	Log.Message("\Handling BeginVisualizerQuadOverdraw event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginvisualizerquadoverdraw_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginVisualizerQuadOverdraw.Connect(beginvisualizerquadoverdraw_event_connections, beginvisualizerquadoverdraw_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginVisualizerQuadOverdraw.Connect(beginvisualizerquadoverdraw_event_connections, () => {
		Log.Message("Handling BeginVisualizerQuadOverdraw event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginvisualizerquadoverdraw_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginVisualizerQuadOverdraw event with a handler function
publisher.EventBeginVisualizerQuadOverdraw.Connect(beginvisualizerquadoverdraw_event_handler);

// remove subscription to the BeginVisualizerQuadOverdraw event later by the handler function
publisher.EventBeginVisualizerQuadOverdraw.Disconnect(beginvisualizerquadoverdraw_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginvisualizerquadoverdraw_event_connection;

// subscribe to the BeginVisualizerQuadOverdraw event with a lambda handler function and keeping the connection
beginvisualizerquadoverdraw_event_connection = publisher.EventBeginVisualizerQuadOverdraw.Connect(() => {
		Log.Message("Handling BeginVisualizerQuadOverdraw event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginvisualizerquadoverdraw_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginvisualizerquadoverdraw_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginvisualizerquadoverdraw_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginVisualizerQuadOverdraw events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginVisualizerQuadOverdraw.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginVisualizerQuadOverdraw.Enabled = true;

```

</details>

## 🔒︎ Event EventEndVisualizerQuadOverdraw

The event triggered after *[Quad Overdraw](../../../content/optimization/geometry/quad_overdraw/index.md#tool_overview)* visualizer rendering. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndVisualizerQuadOverdraw event handler
void endvisualizerquadoverdraw_event_handler()
{
	Log.Message("\Handling EndVisualizerQuadOverdraw event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endvisualizerquadoverdraw_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndVisualizerQuadOverdraw.Connect(endvisualizerquadoverdraw_event_connections, endvisualizerquadoverdraw_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndVisualizerQuadOverdraw.Connect(endvisualizerquadoverdraw_event_connections, () => {
		Log.Message("Handling EndVisualizerQuadOverdraw event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endvisualizerquadoverdraw_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndVisualizerQuadOverdraw event with a handler function
publisher.EventEndVisualizerQuadOverdraw.Connect(endvisualizerquadoverdraw_event_handler);

// remove subscription to the EndVisualizerQuadOverdraw event later by the handler function
publisher.EventEndVisualizerQuadOverdraw.Disconnect(endvisualizerquadoverdraw_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endvisualizerquadoverdraw_event_connection;

// subscribe to the EndVisualizerQuadOverdraw event with a lambda handler function and keeping the connection
endvisualizerquadoverdraw_event_connection = publisher.EventEndVisualizerQuadOverdraw.Connect(() => {
		Log.Message("Handling EndVisualizerQuadOverdraw event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endvisualizerquadoverdraw_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endvisualizerquadoverdraw_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endvisualizerquadoverdraw_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndVisualizerQuadOverdraw events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndVisualizerQuadOverdraw.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndVisualizerQuadOverdraw.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginOpacityGBuffer

The event triggered before filling the Gbuffer. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginOpacityGBuffer event handler
void beginopacitygbuffer_event_handler()
{
	Log.Message("\Handling BeginOpacityGBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacitygbuffer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginOpacityGBuffer.Connect(beginopacitygbuffer_event_connections, beginopacitygbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginOpacityGBuffer.Connect(beginopacitygbuffer_event_connections, () => {
		Log.Message("Handling BeginOpacityGBuffer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginopacitygbuffer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginOpacityGBuffer event with a handler function
Render.EventBeginOpacityGBuffer.Connect(beginopacitygbuffer_event_handler);

// remove subscription to the BeginOpacityGBuffer event later by the handler function
Render.EventBeginOpacityGBuffer.Disconnect(beginopacitygbuffer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginopacitygbuffer_event_connection;

// subscribe to the BeginOpacityGBuffer event with a lambda handler function and keeping the connection
beginopacitygbuffer_event_connection = Render.EventBeginOpacityGBuffer.Connect(() => {
		Log.Message("Handling BeginOpacityGBuffer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginopacitygbuffer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginopacitygbuffer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginopacitygbuffer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginOpacityGBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginOpacityGBuffer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginOpacityGBuffer.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginAuxiliarySurfaces

The event triggered before auxiliary surfaces rendering. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginAuxiliarySurfaces event handler
void beginauxiliarysurfaces_event_handler()
{
	Log.Message("\Handling BeginAuxiliarySurfaces event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginauxiliarysurfaces_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginAuxiliarySurfaces.Connect(beginauxiliarysurfaces_event_connections, beginauxiliarysurfaces_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginAuxiliarySurfaces.Connect(beginauxiliarysurfaces_event_connections, () => {
		Log.Message("Handling BeginAuxiliarySurfaces event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginauxiliarysurfaces_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginAuxiliarySurfaces event with a handler function
Render.EventBeginAuxiliarySurfaces.Connect(beginauxiliarysurfaces_event_handler);

// remove subscription to the BeginAuxiliarySurfaces event later by the handler function
Render.EventBeginAuxiliarySurfaces.Disconnect(beginauxiliarysurfaces_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginauxiliarysurfaces_event_connection;

// subscribe to the BeginAuxiliarySurfaces event with a lambda handler function and keeping the connection
beginauxiliarysurfaces_event_connection = Render.EventBeginAuxiliarySurfaces.Connect(() => {
		Log.Message("Handling BeginAuxiliarySurfaces event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginauxiliarysurfaces_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginauxiliarysurfaces_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginauxiliarysurfaces_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginAuxiliarySurfaces events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginAuxiliarySurfaces.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginAuxiliarySurfaces.Enabled = true;

```

</details>

## 🔒︎ Event EventEndAuxiliarySurfaces

The event triggered after auxiliary surfaces rendering. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndAuxiliarySurfaces event handler
void endauxiliarysurfaces_event_handler()
{
	Log.Message("\Handling EndAuxiliarySurfaces event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endauxiliarysurfaces_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndAuxiliarySurfaces.Connect(endauxiliarysurfaces_event_connections, endauxiliarysurfaces_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndAuxiliarySurfaces.Connect(endauxiliarysurfaces_event_connections, () => {
		Log.Message("Handling EndAuxiliarySurfaces event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endauxiliarysurfaces_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndAuxiliarySurfaces event with a handler function
Render.EventEndAuxiliarySurfaces.Connect(endauxiliarysurfaces_event_handler);

// remove subscription to the EndAuxiliarySurfaces event later by the handler function
Render.EventEndAuxiliarySurfaces.Disconnect(endauxiliarysurfaces_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endauxiliarysurfaces_event_connection;

// subscribe to the EndAuxiliarySurfaces event with a lambda handler function and keeping the connection
endauxiliarysurfaces_event_connection = Render.EventEndAuxiliarySurfaces.Connect(() => {
		Log.Message("Handling EndAuxiliarySurfaces event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endauxiliarysurfaces_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endauxiliarysurfaces_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endauxiliarysurfaces_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndAuxiliarySurfaces events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndAuxiliarySurfaces.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndAuxiliarySurfaces.Enabled = true;

```

</details>

## 🔒︎ Event EventEndOpacityGBuffer

The event triggered after filling the Gbuffer. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndOpacityGBuffer event handler
void endopacitygbuffer_event_handler()
{
	Log.Message("\Handling EndOpacityGBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacitygbuffer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndOpacityGBuffer.Connect(endopacitygbuffer_event_connections, endopacitygbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndOpacityGBuffer.Connect(endopacitygbuffer_event_connections, () => {
		Log.Message("Handling EndOpacityGBuffer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endopacitygbuffer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndOpacityGBuffer event with a handler function
Render.EventEndOpacityGBuffer.Connect(endopacitygbuffer_event_handler);

// remove subscription to the EndOpacityGBuffer event later by the handler function
Render.EventEndOpacityGBuffer.Disconnect(endopacitygbuffer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endopacitygbuffer_event_connection;

// subscribe to the EndOpacityGBuffer event with a lambda handler function and keeping the connection
endopacitygbuffer_event_connection = Render.EventEndOpacityGBuffer.Connect(() => {
		Log.Message("Handling EndOpacityGBuffer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endopacitygbuffer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endopacitygbuffer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endopacitygbuffer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndOpacityGBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndOpacityGBuffer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndOpacityGBuffer.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginOpacityDecals

The event triggered before the opacity decals rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginOpacityDecals event handler
void beginopacitydecals_event_handler()
{
	Log.Message("\Handling BeginOpacityDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacitydecals_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginOpacityDecals.Connect(beginopacitydecals_event_connections, beginopacitydecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginOpacityDecals.Connect(beginopacitydecals_event_connections, () => {
		Log.Message("Handling BeginOpacityDecals event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginopacitydecals_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginOpacityDecals event with a handler function
Render.EventBeginOpacityDecals.Connect(beginopacitydecals_event_handler);

// remove subscription to the BeginOpacityDecals event later by the handler function
Render.EventBeginOpacityDecals.Disconnect(beginopacitydecals_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginopacitydecals_event_connection;

// subscribe to the BeginOpacityDecals event with a lambda handler function and keeping the connection
beginopacitydecals_event_connection = Render.EventBeginOpacityDecals.Connect(() => {
		Log.Message("Handling BeginOpacityDecals event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginopacitydecals_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginopacitydecals_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginopacitydecals_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginOpacityDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginOpacityDecals.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginOpacityDecals.Enabled = true;

```

</details>

## 🔒︎ Event EventEndOpacityDecals

The event triggered after the opacity decals rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndOpacityDecals event handler
void endopacitydecals_event_handler()
{
	Log.Message("\Handling EndOpacityDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacitydecals_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndOpacityDecals.Connect(endopacitydecals_event_connections, endopacitydecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndOpacityDecals.Connect(endopacitydecals_event_connections, () => {
		Log.Message("Handling EndOpacityDecals event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endopacitydecals_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndOpacityDecals event with a handler function
Render.EventEndOpacityDecals.Connect(endopacitydecals_event_handler);

// remove subscription to the EndOpacityDecals event later by the handler function
Render.EventEndOpacityDecals.Disconnect(endopacitydecals_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endopacitydecals_event_connection;

// subscribe to the EndOpacityDecals event with a lambda handler function and keeping the connection
endopacitydecals_event_connection = Render.EventEndOpacityDecals.Connect(() => {
		Log.Message("Handling EndOpacityDecals event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endopacitydecals_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endopacitydecals_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endopacitydecals_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndOpacityDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndOpacityDecals.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndOpacityDecals.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginAuxiliaryDecals

The event triggered before the auxiliary decals rendering. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginAuxiliaryDecals event handler
void beginauxiliarydecals_event_handler()
{
	Log.Message("\Handling BeginAuxiliaryDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginauxiliarydecals_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginAuxiliaryDecals.Connect(beginauxiliarydecals_event_connections, beginauxiliarydecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginAuxiliaryDecals.Connect(beginauxiliarydecals_event_connections, () => {
		Log.Message("Handling BeginAuxiliaryDecals event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginauxiliarydecals_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginAuxiliaryDecals event with a handler function
Render.EventBeginAuxiliaryDecals.Connect(beginauxiliarydecals_event_handler);

// remove subscription to the BeginAuxiliaryDecals event later by the handler function
Render.EventBeginAuxiliaryDecals.Disconnect(beginauxiliarydecals_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginauxiliarydecals_event_connection;

// subscribe to the BeginAuxiliaryDecals event with a lambda handler function and keeping the connection
beginauxiliarydecals_event_connection = Render.EventBeginAuxiliaryDecals.Connect(() => {
		Log.Message("Handling BeginAuxiliaryDecals event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginauxiliarydecals_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginauxiliarydecals_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginauxiliarydecals_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginAuxiliaryDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginAuxiliaryDecals.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginAuxiliaryDecals.Enabled = true;

```

</details>

## 🔒︎ Event EventEndAuxiliaryDecals

The event triggered after the auxiliary decals rendering. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndAuxiliaryDecals event handler
void endauxiliarydecals_event_handler()
{
	Log.Message("\Handling EndAuxiliaryDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endauxiliarydecals_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndAuxiliaryDecals.Connect(endauxiliarydecals_event_connections, endauxiliarydecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndAuxiliaryDecals.Connect(endauxiliarydecals_event_connections, () => {
		Log.Message("Handling EndAuxiliaryDecals event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endauxiliarydecals_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndAuxiliaryDecals event with a handler function
Render.EventEndAuxiliaryDecals.Connect(endauxiliarydecals_event_handler);

// remove subscription to the EndAuxiliaryDecals event later by the handler function
Render.EventEndAuxiliaryDecals.Disconnect(endauxiliarydecals_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endauxiliarydecals_event_connection;

// subscribe to the EndAuxiliaryDecals event with a lambda handler function and keeping the connection
endauxiliarydecals_event_connection = Render.EventEndAuxiliaryDecals.Connect(() => {
		Log.Message("Handling EndAuxiliaryDecals event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endauxiliarydecals_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endauxiliarydecals_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endauxiliarydecals_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndAuxiliaryDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndAuxiliaryDecals.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndAuxiliaryDecals.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginCurvature

The event triggered before the [SSBevel](../../../editor2/settings/render_settings/ssbevel/index.md) effect rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginCurvature event handler
void begincurvature_event_handler()
{
	Log.Message("\Handling BeginCurvature event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begincurvature_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginCurvature.Connect(begincurvature_event_connections, begincurvature_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginCurvature.Connect(begincurvature_event_connections, () => {
		Log.Message("Handling BeginCurvature event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begincurvature_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginCurvature event with a handler function
Render.EventBeginCurvature.Connect(begincurvature_event_handler);

// remove subscription to the BeginCurvature event later by the handler function
Render.EventBeginCurvature.Disconnect(begincurvature_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begincurvature_event_connection;

// subscribe to the BeginCurvature event with a lambda handler function and keeping the connection
begincurvature_event_connection = Render.EventBeginCurvature.Connect(() => {
		Log.Message("Handling BeginCurvature event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begincurvature_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begincurvature_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begincurvature_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginCurvature events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginCurvature.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginCurvature.Enabled = true;

```

</details>

## 🔒︎ Event EventEndCurvature

The event triggered after the [SSBevel](../../../editor2/settings/render_settings/ssbevel/index.md) effect rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndCurvature event handler
void endcurvature_event_handler()
{
	Log.Message("\Handling EndCurvature event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endcurvature_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndCurvature.Connect(endcurvature_event_connections, endcurvature_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndCurvature.Connect(endcurvature_event_connections, () => {
		Log.Message("Handling EndCurvature event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endcurvature_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndCurvature event with a handler function
Render.EventEndCurvature.Connect(endcurvature_event_handler);

// remove subscription to the EndCurvature event later by the handler function
Render.EventEndCurvature.Disconnect(endcurvature_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endcurvature_event_connection;

// subscribe to the EndCurvature event with a lambda handler function and keeping the connection
endcurvature_event_connection = Render.EventEndCurvature.Connect(() => {
		Log.Message("Handling EndCurvature event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endcurvature_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endcurvature_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endcurvature_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndCurvature events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndCurvature.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndCurvature.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginCurvatureComposite

The event triggered before the curvature rendering stage for the [SSDirt](../../../editor2/settings/render_settings/ssdirt/index.md) effect. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginCurvatureComposite event handler
void begincurvaturecomposite_event_handler()
{
	Log.Message("\Handling BeginCurvatureComposite event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begincurvaturecomposite_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginCurvatureComposite.Connect(begincurvaturecomposite_event_connections, begincurvaturecomposite_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginCurvatureComposite.Connect(begincurvaturecomposite_event_connections, () => {
		Log.Message("Handling BeginCurvatureComposite event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begincurvaturecomposite_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginCurvatureComposite event with a handler function
Render.EventBeginCurvatureComposite.Connect(begincurvaturecomposite_event_handler);

// remove subscription to the BeginCurvatureComposite event later by the handler function
Render.EventBeginCurvatureComposite.Disconnect(begincurvaturecomposite_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begincurvaturecomposite_event_connection;

// subscribe to the BeginCurvatureComposite event with a lambda handler function and keeping the connection
begincurvaturecomposite_event_connection = Render.EventBeginCurvatureComposite.Connect(() => {
		Log.Message("Handling BeginCurvatureComposite event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begincurvaturecomposite_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begincurvaturecomposite_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begincurvaturecomposite_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginCurvatureComposite events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginCurvatureComposite.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginCurvatureComposite.Enabled = true;

```

</details>

## 🔒︎ Event EventEndCurvatureComposite

The event triggered after the curvature rendering stage for the [SSDirt](../../../editor2/settings/render_settings/ssdirt/index.md) effect. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndCurvatureComposite event handler
void endcurvaturecomposite_event_handler()
{
	Log.Message("\Handling EndCurvatureComposite event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endcurvaturecomposite_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndCurvatureComposite.Connect(endcurvaturecomposite_event_connections, endcurvaturecomposite_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndCurvatureComposite.Connect(endcurvaturecomposite_event_connections, () => {
		Log.Message("Handling EndCurvatureComposite event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endcurvaturecomposite_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndCurvatureComposite event with a handler function
Render.EventEndCurvatureComposite.Connect(endcurvaturecomposite_event_handler);

// remove subscription to the EndCurvatureComposite event later by the handler function
Render.EventEndCurvatureComposite.Disconnect(endcurvaturecomposite_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endcurvaturecomposite_event_connection;

// subscribe to the EndCurvatureComposite event with a lambda handler function and keeping the connection
endcurvaturecomposite_event_connection = Render.EventEndCurvatureComposite.Connect(() => {
		Log.Message("Handling EndCurvatureComposite event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endcurvaturecomposite_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endcurvaturecomposite_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endcurvaturecomposite_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndCurvatureComposite events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndCurvatureComposite.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndCurvatureComposite.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSSRTGI

The event triggered before the SSRTGI rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSSRTGI event handler
void beginssrtgi_event_handler()
{
	Log.Message("\Handling BeginSSRTGI event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginssrtgi_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginSSRTGI.Connect(beginssrtgi_event_connections, beginssrtgi_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginSSRTGI.Connect(beginssrtgi_event_connections, () => {
		Log.Message("Handling BeginSSRTGI event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginssrtgi_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSSRTGI event with a handler function
Render.EventBeginSSRTGI.Connect(beginssrtgi_event_handler);

// remove subscription to the BeginSSRTGI event later by the handler function
Render.EventBeginSSRTGI.Disconnect(beginssrtgi_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginssrtgi_event_connection;

// subscribe to the BeginSSRTGI event with a lambda handler function and keeping the connection
beginssrtgi_event_connection = Render.EventBeginSSRTGI.Connect(() => {
		Log.Message("Handling BeginSSRTGI event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginssrtgi_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginssrtgi_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginssrtgi_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSSRTGI events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginSSRTGI.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginSSRTGI.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSSRTGI

The event triggered after the SSRTGI rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSSRTGI event handler
void endssrtgi_event_handler()
{
	Log.Message("\Handling EndSSRTGI event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endssrtgi_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndSSRTGI.Connect(endssrtgi_event_connections, endssrtgi_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndSSRTGI.Connect(endssrtgi_event_connections, () => {
		Log.Message("Handling EndSSRTGI event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endssrtgi_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSSRTGI event with a handler function
Render.EventEndSSRTGI.Connect(endssrtgi_event_handler);

// remove subscription to the EndSSRTGI event later by the handler function
Render.EventEndSSRTGI.Disconnect(endssrtgi_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endssrtgi_event_connection;

// subscribe to the EndSSRTGI event with a lambda handler function and keeping the connection
endssrtgi_event_connection = Render.EventEndSSRTGI.Connect(() => {
		Log.Message("Handling EndSSRTGI event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endssrtgi_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endssrtgi_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endssrtgi_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSSRTGI events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndSSRTGI.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndSSRTGI.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginOpacityLights

The event triggered before the opacity lightgs rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginOpacityLights event handler
void beginopacitylights_event_handler()
{
	Log.Message("\Handling BeginOpacityLights event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacitylights_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginOpacityLights.Connect(beginopacitylights_event_connections, beginopacitylights_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginOpacityLights.Connect(beginopacitylights_event_connections, () => {
		Log.Message("Handling BeginOpacityLights event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginopacitylights_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginOpacityLights event with a handler function
Render.EventBeginOpacityLights.Connect(beginopacitylights_event_handler);

// remove subscription to the BeginOpacityLights event later by the handler function
Render.EventBeginOpacityLights.Disconnect(beginopacitylights_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginopacitylights_event_connection;

// subscribe to the BeginOpacityLights event with a lambda handler function and keeping the connection
beginopacitylights_event_connection = Render.EventBeginOpacityLights.Connect(() => {
		Log.Message("Handling BeginOpacityLights event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginopacitylights_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginopacitylights_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginopacitylights_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginOpacityLights events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginOpacityLights.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginOpacityLights.Enabled = true;

```

</details>

## 🔒︎ Event EventEndOpacityLights

The event triggered after the opacity lightgs rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndOpacityLights event handler
void endopacitylights_event_handler()
{
	Log.Message("\Handling EndOpacityLights event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacitylights_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndOpacityLights.Connect(endopacitylights_event_connections, endopacitylights_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndOpacityLights.Connect(endopacitylights_event_connections, () => {
		Log.Message("Handling EndOpacityLights event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endopacitylights_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndOpacityLights event with a handler function
Render.EventEndOpacityLights.Connect(endopacitylights_event_handler);

// remove subscription to the EndOpacityLights event later by the handler function
Render.EventEndOpacityLights.Disconnect(endopacitylights_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endopacitylights_event_connection;

// subscribe to the EndOpacityLights event with a lambda handler function and keeping the connection
endopacitylights_event_connection = Render.EventEndOpacityLights.Connect(() => {
		Log.Message("Handling EndOpacityLights event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endopacitylights_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endopacitylights_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endopacitylights_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndOpacityLights events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndOpacityLights.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndOpacityLights.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginOpacityVoxelProbes

The event triggered before the opacity voxel probes rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginOpacityVoxelProbes event handler
void beginopacityvoxelprobes_event_handler()
{
	Log.Message("\Handling BeginOpacityVoxelProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacityvoxelprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginOpacityVoxelProbes.Connect(beginopacityvoxelprobes_event_connections, beginopacityvoxelprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginOpacityVoxelProbes.Connect(beginopacityvoxelprobes_event_connections, () => {
		Log.Message("Handling BeginOpacityVoxelProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginopacityvoxelprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginOpacityVoxelProbes event with a handler function
Render.EventBeginOpacityVoxelProbes.Connect(beginopacityvoxelprobes_event_handler);

// remove subscription to the BeginOpacityVoxelProbes event later by the handler function
Render.EventBeginOpacityVoxelProbes.Disconnect(beginopacityvoxelprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginopacityvoxelprobes_event_connection;

// subscribe to the BeginOpacityVoxelProbes event with a lambda handler function and keeping the connection
beginopacityvoxelprobes_event_connection = Render.EventBeginOpacityVoxelProbes.Connect(() => {
		Log.Message("Handling BeginOpacityVoxelProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginopacityvoxelprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginopacityvoxelprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginopacityvoxelprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginOpacityVoxelProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginOpacityVoxelProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginOpacityVoxelProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventEndOpacityVoxelProbes

The event triggered after the opacity voxel probes rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndOpacityVoxelProbes event handler
void endopacityvoxelprobes_event_handler()
{
	Log.Message("\Handling EndOpacityVoxelProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacityvoxelprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndOpacityVoxelProbes.Connect(endopacityvoxelprobes_event_connections, endopacityvoxelprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndOpacityVoxelProbes.Connect(endopacityvoxelprobes_event_connections, () => {
		Log.Message("Handling EndOpacityVoxelProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endopacityvoxelprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndOpacityVoxelProbes event with a handler function
Render.EventEndOpacityVoxelProbes.Connect(endopacityvoxelprobes_event_handler);

// remove subscription to the EndOpacityVoxelProbes event later by the handler function
Render.EventEndOpacityVoxelProbes.Disconnect(endopacityvoxelprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endopacityvoxelprobes_event_connection;

// subscribe to the EndOpacityVoxelProbes event with a lambda handler function and keeping the connection
endopacityvoxelprobes_event_connection = Render.EventEndOpacityVoxelProbes.Connect(() => {
		Log.Message("Handling EndOpacityVoxelProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endopacityvoxelprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endopacityvoxelprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endopacityvoxelprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndOpacityVoxelProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndOpacityVoxelProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndOpacityVoxelProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginOpacityEnvironmentProbes

The event triggered before the opacity environment probes rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginOpacityEnvironmentProbes event handler
void beginopacityenvironmentprobes_event_handler()
{
	Log.Message("\Handling BeginOpacityEnvironmentProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacityenvironmentprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginOpacityEnvironmentProbes.Connect(beginopacityenvironmentprobes_event_connections, beginopacityenvironmentprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginOpacityEnvironmentProbes.Connect(beginopacityenvironmentprobes_event_connections, () => {
		Log.Message("Handling BeginOpacityEnvironmentProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginopacityenvironmentprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginOpacityEnvironmentProbes event with a handler function
Render.EventBeginOpacityEnvironmentProbes.Connect(beginopacityenvironmentprobes_event_handler);

// remove subscription to the BeginOpacityEnvironmentProbes event later by the handler function
Render.EventBeginOpacityEnvironmentProbes.Disconnect(beginopacityenvironmentprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginopacityenvironmentprobes_event_connection;

// subscribe to the BeginOpacityEnvironmentProbes event with a lambda handler function and keeping the connection
beginopacityenvironmentprobes_event_connection = Render.EventBeginOpacityEnvironmentProbes.Connect(() => {
		Log.Message("Handling BeginOpacityEnvironmentProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginopacityenvironmentprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginopacityenvironmentprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginopacityenvironmentprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginOpacityEnvironmentProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginOpacityEnvironmentProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginOpacityEnvironmentProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventEndOpacityEnvironmentProbes

The event triggered after the opacity environment probes rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndOpacityEnvironmentProbes event handler
void endopacityenvironmentprobes_event_handler()
{
	Log.Message("\Handling EndOpacityEnvironmentProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacityenvironmentprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndOpacityEnvironmentProbes.Connect(endopacityenvironmentprobes_event_connections, endopacityenvironmentprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndOpacityEnvironmentProbes.Connect(endopacityenvironmentprobes_event_connections, () => {
		Log.Message("Handling EndOpacityEnvironmentProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endopacityenvironmentprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndOpacityEnvironmentProbes event with a handler function
Render.EventEndOpacityEnvironmentProbes.Connect(endopacityenvironmentprobes_event_handler);

// remove subscription to the EndOpacityEnvironmentProbes event later by the handler function
Render.EventEndOpacityEnvironmentProbes.Disconnect(endopacityenvironmentprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endopacityenvironmentprobes_event_connection;

// subscribe to the EndOpacityEnvironmentProbes event with a lambda handler function and keeping the connection
endopacityenvironmentprobes_event_connection = Render.EventEndOpacityEnvironmentProbes.Connect(() => {
		Log.Message("Handling EndOpacityEnvironmentProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endopacityenvironmentprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endopacityenvironmentprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endopacityenvironmentprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndOpacityEnvironmentProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndOpacityEnvironmentProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndOpacityEnvironmentProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginOpacityPlanarProbes

The event triggered before the opacity planar probes rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginOpacityPlanarProbes event handler
void beginopacityplanarprobes_event_handler()
{
	Log.Message("\Handling BeginOpacityPlanarProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginopacityplanarprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginOpacityPlanarProbes.Connect(beginopacityplanarprobes_event_connections, beginopacityplanarprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginOpacityPlanarProbes.Connect(beginopacityplanarprobes_event_connections, () => {
		Log.Message("Handling BeginOpacityPlanarProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginopacityplanarprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginOpacityPlanarProbes event with a handler function
Render.EventBeginOpacityPlanarProbes.Connect(beginopacityplanarprobes_event_handler);

// remove subscription to the BeginOpacityPlanarProbes event later by the handler function
Render.EventBeginOpacityPlanarProbes.Disconnect(beginopacityplanarprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginopacityplanarprobes_event_connection;

// subscribe to the BeginOpacityPlanarProbes event with a lambda handler function and keeping the connection
beginopacityplanarprobes_event_connection = Render.EventBeginOpacityPlanarProbes.Connect(() => {
		Log.Message("Handling BeginOpacityPlanarProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginopacityplanarprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginopacityplanarprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginopacityplanarprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginOpacityPlanarProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginOpacityPlanarProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginOpacityPlanarProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventEndOpacityPlanarProbes

The event triggered after the opacity planar probes rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndOpacityPlanarProbes event handler
void endopacityplanarprobes_event_handler()
{
	Log.Message("\Handling EndOpacityPlanarProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endopacityplanarprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndOpacityPlanarProbes.Connect(endopacityplanarprobes_event_connections, endopacityplanarprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndOpacityPlanarProbes.Connect(endopacityplanarprobes_event_connections, () => {
		Log.Message("Handling EndOpacityPlanarProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endopacityplanarprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndOpacityPlanarProbes event with a handler function
Render.EventEndOpacityPlanarProbes.Connect(endopacityplanarprobes_event_handler);

// remove subscription to the EndOpacityPlanarProbes event later by the handler function
Render.EventEndOpacityPlanarProbes.Disconnect(endopacityplanarprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endopacityplanarprobes_event_connection;

// subscribe to the EndOpacityPlanarProbes event with a lambda handler function and keeping the connection
endopacityplanarprobes_event_connection = Render.EventEndOpacityPlanarProbes.Connect(() => {
		Log.Message("Handling EndOpacityPlanarProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endopacityplanarprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endopacityplanarprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endopacityplanarprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndOpacityPlanarProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndOpacityPlanarProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndOpacityPlanarProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginRefractionBuffer

The event triggered before filling the refraction buffer. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginRefractionBuffer event handler
void beginrefractionbuffer_event_handler()
{
	Log.Message("\Handling BeginRefractionBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginrefractionbuffer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginRefractionBuffer.Connect(beginrefractionbuffer_event_connections, beginrefractionbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginRefractionBuffer.Connect(beginrefractionbuffer_event_connections, () => {
		Log.Message("Handling BeginRefractionBuffer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginrefractionbuffer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginRefractionBuffer event with a handler function
Render.EventBeginRefractionBuffer.Connect(beginrefractionbuffer_event_handler);

// remove subscription to the BeginRefractionBuffer event later by the handler function
Render.EventBeginRefractionBuffer.Disconnect(beginrefractionbuffer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginrefractionbuffer_event_connection;

// subscribe to the BeginRefractionBuffer event with a lambda handler function and keeping the connection
beginrefractionbuffer_event_connection = Render.EventBeginRefractionBuffer.Connect(() => {
		Log.Message("Handling BeginRefractionBuffer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginrefractionbuffer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginrefractionbuffer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginrefractionbuffer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginRefractionBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginRefractionBuffer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginRefractionBuffer.Enabled = true;

```

</details>

## 🔒︎ Event EventEndRefractionBuffer

The event triggered after filling the refraction buffer. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndRefractionBuffer event handler
void endrefractionbuffer_event_handler()
{
	Log.Message("\Handling EndRefractionBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endrefractionbuffer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndRefractionBuffer.Connect(endrefractionbuffer_event_connections, endrefractionbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndRefractionBuffer.Connect(endrefractionbuffer_event_connections, () => {
		Log.Message("Handling EndRefractionBuffer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endrefractionbuffer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndRefractionBuffer event with a handler function
Render.EventEndRefractionBuffer.Connect(endrefractionbuffer_event_handler);

// remove subscription to the EndRefractionBuffer event later by the handler function
Render.EventEndRefractionBuffer.Disconnect(endrefractionbuffer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endrefractionbuffer_event_connection;

// subscribe to the EndRefractionBuffer event with a lambda handler function and keeping the connection
endrefractionbuffer_event_connection = Render.EventEndRefractionBuffer.Connect(() => {
		Log.Message("Handling EndRefractionBuffer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endrefractionbuffer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endrefractionbuffer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endrefractionbuffer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndRefractionBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndRefractionBuffer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndRefractionBuffer.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginTransparentBlurBuffer

The event triggered before filling the transparent blur buffer. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginTransparentBlurBuffer event handler
void begintransparentblurbuffer_event_handler()
{
	Log.Message("\Handling BeginTransparentBlurBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begintransparentblurbuffer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginTransparentBlurBuffer.Connect(begintransparentblurbuffer_event_connections, begintransparentblurbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginTransparentBlurBuffer.Connect(begintransparentblurbuffer_event_connections, () => {
		Log.Message("Handling BeginTransparentBlurBuffer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begintransparentblurbuffer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginTransparentBlurBuffer event with a handler function
Render.EventBeginTransparentBlurBuffer.Connect(begintransparentblurbuffer_event_handler);

// remove subscription to the BeginTransparentBlurBuffer event later by the handler function
Render.EventBeginTransparentBlurBuffer.Disconnect(begintransparentblurbuffer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begintransparentblurbuffer_event_connection;

// subscribe to the BeginTransparentBlurBuffer event with a lambda handler function and keeping the connection
begintransparentblurbuffer_event_connection = Render.EventBeginTransparentBlurBuffer.Connect(() => {
		Log.Message("Handling BeginTransparentBlurBuffer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begintransparentblurbuffer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begintransparentblurbuffer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begintransparentblurbuffer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginTransparentBlurBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginTransparentBlurBuffer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginTransparentBlurBuffer.Enabled = true;

```

</details>

## 🔒︎ Event EventEndTransparentBlurBuffer

The event triggered after filling the transparent blur buffer. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndTransparentBlurBuffer event handler
void endtransparentblurbuffer_event_handler()
{
	Log.Message("\Handling EndTransparentBlurBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endtransparentblurbuffer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndTransparentBlurBuffer.Connect(endtransparentblurbuffer_event_connections, endtransparentblurbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndTransparentBlurBuffer.Connect(endtransparentblurbuffer_event_connections, () => {
		Log.Message("Handling EndTransparentBlurBuffer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endtransparentblurbuffer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndTransparentBlurBuffer event with a handler function
Render.EventEndTransparentBlurBuffer.Connect(endtransparentblurbuffer_event_handler);

// remove subscription to the EndTransparentBlurBuffer event later by the handler function
Render.EventEndTransparentBlurBuffer.Disconnect(endtransparentblurbuffer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endtransparentblurbuffer_event_connection;

// subscribe to the EndTransparentBlurBuffer event with a lambda handler function and keeping the connection
endtransparentblurbuffer_event_connection = Render.EventEndTransparentBlurBuffer.Connect(() => {
		Log.Message("Handling EndTransparentBlurBuffer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endtransparentblurbuffer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endtransparentblurbuffer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endtransparentblurbuffer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndTransparentBlurBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndTransparentBlurBuffer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndTransparentBlurBuffer.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSSSS

The event triggered before the Screen-Space Shadow Shafts rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSSSS event handler
void beginssss_event_handler()
{
	Log.Message("\Handling BeginSSSS event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginssss_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginSSSS.Connect(beginssss_event_connections, beginssss_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginSSSS.Connect(beginssss_event_connections, () => {
		Log.Message("Handling BeginSSSS event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginssss_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSSSS event with a handler function
Render.EventBeginSSSS.Connect(beginssss_event_handler);

// remove subscription to the BeginSSSS event later by the handler function
Render.EventBeginSSSS.Disconnect(beginssss_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginssss_event_connection;

// subscribe to the BeginSSSS event with a lambda handler function and keeping the connection
beginssss_event_connection = Render.EventBeginSSSS.Connect(() => {
		Log.Message("Handling BeginSSSS event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginssss_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginssss_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginssss_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSSSS events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginSSSS.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginSSSS.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSSSS

The event triggered after the Screen-Space Shadow Shafts rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSSSS event handler
void endssss_event_handler()
{
	Log.Message("\Handling EndSSSS event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endssss_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndSSSS.Connect(endssss_event_connections, endssss_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndSSSS.Connect(endssss_event_connections, () => {
		Log.Message("Handling EndSSSS event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endssss_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSSSS event with a handler function
Render.EventEndSSSS.Connect(endssss_event_handler);

// remove subscription to the EndSSSS event later by the handler function
Render.EventEndSSSS.Disconnect(endssss_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endssss_event_connection;

// subscribe to the EndSSSS event with a lambda handler function and keeping the connection
endssss_event_connection = Render.EventEndSSSS.Connect(() => {
		Log.Message("Handling EndSSSS event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endssss_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endssss_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endssss_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSSSS events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndSSSS.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndSSSS.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSSR

The event triggered before the SSR rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSSR event handler
void beginssr_event_handler()
{
	Log.Message("\Handling BeginSSR event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginssr_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginSSR.Connect(beginssr_event_connections, beginssr_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginSSR.Connect(beginssr_event_connections, () => {
		Log.Message("Handling BeginSSR event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginssr_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSSR event with a handler function
Render.EventBeginSSR.Connect(beginssr_event_handler);

// remove subscription to the BeginSSR event later by the handler function
Render.EventBeginSSR.Disconnect(beginssr_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginssr_event_connection;

// subscribe to the BeginSSR event with a lambda handler function and keeping the connection
beginssr_event_connection = Render.EventBeginSSR.Connect(() => {
		Log.Message("Handling BeginSSR event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginssr_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginssr_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginssr_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSSR events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginSSR.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginSSR.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSSR

The event triggered after the SSR rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSSR event handler
void endssr_event_handler()
{
	Log.Message("\Handling EndSSR event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endssr_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndSSR.Connect(endssr_event_connections, endssr_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndSSR.Connect(endssr_event_connections, () => {
		Log.Message("Handling EndSSR event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endssr_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSSR event with a handler function
Render.EventEndSSR.Connect(endssr_event_handler);

// remove subscription to the EndSSR event later by the handler function
Render.EventEndSSR.Disconnect(endssr_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endssr_event_connection;

// subscribe to the EndSSR event with a lambda handler function and keeping the connection
endssr_event_connection = Render.EventEndSSR.Connect(() => {
		Log.Message("Handling EndSSR event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endssr_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endssr_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endssr_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSSR events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndSSR.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndSSR.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSSAO

The event triggered before the SSAO rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSSAO event handler
void beginssao_event_handler()
{
	Log.Message("\Handling BeginSSAO event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginssao_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginSSAO.Connect(beginssao_event_connections, beginssao_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginSSAO.Connect(beginssao_event_connections, () => {
		Log.Message("Handling BeginSSAO event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginssao_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSSAO event with a handler function
Render.EventBeginSSAO.Connect(beginssao_event_handler);

// remove subscription to the BeginSSAO event later by the handler function
Render.EventBeginSSAO.Disconnect(beginssao_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginssao_event_connection;

// subscribe to the BeginSSAO event with a lambda handler function and keeping the connection
beginssao_event_connection = Render.EventBeginSSAO.Connect(() => {
		Log.Message("Handling BeginSSAO event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginssao_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginssao_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginssao_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSSAO events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginSSAO.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginSSAO.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSSAO

The event triggered after the SSAO rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSSAO event handler
void endssao_event_handler()
{
	Log.Message("\Handling EndSSAO event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endssao_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndSSAO.Connect(endssao_event_connections, endssao_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndSSAO.Connect(endssao_event_connections, () => {
		Log.Message("Handling EndSSAO event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endssao_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSSAO event with a handler function
Render.EventEndSSAO.Connect(endssao_event_handler);

// remove subscription to the EndSSAO event later by the handler function
Render.EventEndSSAO.Disconnect(endssao_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endssao_event_connection;

// subscribe to the EndSSAO event with a lambda handler function and keeping the connection
endssao_event_connection = Render.EventEndSSAO.Connect(() => {
		Log.Message("Handling EndSSAO event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endssao_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endssao_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endssao_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSSAO events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndSSAO.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndSSAO.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSSGI

The event triggered before the SSGI rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSSGI event handler
void beginssgi_event_handler()
{
	Log.Message("\Handling BeginSSGI event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginssgi_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginSSGI.Connect(beginssgi_event_connections, beginssgi_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginSSGI.Connect(beginssgi_event_connections, () => {
		Log.Message("Handling BeginSSGI event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginssgi_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSSGI event with a handler function
Render.EventBeginSSGI.Connect(beginssgi_event_handler);

// remove subscription to the BeginSSGI event later by the handler function
Render.EventBeginSSGI.Disconnect(beginssgi_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginssgi_event_connection;

// subscribe to the BeginSSGI event with a lambda handler function and keeping the connection
beginssgi_event_connection = Render.EventBeginSSGI.Connect(() => {
		Log.Message("Handling BeginSSGI event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginssgi_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginssgi_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginssgi_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSSGI events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginSSGI.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginSSGI.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSSGI

The event triggered after the SSGI rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSSGI event handler
void endssgi_event_handler()
{
	Log.Message("\Handling EndSSGI event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endssgi_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndSSGI.Connect(endssgi_event_connections, endssgi_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndSSGI.Connect(endssgi_event_connections, () => {
		Log.Message("Handling EndSSGI event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endssgi_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSSGI event with a handler function
Render.EventEndSSGI.Connect(endssgi_event_handler);

// remove subscription to the EndSSGI event later by the handler function
Render.EventEndSSGI.Disconnect(endssgi_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endssgi_event_connection;

// subscribe to the EndSSGI event with a lambda handler function and keeping the connection
endssgi_event_connection = Render.EventEndSSGI.Connect(() => {
		Log.Message("Handling EndSSGI event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endssgi_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endssgi_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endssgi_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSSGI events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndSSGI.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndSSGI.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSky

The event triggered before the sky rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSky event handler
void beginsky_event_handler()
{
	Log.Message("\Handling BeginSky event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsky_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginSky.Connect(beginsky_event_connections, beginsky_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginSky.Connect(beginsky_event_connections, () => {
		Log.Message("Handling BeginSky event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginsky_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSky event with a handler function
Render.EventBeginSky.Connect(beginsky_event_handler);

// remove subscription to the BeginSky event later by the handler function
Render.EventBeginSky.Disconnect(beginsky_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginsky_event_connection;

// subscribe to the BeginSky event with a lambda handler function and keeping the connection
beginsky_event_connection = Render.EventBeginSky.Connect(() => {
		Log.Message("Handling BeginSky event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginsky_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginsky_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginsky_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSky events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginSky.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginSky.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSky

The event triggered after the sky rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSky event handler
void endsky_event_handler()
{
	Log.Message("\Handling EndSky event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsky_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndSky.Connect(endsky_event_connections, endsky_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndSky.Connect(endsky_event_connections, () => {
		Log.Message("Handling EndSky event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endsky_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSky event with a handler function
Render.EventEndSky.Connect(endsky_event_handler);

// remove subscription to the EndSky event later by the handler function
Render.EventEndSky.Disconnect(endsky_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endsky_event_connection;

// subscribe to the EndSky event with a lambda handler function and keeping the connection
endsky_event_connection = Render.EventEndSky.Connect(() => {
		Log.Message("Handling EndSky event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endsky_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endsky_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endsky_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSky events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndSky.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndSky.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginCompositeDeferred

The event triggered before the clouds deferred composite stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginCompositeDeferred event handler
void begincompositedeferred_event_handler()
{
	Log.Message("\Handling BeginCompositeDeferred event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begincompositedeferred_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginCompositeDeferred.Connect(begincompositedeferred_event_connections, begincompositedeferred_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginCompositeDeferred.Connect(begincompositedeferred_event_connections, () => {
		Log.Message("Handling BeginCompositeDeferred event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begincompositedeferred_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginCompositeDeferred event with a handler function
Render.EventBeginCompositeDeferred.Connect(begincompositedeferred_event_handler);

// remove subscription to the BeginCompositeDeferred event later by the handler function
Render.EventBeginCompositeDeferred.Disconnect(begincompositedeferred_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begincompositedeferred_event_connection;

// subscribe to the BeginCompositeDeferred event with a lambda handler function and keeping the connection
begincompositedeferred_event_connection = Render.EventBeginCompositeDeferred.Connect(() => {
		Log.Message("Handling BeginCompositeDeferred event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begincompositedeferred_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begincompositedeferred_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begincompositedeferred_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginCompositeDeferred events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginCompositeDeferred.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginCompositeDeferred.Enabled = true;

```

</details>

## 🔒︎ Event EventEndCompositeDeferred

The event triggered after the clouds deferred composite stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndCompositeDeferred event handler
void endcompositedeferred_event_handler()
{
	Log.Message("\Handling EndCompositeDeferred event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endcompositedeferred_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndCompositeDeferred.Connect(endcompositedeferred_event_connections, endcompositedeferred_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndCompositeDeferred.Connect(endcompositedeferred_event_connections, () => {
		Log.Message("Handling EndCompositeDeferred event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endcompositedeferred_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndCompositeDeferred event with a handler function
Render.EventEndCompositeDeferred.Connect(endcompositedeferred_event_handler);

// remove subscription to the EndCompositeDeferred event later by the handler function
Render.EventEndCompositeDeferred.Disconnect(endcompositedeferred_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endcompositedeferred_event_connection;

// subscribe to the EndCompositeDeferred event with a lambda handler function and keeping the connection
endcompositedeferred_event_connection = Render.EventEndCompositeDeferred.Connect(() => {
		Log.Message("Handling EndCompositeDeferred event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endcompositedeferred_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endcompositedeferred_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endcompositedeferred_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndCompositeDeferred events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndCompositeDeferred.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndCompositeDeferred.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginTransparent

The event triggered before the transparent objects rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginTransparent event handler
void begintransparent_event_handler()
{
	Log.Message("\Handling BeginTransparent event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begintransparent_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginTransparent.Connect(begintransparent_event_connections, begintransparent_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginTransparent.Connect(begintransparent_event_connections, () => {
		Log.Message("Handling BeginTransparent event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begintransparent_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginTransparent event with a handler function
Render.EventBeginTransparent.Connect(begintransparent_event_handler);

// remove subscription to the BeginTransparent event later by the handler function
Render.EventBeginTransparent.Disconnect(begintransparent_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begintransparent_event_connection;

// subscribe to the BeginTransparent event with a lambda handler function and keeping the connection
begintransparent_event_connection = Render.EventBeginTransparent.Connect(() => {
		Log.Message("Handling BeginTransparent event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begintransparent_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begintransparent_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begintransparent_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginTransparent events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginTransparent.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginTransparent.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginClouds

The event triggered before the clouds rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginClouds event handler
void beginclouds_event_handler()
{
	Log.Message("\Handling BeginClouds event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginclouds_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginClouds.Connect(beginclouds_event_connections, beginclouds_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginClouds.Connect(beginclouds_event_connections, () => {
		Log.Message("Handling BeginClouds event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginclouds_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginClouds event with a handler function
Render.EventBeginClouds.Connect(beginclouds_event_handler);

// remove subscription to the BeginClouds event later by the handler function
Render.EventBeginClouds.Disconnect(beginclouds_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginclouds_event_connection;

// subscribe to the BeginClouds event with a lambda handler function and keeping the connection
beginclouds_event_connection = Render.EventBeginClouds.Connect(() => {
		Log.Message("Handling BeginClouds event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginclouds_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginclouds_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginclouds_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginClouds events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginClouds.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginClouds.Enabled = true;

```

</details>

## 🔒︎ Event EventEndClouds

The event triggered after the clouds rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndClouds event handler
void endclouds_event_handler()
{
	Log.Message("\Handling EndClouds event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endclouds_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndClouds.Connect(endclouds_event_connections, endclouds_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndClouds.Connect(endclouds_event_connections, () => {
		Log.Message("Handling EndClouds event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endclouds_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndClouds event with a handler function
Render.EventEndClouds.Connect(endclouds_event_handler);

// remove subscription to the EndClouds event later by the handler function
Render.EventEndClouds.Disconnect(endclouds_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endclouds_event_connection;

// subscribe to the EndClouds event with a lambda handler function and keeping the connection
endclouds_event_connection = Render.EventEndClouds.Connect(() => {
		Log.Message("Handling EndClouds event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endclouds_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endclouds_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endclouds_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndClouds events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndClouds.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndClouds.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWater

The event triggered before the water rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWater event handler
void beginwater_event_handler()
{
	Log.Message("\Handling BeginWater event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwater_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginWater.Connect(beginwater_event_connections, beginwater_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginWater.Connect(beginwater_event_connections, () => {
		Log.Message("Handling BeginWater event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginwater_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWater event with a handler function
Render.EventBeginWater.Connect(beginwater_event_handler);

// remove subscription to the BeginWater event later by the handler function
Render.EventBeginWater.Disconnect(beginwater_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginwater_event_connection;

// subscribe to the BeginWater event with a lambda handler function and keeping the connection
beginwater_event_connection = Render.EventBeginWater.Connect(() => {
		Log.Message("Handling BeginWater event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginwater_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginwater_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginwater_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWater events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginWater.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginWater.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWaterGBuffer

The event triggered before the Water G-Buffer rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWaterGBuffer event handler
void beginwatergbuffer_event_handler()
{
	Log.Message("\Handling BeginWaterGBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwatergbuffer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventBeginWaterGBuffer.Connect(beginwatergbuffer_event_connections, beginwatergbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventBeginWaterGBuffer.Connect(beginwatergbuffer_event_connections, () => {
		Log.Message("Handling BeginWaterGBuffer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginwatergbuffer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWaterGBuffer event with a handler function
publisher.EventBeginWaterGBuffer.Connect(beginwatergbuffer_event_handler);

// remove subscription to the BeginWaterGBuffer event later by the handler function
publisher.EventBeginWaterGBuffer.Disconnect(beginwatergbuffer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginwatergbuffer_event_connection;

// subscribe to the BeginWaterGBuffer event with a lambda handler function and keeping the connection
beginwatergbuffer_event_connection = publisher.EventBeginWaterGBuffer.Connect(() => {
		Log.Message("Handling BeginWaterGBuffer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginwatergbuffer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginwatergbuffer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginwatergbuffer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWaterGBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventBeginWaterGBuffer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventBeginWaterGBuffer.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWaterGBuffer

The event triggered after the Water G-Buffer rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWaterGBuffer event handler
void endwatergbuffer_event_handler()
{
	Log.Message("\Handling EndWaterGBuffer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwatergbuffer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndWaterGBuffer.Connect(endwatergbuffer_event_connections, endwatergbuffer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndWaterGBuffer.Connect(endwatergbuffer_event_connections, () => {
		Log.Message("Handling EndWaterGBuffer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endwatergbuffer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWaterGBuffer event with a handler function
publisher.EventEndWaterGBuffer.Connect(endwatergbuffer_event_handler);

// remove subscription to the EndWaterGBuffer event later by the handler function
publisher.EventEndWaterGBuffer.Disconnect(endwatergbuffer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endwatergbuffer_event_connection;

// subscribe to the EndWaterGBuffer event with a lambda handler function and keeping the connection
endwatergbuffer_event_connection = publisher.EventEndWaterGBuffer.Connect(() => {
		Log.Message("Handling EndWaterGBuffer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endwatergbuffer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endwatergbuffer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endwatergbuffer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWaterGBuffer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndWaterGBuffer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndWaterGBuffer.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWaterDecals

The event triggered before the water decals rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWaterDecals event handler
void beginwaterdecals_event_handler()
{
	Log.Message("\Handling BeginWaterDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwaterdecals_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginWaterDecals.Connect(beginwaterdecals_event_connections, beginwaterdecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginWaterDecals.Connect(beginwaterdecals_event_connections, () => {
		Log.Message("Handling BeginWaterDecals event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginwaterdecals_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWaterDecals event with a handler function
Render.EventBeginWaterDecals.Connect(beginwaterdecals_event_handler);

// remove subscription to the BeginWaterDecals event later by the handler function
Render.EventBeginWaterDecals.Disconnect(beginwaterdecals_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginwaterdecals_event_connection;

// subscribe to the BeginWaterDecals event with a lambda handler function and keeping the connection
beginwaterdecals_event_connection = Render.EventBeginWaterDecals.Connect(() => {
		Log.Message("Handling BeginWaterDecals event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginwaterdecals_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginwaterdecals_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginwaterdecals_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWaterDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginWaterDecals.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginWaterDecals.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWaterDecals

The event triggered after the water decals rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWaterDecals event handler
void endwaterdecals_event_handler()
{
	Log.Message("\Handling EndWaterDecals event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwaterdecals_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndWaterDecals.Connect(endwaterdecals_event_connections, endwaterdecals_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndWaterDecals.Connect(endwaterdecals_event_connections, () => {
		Log.Message("Handling EndWaterDecals event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endwaterdecals_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWaterDecals event with a handler function
Render.EventEndWaterDecals.Connect(endwaterdecals_event_handler);

// remove subscription to the EndWaterDecals event later by the handler function
Render.EventEndWaterDecals.Disconnect(endwaterdecals_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endwaterdecals_event_connection;

// subscribe to the EndWaterDecals event with a lambda handler function and keeping the connection
endwaterdecals_event_connection = Render.EventEndWaterDecals.Connect(() => {
		Log.Message("Handling EndWaterDecals event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endwaterdecals_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endwaterdecals_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endwaterdecals_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWaterDecals events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndWaterDecals.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndWaterDecals.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWaterLights

The event triggered before the water lights rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWaterLights event handler
void beginwaterlights_event_handler()
{
	Log.Message("\Handling BeginWaterLights event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwaterlights_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginWaterLights.Connect(beginwaterlights_event_connections, beginwaterlights_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginWaterLights.Connect(beginwaterlights_event_connections, () => {
		Log.Message("Handling BeginWaterLights event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginwaterlights_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWaterLights event with a handler function
Render.EventBeginWaterLights.Connect(beginwaterlights_event_handler);

// remove subscription to the BeginWaterLights event later by the handler function
Render.EventBeginWaterLights.Disconnect(beginwaterlights_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginwaterlights_event_connection;

// subscribe to the BeginWaterLights event with a lambda handler function and keeping the connection
beginwaterlights_event_connection = Render.EventBeginWaterLights.Connect(() => {
		Log.Message("Handling BeginWaterLights event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginwaterlights_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginwaterlights_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginwaterlights_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWaterLights events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginWaterLights.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginWaterLights.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWaterLights

The event triggered after the water lights rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWaterLights event handler
void endwaterlights_event_handler()
{
	Log.Message("\Handling EndWaterLights event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwaterlights_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndWaterLights.Connect(endwaterlights_event_connections, endwaterlights_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndWaterLights.Connect(endwaterlights_event_connections, () => {
		Log.Message("Handling EndWaterLights event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endwaterlights_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWaterLights event with a handler function
Render.EventEndWaterLights.Connect(endwaterlights_event_handler);

// remove subscription to the EndWaterLights event later by the handler function
Render.EventEndWaterLights.Disconnect(endwaterlights_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endwaterlights_event_connection;

// subscribe to the EndWaterLights event with a lambda handler function and keeping the connection
endwaterlights_event_connection = Render.EventEndWaterLights.Connect(() => {
		Log.Message("Handling EndWaterLights event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endwaterlights_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endwaterlights_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endwaterlights_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWaterLights events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndWaterLights.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndWaterLights.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWaterVoxelProbes

The event triggered before the water voxel probes rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWaterVoxelProbes event handler
void beginwatervoxelprobes_event_handler()
{
	Log.Message("\Handling BeginWaterVoxelProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwatervoxelprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginWaterVoxelProbes.Connect(beginwatervoxelprobes_event_connections, beginwatervoxelprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginWaterVoxelProbes.Connect(beginwatervoxelprobes_event_connections, () => {
		Log.Message("Handling BeginWaterVoxelProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginwatervoxelprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWaterVoxelProbes event with a handler function
Render.EventBeginWaterVoxelProbes.Connect(beginwatervoxelprobes_event_handler);

// remove subscription to the BeginWaterVoxelProbes event later by the handler function
Render.EventBeginWaterVoxelProbes.Disconnect(beginwatervoxelprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginwatervoxelprobes_event_connection;

// subscribe to the BeginWaterVoxelProbes event with a lambda handler function and keeping the connection
beginwatervoxelprobes_event_connection = Render.EventBeginWaterVoxelProbes.Connect(() => {
		Log.Message("Handling BeginWaterVoxelProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginwatervoxelprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginwatervoxelprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginwatervoxelprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWaterVoxelProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginWaterVoxelProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginWaterVoxelProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWaterVoxelProbes

The event triggered after the water voxel probes rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWaterVoxelProbes event handler
void endwatervoxelprobes_event_handler()
{
	Log.Message("\Handling EndWaterVoxelProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwatervoxelprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndWaterVoxelProbes.Connect(endwatervoxelprobes_event_connections, endwatervoxelprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndWaterVoxelProbes.Connect(endwatervoxelprobes_event_connections, () => {
		Log.Message("Handling EndWaterVoxelProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endwatervoxelprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWaterVoxelProbes event with a handler function
Render.EventEndWaterVoxelProbes.Connect(endwatervoxelprobes_event_handler);

// remove subscription to the EndWaterVoxelProbes event later by the handler function
Render.EventEndWaterVoxelProbes.Disconnect(endwatervoxelprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endwatervoxelprobes_event_connection;

// subscribe to the EndWaterVoxelProbes event with a lambda handler function and keeping the connection
endwatervoxelprobes_event_connection = Render.EventEndWaterVoxelProbes.Connect(() => {
		Log.Message("Handling EndWaterVoxelProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endwatervoxelprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endwatervoxelprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endwatervoxelprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWaterVoxelProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndWaterVoxelProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndWaterVoxelProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWaterEnvironmentProbes

The event triggered before the water environment probes rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWaterEnvironmentProbes event handler
void beginwaterenvironmentprobes_event_handler()
{
	Log.Message("\Handling BeginWaterEnvironmentProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwaterenvironmentprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginWaterEnvironmentProbes.Connect(beginwaterenvironmentprobes_event_connections, beginwaterenvironmentprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginWaterEnvironmentProbes.Connect(beginwaterenvironmentprobes_event_connections, () => {
		Log.Message("Handling BeginWaterEnvironmentProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginwaterenvironmentprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWaterEnvironmentProbes event with a handler function
Render.EventBeginWaterEnvironmentProbes.Connect(beginwaterenvironmentprobes_event_handler);

// remove subscription to the BeginWaterEnvironmentProbes event later by the handler function
Render.EventBeginWaterEnvironmentProbes.Disconnect(beginwaterenvironmentprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginwaterenvironmentprobes_event_connection;

// subscribe to the BeginWaterEnvironmentProbes event with a lambda handler function and keeping the connection
beginwaterenvironmentprobes_event_connection = Render.EventBeginWaterEnvironmentProbes.Connect(() => {
		Log.Message("Handling BeginWaterEnvironmentProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginwaterenvironmentprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginwaterenvironmentprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginwaterenvironmentprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWaterEnvironmentProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginWaterEnvironmentProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginWaterEnvironmentProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWaterEnvironmentProbes

The event triggered after the water environment probes rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWaterEnvironmentProbes event handler
void endwaterenvironmentprobes_event_handler()
{
	Log.Message("\Handling EndWaterEnvironmentProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwaterenvironmentprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndWaterEnvironmentProbes.Connect(endwaterenvironmentprobes_event_connections, endwaterenvironmentprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndWaterEnvironmentProbes.Connect(endwaterenvironmentprobes_event_connections, () => {
		Log.Message("Handling EndWaterEnvironmentProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endwaterenvironmentprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWaterEnvironmentProbes event with a handler function
Render.EventEndWaterEnvironmentProbes.Connect(endwaterenvironmentprobes_event_handler);

// remove subscription to the EndWaterEnvironmentProbes event later by the handler function
Render.EventEndWaterEnvironmentProbes.Disconnect(endwaterenvironmentprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endwaterenvironmentprobes_event_connection;

// subscribe to the EndWaterEnvironmentProbes event with a lambda handler function and keeping the connection
endwaterenvironmentprobes_event_connection = Render.EventEndWaterEnvironmentProbes.Connect(() => {
		Log.Message("Handling EndWaterEnvironmentProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endwaterenvironmentprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endwaterenvironmentprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endwaterenvironmentprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWaterEnvironmentProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndWaterEnvironmentProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndWaterEnvironmentProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginWaterPlanarProbes

The event triggered before the water planar probes rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginWaterPlanarProbes event handler
void beginwaterplanarprobes_event_handler()
{
	Log.Message("\Handling BeginWaterPlanarProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginwaterplanarprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginWaterPlanarProbes.Connect(beginwaterplanarprobes_event_connections, beginwaterplanarprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginWaterPlanarProbes.Connect(beginwaterplanarprobes_event_connections, () => {
		Log.Message("Handling BeginWaterPlanarProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginwaterplanarprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginWaterPlanarProbes event with a handler function
Render.EventBeginWaterPlanarProbes.Connect(beginwaterplanarprobes_event_handler);

// remove subscription to the BeginWaterPlanarProbes event later by the handler function
Render.EventBeginWaterPlanarProbes.Disconnect(beginwaterplanarprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginwaterplanarprobes_event_connection;

// subscribe to the BeginWaterPlanarProbes event with a lambda handler function and keeping the connection
beginwaterplanarprobes_event_connection = Render.EventBeginWaterPlanarProbes.Connect(() => {
		Log.Message("Handling BeginWaterPlanarProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginwaterplanarprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginwaterplanarprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginwaterplanarprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginWaterPlanarProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginWaterPlanarProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginWaterPlanarProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWaterPlanarProbes

The event triggered after the water planar probes rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWaterPlanarProbes event handler
void endwaterplanarprobes_event_handler()
{
	Log.Message("\Handling EndWaterPlanarProbes event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwaterplanarprobes_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndWaterPlanarProbes.Connect(endwaterplanarprobes_event_connections, endwaterplanarprobes_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndWaterPlanarProbes.Connect(endwaterplanarprobes_event_connections, () => {
		Log.Message("Handling EndWaterPlanarProbes event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endwaterplanarprobes_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWaterPlanarProbes event with a handler function
Render.EventEndWaterPlanarProbes.Connect(endwaterplanarprobes_event_handler);

// remove subscription to the EndWaterPlanarProbes event later by the handler function
Render.EventEndWaterPlanarProbes.Disconnect(endwaterplanarprobes_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endwaterplanarprobes_event_connection;

// subscribe to the EndWaterPlanarProbes event with a lambda handler function and keeping the connection
endwaterplanarprobes_event_connection = Render.EventEndWaterPlanarProbes.Connect(() => {
		Log.Message("Handling EndWaterPlanarProbes event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endwaterplanarprobes_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endwaterplanarprobes_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endwaterplanarprobes_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWaterPlanarProbes events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndWaterPlanarProbes.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndWaterPlanarProbes.Enabled = true;

```

</details>

## 🔒︎ Event EventEndWater

The event triggered after the water rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndWater event handler
void endwater_event_handler()
{
	Log.Message("\Handling EndWater event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endwater_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndWater.Connect(endwater_event_connections, endwater_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndWater.Connect(endwater_event_connections, () => {
		Log.Message("Handling EndWater event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endwater_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndWater event with a handler function
Render.EventEndWater.Connect(endwater_event_handler);

// remove subscription to the EndWater event later by the handler function
Render.EventEndWater.Disconnect(endwater_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endwater_event_connection;

// subscribe to the EndWater event with a lambda handler function and keeping the connection
endwater_event_connection = Render.EventEndWater.Connect(() => {
		Log.Message("Handling EndWater event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endwater_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endwater_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endwater_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndWater events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndWater.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndWater.Enabled = true;

```

</details>

## 🔒︎ Event EventEndTransparent

The event triggered after the transparent objects rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndTransparent event handler
void endtransparent_event_handler()
{
	Log.Message("\Handling EndTransparent event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endtransparent_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndTransparent.Connect(endtransparent_event_connections, endtransparent_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndTransparent.Connect(endtransparent_event_connections, () => {
		Log.Message("Handling EndTransparent event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endtransparent_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndTransparent event with a handler function
Render.EventEndTransparent.Connect(endtransparent_event_handler);

// remove subscription to the EndTransparent event later by the handler function
Render.EventEndTransparent.Disconnect(endtransparent_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endtransparent_event_connection;

// subscribe to the EndTransparent event with a lambda handler function and keeping the connection
endtransparent_event_connection = Render.EventEndTransparent.Connect(() => {
		Log.Message("Handling EndTransparent event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endtransparent_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endtransparent_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endtransparent_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndTransparent events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndTransparent.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndTransparent.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginSrgbCorrection

The event triggered before the sRGB correction stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginSrgbCorrection event handler
void beginsrgbcorrection_event_handler()
{
	Log.Message("\Handling BeginSrgbCorrection event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginsrgbcorrection_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginSrgbCorrection.Connect(beginsrgbcorrection_event_connections, beginsrgbcorrection_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginSrgbCorrection.Connect(beginsrgbcorrection_event_connections, () => {
		Log.Message("Handling BeginSrgbCorrection event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginsrgbcorrection_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginSrgbCorrection event with a handler function
Render.EventBeginSrgbCorrection.Connect(beginsrgbcorrection_event_handler);

// remove subscription to the BeginSrgbCorrection event later by the handler function
Render.EventBeginSrgbCorrection.Disconnect(beginsrgbcorrection_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginsrgbcorrection_event_connection;

// subscribe to the BeginSrgbCorrection event with a lambda handler function and keeping the connection
beginsrgbcorrection_event_connection = Render.EventBeginSrgbCorrection.Connect(() => {
		Log.Message("Handling BeginSrgbCorrection event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginsrgbcorrection_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginsrgbcorrection_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginsrgbcorrection_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginSrgbCorrection events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginSrgbCorrection.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginSrgbCorrection.Enabled = true;

```

</details>

## 🔒︎ Event EventEndSrgbCorrection

The event triggered after the sRGB correction stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndSrgbCorrection event handler
void endsrgbcorrection_event_handler()
{
	Log.Message("\Handling EndSrgbCorrection event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endsrgbcorrection_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndSrgbCorrection.Connect(endsrgbcorrection_event_connections, endsrgbcorrection_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndSrgbCorrection.Connect(endsrgbcorrection_event_connections, () => {
		Log.Message("Handling EndSrgbCorrection event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endsrgbcorrection_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndSrgbCorrection event with a handler function
Render.EventEndSrgbCorrection.Connect(endsrgbcorrection_event_handler);

// remove subscription to the EndSrgbCorrection event later by the handler function
Render.EventEndSrgbCorrection.Disconnect(endsrgbcorrection_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endsrgbcorrection_event_connection;

// subscribe to the EndSrgbCorrection event with a lambda handler function and keeping the connection
endsrgbcorrection_event_connection = Render.EventEndSrgbCorrection.Connect(() => {
		Log.Message("Handling EndSrgbCorrection event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endsrgbcorrection_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endsrgbcorrection_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endsrgbcorrection_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndSrgbCorrection events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndSrgbCorrection.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndSrgbCorrection.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginAdaptationColorAverage

The event triggered before the calculation of automatic exposure and white balance correction. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginAdaptationColorAverage event handler
void beginadaptationcoloraverage_event_handler()
{
	Log.Message("\Handling BeginAdaptationColorAverage event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginadaptationcoloraverage_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginAdaptationColorAverage.Connect(beginadaptationcoloraverage_event_connections, beginadaptationcoloraverage_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginAdaptationColorAverage.Connect(beginadaptationcoloraverage_event_connections, () => {
		Log.Message("Handling BeginAdaptationColorAverage event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginadaptationcoloraverage_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginAdaptationColorAverage event with a handler function
Render.EventBeginAdaptationColorAverage.Connect(beginadaptationcoloraverage_event_handler);

// remove subscription to the BeginAdaptationColorAverage event later by the handler function
Render.EventBeginAdaptationColorAverage.Disconnect(beginadaptationcoloraverage_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginadaptationcoloraverage_event_connection;

// subscribe to the BeginAdaptationColorAverage event with a lambda handler function and keeping the connection
beginadaptationcoloraverage_event_connection = Render.EventBeginAdaptationColorAverage.Connect(() => {
		Log.Message("Handling BeginAdaptationColorAverage event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginadaptationcoloraverage_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginadaptationcoloraverage_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginadaptationcoloraverage_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginAdaptationColorAverage events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginAdaptationColorAverage.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginAdaptationColorAverage.Enabled = true;

```

</details>

## 🔒︎ Event EventEndAdaptationColorAverage

The event triggered after the calculation of automatic exposure and white balance correction. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndAdaptationColorAverage event handler
void endadaptationcoloraverage_event_handler()
{
	Log.Message("\Handling EndAdaptationColorAverage event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endadaptationcoloraverage_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndAdaptationColorAverage.Connect(endadaptationcoloraverage_event_connections, endadaptationcoloraverage_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndAdaptationColorAverage.Connect(endadaptationcoloraverage_event_connections, () => {
		Log.Message("Handling EndAdaptationColorAverage event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endadaptationcoloraverage_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndAdaptationColorAverage event with a handler function
Render.EventEndAdaptationColorAverage.Connect(endadaptationcoloraverage_event_handler);

// remove subscription to the EndAdaptationColorAverage event later by the handler function
Render.EventEndAdaptationColorAverage.Disconnect(endadaptationcoloraverage_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endadaptationcoloraverage_event_connection;

// subscribe to the EndAdaptationColorAverage event with a lambda handler function and keeping the connection
endadaptationcoloraverage_event_connection = Render.EventEndAdaptationColorAverage.Connect(() => {
		Log.Message("Handling EndAdaptationColorAverage event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endadaptationcoloraverage_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endadaptationcoloraverage_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endadaptationcoloraverage_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndAdaptationColorAverage events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndAdaptationColorAverage.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndAdaptationColorAverage.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginAdaptationColor

The event triggered before the color adaptation rendering stage (automatic exposure and white balance correction). You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginAdaptationColor event handler
void beginadaptationcolor_event_handler()
{
	Log.Message("\Handling BeginAdaptationColor event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginadaptationcolor_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginAdaptationColor.Connect(beginadaptationcolor_event_connections, beginadaptationcolor_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginAdaptationColor.Connect(beginadaptationcolor_event_connections, () => {
		Log.Message("Handling BeginAdaptationColor event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginadaptationcolor_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginAdaptationColor event with a handler function
Render.EventBeginAdaptationColor.Connect(beginadaptationcolor_event_handler);

// remove subscription to the BeginAdaptationColor event later by the handler function
Render.EventBeginAdaptationColor.Disconnect(beginadaptationcolor_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginadaptationcolor_event_connection;

// subscribe to the BeginAdaptationColor event with a lambda handler function and keeping the connection
beginadaptationcolor_event_connection = Render.EventBeginAdaptationColor.Connect(() => {
		Log.Message("Handling BeginAdaptationColor event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginadaptationcolor_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginadaptationcolor_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginadaptationcolor_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginAdaptationColor events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginAdaptationColor.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginAdaptationColor.Enabled = true;

```

</details>

## 🔒︎ Event EventEndAdaptationColor

The event triggered after the color adaptation rendering stage (automatic exposure and white balance correction). You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndAdaptationColor event handler
void endadaptationcolor_event_handler()
{
	Log.Message("\Handling EndAdaptationColor event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endadaptationcolor_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndAdaptationColor.Connect(endadaptationcolor_event_connections, endadaptationcolor_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndAdaptationColor.Connect(endadaptationcolor_event_connections, () => {
		Log.Message("Handling EndAdaptationColor event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endadaptationcolor_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndAdaptationColor event with a handler function
Render.EventEndAdaptationColor.Connect(endadaptationcolor_event_handler);

// remove subscription to the EndAdaptationColor event later by the handler function
Render.EventEndAdaptationColor.Disconnect(endadaptationcolor_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endadaptationcolor_event_connection;

// subscribe to the EndAdaptationColor event with a lambda handler function and keeping the connection
endadaptationcolor_event_connection = Render.EventEndAdaptationColor.Connect(() => {
		Log.Message("Handling EndAdaptationColor event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endadaptationcolor_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endadaptationcolor_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endadaptationcolor_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndAdaptationColor events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndAdaptationColor.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndAdaptationColor.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginTAA

The event triggered before the Temporal Anti-Aliasing (TAA) pass. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginTAA event handler
void begintaa_event_handler()
{
	Log.Message("\Handling BeginTAA event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begintaa_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginTAA.Connect(begintaa_event_connections, begintaa_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginTAA.Connect(begintaa_event_connections, () => {
		Log.Message("Handling BeginTAA event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begintaa_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginTAA event with a handler function
Render.EventBeginTAA.Connect(begintaa_event_handler);

// remove subscription to the BeginTAA event later by the handler function
Render.EventBeginTAA.Disconnect(begintaa_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begintaa_event_connection;

// subscribe to the BeginTAA event with a lambda handler function and keeping the connection
begintaa_event_connection = Render.EventBeginTAA.Connect(() => {
		Log.Message("Handling BeginTAA event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begintaa_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begintaa_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begintaa_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginTAA events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginTAA.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginTAA.Enabled = true;

```

</details>

## 🔒︎ Event EventEndTAA

The event triggered after the Temporal Anti-Aliasing (TAA) pass. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndTAA event handler
void endtaa_event_handler()
{
	Log.Message("\Handling EndTAA event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endtaa_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndTAA.Connect(endtaa_event_connections, endtaa_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndTAA.Connect(endtaa_event_connections, () => {
		Log.Message("Handling EndTAA event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endtaa_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndTAA event with a handler function
Render.EventEndTAA.Connect(endtaa_event_handler);

// remove subscription to the EndTAA event later by the handler function
Render.EventEndTAA.Disconnect(endtaa_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endtaa_event_connection;

// subscribe to the EndTAA event with a lambda handler function and keeping the connection
endtaa_event_connection = Render.EventEndTAA.Connect(() => {
		Log.Message("Handling EndTAA event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endtaa_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endtaa_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endtaa_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndTAA events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndTAA.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndTAA.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginCameraEffects

The event triggered before the camera effects stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginCameraEffects event handler
void begincameraeffects_event_handler()
{
	Log.Message("\Handling BeginCameraEffects event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begincameraeffects_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginCameraEffects.Connect(begincameraeffects_event_connections, begincameraeffects_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginCameraEffects.Connect(begincameraeffects_event_connections, () => {
		Log.Message("Handling BeginCameraEffects event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begincameraeffects_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginCameraEffects event with a handler function
Render.EventBeginCameraEffects.Connect(begincameraeffects_event_handler);

// remove subscription to the BeginCameraEffects event later by the handler function
Render.EventBeginCameraEffects.Disconnect(begincameraeffects_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begincameraeffects_event_connection;

// subscribe to the BeginCameraEffects event with a lambda handler function and keeping the connection
begincameraeffects_event_connection = Render.EventBeginCameraEffects.Connect(() => {
		Log.Message("Handling BeginCameraEffects event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begincameraeffects_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begincameraeffects_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begincameraeffects_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginCameraEffects events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginCameraEffects.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginCameraEffects.Enabled = true;

```

</details>

## 🔒︎ Event EventEndCameraEffects

The event triggered after the camera effects stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndCameraEffects event handler
void endcameraeffects_event_handler()
{
	Log.Message("\Handling EndCameraEffects event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endcameraeffects_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndCameraEffects.Connect(endcameraeffects_event_connections, endcameraeffects_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndCameraEffects.Connect(endcameraeffects_event_connections, () => {
		Log.Message("Handling EndCameraEffects event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endcameraeffects_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndCameraEffects event with a handler function
Render.EventEndCameraEffects.Connect(endcameraeffects_event_handler);

// remove subscription to the EndCameraEffects event later by the handler function
Render.EventEndCameraEffects.Disconnect(endcameraeffects_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endcameraeffects_event_connection;

// subscribe to the EndCameraEffects event with a lambda handler function and keeping the connection
endcameraeffects_event_connection = Render.EventEndCameraEffects.Connect(() => {
		Log.Message("Handling EndCameraEffects event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endcameraeffects_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endcameraeffects_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endcameraeffects_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndCameraEffects events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndCameraEffects.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndCameraEffects.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginPostMaterials

The event triggered before the post materials rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginPostMaterials event handler
void beginpostmaterials_event_handler()
{
	Log.Message("\Handling BeginPostMaterials event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginpostmaterials_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginPostMaterials.Connect(beginpostmaterials_event_connections, beginpostmaterials_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginPostMaterials.Connect(beginpostmaterials_event_connections, () => {
		Log.Message("Handling BeginPostMaterials event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginpostmaterials_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginPostMaterials event with a handler function
Render.EventBeginPostMaterials.Connect(beginpostmaterials_event_handler);

// remove subscription to the BeginPostMaterials event later by the handler function
Render.EventBeginPostMaterials.Disconnect(beginpostmaterials_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginpostmaterials_event_connection;

// subscribe to the BeginPostMaterials event with a lambda handler function and keeping the connection
beginpostmaterials_event_connection = Render.EventBeginPostMaterials.Connect(() => {
		Log.Message("Handling BeginPostMaterials event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginpostmaterials_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginpostmaterials_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginpostmaterials_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginPostMaterials events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginPostMaterials.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginPostMaterials.Enabled = true;

```

</details>

## 🔒︎ Event EventEndPostMaterials

The event triggered after the post materials rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndPostMaterials event handler
void endpostmaterials_event_handler()
{
	Log.Message("\Handling EndPostMaterials event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endpostmaterials_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndPostMaterials.Connect(endpostmaterials_event_connections, endpostmaterials_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndPostMaterials.Connect(endpostmaterials_event_connections, () => {
		Log.Message("Handling EndPostMaterials event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endpostmaterials_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndPostMaterials event with a handler function
Render.EventEndPostMaterials.Connect(endpostmaterials_event_handler);

// remove subscription to the EndPostMaterials event later by the handler function
Render.EventEndPostMaterials.Disconnect(endpostmaterials_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endpostmaterials_event_connection;

// subscribe to the EndPostMaterials event with a lambda handler function and keeping the connection
endpostmaterials_event_connection = Render.EventEndPostMaterials.Connect(() => {
		Log.Message("Handling EndPostMaterials event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endpostmaterials_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endpostmaterials_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endpostmaterials_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndPostMaterials events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndPostMaterials.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndPostMaterials.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginDebugMaterials

The event triggered before the debug materials stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginDebugMaterials event handler
void begindebugmaterials_event_handler()
{
	Log.Message("\Handling BeginDebugMaterials event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections begindebugmaterials_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginDebugMaterials.Connect(begindebugmaterials_event_connections, begindebugmaterials_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginDebugMaterials.Connect(begindebugmaterials_event_connections, () => {
		Log.Message("Handling BeginDebugMaterials event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
begindebugmaterials_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginDebugMaterials event with a handler function
Render.EventBeginDebugMaterials.Connect(begindebugmaterials_event_handler);

// remove subscription to the BeginDebugMaterials event later by the handler function
Render.EventBeginDebugMaterials.Disconnect(begindebugmaterials_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection begindebugmaterials_event_connection;

// subscribe to the BeginDebugMaterials event with a lambda handler function and keeping the connection
begindebugmaterials_event_connection = Render.EventBeginDebugMaterials.Connect(() => {
		Log.Message("Handling BeginDebugMaterials event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
begindebugmaterials_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
begindebugmaterials_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
begindebugmaterials_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginDebugMaterials events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginDebugMaterials.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginDebugMaterials.Enabled = true;

```

</details>

## 🔒︎ Event EventEndDebugMaterials

The event triggered after the debug materials stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndDebugMaterials event handler
void enddebugmaterials_event_handler()
{
	Log.Message("\Handling EndDebugMaterials event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections enddebugmaterials_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndDebugMaterials.Connect(enddebugmaterials_event_connections, enddebugmaterials_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndDebugMaterials.Connect(enddebugmaterials_event_connections, () => {
		Log.Message("Handling EndDebugMaterials event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
enddebugmaterials_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndDebugMaterials event with a handler function
Render.EventEndDebugMaterials.Connect(enddebugmaterials_event_handler);

// remove subscription to the EndDebugMaterials event later by the handler function
Render.EventEndDebugMaterials.Disconnect(enddebugmaterials_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection enddebugmaterials_event_connection;

// subscribe to the EndDebugMaterials event with a lambda handler function and keeping the connection
enddebugmaterials_event_connection = Render.EventEndDebugMaterials.Connect(() => {
		Log.Message("Handling EndDebugMaterials event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
enddebugmaterials_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
enddebugmaterials_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
enddebugmaterials_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndDebugMaterials events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndDebugMaterials.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndDebugMaterials.Enabled = true;

```

</details>

## 🔒︎ Event EventBeginVisualizer

The event triggered before the visualizer rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the BeginVisualizer event handler
void beginvisualizer_event_handler()
{
	Log.Message("\Handling BeginVisualizer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections beginvisualizer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventBeginVisualizer.Connect(beginvisualizer_event_connections, beginvisualizer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventBeginVisualizer.Connect(beginvisualizer_event_connections, () => {
		Log.Message("Handling BeginVisualizer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
beginvisualizer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the BeginVisualizer event with a handler function
Render.EventBeginVisualizer.Connect(beginvisualizer_event_handler);

// remove subscription to the BeginVisualizer event later by the handler function
Render.EventBeginVisualizer.Disconnect(beginvisualizer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection beginvisualizer_event_connection;

// subscribe to the BeginVisualizer event with a lambda handler function and keeping the connection
beginvisualizer_event_connection = Render.EventBeginVisualizer.Connect(() => {
		Log.Message("Handling BeginVisualizer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
beginvisualizer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
beginvisualizer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
beginvisualizer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring BeginVisualizer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventBeginVisualizer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventBeginVisualizer.Enabled = true;

```

</details>

## 🔒︎ Event EventEndVisualizer

The event triggered after the visualizer rendering stage. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndVisualizer event handler
void endvisualizer_event_handler()
{
	Log.Message("\Handling EndVisualizer event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endvisualizer_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndVisualizer.Connect(endvisualizer_event_connections, endvisualizer_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndVisualizer.Connect(endvisualizer_event_connections, () => {
		Log.Message("Handling EndVisualizer event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endvisualizer_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndVisualizer event with a handler function
Render.EventEndVisualizer.Connect(endvisualizer_event_handler);

// remove subscription to the EndVisualizer event later by the handler function
Render.EventEndVisualizer.Disconnect(endvisualizer_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endvisualizer_event_connection;

// subscribe to the EndVisualizer event with a lambda handler function and keeping the connection
endvisualizer_event_connection = Render.EventEndVisualizer.Connect(() => {
		Log.Message("Handling EndVisualizer event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endvisualizer_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endvisualizer_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endvisualizer_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndVisualizer events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndVisualizer.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndVisualizer.Enabled = true;

```

</details>

## 🔒︎ Event EventEndScreen

The event triggered after the stage of rendering each screen (a stereo image has 2 screens, while a cubemap will have 6). You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndScreen event handler
void endscreen_event_handler()
{
	Log.Message("\Handling EndScreen event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endscreen_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEndScreen.Connect(endscreen_event_connections, endscreen_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEndScreen.Connect(endscreen_event_connections, () => {
		Log.Message("Handling EndScreen event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endscreen_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndScreen event with a handler function
Render.EventEndScreen.Connect(endscreen_event_handler);

// remove subscription to the EndScreen event later by the handler function
Render.EventEndScreen.Disconnect(endscreen_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endscreen_event_connection;

// subscribe to the EndScreen event with a lambda handler function and keeping the connection
endscreen_event_connection = Render.EventEndScreen.Connect(() => {
		Log.Message("Handling EndScreen event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endscreen_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endscreen_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endscreen_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndScreen events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEndScreen.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEndScreen.Enabled = true;

```

</details>

## 🔒︎ Event EventEnd

The event triggered when rendering of the frame ends. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the End event handler
void end_event_handler()
{
	Log.Message("\Handling End event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections end_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Render.EventEnd.Connect(end_event_connections, end_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Render.EventEnd.Connect(end_event_connections, () => {
		Log.Message("Handling End event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
end_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the End event with a handler function
Render.EventEnd.Connect(end_event_handler);

// remove subscription to the End event later by the handler function
Render.EventEnd.Disconnect(end_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection end_event_connection;

// subscribe to the End event with a lambda handler function and keeping the connection
end_event_connection = Render.EventEnd.Connect(() => {
		Log.Message("Handling End event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
end_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
end_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
end_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring End events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Render.EventEnd.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Render.EventEnd.Enabled = true;

```

</details>

## 🔒︎ Event EventEndFrameExecuteCommandLists

The Event triggered after *ExecuteCommandLists* just before *Present*. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndFrameExecuteCommandLists event handler
void endframeexecutecommandlists_event_handler()
{
	Log.Message("\Handling EndFrameExecuteCommandLists event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endframeexecutecommandlists_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndFrameExecuteCommandLists.Connect(endframeexecutecommandlists_event_connections, endframeexecutecommandlists_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndFrameExecuteCommandLists.Connect(endframeexecutecommandlists_event_connections, () => {
		Log.Message("Handling EndFrameExecuteCommandLists event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endframeexecutecommandlists_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndFrameExecuteCommandLists event with a handler function
publisher.EventEndFrameExecuteCommandLists.Connect(endframeexecutecommandlists_event_handler);

// remove subscription to the EndFrameExecuteCommandLists event later by the handler function
publisher.EventEndFrameExecuteCommandLists.Disconnect(endframeexecutecommandlists_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endframeexecutecommandlists_event_connection;

// subscribe to the EndFrameExecuteCommandLists event with a lambda handler function and keeping the connection
endframeexecutecommandlists_event_connection = publisher.EventEndFrameExecuteCommandLists.Connect(() => {
		Log.Message("Handling EndFrameExecuteCommandLists event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endframeexecutecommandlists_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endframeexecutecommandlists_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endframeexecutecommandlists_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndFrameExecuteCommandLists events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndFrameExecuteCommandLists.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndFrameExecuteCommandLists.Enabled = true;

```

</details>

## 🔒︎ Event EventEndVRQuadComposeEyeSwapchains

The Event triggered after composing VR viewports, enabling you to subscribe and perform certain actions (e.g. implement a binoculars effect using post-materials). You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the EndVRQuadComposeEyeSwapchains event handler
void endvrquadcomposeeyeswapchains_event_handler()
{
	Log.Message("\Handling EndVRQuadComposeEyeSwapchains event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections endvrquadcomposeeyeswapchains_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventEndVRQuadComposeEyeSwapchains.Connect(endvrquadcomposeeyeswapchains_event_connections, endvrquadcomposeeyeswapchains_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventEndVRQuadComposeEyeSwapchains.Connect(endvrquadcomposeeyeswapchains_event_connections, () => {
		Log.Message("Handling EndVRQuadComposeEyeSwapchains event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
endvrquadcomposeeyeswapchains_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the EndVRQuadComposeEyeSwapchains event with a handler function
publisher.EventEndVRQuadComposeEyeSwapchains.Connect(endvrquadcomposeeyeswapchains_event_handler);

// remove subscription to the EndVRQuadComposeEyeSwapchains event later by the handler function
publisher.EventEndVRQuadComposeEyeSwapchains.Disconnect(endvrquadcomposeeyeswapchains_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection endvrquadcomposeeyeswapchains_event_connection;

// subscribe to the EndVRQuadComposeEyeSwapchains event with a lambda handler function and keeping the connection
endvrquadcomposeeyeswapchains_event_connection = publisher.EventEndVRQuadComposeEyeSwapchains.Connect(() => {
		Log.Message("Handling EndVRQuadComposeEyeSwapchains event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
endvrquadcomposeeyeswapchains_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
endvrquadcomposeeyeswapchains_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
endvrquadcomposeeyeswapchains_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring EndVRQuadComposeEyeSwapchains events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventEndVRQuadComposeEyeSwapchains.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventEndVRQuadComposeEyeSwapchains.Enabled = true;

```

</details>

## 🔒︎ Event<string, string> EventGPUCrashDump

The Event triggered when a GPU crash is detected and a crash dump file has been written. The event provides the path to the dump file and an error message containing crash details (device status, page fault info, active shaders). Requires *video_debug_crash_dump* to be enabled and an NVIDIA GPU with Nsight Aftermath support. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(string **dump_path**, string **message**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the GPUCrashDump event handler
void gpucrashdump_event_handler(string dump_path,  string message)
{
	Log.Message("\Handling GPUCrashDump event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections gpucrashdump_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventGPUCrashDump.Connect(gpucrashdump_event_connections, gpucrashdump_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventGPUCrashDump.Connect(gpucrashdump_event_connections, (string dump_path,  string message) => {
		Log.Message("Handling GPUCrashDump event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
gpucrashdump_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the GPUCrashDump event with a handler function
publisher.EventGPUCrashDump.Connect(gpucrashdump_event_handler);

// remove subscription to the GPUCrashDump event later by the handler function
publisher.EventGPUCrashDump.Disconnect(gpucrashdump_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection gpucrashdump_event_connection;

// subscribe to the GPUCrashDump event with a lambda handler function and keeping the connection
gpucrashdump_event_connection = publisher.EventGPUCrashDump.Connect((string dump_path,  string message) => {
		Log.Message("Handling GPUCrashDump event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
gpucrashdump_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
gpucrashdump_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
gpucrashdump_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring GPUCrashDump events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventGPUCrashDump.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventGPUCrashDump.Enabled = true;

```

</details>

## Render.SHOW_TEXTURE_RESOLUTION_STREAMING_ACCOUNTING ShowTextureResolutionStreamingAccountingMode

***Console*:**`render_show_texture_resolution_streaming_accounting_mode`The streaming accounting mode. The following modes are available:
- *Actual Resolution* renders texel density based on the actual streaming result.
- *Requested Texture Resolution* renders texel density for the current surface only, based on the surface texture resolution requested by the streaming system.
- *Source Texture Resolution* renders texel density relative to the 0 mip level of the texture as if mipmap loading is disabled in the streaming system. This mode helps determine if the source texture resolution should be reduced.

  One of the following values:
- **0** - Actual Resolution (by default)
- **1** - Requested Texture Resolution
- **2** - Source Texture Resolution

## int IndirectLightingInterleavedSamples

***Console*:**`render_indirect_lighting_interleaved_samples`The number of samples for interleaved rendering of indirect lighting defining the number of pixels to be skipped during interleaved rendering of indirect lighting with subsequent reconstruction of neighboring pixels using the data from previous frames (defines the size of reduced lights buffer relative to original size).
- **1 x 2** - half of all pixels are rendered skipping each second line (1.0 * width x 0.5 * height)
- **2 x 2** - quarter of all pixels are rendered skipping each second line and row (0.5 * width x 0.5 * height)

  One of the following values:
- **0** - 1 x 2
- **1** - 2 x 2 (by default)

## int IndirectLightingInterleavedColorClamping

***Console*:**`render_indirect_lighting_interleaved_color_clamping`The color clamping mode to be used for interleaved rendering of indirect lighting. This mode is used to reduce ghosting effect: higher values increase clamping intensity but may cause flickering on rippled reflective surfaces (as this mode is not so good at the object's edges). When disabled, shadows and reflections have a lag as they are several frames behind. One of the following values:
- **0** - Disabled
- **1** - Low
- **2** - High (by default)

## bool IndirectLightingInterleavedCatmullResampling

***Console*:**`render_indirect_lighting_interleaved_catmull_resampling`The value indicating whether Catmull-Rom resampling is enabled or not. Catmull-Rom resampling allows you to reduce image blurring when the camera moves forward/backward. It is recommended to disable resampling for low quality presets. The default value is **false**.
## float LocalTonemapperColorDifferenceThreshold

***Console*:**`render_local_tonemapper_color_difference_threshold`The threshold value that determines the extent to which color differences on the screen are considered. If you set the value to 1, the result will appear as if the [*Color Difference*](#LocalTonemapperColorDifferenceEnabled) feature is turned off.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.1f**.
## bool LocalTonemapperColorDifferenceEnabled

***Console*:**`render_local_tonemapper_color_difference_enabled`The value indicating whether considering of the image color rendered on the screen is enabled. Enabling this feature allows reducing halo artifacts on surfaces with sharp color transitions. For example, it can significantly improve the appearance of a distinct shadow from the sun on asphalt. The default value is **false**.
## bool LocalTonemapperDepthDifferenceEnabled

***Console*:**`render_local_tonemapper_depth_difference_enabled`The value indicating whether considering of the depth difference between objects in the scene is enabled. Enabling this feature allows reducing halo artifacts around objects. However, we recommend using it only in exceptional cases, as it is a performance-costly operation. The default value is **false**.
## int LocalTonemapperBlurUpscaleKernelSize

***Console*:**`render_local_tonemapper_blur_upscale_kernel_size`The size of the kernel used for upscaling the blurred image. The higher the value the better the upscaling quality, but the lower the performance. It is recommended to set the kernel size as follows:
- *3x3* for the *Half* resolution.
- *5x5* for the *Quarter* resolution.

  One of the following values:
- **0** - 3x3 (by default)
- **1** - 5x5

## bool LocalTonemapperBlurUpscale

***Console*:**`render_local_tonemapper_blur_upscale`The value indicating whether upscaling the blurred image from the *Quarter* or *Half* resolution to the *Full* one is enabled. The default value is **false**.
## int LocalTonemapperBlurResolution

***Console*:**`render_local_tonemapper_blur_resolution`The resolution of the blur applied during the tone mapping process.
> **Notice:** It is recommended to use the *Half* resolution in conjunction with the *[Blur Upscale](#LocalTonemapperBlurUpscale)* mode enabled.

  One of the following values:

- *Quarter* - quarter resolution
- *Half* - half resolution
- *Full* - full resolution (by default)

## bool LocalTonemapperDebug

***Console*:**`render_local_tonemapper_debug`The value indicating whether the debug mode for the local tonemapper is enabled. The default value is **false**.
## int DenoiseColorClampingBlurResolution

***Console*:**`render_denoise_color_clamping_blur_resolution`The resolution of the Color Clamping Blur buffer. This buffer allows for reducing ghosting artifacts and information lost areas. The *Full* resolution is the slowest one, so we don't recommend using it. One of the following values:

- *Quarter* - quarter resolution
- *Half* - half resolution
- *Full* - full resolution (by default)

## float DenoiseWrongVelocityFixByDepthThreshold

***Console*:**`render_denoise_wrong_velocity_fix_by_depth_threshold`The threshold value of the difference between the depth in the current pixel and the pixel read using reprojection based on velocity. This threshold defines when to applying correction of incorrect velocity during the denoise process.
Range of values: **[0.0f, inf]**. The default value is : **0.03f**.
## bool DenoiseWrongVelocityFixByDepthEnabled

***Console*:**`render_denoise_wrong_velocity_fix_by_depth_enabled`The value indicating whether correction of a wrong velocity during the denoise process is enabled. It helps reduce ghosting artifacts around moving objects. The default value is **false**.
## float TAAInformationLostDepthThreshold

***Console*:**`render_taa_information_lost_depth_threshold`The threshold value for the depth difference used to calculate information lost areas. "Information lost" refers to rendering of the surfaces that weren't rendered in the prevoius frame.
Range of values: **[0.0f, inf]**. The default value is : **0.1f**.
## float StreamingTexturesMipmapsDensity

***Console*:**`render_streaming_textures_mipmaps_density`The density of mipmaps relative to the screen resolution. This value helps to define which mipmap should be loaded at the current moment. You can specify different values for different quality presets.
Range of values: **[0.0f, 1000000.0f]**. The default value is : **2.0f**.
## bool StreamingTexturesMipmaps

***Console*:**`render_streaming_textures_mipmaps`The value indicating whether texture mipmap loading is enabled. The default value is **false**.
## Render.STREAMING_VRAM_BUDGET StreamingVRAMBudget

***Console*:**`render_streaming_vram_budget`The mode for determining the amount of available VRAM. The following modes are available:
- *System* - the available VRAM size is obtained from the operating system.
- *Driver* - the VRAM available for the application is determined by the video driver.
- *Full GPU Memory* - all VRAM is available for the application.

  One of the following values:
- **0** - System
- **1** - Driver (by default)
- **2** - Full GPU Memory

## bool StreamingVRAMOvercommit

***Console*:**`render_streaming_vram_overcommit`The value indicating whether VRAM limits (both the usage limit and free space) are applied. The default value is **false**.
## bool StreamingCommittedMemoryOvercommit

***Console*:**`render_streaming_committed_memory_overcommit`The value indicating whether the Engine enforces internal limits on committed memory usage.
- When **disabled**, the Engine respects the **Free Space Committed RAM** setting and will not allocate more committed memory than the configured limit allows. In this mode, the amount of physical RAM and VRAM available to the Engine is effectively reduced to the portion of committed memory accessible within this limit.
- When **enabled** (default), the Engine ignores the **Free Space Committed RAM** restriction and can use **all available committed memory** provided by the system. This may improve streaming performance, especially under high memory pressure (for example, when browsers or other background applications are running, or after long system uptime), but it also increases the risk of instability if the system runs out of virtual memory.


> **Warning:** With overcommit enabled, crashes may occur if:
>
>
> - the system has no page file
> - there is insufficient free disk space on the drive where the page file is located.
>
>
> If system committed memory is fully exhausted, this may affect not only the Engine, but also **other running applications**.

  The default value is **true**.
## int StreamingFreeSpaceRAM

***Console*:**`render_streaming_free_space_ram`The amount of physical memory that the Engine will always keep free and never allocate for its own use, in Mbytes.
Range of values: **[0, INT_MAX]**. The default value is : **1024**.
## int StreamingFreeSpaceVRAM

***Console*:**`render_streaming_free_space_vram`The amount of VRAM that the Engine will always keep free and never allocate for its own use, in Mbytes.
Range of values: **[0, INT_MAX]**. The default value is : **512**.
## int StreamingFreeSpaceRAMCommitted

***Console*:**`render_streaming_free_space_ram_committed`The amount of committed memory that the Engine will always keep free and never allocate for its own use, in Mbytes.
Range of values: **[0, INT_MAX]**. The default value is : **512**.
## float IndirectLightingInterleavedColorClampingVelocityThreshold

***Console*:**`render_indirect_lighting_interleaved_color_clamping_velocity_threshold`The velocity threshold of color clamping for interleaved indirect lighting. The higher the value, the less the ghosting effect. However, increasing the threshold may change the overall image brightness due to excessive color clamping.
Range of values: **[0.0f, 1000.0f]**. The default value is : **100.0f**.
## float IndirectLightingInterleavedColorClampingIntensity

***Console*:**`render_indirect_lighting_interleaved_color_clamping_intensity`The constant size of the intensity of color clamping for interleaved indirect lighting.
Range of values: **[0.0f, 100.0f]**. The default value is : **0.0f**.
## float LocalTonemapperEffectOnDarkAreasGamma

***Console*:**`render_local_tonemapper_effect_on_dark_areas_gamma`The gamma correction value for dark areas. Specifying values greater than 1 decreases the local tone mapping effect in extremely dark areas.
Range of values: **[0.0f, inf]**. The default value is : **5.0f**.
## int StreamingUsageLimitRAM

***Console*:**`render_streaming_usage_limit_ram`The percentage of the total physical memory (RAM) that the Engine is allowed to use for streaming. If the streaming exceeds the RAM usage limit, the application may become unstable or crash.
Range of values: **[10, 100]**. The default value is : **80**.
## int StreamingUsageLimitVRAM

***Console*:**`render_streaming_usage_limit_vram`The percentage of the committed video memory available for streaming. If the streaming exceeds the VRAM usage limit, it will start using RAM for loading graphic resources.
Range of values: **[10, 100]**. The default value is : **80**.
## Render.MATERIALS_QUALITY MaterialsQuality

***Console*:**`render_materials_quality`The quality level of the rendered materials. Depending on the specified level, a certain set of features inside graph-based materials connected to the corresponding input of a ***[Material Quality Switch](../../../content/materials/graph/node_library/misc/material_quality_switch.md)*** node will be applied. One of the following values:
- **0** - Low
- **1** - Medium
- **2** - High (by default)

## Render.SHADING_QUALITY ShadingQuality

***Console*:**`render_shading_quality`The quality level of shading. Depending on the specified level, a certain set of shading features inside graph-based materials connected to the corresponding input of a ***[Shading Quality Switch](../../../content/materials/graph/node_library/misc/shading_quality_switch.md)*** node will be applied. One of the following values:
- **0** - Low
- **1** - Medium
- **2** - High (by default)

## bool Multithreaded

***Console*:**`render_multithreaded`The value indicating if the multithreaded rendering mode is enabled (DX12 only). The default value is **true**.
## bool MultithreadedEditor

***Console*:**`render_multithreaded_editor`The value indicating if the multithreaded rendering mode in the Editor is enabled (DX12 only). The default value is **false**.
## float ShowQuadOverdrawBlend

***Console*:**`render_show_quad_overdraw_blend`The opacity of the *[Quad Overdraw](../../../content/optimization/geometry/quad_overdraw/index.md#tool_overview)* visualizer.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
## int ShowQuadOverdrawThreshold

***Console*:**`render_show_quad_overdraw_threshold`The threshold value of the *[Quad Overdraw](../../../content/optimization/geometry/quad_overdraw/index.md#tool_overview)* visualizer.
Range of values: **[1, 1000000]**. The default value is : **40**.
## bool ShowQuadOverdrawWaterGlobal

***Console*:**`render_show_quad_overdraw_water_global`The *[Water Global](../../../objects/objects/water/water_object.md)* rendering enabled state in the *[Quad Overdraw](../../../content/optimization/geometry/quad_overdraw/index.md#tool_overview)* visualizer. The default value is **false**.
## bool ShowQuadOverdrawLandscapeTerrain

***Console*:**`render_show_quad_overdraw_landscape_terrain`The *[Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md)* rendering enabled state in the *[Quad Overdraw](../../../content/optimization/geometry/quad_overdraw/index.md#tool_overview)* visualizer. The default value is **false**.
## bool ShowQuadOverdrawWireframe

***Console*:**`render_show_quad_overdraw_wireframe`The Wireframe rendering enabled state in the *[Quad Overdraw](../../../content/optimization/geometry/quad_overdraw/index.md#tool_overview)* visualizer. The default value is **false**.
## Render.SHOW_QUAD_OVERDRAW_PASSES ShowQuadOverdrawPasses

***Console*:**`render_show_quad_overdraw_passes`The operating mode of the *[Quad Overdraw](../../../content/optimization/geometry/quad_overdraw/index.md#tool_overview)* visualizer. The following options are available:
- *All Passes with Depth Pre-Pass* (default) - Displays the total number of overdraws, including all passes (*Auxiliary, Emission, Ambient, Light*, and others), and depth pre-passes.
- *Single Geometry Pass with Depth Pre-Pass* - Displays the number of overdraws for the primary rendering pass of the content after applying the depth pre-pass. Separate passes (such as Auxiliary or Emission) are not counted in this mode.
- *Single Geometry Pass without Depth Pre-Pass* - Displays the number of content overdraws without using depth pre-pass (before any early depth rejection is applied).

  One of the following values:
- **0** - All Passes with Depth Pre-Pass (by default)
- **1** - Single Geometry Pass with Depth Pre-Pass
- **2** - Single Geometry Pass without Depth Pre-Pass

## Render.SHOW_QUAD_OVERDRAW_DISPLAY_MODE ShowQuadOverdrawDisplayMode

***Console*:**`render_show_quad_overdraw_display_mode`The display mode of the *[Quad Overdraw](../../../content/optimization/geometry/quad_overdraw/index.md#tool_overview)* visualizer. The following display modes are available:
- *Gradient* - displays a color gradient representing overdraw intensity from black (0) to **white (*[ShowQuadOverdrawThreshold](../../...md#setShowQuadOverdrawThreshold_int_void)*)**.
- *Discrete threshold* - highlights in red only the areas where the overdraw exceeds the specified threshold.

  One of the following values:
- **0** - Gradient (by default)
- **1** - Discrete threshold

## bool ShowQuadOverdrawEnabled

***Console*:**`render_show_quad_overdraw_enabled`The *[Quad Overdraw](../../../content/optimization/geometry/quad_overdraw/index.md#tool_overview)* visualizer enabled state. The default value is **false**.
## float ShowVertexDensityBlend

***Console*:**`render_show_vertex_density_blend`The opacity of the *[Vertex Density](../../../content/optimization/geometry/vertex_density/index.md#tool_overview)* visualizer.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
## int ShowVertexDensityThreshold

***Console*:**`render_show_vertex_density_threshold`The threshold value of the *[Vertex Density](../../../content/optimization/geometry/vertex_density/index.md#tool_overview)* visualizer.
Range of values: **[1, 1000000]**. The default value is : **100**.
## int ShowVertexDensitySearchArea

***Console*:**`render_show_vertex_density_search_area`The size of the vertex search area (in pixels).
Range of values: **[1, 1024]**. The default value is : **8**.
## bool ShowVertexDensityDepthTest

***Console*:**`render_show_vertex_density_depth_test`The *[Vertex Density](../../../content/optimization/geometry/vertex_density/index.md#tool_overview)* depth testing enabled state. The default value is **true**.
## Render.SHOW_VERTEX_DENSITY_MODE ShowVertexDensityMode

***Console*:**`render_show_vertex_density_mode`The mode of the *[Vertex Density](../../../content/optimization/geometry/vertex_density/index.md#tool_overview)* visualizer. The following modes are available:
- *Discrete Threshold* - highlights in red only the areas where the vertex density exceeds the specified threshold within the defined area.
- *Gradient* - displays a color gradient representing vertex density from black (0) to **white (*[ShowVertexDensityThreshold](../../...md#setShowVertexDensityThreshold_int_void)*)** within the defined searching area.

  One of the following values:
- **0** - Discrete threshold (by default)
- **1** - Gradient

## bool ShowVertexDensityEnabled

***Console*:**`render_show_vertex_density_enabled`The *[Vertex Density](../../../content/optimization/geometry/vertex_density/index.md#tool_overview)* visualizer enabled state. The default value is **false**.
## float LightsDitherScale

***Console*:**`render_lights_dither_scale`The dithering intensity for light rendering. Dithering adds subtle noise to reduce color banding in light gradients.
Range of values: **[0.0f, 1.0f]**. The default value is : **1.0f**.
## 🔒︎ float EnvironmentMoonAngularSize

The current angular size of the moon in degrees, as determined by the active environment preset. This is a read-only value interpolated from the environment presets. To change it, use [RenderEnvironmentPreset](../../../api/library/rendering/class.renderenvironmentpreset_cs.md).
## 🔒︎ float EnvironmentSunAngularSize

The current angular size of the sun in degrees, as determined by the active environment preset. This is a read-only value interpolated from the environment presets. To change it, use [RenderEnvironmentPreset](../../../api/library/rendering/class.renderenvironmentpreset_cs.md).
## float EnvironmentHazeDitherScale

***Console*:**`render_environment_haze_dither_scale`The dithering intensity for haze rendering. Dithering adds subtle noise to reduce color banding in haze gradients.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**.
## float EnvironmentDitherScale

***Console*:**`render_environment_dither_scale`The dithering intensity for environment rendering. Dithering adds subtle noise to reduce color banding in environment gradients.
Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**.
## bool FSRShowDebugView

***Console*:**`render_upscale_fsr_show_debug_view`The value indicating if FSR debug view is enabled. The default value is **false**.
## Render.RENDER_UPSCALE_ORDER UpscaleOrder

***Console*:**`render_upscale_order`The stage of the rendering pipeline at which upscaling is applied. One of the following values:
- **0** - upscale before post-effects. (by default)
- **1** - upscale after color adaptation.
- **2** - upscale before TAA
- **3** - upscale after post-effects (before the Sharpen effect)

## int StreamingIGpuVRAMBalance

***Console*:**`render_streaming_igpu_vram_balance`The percentage of total system RAM to be used as the VRAM budget for integrated GPUs. Applicable when [StreamingIGpuVRAMMode](#StreamingIGpuVRAMMode) is set to [BALANCE](#STREAMING_IGPU_VRAM_MODE_BALANCE).
Range of values: **[10, 80]**. The default value is : **40**.
## int StreamingIGpuVRAMSize

***Console*:**`render_streaming_igpu_vram_size`The custom VRAM size (in MB) to be used as the VRAM budget for integrated GPUs. Applicable when [StreamingIGpuVRAMMode](#StreamingIGpuVRAMMode) is set to [SIZE](#STREAMING_IGPU_VRAM_MODE_SIZE).
Range of values: **[512, 32768]**. The default value is : **4096**.
## Render.STREAMING_IGPU_VRAM_MODE StreamingIGpuVRAMMode

***Console*:**`render_streaming_igpu_vram_mode`The mode that determines how the engine calculates the available VRAM budget for integrated GPUs (iGPU) that share system RAM instead of having dedicated video memory. One of the following values:
- **0** - system (by default)
- **1** - custom size
- **2** - total memory balance

## 🔒︎ int NumCompiledPSOGlobal

The number of global PSOs compiled during the current frame. Global PSOs represent the render pipeline state set dynamically before each draw call, as opposed to PSOs embedded in shader code.
### Members

---

## bool IsAPISupported ( int api )

Returns a value indicating if the specified graphics API (Null/Vulkan/DirectX) is currently supported.
### Arguments

- *int* **api** - Graphics API ID. One of the [API_*](#API_NULL) values.

### Return value

true if the specified graphics API is currently supported; otherwise, false.
## bool IsUpscaleModeSupported ( Render.RENDER_UPSCALE_MODE mode )

Returns a value indicating if the specified upscale mode (FSR/DLSS) is currently supported.
### Arguments

- *[Render.RENDER_UPSCALE_MODE](../../../api/library/rendering/class.render_cs.md#RENDER_UPSCALE_MODE)* **mode** - Upscaling mode to check. Defines a technology to be used to render high-resolution images based on the lower resolution source, which may help preserve image quality while getting more fps.

### Return value

true if the specified upscale mode is currently supported; otherwise, false.
## void BeginDebugGroup ( string name )

Starts a [GPU debug group](../../../tools/profiling/microprofile/index_cs.md#gpu_debug_group) with a specified name in Microprofiler.
### Arguments

- *string* **name** - Name of debug group.

## void EndDebugGroup ( )

Ends a [GPU debug group](../../../tools/profiling/microprofile/index_cs.md#gpu_debug_group) previously started via the [beginDebugGroup()](#beginDebugGroup_cstr_void) method.
## void MemoryClear ( bool soft = false )

Clears the video memory, ffp buffer and memory pools, deletes textures and all meshes, including skinned meshes and decals. This method is called automatically after the world is loaded or the render preset has been changed. It is recommended to use it only in case a significant amount of memory needs to be released, the resources will be force removed at the end of the frame.
### Arguments

- *bool* **soft** - If set to true, performs a soft clear: only unused textures and meshes are destroyed and memory pools are cleared. If set to false (default), performs a full clear: all temporary textures and resources are also destroyed and will be recreated on demand.

## Texture GetBlack2DArrayTexture ( )

Returns black 2D array texture.
### Return value

Black 2D array texture.
## Texture GetBlack2DTexture ( )

Returns black 2D texture.
### Return value

Black 2D texture.
## Texture GetBlack2DUIntTexture ( )

Returns black 2D UInt texture.
### Return value

Black 2D UInt texture.
## Texture GetBlack3DTexture ( )

Returns black 3D texture.
### Return value

Black 3D texture.
## Texture GetBlackCubeTexture ( )

Returns black Cube texture.
### Return value

Black Cube texture.
## Texture GetGray2DArrayTexture ( )

Returns gray 2D array texture.
### Return value

Gray 2D array texture.
## Texture GetGray2DTexture ( )

Returns gray 2D texture.
### Return value

Gray 2D texture.
## Texture GetGray2DUIntTexture ( )

Returns gray 2D UInt texture.
### Return value

Gray 2D UInt texture.
## Texture GetGray3DTexture ( )

Returns gray 3D texture.
### Return value

Gray 3D texture.
## Texture GetGrayCubeTexture ( )

Returns gray Cube texture.
### Return value

Gray Cube texture.
## Texture GetWhite2DArrayTexture ( )

Returns white 2D array texture.
### Return value

White 2D array texture.
## Texture GetWhite2DTexture ( )

Returns white 2D texture.
### Return value

White 2D texture.
## Texture GetWhite2DUIntTexture ( )

Returns white 2D UInt texture.
### Return value

White 2D UInt texture.
## Texture GetWhite3DTexture ( )

Returns white 3D texture.
### Return value

White 3D texture.
## Texture GetWhiteCubeTexture ( )

Returns white Cube texture.
### Return value

White Cube texture.
## uint GetMaxTextureBufferSize ( )

Returns the maximum size of the texture buffer.
### Return value

Maximum size of the texture buffer.
## void AddScriptableMaterial ( Material material )

Adds a new global [scriptable material](../../../content/materials/scriptable.md). To apply a scriptable material per-camera or per-player, use the *[addScriptableMaterial()](../../../api/library/rendering/class.camera_cs.md#addScriptableMaterial_Material_void)* method of the Camera class or [the same method of the Player class](../../../api/library/players/class.player_cs.md#addScriptableMaterial_Material_void) respectively. The order of execution for scripts assigned to scriptable materials is defined by material's number in the list of materials applied globally.
> **Notice:** Scriptable materials applied globally have their expressions executed before the ones that are applied [per-camera](../../../api/library/rendering/class.camera_cs.md#addScriptableMaterial_Material_void) or [per-player](../../../api/library/players/class.player_cs.md#addScriptableMaterial_Material_void).


### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Scriptable material to be applied globally.

## void InsertScriptableMaterial ( int num , Material material )

Inserts a new global [scriptable material](../../../content/materials/scriptable.md) to the list of globally applied scriptable materials. To apply a scriptable material per-camera or per-player, use the *[insertScriptableMaterial()](../../../api/library/rendering/class.camera_cs.md#insertScriptableMaterial_int_Material_void)* method of the Camera class or [the same method of the Player class](../../../api/library/players/class.player_cs.md#insertScriptableMaterial_int_Material_void) respectively. The order of execution for scripts assigned to scriptable materials is defined by material's number in the list of materials applied globally.
> **Notice:** Scriptable materials applied globally have their expressions executed before the ones that are applied [per-camera](../../../api/library/rendering/class.camera_cs.md#insertScriptableMaterial_int_Material_void) or [per-player](../../../api/library/players/class.player_cs.md#insertScriptableMaterial_int_Material_void).


### Arguments

- *int* **num** - Position at which a new scriptable material is to be inserted.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Scriptable material to be inserted into the list of globally applied scriptable materials.

## void RemoveScriptableMaterial ( int num )

Removes the global [scriptable material](../../../content/materials/scriptable.md) with the specified number.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

## int FindScriptableMaterial ( Material material )

Returns the number of the specified [scriptable material](../../../content/materials/scriptable.md) applied globally. This number determines the order in which the assigned expressions are executed.
> **Notice:** Scriptable materials applied globally have their expressions executed before the ones that are applied [per-camera](../../../api/library/rendering/class.camera_cs.md#addScriptableMaterial_Material_void) or [per-player](../../../api/library/players/class.player_cs.md#addScriptableMaterial_Material_void).


### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Scriptable material for which a number is to be found.

### Return value

Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int), or -1 if the specified material was not found.
## void SetScriptableMaterial ( int num , Material material )

Replaces the [scriptable material](../../../content/materials/scriptable.md) with the specified number with the new scriptable material specified. The number of material determines the order in which the expressions assigned to it are executed.
> **Notice:** Scriptable materials applied globally have their expressions executed before the ones that are applied [per-camera](../../../api/library/rendering/class.camera_cs.md#addScriptableMaterial_Material_void) or [per-player](../../../api/library/players/class.player_cs.md#addScriptableMaterial_Material_void).


### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - New scriptable material to replace the one with the specified number.

## Material GetScriptableMaterial ( int num )

Returns a [scriptable material](../../../content/materials/scriptable.md) applied globally by its number.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

### Return value

Scriptable material applied globally with the specified number.
## void SetScriptableMaterialEnabled ( int num , bool enabled )

Enables or disables the [scriptable material](../../../content/materials/scriptable.md) with the specified number. When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *bool* **enabled** - 1 to enable the scriptable material with the specified number, 0 to disable it.

## bool GetScriptableMaterialEnabled ( int num )

Returns a value indicating if the [scriptable material](../../../content/materials/scriptable.md) with the specified number is enabled (active). When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **num** - Scriptable material number in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

### Return value

1 if the scriptable material with the specified number is enabled; otherwise, 0.
## void SwapScriptableMaterials ( int num_0 , int num_1 )

Swaps two [scriptable materials](../../../content/materials/scriptable.md) with specified numbers. The number of material determines the order in which the expressions assigned to it are executed.
> **Notice:** Scriptable materials applied globally have their expressions executed before the ones that are applied [per-camera](../../../api/library/rendering/class.camera_cs.md#addScriptableMaterial_Material_void) or [per-player](../../../api/library/players/class.player_cs.md#addScriptableMaterial_Material_void).


### Arguments

- *int* **num_0** - Number of the first scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).
- *int* **num_1** - Number of the second scriptable material in the range from 0 to the [total number of scriptable materials](#getNumScriptableMaterials_int).

## void ClearScriptableMaterials ( )

Clears all global [scriptable materials](../../../content/materials/scriptable.md).
## Texture GetTemporaryTexture ( int width , int height , int depth , int format , int flags = 0 , int type , string name = 0 , Render.TEXTURE_ACCESSORY accessory = TEXTURE_ACCESSORY.NONE , Render.TEXTURE_LIFETIME lifetime = TEXTURE_LIFETIME.FRAME_VIEWPORT , bool auto_release = false )


Allocates a temporary render texture with the specified width, height, depth, format, flags, and type. This function can be used when you need a quick render texture to perform some temporary calculations. Release it using *[releaseTemporaryTexture()](#releaseTemporaryTexture_Texture_void)* as soon as you're done with it, so another call can start reusing it, if necessary. In any case, such texture shall be released automatically in the next frame.


UNIGINE keeps an internal pool of temporary render textures, so a call to this method most often just returns an already created one (if the size and format match). These temporary textures are actually destroyed when they aren't used for a couple of frames.


If you are doing a series of post-processing "blits", it's best for performance to get and release a temporary render texture for each blit, instead of getting one or two render textures upfront and reusing them.


> **Notice:** You can't rely on any particular contents of a temporary texture obtained from this function: it might be garbage, or it might be cleared to some color, depending on the platform.


It also automatically gives names to resources, which can be used for identification in [debug](../../../tools/profiling/microprofile/index_cs.md#gpu_debug_group).


### Arguments

- *int* **width** - Width of the texture, in pixels.
- *int* **height** - Height of the texture, in pixels.
- *int* **depth** - Depth of the texture, in pixels.
- *int* **format** - Texture format: one of the [Texture.FORMAT_*](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags.
- *int* **type** - Texture type (2D, 3D, Cube, etc.): one of the [Texture.TEXTURE_*](../../../api/library/rendering/class.texture_cs.md#TEXTURE_2D) values.
- *string* **name** - Name to be used for this temporary texture (optional). If not specified, a new name for it will be generated automatically.
- *[Render.TEXTURE_ACCESSORY](../../../api/library/rendering/class.render_cs.md#TEXTURE_ACCESSORY)* **accessory** - Texture render sequence accessory type. One of the [TEXTURE_ACCESSORY_*](#TEXTURE_ACCESSORY_NONE) values.
- *[Render.TEXTURE_LIFETIME](../../../api/library/rendering/class.render_cs.md#TEXTURE_LIFETIME)* **lifetime** - Texture lifetime (the texture will be released automatically when its lifetime expires, if the auto_release flag is set). One of the [TEXTURE_LIFETIME*](#TEXTURE_LIFETIME_FRAME_VIEWPORT) values.
- *bool* **auto_release** - true to enable automatic release of the temporary texture by its [lifetime](#TEXTURE_LIFETIME), false to release it manually.

### Return value

Temporary texture.
## Texture GetTemporaryTexture ( Texture texture , string name = 0 , Render.TEXTURE_ACCESSORY accessory = TEXTURE_ACCESSORY.NONE , Render.TEXTURE_LIFETIME lifetime = TEXTURE_LIFETIME.FRAME_VIEWPORT , bool auto_release = false )


Allocates a temporary render texture with the specified width, height, depth, format, flags, and type. This function can be used when you need a quick render texture to perform some temporary calculations. Release it using *[releaseTemporaryTexture()](#releaseTemporaryTexture_Texture_void)* as soon as you're done with it, so another call can start reusing it, if necessary. In any case, such texture shall be released automatically in the next frame.


UNIGINE keeps an internal pool of temporary render textures, so a call to this method most often just returns an already created one (if the size and format match). These temporary textures are actually destroyed when they aren't used for a couple of frames.


If you are doing a series of post-processing "blits", it's best for performance to get and release a temporary render texture for each blit, instead of getting one or two render textures upfront and reusing them.


> **Notice:** You can't rely on any particular contents of a temporary texture obtained from this function: it might be garbage, or it might be cleared to some color, depending on the platform.


It also automatically gives names to resources, which can be used for identification in [debug](../../../tools/profiling/microprofile/index_cs.md#gpu_debug_group).


### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture**
- *string* **name** - Name to be used for this temporary texture (optional). If not specified, a new name for it will be generated automatically.
- *[Render.TEXTURE_ACCESSORY](../../../api/library/rendering/class.render_cs.md#TEXTURE_ACCESSORY)* **accessory** - Texture render sequence accessory type. One of the [TEXTURE_ACCESSORY_*](#TEXTURE_ACCESSORY_NONE) values.
- *[Render.TEXTURE_LIFETIME](../../../api/library/rendering/class.render_cs.md#TEXTURE_LIFETIME)* **lifetime** - Texture lifetime (the texture will be released automatically when its lifetime expires, if the auto_release flag is set). One of the [TEXTURE_LIFETIME*](#TEXTURE_LIFETIME_FRAME_VIEWPORT) values.
- *bool* **auto_release** - true to enable automatic release of the temporary texture by its [lifetime](#TEXTURE_LIFETIME), false to release it manually.

### Return value

Temporary texture.
## Texture GetTemporaryTexture ( Image image , int flags = -1 , string name = 0 , Render.TEXTURE_ACCESSORY accessory = TEXTURE_ACCESSORY.NONE , Render.TEXTURE_LIFETIME lifetime = TEXTURE_LIFETIME.FRAME_VIEWPORT , bool auto_release = false )

### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image**
- *int* **flags** - Texture flags.
- *string* **name** - Name to be used for this temporary texture (optional). If not specified, a new name for it will be generated automatically.
- *[Render.TEXTURE_ACCESSORY](../../../api/library/rendering/class.render_cs.md#TEXTURE_ACCESSORY)* **accessory** - Texture render sequence accessory type. One of the [TEXTURE_ACCESSORY_*](#TEXTURE_ACCESSORY_NONE) values.
- *[Render.TEXTURE_LIFETIME](../../../api/library/rendering/class.render_cs.md#TEXTURE_LIFETIME)* **lifetime** - Texture lifetime (the texture will be released automatically when its lifetime expires, if the auto_release flag is set). One of the [TEXTURE_LIFETIME*](#TEXTURE_LIFETIME_FRAME_VIEWPORT) values.
- *bool* **auto_release** - true to enable automatic release of the temporary texture by its [lifetime](#TEXTURE_LIFETIME), false to release it manually.

### Return value

Temporary texture.
## Texture GetTemporaryTexture2D ( int width , int height , int format , int flags = -1 , string name = 0 , Render.TEXTURE_ACCESSORY accessory = TEXTURE_ACCESSORY.NONE , Render.TEXTURE_LIFETIME lifetime = TEXTURE_LIFETIME.FRAME_VIEWPORT , bool auto_release = false )


Allocates a temporary 2D texture with the specified width, height, format, and flags. This function can be used when you need a quick render texture to perform some temporary calculations. Release it using *[releaseTemporaryTexture()](#releaseTemporaryTexture_Texture_void)* as soon as you're done with it, so another call can start reusing it, if necessary. In any case, such texture shall be released automatically in the next frame.


UNIGINE keeps an internal pool of temporary render textures, so a call to this method most often just returns an already created one (if the size and format match). These temporary textures are actually destroyed when they aren't used for a couple of frames.


If you are doing a series of post-processing "blits", it's best for performance to get and release a temporary render texture for each blit, instead of getting one or two render textures upfront and reusing them.


> **Notice:** You can't rely on any particular contents of a temporary texture obtained from this function: it might be garbage, or it might be cleared to some color, depending on the platform.


### Arguments

- *int* **width** - Width of the 2D texture, in pixels.
- *int* **height** - Height of the 2D texture, in pixels.
- *int* **format** - Texture format: one of the [Texture.FORMAT_*](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags.
- *string* **name** - Name to be used for this temporary texture (optional). If not specified, a new name for it will be generated automatically.
- *[Render.TEXTURE_ACCESSORY](../../../api/library/rendering/class.render_cs.md#TEXTURE_ACCESSORY)* **accessory** - Texture render sequence accessory type. One of the [TEXTURE_ACCESSORY_*](#TEXTURE_ACCESSORY_NONE) values.
- *[Render.TEXTURE_LIFETIME](../../../api/library/rendering/class.render_cs.md#TEXTURE_LIFETIME)* **lifetime** - Texture lifetime (the texture will be released automatically when its lifetime expires, if the auto_release flag is set). One of the [TEXTURE_LIFETIME*](#TEXTURE_LIFETIME_FRAME_VIEWPORT) values.
- *bool* **auto_release** - true to enable automatic release of the temporary texture by its [lifetime](#TEXTURE_LIFETIME), false to release it manually.

### Return value

Temporary 2D texture.
## Texture GetTemporaryTexture2DArray ( int width , int height , int depth , int format , int flags = 0 , string name = 0 , Render.TEXTURE_ACCESSORY accessory = TEXTURE_ACCESSORY.NONE , Render.TEXTURE_LIFETIME lifetime = TEXTURE_LIFETIME.FRAME_VIEWPORT , bool auto_release = false )


Allocates a temporary 2D array texture with the specified width, height, number of layers, format, and flags. This function can be used when you need a quick render texture to perform some temporary calculations. Release it using *[releaseTemporaryTexture()](#releaseTemporaryTexture_Texture_void)* as soon as you're done with it, so another call can start reusing it, if necessary. In any case, such texture shall be released automatically in the next frame.


UNIGINE keeps an internal pool of temporary render textures, so a call to this method most often just returns an already created one (if the size and format match). These temporary textures are actually destroyed when they aren't used for a couple of frames.


If you are doing a series of post-processing "blits", it's best for performance to get and release a temporary render texture for each blit, instead of getting one or two render textures upfront and reusing them.


> **Notice:** You can't rely on any particular contents of a temporary texture obtained from this function: it might be garbage, or it might be cleared to some color, depending on the platform.


### Arguments

- *int* **width** - Width of the 2D array texture, in pixels.
- *int* **height** - Height of the 2D array texture, in pixels.
- *int* **depth** - Number of layers in the 2D array texture.
- *int* **format** - Texture format: one of the [Texture.FORMAT_*](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags.
- *string* **name** - Name to be used for this temporary 2D array texture (optional). If not specified, a new name for it will be generated automatically.
- *[Render.TEXTURE_ACCESSORY](../../../api/library/rendering/class.render_cs.md#TEXTURE_ACCESSORY)* **accessory** - Texture render sequence accessory type. One of the [TEXTURE_ACCESSORY_*](#TEXTURE_ACCESSORY_NONE) values.
- *[Render.TEXTURE_LIFETIME](../../../api/library/rendering/class.render_cs.md#TEXTURE_LIFETIME)* **lifetime** - Texture lifetime (the texture will be released automatically when its lifetime expires, if the auto_release flag is set). One of the [TEXTURE_LIFETIME*](#TEXTURE_LIFETIME_FRAME_VIEWPORT) values.
- *bool* **auto_release** - true to enable automatic release of the temporary texture by its [lifetime](#TEXTURE_LIFETIME), false to release it manually.

### Return value

Temporary 2D array texture.
## Texture GetTemporaryTexture3D ( int width , int height , int depth , int format , int flags = 0 , string name = 0 , Render.TEXTURE_ACCESSORY accessory = TEXTURE_ACCESSORY.NONE , Render.TEXTURE_LIFETIME lifetime = TEXTURE_LIFETIME.FRAME_VIEWPORT , bool auto_release = false )


Allocates a temporary 3D texture with the specified width, height, depth, format, and flags. This function can be used when you need a quick render texture to perform some temporary calculations. Release it using *[releaseTemporaryTexture()](#releaseTemporaryTexture_Texture_void)* as soon as you're done with it, so another call can start reusing it, if necessary. In any case, such texture shall be released automatically in the next frame.


UNIGINE keeps an internal pool of temporary render textures, so a call to this method most often just returns an already created one (if the size and format match). These temporary textures are actually destroyed when they aren't used for a couple of frames.


If you are doing a series of post-processing "blits", it's best for performance to get and release a temporary render texture for each blit, instead of getting one or two render textures upfront and reusing them.


> **Notice:** You can't rely on any particular contents of a temporary texture obtained from this function: it might be garbage, or it might be cleared to some color, depending on the platform.


### Arguments

- *int* **width** - Width of the 3D texture, in pixels.
- *int* **height** - Height of the 3D texture, in pixels.
- *int* **depth** - Depth of the 3D texture, in pixels.
- *int* **format** - Texture format: one of the [Texture.FORMAT_*](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags.
- *string* **name** - Name to be used for this temporary 3D texture (optional). If not specified, a new name for it will be generated automatically.
- *[Render.TEXTURE_ACCESSORY](../../../api/library/rendering/class.render_cs.md#TEXTURE_ACCESSORY)* **accessory** - Texture render sequence accessory type. One of the [TEXTURE_ACCESSORY_*](#TEXTURE_ACCESSORY_NONE) values.
- *[Render.TEXTURE_LIFETIME](../../../api/library/rendering/class.render_cs.md#TEXTURE_LIFETIME)* **lifetime** - Texture lifetime (the texture will be released automatically when its lifetime expires, if the auto_release flag is set). One of the [TEXTURE_LIFETIME*](#TEXTURE_LIFETIME_FRAME_VIEWPORT) values.
- *bool* **auto_release** - true to enable automatic release of the temporary texture by its [lifetime](#TEXTURE_LIFETIME), false to release it manually.

### Return value

Temporary 3D texture.
## Texture GetTemporaryTextureCube ( int width , int height , int format , int flags = -1 , string name = 0 , Render.TEXTURE_ACCESSORY accessory = TEXTURE_ACCESSORY.NONE , Render.TEXTURE_LIFETIME lifetime = TEXTURE_LIFETIME.FRAME_VIEWPORT , bool auto_release = false )


Allocates a temporary cubemap texture with the specified width, height, format, and flags. This function can be used when you need a quick render texture to perform some temporary calculations. Release it using *[releaseTemporaryTexture()](#releaseTemporaryTexture_Texture_void)* as soon as you're done with it, so another call can start reusing it, if necessary. In any case, such texture shall be released automatically in the next frame.


UNIGINE keeps an internal pool of temporary render textures, so a call to this method most often just returns an already created one (if the size and format match). These temporary textures are actually destroyed when they aren't used for a couple of frames.


If you are doing a series of post-processing "blits", it's best for performance to get and release a temporary render texture for each blit, instead of getting one or two render textures upfront and reusing them.


> **Notice:** You can't rely on any particular contents of a temporary texture obtained from this function: it might be garbage, or it might be cleared to some color, depending on the platform.


### Arguments

- *int* **width** - Width of the cubemap texture, in pixels.
- *int* **height** - Height of the cubemap texture, in pixels.
- *int* **format** - Texture format: one of the [Texture.FORMAT_*](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags.
- *string* **name** - Name to be used for this temporary cubemap texture (optional). If not specified, a new name for it will be generated automatically.
- *[Render.TEXTURE_ACCESSORY](../../../api/library/rendering/class.render_cs.md#TEXTURE_ACCESSORY)* **accessory** - Texture render sequence accessory type. One of the [TEXTURE_ACCESSORY_*](#TEXTURE_ACCESSORY_NONE) values.
- *[Render.TEXTURE_LIFETIME](../../../api/library/rendering/class.render_cs.md#TEXTURE_LIFETIME)* **lifetime** - Texture lifetime (the texture will be released automatically when its lifetime expires, if the auto_release flag is set). One of the [TEXTURE_LIFETIME*](#TEXTURE_LIFETIME_FRAME_VIEWPORT) values.
- *bool* **auto_release** - true to enable automatic release of the temporary texture by its [lifetime](#TEXTURE_LIFETIME), false to release it manually.

### Return value

Temporary cubemap texture.
## Texture GetTemporaryTextureCubeArray ( int width , int height , int depth , int format , int flags = -1 , string name = 0 , Render.TEXTURE_ACCESSORY accessory = TEXTURE_ACCESSORY.NONE , Render.TEXTURE_LIFETIME lifetime = TEXTURE_LIFETIME.FRAME_VIEWPORT , bool auto_release = false )


Allocates a temporary cubemap texture array with the specified width, height, number of layers, format, and flags. This function can be used when you need a quick render texture to perform some temporary calculations. Release it using *[releaseTemporaryTexture()](#releaseTemporaryTexture_Texture_void)* as soon as you're done with it, so another call can start reusing it, if necessary. In any case, such texture shall be released automatically in the next frame.


UNIGINE keeps an internal pool of temporary render textures, so a call to this method most often just returns an already created one (if the size and format match). These temporary textures are actually destroyed when they aren't used for a couple of frames.


If you are doing a series of post-processing "blits", it's best for performance to get and release a temporary render texture for each blit, instead of getting one or two render textures upfront and reusing them.


> **Notice:** You can't rely on any particular contents of a temporary texture obtained from this function: it might be garbage, or it might be cleared to some color, depending on the platform.


### Arguments

- *int* **width** - Width of the cubemap cubemap array, in pixels.
- *int* **height** - Height of the cubemap cubemap array, in pixels.
- *int* **depth** - Number of layers in the cubemap array texture.
- *int* **format** - Texture format: one of the [Texture.FORMAT_*](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags.
- *string* **name** - Name to be used for this temporary cubemap array texture (optional). If not specified, a new name for it will be generated automatically.
- *[Render.TEXTURE_ACCESSORY](../../../api/library/rendering/class.render_cs.md#TEXTURE_ACCESSORY)* **accessory** - Texture render sequence accessory type. One of the [TEXTURE_ACCESSORY_*](#TEXTURE_ACCESSORY_NONE) values.
- *[Render.TEXTURE_LIFETIME](../../../api/library/rendering/class.render_cs.md#TEXTURE_LIFETIME)* **lifetime** - Texture lifetime (the texture will be released automatically when its lifetime expires, if the auto_release flag is set). One of the [TEXTURE_LIFETIME*](#TEXTURE_LIFETIME_FRAME_VIEWPORT) values.
- *bool* **auto_release** - true to enable automatic release of the temporary texture by its [lifetime](#TEXTURE_LIFETIME), false to release it manually.

### Return value

Temporary cubemap texture array.
## Texture GetTemporaryOldTexture ( Material mat , int texture_id , int width , int height , int depth , int format , int flags , int type , string name , Render.TEXTURE_ACCESSORY accessory = TEXTURE_ACCESSORY.NONE )


Allocates a temporary render texture from the previous frame with the specified width, height, depth, format, flags, and accessory type. This function can be used when you need a quick render texture to perform some temporary calculations. This texture doesn't require to be released.


UNIGINE keeps an internal pool of temporary render textures, so a call to this method most often just returns an already created one (if the size and format match). These temporary textures are actually destroyed when they aren't used for a couple of frames.


If you are doing a series of post-processing "blits", it's best for performance to get and release a temporary render texture for each blit, instead of getting one or two render textures upfront and reusing them.


> **Notice:** You can't rely on any particular contents of a temporary texture obtained from this function: it might be garbage, or it might be cleared to some color, depending on the platform.


It also automatically gives names to resources, which can be used for identification in [debug](../../../tools/profiling/microprofile/index_cs.md#gpu_debug_group).


### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **mat** - Material that will use the texture with the specified ID.
- *int* **texture_id** - Texture ID set by the user, value in the range [0, 255].
- *int* **width** - Width of the texture, in pixels.
- *int* **height** - Height of the texture, in pixels.
- *int* **depth** - Depth of the texture, in pixels.
- *int* **format** - Texture format: one of the [Texture.FORMAT_*](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags.
- *int* **type** - Texture type (2D, 3D, Cube, etc.): one of the [Texture.TEXTURE_*](../../../api/library/rendering/class.texture_cs.md#TEXTURE_2D) values.
- *string* **name** - Name to be used for this temporary texture (optional).
- *[Render.TEXTURE_ACCESSORY](../../../api/library/rendering/class.render_cs.md#TEXTURE_ACCESSORY)* **accessory** - Texture render sequence accessory type. One of the [TEXTURE_ACCESSORY_*](#TEXTURE_ACCESSORY_NONE) values.

### Return value

Temporary texture from the previous frame.
## Texture GetTemporaryOldTexture ( Material mat , int texture_id , Texture texture , string name , Render.TEXTURE_ACCESSORY accessory = TEXTURE_ACCESSORY.NONE )


Allocates a temporary render texture from the previous frame for the specified source texture (using all its parameters: resolution, flags, etc.). This function can be used when you need a quick render texture to perform some temporary calculations. This texture doesn't require to be released.


UNIGINE keeps an internal pool of temporary render textures, so a call to this method most often just returns an already created one (if the size and format match). These temporary textures are actually destroyed when they aren't used for a couple of frames.


If you are doing a series of post-processing "blits", it's best for performance to get and release a temporary render texture for each blit, instead of getting one or two render textures upfront and reusing them.


> **Notice:** You can't rely on any particular contents of a temporary texture obtained from this function: it might be garbage, or it might be cleared to some color, depending on the platform.


It also automatically gives names to resources, which can be used for identification in [debug](../../../tools/profiling/microprofile/index_cs.md#gpu_debug_group).


### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **mat** - Material that will use the texture with the specified ID.
- *int* **texture_id** - Texture ID set by the user, value in the range [0, 255].
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Source texture for which a temporary texture is to be allocated in the pool.
- *string* **name** - Name to be used for this temporary texture (optional).
- *[Render.TEXTURE_ACCESSORY](../../../api/library/rendering/class.render_cs.md#TEXTURE_ACCESSORY)* **accessory** - Texture render sequence accessory type. One of the [TEXTURE_ACCESSORY_*](#TEXTURE_ACCESSORY_NONE) values.

### Return value

Temporary texture from the previous frame.
## Texture GetTemporaryOldTexture ( Material mat , int texture_id , Image image , int flags = -1 , string name = 0 , Render.TEXTURE_ACCESSORY accessory = TEXTURE_ACCESSORY.NONE )


Allocates a temporary render texture from the previous frame with the specified width, height, depth, format, flags, and accessory type. This function can be used when you need a quick render texture to perform some temporary calculations. This texture doesn't require to be released.


UNIGINE keeps an internal pool of temporary render textures, so a call to this method most often just returns an already created one (if the size and format match). These temporary textures are actually destroyed when they aren't used for a couple of frames.


If you are doing a series of post-processing "blits", it's best for performance to get and release a temporary render texture for each blit, instead of getting one or two render textures upfront and reusing them.


> **Notice:** You can't rely on any particular contents of a temporary texture obtained from this function: it might be garbage, or it might be cleared to some color, depending on the platform.


It also automatically gives names to resources, which can be used for identification in [debug](../../../tools/profiling/microprofile/index_cs.md#gpu_debug_group).


### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **mat** - Material that will use the texture with the specified ID.
- *int* **texture_id** - Texture ID set by the user, value in the range [0, 255].
- *[Image](../../../api/library/common/class.image_cs.md)* **image**
- *int* **flags** - Texture flags.
- *string* **name** - Name to be used for this temporary texture (optional).
- *[Render.TEXTURE_ACCESSORY](../../../api/library/rendering/class.render_cs.md#TEXTURE_ACCESSORY)* **accessory** - Texture render sequence accessory type. One of the [TEXTURE_ACCESSORY_*](#TEXTURE_ACCESSORY_NONE) values.

### Return value

Temporary 3D texture from the previous frame.
## Texture GetTemporaryOldTexture2D ( Material mat , int texture_id , int width , int height , int format , int flags = -1 , string name = 0 , Render.TEXTURE_ACCESSORY accessory = TEXTURE_ACCESSORY.NONE )


Allocates a temporary 2D texture with the specified width, height, format, and flags. This function can be used when you need a quick render texture to perform some temporary calculations. This texture doesn't require to be released.


UNIGINE keeps an internal pool of temporary render textures, so a call to this method most often just returns an already created one (if the size and format match). These temporary textures are actually destroyed when they aren't used for a couple of frames.


If you are doing a series of post-processing "blits", it's best for performance to get and release a temporary render texture for each blit, instead of getting one or two render textures upfront and reusing them.


> **Notice:** You can't rely on any particular contents of a temporary texture obtained from this function: it might be garbage, or it might be cleared to some color, depending on the platform.


It also automatically gives names to resources, which can be used for identification in [debug](../../../tools/profiling/microprofile/index_cs.md#gpu_debug_group).


### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **mat** - Material that will use the texture with the specified ID.
- *int* **texture_id** - Texture ID set by the user, value in the range [0, 255].
- *int* **width** - Width of the texture, in pixels.
- *int* **height** - Height of the texture, in pixels.
- *int* **format** - Texture format: one of the [Texture.FORMAT_*](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags.
- *string* **name**
- *[Render.TEXTURE_ACCESSORY](../../../api/library/rendering/class.render_cs.md#TEXTURE_ACCESSORY)* **accessory** - Texture render sequence accessory type. One of the [TEXTURE_ACCESSORY_*](#TEXTURE_ACCESSORY_NONE) values.

### Return value

Temporary 2D texture from the previous frame.
## Texture GetTemporaryOldTexture2DArray ( Material mat , int texture_id , int width , int height , int depth , int format , int flags = -1 , string name = 0 , Render.TEXTURE_ACCESSORY accessory = TEXTURE_ACCESSORY.NONE )


Allocates a temporary 2D array texture with the specified width, height, format, and flags. This function can be used when you need a quick render texture to perform some temporary calculations. This texture doesn't require to be released.


UNIGINE keeps an internal pool of temporary render textures, so a call to this method most often just returns an already created one (if the size and format match). These temporary textures are actually destroyed when they aren't used for a couple of frames.


If you are doing a series of post-processing "blits", it's best for performance to get and release a temporary render texture for each blit, instead of getting one or two render textures upfront and reusing them.


> **Notice:** You can't rely on any particular contents of a temporary texture obtained from this function: it might be garbage, or it might be cleared to some color, depending on the platform.


It also automatically gives names to resources, which can be used for identification in [debug](../../../tools/profiling/microprofile/index_cs.md#gpu_debug_group).


### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **mat** - Material that will use the texture with the specified ID.
- *int* **texture_id** - Texture ID set by the user, value in the range [0, 255].
- *int* **width** - Width of the texture, in pixels.
- *int* **height** - Height of the texture, in pixels.
- *int* **depth** - Number of layers in the array, in pixels.
- *int* **format** - Texture format: one of the [Texture.FORMAT_*](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags.
- *string* **name**
- *[Render.TEXTURE_ACCESSORY](../../../api/library/rendering/class.render_cs.md#TEXTURE_ACCESSORY)* **accessory** - Texture render sequence accessory type. One of the [TEXTURE_ACCESSORY_*](#TEXTURE_ACCESSORY_NONE) values.

### Return value

Temporary 2D array texture from the previous frame.
## Texture GetTemporaryOldTexture3D ( Material mat , int texture_id , int width , int height , int depth , int format , int flags = -1 , string name = 0 , Render.TEXTURE_ACCESSORY accessory = TEXTURE_ACCESSORY.NONE )


Allocates a temporary 3D texture with the specified width, height, format, and flags. This function can be used when you need a quick render texture to perform some temporary calculations. This texture doesn't require to be released.


UNIGINE keeps an internal pool of temporary render textures, so a call to this method most often just returns an already created one (if the size and format match). These temporary textures are actually destroyed when they aren't used for a couple of frames.


If you are doing a series of post-processing "blits", it's best for performance to get and release a temporary render texture for each blit, instead of getting one or two render textures upfront and reusing them.


> **Notice:** You can't rely on any particular contents of a temporary texture obtained from this function: it might be garbage, or it might be cleared to some color, depending on the platform.


It also automatically gives names to resources, which can be used for identification in [debug](../../../tools/profiling/microprofile/index_cs.md#gpu_debug_group).


### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **mat** - Material that will use the texture with the specified ID.
- *int* **texture_id** - Texture ID set by the user, value in the range [0, 255].
- *int* **width** - Width of the texture, in pixels.
- *int* **height** - Height of the texture, in pixels.
- *int* **depth** - Depth of the texture, in pixels.
- *int* **format** - Texture format: one of the [Texture.FORMAT_*](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags.
- *string* **name** - Name to be used for this temporary texture (optional).
- *[Render.TEXTURE_ACCESSORY](../../../api/library/rendering/class.render_cs.md#TEXTURE_ACCESSORY)* **accessory** - Texture render sequence accessory type. One of the [TEXTURE_ACCESSORY_*](#TEXTURE_ACCESSORY_NONE) values.

### Return value

Temporary 3D texture from the previous frame.
## Texture GetTemporaryOldTextureCube ( Material mat , int texture_id , int width , int height , int format , int flags = -1 , string name = 0 , Render.TEXTURE_ACCESSORY accessory = TEXTURE_ACCESSORY.NONE )


Allocates a temporary cubemap texture with the specified width, height, format, and flags. This function can be used when you need a quick render texture to perform some temporary calculations. This texture doesn't require to be released.


UNIGINE keeps an internal pool of temporary render textures, so a call to this method most often just returns an already created one (if the size and format match). These temporary textures are actually destroyed when they aren't used for a couple of frames.


If you are doing a series of post-processing "blits", it's best for performance to get and release a temporary render texture for each blit, instead of getting one or two render textures upfront and reusing them.


> **Notice:** You can't rely on any particular contents of a temporary texture obtained from this function: it might be garbage, or it might be cleared to some color, depending on the platform.


It also automatically gives names to resources, which can be used for identification in [debug](../../../tools/profiling/microprofile/index_cs.md#gpu_debug_group).


### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **mat** - Material that will use the texture with the specified ID.
- *int* **texture_id** - Texture ID set by the user, value in the range [0, 255].
- *int* **width** - Width of the texture, in pixels.
- *int* **height** - Height of the texture, in pixels.
- *int* **format** - Texture format: one of the [Texture.FORMAT_*](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags.
- *string* **name** - Name to be used for this temporary texture (optional).
- *[Render.TEXTURE_ACCESSORY](../../../api/library/rendering/class.render_cs.md#TEXTURE_ACCESSORY)* **accessory** - Texture render sequence accessory type. One of the [TEXTURE_ACCESSORY_*](#TEXTURE_ACCESSORY_NONE) values.

### Return value

Temporary cubemap texture from the previous frame.
## Texture GetTemporaryOldTextureCubeArray ( Material mat , int texture_id , int width , int height , int depth , int format , int flags = -1 , string name = 0 , Render.TEXTURE_ACCESSORY accessory = TEXTURE_ACCESSORY.NONE )


Allocates a temporary cubemap texture array with the specified width, height, format, and flags. This function can be used when you need a quick render texture to perform some temporary calculations. This texture doesn't require to be released.


UNIGINE keeps an internal pool of temporary render textures, so a call to this method most often just returns an already created one (if the size and format match). These temporary textures are actually destroyed when they aren't used for a couple of frames.


If you are doing a series of post-processing "blits", it's best for performance to get and release a temporary render texture for each blit, instead of getting one or two render textures upfront and reusing them.


> **Notice:** You can't rely on any particular contents of a temporary texture obtained from this function: it might be garbage, or it might be cleared to some color, depending on the platform.


It also automatically gives names to resources, which can be used for identification in [debug](../../../tools/profiling/microprofile/index_cs.md#gpu_debug_group).


### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **mat** - Material that will use the texture with the specified ID.
- *int* **texture_id** - Texture ID set by the user, value in the range [0, 255].
- *int* **width** - Width of the texture, in pixels.
- *int* **height** - Height of the texture, in pixels.
- *int* **depth** - Number of layers in the cubemap array texture.
- *int* **format** - Texture format: one of the [Texture.FORMAT_*](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) values.
- *int* **flags** - Texture flags.
- *string* **name** - Name to be used for this temporary texture (optional).
- *[Render.TEXTURE_ACCESSORY](../../../api/library/rendering/class.render_cs.md#TEXTURE_ACCESSORY)* **accessory** - Texture render sequence accessory type. One of the [TEXTURE_ACCESSORY_*](#TEXTURE_ACCESSORY_NONE) values.

### Return value

Temporary cubemap texture array from the previous frame.
## void ReleaseTemporaryTexture ( Texture texture )

Releases the temporary texture previously obtained via *[getTemporaryTexture()](#getTemporaryTexture_Texture_cstr_int_int_int_Texture)*, *[getTemporaryTexture2D()](#getTemporaryTexture2D_int_int_int_int_cstr_int_int_int_Texture)*, *[getTemporaryTexture2DArray()](#getTemporaryTexture2DArray_int_int_int_int_int_cstr_int_int_int_Texture)*, *[getTemporaryTexture3D()](#getTemporaryTexture3D_int_int_int_int_int_cstr_int_int_int_Texture)*, *[getTemporaryTextureCube()](#getTemporaryTextureCube_int_int_int_int_cstr_int_int_int_Texture)*, or *[getTemporaryTextureCubeArray()](#getTemporaryTextureCubeArray_int_int_int_int_int_cstr_int_int_int_Texture)* method and returns it to the pool.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Temporary texture or texture array to be returned to the pool.

## void ReleaseTemporaryTextures ( Texture [] textures )

Releases the specified list of temporary textures previously obtained via *[getTemporaryTexture()](#getTemporaryTexture_Texture_cstr_int_int_int_Texture)*, *[getTemporaryTexture2D()](#getTemporaryTexture2D_int_int_int_int_cstr_int_int_int_Texture)*, *[getTemporaryTexture2DArray()](#getTemporaryTexture2DArray_int_int_int_int_int_cstr_int_int_int_Texture)*, *[getTemporaryTexture3D()](#getTemporaryTexture3D_int_int_int_int_int_cstr_int_int_int_Texture)*, *[getTemporaryTextureCube()](#getTemporaryTextureCube_int_int_int_int_cstr_int_int_int_Texture)*, or *[getTemporaryTextureCubeArray()](#getTemporaryTextureCubeArray_int_int_int_int_int_cstr_int_int_int_Texture)* method and returns it to the pool.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)[]* **textures** - List of temporary textures or texture arrays to be returned to the pool.

## bool IsTemporaryTexture ( Texture texture )

Returns a value indicating if the specified texture is a temporary one.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Texture to be checked.

### Return value

true if the specified texture is a temporary one; otherwise, false.
## bool IsTemporaryOldTexture ( Texture texture )

Returns a value indicating if the specified texture is a temporary texture from the previous frame.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Texture to be checked.

### Return value

true if the specified texture is a temporary texture from the previous frame; otherwise, false.
## RenderTarget GetTemporaryRenderTarget ( )


Allocates a temporary [render target](../../../api/library/rendering/class.rendertarget_cs.md). This function can be used when you need a quick render target to perform some temporary calculations. Release it using [*releaseTemporaryRenderTarget()*](#releaseTemporaryRenderTarget_RenderTarget_void) as soon as you're done with it, so another call can start reusing it if necessary. In any case such render target shall be released automatically in the next frame.


UNIGINE keeps an internal pool of temporary render targets, so a call to this method most often just returns an already created one (if the size and format matches). These temporary render targets are actually destroyed when they aren't used for a couple of frames.


If you are doing a series of post-processing "blits", it's best for performance to get and release a temporary render targets for each blit, instead of getting one or two render targets upfront and reusing them.

> **Notice:** You can't depend on any particular contents of a temporary render target obtained from this function: it might be garbage, or it might be cleared to some color, depending on the platform.


### Return value

Temporary render target.
## void ReleaseTemporaryRenderTarget ( RenderTarget render_target )

Releases the temporary [render target](../../../api/library/rendering/class.rendertarget_cs.md) previously obtained via [*getTemporaryRenderTarget()*](#getTemporaryRenderTarget_RenderTarget) method and returns it to the pool.
### Arguments

- *[RenderTarget](../../../api/library/rendering/class.rendertarget_cs.md)* **render_target** - Temporary render target to be returned to the pool.

## int CompressImage ( TextureToImageTransfered on_compressed , Image image , int quality = 1 , int new_image_format = -1 , int use_mip_maps = -1 )

Converts the image to a specified compressed format. The result is to be processed in the callback function specified. If compression by the GPU is not supported, the *[Image::compress()](../../../api/library/common/class.image_cs.md#compress_int_int)* method will be called instead.
### Arguments

- *TextureToImageTransfered* **on_compressed** - Callback function to be fired on compressing an image.
- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to compress.
- *int* **quality** - Compression quality:

  - 0 - fast compression, low compressed image quality.
  - 1 - high compressed image quality, slow compression (by default).
- *int* **new_image_format** - Compressed texture format: one of the [Texture::FORMAT_*](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) variables. This is an optional argument. If no format is specified, default conversion will be performed (depending on the type of the source image).
- *int* **use_mip_maps** - Flag indicating whether texture mipmaps should be generated for the compressed image: 1 to generate mipmaps, 0 not to generate. This is an optional argument. If no value is specified, mipmaps will be generated only if the source image has the mipmaps.

### Return value

1 if the image has been compressed successfully; otherwise, 0.
## int CompressTexture ( TextureToImageTransfered on_compressed , Texture texture , Image destination , int quality = 1 , int new_texture_format = -1 , int use_mip_maps = -1 )

Compresses the given texture to the specified format. The result is to be processed in the callback function specified.
> **Notice:** Only 2d and 2d array textures can be compressed.


### Arguments

- *TextureToImageTransfered* **on_compressed** - Callback function to be called on compressing the texture where you can get the result.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Source texture to compress.
- *[Image](../../../api/library/common/class.image_cs.md)* **destination** - Image into which the compressed texture will be saved.
- *int* **quality** - Compression quality:

  - 0 - fast compression, low compressed image quality.
  - 1 - high compressed image quality, slow compression (by default).
- *int* **new_texture_format** - Compressed texture format: one of the [Texture::FORMAT_*](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1) variables. This is an optional argument. If no format is specified, default conversion will be performed (depending on the type of the source image).
- *int* **use_mip_maps** - Flag indicating whether texture mipmaps should be generated for the compressed image: 1 to generate mipmaps, 0 not to generate. This is an optional argument. If no value is specified, mipmaps will be generated only if the source image has the mipmaps.

### Return value

1 if the texture has been compressed successfully; otherwise, 0.
## int AsyncCompressTexture ( TextureToImageTransfered on_compressed , TextureToImageTransfered on_compressed_async , Texture texture , int quality = 1 , int new_texture_format = -1 , int use_mip_maps = -1 )

Performs asynchronous compression of the specified texture and transfers it to CPU side (*Image*). The method enables you to specify a callback function in which you can process the obtained result (resulting *[Image](../../../api/library/common/class.image_cs.md)*).
> **Notice:** Only 2d and 2d array textures can be compressed.

### Arguments

- *TextureToImageTransfered* **on_compressed** - Callback function to be called in the main thread upon completion of the transfer operation where you can get the result.The function should have the following signature: void TextureToImageTransfered(*Image* **image**). You can pass NULL if this callback is not needed.
- *TextureToImageTransfered* **on_compressed_async** - Callback function to be called right in the async thread upon completion of the transfer operation where you can get the result.The function should have the following signature: void TextureToImageTransfered(*Image* **image**). You can pass NULL if this callback is not needed.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Source texture to be transferred to an *[Image](../../../api/library/common/class.image_cs.md)* (GPU -> CPU).
- *int* **quality** - Compression quality:

  - 0 - fast compression, low compressed image quality.
  - 1 - high compressed image quality, slow compression (by default).
- *int* **new_texture_format** - Compressed texture format: one of the *[Texture.FORMAT_*](../../../api/library/rendering/class.texture_cs.md#FORMAT_ATI1)* variables. This is an optional argument. If no format is specified, default conversion will be performed (depending on the type of the source).
- *int* **use_mip_maps** - Flag indicating whether texture mipmaps should be generated for the compressed image: 1 to generate mipmaps, 0 not to generate. This is an optional argument. If no value is specified, mipmaps will be generated only if the source has mipmaps.

### Return value

1 if the source texture has been compressed and transferred to CPU successfully; otherwise, 0.
## int AsyncCompressImage ( TextureToImageTransfered on_compressed , TextureToImageTransfered on_compressed_async , Image image , int quality = 1 , int new_image_format = -1 , int use_mip_maps = -1 )

Performs asynchronous compression of the specified image. The method enables you to specify a callback function in which you can process the obtained result (resulting *[Image](../../../api/library/common/class.image_cs.md)*).
> **Notice:** Only 2d and 2d array images can be compressed.

### Arguments

- *TextureToImageTransfered* **on_compressed** - Callback function to be called in the main thread upon completion of the compress operation where you can get the result.The function should have the following signature: void TextureToImageTransfered(*Image* **image**). You can pass NULL if this callback is not needed.
- *TextureToImageTransfered* **on_compressed_async** - Callback function to be called right in the async thread upon completion of the compress operation where you can get the result.The function should have the following signature: void TextureToImageTransfered(*Image* **image**). You can pass NULL if this callback is not needed.
- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to be compressed.
- *int* **quality** - Compression quality:

  - 0 - fast compression, low compressed image quality.
  - 1 - high compressed image quality, slow compression (by default).
- *int* **new_image_format** - Compressed image format: one of the *[Image.FORMAT_*](../../../api/library/common/class.image_cs.md#FORMAT_ATI1)* variables. This is an optional argument. If no format is specified, default conversion will be performed (depending on the type of the source).
- *int* **use_mip_maps** - Flag indicating whether mipmaps should be generated for the compressed image: 1 to generate mipmaps, 0 not to generate. This is an optional argument. If no value is specified, mipmaps will be generated only if the source image has the mipmaps.

### Return value

1 if the source image has been compressed successfully; otherwise, 0.
## void TransferTextureToImage ( TextureToImageTransfered on_transfered , Texture src )

Transfers the specified source texture to an *[Image](../../../api/library/common/class.image_cs.md)* (from GPU to CPU side). The method enables you to specify a callback function in which you can process the obtained result (resulting *[Image](../../../api/library/common/class.image_cs.md)*). The result will be obtained at the *swap* stage of the same frame (calls CPU-GPU synchronization).
### Arguments

- *TextureToImageTransfered* **on_transfered** - Callback function to be called upon completion of the transfer operation where you can get the result.The function should have the following signature: void TextureToImageTransfered(*Image* **image**).
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **src** - Source texture to be transferred to an *[Image](../../../api/library/common/class.image_cs.md)* (GPU -> CPU).

## void AsyncTransferTextureToImage ( TextureToImageTransfered on_transfered , TextureToImageTransfered on_transfered_async , Texture src )

Transfers the specified source texture to an *[Image](../../../api/library/common/class.image_cs.md)* (from GPU to CPU side) asynchronously, without CPU-GPU synchronization. The method enables you to specify a callback function in which you can process the obtained result (resulting *[Image](../../../api/library/common/class.image_cs.md)*). The result will be obtained later in one of the subsequent frames.
```csharp
// creating a new texture
Texture texture = new Texture();

// rendering to a texture
viewport.RenderTexture2D(player.Camera, texture, width, height);

// transferring texture (GPU) data to CPU
Render.AsyncTransferTextureToImage(
	null,
	(Image image) =>
		{
			// flipping image if necessary
			if (!Render.IsFlipped)
				image.FlipY();

			// saving an image to a file
			image.Save("screenshot.texture");
		},
	texture);

```


### Arguments

- *TextureToImageTransfered* **on_transfered** - Callback function to be called in the main thread upon completion of the transfer operation where you can get the result.The function should have the following signature: void TextureToImageTransfered(*Image* **image**). You can pass NULL if this callback is not needed.
- *TextureToImageTransfered* **on_transfered_async** - Callback function to be called right in the async thread upon completion of the transfer operation where you can get the result.The function should have the following signature: void TextureToImageTransfered(*Image* **image**). You can pass NULL if this callback is not needed.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **src** - Source texture to be transferred to an *[Image](../../../api/library/common/class.image_cs.md)* (GPU -> CPU).

## void AsyncTransferStructuredBuffer ( StructuredBufferTransfered on_transfered , StructuredBufferTransfered on_transfered_async , StructuredBuffer src )

Transfers the data of the specified source structured buffer from GPU to CPU side asynchronously, without CPU-GPU synchronization. The method enables you to specify a callback function in which you can process the obtained result. The result will be obtained later in one of the subsequent frames.
### Arguments

- *StructuredBufferTransfered* **on_transfered** - Callback function to be called in the main thread upon completion of the transfer operation where you can get the result.The function should have the following signature: void StructuredBufferTransfered(*IntPtr* **dest**). You can pass NULL if this callback is not needed.
- *StructuredBufferTransfered* **on_transfered_async** - Callback function to be called right in the async upon completion of the transfer operation where you can get the result.The function should have the following signature: void StructuredBufferTransfered(*IntPtr* **dest**). You can pass NULL if this callback is not needed.
- *[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cs.md)* **src** - Source structured buffer to be transferred (GPU -> CPU).

## void TransferStructuredBuffer ( StructuredBufferTransfered on_transfered , StructuredBuffer src )

Transfers the data of the specified source structured buffer from GPU to CPU side. The method enables you to specify a callback function in which you can process the obtained result. The result will be obtained at the *swap* stage of the same frame (calls CPU-GPU synchronization).
### Arguments

- *StructuredBufferTransfered* **on_transfered** - Callback function to be called in the main thread upon completion of the transfer operation.The function should have the following signature: void StructuredBufferTransfered(*IntPtr* **dest**).
- *[StructuredBuffer](../../../api/library/rendering/class.structuredbuffer_cs.md)* **src** - Source structured buffer to be transferred (GPU -> CPU).

## bool CreateMipmapsCubeGGXImage ( Image image , Texture dest , Render.GGX_MIPMAPS_QUALITY quality )

Generates mipmaps for a cubemap image using GGX BRDF microfacet model.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Cubemap image. [IMAGE_CUBE](../../../api/library/common/class.image_cs.md#IMAGE_CUBE) or [IMAGE_CUBE_ARRAY](../../../api/library/common/class.image_cs.md#IMAGE_CUBE_ARRAY) types are accepted.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **dest** - Destination [Texture](../../../api/library/rendering/class.texture_cs.md) instance to save the result.
- *[Render.GGX_MIPMAPS_QUALITY](../../../api/library/rendering/class.render_cs.md#GGX_MIPMAPS_QUALITY)* **quality** - Quality of GGX mipmaps. One of the *[GGX_MIPMAPS_QUALITY](#GGX_MIPMAPS_QUALITY)* values.

### Return value

true if mipmaps for the specified cubemap image were generated successfully; otherwise - false.
## bool CreateMipmapsCubeGGXTexture ( Texture texture , Render.GGX_MIPMAPS_QUALITY quality , bool realtime = true )

Generates mipmaps for a cubemap texture using GGX BRDF microfacet model.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Cubemap texture. [TEXTURE_CUBE](../../../api/library/rendering/class.texture_cs.md#TEXTURE_CUBE) or [TEXTURE_CUBE_ARRAY](../../../api/library/rendering/class.texture_cs.md#TEXTURE_CUBE_ARRAY) types are accepted.
- *[Render.GGX_MIPMAPS_QUALITY](../../../api/library/rendering/class.render_cs.md#GGX_MIPMAPS_QUALITY)* **quality** - Quality of GGX mipmaps. One of the *[GGX_MIPMAPS_QUALITY](#GGX_MIPMAPS_QUALITY)* values.
- *bool* **realtime** - true if the operation should be performed in real-time mode; otherwise - false.

### Return value

true if mipmaps for the specified cubemap image were generated successfully; otherwise - false.
## int CreateShorelineDistanceField ( Texture image , Image mask , int shoreline_radius , int blur_radius , int downsample_resolution )

Grabs a shoreline distance field texture with the specified parameters.
### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **image** - Texture to grab a shoreline texture to.
- *[Image](../../../api/library/common/class.image_cs.md)* **mask** - An **R16** mask texture Image. Each pixel of the mask has the following color value:0 if water level at this point of the grid is above the terrain level; otherwise, 65535.
- *int* **shoreline_radius** - Shoreline radius value within the **[4; 128]** range. Padding distance (from the shore to the beginning of swash zone).
- *int* **blur_radius** - Blur radius value within the **[0; 32]** range. Higher values make shoreline smoother.
- *int* **downsample_resolution** - Texture resolution value, can be one of the following: **16, 32, 64, 128, 256, 512, 1024, 2048**.

### Return value

1 if the shoreline distance field texture is grabbed successfully; otherwise, 0.
## int SetColorCorrectionLUTImage ( Image image )

Sets a new color transformation image (LUT). This function resets a LUT texture name to null if it has been previously set via [setColorCorrectionLUTPath()](#setColorCorrectionLUTPath_cstr_void).
```csharp
Image lut;
Image lut_0;
Image lut_1;

lut = new Image();
lut_0 = new Image("unigine_project/textures/lookup_first.texture");
lut_1 = new Image("unigine_project/textures/lookup_second.texture");

float k = MathLib.Sin(Game.Time * 2.0f) * 0.5f + 0.5f;

lut.Copy(lut_0,0);
lut.Blend(lut_1, 0, 0, 0, 0, lut.GetWidth(), lut.GetHeight(), k);

Render.SetColorCorrectionLUTImage(lut);

```


### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Color transformation image.

### Return value

1 if the image is set successfully; otherwise, 0.
## int GetColorCorrectionLUTImage ( Image image )

Return the current color transformation image (LUT).
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to store the color transformation texture in.

### Return value

1 if an image is successfully received; otherwise, 0.
## void ResetColorCorrectionRamp ( )

Resets the [Color Correction ramp](../../../editor2/settings/render_settings/color/index.md#color_curve) to the default value.
![](default_color_curve.png)


## void ResetColorCorrectionSaturationRamp ( )

Resets the [Saturation Correction ramp](../../../editor2/settings/render_settings/color/index.md#saturation) to the default value.
![](default_saturation_curve.png)


## void ResetAutoExposureRamp ( )

Resets the correction curve for the overall scene saturation.
## bool LoadSettings ( string file , bool clear = false )

Loads render settings from a given file.
### Arguments

- *string* **file** - Path to an XML file with desired settings.
- *bool* **clear** - Clear flag. Set true to clear settings before loading (new settings shall be applied right after loading them), or false not to clear.

### Return value

1 if the settings are loaded successfully; otherwise, 0.
## bool LoadWorld ( Xml xml )

Loads render state from the Xml.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Xml node.

### Return value

true if the state is loaded successfully; otherwise, false.
## void RenderComputeMaterial ( Render.PASS pass , Material material , int width , int height , int depth = 1 )

Sets up a material and dispatches to compute shader. The material must have a post shader associated with it.
### Arguments

- *[Render.PASS](../../../api/library/rendering/class.render_cs.md#PASS)* **pass** - Rendering pass number in range [0;[NUM_PASSES](#NUM_PASSES)) (one of the *[PASS_*](#PASS_WIREFRAME)* variables).
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Material to be used.
- *int* **width** - Local X work-group size of the compute shader.
- *int* **height** - Local Y work-group size of the compute shader.
- *int* **depth** - Local Z work-group size of the compute shader. The default value is 1.

## void RenderTexture2D ( Camera camera , Texture texture , int skip_flags )

Renders the scene into a 2D texture in accordance with the specified parameters. The viewport position is taken from the camera created via [Camera](../../../api/library/rendering/class.camera_cs.md) class.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - [Camera](../../../api/library/rendering/class.camera_cs.md) to be used.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - [Texture](../../../api/library/rendering/class.texture_cs.md) to save the result to.
- *int* **skip_flags** - Skip the effects: 0 enables all the effects.

  - VIEWPORT_SKIP_SHADOWS
  - VIEWPORT_SKIP_VISUALIZER
  - VIEWPORT_SKIP_SRGB
  - VIEWPORT_SKIP_POSTEFFECTS
  - VIEWPORT_SKIP_VELOCITY
  - VIEWPORT_SKIP_DYNAMIC_REFLECTIONS

## void RenderTexture2D ( Camera camera , Texture texture , int width , int height , int hdr , int skip_flags )

Renders the scene into a 2D texture of the given size in accordance with the specified parameters. The viewport position is taken from the camera created via [Camera](../../../api/library/rendering/class.camera_cs.md) class.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - [Camera](../../../api/library/rendering/class.camera_cs.md) to be used.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - [Texture](../../../api/library/rendering/class.texture_cs.md) to save the result to.
- *int* **width** - Width of the projected texture, in units.
- *int* **height** - Height of the projected texture, in units.
- *int* **hdr** - 1 - enable HDR, 0 - disable HDR.
- *int* **skip_flags** - Skip the effects: 0 enables all the effects.

  - VIEWPORT_SKIP_SHADOWS
  - VIEWPORT_SKIP_VISUALIZER
  - VIEWPORT_SKIP_SRGB
  - VIEWPORT_SKIP_POSTEFFECTS
  - VIEWPORT_SKIP_VELOCITY
  - VIEWPORT_SKIP_DYNAMIC_REFLECTIONS

## void RenderTextureCube ( Camera camera , Texture texture , int skip_flags )

Renders the scene into a cube map texture in accordance with the specified parameters.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - [Camera](../../../api/library/rendering/class.camera_cs.md) to be used.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - [Texture](../../../api/library/rendering/class.texture_cs.md) to save the result to.
- *int* **skip_flags** - Skip the effects: 0 enables all the effects.

  - VIEWPORT_SKIP_SHADOWS
  - VIEWPORT_SKIP_VISUALIZER
  - VIEWPORT_SKIP_SRGB
  - VIEWPORT_SKIP_POSTEFFECTS
  - VIEWPORT_SKIP_VELOCITY
  - VIEWPORT_SKIP_DYNAMIC_REFLECTIONS

## void RenderTextureCube ( Camera camera , Texture texture , int size , int hdr , int skip_flags , bool local_space = 0 )

Renders the scene into a cube map in accordance with the specified parameters. The viewport position is taken from the camera created via [Camera](../../../api/library/rendering/class.camera_cs.md) class.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - [Camera](../../../api/library/rendering/class.camera_cs.md) to be used.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - [Texture](../../../api/library/rendering/class.texture_cs.md) to save the result to.
- *int* **size** - Texture dimensions (cube map edge size).
- *int* **hdr** - 1 - enable HDR; 0 - disable HDR.
- *int* **skip_flags** - Skip the effects: 0 enables all the effects.

  - VIEWPORT_SKIP_SHADOWS
  - VIEWPORT_SKIP_VISUALIZER
  - VIEWPORT_SKIP_SRGB
  - VIEWPORT_SKIP_POSTEFFECTS
  - VIEWPORT_SKIP_VELOCITY
  - VIEWPORT_SKIP_DYNAMIC_REFLECTIONS
- *bool* **local_space** - 1 - local space coordinates; 0 - world space coordinates.

## void RenderNodeTexture2D ( Camera camera , Node node , Texture texture , int skip_flags , int light_usage , string environment_texture_name )

Renders the given node into a 2D texture in accordance with the specified parameters. The viewport position is taken from the camera created via [Camera](../../../api/library/rendering/class.camera_cs.md) class. The node can be rendered using the specific type of lighting and environment cubemap.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - [Camera](../../../api/library/rendering/class.camera_cs.md) to be used.
- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - [Node](../../../api/library/nodes/class.node_cs.md) to be rendered.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - [Texture](../../../api/library/rendering/class.texture_cs.md) to save the result to.
- *int* **skip_flags** - Skip the effects. One of the [SKIP_*](../../../api/library/rendering/class.viewport_cs.md#SKIP_DYNAMIC_REFLECTIONS) variables should be specified. 0 enables all the effects.
- *int* **light_usage** - Sets the light sources that will affect the node (one of the [USAGE_*_LIGHTING](../../../api/library/rendering/class.viewport_cs.md#USAGE_WORLD_LIGHT) Viewport class variables.)
- *string* **environment_texture_name** - Path to the environment cubemap to be used. Takes effect if the [first](../../../api/library/rendering/class.viewport_cs.md#USAGE_AUX_LIGHT) (auxiliary light) or [second](../../../api/library/rendering/class.viewport_cs.md#USAGE_NODE_LIGHT) (node light) lighting mode is used (see the *light_usage* argument above). In case LightWorld is used ([zero mode](../../../api/library/rendering/class.viewport_cs.md#USAGE_WORLD_LIGHT)), the environment cubemap used for the current world will be used.

## void RenderNodeTexture2D ( Camera camera , Node node , Texture texture , int width , int height , int hdr , int skip_flags , int light_usage , string environment_texture_name )

Renders the 2D texture of the given node in accordance with the specified parameters. The viewport position is taken from the camera created via [Camera](../../../api/library/rendering/class.camera_cs.md) class. The node can be rendered using the specific type of lighting and environment cubemap.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_cs.md)* **camera** - [Camera](../../../api/library/rendering/class.camera_cs.md) to be used.
- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - [Node](../../../api/library/nodes/class.node_cs.md) to be rendered.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - [Texture](../../../api/library/rendering/class.texture_cs.md) to save the result to.
- *int* **width** - Width of the texture, in units.
- *int* **height** - Height of the texture, in units.
- *int* **hdr** - HDR flag. This parameter determines the format of the 2D texture:

  - 1 - texture format will be set to **RGBA16F**. It means that the HDR texture buffer will store pixel values outside the [0;1] range (i.e. both negative and positive values).
  - 0 - texture format will be set to **RGBA8**.
- *int* **skip_flags** - Skip the effects. One of the [SKIP_*](../../../api/library/rendering/class.viewport_cs.md#SKIP_DYNAMIC_REFLECTIONS) variables should be specified. 0 enables all the effects.
- *int* **light_usage** - Sets the light sources that will affect the node (one of the [USAGE_*_LIGHTING](../../../api/library/rendering/class.viewport_cs.md#USAGE_WORLD_LIGHT) Viewport class variables).
- *string* **environment_texture_name** - Path to the environment cubemap to be used. Takes effect if the [first](../../../api/library/rendering/class.viewport_cs.md#USAGE_AUX_LIGHT) (auxiliary light) or [second](../../../api/library/rendering/class.viewport_cs.md#USAGE_NODE_LIGHT) (node light) lighting mode is used (see the *light_usage* argument above). In case LightWorld is used ([zero mode](../../../api/library/rendering/class.viewport_cs.md#USAGE_WORLD_LIGHT)), the environment cubemap used for the current world will be used.

## void RenderScreenMaterial ( string material_name )

Renders a screen-space material with the given name.
```csharp
RenderTarget render_target;
//...
render_target.Enable();
Render.RenderScreenMaterial("new_material_post");
render_target.Disable();
render_target.UnbindColorTextures();

```


### Arguments

- *string* **material_name** - Material name.

## void RenderScreenMaterial ( string material_name , Texture color_texture )

Renders a screen-space material with the specified name and the color texture.
```csharp
RenderTarget render_target;
Texture texture;
Texture texture_2;
//...
render_target.BindColorTexture(0, texture);
render_target.Enable();
Render.RenderScreenMaterial("new_material_post", texture);
render_target.Disable();
render_target.UnbindColorTextures();

```


### Arguments

- *string* **material_name** - Material name.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **color_texture** - Color texture.

## void RenderScreenMaterial ( string material_name , string texture_name , Texture texture )

Renders a screen-space material with the given texture. For example:
```csharp
RenderTarget render_target;
Texture texture;
Texture texture_2;
//...
render_target.bindColorTexture(0, texture);
render_target.enable();
Material material = Materials.findMaterial("new_material_post");
render.renderScreenMaterial(material, "color", texture_2);
render_target.disable();
render_target.unbindColorTextures();

```


### Arguments

- *string* **material_name** - Material.
- *string* **texture_name** - Material texture name.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **texture** - Texture.

## void RenderTAA ( Texture color_texture , Texture color_old_texture )


```csharp
RenderTarget render_target;
Texture buffer;
Texture buffer_old;
Texture buffer_taa;
//...
render_target.BindColorTexture(0, buffer_taa);
render_target.Enable();
Render.RenderTAA(buffer, buffer_old);
render_target.Disable();
render_target.UnbindColorTextures();

```


### Arguments

- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **color_texture** - Color texture.
- *[Texture](../../../api/library/rendering/class.texture_cs.md)* **color_old_texture** - Old color texture.

## bool SaveSettings ( string file )

Saves the current renderer settings to a given file.
### Arguments

- *string* **file** - Path to a target file.

### Return value

true if the settings are saved successfully; otherwise, false.
## bool SaveState ( Stream stream )

Saves a render state into the stream.
Saving into the stream requires creating a blob to save into. To restore the saved state the [RestoreState()](#restoreState_Stream_int) method is used:


```csharp
// set state
Render.CloudsInterleavedRendering = 0; // interleave = 0

// save state
Blob blob_state = new Blob();
Render.SaveState(blob_state);

// change state
Render.CloudsInterleavedRendering = 2; // now interleave = 2

// restore state
blob_state.SeekSet(0);		// returning the carriage to the start of the blob
Render.RestoreState(blob_state); // restore interleave = 0

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to save a state into.

### Return value

true if the state is saved successfully; otherwise, false.
## bool RestoreState ( Stream stream )

Restores a render state from the stream.
Restoring from the stream requires creating a blob to save into and saving the state using the [SaveState()](#saveState_Stream_int) method:


```csharp
// set state
Render.CloudsInterleavedRendering = 0; // interleave = 0

// save state
Blob blob_state = new Blob();
Render.SaveState(blob_state);

// change state
Render.CloudsInterleavedRendering = 2; // now interleave = 2

// restore state
blob_state.SeekSet(0);		// returning the carriage to the start of the blob
Render.RestoreState(blob_state); // restore interleave = 0

```


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to restore a state from.

### Return value

true if the state is restored successfully; otherwise, false.
## bool SaveWorld ( Xml xml )

Saves the render state into the given Xml node.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Xml node.

### Return value

true if the state is saved successfully; otherwise, false.
## RenderEnvironmentPreset GetEnvironmentPreset ( int num )

Returns the environment preset of the given number.
```csharp
// get the second environment preset
RenderEnvironmentPreset preset = Render.GetEnvironmentPreset(1);
// print the sky intensity of the obtained preset
Log.Message("{0}\n", preset.GetSkyIntensity());

```


### Arguments

- *int* **num** - The number of the environment preset. The value is clamped to the [0;2] range.

### Return value

Environment preset.
## string GetCloudsQualityPresetName ( int num )

Returns the Clouds Quality preset name by given index.
### Arguments

- *int* **num** - Clouds Quality preset index.

### Return value

Clouds Quality preset name.
## string GetAAPresetName ( int num )

Returns the AA (Anti-Aliasing) preset name by given index.
### Arguments

- *int* **num** - AA preset index.

### Return value

AA preset name.
## string GetTAAPresetName ( int num )

Returns the TAA (Temporal Anti-Aliasing) preset name by given index.
### Arguments

- *int* **num** - TAA preset index.

### Return value

TAA preset name.
## string GetDenoisePresetName ( int num )

Returns the denoiser preset name by given index.
### Arguments

- *int* **num** - Denoiser preset index.

### Return value

Denoiser preset name.
## string GetSSRTGIPresetName ( int num )

Returns the SSRTGI (Screen-Space Ray-Traced Global Illumination) preset name by given index.
### Arguments

- *int* **num** - SSRTGI preset index.

### Return value

SSRTGI preset name.
## string GetSSRPresetName ( int num )

Returns the SSR preset name by given index.
### Arguments

- *int* **num** - SSR preset index.

### Return value

SSR preset name.
## string GetSSSSSPresetName ( int num )

Returns the SSSSS preset name by given index.
### Arguments

- *int* **num** - SSSSS preset index.

### Return value

SSSSS preset name.
## string GetMotionBlurPresetName ( int num )

Returns the Motion Blur preset name by given index.
### Arguments

- *int* **num**

### Return value

Motion Blur preset name.
## string GetDOFPresetName ( int num )

Returns the DOF preset name by given index.
### Arguments

- *int* **num**

### Return value

DOF preset name.
## string GetLandscapeTerrainGeometryPresetName ( int num )

Returns the Landscape Terrain Geometry preset name by given index.
### Arguments

- *int* **num** - Landscape Terrain Geometry preset index.

### Return value

Landscape Terrain Geometry preset name.
## string GetLandscapeTerrainStreamingPresetName ( int num )

Returns the Landscape Terrain Streaming preset name by given index.
### Arguments

- *int* **num** - Landscape Terrain Streaming preset index.

### Return value

Landscape Terrain Streaming preset name.
## string GetWaterGeometryPresetName ( int num )

Returns the Global Water Geometry preset name by given index.
### Arguments

- *int* **num** - Global Water Geometry preset index.

### Return value

Global Water Geometry preset name.
## bool IsViewportModeStereo ( Render.VIEWPORT_MODE mode )

Returns a value indicating if the specified mode is one of the stereo rendering modes.
### Arguments

- *[Render.VIEWPORT_MODE](../../../api/library/rendering/class.render_cs.md#VIEWPORT_MODE)* **mode** - Viewport mode to be checked. One of the [VIEWPORT_MODE_*](#VIEWPORT_MODE_DEFAULT) values.

### Return value

true if the specified mode is one of the stereo rendering modes; otherwise false.
## bool IsViewportModePanorama ( Render.VIEWPORT_MODE mode )

Returns a value indicating if the specified mode is one of the panorama rendering modes.
### Arguments

- *[Render.VIEWPORT_MODE](../../../api/library/rendering/class.render_cs.md#VIEWPORT_MODE)* **mode** - Viewport mode to be checked. One of the [VIEWPORT_MODE_*](#VIEWPORT_MODE_DEFAULT) values.

### Return value

true if the specified mode is one of the panorama rendering modes; otherwise false.
## void ClearDebugMaterials ( )

Clears all global [debug materials](../../../content/materials/library/debug/index.md).
## void SetDebugMaterial ( int num , Material material )

Replaces the [debug material](../../../content/materials/library/debug/index.md) with the specified number with the new debug material specified. The number of material determines the order in which the expressions assigned to it are executed.
### Arguments

- *int* **num** - Debug material number in the range from 0 to the [total number of debug materials](#getNumDebugMaterials_int).
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - New debug material to replace the one with the specified number.

## Material GetDebugMaterial ( int num )

Returns a [debug material](../../../content/materials/library/debug/index.md) applied globally by its number.
### Arguments

- *int* **num** - Debug material number in the range from 0 to the [total number of debug materials](#getNumDebugMaterials_int).

### Return value

Debug material applied globally with the specified number.
## void InsertDebugMaterial ( int num , Material material )

Inserts a new global [debug material](../../../content/materials/library/debug/index.md) to the list of globally applied debug materials.
### Arguments

- *int* **num** - Position at which a new debug material is to be inserted.
- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Debug material to be inserted into the list of globally applied debug materials.

## int FindDebugMaterial ( Material material )

Returns the number of the specified [debug material](../../../content/materials/library/debug/index.md) applied globally. This number determines the order in which the assigned expressions are executed.
### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Debug material for which a number is to be found.

### Return value

Debug material number in the range from 0 to the [total number of debug materials](#getNumDebugMaterials_int), or -1 if the specified material was not found.
## void AddDebugMaterial ( Material material )

Adds a new global [debug material](../../../content/materials/library/debug/index.md).
### Arguments

- *[Material](../../../api/library/rendering/class.material_cs.md)* **material** - Debug material to be applied globally.

## void RemoveDebugMaterial ( int num )

Removes the global [debug material](../../../content/materials/library/debug/index.md) with the specified number.
### Arguments

- *int* **num** - Debug material number in the range from 0 to the [total number of debug materials](#getNumDebugMaterials_int).

## void SwapDebugMaterials ( int num_0 , int num_1 )

Swaps two [debug materials](../../../content/materials/library/debug/index.md) with specified numbers. The number of material determines the order in which the expressions assigned to it are executed.
### Arguments

- *int* **num_0** - Number of the first debug material in the range from 0 to the [total number of debug materials](#getNumDebugMaterials_int).
- *int* **num_1** - Number of the second debug material in the range from 0 to the [total number of debug materials](#getNumDebugMaterials_int).

## void SetDebugMaterialEnabled ( int num , bool enabled )

Enables or disables the [debug material](../../../content/materials/library/debug/index.md) with the specified number. When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **num** - Debug material number in the range from 0 to the [total number of debug materials](#getNumDebugMaterials_int).
- *bool* **enabled** - 1 to enable the debug material with the specified number, 0 to disable it.

## bool GetDebugMaterialEnabled ( int num )

Returns a value indicating if the [debug material](../../../content/materials/library/debug/index.md) with the specified number is enabled (active). When a material is disabled (inactive), the scripts attached to it are not executed.
### Arguments

- *int* **num** - Debug material number in the range from 0 to the [total number of debug materials](#getNumDebugMaterials_int).

### Return value

1 if the debug material with the specified number is enabled; otherwise, 0.
## Texture GetCacheTexture ( UGUID guid , bool forced = false )

Returns the texture cache by the texture GUID.
### Arguments

- *[UGUID](../../../api/library/filesystem/class.uguid_cs.md)* **guid** - Texture GUID.
- *bool* **forced**

### Return value

Texture cache.
## void ReloadResource ( string path )

Instantaneously reloads the resource (texture, node, geometry - MeshStatic/MeshSkinned) by GUID.
### Arguments

- *string* **path** - Path to the resource to be reloaded.

## void ReloadResource ( string[] pathes )

Instantaneously reloads the resources (texture, node, geometry - MeshStatic/MeshSkinned) by GUID.
### Arguments

- *string[]* **pathes** - A set of paths to the resources to be reloaded.
