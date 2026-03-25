# Saturate Node


![](../img/saturate.png)

### Description

Outputs the input value clamped between 0 and 1.


- 0 is returned if input is less than 0
- value is returned if input is between 0 and 1
- 1 is returned if input is greater than 1


## Usage Examples

**Example 1**

This node is widely used, as very often values out of the [0; 1] range can cause calculation failures in algorithms. For example, if we take `dot (Normal_World_Space, Float3(0,0,1))` and look at a sphere, we'll have -1 at its lower pole, while we expect to have 0 there, as we do not see negative values and just want to get a gradient from 0 to 1. So, in this case we can connect the output of the **Dot** node to **Saturate**.
