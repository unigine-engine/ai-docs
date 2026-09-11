# Make DVec2


![](../../img/make_dvec2.png)

### Description

Assembles a DVec2 from 2 floating-point values, one per component. The components are supplied at single precision; the assembled vector holds them at double precision.


A component left unconnected takes the value typed into the node body, so a vector can be built with only the components that vary wired up.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/float.png) | **X** | The X component. |
| ![](../../img/types/float.png) | **Y** | The Y component. |
| ![](../../img/types/dvec2.png) | **Result** | The assembled vector. |


## See Also


- [Make DVec3](../../../../../../code/plugins/scenariomanager/node_library/vector/make/dvec3.md)
- [Make DVec4](../../../../../../code/plugins/scenariomanager/node_library/vector/make/dvec4.md)
- [Break DVec2](../../../../../../code/plugins/scenariomanager/node_library/vector/break/dvec2.md)
