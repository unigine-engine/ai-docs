# Glass Sample


This material graph sample demonstrates different implementations of glass materials for different needs.


![](result.jpg)

*Thick colored glass*


## Blended Reflective Material


| [**View Fullscreen**](https://matgraph.unigine.com/SampleGlassBlendModeAdd_2.21/fullView) |
|---|


The `glass_blend_mode_add` sample is a material providing [raymarched](../../../../../content/materials/graph/node_library/misc/reflection_raymarched.md) [fresnel](../../../../../content/materials/graph/node_library/misc/fresnel.md)-based reflection in the *Additive* blending mode that can be used as a reflective component in compound materials.


## Blended Refractive Material for Thick Glass


| [**View Fullscreen**](https://matgraph.unigine.com/SampleGlassBlendModeRefractionThick_2.21/fullView) |
|---|


The `glass_blend_mode_refraction_thick` sample implements [fresnel](../../../../../content/materials/graph/node_library/misc/fresnel.md)-based refraction for thick objects in the *Multiplicative* blending mode. It showcases the use of the **[Refraction Screen UV Offset For Thick Objects](../../../../../content/materials/graph/node_library/misc/refraction_screen_uv_offset_for_thick_objects.md)** node and can be used as a refractive component in compound materials.


## Blended Refractive Material for Thin Glass


| [**View Fullscreen**](https://matgraph.unigine.com/SampleGlassBlendModeRefractionThin_2.21/fullView) |
|---|


The `glass_blend_mode_refraction_thin` sample implements [fresnel](../../../../../content/materials/graph/node_library/misc/fresnel.md)-based refraction for thin objects in the *Multiplicative* blending mode. It showcases the use of the **[Refraction Screen UV Offset For Thin Objects](../../../../../content/materials/graph/node_library/misc/refraction_screen_uv_offset_for_thin_objects.md)** node and can be used as a refractive component in compound materials.


## High-Quality Thick Colored Glass


| [**View Fullscreen**](https://matgraph.unigine.com/SampleGlassThickColoredHighQuality_2.21/fullView) |
|---|


The `glass_thick_colored_high_quality` sample showcases an implementation of high-quality *raymarched* [reflection](../../../../../content/materials/graph/node_library/misc/reflection_raymarched.md) and [refraction](../../../../../content/materials/graph/node_library/misc/refraction_raymarched.md) for thick colored glass objects. The **[Fresnel](../../../../../content/materials/graph/node_library/misc/fresnel.md)** node defines the mutually exclusive intensities of each component.


## Low-Quality Thick Colored Glass


| [**View Fullscreen**](https://matgraph.unigine.com/SampleGlassThickColoredLowQuality_2.21/fullView) |
|---|


The `glass_thick_colored_low_quality` sample showcases an implementation of low-quality refraction for thick colored objects by means of the **[Refraction Simple For Thick Objects](../../../../../content/materials/graph/node_library/misc/refraction_simple_for_thick_objects.md)** node. The **[Fresnel](../../../../../content/materials/graph/node_library/misc/fresnel.md)** node defines the intensity of refraction.


## Thin Colored Glass


| [**View Fullscreen**](https://matgraph.unigine.com/SampleGlassThinColored_2.21/fullView) |
|---|


The `glass_thin_colored` sample showcases the use of the **[Refraction Simple For Thin Objects](../../../../../content/materials/graph/node_library/misc/refraction_simple_for_thin_objects.md)** and **[Reflection Raymarched](../../../../../content/materials/graph/node_library/misc/reflection_raymarched.md)** nodes for thin colored glass objects. The **[Fresnel](../../../../../content/materials/graph/node_library/misc/fresnel.md)** node defines the mutually exclusive intensities of each component.
