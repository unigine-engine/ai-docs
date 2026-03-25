# Basic Operations in Tracker


The article describes the basic operations that can be done in the *Tracker*.


## Creating a Track


To create a track with key frames to animate a parameter (render setting, node or material parameter, etc.):


1. Choose *Tools -> Tracker* in the Main Menu to open the *Tracker*.
2. Click ![](../line_add.png) to add a track that will animate some parameter. The *Add Parameter* window will open.
3. Choose a parameter in the list. ![](add_parameter_window.png)
4. If a track animates some node, material setting or a property parameter, etc., bind this track to it via the *Select Node* window that opens. ![](select_node_window.png)
5. [Create](#create_key_frame) the required number of key frames by clicking the track line or the graph. ![](add_key.png)
6. Double-click the created key frame to set or change its value. Here, you can also set a [transition mode](../../../../editor2/tools/tracker/index.md#key_transition) for values. ![](../key_params_window.png) Check all [available ways of key frame editing.](#edit_key_frame)


## Saving and Loading a Track


To save a track to a `.track` file, click **[Save](../../../../editor2/tools/tracker/index.md#save_track)** and specify a track file name in the dialog window that opens.


> **Notice:** If there are several tracks in the Tracks List, all of them will be saved in a single `.track` file.


To load the previously saved track, click **[Load](../../../../editor2/tools/tracker/index.md#load_track)** and choose the track file in the dialog window that opens.


## Playing Animation


- To play animation once, click ![](../time_play.png) in the bottom right corner of the *Tracker*.
- To play animation in a loop, click ![](../time_loop.png).


> **Notice:** For animation to play, the track with the parameter should be enabled (the ![](../enable_track.png) should be toggled on).


## Setting Playback Range


After the track is created, set up the time of animation playback. It would be a common parameter for all tracks in the *Tracker*.


1. Click ![](../time_settings.png) to open time settings.
2. Set the [playback range](../../../../editor2/tools/tracker/index.md#playback_range) that specifies duration of the track playback.
3. Set the [playback speed](../../../../editor2/tools/tracker/index.md#unit_time).


The playback range can be additionally limited (for example, to avoid playing the whole created track, when only one parameter change needs to be tested). There are two ways for that:


- Set the **[From - To](../../../../editor2/tools/tracker/index.md#from_to_range)** range. For example, in the picture below the track will be played only for 0.5 units.
- Drag sliders at either edge of the animation playback line (the same playback line can also be found under the graph): ![](from_to.png)


## Operations on Key Frames


### Creating a Key Frame


There are two approaches to working with key frames:


- Create the required number of key frames and then edit its values by means of the *Tracker* only.
- In UnigineEditor, tweak the parameter that is animated and add a new key frame based on it: the value of such key frame will be automatically set to the current value of the parameter.


#### Creating a Key Frame by Means of Tracker Only


To create a key frame, click the track line:


![](add_key.png)


If there is a graph for the current track, you can create a key frame by clicking directly on the graph:


![](add_key_on_graph.png)


#### Creating a Key Frame from Editor Parameter


After the parameter is added to the *Tracker* to be animated, a track controls its value. You cannot change it in UnigineEditor while the track is enabled. In order to tweak such parameter in UnigineEditor and after that add a new key frame based on it, perform the following:


1. Disable the track with the target parameter by pressing ![](../enable_track.png)
2. Change the parameter by means of UnigineEditor.
3. Create a key frame in the *Tracker*:

  1. Set the time slider in the position where a key frame should be created. ![](time_slider.png)
  2. Select the track with the parameter and click ![](../line_save.png).
4. Enable the track again and play the animation.


The value of the added key frame can be edited [by means of the *Tracker*](#edit_key_frame).


### Editing a Key Frame


To change the value of the created key frame, use one of the following ways:


- Double-click it and specify the required value in the **Value** field of the window that opens.
- [Select the key frame](#select_key_frame) and specify the value in the **Value** field on the upper panel of the *Tracker*.
- Move the selected key frame along the track line to increase or decrease the value.
- If there is a graph for the track, move the target key frame point up to increase the value, or down to decrease it. ![](edit_key_on_graph.gif)


### Selecting a Key Frame


To select a single key frame, simply click it on the track line or on the graph. It will be highlighted white.


To select several key frames, use the *selection box*: click and hold the left mouse button, drag the mouse to select multiple key frames (either on the track line or on the graph):


![](multi_select.png)

*Selecting Multiple Key Frames*


Also, you can press and hold **Ctrl** and select the required key frames one by one.


*Tracker* supports *multi-selection editing* of key frames: you can select multiple keys and set **Time** on the track or **Value** for several parameters simultaneously.


### Cloning a Key Frame


To clone the selected key frame (or multiple keys), press and hold **Shift** while dragging the key frame on the track line or on the graph.


### Snapping to Other Key Frames


To snap the key frame to key frames on other tracks, hold **Alt** while moving it along the track line. Snapping mode can also be turned on by pressing ![](../key_snap.png) on the upper panel.


![](snap_to_track.gif)

*Moving Key Frame Snapped to Other Key Frames*


### Deleting a Key Frame


To delete a key frame, select it on the line and drag the mouse upwards.


![](delete_key.png)


The other ways to delete the key is to click ![](../key_remove.png) or press **Delete**.


## Operations on Graphs


For parameters with values, you can also enable the tracker graph by clicking ![](../enable_track_graph.png) to the right of the parameter in the tracks list.


> **Notice:** Simple tracks (like tracks that toggle objects on and off) do not have a graph.


The graph allows [editing key frames](#edit_key_frame) as well as the track line. It also displays the [transition mode](../../../../editor2/tools/tracker/index.md#key_transition) set for the key frame.


- To change the **graph arrange mode**, use the [special icons](../../../../editor2/tools/tracker/index.md#graph_arrange).
- To **move around** the graph, hold the middle mouse button while dragging it.
- To **scale** the graph, hold the right mouse button while moving the mouse up or down. At that, the tracks list will also be scaled.


![](move_scale_graph.gif)

*Moving Around and Scaling Graph*
