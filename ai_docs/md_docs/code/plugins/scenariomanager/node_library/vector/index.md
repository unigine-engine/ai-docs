# Vector Nodes


Nodes that operate on vectors as whole quantities - directions, offsets and positions - rather than on their components one at a time. They have no execution ports and are evaluated whenever their result is needed.


Assembling and taking apart vectors, and converting between vector types, are covered by the [Make](../../../../../code/plugins/scenariomanager/node_library/vector/make/index.md), [Break](../../../../../code/plugins/scenariomanager/node_library/vector/break/index.md) and [Convert](../../../../../code/plugins/scenariomanager/node_library/vector/convert/index.md) subcategories.


## Working with Vec3


The nodes of this category operate on Vec3. A vector of another type connected to one of them is converted first, which for a double-precision value means its extra precision is not kept.


To work with world positions at their full precision, keep them in DVec3 and convert only where a direction or a length is needed.


## Vector Operations and Component-Wise Math


Adding or scaling a vector can also be done with the [Math](../../../../../code/plugins/scenariomanager/node_library/math/index.md) nodes, which apply their operation to each component separately and accept vectors as well as numbers.


The operations here are the ones that treat a vector as a geometric quantity and have no component-wise equivalent: [Dot](../../../../../code/plugins/scenariomanager/node_library/vector/dot.md) and [Cross](../../../../../code/plugins/scenariomanager/node_library/vector/cross.md) relate two directions to each other, [Length](../../../../../code/plugins/scenariomanager/node_library/vector/length.md) and [Vec3 Distance](../../../../../code/plugins/scenariomanager/node_library/vector/distance.md) measure, and [Vec3 Normalize](../../../../../code/plugins/scenariomanager/node_library/vector/normalize.md) and [Reflect](../../../../../code/plugins/scenariomanager/node_library/vector/reflect.md) produce a direction.


## Articles in This Section

- [Vec3 Add Node](../../../../../code/plugins/scenariomanager/node_library/vector/add.md)

- [Cross Node](../../../../../code/plugins/scenariomanager/node_library/vector/cross.md)

- [Vec3 Distance Node](../../../../../code/plugins/scenariomanager/node_library/vector/distance.md)

- [Vec3 Distance2 Node](../../../../../code/plugins/scenariomanager/node_library/vector/distance2.md)

- [Dot Node](../../../../../code/plugins/scenariomanager/node_library/vector/dot.md)

- [Length Node](../../../../../code/plugins/scenariomanager/node_library/vector/length.md)

- [Vec3 Lerp Node](../../../../../code/plugins/scenariomanager/node_library/vector/lerp.md)

- [Vec3 Multiply Add Node](../../../../../code/plugins/scenariomanager/node_library/vector/mad.md)

- [Vec3 negate Node](../../../../../code/plugins/scenariomanager/node_library/vector/negate.md)

- [Vec3 Normalize Node](../../../../../code/plugins/scenariomanager/node_library/vector/normalize.md)

- [Reflect Node](../../../../../code/plugins/scenariomanager/node_library/vector/reflect.md)

- [Vec3 Scale Node](../../../../../code/plugins/scenariomanager/node_library/vector/scale.md)

- [Vec3 Sub Node](../../../../../code/plugins/scenariomanager/node_library/vector/subtract.md)

- [Break](../../../../../code/plugins/scenariomanager/node_library/vector/break/index.md)

  - [Break DVec2 Node](../../../../../code/plugins/scenariomanager/node_library/vector/break/dvec2.md)
  - [Break DVec3 Node](../../../../../code/plugins/scenariomanager/node_library/vector/break/dvec3.md)
  - [Break DVec4 Node](../../../../../code/plugins/scenariomanager/node_library/vector/break/dvec4.md)
  - [Break IVec2 Node](../../../../../code/plugins/scenariomanager/node_library/vector/break/ivec2.md)
  - [Break IVec3 Node](../../../../../code/plugins/scenariomanager/node_library/vector/break/ivec3.md)
  - [Break IVec4 Node](../../../../../code/plugins/scenariomanager/node_library/vector/break/ivec4.md)
  - [Break Vec2 Node](../../../../../code/plugins/scenariomanager/node_library/vector/break/vec2.md)
  - [Break Vec3 Node](../../../../../code/plugins/scenariomanager/node_library/vector/break/vec3.md)
  - [Break Vec4 Node](../../../../../code/plugins/scenariomanager/node_library/vector/break/vec4.md)

- [Convert](../../../../../code/plugins/scenariomanager/node_library/vector/convert/index.md)

  - [DVec2 to Vec2 Node](../../../../../code/plugins/scenariomanager/node_library/vector/convert/dvec2_to_vec2.md)
  - [DVec3 to Vec3 Node](../../../../../code/plugins/scenariomanager/node_library/vector/convert/dvec3_to_vec3.md)
  - [DVec4 to Vec4 Node](../../../../../code/plugins/scenariomanager/node_library/vector/convert/dvec4_to_vec4.md)
  - [IVec2 to Vec2 Node](../../../../../code/plugins/scenariomanager/node_library/vector/convert/ivec2_to_vec2.md)
  - [IVec3 to Vec3 Node](../../../../../code/plugins/scenariomanager/node_library/vector/convert/ivec3_to_vec3.md)
  - [IVec4 to Vec4 Node](../../../../../code/plugins/scenariomanager/node_library/vector/convert/ivec4_to_vec4.md)
  - [Vec2 to DVec2 Node](../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec2_to_dvec2.md)
  - [Vec2 to IVec2 Node](../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec2_to_ivec2.md)
  - [Vec2 to Vec3 Node](../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec2_to_vec3.md)
  - [Vec3 to DVec3 Node](../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_dvec3.md)
  - [Vec3 to IVec3 Node](../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_ivec3.md)
  - [Vec3 to Vec2 Node](../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_vec2.md)
  - [Vec3 to Vec4 Node](../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec3_to_vec4.md)
  - [Vec4 to DVec4 Node](../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec4_to_dvec4.md)
  - [Vec4 to IVec4 Node](../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec4_to_ivec4.md)
  - [Vec4 to Vec3 Node](../../../../../code/plugins/scenariomanager/node_library/vector/convert/vec4_to_vec3.md)

- [Make](../../../../../code/plugins/scenariomanager/node_library/vector/make/index.md)

  - [Make DVec2 Node](../../../../../code/plugins/scenariomanager/node_library/vector/make/dvec2.md)
  - [Make DVec3 Node](../../../../../code/plugins/scenariomanager/node_library/vector/make/dvec3.md)
  - [Make DVec4 Node](../../../../../code/plugins/scenariomanager/node_library/vector/make/dvec4.md)
  - [Make IVec2 Node](../../../../../code/plugins/scenariomanager/node_library/vector/make/ivec2.md)
  - [Make IVec3 Node](../../../../../code/plugins/scenariomanager/node_library/vector/make/ivec3.md)
  - [Make IVec4 Node](../../../../../code/plugins/scenariomanager/node_library/vector/make/ivec4.md)
  - [Make Vec2 Node](../../../../../code/plugins/scenariomanager/node_library/vector/make/vec2.md)
  - [Make Vec3 Node](../../../../../code/plugins/scenariomanager/node_library/vector/make/vec3.md)
  - [Make Vec4 Node](../../../../../code/plugins/scenariomanager/node_library/vector/make/vec4.md)
