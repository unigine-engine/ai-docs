# Power Node


![](../img/power.png)

### Description

Outputs Value to the Power-th power of the input scalars and vectors.


- With Power > 0 it corresponds to multiplying Value by itself Power times, e.g. Value = 2, Power = 3 results in 2 x 2 x 2
- With Power < 0 it corresponds to the inverse operation to the one described above, e.g. Value = 2, Power = -2 results in 1/(2 x 2)
- If Power = 0 then it will always output 1 regardless of the specified input Value.


Power on multi-component data types generates an output of the same type with the operator applied per-component.


Note: Please check the following table for a complete behavior of the power operation depending on its input values.


| Value | Power | Result |
|---|---|---|
| < 0 | any | NaN |
| > 0 | == 0 | 1 |
| == 0 | > 0 | 0 |
| == 0 | < 0 | Infinite |
| > 0 | < 0 | 1 / Value-Power |
| == 0 | == 0 | Depends on GPU (0, 1 or NaN) |


## Usage Example

| [**View Fullscreen**](https://matgraph.unigine.com/DocsPower_2.21/fullView) |
|---|
