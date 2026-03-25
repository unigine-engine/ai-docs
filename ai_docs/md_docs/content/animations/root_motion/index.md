# Root Motion


Root motion is a technique where character movement is driven by the animation itself rather than by game code. The animator controls the exact distance and timing of every step, dodge, or attack - the application just applies the result to the character's position.

   Sorry, your browser does not support embedded videos.
*Left: root motion disabled, the character runs forward and snaps back to the origin on each loop. Right: root motion enabled, the movement is extracted into a delta, and the character stays in place waiting to be moved by application code*


This is useful for combat attacks, climbing, vaulting, cinematic sequences, and any locomotion where precise animation-driven positioning matters.


## Enabling Root Motion in the Graph


Root motion is a **graph-level setting**. To enable it:


1. Open the animation graph (`*.agraph`) in the [Animation Graph Editor](../../../content/animations/graph/index.md). ![](root_motion_setting.png)
2. In the graph settings, enable the *Root Motion* checkbox:

  - **Disabled** (default) - the animation plays as authored: the root bone moves and the skeleton travels through space. The scene node position does not change. When the clip loops, the skeleton jumps back to the node origin. Use this when you do not need root motion data at all (ambient NPCs, menu characters, cosmetic animations).
  - **Enabled** - each frame, the system extracts the root bone's displacement and rotation, removing them from the skeleton pose (so the character stays in place). The extracted movement is returned as a **root motion delta** - a per-frame offset (position + rotation) available via *[getRootMotionDelta()](../../../api/library/animations/skeletal/class.animscript_cpp.md#getRootMotionDelta_Transform)*. Your application code decides whether to apply this delta to the scene node or ignore it. This allows mixing animation-driven movement (attacks, dodges, cinematics) with code-driven movement (locomotion) within the same graph.


> **Notice:** In the preview viewport, the character moves according to the root motion data. Toggle *Fix Root Bone in Origin* to keep the character centered while inspecting the animation.


## Preparing Animation


### Creating Root Motion Joint


Root motion requires a dedicated root bone that moves through space. If your source file does not have one, you can create it during import:


1. In the import settings, enable [*Create Root Motion Joint*](../../../editor2/fbx/index.md#options_root_motion_joint).
2. Set the *Target Root Motion Joint* to specify which existing joint should become the source of root motion data.
3. Configure which motion components to extract from the target joint into the new root:

  - **Position Component** (All, XY, XZ, YZ, X, Y, Z, None) - which translation axes to move into the root motion joint. For a running character, XZ extracts forward/sideways locomotion while leaving vertical bounce on the original joint.
  - **Rotation Component** - which rotation to move into the root motion joint:

    - All - full rotation is extracted.
    - Only Vertical Axis - extracts turning (yaw) while leaving body tilts on the original joint.
    - None - no rotation is extracted.


This creates a new ***root_motion_joint*** that becomes the parent of all existing root joints. The selected components are moved into it; everything else stays on the original joint.


> **Notice:** In-place animations (where the root bone stays at the origin) do not produce root motion deltas.


### Root Motion Present


Each animation clip has a *Root Motion Present* checkbox in its common settings. Enable it to mark the clip as containing root motion data. Only clips with this flag enabled will produce root motion deltas during playback.


![](root_motion_present.png)


This setting is stored as part of the animation asset and survives reimport.


## Root Motion and Blending


When multiple animations are blended, the resulting movement is interpolated with the same weights as the poses. For example, blending a slow walk and a fast run at 50/50 produces movement at a speed halfway between the two. Animations applied via **[Apply Additive](../../../content/animations/graph/node_library/blend/apply_additive.md)** do not contribute root motion.


> **Notice:** If a [blend mask](../../../content/animations/blend_masks/index.md) assigns zero influence to the root bone, root motion from that input is ignored. Make sure the root bone has non-zero mask weight for inputs that should contribute root motion.


## Accessing Root Motion from Code


Application code reads the root motion delta each frame and applies it to the character. The following methods are available on the animation graph object:


| *[isActiveRootMotion](../../../api/library/animations/skeletal/class.animscript_cpp.md#isActiveRootMotion_int)* | Returns whether root motion is enabled and producing deltas. |
|---|---|
| *[getRootMotionDelta](../../../api/library/animations/skeletal/class.animscript_cpp.md#getRootMotionDelta_Transform)* | Returns the root motion delta for the current frame as a Transform (position and rotation). |


> **Notice:** The delta is in the character's local space.


## See Also


- C++ Sample:
- [Animation Graph Editor](../../../content/animations/graph/index.md)
- [Node Library](../../../content/animations/graph/node_library/index.md)
- [State Machines](../../../content/animations/state_machines/index.md)
- [Animation Synchronization](../../../content/animations/synchronization/index.md)
