# Sequencer Editor


**Sequencer Editor** is the main window you work on a sequence in. Here you create channels for the parameters to animate, choose the objects those parameters belong to, and lay out how the animation plays over time.


![Sequencer layout](layout.png)

*The Sequencer window with two channels and their keys set up*


## Sequencer Editor Layout


The ***Sequencer Editor*** window is made of three parts:


- **Toolbar** - opening and saving, playback, filtering, and the sequence settings
- **Working Area** - the channels and the timeline, where the animation is built
- **Properties Panel** - the settings of whatever is selected


## Toolbar


The toolbar sits at the top of the Sequencer window and holds the general controls for the sequence.


![Sequencer toolbar](toolbar.png)


### File and Navigation


These controls handle the `*.seq` file itself and show where you currently are inside it.


![File and navigation controls](file_and_navigation.png)


| Control | Action | Shortcut |
|---|---|---|
| **Load** | Open a `*.seq` file. |  |
| **Save** | Write the current sequence to its file. | ***Ctrl + S*** |
| **Save menu** | The button next to Save, with two more actions: *New Empty Sequence* starts a fresh one, *Save As* saves to a new file. |  |
| **Sequence name** | The name of the loaded sequence, shown as a button - click it to reveal the asset in the *Asset Browser*. |  |
| **Breadcrumb bar** | Shows how deep you are in nested sub-sequences. Its arrows step through where you have been; clicking a crumb jumps to that level. |  |


### Playback Controls


These controls move the playhead and play the sequence in the viewport.


![Playback controls](playback_controls.png)


| Control | Action | Shortcut |
|---|---|---|
| **Go to Start** | Stop and jump to the beginning of the range. |  |
| **Step Back** | Move back one frame, or 0.1s in seconds mode. | ***Left Arrow*** |
| **Play / Pause** | Start or pause playback. | ***Spacebar*** |
| **Step Forward** | Move forward one frame, or 0.1s in seconds mode. | ***Right Arrow*** |
| **Go to End** | Stop and jump to the end of the range. |  |
| **Loop** | When on, playback restarts from the beginning on reaching the end. |  |


### Search


The **search box** filters rows by channel or clip name as you type: non-matching channels are hidden and non-matching clips are dimmed. It filters both sections of the working area at once, and keeps working while they are hidden.


![Search box](searchbox.png)


### Snap


The **Snap** button is the master switch for all snapping. The menu button next to it turns on three kinds independently:


![Snap settings](snap_settings.png)


- **Snap to Frames** - dragging keys and clips snaps to the nearest frame. In seconds mode it snaps to 0.1s steps and is labeled Snap to Seconds.
- **Snap to Nearby** - dragging snaps onto nearby anchors: other keys, clip edges, the playhead, region markers, and the sequence start and end.
- **Snap to Value Grid** - a dragged curve key snaps to the nearest multiple of a value step. A **Value Grid Step** field appears next to it to set that spacing.


### Auto-Key


When **Auto-Key** ![](auto_key.png) is on, editing a parameter **that a channel already animates** records the new value at the playhead automatically - move an object with the transform gizmo, or type a value in the Parameters window, and a key appears. It never creates a channel on its own: add the channel first, then Auto-Key fills in keys as you work.


### Section Toggles


The **Dope Sheet** and **Curves** ![](dope_sheet_and_curves.png) buttons show and hide each section of the working area.


These toggles are useful when one of them needs more room. For example, you can turn the **Dope Sheet** off and leave the **Curves** editor alone on screen to shape a curve precisely.


## Working Area


This is the place where the animation is actually made: channels are created here, their parameters chosen, and their keys placed and shaped.


The **playhead** is the vertical line marking the current time. The scene is shown at that moment, and the buttons on a channel row work from it: **Set Key** places its keys there, and **Add Clip** inserts a clip there. Drag it along the ruler to move through the animation, and the scene follows.


![Timeline and Playhead](timeline.png)

*TheTimeline Ruler, with the playhead running along it to mark the current frame - or second, depending on thetime format. The rest of the timeline settings are described inSequence Settingsbelow*


