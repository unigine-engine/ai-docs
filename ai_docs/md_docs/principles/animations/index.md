# Animation System


Almost anything in a UNIGINE world can be animated, and two systems do most of the work.


An **[Animation Graph](../../content/animations/index.md)** decides what a character's body does while the game runs - walking, aiming, planting a foot on a slope. The **[Sequencer](../../editor2/tools/sequencer/index.md)** plays back a timeline laid out in advance - a lift running its cycle, a lamp dimming at dusk, a full cutscene. The rest comes from physics, from a material, or from a few lines in a component.

   Sorry, your browser does not support embedded videos.
*The Sequencer: parameters keyed on a timeline*


## Choosing an Approach


| What you want to animate | Where to go |
|---|---|
| A character's body, reacting to gameplay | [Animation Graph](../../content/animations/index.md) |
| A cutscene: shots, sound, music, action | [Sequencer](../../editor2/tools/sequencer/index.md) |
| One parameter over time, on a single object or on a whole set | [Sequencer](../../editor2/tools/sequencer/index.md) |
| A character's body in a staged scene | [Sequencer](../../editor2/tools/sequencer/index.md) |
| A value that follows from runtime state | Code in a [component](../../principles/component_system/index.md) |
| Motion that comes out of a simulation | [Physics](../../principles/physics/index.md): bodies, joints, forces |
| Surface-level motion: sway, scroll, ripple | [Material graph](../../content/materials/graph/index.md) and [scriptable materials](../../content/materials/scriptable.md) |
| Facial expressions and blend shapes | [Morph targets](../../content/tutorials/morph/index_cpp.md) on a skinned mesh |
| Movement along a fixed route | [Transform Path](../../objects/worlds/world_transforms/transform_path/index.md) |
| Massed small-scale motion | [Particle systems](../../objects/effects/particles/index.md) |


## Skeletal Animation


Everything with a skeleton goes through this path, from a player character to a rigged machine.


Such a character is a `*.skeleton`, a `*.mesh_skinned` and a set of `*.anim` clips, split out of an `FBX`, `glTF` or `USD` file on import. In the scene a *[Skeleton Pose](../../objects/animations/nodeskeletonpose/index.md)* node computes the pose and a *[Skinned Mesh](../../objects/objects/mesh_skinned/index.md)* shows it. See [Preparing Animation Assets](../../content/animations/animation_assets/index.md).


![](../../content/animations/animation_assets/mesh_skinned_drag_and_drop.png)

*Dropping a skinned mesh into the viewport sets up both nodes at once*


### The Animation Graph


The pose comes from an `*.agraph` - a node network you build in a visual editor and preview on the character as you work. Your code writes a handful of parameters into it - a movement speed, a jump trigger - and the graph works out the rest. One graph built this way serves a whole cast.


It is compiled into a native library on save, so what runs each frame is machine code.

   Sorry, your browser does not support embedded videos.
*The Animation Graph editor*


**[State machines](../../content/animations/state_machines/index.md)** organize behaviour into states with conditional transitions between them: idle, walk, run, jump. Each state holds its own graph, each transition its own condition, so the character picks its own animation from the numbers gameplay hands it.


![](../../content/animations/state_machines/state_machine_example.png)

*A locomotion state machine*


**[Blend spaces](../../content/animations/blend_spaces/index.md)** blend a set of clips by two continuous inputs. A single stick drives the whole locomotion set through them, and the switching between its clips disappears.

   Sorry, your browser does not support embedded videos.
*Previewing a blend at a position in the space*


**[Blend masks](../../content/animations/blend_masks/index.md)** restrict a blend to part of the skeleton, so a character reloads or waves while its legs keep walking.

   Sorry, your browser does not support embedded videos.
*Waving on the upper body while the legs keep walking*


**[Root motion](../../content/animations/root_motion/index.md)** takes the movement authored into a clip out of the pose and hands it to your code as a per-frame delta. The animator sets the exact distance and timing of every step, which is what makes an attack land where it was animated to land and a vault clear its obstacle.

   Sorry, your browser does not support embedded videos.
*Left: the character snaps back on each loop. Right: the movement is extracted as a delta*


**[Procedural control](../../content/animations/procedural_control/index.md)** poses joints from the state of the scene. A raycast finds the real ground and IK bends the leg to it, so the foot lands on the slope instead of hovering over it; a look-at keeps the head on a moving target, and joint limits keep the result anatomically possible.

   Sorry, your browser does not support embedded videos.
*Two Bone IK reaching a target*


**[Retargeting](../../content/animations/retargeting/index.md)** scales joint translations to the body that receives them, so one animation library serves the whole cast whatever their build.

  ![](../../content/animations/retargeting/wrong_retargeting.png)
*Without retargeting: the child plays the adult's animation as authored, and the proportions come out wrong*

  ![](../../content/animations/retargeting/correct_retargeting.png)
*With retargeting: the same animation is scaled to the child's proportions*


## Timeline Animation


