# Break DVec4


![](../../img/break_dvec4.png)

### Description

Splits a DVec4 into its 4 components, so that each can be read or processed on its own.


> **Notice:** The components come out as single-precision values, so the extra precision of a DVec3 world position is not preserved. Keep such a position whole where its precision matters.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/dvec4.png) | **V** | The vector to split. |
| ![](../../img/types/float.png) | **X** | The X component. |
| ![](../../img/types/float.png) | **Y** | The Y component. |
| ![](../../img/types/float.png) | **Z** | The Z component. |
| ![](../../img/types/float.png) | **W** | The W component. |


## See Also


- [Break DVec2](../../../../../../code/plugins/scenariomanager/node_library/vector/break/dvec2.md)
- [Break DVec3](../../../../../../code/plugins/scenariomanager/node_library/vector/break/dvec3.md)
- [Make DVec4](../../../../../../code/plugins/scenariomanager/node_library/vector/make/dvec4.md)
