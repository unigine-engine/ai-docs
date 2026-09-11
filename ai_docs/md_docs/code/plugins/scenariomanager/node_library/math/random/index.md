# Random


Nodes that draw random values, so that a scenario varies between runs instead of unfolding identically every time.


## Repeatable Runs


All random nodes of a graph draw from one shared sequence. Left alone, that sequence starts from a value chosen anew at each launch and the graph behaves differently every run.


[Set Seed](../../../../../../code/plugins/scenariomanager/node_library/math/random/set_seed.md) fixes the starting point, which makes every draw that follows repeat exactly - the basis for a scenario with random elements that can still be replayed and compared. Trigger it before the first random node runs.


> **Notice:** Because the sequence is shared, the order in which random nodes execute is part of what a seed reproduces. Adding or removing a draw shifts every draw after it.


## Articles in This Section

- [Random Float Node](../../../../../../code/plugins/scenariomanager/node_library/math/random/random_float.md)

- [Random Int Node](../../../../../../code/plugins/scenariomanager/node_library/math/random/random_int.md)

- [Random Vec3 Node](../../../../../../code/plugins/scenariomanager/node_library/math/random/random_vec3.md)

- [Set Seed Node](../../../../../../code/plugins/scenariomanager/node_library/math/random/set_seed.md)
