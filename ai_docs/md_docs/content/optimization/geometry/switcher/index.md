# Switching Nodes On and Off


Simultaneous switching off some parts of the world that are far away from the camera helps to increase the performance.


UNIGINE provides a *[World Switcher](../../../../objects/worlds/world_switcher/index.md)* node that disables and enables all its children at a certain distance. To create and set up the *Switcher*, perform the following:


1. In the Menu Bar, choose *Create → Optimization → Switcher* and add it to the world.
2. Add all the nodes that should be switched on and off as children to the *Switcher* node: in the [World Hierarchy](../../../../editor2/organizing_nodes/index.md), drag the nodes to the *World Switcher* node.
3. In the *World Switcher* tab of the *Parameters* window, specify the [switching distances](../../../../objects/worlds/world_switcher/index.md#editing). ![](switching_distances.png) If you specify the distance that is large enough (for example, several hundred meters), the nodes will disappear unnoticeably for a user.


### See Also


- [The video tutorial on creating a *Switcher*](https://youtu.be/Iqsr3fEvnis?t=893)
