# Transform Path


**Transform Path** is a succession of transformations based on an arbitrary path. The objects that are made children of the *Transform Path* can move along with these transformations.


![](index.gif)


### See also


- The *[WorldTransformPath](../../../../api/library/worlds/class.worldtransformpath_cpp.md)* class to manage *Transform Path* via API


## Adding Transform Path


To add *Transform Path* to the scene via UnigineEditor, do the following:


1. [Run](../../../../sdk/projects/index_cpp.md#run) the project with UnigineEditor.
2. On the Menu bar, click *Create -> Transform Path*. ![](create.png)
3. Choose the path to the `*.path` file. > **Notice:** The path can be changed afterwards in the *World Transform Path* section of the *Parameters* window.
4. Place the object somewhere in the world.


## Adding Objects Moving along the Path


To make objects move along the path, do the following:


1. Make the object a [child](../../../../editor2/organizing_nodes/index.md#make_child_node) of the path.
2. Set the same initial positions for the object and the path. > **Notice:** If the object coordinates differ from the path coordinates, the object will have the corresponding offset relative to the path.
3. To put the object in motion, click **[Play](#play)** on the *Node* tab.
4. Adjust the [playback parameters](#playback).


## Parameters


In the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window, you can adjust the following parameters of *Transform Path*:


![](parameters.png)


| Path | Sets a path to the new `*.path` file. |
|---|---|
| Orientation | Indicates whether the object should be oriented along the path or keep its initial position. |


### Playback Parameters


*Transform Path* has the following playback parameters:


| Loop | Loops the transformation defined by the path. |
|---|---|
| Update Distance Limit | Sets the distance from the camera within which the object should be updated. |
| Time | Sets the time, from which the playback of the transformation defined by the path starts. > **Notice:** If the object is [oriented](#orientation) along the path, its transformation corresponds to the path transformation at the specified time. Otherwise, only the object position is changed. |
| Speed | Sets the speed of the transformation playback. > **Notice:** Negative values provide the reverse playback. |
| Play | Continues playback of the transformation defined by the path if it has been paused, or starts the playback, if it has been stopped. |
| Stop | Stops the playback of the transformation defined by the path. This function saves the playback position so that playing of the transformation defined by the path can be resumed from the same point. |
