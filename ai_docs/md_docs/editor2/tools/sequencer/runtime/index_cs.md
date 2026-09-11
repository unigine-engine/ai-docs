# Runtime Playback (CS)


A `*.seq` file stores keys and the addresses of what they drive - which node, which material, which component field. It holds no scene objects of its own and does not advance on its own. Both are the job of a **player**: it walks the timeline and resolves those addresses to live objects, which is why one file can drive a different set of objects from every player that runs it.


There are two players, and one drives the other:


- **[NodeSequencePlayer](../../../../api/library/nodes/class.nodesequenceplayer_cs.md)** - a node in the world. It saves its setup into the `*.world` file, has a transport in the node inspector, and needs no code at all. Its parameters are covered in the [Sequence Player](../../../../objects/animations/sequence_player/index.md) article.
- **[AnimationSequencePlayer](../../../../api/library/animations/timeline/class.animationsequenceplayer_cs.md)** - the playback machine itself. The node keeps one and ticks it, and you can also create one directly and hold it in your own code, with no node in the scene.


This article covers playing a finished sequence: getting it to run at all, starting and stopping it from code, and deciding what happens to the scene once it is over.


## Playing a Sequence in the Scene


The shortest way needs no code at all.


1. Add a **NodeSequencePlayer** node to the world.
2. Assign your `*.seq` to it in the *Parameters* window.
3. Switch on **Play On Enable**.


The sequence now plays as soon as the node is enabled, which for a node sitting in the world means as soon as the world is loaded. **Loop**, **Speed** and the playback range are in the same panel, so a looping ambient animation is three clicks away. The whole panel is described in the [Sequence Player](../../../../objects/animations/sequence_player/index.md#parameters) article.


> **Notice:** **Play On Enable** picks playback up at the current time, not at the beginning. To always start over, add *[RestartOnEnable](../../../../api/library/nodes/class.nodesequenceplayer_cs.md#RestartOnEnable)*.


The node saves all of this into the `*.world` and survives cloning, so a prop that animates itself can be duplicated around the level and every copy plays on its own.


## Controlling Playback from Code


To start a cutscene on a trigger rather than on load, leave **Play On Enable** off and drive the node from a component. It has the transport controls you would expect: play, pause, stop, the current time, the speed and the loop flag.


```csharp
// C# component attached to the NodeSequencePlayer node in the scene.
NodeSequencePlayer player = node as NodeSequencePlayer;

player.Speed = 1.0f;
player.Loop = false;
player.Play();

// later
player.Time = 2.5f;   // jump to a moment
player.Pause();
player.Stop();        // rewinds and releases the scene

```


Two more that come up often: the player reports its own *[Duration](../../../../api/library/nodes/class.nodesequenceplayer_cs.md#Duration)*, and *[SetTimeRegion()](../../../../api/library/nodes/class.nodesequenceplayer_cs.md#setTimeRegion_float_float_void)* plays only a part of the file, which is handy when one sequence holds several takes.


## Reaching the Player Inside the Node


The node is a thin wrapper. Under the hood it keeps an [AnimationSequencePlayer](../../../../api/library/animations/timeline/class.animationsequenceplayer_cs.md) and ticks it every frame, and the inspector fields and transport buttons are that player's controls put on a node. Everything the node does not expose - the playback weight, the event callbacks, per-instance retargeting - is reached through *[Player](../../../../api/library/nodes/class.nodesequenceplayer_cs.md#Player)*.


```csharp
AnimationSequencePlayer inner = player.Player;

inner.Weight = 0.5f;   // half the sequence's effect on its targets

inner.EventFinished.Connect(() =>
{
	// the sequence reached its end
});

```


> **Notice:** Assigning a different sequence to the node builds a new player, so a pointer taken earlier no longer refers to the one that plays. Take it again after every change of the sequence file.


## Playing Without a Node


A node in the world is not always wanted. An animated interface or a hundred instances of one blink cycle are easier to keep in your own code, so an [AnimationSequencePlayer](../../../../api/library/animations/timeline/class.animationsequenceplayer_cs.md) can be created directly - from a file path, from an asset GUID, or from a sequence built in memory.


```csharp
AnimationSequencePlayer player = new AnimationSequencePlayer("sequences/blink.seq");
player.AutoTick = true;   // let the engine advance it every frame
player.Play();

```


Such a player has the same transport as the one inside the node. *[AutoTick](../../../../api/library/animations/timeline/class.animationsequenceplayer_cs.md#AutoTick)* is what makes the engine advance it every frame; with it off you call *[Update()](../../../../api/library/animations/timeline/class.animationsequenceplayer_cs.md#update_float_void)* yourself, which is what you want when playback has to follow a clock of your own.


**Speed** and **Loop** begin as whatever the sequence itself carries. Setting either on a player overrides it for that player alone; *[ResetSpeed()](../../../../api/library/animations/timeline/class.animationsequenceplayer_cs.md#)* and *[ResetLoop()](../../../../api/library/animations/timeline/class.animationsequenceplayer_cs.md#)* drop the override so the value follows the file again, and *[IsSpeedCustom](../../../../api/library/animations/timeline/class.animationsequenceplayer_cs.md#)* with *[IsLoopCustom](../../../../api/library/animations/timeline/class.animationsequenceplayer_cs.md#)* report whether one is in place. Hand a player a different sequence and it picks up the new file's values wherever it holds no override of its own.


The player is reference counted and lives while anything holds it, and the file behind it is loaded once and shared, so a hundred players over one sequence cost one sequence in memory.


## When Playback Stops


A sequence takes control of everything it animates, which raises a question at the end: who owns those objects now?


**Restore Original Values** answers it. The animated values can be left exactly where the sequence put them, put back to what they were before it started, or restored continuously. The choice is made with the sequence in the editor and described in the [Sequencer Editor](../../../../editor2/tools/sequencer/editor/index.md#restore_mode) article; a single player can depart from it through *[OriginalsRestoreMode](../../../../api/library/animations/timeline/class.animationsequenceplayer_cs.md#OriginalsRestoreMode)*, and a node through the same field in its inspector.


*[Weight](../../../../api/library/animations/timeline/class.animationsequenceplayer_cs.md#Weight)* does the same job gradually. It runs from 0 to 1 and fades the whole sequence's contribution, so a cutscene can dissolve back into live gameplay instead of snapping. At 1 the sequence drives its targets as usual, and at 0 it writes nothing, leaving whatever ran those objects before to take over again.


> **Notice:** Weight fades the values only. Events still fire at their times whatever the weight is, so a sequence faded out of sight can still drive game logic.


## See Also


- [Events](../../../../editor2/tools/sequencer/channel_reference/events/index_cs.md)
- [Targets](../../../../editor2/tools/sequencer/targets/index.md)
- [Sequencer Editor](../../../../editor2/tools/sequencer/editor/index.md)
- [Sequence Player](../../../../objects/animations/sequence_player/index.md) node
- [NodeSequencePlayer](../../../../api/library/nodes/class.nodesequenceplayer_cs.md) class
- [AnimationSequencePlayer](../../../../api/library/animations/timeline/class.animationsequenceplayer_cs.md) class
