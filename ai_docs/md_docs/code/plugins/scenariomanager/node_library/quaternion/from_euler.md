# Euler to Quat


![](../img/euler_to_quat.png)

### Description

Builds a rotation from three angles supplied as the components of **A**: X, Y and Z each give the rotation about that axis.


Angles are measured in degrees and applied in the Z, X, Y order. Because the order matters, the same three angles taken in a different order describe a different orientation - which is why rotations are combined as quaternions rather than by adding up angles.


This is the node to use where a rotation is authored by a person or arrives from settings; [Quat to Euler](../../../../../code/plugins/scenariomanager/node_library/quaternion/to_euler.md) converts back for display.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/vec3.png) | **A** | The rotation angles about the X, Y and Z axes, in degrees. |
| ![](../img/types/quat.png) | **Result** | The resulting rotation. |


## See Also


- [Quat to Euler](../../../../../code/plugins/scenariomanager/node_library/quaternion/to_euler.md)
- [Make Quat](../../../../../code/plugins/scenariomanager/node_library/quaternion/make/quat.md)
- [Quat Multiply](../../../../../code/plugins/scenariomanager/node_library/quaternion/multiply.md)
