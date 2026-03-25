# Animation - Characters

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/csharp-component-samples](https://github.com/unigine-engine/csharp-component-samples)**.


## Additive Animation Blending

Additive blending of two animations.

Additive blending is a technique for combining skeletal model animations, enabling smooth transitions and the seamless merging of character or object movements.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/animation_characters/additive_animation_blending*
## Bones: Partial Blend

This sample demonstrates partial blending between two animations using bone-specific interpolation.

The *AnimationPartialInterpolation.cs* component plays two skeletal animations simultaneously on a skinned mesh and blends them only for selected bones. The blend weight can be adjusted at runtime using the keyboard.


Use the *interpolatedBones* array in the *Parameters* window to define which bones are affected by blending. The *[ObjectMeshSkinned](../../../api/library/objects/class.objectmeshskinned_cpp.md)* class is used to apply animation layers and interpolate transforms.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/animation_characters/bones_partial_blend*
## Linear Animation Blending

Linear interpolation of two animations.

Interpolating skeletal animations allows you to create smooth and natural transitions between different character or object movements.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/animation_characters/linear_animation_blending*
