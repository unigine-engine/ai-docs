# Animation - Generic

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/csharp-component-samples](https://github.com/unigine-engine/csharp-component-samples)**.


## Animation Layers Playback

Animation playback uses animation layers.

The possibility to control every frame provides boundless opportunities in setting the animation playback.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/animation_generic/animation_layers_playback*
## Bones: Rotation

This sample demonstrates how to control animation playback and directly modify bone transforms.

The *AnimationRotation.cs* component plays skeletal animations using `.anim` files and programmatically applies additional transformations to specific bones. In this example, the shooting animation is blended with the idle animation, while the turret is rotated via code by modifying the transform of a specific joint.


Animations are assigned to separate layers using the *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)* class. Blending is performed between the idle animation and a dynamically selected shooting animation


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/animation_generic/bones_rotation*
## Curve Animation

This sample demonstrates how to animate both node transforms and material parameters using *[Curve2D](../../../api/library/common/class.curve2d_cpp.md)*. Separate *Curve2d* tracks control a node's position, rotation, and scale, evaluated each frame to build the final transformation matrix.


This setup is useful for creating looping motions and dynamic material effects without relying on external animation assets.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/animation_generic/curve_animation*
## Material Parameters Animation

The *Materials* sample illustrates how to change the following parameters of [materials](../../../api/library/rendering/class.material_cpp.md) at runtime:


- [Albedo color](../../../content/materials/library/mesh_base/index.md#parameter_albedo)
- [Albedo texture](../../../content/materials/library/mesh_base/index.md#texture_albedo)
- [Metalness](../../../content/materials/library/mesh_base/index.md#parameter_metalness)
- [Emission](../../../content/materials/library/mesh_base/index.md#option_emission) state
- [Cast World Shadow](../../../editor2/node_parameters/visual_representation/index.md#cast_world_shadows).


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/animation_generic/material_parameters_animation*
## Track Playback

![](../../../samples/img/csharp_component_samples_track_playback.jpg)

This sample demonstrates how to use *Tracker* to animate objects by changing their position, rotation, and scale through tracks created in the **[Tracker](../../../editor2/tools/tracker/index.md)** tool.


Tracks in code are referred to via names and IDs.


The **TrackPlayback** component uses a C# wrapper for *Tracker* functionality implemented in the **Tracker.cs** file.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/animation_generic/track_playback*
