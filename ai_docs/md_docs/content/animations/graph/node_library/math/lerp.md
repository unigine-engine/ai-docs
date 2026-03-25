# Lerp


![](../img/lerp.png)

### Description

Performs linear interpolation between **A** and **B** by the factor **T**:


- **T** = 0 returns **A**
- **T** = 1 returns **B**
- **T** = 0.5 returns the midpoint


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/undefined.png) | **A** | The start value. |
| ![](../img/types/undefined.png) | **B** | The end value. |
| ![](../img/types/float.png) | **T** | The interpolation factor, typically in the range [0, 1]. |
| ![](../img/types/undefined.png) | **Result** | The interpolated value. |
