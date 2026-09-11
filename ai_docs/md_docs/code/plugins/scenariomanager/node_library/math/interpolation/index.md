# Interpolation


Nodes that move a value between two others, rescale it from one range to another, or keep it within limits - the arithmetic behind a value that changes gradually rather than jumping.


## Blend Factors and Ranges


[Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md) applies a factor, [Inverse Lerp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/inverse_lerp.md) recovers one from a measured value, and [Remap](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/remap.md) does both at once to convert between ranges.


Most of these nodes do not restrict the factor to the 0 to 1 range, so a value outside it continues past the ends. [Clamp](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/clamp.md) and [SmoothStep](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/smoothstep.md) are the ones that hold the result within bounds.


## Articles in This Section

- [Clamp Node](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/clamp.md)

- [Inverse Lerp Node](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/inverse_lerp.md)

- [Lerp Node](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md)

- [Remap Node](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/remap.md)

- [SmoothDamp Node](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/smoothdamp.md)

- [SmoothStep Node](../../../../../../code/plugins/scenariomanager/node_library/math/interpolation/smoothstep.md)
