# Unigine::AnimationBindNode Class (CS)

**Inherits from:** AnimationBind


This binding points a channel at a node, which is the most common thing a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cs.md) animates: a transform, a light parameter, anything a node exposes.


The node is named by the targets of the [AnimationBind](../../../../api/library/animations/timeline/class.animationbind_cs.md) base class, either directly or through a query that resolves to a set of nodes when the sequence is played.


## AnimationBindNode Class

### Members

---

## AnimationBindNode ( )

Constructor. Creates an empty node binding.
## void SetNodes ( Node [] OUT_nodes )

Points the binding at a set of nodes at once, so that one channel drives every one of them.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Nodes the binding is to point at. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## Node GetTargetResolvedNode ( int i )

Returns the node the specified target of the binding resolves to in the loaded scene.
### Arguments

- *int* **i** - Target number.

### Return value

Node the target resolves to, or NULL (null in C#) if it resolves to none.
