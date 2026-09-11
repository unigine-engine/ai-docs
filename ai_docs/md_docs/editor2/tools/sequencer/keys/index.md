# Keys and Curves


A **Key** pins the value of a parameter at one moment in time. Two keys already make an animation: the value travels from the first to the second, and the **Curve** between them is the path it takes.


![](curves_example.png)


Blocking an animation out is placing keys. Polishing it is shaping the curve that runs between them.


## Adding Keys


A key can be put on the timeline in several ways, and they differ in where the value comes from:


- **Double-click empty row space, or choose *Add Key* in the right-click menu.** ![](add_key_menu.png) Both create a key at the point you clicked, holding the object's current value. In the Curves editor the height of the click sets the value instead.
- **Set Key on the channel row.** ![](set_key_button.png) Creates a key at the playhead holding the object's current value, or updates the key already there, keeping its tangents.
- ***Set Key in Sequencer* on the parameter itself.** ![Set Key in Sequencer](set_key_in_sequencer.png) *The command on a node'sPosition. The same item appears on any parameter the Sequencer can animate* Right-click the parameter wherever the editor shows it and the key is written without going to the Sequencer at all. The item is offered on node and surface parameters in the *Parameters* window, on the parameters of a material or a property, and in the *Settings* window on the global settings that can be animated. > **Notice:** The command is only in the menu while the Sequencer window is open, and it writes into the sequence currently open in it.
- **Auto-Key** ![](auto_key.png) **on the toolbar.** Records a key at the playhead every time you edit the parameter itself, with the gizmo or in the *Parameters* window.


All of them write the object's current value, so the way an animation is built is always the same: put the playhead where a moment should happen, pose the object, and record it.


## Key Properties


Every key carries four things. Selecting it brings them into the properties panel, where each can be edited by hand:


![](key_properties.png)


- **Time** - the moment on the timeline the value is pinned at.
- **Value** - what the parameter equals at that moment. Its type follows the channel: a brightness key holds a number, a color key holds a color, a rotation key holds an orientation.
- **Key Type** - how the curve passes through this key, and what kind of segment leaves it.
- **Tangents** - the handles that bend the curve on each side of the key.


The panel also carries a small Curves editor of its own, showing the selected keys with their handles. It behaves the same way as the full one, described in [Sequencer Editor](../../../../editor2/tools/sequencer/editor/index.md#curves).


## Editing Keys


Keys are edited the same way in the Dope Sheet and in the Curves editor, since the two show the same data: an edit in one appears in the other at once.


| Click a key | Select it. ***Shift*** adds to the selection, ***Ctrl*** adds or removes. |
|---|---|
| Drag over empty space | Box-select every key the box covers. |
| Drag a key | Move it in time. In the Curves editor, dragging up or down also changes its value. |
| Drag a tangent handle | Bend the curve on that side of the key. Curves editor only. |
| Double-click a [flag key](../../../../editor2/tools/sequencer/channels/index.md#boolean) | Flip it between on and off. |
| Right-click a key | Open the menu: the interpolation types, *Copy*, *Paste*, *Duplicate* and *Delete*. |
| ***Ctrl + C*** / ***Ctrl + V*** / ***Ctrl + D*** / ***Delete*** | Copy, paste, duplicate and delete the selection. |


With [snapping](../../../../editor2/tools/sequencer/editor/index.md#snap) on, a dragged key lands on a frame or on a nearby anchor rather than wherever it was released.


> **Notice:** Pasted keys land where the cursor is - the row and the time of the right-click, or of the ***Ctrl + V***. They do not return to the time they were copied from.


## Shaping the Curve


How the value moves between two keys is decided by their **key type**. There are six types, offered on a key's right-click menu and in the properties panel.


| ![](key_types_2.png) | ![](key_types.png) |
|---|---|


> **Notice:** Channels holding a value with no in-between, such as a flag or a piece of text, are always stepped. They have no tangents, and no key type is offered for them at all. See [Stepped Values](../../../../editor2/tools/sequencer/channels/index.md#switching_values).


Four of the six use **tangents**: two handles on the key, one to each side. The left handle bends the curve coming in, the right one bends the curve going out. A handle only appears where there is a neighboring key, so the first key has no left handle and the last has no right one.


Drag a handle in the Curves editor to flatten the segment into a hold, steepen it into a fast move, or pull it past the key into an overshoot. The key type decides whether you can drag at all, and what the other handle does when you do.


The handles are also shown as numbers in the properties panel, under **Left Tangent** and **Right Tangent**.


![](tangent_properties.png)


- **Time** - how far along the timeline the handle reaches.
- **Value** - how far above or below the key it sits.


### Auto Flat


The curve flattens at the key, so the value eases into it and out of it. This is the type every new key is created with.


Its handles are kept level and sized automatically, drawn faint, and cannot be dragged. The engine rewrites them whenever a neighboring key moves, so switch the key to **Aligned** or **Break** to shape it by hand.


![](type_auto_flat.png)


### Linear


A straight line to the next key, at constant speed and with no easing. The key has no handles.


![](type_linear.png)


### Smooth


The curve passes through the key without a kink, easing the same amount on both sides.


Drag one handle and the other mirrors it: both of its numbers take the opposite sign, so the two are always the same length.


![](type_smooth.png)


### Aligned


The curve passes through the key without a kink, but eases by a different amount on each side.


Drag one handle and the other turns to face the opposite way.


![](type_aligned.png)


### Break


The curve can turn a corner at the key and leave in a new direction.


The two handles are fully independent: drag one and the other stays exactly where it is.


![](type_break.png)


### Constant


The value holds all the way to the next key, then jumps. There is no motion in between, so the key has no handles.


![](type_constant.png)


## See Also


- [Channels](../../../../editor2/tools/sequencer/channels/index.md)
- [Sequencer Editor](../../../../editor2/tools/sequencer/editor/index.md)
- [Clips](../../../../editor2/tools/sequencer/clips/index.md)
