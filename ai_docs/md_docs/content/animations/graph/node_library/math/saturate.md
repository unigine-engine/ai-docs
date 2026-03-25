# Saturate


![](../img/saturate.png)

### Description

Clamps the input value to the range [0, 1]. Equivalent to **[Clamp](../../../../../content/animations/graph/node_library/math/clamp.md)** with **Min** = 0 and **Max** = 1.


- Values below 0 become 0
- Values above 1 become 1
- Values in between are unchanged


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/undefined.png) | **Value** | The input value. |
| ![](../img/types/undefined.png) | **Result** | The input value clamped to [0, 1]. |
