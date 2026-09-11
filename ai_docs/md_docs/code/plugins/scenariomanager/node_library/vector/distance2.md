# Vec3 Distance2


![](../img/vec3_distance2.png)

### Description

Outputs the squared distance between the points **A** and **B**, skipping the square root that [Vec3 Distance](../../../../../code/plugins/scenariomanager/node_library/vector/distance.md) takes.


Squaring preserves order, so comparing squared distances ranks two points the same way comparing real distances would - which is what makes this the cheaper node for a proximity test or for finding the nearest of several targets.


> **Notice:** The value is not a distance and must not be mixed with one. A radius compared against it has to be squared as well.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/vec3.png) | **A** | The first point. |
| ![](../img/types/vec3.png) | **B** | The second point. |
| ![](../img/types/float.png) | **Result** | The squared distance between the two points. |


## See Also


- [Vec3 Distance](../../../../../code/plugins/scenariomanager/node_library/vector/distance.md)
- [Length](../../../../../code/plugins/scenariomanager/node_library/vector/length.md)
- [Sqrt](../../../../../code/plugins/scenariomanager/node_library/math/sqrt.md)
