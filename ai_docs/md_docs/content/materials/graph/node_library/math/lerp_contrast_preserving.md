# Lerp Contrast Preserving Node


![](../img/lerp_contrast_preserving.png)

### Description

This node is used to blend (linear interpolation) between two input colors Color 0 and Color 1 depending on the Blend (0-1) value. The colors Color 0 Blurred and Color 1 Blurred enable you to affect intermediate color values.


- if Blend = 0 the node outputs Color 0 value
- if Blend = 1 the node outputs Color 1 value
- for all other Blend (0-1) values the node outputs a linear blend of Color 0 and Color 1 with respect to the Color 0 Blurred and Color 1 Blurred values.


This node preserves contrast avoiding intermediate "dirty" color shades unlike the [Lerp](../../../../../content/materials/graph/node_library/math/lerp.md) node. For example, if you decide to blend red and green color, Lerp Contrast Preserving will let you get yellow output, while with Lerp you'll get muddy brown.
