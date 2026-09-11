# Skeletal Animation


A **Skeletal Animation** channel plays skeletal animation clips (`*.anim` files) on a character over the timeline. It is how you place character motion inside a cutscene: a walk here, a turn there, a wave at the end. Each clip is one `*.anim` file. Arrange the clips in the order and timing you want, and the character performs them as the playhead moves across.


![](skeletal_animation.png)


## Binding to a Skeleton Pose


The channel drives a **Skeleton Pose** node (*[NodeSkeletonPose](../../../../../objects/animations/nodeskeletonpose/index.md)*). Drag that node in and the skinned mesh follows on its own: the pose node moves the bones, the mesh only shows the result.


![](skeletal_animation_target.png)


## Filling the Channel


Add `*.anim` clips to the channel as blocks on the timeline. The simplest way is to double-click an empty spot on the row - a clip is created there and you pick its `*.anim` in the clip's properties. Each clip plays its animation while the playhead is over it. Clips are trimmed, moved, retimed, and looped past the animation's own length, just like the other clip channels, as described in the [Clips](../../../../../editor2/tools/sequencer/clips/index.md) article. How fast a clip plays its animation is set by the **Speed** curve on its [sub-tracks](../../../../../editor2/tools/sequencer/clips/index.md#sub_tracks).


![](picking_animation.png)


## Reading the Clip


The bars drawn inside a clip are a diagram of the motion in it. Each one measures how much the skeleton moves at that moment, so a flat stretch is a hold and a tall one is a burst of action. The rhythm of an animation can be read off the clip without playing it.


The diagram is drawn through the clip's own trim, speed and looping, so it shows what actually plays rather than the contents of the file. That includes the ghosted stretch past the end of the animation, described in [Clips](../../../../../editor2/tools/sequencer/clips/index.md#beyond).


## Overlapping Clips


When two clips overlap in time, they blend as layers rather than one replacing the other. The clip on the higher row sits on top, and within one row the later-starting clip is on top.


The top clip has first claim on the character. If its **Weight** does not take all of it, what is left goes to the clip below, and so on down the rows. Whatever no clip claims is filled in with the character's rest pose. At full weight the top clip leaves nothing behind it, which is why clips laid end to end still cut cleanly from one animation to the next.


To cross one animation into another, ramp the **Weight** of the upper clip alone, from 0 to 1 across the overlap, and leave the lower one at full. Whatever the upper clip does not take passes down on its own. Weight is keyed on the clip's own [sub-tracks](../../../../../editor2/tools/sequencer/clips/index.md#sub_tracks), so expand the clip to reach it.


![](anim_transitions.png)


> **Notice:** Do not fade both clips at once. Neither of them claims the character in full then, the rest pose fills what is left over, and the result reads as limp. Only the upper clip is ever faded.


A channel blends at most 16 clips covering the same moment. Where no clip covers at all, the character holds its rest pose rather than being released.
