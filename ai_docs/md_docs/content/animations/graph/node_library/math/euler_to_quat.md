# Euler to Quat


![](../img/euler_to_quat.png)

### Description

Composes a quaternion from three Euler angles given in degrees. The **Order** property selects the axis composition order. This node is convenient for producing a quaternion value from readable degree inputs, for example to drive the **Preferred Rotation** input of a joint limit node.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **X** | Rotation around the X axis, in degrees. Default: 0.0. |
| ![](../img/types/float.png) | **Y** | Rotation around the Y axis, in degrees. Default: 0.0. |
| ![](../img/types/float.png) | **Z** | Rotation around the Z axis, in degrees. Default: 0.0. |
| ![](../img/types/quat.png) | **Quat** | The resulting quaternion. |


## Properties


| Order | Axis composition order used to build the quaternion: XYZ, XZY, YXZ, YZX, ZXY, or ZYX. The default value is ZXY. |
|---|---|


## See Also


- [Quat to Euler](../../../../../content/animations/graph/node_library/math/quat_to_euler.md) node for the inverse conversion.
