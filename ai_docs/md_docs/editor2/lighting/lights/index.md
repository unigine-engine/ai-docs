# Light Sources


This section covers types of dynamic light sources and lights-related concepts.


## Light Sources


To create a light source, open the Menu bar and click *Create -> Lights*.


![](create.png)


Light sources provide direct real-time lighting which is used for shading on the **[Deferred](../../../principles/render/sequence/index.md#lights)** and **[Forward](../../../principles/render/sequence/index.md#transparent)** passes of the Rendering Sequence.


The light's **[Mode](../../../objects/lights/parameters/index.md#light_mode)** defines the impact of the light source on the [light baking](../../../editor2/lighting/gi/index.md#static_gi) process and affects rendering of shadows from it:


- **Dynamic** light sources provide direct real-time lighting only and are turned off while light baking is being calculated. Such light sources provide dynamic shadows only.
- **Static** lights sources contribute to baking of indirect lighting and remain enabled all the time providing direct real-time lighting. When baked, such light sources are not to be moved; otherwise, this option can cause lack of physical accuracy registered by the eye. Static light sources are able to provide both cached and mixed shadows.


### World Light


![](../../../objects/lights/world/world_light_index.png)


The **[World Light](../../../objects/lights/world/index.md)** is an infinitely remote light source casting orthographically projected beams onto the scene. The shadows cast by this light are parallel, which provides a realistic simulation of the light of celestial bodies, such as the Sun and the Moon.


The World Light takes part in the [Scattering](../../../editor2/lighting/environment.md#scattering) simulation.


### Omni Light


![](../../../objects/lights/omni/index.png)


The **[Omni Light](../../../objects/lights/omni/index.md)** is a point source emitting light in all directions and realistically reproducing shadow cast. This type of light serves to simulate light sources with bright center and equal roll-off of intensity. Omni Light proves useful for general lighting purposes in indoor scenes because of its nondirectional qualities.


### Projected Light


![](../../../content/optimization/lights/proj_light.png)


The **[Projected Light](../../../objects/lights/proj/index.md)** source casts light from a single point forming a focused beam aimed in a specific direction. This type of light is visualized in a form of a pyramid. Due to its form, it is versatile and can be conveniently used to simulate the numerous light emitting sources: for example, car headlights, flash light, or street lamps.


## Area Lights


![](area.gif)


By default, light sources are represented by a point that emits lighting. Both [Omni](#omni) and [Projected](#proj) light sources have the **[Shape settings](../../../objects/lights/parameters/index.md#shape_settings)** intended to define the shape of an area light source. Area light sources provide wider light spots and correct specular highlights on geometry.


The following shapes are available:


- Sphere
- Capsule
- Rectangle


> **Notice:** Soft shadows from area lights are simulated by using the [Penumbra](../../../editor2/lighting/lights/shadows.md#area) settings.


## Emissive Objects


![](emissive.png)


The *[mesh_base](../../../content/materials/library/mesh_base/index.md#option_emission)*, [decal_base](../../../content/materials/library/decal_base/index.md#option_emission) and [particles_base](../../../content/materials/library/particles_base/index.md#parameters_emission) materials support the **Emission** feature, allowing any geometry to appear as a bright surface. However, it does not illuminate the environment, only the glow effect is rendered by default. Lighting from an emissive object can be [baked](../../../editor2/lighting/gi/bake_lighting/index.md) into GI and computed in real time by using [Screen-Space GI](../../../editor2/settings/render_settings/global_illumination/index.md).


## See Also


- The [Light Sources](../../../objects/lights/index.md) section.
- The [Lights Optimization](../../../content/optimization/lights/index.md) article.
- [Video Tutorial: Lighting](../../../videotutorials/essentials/lights.md).
