# Path Body


**Path body** represents a spline along which an arbitrary [rigid body](../../../../principles/physics/bodies/rigid/index.md) can be moved. This type of body can be used to create a physically simulated train moving along the railtrack.


![Path body](path_body.jpg)

*APath bodyused as a railway track for a train*


To connect a rigid body to a *Path body* use a *[Path joint](../../../../principles/physics/joints/index.md#path)*.


> **Notice:** Assign a [shape](../../../../principles/physics/shapes/index.md) to a rigid body before connecting it to a *Path body*!


### See also


- *[BodyPath](../../../../api/library/physics/class.bodypath_cpp.md)* class
- Fragment of the video tutorial on physics overviewing the *[Path body](https://youtu.be/w_GJrE-6HtI?t=1124s)*


## Assigning a Path Body


To assign a *Path body* to an object via [UnigineEditor](../../../../editor2/index.md) perform the following steps:


1. Open the *[World Hierarchy](../../../../editor2/interface/index.md#world_hierarchy)* window.
2. Select an object to assign a *Path body* to.
3. Go to the ***Physics*** tab in the *[Parameters](../../../../editor2/interface/index.md#parameters)* window and assign a physical [body](../../../../principles/physics/bodies/index.md) to the selected object by selecting *Body -> **Path***. ![Adding a body](../add_body.jpg)
4. Specify a `*.path` file.
5. Set body's name and change other parameters if necessary.