Anything that has to happen on cue goes here, from a door that opens when the player arrives to a cutscene with cameras, sound and music on it.


A sequence is one `*.seq` file playing a set of **[channels](../../editor2/tools/sequencer/channels/index.md)** on a shared timeline. A channel animates one parameter, on one object or on a whole set of them, and holds either keys or clips.


![](../../editor2/tools/sequencer/sequence_structure.png)

*A sequence with a clip channel and a keyed channel*


**[Keys and curves](../../editor2/tools/sequencer/keys/index.md)** set the value at a few moments and the Engine fills in between. The curve running from one key to the next is the path the value takes, shaped by the key type and its tangents - the difference between a lift that slams to a halt and one that settles.


![](../../editor2/tools/sequencer/keys/key_types.png)

*The six key types*


**[Clips](../../editor2/tools/sequencer/clips/index.md)** cover a span instead of a moment, carrying a sound, a character animation, a camera or a nested sequence. Trim them, retime them, blend them by weight: a character's walk is laid under the line of dialogue that plays over it, and both are moved around until the shot reads.


![](../../editor2/tools/sequencer/channels/clips.png)

*Clip channels and a keyed channel in one sequence*


**[Cinematic channels](../../editor2/tools/sequencer/channel_reference/cinematic/index.md)** are the pieces a cutscene is assembled from, each built for its own job. Cut between cameras, and fire a named event at the frame the explosion goes off so your code spawns the debris on cue.


![](../../editor2/tools/sequencer/channel_reference/cinematic/cinematic_channels.png)

*The cinematic half of the channel picker*


**[Targets](../../editor2/tools/sequencer/targets/index.md)** keep the animation and the objects apart. Point a channel at one node, or describe a set of them by name, tag, component or type - the rule keeps matching while the sequence plays, so one curve dims a whole street of lamps, including the ones that were not there when it was drawn. The same file also runs on a hundred identical doors, each playing it on its own.


![](../../editor2/tools/sequencer/targets/multiple_targets.png)

*Two lamps driven by the same keys*


**[Component channels](../../editor2/tools/sequencer/channel_reference/component/index.md)** animate a field of one of your own components, C++ or C# alike, so a value that lives in your game code goes on a curve like any engine parameter.


A finished sequence is played by a *[Sequence Player](../../objects/animations/sequence_player/index.md)* node with no code at all, or from your own code - see [Runtime Playback](../../editor2/tools/sequencer/runtime/index_cpp.md).


> **Notice:** The *Tools* menu also holds the **[Tracker](../../editor2/tools/tracker/index.md)**, the keyframe tool the Sequencer replaces. It sits right above the Sequencer in that menu and is kept for projects already built around it; new work belongs in the Sequencer.
>
>
> Work already done in the Tracker carries over: its `*.track` files convert into sequences, as described in [Converting Legacy Tracks](../../editor2/tools/sequencer/track_import/index.md).


## Where the Two Systems Meet


A cutscene reaches a character in one of two ways. A [Skeletal Animation](../../editor2/tools/sequencer/channel_reference/skeletal_animation/index.md) channel lays `*.anim` clips over it and poses the body directly. An [Animation Graph Parameter](../../editor2/tools/sequencer/channel_reference/anim_graph_parameters/index.md) channel leaves the graph in charge and moves its inputs instead, so the character keeps blending and reacting while the sequence tells it what it is doing.


![](../../editor2/tools/sequencer/channel_reference/skeletal_animation/anim_transitions.png)

*Clips crossfading on a Skeletal Animation channel*


## Animation Without a Timeline or a Graph


- **Code** - a [component](../../principles/component_system/index.md) writes the value every frame, when it follows from runtime state no curve could anticipate.
- **Physics** - a [ragdoll body](../../principles/physics/bodies/ragdoll/index.md) for a character that has lost control, a [cloth body](../../principles/physics/bodies/cloth/index.md) for fabric, joints and forces for machinery.
- **Materials** - vertex animation, UV motion and flowmaps run in the shader and reach every instance at once. See the [material graph](../../content/materials/graph/index.md) and [scriptable materials](../../content/materials/scriptable.md); vegetation is driven locally by a [Field Animation](../../objects/effects/fields/field_animation/index.md) node.
- **Morph targets** - blend shapes on a skinned mesh, the usual route for facial expressions. See [Adding Morph Targets](../../content/tutorials/morph/index_cpp.md).
- **Fixed routes** - a [Transform Path](../../objects/worlds/world_transforms/transform_path/index.md) carries its children along a path.
- **Particles** - a [particle system](../../objects/effects/particles/index.md) animates a great many short-lived things at once.


## See Also


- [Animation Graph Overview](../../content/animations/index.md) - building character animation
- [Sequencer](../../editor2/tools/sequencer/index.md) - authoring timeline animation
- [Animations-Related Classes](../../api/library/animations/index.md) - the API reference
- [Animations File Formats](../../code/formats/animations_formats.md) - `*.anim`, `*.skeleton` and the rest on disk
