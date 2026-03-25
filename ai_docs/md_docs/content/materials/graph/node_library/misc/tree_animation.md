# Tree Animation Node


![](../img/tree_animation.png)

### Description

This node simulates dynamic wind-based bending animation for tree models by deforming vertex positions in tangent space. Vertex color channels are used to define areas of the mesh (trunk, branches, leaves) and assign them specific animation behavior.


You can find usage examples for this node in the *[Vegetation -> Tree Animation Sample](../../../../../content/samples/main_samples/vegetation.md)* material graph sample.


## Usage Example

| [**View Fullscreen**](https://matgraph.unigine.com/SampleTreeAnimation_2.21/fullView) |
|---|

#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **Stem Speed** | Controls the oscillation frequency of the trunk. Higher values simulate stronger or more turbulent wind by increasing swaying speed. |
| ![](../img/types/float.png) | **Stem Wind Offset** | Adds a phase offset to the trunk animation to create variation between instances of the same tree. |
| ![](../img/types/float.png) | **Branches Speed** | Controls the swaying speed of branches relative to the trunk. Higher values simulate lighter, more flexible branches reacting to wind. |
| ![](../img/types/float.png) | **Branches Offset** | Applies a phase offset to the animation of branches, introducing variation in their motion timing relative to the trunk. |
| ![](../img/types/float.png) | **Leaves Tiling** | Controls how densely the leaf animation is tiled across the mesh. Higher values create more detailed, repetitive motion. |
| ![](../img/types/float.png) | **Leaves Speed** | Controls the speed of leaf fluttering. Higher values simulate lighter leaves in strong wind. |
| ![](../img/types/float.png) | **Leaves Offset** | Introduces variation to the timing and direction of leaf motion. This avoids uniform fluttering and adds a more organic, chaotic feel to the canopy, as if individual leaves are responding to subtle air currents. |
| ![](../img/types/float2.png) | **Wind Direction** | A 2D vector (X, Y) defining wind direction in world space. Used to orient the animation according to wind flow. |
| ![](../img/types/float.png) | **Object Height** | A multiplier based on tree height. Taller trees sway more noticeably under wind influence. |
| ![](../img/types/float.png) | **Stem Time Offset (Sec)** | Delays the trunk animation start (in seconds), helping desynchronize tree instances. |
| ![](../img/types/float.png) | **Branches Time Offset (Sec)** | Offsets the branch animation relative to the trunk's animation. This timing offset simulates the natural lag between trunk movement and how branches react to it. |
| ![](../img/types/float3.png) | **Vertex Offset Tangent Space** | Final vertex offset in tangent space, used to deform the mesh based on wind animation. |
