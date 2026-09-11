# World Nodes


A set of world nodes:


- ![](trigger.png) **� [World Trigger](../../objects/worlds/world_trigger/index.md)** � a cuboid-shaped node, which fires callbacks when any node (collider or not) gets inside or outside of it.
- ![](clutter.png) **� [World Clutter](../../objects/worlds/world_clutter/index.md)** � a node used to manage a great number of node references, baked as one object. Objects are scattered, scaled and oriented randomly, they cannot be managed manually.
- ![](switcher.png) **� [Switcher](../../objects/worlds/world_switcher/index.md)** � a cuboid-shaped node, switching off (or turning on) all of the nodes inside of it immediately. *Switcher* should be a parent node for the nodes it controls.
- ![](occluder.png) **� [Occluder](../../objects/worlds/world_occluders/index.md)** � a node used to cull objects that are not seen behind it.
- ![](transform.png) **� [Transform](../../objects/worlds/world_transforms/index.md)** � a succession of transformations based on an arbitrary path.
- ![](expression.png) **� [World Expression](../../objects/worlds/world_expression/index.md)** � a cuboid-shaped node, inside of which arbitrary expressions are executed. These expressions can be executed for children nodes of *World Expression* as well.
- ![](spline_graph.png) **� [World Spline Graph](../../objects/worlds/world_spline_graph/index.md)** � a node used to place various nodes at points and along the segments (linear or curved) of a spline graph. It can be utilized to create roads, pipelines, etc.
