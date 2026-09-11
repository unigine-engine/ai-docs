# Make Quat


![](../../img/make_quat.png)

### Description

Builds a rotation of **Angle** degrees about the axis given by **Axis X**, **Axis Y** and **Axis Z**.


Describing a rotation as a turn about one axis is the direct way to express a single motion - a hatch swinging about its hinge, or a turret traversing about the vertical. Where the rotation is authored as three separate angles instead, use [Euler to Quat](../../../../../../code/plugins/scenariomanager/node_library/quaternion/from_euler.md).


> **Notice:** This node builds a rotation from an axis and an angle. To supply the four stored components of a quaternion directly, use the [Quat](../../../../../../code/plugins/scenariomanager/node_library/constants/quat.md) constant.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/float.png) | **Axis X** | The X component of the axis to rotate about. |
| ![](../../img/types/float.png) | **Axis Y** | The Y component of the axis to rotate about. |
| ![](../../img/types/float.png) | **Axis Z** | The Z component of the axis to rotate about. |
| ![](../../img/types/float.png) | **Angle (degrees)** | The angle to rotate by, in degrees. |
| ![](../../img/types/quat.png) | **Result** | The resulting rotation. |


## See Also


- [Break Quat](../../../../../../code/plugins/scenariomanager/node_library/quaternion/break/quat.md)
- [Euler to Quat](../../../../../../code/plugins/scenariomanager/node_library/quaternion/from_euler.md)
- [Quat Multiply](../../../../../../code/plugins/scenariomanager/node_library/quaternion/multiply.md)
