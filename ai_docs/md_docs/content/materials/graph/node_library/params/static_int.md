# Static Int Parameter Node


![](../img/int_param.png)

### Description

This is an integer parameter, but unlike **[int](../../../../../content/materials/graph/node_library/textures/sample_texture.md)** it cannot be changed in your material at runtime. The behavior is similar to the **[bool](../../../../../content/materials/graph/node_library/params/bool.md)** parameter, but can have more than one value.


This value should be used to pre-define a certain value in the Editor, for example, when used with the **[Equal](../../../../../content/materials/graph/node_library/logical/equal.md)** node connected to the the *Condition* input of the **[Branch](../../../../../content/materials/graph/node_library/logical/branch.md)** node, only the branch connected to the *True* input is evaluated.)
