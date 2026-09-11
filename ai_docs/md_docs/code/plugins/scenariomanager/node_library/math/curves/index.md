# Curves


Nodes that evaluate a curve at a position along it, for progressions and paths that follow a shape rather than a straight line. Each comes in a form that works on single numbers and one that works on points in space.


## Choosing a Curve


[Bezier](../../../../../../code/plugins/scenariomanager/node_library/math/curves/bezier.md) is shaped by control points the curve is pulled toward but does not reach, which suits a shape that is designed - an easing profile, or a route bent around an obstacle.


[CatmullRom](../../../../../../code/plugins/scenariomanager/node_library/math/curves/catmullrom.md) passes through the values it is given, which suits a series of samples or waypoints that must be honoured exactly.


> **Notice:** Equal steps along a curve do not cover equal distances, so movement driven directly by the position varies in speed where the curve bends.


## Articles in This Section

- [Bezier Node](../../../../../../code/plugins/scenariomanager/node_library/math/curves/bezier.md)

- [Bezier Vec3 Node](../../../../../../code/plugins/scenariomanager/node_library/math/curves/bezier_vec3.md)

- [CatmullRom Node](../../../../../../code/plugins/scenariomanager/node_library/math/curves/catmullrom.md)

- [CatmullRom Vec3 Node](../../../../../../code/plugins/scenariomanager/node_library/math/curves/catmullrom_vec3.md)