Below the ruler are the two main sections:


- **Dope Sheet** - shows **when** things happen.
- **Curves** - shows **how** the values move between those moments.


They are **two views of the same animated parameters**, so both hold the **same channels** and edit the **same keys**, with a shared selection: whatever you add or change in one appears in the other at once.


Time is shared between the sections: zoom or pan one along time and the other follows. Only the value axis and the row scrolling stay local to each.


### Channels


A **Channel** is one animated parameter, and it is the main building block of a sequence.


Each channel holds three things:


- the parameter it drives
- the target(s), that will be animated with this channel of the sequence
- keys laid out over time


> **Notice:** These are covered in full in the [Channels](../../../../editor2/tools/sequencer/channels/index.md), [Targets](../../../../editor2/tools/sequencer/targets/index.md) and [Keys and Curves](../../../../editor2/tools/sequencer/keys/index.md) articles.


The main operations on channels, available both from the toolbar above the list and from the row's right-click menu:


| Adding a new Channel | - The **+** button - Pressing ***Tab*** over the working area - Dragging a node from the *World Nodes* panel - Using *Set Key in Sequencer* feature |
|---|---|
| Duplicating and Deleting | - The toolbar buttons - The right-click menu - Pressing ***Ctrl + D*** or ***Delete*** with the cursor over the list |
| Copying and Pasting | - *Copy* and *Paste* in the menu, or ***Ctrl + C*** and ***Ctrl + V*** - the whole channel with everything on it - *Paste Keys* - only the keys from the clipboard, onto the channel already selected |
| Reordering | - The **Move Up** and **Move Down** buttons, on the toolbar or in the menu - Dragging a row to where it should sit Order is not only cosmetic: where two channels drive the same parameter of the same object, the higher row wins. |
| Changing the Channel | *Change Channel�* reopens the picker the channel was created from and retypes it. Keys already placed are carried over, as far as the new value type accepts them. |
| Finding the Target | *Go to Target* selects the driven object in the scene. Clicking the object name on the row itself does the same. |
| Enabling and Disabling | The *Enabled* item in the menu, or the check box of the same name in the properties panel. A disabled channel keeps its keys and simply stops driving its parameter. |


![Channel list](ordering_and_regrouping.png)

*Right-click a channel to open the common channel operations*


### Dope Sheet


The Dope Sheet is where you set the timing of the animation. Each channel takes one row, and its keys are marked along the time axis - as diamonds on a keyed channel, as blocks on a clip channel. Dragging a key changes when it happens, not what it holds.


![Dope Sheet](dope_sheet.png)

*The Dope Sheet panel: the channels on the left, the timing of their keys on the right*


| Wheel | Scroll the rows. |
|---|---|
| Shift + wheel | Zoom the time axis (horizontally). |
| Middle-drag | Pan. |
| Left-drag in the ruler | Scrub the playhead. |
| Right-drag on the canvas | Scrub without leaving the row being worked on. |


### Curves


The Curves editor is where you shape how a value moves between keys. The channels are drawn against two axes here, time across and value up: a key's height is its value, and the line between two keys is the path the value takes from one to the other. A channel of several components draws one curve per component.


Placing keys and shaping the curve between them is covered in [Keys and Curves](../../../../editor2/tools/sequencer/keys/index.md).


![Curves](curves.png)

*The Curves panel: the same channels as in the Dope Sheet on the left, the curves of their keys on the right*


Having a second axis, this section adds five buttons of its own at the right-hand end of its channel-list toolbar:


| **Filter Curves** ![](filter_curves.png) | Master switch for filtering what is drawn. Its menu button turns on two filters independently: - **Selected Channels** - draw only the curves of the selected channels - **Selected Keys** - draw only the curves that own a selected key With both on, only the curves matching each condition are drawn. |
|---|---|
| **Focus Selection** ![](focus_selection.png) | Frame the selected keys on both axes, or every visible curve when nothing is selected (***F***). |
| **Fit Values** ![](fit_values.png) | Frame the same content on the value axis only. |
| **Fit Time** ![](fit_time.png) | Frame the same content on the time axis only. |
| **Channel Envelope** ![](channel_envelope.png) | Shade the band between the lowest and highest curve of a multi-component channel, so its X, Y and Z (or R, G, B and A) read as one channel rather than three separate lines. |


