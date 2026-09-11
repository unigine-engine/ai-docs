# Random Int


![](../../img/random_int.png)

### Description

Outputs a random whole number from **Min** up to but not including **Max**. Picking one of five options therefore means a range of 0 to 5, which yields 0 through 4.


Each evaluation draws a new number. Unless a seed is set with [Set Seed](../../../../../../code/plugins/scenariomanager/node_library/math/random/set_seed.md), the sequence differs from run to run.


> **Notice:** When **Max** is not greater than **Min** the range is empty and the node outputs **Min**.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/int.png) | **Min** | The lowest value that can be drawn. Defaults to 0. |
| ![](../../img/types/int.png) | **Max** | The upper bound, which is never drawn itself. Defaults to 100. |
| ![](../../img/types/int.png) | **Result** | The random value. |


## See Also


- [Random Float](../../../../../../code/plugins/scenariomanager/node_library/math/random/random_float.md)
- [Random Vec3](../../../../../../code/plugins/scenariomanager/node_library/math/random/random_vec3.md)
- [Set Seed](../../../../../../code/plugins/scenariomanager/node_library/math/random/set_seed.md)
