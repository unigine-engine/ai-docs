# Time Node


![](../img/time.png)

### Description

This node outputs a float value of time in seconds since the moment of the application startup.


> **Notice:** This node has parameters (see below) that define its behavior, to view and change them double-click somewhere inside the node.


## Parameters

| #### Mode |
|---|
| Timer mode, defines how the time is calculated, when you put animations and particle simulation on pause. One of the following options:: - **Game** - pauses time calculation, when animations and particle simulation are put on pause. - **Real** - continues time calculation, even when animations and particle simulation are put on pause. |

| #### Type |
|---|
| Defines the output value, either current or previous frame time can be returned depending on the option selected. One of the following options:: - **Auto** - Material Graph automatically defines, when to use current or previous frame time. We strongly recommend you to use this option in case you move your vertices depending on time, as this provides automatic calculation of correct velocity for geometry deformation ensuring correct operation of Motion Blur, TAA, and other post-effects that use velocity buffer. - **Current** - always return the time of the current frame. But in case there is deformation of vertices you won't obtain automatically calculated velocity for them. - **Old** - always return the time of the previous frame. But in case there is deformation of vertices you won't obtain automatically calculated velocity for them. |

## Usage Examples

**Scrolling UV**


![Scrolling UV example](../../node_library/img/time_ex.gif)


This material graph demonstrates a basic UV scrolling effect using the **Time** node. The time value is added to the **UV coordinates** (both X and Y), causing the texture to scroll diagonally over time. This is done by connecting the **Time** node output to the **[Add](../../../../../content/materials/graph/node_library/math/add.md)** node, where it's combined with the **[Vertex UV 0](../../../../../content/materials/graph/node_library/input/vertex_uv_0.md)**. The modified UVs are used to sample the texture, creating continuous motion across both axes.


| [**View Fullscreen**](https://matgraph.unigine.com/DocsTime_2.21/fullView) |
|---|
