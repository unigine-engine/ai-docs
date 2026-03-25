# Smooth Step


![](../img/smooth_step.png)

### Description

Performs smooth Hermite interpolation based on where **X** falls relative to **Edge0** and **Edge1**:


- **X** <= **Edge0** returns 0
- **X** >= **Edge1** returns 1
- In between, returns a smooth curve from 0 to 1


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **Edge0** | The lower edge of the transition. |
| ![](../img/types/float.png) | **Edge1** | The upper edge of the transition. |
| ![](../img/types/float.png) | **X** | The value to evaluate. |
| ![](../img/types/float.png) | **Result** | The smoothly interpolated value between 0 and 1. |
