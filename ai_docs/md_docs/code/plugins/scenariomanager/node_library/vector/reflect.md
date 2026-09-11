# Reflect


![](../img/reflect.png)

### Description

Bounces the direction **A** off a surface whose normal is **B**, as a ray reflects off a mirror: the component along the normal is reversed while the component along the surface is kept.


This gives the outgoing direction of a ricochet or a bounce from a computed contact normal.


> **Notice:** The normal is expected to be of unit length. Pass it through [Vec3 Normalize](../../../../../code/plugins/scenariomanager/node_library/vector/normalize.md) first if it was computed rather than taken from a collision.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/vec3.png) | **A** | The incoming direction. |
| ![](../img/types/vec3.png) | **B** | The normal of the surface to reflect off. |
| ![](../img/types/vec3.png) | **Result** | The reflected direction. |


## See Also


- [Vec3 Normalize](../../../../../code/plugins/scenariomanager/node_library/vector/normalize.md)
- [Cross](../../../../../code/plugins/scenariomanager/node_library/vector/cross.md)
- [Dot](../../../../../code/plugins/scenariomanager/node_library/vector/dot.md)
