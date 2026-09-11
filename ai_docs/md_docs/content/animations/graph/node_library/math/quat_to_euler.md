# Quat to Euler


![](../img/quat_to_euler.png)

### Description

Decomposes a quaternion into three Euler angles in degrees. The **Order** property selects the axis decomposition order and must match how the quaternion was authored to get the expected angles.


Note that converting a quaternion to Euler angles and back does not always return the original values, because of gimbal lock and the periodicity of angles. This is a mathematical property of the Euler representation, not an error.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/quat.png) | **Quat** | The quaternion to decompose. |
| ![](../img/types/float.png) | **X** | Rotation around the X axis, in degrees. |
| ![](../img/types/float.png) | **Y** | Rotation around the Y axis, in degrees. |
| ![](../img/types/float.png) | **Z** | Rotation around the Z axis, in degrees. |


## Properties


| Order | Axis decomposition order used to extract the angles: XYZ, XZY, YXZ, YZX, ZXY, or ZYX. The default value is ZXY. |
|---|---|


## See Also


- [Euler to Quat](../../../../../content/animations/graph/node_library/math/euler_to_quat.md) node for the inverse conversion.
