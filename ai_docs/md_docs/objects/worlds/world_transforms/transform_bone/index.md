# Transform Joint


**Transform Joint** is an object that obtains transformations of the specific joint of the *Skinned Mesh*. The nodes that are made children of *Transform Joint* move in accordance with these transformations. You can use it, for example, to attach a weapon to your character's hand.


![](index.gif)

*Skinned Meshin the example contains 6 joints.Transform Jointwith a multicolored set of boxes is assigned to its third joint*


### See also


- The *[WorldTransformJoint](../../../../api/library/worlds/class.worldtransformjoint_cpp.md)* class to manage *Transform Joint* via API
- The sample `<UnigineSDK>/data/samples/worlds/joint_00`


## Adding Transform Joint to the Skinned Mesh


To add a *Transform Joint* to the scene via UnigineEditor, do the following:


1. [Run](../../../../sdk/projects/index_cpp.md#run) the project with UnigineEditor.
2. On the Menu bar, click *Create -> Mesh -> Skinned Joint*. ![](create.png)
3. Place the node somewhere in the world.
4. Make the *Transform Joint* the [child](../../../../editor2/organizing_nodes/index.md#make_child_node) of a *Skinned Mesh*.
5. Make the required objects [children](../../../../editor2/organizing_nodes/index.md#make_child_node) of the *Transform Joint*.
6. In the *Node* tab, specify the *Transform Joint* [parameters](#parameters).


## Parameters


In the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window, you can adjust the following parameters of *Transform Joint*:


![](parameters.png)


| Joint | Specifies the joint, transformations of which are applied to objects. |
|---|---|
