# Animation Graph Parameters


An **Animation Graph Parameter** channel animates one of the parameters an [animation graph](../../../../../content/animations/index.md) exposes - the values its states and transitions read: a speed, a blend weight, a flag, a trigger.


This is the difference between playing an animation at a character and steering the one it already runs. A [Skeletal Animation](../../../../../editor2/tools/sequencer/channel_reference/skeletal_animation/index.md) channel lays a clip over the character; this channel leaves the graph in charge and moves its inputs, so the character keeps blending, transitioning, and reacting as it normally does while the sequence decides what it is doing.


## Two Graphs to Reach


A graph is reached in one of two ways, and the picker offers a separate family for each:


- **Node Skeleton Pose** - the graph assigned to a pose node in the scene. The channel targets that node like any other node channel, and the parameter list is read from the graph the pose carries.
- **Anim Script** - a graph that exists only while the application runs, handed to the channel from code. Nothing in the editor points at it, so both the graph and its parameter name are supplied at runtime.


| ![Node Skeleton Pose family](nodeskeletonpose_access.png) *The graph carried by a pose node in the scene* | ![Anim Script family](animscript_direct_access.png) *The graph handed to the channel from code* |
|---|---|


The two behave identically once the graph is known. The choice is only about where the graph comes from.


## Choosing the Parameter


As with materials, the channel is created first and filled in afterwards: the picker offers one entry per value type, and which parameter is driven is named in the channel properties, in the **Graph Param** field.


The list there is read live from the graph itself, so it holds the parameters that graph actually declares, each with its type - Speed (Float). Picking one retypes the channel to match, so the type chosen in the menu need not be correct.


![Graph Param](nodeskeletonpose_params_example.png)

*The target is set and its graph answers, soGraph Paramoffers what that graph declares - a float the states read, and a trigger they wait on*


> **Notice:** The list stays empty until the graph is known and initialized: on a pose node that means a target is set and the pose carries a graph, and on a runtime graph it means the application is running and code has handed one over. An empty list is not an error, only a step not taken yet - the name can be typed in and resolves once the graph answers to it.


## Keep the Names Stable


A graph parameter is recorded by name, so the channel holds as long as the name does. Rename the parameter in the graph and the channel no longer finds it; the sequence still holds the curve, but nothing reads it until the channel is pointed at the new name.


## See Also


- [Animation Graph](../../../../../content/animations/index.md)
- [Skeletal Animation](../../../../../editor2/tools/sequencer/channel_reference/skeletal_animation/index.md)
- [Channels](../../../../../editor2/tools/sequencer/channels/index.md)
