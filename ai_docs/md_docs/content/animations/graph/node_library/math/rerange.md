# Rerange


![](../img/rerange.png)

### Description

Linearly remaps **Value** from the range [**In Min**, **In Max**] to the range [**Out Min**, **Out Max**]. Values outside the input range are clamped.


For example, remapping from [0, 10] to [0, 100]: a value of 3 becomes 30.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/undefined.png) | **Value** | The value to remap. |
| ![](../img/types/undefined.png) | **In Min** | Input range minimum. |
| ![](../img/types/undefined.png) | **In Max** | Input range maximum. |
| ![](../img/types/undefined.png) | **Out Min** | Output range minimum. |
| ![](../img/types/undefined.png) | **Out Max** | Output range maximum. |
| ![](../img/types/undefined.png) | **Result** | The remapped value. |
