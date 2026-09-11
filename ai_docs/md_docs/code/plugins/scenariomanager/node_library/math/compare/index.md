# Compare


Nodes that compare two values and output a boolean, which is what a [Branch](../../../../../../code/plugins/scenariomanager/node_library/flow/branch.md) or a loop condition reads to decide what happens next.


## Comparing Real Numbers


Values that should be equal often differ in their last digits after being computed, so [Equal](../../../../../../code/plugins/scenariomanager/node_library/math/compare/equal.md) and [NotEqual](../../../../../../code/plugins/scenariomanager/node_library/math/compare/not_equal.md) allow a small tolerance rather than demanding an exact match. The ordering comparisons are exact.


Where vectors are compared, equality considers every component, while the ordering comparisons use only the first one.


## Articles in This Section

- [Equal Node](../../../../../../code/plugins/scenariomanager/node_library/math/compare/equal.md)

- [Greater Node](../../../../../../code/plugins/scenariomanager/node_library/math/compare/greater.md)

- [GreaterEqual Node](../../../../../../code/plugins/scenariomanager/node_library/math/compare/greater_eq.md)

- [Less Node](../../../../../../code/plugins/scenariomanager/node_library/math/compare/less.md)

- [LessEqual Node](../../../../../../code/plugins/scenariomanager/node_library/math/compare/less_eq.md)

- [NotEqual Node](../../../../../../code/plugins/scenariomanager/node_library/math/compare/not_equal.md)
