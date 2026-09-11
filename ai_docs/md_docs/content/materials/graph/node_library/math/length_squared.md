# Length Squared Node


![](../img/length_squared.png)

### Description

Outputs the squared length of the input vector. This method is much faster than **[Length](../../../../../content/materials/graph/node_library/math/length.md)** � the calculation is basically the same only without the slow **[Sqrt](../../../../../content/materials/graph/node_library/math/square_root.md)** call. If you are using lengths simply to compare distances, then it is faster to compare squared lengths against the squares of distances as the comparison gives the same result.
