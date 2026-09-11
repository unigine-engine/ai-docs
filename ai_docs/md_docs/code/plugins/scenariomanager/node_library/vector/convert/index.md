# Convert


Nodes that convert a vector from one type to another - between precisions, between whole and real components, and between vectors of different widths.


## What a Conversion Costs


Widening is exact. Narrowing is not: going from double to single precision loses accuracy, which is most visible in a world position far from the origin, and going from real to whole components discards the fractional part by truncating toward zero rather than rounding.


Changing the width either drops the components that do not fit or takes the new one from an extra input.


## See Also


- [Make](../../../../../../code/plugins/scenariomanager/node_library/vector/make/index.md)
- [Break](../../../../../../code/plugins/scenariomanager/node_library/vector/break/index.md)
- [Convert](../../../../../../code/plugins/scenariomanager/node_library/convert/index.md)


## Articles in This Section

- [DVec2 to Vec2 Node](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/dvec2_to_vec2.md)

- [DVec3 to Vec3 Node](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/dvec3_to_vec3.md)

- [DVec4 to Vec4 Node](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/dvec4_to_vec4.md)

- [IVec2 to Vec2 Node](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/ivec2_to_vec2.md)

- [IVec3 to Vec3 Node](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/ivec3_to_vec3.md)

- [IVec4 to Vec4 Node](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/ivec4_to_vec4.md)

- [Vec2 to DVec2 Node](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec2_to_dvec2.md)

- [Vec2 to IVec2 Node](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec2_to_ivec2.md)

- [Vec2 to Vec3 Node](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec2_to_vec3.md)

- [Vec3 to DVec3 Node](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_dvec3.md)

- [Vec3 to IVec3 Node](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_ivec3.md)

- [Vec3 to Vec2 Node](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_vec2.md)

- [Vec3 to Vec4 Node](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_vec4.md)

- [Vec4 to DVec4 Node](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec4_to_dvec4.md)

- [Vec4 to IVec4 Node](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec4_to_ivec4.md)

- [Vec4 to Vec3 Node](../../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec4_to_vec3.md)
