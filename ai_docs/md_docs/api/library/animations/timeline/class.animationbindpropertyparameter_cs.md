# Unigine::AnimationBindPropertyParameter Class (CS)

**Inherits from:** AnimationBind


This binding points a channel at a parameter of a property, which is how a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cs.md) animates the data your project keeps on its nodes and surfaces.


The property is reached from an asset, from a node or from a surface, and the animated parameter inside it is addressed by its path.


## AnimationBindPropertyParameter Class

### Enums

## ACCESS

Access mode. It decides the way the animated property is obtained.
| Name | Description |
|---|---|
| **UNKNOWN** = -1 | The way to obtain the property is not set. |
| **FROM_ASSET** = 0 | The property is taken from a property asset, so the animation writes into the asset itself and reaches everything that uses it. |
| **FROM_NODE** = 1 | The property is taken from a node it is assigned to. |
| **FROM_SURFACE** = 2 | The property is taken from a surface it is assigned to. |

### Properties

## AnimationBindPropertyParameter.ACCESS Access

The access mode of the binding. It decides the way the animated property is obtained.
## 🔒︎ string NodePropertyDescriptionName

The name of the property the binding looks for on the node.
## 🔒︎ int NodePropertyDescriptionIndex

The slot of the property on the node, which tells apart several properties assigned to one node.
## string SurfacePattern

The pattern the surface names are matched against. It picks the surfaces the binding works on inside every object the target resolves to.
## string ParameterPath

The path to the animated parameter inside the property.
### Members

---

## AnimationBindPropertyParameter ( )

Constructor. Creates an empty property parameter binding.
## void SetNodes ( Node [] OUT_nodes )

Points the binding at a set of nodes at once, so that one channel drives every one of them.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Nodes the binding is to point at. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetAssets ( UGUID [] OUT_file_guids )

Points the binding at a set of assets at once.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)[]* **OUT_file_guids** - File GUIDs of the assets. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetNodePropertyDescription ( string name , int index )

Sets which property of the node is animated, by its name and the slot it takes.
### Arguments

- *string* **name** - Name of the property on the node.
- *int* **index** - Slot of the property on the node.

## int GetNumTargetSurfaceMatches ( int i )

Returns how many surfaces the specified target resolves to, which is what tells a surface pattern that found nothing from one that found many.
### Arguments

- *int* **i** - Target number.

### Return value

Number of surfaces the target resolves to.
## Node GetTargetResolvedNode ( int i )

Returns the node the specified target of the binding resolves to in the loaded scene.
### Arguments

- *int* **i** - Target number.

### Return value

Node the target resolves to, or NULL (null in C#) if it resolves to none.
## Property GetTargetResolvedProperty ( int i )

Returns the property the specified target of the binding resolves to, that is, the property instance carried by the node the target names. This is the object the animated parameter is written into.
### Arguments

- *int* **i** - Target number.

### Return value

Property the target resolves to, or NULL (null in C#) if it resolves to none.
