# Frac Node


![](../img/fraction.png)

### Description

Outputs the fractional (or decimal) part of the input scalar value (or individual components of input vectors); which is greater than or equal to 0 and less than 1. Simply put it does something like: `Input - Floor( Input )`, which removes the integer part of the value leaving only the fractional one.

## Usage Examples

**Example 1**

[![](../img/fraction_ex_1.png)](../img/fraction_ex_1.png)


The **Frac** node takes Vertex Position coordinate along the X axis in object's local space Scaled by 4 with the **[Multiply](../../../../../content/materials/graph/node_library/math/multiply.md)** node and provides *Albedo* values for the Material changing the color from black (0,0,0) to white (1, 1, 1) across each 1/4 units of length along the X axis.


| [**View Fullscreen**](https://matgraph.unigine.com/DocsFrac_2.21/fullView) |
|---|
