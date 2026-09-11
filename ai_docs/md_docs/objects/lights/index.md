# Light Sources


While the 3D geometry defines the shape of your content, **lighting** is the basis of every virtual scene defining colors and final look of your objects. *UNIGINE* features the following types of the light sources:


- **Dynamic** lighting is a customizable solution providing real-time lighting calculation. This advanced technique provides very realistic lighting as it can illuminate dynamic objects. Light sources themselves can be moved or changed in real time (for example, turned on and off). As the most objects in the scene are rendered in the deferred pass, dynamic light sources won't cause big performance losses.
- **Static** (precomputed) lighting is an efficient and useful solution for lighting relatively static scenes. It allows dropping most lighting computations, leaving only simple texture lookups to be performed at the rendering time. Still, this method only roughly simulates lighting for moving objects entering the scene and sometimes lacks physical accuracy registered by the eye.


| Light Source | Image | Dynamic Mode | Static Mode |
|---|---|---|---|
| *[LightOmni](../../objects/lights/omni/index.md)* (omnidirectional point light) | [![](light_omni_sm.png)](light_omni.jpg) | Emits light from a point source in all directions. | Emits light from a point source in all directions and uses a prebaked shadow cubemap for static objects lit by *Omni Light*. |
| *[LightProj](../../objects/lights/proj/index.md)* (projected light) | [![](light_proj_sm.png)](light_proj.jpg) | Emits light from a single point forming a focused beam aimed in a specific direction. | Emits light from a single point forming a focused beam aimed in a specific direction and uses a prebaked 2D depth texture to store shadows of static objects lit by *Projected Light*. |
| *[LightWorld](../../objects/lights/world/index.md)* (sun light) | [![](light_world_sm.png)](light_world.jpg) | Casts parallel beams onto the scene from an infinitely remote point. | � |
| *[LightEnvironmentProbe](../../objects/lights/envprobe/index.md)* (Environment Probe) | [![](envprobe_sm.png)](envprobe.jpg) | Grabs a cubemap each frame thus providing objects in the scene with dynamic reflections from a point source in all directions. | Uses a prebaked cubemap to provide objects in the scene with reflections from a point source in all directions. |
| *[LightVoxelProbe](../../objects/lights/voxelprobe/index.md)* (Voxel Probe) | [![](voxelprobe_sm.png)](voxelprobe.png) | � | Provides volume to bake lighting. Uses a prebaked voxel map to provide objects in the scene with indirect lighting from any light source. |
| *[LightPlanarProbe](../../objects/lights/planar/index.md)* (Planar Reflection Probe) | [![](planarprobe_sm.png)](planarprobe.png) | Сaptures and projects a reflection relative to the camera onto a surface like a mirror. Uses a temporary texture created every frame. | � |


## Usage of Light Sources


The basic workflow is to use dynamic light sources and *Voxel Probe* for lighting, and *Environment Probe* for reflections. This approach ensures the best result, however, you can also enable both [lighting](../../objects/lights/envprobe/index.md#indirect_diffuse) and [reflections](../../objects/lights/voxelprobe/index.md#reflections_parameters) for *Voxel* or *Environment Probe* via the corresponding options.


![](probes.gif)


Light sources provide lighting to surfaces in the following priority:


1. ***Omni, Projected* and *World* light sources'** dynamic direct light.
2. **Voxel probe**'s [ambient light](../../objects/lights/voxelprobe/index.md#ambient_parameters) and/or [reflection](../../objects/lights/voxelprobe/index.md#reflections_parameters).
3. **Environment probe**'s [ambient light](../../objects/lights/envprobe/index.md#indirect_diffuse) and/or [reflection](../../objects/lights/envprobe/index.md#indirect_specular).


### See Also


- The [Light Sources Parameters](../../objects/lights/parameters/index.md) article
- The [Lighting](../../editor2/lighting/index.md) section containing information on all available types of light objects and light-related tools
- The article about [Bake Lighting Tool](../../editor2/lighting/gi/bake_lighting/index.md)
- The [Lights Optimization](../../content/optimization/lights/index.md) article
- [Video Tutorial: Lighting](../../videotutorials/essentials/lights.md)
- [Video Tutorial: Global Illumination](../../videotutorials/essentials/global_illumination.md)
