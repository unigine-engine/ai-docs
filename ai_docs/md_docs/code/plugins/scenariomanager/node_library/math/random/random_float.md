# Random Float


![](../../img/random_float.png)

### Description

Outputs a random real number between **Min** and **Max**, with every value in the range equally likely.


Each evaluation draws a new number, so a graph that reads the output twice gets two different values. To reuse one draw, store it with a variable node.


Unless a seed is set with [Set Seed](../../../../../../code/plugins/scenariomanager/node_library/math/random/set_seed.md), the sequence differs from run to run.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/float.png) | **Min** | The lower end of the range. Defaults to 0. |
| ![](../../img/types/float.png) | **Max** | The upper end of the range. Defaults to 1. |
| ![](../../img/types/float.png) | **Result** | The random value. |


## See Also


- [Random Int](../../../../../../code/plugins/scenariomanager/node_library/math/random/random_int.md)
- [Random Vec3](../../../../../../code/plugins/scenariomanager/node_library/math/random/random_vec3.md)
- [Set Seed](../../../../../../code/plugins/scenariomanager/node_library/math/random/set_seed.md)
