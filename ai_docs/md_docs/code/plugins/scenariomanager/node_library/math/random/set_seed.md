# Set Seed


![](../../img/set_seed.png)

### Description

Sets the starting point of the random sequence used by the random nodes of the graph. Running a graph from the same seed makes every draw that follows repeat exactly, which is what turns a scenario with random elements into one that can be replayed and compared.


Without this node the sequence starts from a value chosen anew at each launch, so the graph behaves differently every run. Trigger **Set Seed** before the first random node runs - typically at the start of the scenario - for the whole sequence to be determined.


> **Notice:** All random nodes of a graph share one sequence, so the order in which they execute is part of what the seed reproduces. Adding or removing a random draw shifts every draw after it.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/exec.png) | **Action** | Sets the seed. |
| ![](../../img/types/int.png) | **Seed** | The seed value. Defaults to 12345. |
| ![](../../img/types/exec.png) | **Event** | Triggered once the seed is set. |


## See Also


- [Random Float](../../../../../../code/plugins/scenariomanager/node_library/math/random/random_float.md)
- [Random Int](../../../../../../code/plugins/scenariomanager/node_library/math/random/random_int.md)
- [Random Vec3](../../../../../../code/plugins/scenariomanager/node_library/math/random/random_vec3.md)
