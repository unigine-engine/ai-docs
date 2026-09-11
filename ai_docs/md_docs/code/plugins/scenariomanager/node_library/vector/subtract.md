# Vec3 Sub


![](../img/vec3_sub.png)

### Description

Subtracts **B** from **A**.


Subtracting one position from another gives the offset that leads from the second to the first, which is the starting point for finding a heading or a distance: normalize it for a direction, or take its length for how far apart the two are.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/vec3.png) | **A** | The vector to subtract from. |
| ![](../img/types/vec3.png) | **B** | The vector to subtract. |
| ![](../img/types/vec3.png) | **Result** | The difference of the two vectors. |


## See Also


- [Vec3 Add](../../../../../code/plugins/scenariomanager/node_library/vector/add.md)
- [Vec3 Distance](../../../../../code/plugins/scenariomanager/node_library/vector/distance.md)
- [Vec3 Normalize](../../../../../code/plugins/scenariomanager/node_library/vector/normalize.md)