| Wheel | Zoom both axes. |
|---|---|
| Shift + wheel | Zoom the time axis only (horizontally). |
| Ctrl + wheel | Zoom the value axis only (vertically). |
| Middle-drag | Pan freely. |


## Properties Panel


The panel on the right changes with the selection: it shows the settings of whatever is currently picked, in three collapsible sections, and only those with something to show are filled.


| Clip | The selected clip: its source, timing, trim and color. See [Clips](../../../../editor2/tools/sequencer/clips/index.md). |
|---|---|
| Channel | The selected channel or group: what it animates, what it drives, and its read-only status. See [Channels](../../../../editor2/tools/sequencer/channels/index.md) and [Targets](../../../../editor2/tools/sequencer/targets/index.md). |
| Selected Keys | The selected keys: time, value, key type and tangents. See [Keys and Curves](../../../../editor2/tools/sequencer/keys/index.md). Above the fields sits a compact curve editor showing just those keys, with its own ruler and framing buttons, so keys can be shaped while the Curves section is hidden or framed elsewhere. |


| ![](properties_key.png) *Keys Section* | ![](properties_clip.png) *Clip Section* | ![](properties_channel.png) *Channel Section* |
|---|---|---|


The panel edits every selected item at once. Where a value differs across the selection the field shows a dash; typing into it writes that value to all of them.


## Sequence Settings


The gear button on the toolbar opens the settings that apply to the sequence as a whole:


![Sequence Settings](sequence_settings.png)


- **Sequence Duration** - the total length of the sequence.
- **Playback Speed** - a multiplier for playback speed.
- **Scene Apply Mode** - whether previewing writes values into the scene, described below.
- **Restore Original Values** - what becomes of the animated values once playback stops, described below.
- **Time Format** - whether the timeline reads in frames or seconds. In frames a frame-rate field appears beside it, mapping frames to real time; changing it re-labels the timeline without moving any key.
- **Limit Playback Range**, with **Range Start** / **Range End** and **Keep Playhead In Range** - play only a part of the sequence, and optionally keep the playhead inside it.


### Scene Apply Mode


A sequence drives the parameters of real scene objects, so previewing it changes those objects in the viewport. This setting decides whether the editor writes those values into the scene. It shapes the editor preview only - a sequence played at runtime always drives its targets and ignores it.


| On Change (default) | Every animated object takes the value its curve holds under the playhead, applied each time the frame changes. Between those changes the objects are left alone, so they can be moved by hand; the next playhead move or key edit returns them to the animated pose. |
|---|---|
| Always | The sequencer writes into the scene every frame and fully owns the animated parameters. Any change from outside - the gizmo, the Parameters window, another tool, or code - is overwritten on the next frame. |
| Never | The sequencer never writes to the scene, so curves can be inspected and edited without disturbing it. |


### Restore Original Values


A sequence overwrites the parameters it animates while it plays. This setting decides what becomes of them once playback stops. It is the authoring default stored in the `*.seq`; at runtime a player can override it (see [Runtime Playback](../../../../editor2/tools/sequencer/runtime/index_cpp.md)).


| Never | The sequence keeps whatever values it applied last. Use it when the animation is meant to change the world for good - a door that swings open stays open. |
|---|---|
| On Stop (default) | The values are captured before the sequence starts changing them, and put back when playback stops. Use it for a cutscene that should leave the scene as it was. |
| Each Frame | The animation plays as an overlay: the originals are restored at the start of every frame and the sequence applied on top, so the viewport shows the animation while game logic still reads the original values. Use it for a camera bob that must not disturb aiming logic. |


## See Also


- [Channels](../../../../editor2/tools/sequencer/channels/index.md)
- [Targets](../../../../editor2/tools/sequencer/targets/index.md)
- [Keys and Curves](../../../../editor2/tools/sequencer/keys/index.md)
- [Clips](../../../../editor2/tools/sequencer/clips/index.md)
