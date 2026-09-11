# Animation Synchronization


When blending between animations of different durations, cyclic events can drift out of phase, causing visual artifacts such as foot sliding. To prevent this, nodes can be grouped into **Sync Groups** that share a single timeline.


## Sync Groups


A **Sync Group** is a named collection of animation playback nodes that share a synchronized timeline. You assign nodes to a sync group by setting the *Sync Group* property to a non-empty string. All nodes with the same group name are automatically linked.


Each sync group maintains:


- A **shared playback** that all members follow.
- A **Leader** - the active member that advances the timeline each frame. The leader's **Speed** drives the playback rate for the entire group; individual speed settings of other members are ignored while synchronized.

  ![](without_sync_group.png)
*Without a sync group: each player advances its own timeline independently, causing animations to drift out of phase.*

  ![](with_sync_group.png)
*With a sync group: all members follow the leader's timeline, keeping animations in phase.*


A member is considered active when it participates in the current blend with a non-zero weight. Inactive members (zero weight) are excluded from leader election and do not receive synchronized time.


Two types of nodes can participate in sync groups:


- **[Animation Player](../../../content/animations/graph/node_library/animation/animation_player.md)** nodes
- **[Blend Space 2D Sync](../../../content/animations/graph/node_library/blend_space/blend_space_2d_sync.md)** nodes


## Sync Roles


Each member of a sync group has a role that determines its priority when choosing the leader. Priority order: Leader > Weighted Leader > Follower.


### Weighted Leader (Default)


The default role. The member with the highest blend weight automatically becomes the leader each frame; all others follow. During a crossfade, leadership transfers naturally as weights shift, so there are no jumps or pops.


### Leader


Always becomes the leader when active, regardless of blend weights. Takes priority over all Weighted Leader members. Use this when a specific animation must always control timing - for example, if one animation has been authored as the timing reference and others should follow it unconditionally.


> **Notice:** Only one member per sync group should have the Leader role. If multiple Leader members are active simultaneously, the first one found takes priority.


### Follower


Never becomes the leader as long as any Leader or Weighted Leader member is active. If only Follower members remain, the one with the highest blend weight leads. Use this for auxiliary animations that should always follow other members' timing, even if they have a high blend weight.


## Setting Up a Sync Group


To set up a sync group:


1. Select an **Animation Player** or **Blend Space 2D Sync** node in the graph.
2. In the *Selected Item* panel, set the *Sync Group* property to a group name (e.g., Locomotion).
3. Set the *Sync Role* to the desired role (Weighted Leader, Leader, or Follower).
4. Repeat for all other nodes that should be synchronized with the same group name.


The sync group name is a free-form string. Any nodes that share the same name are automatically grouped together at runtime. An empty group name means the node is not synchronized - it advances its own playback time independently based on its speed and looping settings.


## Sync Methods


Each sync group has a *Sync Method* property that determines how members synchronize their playback positions. All members of the same sync group should use the same method.


### Normalized Time (Default)


The default method. Each frame, the leader advances its playback time using its own speed and duration, then converts it to normalized time. All other members receive this normalized time and map it to their own durations - so a walk animation at 1.2 seconds and a run animation at 0.8 seconds both reach their midpoint at the same moment.


This method works well when all animations have matching phase - meaning corresponding events (such as foot contacts) occur at the same normalized time across all clips. For example, if both the walk and run clips have the left foot striking the ground at normalized time 0.25, they stay in sync naturally.


![](normalized_time_sync.png)

*Walk and run animations at the same normalized time (0.25). Both are in a matching phase - left foot forward, contacting the ground.*


However, if the animations have different phase relationships (the left foot lands at 0.25 in the walk but at 0.3 in the run), normalized time sync causes foot sliding during blends. In this case, use [Marker Sync](#marker_sync) instead.


### Marker Sync


An alternative synchronization method that uses named time markers placed in animation clips. Instead of mapping a single normalized time across all animations, the system matches markers by name and interpolates between corresponding marker positions. This produces accurate synchronization even when animations have different phase relationships or non-uniform timing.


Continuing the example above: the left foot lands at normalized time 0.25 in the walk but at 0.3 in the run. With marker sync, you place a **Left_Foot** marker at the correct time in each clip, and the system aligns them by name - regardless of their different positions.


![](marker_sync_segments.png)

*Markers divide each animation into segments. Corresponding segments are playedover the same real time, so key events (such as foot contacts) occur at the same moment across all members.*


Marker sync requires at least two markers with matching names across all animations in the sync group. Only markers whose names appear in every active member are used as synchronization anchors.


#### Adding Sync Markers


Sync markers must be added to every animation clip that participates in a marker-synced group. For each clip:


1. Select an animation asset (`.anim`) in the *Asset Browser*.
2. In the *Parameters* window, find the *Sync Markers* section.
3. Scrub the timeline to the desired frame (e.g., the moment the left foot contacts the ground).
4. Click *Add* to place a marker at the current time.
5. Enter a name for the marker (e.g., Left_Foot, Right_Foot).
6. Repeat for all important sync points in the animation.


![](sync_markers.png)

*Sync markers configured on an animation clip. Each marker has a name and a time position.*


Markers are stored as part of the animation asset data. Save the asset after adding or modifying markers.


## Sync Groups and Blend Spaces


Animations within a **[Blend Space 2D Sync](../../../content/animations/graph/node_library/blend_space/blend_space_2d_sync.md)** node are always synchronized internally. The node can also join a sync group to stay in sync with other nodes outside the blend space - for example, keeping an upper-body animation in phase with a locomotion blend space.


## Sync Groups and State Machines


When a **[State Machine](../../../content/animations/state_machines/index.md)** transitions between states, the sync group takes priority over the **Enter Time** set on the transition's **[Transition Result](../../../content/animations/graph/node_library/result/transition_result.md)** node. If the new state's animation node belongs to a sync group that already has other active members, it aligns to the group's current normalized time instead of starting from the configured enter time.


## See Also


- [Animation Graph Editor](../../../content/animations/graph/index.md)
- [Node Library](../../../content/animations/graph/node_library/index.md)
- [Blend Spaces](../../../content/animations/blend_spaces/index.md)
- [State Machines](../../../content/animations/state_machines/index.md)
