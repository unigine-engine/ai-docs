# Fast approXimate Anti-Aliasing (FXAA)


*Fast approXimate Anti-Aliasing (FXAA)* is the cheapest and simplest smoothing algorithm. It is used in post-processing the final image (applied to the whole scene after it has been rendered), and it blurs groups of pixels having sharp changes in brightness. FXAA smooths edges in all pixels on the screen, including those inside alpha-blended textures and those resulting from pixel shader effects. It is straightforward, doesn't have any complex dependencies, and is fast.


The weak point of this technique is that it blurs not only the edges but important details of the textures as well. As a result, the overall contrast of the image deteriorates.


FXAA works well with static images only, but you can combine it with [TAA](../../../principles/render/antialiasing/taa.md) to provide a much better quality for dynamic scenes. FXAA provides anti-aliasing even at a zero intensity value, so this is a recommended setting to be used with TAA to improve image quality at practically no performance cost.


## FXAA Settings


FXAA settings are available for adjustment via the *Render -> Antialiasing* section of the *Settings* window, along with [TAA](../../../principles/render/antialiasing/taa.md), [SRAA](../../../principles/render/antialiasing/sraa.md), and [Supersampling](../../../principles/render/antialiasing/supersampling.md) settings. The following settings are available when the [Custom](../../../principles/render/antialiasing/index.md#aa_custom) preset for Anti-Aliasing is selected.


![FXAA Settings](fxaa.png)

*Anti-Aliasing Settings*


| FXAA | The value indicating if FXAA (post-process anti-aliasing) is enabled. **enabled** by default. `Console access:render_fxaa` ([API control](../../../api/library/rendering/class.render_cpp.md#render_fxaa)) |
|---|---|
| FXAA Intensity | The intensity of FXAA. Intensity specifies the sample offset of FXAA fragment. The higher the value, the more blurred image will be. Range of values: **[0.0f, 1.0f]**. The default value is : **0.0f**. `Console access:render_fxaa_intensity` ([API control](../../../api/library/rendering/class.render_cpp.md#render_fxaa_intensity)) |
