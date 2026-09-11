# Break Quat


![](../../img/break_quat.png)

### Description

Splits a quaternion into the four numbers it stores.


> **Notice:** These are the raw components, not angles, and none of them corresponds to a rotation about a single axis. To read an orientation in a form a person can interpret, use [Quat to Euler](../../../../../../code/plugins/scenariomanager/node_library/quaternion/to_euler.md).


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../../img/types/quat.png) | **Q** | The quaternion to split. |
| ![](../../img/types/float.png) | **X** | The X component. |
| ![](../../img/types/float.png) | **Y** | The Y component. |
| ![](../../img/types/float.png) | **Z** | The Z component. |
| ![](../../img/types/float.png) | **W** | The W component. |


## See Also


- [Make Quat](../../../../../../code/plugins/scenariomanager/node_library/quaternion/make/quat.md)
- [Quat to Euler](../../../../../../code/plugins/scenariomanager/node_library/quaternion/to_euler.md)
- [Quat](../../../../../../code/plugins/scenariomanager/node_library/constants/quat.md)
