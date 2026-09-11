# Dynamic Resolution Scale


> **Notice:** Currently available for DirectX 12 only.
>
>
> Available for both desktop and VR modes.


Dynamic Resolution Scaling (DRS) is a rendering technique that automatically adjusts the **internal rendering resolution** at runtime to maintain stable performance. It monitors rendering performance and depending on the current GPU workload changes the internal resolution to reduce GPU load in demanding scenes while keeping the final output resolution unchanged. This decreases the number of pixels the GPU has to process and helps recover performance.


**How it works:** DRS traces GPU frame time and compares it against the [target FPS](../../../code/console/index.md#render_dynamic_resolution_target_fps). If the frame time exceeds the target threshold for the [specified number of consecutive frames](../../../code/console/index.md#render_dynamic_resolution_down_frames), DRS decreases the internal rendering resolution. When GPU resources become available again (the scene becomes less demanding) for the [specified number of consecutive frames](../../../code/console/index.md#render_dynamic_resolution_up_frames), DRS increases the rendering resolution again to improve visual quality.


## Rendering Resolution vs Output Resolution


Dynamic Resolution Scaling changes the **internal** rendering resolution, **not the final** display resolution.


The output resolution remains the same, while the scene may be rendered at a lower or higher internal resolution before being scaled to the final image size.


Example:


![](example.jpg)


This means that the user interface, final frame size, and display resolution remain unchanged, while the rendering workload is adjusted dynamically in the background.


## Image Quality Considerations


Lowering the internal rendering resolution reduces GPU workload, but it may also affect image quality. Depending on the scale factor and the scene content, the image may become softer or less detailed.


The goal of DRS is to find a balance between performance and visual quality. Small resolution changes are often difficult to notice during motion, while large drops may become visible, especially on thin geometry, detailed textures, text, or distant objects.


For best results, DRS is usually configured with [minimum](../../../code/console/index.md#render_dynamic_resolution_scale_min) and [maximum resolution limits](../../../code/console/index.md#render_dynamic_resolution_scale_max). These limits define how far the rendering resolution is allowed to decrease or increase.


## DRS and Upscaling Technologies


Dynamic Resolution Scaling can also be used together with upscaling technologies. In this case, the scene is rendered at a variable internal resolution and then reconstructed or upscaled to the final output resolution.


[**FSR**](../../../principles/render/upscaling/index.md#fsr2_use) does not impose any additional limitations on dynamic resolution scaling.


When [**DLSS**](../../../principles/render/upscaling/index.md#dlss_use) is used, the rendering resolution range is determined by the selected DLSS mode. For example, DLAA renders at native resolution and therefore does not allow the rendering resolution to be changed dynamically.


## Recommended Usage


Use Dynamic Resolution Scaling when stable performance is more important than keeping the rendering resolution fixed at all times. It is especially useful for real-time applications where temporary frame drops are more noticeable than small changes in sharpness.


When configuring DRS, consider the following:


- Set a reasonable target frame rate.
- Define minimum and maximum resolution limits.
- Avoid setting the minimum resolution too low, as this may noticeably reduce image quality.
- Test DRS in scenes with different GPU workloads.
- Check the behavior together with the selected upscaling mode.
- Remember that DLSS modes may limit the resolution range available to DRS.
