# Animation


UNIGINE provides two separate animation systems serving different purposes.


## Skeletal Animation


**Skeletal Animation** deforms skinned meshes through a skeleton (joint hierarchy). The system separates mesh rendering from animation control:


- [Skinned Mesh](../../objects/objects/mesh_skinned/index.md) - renders the deformable mesh.
- [Skeleton Pose](../../objects/animations/nodeskeletonpose/index.md) - computes the animated pose and applies it to one or more *Skinned Mesh* objects.


The *Skeleton Pose* node supports two modes:


- **Animation Layers** - manual control over blending layers via API.
- **Animation Graph** - animation logic is driven by a visual graph with state machines, blend spaces, and transitions. This is the primary way to build complex character animation.


A typical character setup:


1. A [Skeleton Pose](../../objects/animations/nodeskeletonpose/index.md) node is added to the scene with a `.skeleton` file assigned.
2. One or more [Skinned Mesh](../../objects/objects/mesh_skinned/index.md) objects are placed as children of the *Skeleton Pose* node (or added to its controlled objects list).
3. An animation graph is assigned to drive the animation logic.


> **Notice:** For legacy projects, the [Skinned Mesh (Legacy)](../../objects/objects/mesh_skinned_legacy/index.md) provides a monolithic solution with a built-in animation player.


## Timeline Animation


**Timeline Animation** is a sequencer for animating arbitrary object properties (node transforms, material parameters, property values) over time using keyframed curves.


Timeline animations are stored in `.utrack` and `.uplay` files and played back via the [Animation Playback](../../objects/animations/animation_playback/index.md) node.
