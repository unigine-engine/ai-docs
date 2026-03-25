# Step Node


![](../img/step.png)

### Description

Implements a step function:


![Step function formula](../../node_library/img/step_formula.png)


- Outputs 1 if a value or vector component of A is **less or equal** than the value or corresponding vector component of B
- Outputs 0 if a value or vector component of A is **greater** than the value or corresponding vector component of B


## Usage Examples

**Dissolving effect**

[![](../img/step_ex_1.png)](../img/step_ex_1.png)


The following material graph demonstrates how to use the **Step** node to create a binary mask from a noise texture. The noise values are compared against a *fill_percent* threshold, outputting **0** or **1** to define transparent and opaque regions. This mask is used to control the material's **Opacity**, making areas above the threshold visible.


> **Notice:** The **[Mesh Alpha Test PBR](../../../../../content/materials/graph/index.md#common_settings)** material type is used in this example.


| [**View Fullscreen**](https://matgraph.unigine.com/DocsStep_2.21/fullView) |
|---|
