# Supersampling


**Supersampling** is a technique used to increase the effective resolution of a frame by rendering the scene larger than its final resolution, and then downsampling back with a filter. Sharp edges become anti-aliased as they are averaged from several pixels. This provides a much smoother anti-aliasing, but for a cost of performance. This is the most demanding anti-aliasing algorithm, but it offers the highest quality.


![](supersampling_off.jpg) ![](supersampling_on.jpg)


**Supersampling Ratio** defines the number of samples per pixel used for supersampling and is available for adjustment via the *Render -> Antialiasing* section of the *Settings* window, along with [TAA](../../../principles/render/antialiasing/taa.md), [SRAA](../../../principles/render/antialiasing/sraa.md), and [FXAA](../../../principles/render/antialiasing/fxaa.md) settings.


![TAA Settings](supersampling_settings.png)

*Antialiasing Settings*

  The number of samples per pixel used for [supersampling](../../../principles/render/antialiasing/supersampling.md).
Range of values: **[1e-6f, 8.0f]**. The default value is : **1.0f**.
`Console access:render_supersampling` ([API control](../../../api/library/rendering/class.render_cpp.md#render_supersampling))
The higher the value, the more reduced aliasing is (however, high values may produce visual artifacts and significantly affect performance).


> **Notice:** *Supersampling Ratio* сan be controlled by `render_supersampling` console command.


The resulting number of pixels after supersampling is calculated as follows:


**Number of Pixels** = ( **Width** x **supersampling_ratio** ) x ( **Height** x **supersampling_ratio** )


This gives us a quadratic dependence, which means that when you set supersampling ratio equal to **2** you'll have **x4** pixels (i.e. a **x4** FPS drop). Such ratio provides a significant reduction of artifacts inside the image � not only at boundaries but also in the textures.


A fractional value can also be set, e.g. **1.2** ratio instead of **2**. In this case the image will be rendered **1.2** times larger on each axis, so not every pixel will be averaged. This is a compromise option providing a little more reduced aliasing for a slight FPS drop.


The table below demonstrates how the supersampling ratio affects the number of pixels.


![](supersampling.png)


Supersampling can be used either for scenes with good performance or for rendering in a cinematic mode (video clips). In some cases to reduce rendering load when supersampling is enabled, you can use the [interleaved lights rendering mode](../../../principles/render/interleaved_rendering/index.md).
