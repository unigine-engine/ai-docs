# Quat


![](../img/quat.png)

### Description

Outputs a quaternion built from the **X**, **Y**, **Z** and **W** parameters typed into the node body.


The four parameters are stored as the components of the quaternion exactly as they are written. The default 0, 0, 0, 1 is the identity rotation - the one that leaves an orientation unchanged.


To build a rotation from an axis and an angle rather than from raw components, use [Make Quat](../../../../../code/plugins/scenariomanager/node_library/quaternion/make/quat.md).


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/quat.png) | **Value** | The constant quaternion value. |


## See Also


- [Vec4](../../../../../code/plugins/scenariomanager/node_library/constants/vec4.md)
- [Mat3 Identity](../../../../../code/plugins/scenariomanager/node_library/constants/mat3.md)
