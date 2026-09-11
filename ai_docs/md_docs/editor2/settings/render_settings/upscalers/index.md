# Upscalers


This section contains rendering settings of *[DLSS and FSR upscalers](../../../../principles/render/upscaling/index.md)*.


![](upscalers.png)

*Upscalers Section*


| Upscaling Mode | The Upscaling mode. Defines a technology to be used to render high-resolution images based on the lower resolution source, which may help preserve image quality while getting more fps. One of the following values: - *Disabled* for no upscaling. 1.0x per dimension, the final image has 100% rendered resolution. - *FSR* for Fidelity FX Super Resolution by AMD. - *DLSS* for Deep Learning Super Sampling by NVIDIA. (by default) `Console access:render_upscale_mode` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_upscale_mode)) |
|---|---|


Depending on the specifed *Upscaling Mode*, the set of the settings differs.


## DLSS Settings


![](dlss_settings.png)


> **Notice:** All default [DLSS](https://www.nvidia.com/en-gb/geforce/technologies/dlss/) settings provided are recommended by NVIDIA.


| DLSS Mode | The DLSS quality. - *Ultra Performance* provides the highest performance boost by rendering at ~33.3% of the target resolution and upscaling to the output resolution. This mode is recommended only for 8K output resolution due to the significant reduction in internal image quality. - *Max Performance* provides a higher performance boost than *Balanced* by rendering at ~50% of the target resolution. Use when frame-rate is prioritized but some internal detail should be preserved. It is recommended for users with 1440p/2K monitors, providing better performance with minimal effort. - *Balanced* offers both optimized performance and image quality by rendering at approximately ~58% of the target resolution. Recommended as the general-purpose preset for users who want a compromise between frame-rate and visual fidelity. - *Max Quality* offers higher image quality than *Balanced* by rendering at approximately ~66.7% of the target resolution. Prioritizes visual fidelity while still delivering a meaningful performance improvement over native rendering. - *DLAA* (**Deep Learning Anti-Aliasing**) is an AI-powered tool to eliminate jagged edges in video apps, by rendering at native (100%) resolution. It improves image quality with less performance cost than traditional anti-aliasing methods. Option **#4** is selected by default (see above). `Console access:render_upscale_dlss_mode` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_upscale_dlss_mode)) |
|---|---|
| DLSS Preset | The DLSS preset. - *A* - Legacy preset designed to mitigate ghosting artifacts, particularly in cases where input data (e.g., motion vectors) may be missing. **Intended modes:** Performance, Balanced, Quality - *B* - Variant of Preset A, optimized specifically for Ultra Performance mode. **Intended modes:** Ultra Performance - *C* - Prefers current-frame information, making it well-suited for fast-paced, high-motion content. **Intended modes:** Performance, Balanced, Quality - *D* - Functionally similar to Preset E but less commonly recommended. Preset E is preferred in most cases. **Intended modes:** Performance, Balanced, Quality - *E* - General-purpose preset prioritizing both performance and image stability. **Intended modes:** Performance, Balanced, Quality - *F* - Default preset for Ultra Performance and DLAA modes. Provides stable results across these configurations. **Intended modes:** Ultra Performance, DLAA - *G* is unused. Reverts to default preset behavior. - *H* is unused. Reverts to default preset behavior. - *I* is unused. Reverts to default preset behavior. - *J* - Transformer-based model similar to Preset K. May exhibit slightly less ghosting, but at the cost of additional flickering. Generally superseded by Preset K. **Intended modes:** DLAA, Performance, Balanced, Quality - *K* - Default transformer-based preset delivering the highest image quality. Reduces ghosting and shimmering compared to other presets, though at a higher performance cost. Recommended over Preset J. **Intended modes:** DLAA, Performance, Balanced, Quality Option **#1** is selected by default (see above). `Console access:render_upscale_dlss_preset` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_upscale_dlss_preset)) |


## FSR Settings


![](fsr2_settings.png)


> **Notice:** All default [FSR 3](https://gpuopen.com/fidelityfx-super-resolution-3/) settings provided are recommended by AMD.


| Mode | The quality mode of FSR (FidelityFX Super Resolution upsampling technique). - *Ultra Performance* that offers the highest performance gain while still retaining image quality close to native. Scale factor: 3.0x per dimension (≈33.3% of output resolution) - *Performance* that delivers a substantial performance boost with image quality similar to native rendering. Scale factor: 2.0x per dimension (≈50.0% of output resolution) - *Balanced* that balances performance gains and image quality effectively. Scale factor: 1.7x per dimension (≈58.8% of output resolution) - *Quality* that provides image quality equal to or better than native with a meaningful performance improvement. Scale factor: 1.5x per dimension (≈66.6% of output resolution) - *Native AA* that renders at native resolution (no upscaling, scale factor 1.0x) and applies FSR anti-aliasing only. - *Custom* that uses a custom resolution scale set via the [FSRCustomResolutionScale](#FSRCustomResolutionScale) property (range: 0.1 to 1.0). Option **#1** is selected by default (see above). `Console access:render_upscale_fsr_mode` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_upscale_fsr_mode)) |
|---|---|
| Upscale Sharpness | The sharpness value, where 0 is no additional sharpness and 1 is maximum additional sharpness. Range of values: **[0.0f, 1.0f]**. The default value is : **0.5f**. `Console access:render_upscale_fsr_sharpness` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_upscale_fsr_sharpness)) |
| Pre Exposure | The pre-exposure value by which we divide the input signal to get back to the original signal produced by the game before any packing into lower precision render targets. Range of values: **[0.0f, inf]**. The default value is : **1.0f**. `Console access:render_upscale_fsr_pre_exposure` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_upscale_fsr_pre_exposure)) |


> **Notice:** You can use the referenced commands to perform the same operations via the console.
