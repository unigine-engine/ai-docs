# Animation - Characters

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/cpp-api-samples](https://github.com/unigine-engine/cpp-api-samples)**.


## Bones: Constraints

This sample demonstrates the use of bone rotation constraints and illustrates how they affect the operation of inverse kinematics.

This demonstrates how to create an IK chain for a character's bones, set a target position, and automatically control the bones' movement to produce realistic poses. A target is an object that updates dynamically according to the player's camera position.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_characters/bones_constraints*
## Bones: Foot Placement

This sample demonstrates a naive option for placing feet on a surface using IK chains.

Raycasting is applied to detect surface contact: in each frame, a ray is cast downward from the foot position to find intersections with the surface. The resulting contact point and surface normal are then used to adjust the foot bones' position and orientation, ensuring realistic foot placement.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_characters/bones_foot_placement*
## Bones: Inverse Kinematics

This sample demonstrates how to control bones using inverse kinematics


The pole vector is used as a constraint that defines the plane of joint bending.


The example is useful for creating animations where character bones are automatically positioned and oriented to achieve realistic movement.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_characters/bones_inverse_kinematics*
## Bones: Look At Chains

This sample demonstrates the use of LookAt chains for aiming at a target.


The chain contains the spine and head bones. By setting different weights for each bone you can adjust the targeting effect. The constraint is represented by a pole vector that defines a plane for the upward direction of each bone.


LookAt chains enable interactive control over the position and orientation of a character's eyes, head, shoulders, and other body parts. This is useful for animating the game environment in various situations.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_characters/bones_look_at_chains*
## Bones: Masks

This sample demonstrates how to use bone masks to selectively apply animation data.


Masks enable complex animation combinations. For example, you can preserve the original body movements while limiting head or arm animations to rotation, or scaling specific bones.


In this example, the right (child) model has a component that lists bones using a rotation-only mask from the left (adult) model's animation. The scale is masked out, so the listed bones keep their original size. If the mask is not applied, the bones appear stretched, as all transformations (including scale) are copied from the adult model. This can be seen on the child model's arms, where the mask is not used.


This method is excellent for multi-layered animations, allowing you to mix motions, add effects, or exclude certain parts of the model to achieve specific visual results or behaviors without duplicating full animation sets.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_characters/bones_masks*
## Bones: Retargeting

This sample demonstrates how the same animation can be used on skeletons with different proportions.


The pair on the left represents the use of animation without retargeting. On the right, the animatiotion is retargeted from the adult to the child. The bone length ratio between skeletons is taken into account for adjustment of the position component.


Retargeting is useful when you need to use the same animation source for different characters or objects with varying proportions but similar skeletal structures. This approach significantly speeds up the process of preparing animations.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_characters/bones_retargeting*
## Bones: Root Motion

This sample demonstrates the implementation of the root motion technique.


On the left there is a common looping animation. On the right, the offset of the root bone moves the object itself.


Root motion is particularly valuable for realistic character, vehicle, or object movements in games and simulations.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_characters/bones_root_motion*
## Bones: Sandbox

This sample provides the interface that allows visualizing and experiencing how to configure all available settings for IK chains, LookAt chains, and bone rotation constraints.
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_characters/bones_sandbox*

## Bones: State Machine

This sample demonstrates how to make an animated state machine based on ObjectMeshSkinned.

A state machine is a design pattern that manages various object states�such as idle, walking, or sneaking�and handles transitions between them. The example illustrates how to configure state machines with dynamic controls for walking, turning when idle, and running.


Implementing state machines enables the creation of complex, flexible character behaviors.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/animation_characters/bones_state_machine*
