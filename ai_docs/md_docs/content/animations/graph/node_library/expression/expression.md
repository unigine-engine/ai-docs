# Expression


![](../img/expression.png)

### Description

Evaluates an inline math expression with support for swizzle operations. This node is typically created automatically when connecting ports of different types (for example, extracting a single component from a vector).


Edit the expression text directly on the node. Use x, y, z, w to access input components. Arithmetic operations are supported (e.g., x * 10 + y). Combine components with commas to build a new vector (e.g., y,x swaps the first two components).


Accepts numeric scalar and vector types: float, vec2, vec3, vec4, int, ivec2, ivec3, ivec4. The output type is determined by the number of components in the expression, using the same base type as the input.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/undefined.png) | **(input)** | A numeric scalar or vector value to operate on. |
| ![](../img/types/undefined.png) | **(output)** | The expression result. The base type matches the input, and the number of components is determined by the expression. |


## See Also


- [Compose Vec2](../../../../../content/animations/graph/node_library/vector/compose_vec2.md)
- [Compose Vec3](../../../../../content/animations/graph/node_library/vector/compose_vec3.md)
- [Compose Vec4](../../../../../content/animations/graph/node_library/vector/compose_vec4.md)
