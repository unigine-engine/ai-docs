# Lerp3 Node


![](../img/lerp3.png)

### Description

This node is used to blend (linear interpolation) between three input values A, B, and C depending on the Coefficient.


- if Coefficient = 0 the node outputs A value
- if 0 < Coefficient < 0.5 the node outputs a value interpolated between A and B
- if Coefficient = 0.5 the node outputs B value
- if 0.5 < Coefficient < 1 the node outputs a value interpolated between B and C
- if Coefficient = 1 the node outputs C value


## Usage Example

| [**View Fullscreen**](https://matgraph.unigine.com/DocsLerp3_2.21/fullView) |
|---|
