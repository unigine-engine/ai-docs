# GUI Mesh


A **GUI Mesh** is a non-flat GUI object based on an arbitrary mesh. If the mesh contains several surfaces, the same GUI will be rendered on each of them.


> **Notice:** The GUI will be rendered according to the UV mapping of surfaces.


Basically, the *GUI Mesh* is a non-flat display, on which GUI is rendered. You can interact with such GUI the same way as with GUI created via the *[Gui](../../../api/library/gui/class.gui_cpp.md)* class.


### See also


- The *[ObjectGuiMesh](../../../api/library/objects/class.objectguimesh_cpp.md)* class to edit GUI meshes via API
- A set of samples located in the `data/samples/objects/` directory:

  - [`gui_01`](../../../code/uniginescript/samples/objects/gui_01.md)


## Creating GUI Mesh


You can add a *GUI Mesh* via UnigineEditor and then assign a widget to it via UnigineScript.


To add the *GUI Mesh*:


1. [Run](../../../sdk/projects/index_cpp.md#run) the project with UnigineEditor.
2. On the Menu bar, click *Create -> GUI -> GUI Mesh*. ![](create_gui_mesh.png)
3. Specify a mesh on which the GUI will be rendered.
4. Place the *GUI Mesh* in the world and [specify the required parameters for it](#edit).
5. In the script, get the GUI object via the *[World.getNodeByName()](../../../api/library/engine/class.world_cpp.md#getNodeByName_cstr_Node)* (or *[World.getNodeByID()](../../../api/library/engine/class.world_cpp.md#getNodeByID_int_Node)*if you have the node index) and assign a widget to it by using functions of the *[ObjectGuiMesh](../../../api/library/objects/class.objectguimesh_cpp.md#getGui_Gui)* class.


## Editing GUI Mesh


In the *Gui Mesh* section of the *Node* tab, you can adjust the following parameters of the *GUI Mesh*:


![](edit_gui_mesh.png)

*Nodetab,Gui Meshsection*


| Show Mouse | Indicates if the mouse cursor should be rendered in the *GUI Mesh*. |
|---|---|
| Control Distance | Distance at which the *GUI Mesh* becomes controllable. |
| Screen Width | Width of the *GUI* object in pixels. |
| Screen Height | Height of the *GUI* object in pixels. |
