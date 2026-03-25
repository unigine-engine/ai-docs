# Decompose Euler Node


![](../img/decompose_euler.png)

### Description

Decomposes the **input** rotation matrix to the **output** vector of Euler angles (pitch, roll, yaw).


The Euler angles are specified in the axis rotation sequence - XYZ. It is an order of the rings in the three-axis gimbal set: X axis used as the outer ring (independent ring), while Z axis as the inner one (its rotation depends on other 2 rings).


When we talk about axes in UNIGINE, we assume that:


- **X** axis points to the right giving us a **pitch** angle.
- **Y** axis points forward giving us a **roll** angle.
- **Z** axis points up giving us a **yaw** (heading) angle.


> **Notice:** Players have a different coordinate system:
>
>
> - **X** axis points to the *right* giving us a **pitch** angle.
> - **Y** axis points *up* giving us a **yaw** (heading) angle.
> - **Z** axis points *backward* giving us a **-roll** angle.
