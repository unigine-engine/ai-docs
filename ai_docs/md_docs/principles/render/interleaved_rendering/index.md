# Interleaved Lights Rendering


Rendering lights is one of the most consuming parts of the pipeline: the more light sources are used in your scene the heavier is their impact on performance. The situation gets worse if we have to render the scene in 4K+, as the number of UHD-capable devices grows, and higher rendering resolutions are becoming embraced more broadly.


Interleaved Rendering mode for lights may be helpful in this case. In this mode lighting is rendered during the deferred pass either interlaced (i.e. skipping each second row of pixels - 1/2 of all pixels), or in half resolution (1/4 of all pixels) with subsequent reconstruction of neighboring pixels using the data from previous frames, making it possible to reduce rendering load. The effect is cumulative and works best with [TAA](../../../principles/render/antialiasing/taa.md) enabled. We also recommend to use this mode when *Supersampling* is enabled to reduce rendering load, while keeping the image quality high.


This mode is recommended for relatively static scenes which contain a lot of light sources and do not have a lot of reflective surfaces (as reflections represent a weak spot of the interleaved reconstruction). Please note, that enabling interleaved lights rendering for a scene with a small number of light sources (e.g. a flight simulator scene with a single world light) may cause a performance drop.


> **Notice:** Interleaved Rendering mode requires a high framerate (**60+ FPS**), otherwise anti-aliasing quality reduces and ghosting effect becomes more pronounced.


As this effect is temporal, like TAA, it also requires a warm-up time since the beginning of the first frame and also suffers from the ghosting effect. Most of the artefacts appear when objects and the background are moving in opposite directions (e.g. rotating around the object in focus).


The **Color Clamping** can be used to reduce ghosting effect: *higher* values increase clamping intensity but may cause flickering on rippled reflective surfaces (as interleaved reconstruction is not so good at object's edges). When disabled, shadows and reflections have a lag as they are several frames behind.


You can enable interleaved rendering mode for lights and adjust its parameters via the *[Lights](../../../editor2/settings/render_settings/lights/index.md#interleaved_rendering_options)* section of the *Settings* window (*Window -> Settings -> Render -> Lights*).
