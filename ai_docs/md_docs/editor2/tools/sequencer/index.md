# Keyframe Animation and Cutscenes with Sequencer


**Sequencer** is a keyframe animation tool: you pick a parameter, set its value at a few moments on a timeline, and the Engine fills in everything in between. Almost any parameter in your project can be animated this way, so the tool fits both simple animations and full cinematics.

   Sorry, your browser does not support embedded videos.
With **Sequencer** you can:


- **Animate objects in the world** - doors, platforms, lifts, turrets, anything that has to act on cue.
- **Drive lights, materials and the environment** - a lamp dimming, a color shifting, a day-night cycle, a change of weather.
- **Create cinematics** - switch cameras shot by shot, lay sound and music along the timeline, and play character animation on top.
- **Reach into your own code** - put a component's field on a curve, or fire named events your game logic listens for.
- **Reuse your work** - nest a finished sequence inside a longer one, point the same animation at another object, or drive a whole set of objects from one curve.


## Sequence Structure


A **Sequence** is one `*.seq` file. It plays a set of **channels** together on one timeline, and holds a few settings they all share.


![Sequence Structure](sequence_structure.png)

*A sequence with two channels on one timeline:Camera Cutsholding clips, andNode � Positionholding keys on each of its three axes*


Each **channel** animates one parameter, and it answers three questions:


| Which parameter | One parameter, chosen when the channel is created: a node's position, a light's color, a material's albedo color. Adding a channel and choosing what it animates is covered in the **[Channels](../../../editor2/tools/sequencer/channels/index.md)** article. |
|---|---|
| Which object | Its target - the node, material, property or component the value is written to. Pointing a channel at one object or many is covered in the **[Targets](../../../editor2/tools/sequencer/targets/index.md)** article. |
| How it changes | Its values over time, kept in one of two forms depending on the channel type: - **Keys and curves** - a key pins a value at one moment, and the curve between two keys is the path the value takes from one to the other. Key types and tangents are covered in the **[Keys and Curves](../../../editor2/tools/sequencer/keys/index.md)** article. - **Clips** - a block with a start, a length and a piece of content inside it: a sound, a character animation, a camera, another sequence, or a span during which an event is held open. Trimming, retiming and blending clips is covered in the **[Clips](../../../editor2/tools/sequencer/clips/index.md)** article. |


Playing the file is the job of a **[NodeSequencePlayer](../../../objects/animations/sequence_player/index.md)** placed in the world, or one created from your own code. The same `*.seq` can run in as many players as you like, each with its own playhead, its own speed, and its own set of objects the channels drive. Playing a sequence from your own code is covered in the **[Runtime Playback](../../../editor2/tools/sequencer/runtime/index_cpp.md)** article.


## Creating Your First Sequence


The quickest way to see how all of this fits together is to animate one object.


1. **Create a sequence** Choose *Tools -> Sequencer* in the Menu Bar. It opens on a new sequence, ready to edit. You can also make the file first: right-click in the *Asset Browser* and choose *Create Sequence*, then double-click the asset to open it. | ![Tools Menu](creating_sequence_from_tools_menu.png) *Opening Sequencer from the Tools menu* | ![Asset Browser](creating_sequence_from_asset_browser.png) *Creating the sequence asset* | |---|---|
2. **Point the channel at an object** A new sequence already holds one **Node � Position** channel, pointing at nothing. Drop a node from the scene into its target field and the channel takes it over at once - the object moves to the world origin, because the channel arrives with keys at frame 0 and frame 30 that all hold zero. That jump is the sequence already at work: from here on the object is posed through the Sequencer. The next two steps put your own values into those keys. ![](new_empty_sequence.png)
3. **Switch on Auto-Key and pose the start** Turn on **Auto-Key** ![](auto_key.png) on the toolbar. From now on, posing the object records the new value at the playhead by itself, so the animation is built by moving things rather than by pressing a button after each move. Put the playhead on frame 0 and move the object where the motion should begin. The zeros it came with are replaced with the pose you just made. ![](place_first_frame.png) > **Notice:** Auto-Key is one of several ways to place a key. The others, along with everything about shaping the curve that runs between them, are covered in the [Keys and Curves](../../../editor2/tools/sequencer/keys/index.md) article.
4. **Pose the end** Move the playhead to frame 30. The object snaps back to the origin - frame 30 still holds the zeros it came with. Move it to its destination, and that pose is recorded the same way. ![](place_last_frame.png)
5. **Play the sequence** Press ***Space***, or drag the playhead. The object travels from the first pose to the second, playing on the real object in your world.

   Sorry, your browser does not support embedded videos.
## Articles in This Section

- [Sequencer Editor](../../../editor2/tools/sequencer/editor/index.md)

- [Sequence Channels](../../../editor2/tools/sequencer/channels/index.md)

  - [Targets and Bindings](../../../editor2/tools/sequencer/targets/index.md)
  - [Keys and Curves](../../../editor2/tools/sequencer/keys/index.md)
  - [Clips](../../../editor2/tools/sequencer/clips/index.md)

- [Channel Reference](../../../editor2/tools/sequencer/channel_reference/index.md)

  - [Cinematic Channels](../../../editor2/tools/sequencer/channel_reference/cinematic/index.md)

    - [Camera Cuts](../../../editor2/tools/sequencer/channel_reference/camera_cuts/index.md)
    - [Skeletal Animation](../../../editor2/tools/sequencer/channel_reference/skeletal_animation/index.md)
    - [Sound Channel](../../../editor2/tools/sequencer/channel_reference/sound/index.md)
    - [Music Channel](../../../editor2/tools/sequencer/channel_reference/music/index.md)
    - [Sub-Sequence](../../../editor2/tools/sequencer/channel_reference/sub_sequence/index.md)
    - [Follow Path](../../../editor2/tools/sequencer/channel_reference/follow_path/index.md)
    - [Events Channel (CS)](../../../editor2/tools/sequencer/channel_reference/events/index_cs.md)
    - [Events Channel (CPP)](../../../editor2/tools/sequencer/channel_reference/events/index_cpp.md)
    - [Material Channel](../../../editor2/tools/sequencer/channel_reference/material/index.md)
    - [Component Channel](../../../editor2/tools/sequencer/channel_reference/component/index.md)
    - [Console Command Channel](../../../editor2/tools/sequencer/channel_reference/console/index.md)
  - [Specific Engine Channels](../../../editor2/tools/sequencer/channel_reference/engine/index.md)

    - [Property](../../../editor2/tools/sequencer/channel_reference/property/index.md)
    - [Render Parameters](../../../editor2/tools/sequencer/channel_reference/render_parameters/index.md)
    - [Animation Graph Parameters](../../../editor2/tools/sequencer/channel_reference/anim_graph_parameters/index.md)

- [Runtime Playback (CS)](../../../editor2/tools/sequencer/runtime/index_cs.md)

- [Runtime Playback (CPP)](../../../editor2/tools/sequencer/runtime/index_cpp.md)

- [Converting Legacy Tracks](../../../editor2/tools/sequencer/track_import/index.md)
