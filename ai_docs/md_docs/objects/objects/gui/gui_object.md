# GUI


**GUI** is a flat GUI object that is positioned in the world and to which different [widgets](../../../api/library/gui/class.widget_cpp.md) are assigned to be displayed.


Basically, a flat *GUI* object is a flat display, on which GUI is rendered. You can interact with such GUI the same way as with GUI created via the *[Gui](../../../api/library/gui/class.gui_cpp.md)* class.


Post-process filters can be applied to a flat *GUI* object (for example, motion blur or any other).


### See also


- The *[ObjectGui](../../../api/library/objects/class.objectgui_cpp.md)* class to edit flat *GUI* objects via API
- A set of samples located in the `data/samples/objects/` directory:

  - [`gui_00`](../../../code/uniginescript/samples/objects/gui_00.md)
  - [`gui_02`](../../../code/uniginescript/samples/objects/gui_02.md)
  - [`gui_03`](../../../code/uniginescript/samples/objects/gui_05.md)
  - [`gui_04`](../../../code/uniginescript/samples/objects/gui_06.md)
  - [`gui_05`](../../../code/uniginescript/samples/objects/gui_07.md)


## Creating GUI


You can add a *GUI* object via UnigineEditor and then assign a widget to it via UnigineScript.


To add the *GUI*:


1. [Run](../../../sdk/projects/index_cpp.md#run) the project with UnigineEditor.
2. On the Menu bar, click *Create -> GUI -> GUI*. ![](create_gui_object.png)
3. Place the created *GUI* in the world and [specify the required parameters for it](#edit).
4. In the code, get the *GUI* via the *[World.getNodeByName()](../../../api/library/engine/class.world_cpp.md#getNodeByName_cstr_Node)* (or *[World.getNodeByID()](../../../api/library/engine/class.world_cpp.md#getNodeByID_int_Node)* if the node index is known) and assign a widget to it by using functions of the *[ObjectGui](../../../api/library/objects/class.objectgui_cpp.md#getGui_Gui)* class.


## Editing GUI


In the *Node* tab of the *[Parameters](../../../editor2/node_parameters/index.md)* window, you can adjust the following parameters of the *GUI* object:


![](edit_gui_object.png)

*Nodetab*


| Billboard | Indicates if the *GUI* is rendered as a billboard. \| [![](billboard_unchecked_sm.png)](billboard_unchecked.png) \| [![](billboard_checked_sm.png)](billboard_checked.png) \| \|---\|---\| \| *Billboardis disabled* \| *Billboardis enabled* \| | [![](billboard_unchecked_sm.png)](billboard_unchecked.png) | [![](billboard_checked_sm.png)](billboard_checked.png) | *Billboardis disabled* | *Billboardis enabled* |
|---|---|---|---|---|---|
| [![](billboard_unchecked_sm.png)](billboard_unchecked.png) | [![](billboard_checked_sm.png)](billboard_checked.png) |  |  |  |  |
| *Billboardis disabled* | *Billboardis enabled* |  |  |  |  |
| Background | Indicates if the *GUI* background (black screen) should be rendered. |  |  |  |  |
| Depth Test | Indicates if the depth test should be used for the *GUI* object. |  |  |  |  |
| Show Mouse | Indicates if the mouse cursor should be rendered in the *GUI* object. |  |  |  |  |
| Control Distance | Distance at which the *GUI* object becomes controllable. |  |  |  |  |
| Polygon Offset | Offset of the *GUI* above the background. This parameter is set to avoid z-fighting. |  |  |  |  |
| Physical Width | Width of the *GUI* in units. |  |  |  |  |
| Physical Height | Height of the *GUI* in units. |  |  |  |  |
| Screen Width | Width of the *GUI* in pixels. |  |  |  |  |
| Screen Height | Height of the *GUI* in pixels. |  |  |  |  |
