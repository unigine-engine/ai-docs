# Subpixel Reconstruction Anti-Aliasing (SRAA)


**Subpixel Reconstruction Anti-Aliasing (SRAA)** is an additional anti-aliasing technique that restores small image details. It also provides a net speedup and minimal overhead compared to supersampling. It is recommended to combine this technique with [TAA](../../../principles/render/antialiasing/taa.md) for better anti-aliasing quality.


![](comparison.gif)


## How SRAA works


SRAA is used in deferred rendering to achieve high-quality anti-aliasing by sampling geometry at higher resolution than shading, since shading usually changes more slowly than geometry.


There are two stages in SRAA:


1. **Depth prepass multisampling** generates depth position information at subpixel resolution. Subpixels are subdivision cells of a pixel. Depth prepass samples the geometry in the screen-space and stores samples� position information in a G-buffer. ![](diagram_1.png)
2. **Reconstruction pass** uses the custom *filter* after the deferred shading to refine the shading results and output a screen-resolution, antialiased frame. In the picture below you can see how the SRAA reconstructs one *subpixel*. ![](diagram_2.png) At each geometric sample, all shaded neighbors in a fixed radius are considered and their values are interpolated using our custom filter with weights to restore subpixel details. A neighboring sample with significantly different depth is considered to be across a geometric edge (blue line), and receives a low weight. The filter weights estimate distance between source and target samples by comparing their *depth* values.


UNIGINE's implementation of SRAA uses a depth *threshold* method to identify areas of the frame with edges. This way we eliminate the blur problem that comes from applying a smoothing filter to areas with no depth variation. Despite the fact that this approach uses only depth it keeps acceptable quality and represents a good trade-off for the sake of performance.


Pros and Cons of SRAA:
 �����**+** Subpixel details and geometry reconstruction.
 �����**-** Costs performance.


![](TAA only.png) ![](TAA + SRAA.png)


## SRAA Adjustment


*Subpixel Reconstruction Anti-Aliasing (SRAA)* settings are available for adjustment via the *Render -> Antialiasing* section of the *Settings* window, along with [Fast approXimate Anti-Aliasing (FXAA)](../../../principles/render/antialiasing/fxaa.md), [Temporal Anti-Aliasing (TAA)](../../../principles/render/antialiasing/taa.md) and [Supersampling](../../../principles/render/antialiasing/supersampling.md) settings. The following settings are available when the [Custom](../../../principles/render/antialiasing/index.md#aa_custom) preset for Anti-Aliasing is selected.


![SRAA Settings](sraa.png)

*Anti-Aliasing Settings*


### SRAA Settings


| SRAA | The value indicating if [Subpixel Reconstruction Anti-Aliasing (SRAA)](../../../principles/render/antialiasing/sraa.md) is enabled. **disabled** by default. `Console access:render_sraa` ([API control](../../../api/library/rendering/class.render_cpp.md#render_sraa)) |
|---|---|
| Samples | The number of depth geometry samples per pixel. This value may significantly affect performance, so keep it low when the image quality differences are not apparent. One of the following values: - 2 - 4 (by default) - 8 `Console access:render_sraa_samples` ([API control](../../../api/library/rendering/class.render_cpp.md#render_sraa_samples)) |
| Depth Threshold | The depth threshold value used for edges detection that specifies the area for the SRAA processing. Turn on the debug mode and adjust this parameter in such a way that covers the required edges but at the same time leaves out the unnecessary geometry in the scene. Range of values: **[0.0f, inf]**. The default value is : **0.1f**. `Console access:render_sraa_depth_threshold` ([API control](../../../api/library/rendering/class.render_cpp.md#render_sraa_depth_threshold)) |
| Show Debug | The value indicating if the SRAA debug mode is enabled. This mode shows the geometry edges smoothed by the SRAA. **disabled** by default. `Console access:render_sraa_debug` ([API control](../../../api/library/rendering/class.render_cpp.md#render_sraa_debug)) ![](debug.png) |
| Use TAA | The value indicating if TAA integration is enabled. SRAA will use the shading sample from the previously rendered frame (TAA) to achieve correct anti-aliasing. Uses camera jittering, so it works only when the TAA is enabled. It is recommended to use this option by default. **enabled** by default. `Console access:render_sraa_temporal` ([API control](../../../api/library/rendering/class.render_cpp.md#render_sraa_temporal)) |


### Known Limitations


The SRAA method does not work with transparent objects in the background because the reconstruction phase restores details after the deferred shading, while the transparent objects are rendered later in forward shading pass.


Nevertheless, the UNIGINE supports SRAA with the following objects on screen: water and clouds (the `render_clouds_transparent_order` console command must be set to **0** for the clouds rendering).
