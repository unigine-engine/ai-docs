# Break DVec2


![](../../img/break_dvec2.png)

### Description

Splits a DVec2 into its 2 components, so that each can be read or processed on its own.


> **Notice:** The components come out as single-precision values, so the extra precision of a DVec3 world position is not preserved. Keep such a position whole where its precision matters.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/dvec2.png) | **V** | The vector to split. |
| ![](../../img/types/float.png) | **X** | The X component. |
| ![](../../img/types/float.png) | **Y** | The Y component. |


## See Also


- [Break DVec3](../../../../../../code/plugins/scenariomanager/node_library/vector/break/dvec3.md)
- [Break DVec4](../../../../../../code/plugins/scenariomanager/node_library/vector/break/dvec4.md)
- [Make DVec2](../../../../../../code/plugins/scenariomanager/node_library/vector/make/dvec2.md)
