# Math Nodes


Nodes that perform arithmetic. They have no execution ports and are evaluated whenever their result is needed.


Related operations are grouped into the [Compare](../../../../../code/plugins/scenariomanager/node_library/math/compare/index.md), [Logic](../../../../../code/plugins/scenariomanager/node_library/math/logic/index.md), [Trig](../../../../../code/plugins/scenariomanager/node_library/math/trig/index.md), [Interpolation](../../../../../code/plugins/scenariomanager/node_library/math/interpolation/index.md), [Curves](../../../../../code/plugins/scenariomanager/node_library/math/curves/index.md) and [Random](../../../../../code/plugins/scenariomanager/node_library/math/random/index.md) subcategories.


## Working with Vectors


The **A** and **B** ports of these nodes are of the Any type and accept numbers as well as vectors. When a vector is connected, the operation is applied to each component separately - adding two Vec3 values adds their X, Y and Z components independently.


Mixing a vector with a number applies the number to every component, so multiplying a Vec3 by 2 scales the whole vector.


When the two inputs have different numbers of components, the result takes the larger of the two, and the missing components of the shorter input are filled with its first component.


> **Notice:** Multiplying two vectors component by component is not the same as a dot or cross product. For those, use [Dot](../../../../../code/plugins/scenariomanager/node_library/vector/dot.md) and [Cross](../../../../../code/plugins/scenariomanager/node_library/vector/cross.md).


## Result Type


The type of the result follows the inputs: two integers give an integer, and a double-precision input gives a double-precision result.


Operations that cannot stay in whole numbers always produce a real result, so dividing two integers keeps the fractional part:


- [Divide](../../../../../code/plugins/scenariomanager/node_library/math/divide.md)
- [Modulo](../../../../../code/plugins/scenariomanager/node_library/math/modulo.md)
- [Sqrt](../../../../../code/plugins/scenariomanager/node_library/math/sqrt.md)
- [Log](../../../../../code/plugins/scenariomanager/node_library/math/log.md)
- [Sin](../../../../../code/plugins/scenariomanager/node_library/math/trig/sin.md), [Cos](../../../../../code/plugins/scenariomanager/node_library/math/trig/cos.md), [Tan](../../../../../code/plugins/scenariomanager/node_library/math/trig/tan.md), [Asin](../../../../../code/plugins/scenariomanager/node_library/math/trig/asin.md) and [Acos](../../../../../code/plugins/scenariomanager/node_library/math/trig/acos.md)


> **Notice:** [Atan2](../../../../../code/plugins/scenariomanager/node_library/math/trig/atan2.md) is not among them: it takes two operands and follows the rule above, so two whole offsets give a whole angle.


## Articles in This Section

- [Abs Node](../../../../../code/plugins/scenariomanager/node_library/math/abs.md)

- [Add Node](../../../../../code/plugins/scenariomanager/node_library/math/add.md)

- [Ceil Node](../../../../../code/plugins/scenariomanager/node_library/math/ceil.md)

- [Divide Node](../../../../../code/plugins/scenariomanager/node_library/math/divide.md)

- [Floor Node](../../../../../code/plugins/scenariomanager/node_library/math/floor.md)

- [Log Node](../../../../../code/plugins/scenariomanager/node_library/math/log.md)

- [Max Node](../../../../../code/plugins/scenariomanager/node_library/math/max.md)

- [Min Node](../../../../../code/plugins/scenariomanager/node_library/math/min.md)

- [Modulo Node](../../../../../code/plugins/scenariomanager/node_library/math/modulo.md)

- [Multiply Node](../../../../../code/plugins/scenariomanager/node_library/math/multiply.md)

- [Negate Node](../../../../../code/plugins/scenariomanager/node_library/math/negate.md)

- [Pow Node](../../../../../code/plugins/scenariomanager/node_library/math/pow.md)

- [Round Node](../../../../../code/plugins/scenariomanager/node_library/math/round.md)

- [Sign Node](../../../../../code/plugins/scenariomanager/node_library/math/sign.md)

- [Sqrt Node](../../../../../code/plugins/scenariomanager/node_library/math/sqrt.md)

- [Subtract Node](../../../../../code/plugins/scenariomanager/node_library/math/subtract.md)

