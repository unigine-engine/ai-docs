# Targets


The Sequencer works out values, but on their own they go nowhere. For a value to reach your world the channel has to be told what to apply it to. That is the channel's **target**, and it is set in the *Targets* section of the channel properties.


![Targets Section](channel_targets_section.png)

*TheTargetssection of aNode � Positionchannel. One row is one target, and+button adds another*


A target can be:


- **Node** - a node in the world. Some parameters accept only one class of node, and the field then refuses anything else. The full list is in the [Built-in Node Types](../../../../objects/index.md) article.
- **Material** - a `*.mat` asset, or the material worn by an object's surface.
- **Property** - a `*.prop` asset, or a property worn by a node or by one of its surfaces.
- **Component** - a C++ or C# component attached to a node.
- **Runtime** - an object that exists only while the application runs, handed to the channel from code.


> **Notice:** Channels driving global settings have no *Targets* section at all. A physics or render setting is shared by the whole world, so there is nothing to point at.


Which of them a channel takes is decided by the channel itself: a position channel takes a node, a material parameter channel takes a material. The kind cannot be changed, only the object within that kind.


## Automatic Targets


Most of the time the target is set for you: the channel is created already pointing at an object. This happens in two cases.


1. You drag a node straight into the Sequencer and pick one of its parameters.
2. You right-click a parameter in the *Parameters* window and choose *Set Key in Sequencer*. This one goes a step further and places a key with the current value straight away. ![Set Key in Sequencer](set_key_in_sequencer.png) *Right-clickingPositionin theParameterswindow. The command creates the channel, points it at this node, and keys the current value in one step*


You come to the *Targets* section when a finished sequence has to drive something else, when one channel should drive many objects at once, or when a target has stopped resolving.


## Setting a Target


Usually a channel drives one object, and you name it outright: drop the object into the field beside the **Match by** picker, which stays on **Direct**.


![Direct target](match_by_picker.png)

*A single named target.Match bystays onDirect, and the field beside it holds the node itself*


A channel is not limited to one, though. The **+** button adds another target and the channel drives them all, so a single curve can dim every lamp in a room. An object listed twice is still driven once, which makes overlapping targets safe.


![Several targets](multiple_targets.png)

*Two targets on one channel. Both lamps are driven by the same keys*


> **Notice:** A channel with no target is still a valid channel. It keeps its keys and saves with the sequence, it simply drives nothing until a target is given - so a curve can be shaped first and pointed at an object afterwards.


## Matching Targets by Rules


A target does not have to point at an object directly. Switch **Match by** to any other mode and you describe a set instead. A described target is worked out afresh during playback: an object created later that fits the description is picked up on its own, and one that is removed simply stops being driven.


![Match by modes](match_by_options.png)

*TheMatch bymodes.Directnames one object; the four below it describe a set to be found*


Named objects and rules mix freely in one channel. A rule shows how many objects it currently matches, so it can be checked while it is being written. Zero is not automatically wrong: a rule made for a world that is not populated yet starts working once the objects exist.


### Nodes


A channel taking nodes offers four rules:


| Match by | What the channel drives |
|---|---|
| **By Name** | Every node whose name matches a wildcard such as Pole_Lamp_*. An empty pattern matches nothing, so write * to take everything in scope. |
| **By Property** | Every node carrying a chosen `*.prop` asset. The property works as a tag here: assign it to the objects a sequence should reach, and the rule follows the tag instead of a list of names. |
| **By Component** | Every node carrying a chosen component class, C++ or C#. |
| **By Type** | Every node of a chosen class. The picker offers groups first, such as **Any Light** or **Any Object**, and the concrete node types below them. |


A rule says where to look before it matches anything:


![Scope](rule_scope.png)

*ABy Namerule with itsScopeopen. The rule reports how many objects it currently matches, here six*


| Scope | Where it looks |
|---|---|
| **World** | The currently loaded world. |
| **Subtree** | A chosen root node and all of its descendants. The root is set in one of two ways: - **By ID (Direct)** - one specific node of this scene. - **By Name (Search)** - looked up by name, so it also reaches nodes that appear while the application runs. |
| **From Node Reference** | Every instance loaded from a chosen `*.node` file, together with the content inside each instance. |


### Materials, Properties, and Components


A node stands in the world, so a rule can go and look for it there. The other three do not stand anywhere by themselves. A material and a property are assets, which a node or one of its surfaces may also be wearing, and a component exists only on the node it is attached to. Each of them therefore carries a setting for how it is reached before any rule runs: **Access** on a material or property channel, the **Class Name** on a component channel.


Each of the three is covered in its own articles:


- [Material](../../../../editor2/tools/sequencer/channel_reference/material/index.md) - **Access**, choosing the surface, parameter slots.
- [Property](../../../../editor2/tools/sequencer/channel_reference/property/index.md) - **Access**, **Property Name**, **Param Path**.
- [Component](../../../../editor2/tools/sequencer/channel_reference/component/index.md) - the class, the field, several components on one node.


## Reading a Channel's Target


What a channel ended up with is printed on its row in the channel list, in parentheses after the parameter name:


| Suffix | Meaning |
|---|---|
| The object's name | The channel drives that one object. |
| The name followed by **(missing)** | A named target that can no longer be found. Drawn red. |
| **(multitarget)** | The channel drives two or more objects. |
| **(not assigned)** | No target is set yet. Drawn dimmed. |
| **(no slot)** | The channel addresses a slot that its target does not have, and it accepts no keys. See [Parameter Slots](../../../../editor2/tools/sequencer/channels/index.md#slots). |
| No suffix | The channel needs no target: a global setting, an event, or a nested sequence. |


**(no slot)** is checked before the rest, so a channel that cannot reach its slot says so even while its target is perfectly healthy.


![Target suffixes](reading_channel_targets.png)

*Every case from the table above, on real rows: a resolved name and(multitarget)in green,(not assigned)dimmed,(missing)and(no slot)in red, and a global setting with no suffix at all*


Where the suffix names a single object that resolves, it is also a link: click it to select that object and reveal it in the scene. It stops being a link as soon as there is nothing single to go to, which covers a missing target, a channel driving several objects, and one with no target at all. The same jump is in the row's right-click menu as *Go to Target*, and on the green suffix beside the channel name in the properties panel.


![Go to Target](go_to_target.png)

*Go to Targetin the row's right-click menu. It selects the driven object in the scene, the same as clicking the name on the row*


## Objects That Exist Only at Runtime


Not everything worth animating is a node. A physical body, a shape, a joint, a particle modifier or a GUI widget - these live inside the Engine without standing in the scene as a row of their own, so there is nothing in the Editor to point at them with.


Such a channel is given its target from code: you find it by channel name on the player and hand the object over while the application runs. The same call also replaces an ordinary target written into the file, and the sequence itself is left untouched - which is how one animation serves many instances, with a hundred identical doors playing it, each on its own.


See the **[Runtime Playback](../../../../editor2/tools/sequencer/runtime/index_cpp.md)** article for details.


## See Also


- [Channels](../../../../editor2/tools/sequencer/channels/index.md)
- [Channel Reference](../../../../editor2/tools/sequencer/channel_reference/index.md)
- [Runtime Playback](../../../../editor2/tools/sequencer/runtime/index_cpp.md)
