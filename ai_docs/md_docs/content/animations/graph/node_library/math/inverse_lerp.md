# Inverse Lerp


![](../img/inverse_lerp.png)

### Description

Returns where **Value** falls between **A** and **B** as a fraction. The inverse of **[Lerp](../../../../../content/animations/graph/node_library/math/lerp.md)**.


- **Value** = **A** returns 0
- **Value** = **B** returns 1
- Values outside [**A**, **B**] are clamped to [0, 1]
- If **A** = **B**, returns 0


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **A** | The start of the range. |
| ![](../img/types/float.png) | **B** | The end of the range. |
| ![](../img/types/float.png) | **Value** | The value to locate within the range. |
| ![](../img/types/float.png) | **Result** | The normalized position of **Value** between **A** and **B** (0 when **Value** equals **A**, 1 when **Value** equals **B**). |
