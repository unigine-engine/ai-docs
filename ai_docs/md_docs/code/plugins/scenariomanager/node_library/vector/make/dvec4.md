# Make DVec4


![](../../img/make_dvec4.png)

### Description

Assembles a DVec4 from 4 floating-point values, one per component. The components are supplied at single precision; the assembled vector holds them at double precision.


A component left unconnected takes the value typed into the node body, so a vector can be built with only the components that vary wired up.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/float.png) | **X** | The X component. |
| ![](../../img/types/float.png) | **Y** | The Y component. |
| ![](../../img/types/float.png) | **Z** | The Z component. |
| ![](../../img/types/float.png) | **W** | The W component. |
| ![](../../img/types/dvec4.png) | **Result** | The assembled vector. |


## See Also


- [Make DVec2](../../../../../../code/plugins/scenariomanager/node_library/vector/make/dvec2.md)
- [Make DVec3](../../../../../../code/plugins/scenariomanager/node_library/vector/make/dvec3.md)
- [Break DVec4](../../../../../../code/plugins/scenariomanager/node_library/vector/break/dvec4.md)
