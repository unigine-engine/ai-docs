# Blend Masks


A blend mask controls how a **[Blend Poses](../../../content/animations/graph/node_library/blend/blend_poses.md)** node blends animations on a per-joint basis. Without a blend mask, all joints blend with the same weight. With a blend mask, each joint has its own influence value (0.0 to 1.0) that scales the blend weight for that joint individually.


Blend masks enable partial blending - for example, blending an upper-body aiming animation only on the spine, arms, and head, while the legs remain fully controlled by the locomotion animation.

   Sorry, your browser does not support embedded videos.
*A state machine drives three locomotion animations (idle, walk, run). A blend mask lets the waving animation play on the upper body without affecting the legs, so the character keeps moving normally.*


## How Blend Masks Work


When a blend mask is applied to a **Blend Poses** node, the final blend weight for each joint is calculated as:


Final Weight = Weight × Influence


Where:


- **Weight** is the blend weight input on the **Blend Poses** node (a single value for the whole blend).
- **Influence** is the per-joint value from the blend mask (0.0 to 1.0).


For example, if the **Weight** input is 0.8 and a joint's blend mask influence is 0.5, that joint blends at 0.4 (0.8 x 0.5). Joints with influence 0.0 are not blended at all - they pass through from pose **A** unchanged. Joints with influence 1.0 blend at the full **Weight** value.


The blend mask applies to all joints, including the root bone. If [root motion](../../../content/animations/root_motion/index.md) is enabled, the root bone's influence value affects how root motion is blended - setting it to 0.0 means root motion comes entirely from pose **A**.


## Creating a Blend Mask


Blend masks are created and stored on the skeleton asset. Each skeleton can have multiple named blend masks.


### In the Skeleton Editor


To create a blend mask:


1. Select a skeleton asset in the *Asset Browser*.
2. In the *Blend Masks* section, click *+* to add a new mask.
3. Enter a name for the mask (e.g., UpperBody, LeftArm).
4. For each joint in the skeleton hierarchy, set the influence value from 0.0 (not affected) to 1.0 (fully affected).


| ![](blend_masks_option.png) | ![](upper_body_example.png) |
|---|---|


The joint hierarchy is displayed as a tree. Set high influence values on joints you want to be affected by the blend, and low or zero values on joints you want to pass through unchanged.


You can use intermediate values for smooth transitions between body regions - for example, setting the lower spine to 0.3 and upper spine to 0.7 creates a gradual falloff instead of a hard cut.


## Using a Blend Mask in the Animation Graph


Select a **[Blend Poses](../../../content/animations/graph/node_library/blend/blend_poses.md)** node and choose the blend mask from the *Blend Mask* dropdown in the *Selected Item* panel. The dropdown lists all blend masks defined on the skeleton that is assigned to the graph.


![](choosing_blend_mask.png)


Once a mask is selected, poses are blended using the per-joint influence values defined in that mask.


## See Also


- [Blend Poses](../../../content/animations/graph/node_library/blend/blend_poses.md)
- [Animation Graph Overview](../../../content/animations/index.md)
