# NotEqual


![](../../img/notequal.png)

### Description

Outputs true when **A** and **B** differ.


Values are compared with a small tolerance rather than exactly, so results of different calculations that should match are treated as equal despite the rounding errors of floating-point arithmetic.


Vectors differ when at least one of their components does. Strings are compared as text, exactly.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/any.png) | **A** | The first operand. |
| ![](../../img/types/any.png) | **B** | The second operand. |
| ![](../../img/types/bool.png) | **Result** | The result of the comparison. |


## See Also


- [Greater](../../../../../../code/plugins/scenariomanager/node_library/math/compare/greater.md)
- [Less](../../../../../../code/plugins/scenariomanager/node_library/math/compare/less.md)
- [Equal](../../../../../../code/plugins/scenariomanager/node_library/math/compare/equal.md)