- [Compare](../../../../../code/plugins/scenariomanager/node_library/math/compare/index.md)

  - [Equal Node](../../../../../code/plugins/scenariomanager/node_library/math/compare/equal.md)
  - [Greater Node](../../../../../code/plugins/scenariomanager/node_library/math/compare/greater.md)
  - [GreaterEqual Node](../../../../../code/plugins/scenariomanager/node_library/math/compare/greater_eq.md)
  - [Less Node](../../../../../code/plugins/scenariomanager/node_library/math/compare/less.md)
  - [LessEqual Node](../../../../../code/plugins/scenariomanager/node_library/math/compare/less_eq.md)
  - [NotEqual Node](../../../../../code/plugins/scenariomanager/node_library/math/compare/not_equal.md)

- [Curves](../../../../../code/plugins/scenariomanager/node_library/math/curves/index.md)

  - [Bezier Node](../../../../../code/plugins/scenariomanager/node_library/math/curves/bezier.md)
  - [Bezier Vec3 Node](../../../../../code/plugins/scenariomanager/node_library/math/curves/bezier_vec3.md)
  - [CatmullRom Node](../../../../../code/plugins/scenariomanager/node_library/math/curves/catmullrom.md)
  - [CatmullRom Vec3 Node](../../../../../code/plugins/scenariomanager/node_library/math/curves/catmullrom_vec3.md)

- [Interpolation](../../../../../code/plugins/scenariomanager/node_library/math/interpolation/index.md)

  - [Clamp Node](../../../../../code/plugins/scenariomanager/node_library/math/interpolation/clamp.md)
  - [Inverse Lerp Node](../../../../../code/plugins/scenariomanager/node_library/math/interpolation/inverse_lerp.md)
  - [Lerp Node](../../../../../code/plugins/scenariomanager/node_library/math/interpolation/lerp.md)
  - [Remap Node](../../../../../code/plugins/scenariomanager/node_library/math/interpolation/remap.md)
  - [SmoothDamp Node](../../../../../code/plugins/scenariomanager/node_library/math/interpolation/smoothdamp.md)
  - [SmoothStep Node](../../../../../code/plugins/scenariomanager/node_library/math/interpolation/smoothstep.md)

- [Logic](../../../../../code/plugins/scenariomanager/node_library/math/logic/index.md)

  - [ALL Node](../../../../../code/plugins/scenariomanager/node_library/math/logic/all.md)
  - [AND Node](../../../../../code/plugins/scenariomanager/node_library/math/logic/and.md)
  - [ANY Node](../../../../../code/plugins/scenariomanager/node_library/math/logic/any.md)
  - [NOT Node](../../../../../code/plugins/scenariomanager/node_library/math/logic/not.md)
  - [OR Node](../../../../../code/plugins/scenariomanager/node_library/math/logic/or.md)
  - [XOR Node](../../../../../code/plugins/scenariomanager/node_library/math/logic/xor.md)

- [Random](../../../../../code/plugins/scenariomanager/node_library/math/random/index.md)

  - [Random Float Node](../../../../../code/plugins/scenariomanager/node_library/math/random/random_float.md)
  - [Random Int Node](../../../../../code/plugins/scenariomanager/node_library/math/random/random_int.md)
  - [Random Vec3 Node](../../../../../code/plugins/scenariomanager/node_library/math/random/random_vec3.md)
  - [Set Seed Node](../../../../../code/plugins/scenariomanager/node_library/math/random/set_seed.md)

- [Trig](../../../../../code/plugins/scenariomanager/node_library/math/trig/index.md)

  - [Acos Node](../../../../../code/plugins/scenariomanager/node_library/math/trig/acos.md)
  - [Asin Node](../../../../../code/plugins/scenariomanager/node_library/math/trig/asin.md)
  - [Atan2 Node](../../../../../code/plugins/scenariomanager/node_library/math/trig/atan2.md)
  - [Cos Node](../../../../../code/plugins/scenariomanager/node_library/math/trig/cos.md)
  - [Sin Node](../../../../../code/plugins/scenariomanager/node_library/math/trig/sin.md)
  - [Tan Node](../../../../../code/plugins/scenariomanager/node_library/math/trig/tan.md)
