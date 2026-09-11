# Random Vec3


![](../../img/random_vec3.png)

### Description

Outputs a random vector whose X, Y and Z components each fall between the matching components of **Min** and **Max**. Every component is drawn separately, so the result is spread evenly through the box the two vectors describe.


Giving a component the same value in both inputs pins it, which is how a point is scattered across a horizontal area while its height stays fixed.


Unless a seed is set with [Set Seed](../../../../../../code/plugins/scenariomanager/node_library/math/random/set_seed.md), the sequence differs from run to run.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/vec3.png) | **Min** | The corner of the range with the lowest components. |
| ![](../../img/types/vec3.png) | **Max** | The corner of the range with the highest components. |
| ![](../../img/types/vec3.png) | **Result** | The random vector. |


## See Also


- [Random Float](../../../../../../code/plugins/scenariomanager/node_library/math/random/random_float.md)
- [Random Int](../../../../../../code/plugins/scenariomanager/node_library/math/random/random_int.md)
- [Set Seed](../../../../../../code/plugins/scenariomanager/node_library/math/random/set_seed.md)
