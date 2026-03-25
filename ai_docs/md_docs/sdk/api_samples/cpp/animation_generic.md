# Animation - Generic

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/cpp-api-samples](https://github.com/unigine-engine/cpp-api-samples)**.


## Animation Layers Playback

This sample demonstrates the use of animation layers to create and play object animations. The code shows how you can combine different animation tracks and play them simultaneously or sequentially.
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_generic/animation_layers_playback*

## Curve2D Animation

This sample demonstrates how to animate both node transforms and material parameters using *[Curve2D](../../../api/library/common/class.curve2d_cpp.md)*. Separate *Curve2d* tracks control a node's position, rotation, and scale, evaluated each frame to build the final transformation matrix.


This setup is useful for creating looping motions and dynamic material effects without relying on external animation assets.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_generic/curve2d_animation*
## Global Engine Parameters Animation

This sample demonstrates animating global Engine parameters using **singleton animation modifiers**. It shows real-time animation of physics gravity and render background color through dedicated animation tracks and playbacks.


Animation modifiers give you programmatic control over scene effects, weather changes, time transitions, and the animation of physical properties, resulting in more engaging and interactive scenes.


> **Notice:** All of the animation tracks, playbacks and objects are managed by the animation system and have the "Engine lifetime", i.e. they exist from the point they're loaded or created to when the Engine shutdowns, and therefore are preserved between different worlds.
>
>
> You have to stop active playbacks when switching to another world, if you don't want them continue playing there.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_generic/global_engine_parameters_animation*
## Material Parameters Animation

This sample demonstrates animating materials using **material animation objects**. It is useful for implementing dynamic changes in properties of materials in real time.

This is especially useful for scenes where object properties need to change based on user actions or world events, such as weather or time of day changes.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_generic/material_parameters_animation*
## Node Parameters Animation

This sample demonstrates animating nodes using **node animation objects**. It will be helpful for creating complex animation scenarios for stage objects in real time.

Node animations can serve as a foundation for various effects, including element appearance/disappearance, rotations, resizing, and more.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_generic/node_parameters_animation*
## Physics-Based Animation

This sample shows implementation of physics-based animation for the cat's movements in a simple game where a cat chases a laser pointer (different easing functions are used).
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_generic/physics_based_animation*

## Property Animation

This sample demonstrates animating property parameters using **property parameter animation objects**. Useful for implementing custom effects that depend on property parameters.
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_generic/property_animation*

## Tracker: Playback

Sample demonstrating how to use *Tracker* to animate objects (change their position, rotation, and scale) based on tracks created in the *Tracker* tool.

Tracker comes in handy for creating complex animation scripts.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_generic/tracker_playback*
## Widget Animation

This example shows how to animate widgets using **runtime animation objects**.

It demonstrates how to control and animate interface elements programmatically. Using dynamic animations helps create more lively, appealing user interfaces and enables automation of their behavior.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_generic/widget_animation*
