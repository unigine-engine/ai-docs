# Animation Player


![](../img/animation_player.png)

### Description

Plays an animation clip with looping and speed control. Connect an **[Animation Asset](../../../../../content/animations/graph/node_library/animation/animation_asset.md)** to the **Anim** input, and the node will output the resulting pose each frame. Each Animation Player maintains its own playback state (current time, play direction) independently.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/anim_asset.png) | **Anim** | The animation (`.anim`) to play. You can either connect an **[Animation Asset](../../../../../content/animations/graph/node_library/animation/animation_asset.md)** node or pick the animation directly via the inline asset picker on the node. |
| ![](../img/types/bool.png) | **Loop** | Whether to loop the animation. Default: true. |
| ![](../img/types/float.png) | **Speed** | Playback speed multiplier. Default: 1.0. |
| ![](../img/types/anim_pose.png) | **Pose** | The current animation pose. |


## Properties


The following properties control how different Animation Player nodes synchronize with each other. For details, see [Animation Synchronization](../../../../../content/animations/synchronization/index.md) article.


| Sync Group | Name of a synchronization group. Animation Players in the same group synchronize their playback (e.g., to keep footsteps aligned across walk and run animations). |
|---|---|
| Sync Role | Role in the sync group: Leader, Follower, or Weighted Leader. |
| Sync Method | How playback is synchronized: Normalized Time (all members share the same normalized position) or Marker Sync (synchronize by named markers placed in animation clips). |


## See Also


- [Animation Asset](../../../../../content/animations/graph/node_library/animation/animation_asset.md)
- [Animation Synchronization](../../../../../content/animations/synchronization/index.md)
