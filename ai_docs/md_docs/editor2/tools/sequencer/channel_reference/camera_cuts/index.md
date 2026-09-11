# Camera Cuts


A **Camera Cuts** channel switches which camera the viewer looks through over time. Each clip on the channel is one camera; as playback crosses from one clip to the next, the active camera switches with it.


This is how you edit a cinematic as a sequence of shots - a wide shot, then a close-up, then another angle - by laying the cameras out as clips in the order and timing you want.


![](camera_cuts.png)


> **Notice:** How each camera moves and looks is set elsewhere. Its position, its field of view, its exposure and any special effect are animated on their own channels, bound to that camera node. Set the camera up beforehand, or add those channels alongside this one.


## One Active Player at a Time


In UNIGINE the world has exactly one **active player** at a time - the camera it is viewed and heard through. A Camera Cuts channel switches that active player over time, so its effect is global, not local to the sequence:


- **In the Editor** the cut is only a preview, and it has its own preview mode you must switch the viewport into to see it - see [Previewing the Cut](#previewing) below.
- **At runtime** a running sequence with a Camera Cuts channel takes over the active player. When it ends, the original player is restored only if the sequence's [Restore Original Values](../../../../../editor2/tools/sequencer/editor/index.md#restore_mode) setting restores it; otherwise the last shot's camera stays active. Plan a cinematic's start and end around this.


## Filling the Channel


You fill a Camera Cuts channel by dropping **Player** nodes onto it as clips. The clip field is named **Camera** and takes nothing else.


![](choosing_camera_for_clip.png)


Each clip holds one [Player node](../../../../../objects/players/index.md) and covers a span on the timeline. Arrange the clips end to end in the order the shots should play, and the cut happens where one clip ends and the next begins. Clips are trimmed, moved and retimed like any other, as described in the [Clips](../../../../../editor2/tools/sequencer/clips/index.md) article.


On the timeline the channel is drawn as a **filmstrip band**. Each clip shows a preview thumbnail of what its Player sees, so the edit reads as a row of shots.


## Overlapping Clips


A camera cannot be shared, since the viewer looks through exactly one of them at a time. Where two clips cover the same moment, one of them takes the whole span and the other is ignored. The clip on the higher row wins, and between clips on the same row the one that starts later wins.


The boundary is not softened either. The picture switches on the frame the next clip begins, so a dissolve from one camera to another is not something this channel produces.


> **Notice:** A camera clip carries a Weight curve like every other clip, but here it changes nothing. Weight decides how much of a value reaches the result, and a camera has no in-between to arrive at.


## Previewing and Animating Through the Cut


To watch the cut in the Editor, select *Game Camera* in the viewport's camera list. The viewport then looks through whichever camera the Camera Cuts channel is currently driving, so moving the playhead across a clip boundary switches the view with it, exactly as it will play at runtime.


![](game_camera.png)


With *Game Camera* active you also take direct control of the live camera in the viewport. Put the playhead where a moment should happen, fly the camera to the framing you want, and with [Auto-Key](../../../../../editor2/tools/sequencer/keys/index.md#placing) on its position and rotation are keyed there for you. Move to the next moment and do it again, and the shot is built while you watch the final view.


## Custom Channel Properties


A Camera Cuts channel adds one property of its own to the channel inspector:


- **Preview Aspect** - the aspect ratio of the filmstrip thumbnails (16:9, 4:3, 2.39:1, 1:1, 9:16). This is a view setting for the editor only; it is not saved with the sequence and does not affect playback.
