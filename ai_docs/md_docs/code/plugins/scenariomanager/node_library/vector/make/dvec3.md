# Make DVec3


![](../../img/make_dvec3.png)

### Description

Assembles a DVec3 from 3 floating-point values, one per component. The components are supplied at single precision; the assembled vector holds them at double precision.


A component left unconnected takes the value typed into the node body, so a vector can be built with only the components that vary wired up.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/float.png) | **X** | The X component. |
| ![](../../img/types/float.png) | **Y** | The Y component. |
| ![](../../img/types/float.png) | **Z** | The Z component. |
| ![](../../img/types/dvec3.png) | **Result** | The assembled vector. |


## See Also


- [Make DVec2](../../../../../../code/plugins/scenariomanager/node_library/vector/make/dvec2.md)
- [Make DVec4](../../../../../../code/plugins/scenariomanager/node_library/vector/make/dvec4.md)
- [Break DVec3](../../../../../../code/plugins/scenariomanager/node_library/vector/break/dvec3.md)
