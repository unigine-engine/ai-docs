# Quat to Euler


![](../img/quat_to_euler.png)

### Description

Expresses the rotation **A** as three angles about the X, Y and Z axes, returned as the components of a vector. Angles are in degrees and follow the Z, X, Y order used by [Euler to Quat](../../../../../code/plugins/scenariomanager/node_library/quaternion/from_euler.md), so converting in both directions returns the original rotation.


Angles are the readable form, which makes this the node for showing an orientation on a display or writing it to a log.


> **Notice:** More than one set of angles can describe the same orientation, so the values that come back are not necessarily the ones that went in - only the rotation they represent is the same. Keep rotations as quaternions while they are being computed and convert at the point of display.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/quat.png) | **A** | The rotation to express as angles. |
| ![](../img/types/vec3.png) | **Result** | The angles about the X, Y and Z axes, in degrees. |


## See Also


- [Euler to Quat](../../../../../code/plugins/scenariomanager/node_library/quaternion/from_euler.md)
- [Break Quat](../../../../../code/plugins/scenariomanager/node_library/quaternion/break/quat.md)
- [Format](../../../../../code/plugins/scenariomanager/node_library/string/format.md)
