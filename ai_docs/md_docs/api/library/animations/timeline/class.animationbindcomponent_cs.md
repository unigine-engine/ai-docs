# Unigine::AnimationBindComponent Class (CS)

**Inherits from:** AnimationBind


This binding points a channel at a field of a component assigned to a node, which is how a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cs.md) animates the code of your own project.


The component is addressed by the GUID of its class and the slot it takes on the node, and the animated field by its path inside the component. Everything the bindings share, such as the target list and the match rules, comes from the [AnimationBind](../../../../api/library/animations/timeline/class.animationbind_cs.md) base class.


## AnimationBindComponent Class

### Enums

## KIND

Language the component is written in.
| Name | Description |
|---|---|
| **UNKNOWN** = -1 | The language of the component is not known yet. |
| **CPP** = 0 | The component is a C++ one. |
| **CSHARP** = 1 | The component is a C# one. |

### Properties

## AnimationBindComponent.KIND Kind

The language the component is written in.
## 🔒︎ UGUID ComponentClassGUID

The GUID of the component class the binding points at.
## 🔒︎ int ComponentSlot

The slot of the component on the node, which tells apart several components of one class assigned to the same node.
## string FieldPath

The path to the animated field inside the component.
## string AuthoredFieldType

The type the animated field had when the channel was authored. It is what a field whose type has changed since then is told apart by.
### Members

---

## AnimationBindComponent ( )

Constructor. Creates an empty component binding.
## void SetNodes ( Node [] OUT_nodes )

Points the binding at a set of nodes at once, so that one channel drives the component of each of them.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Nodes the component is looked for on. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void SetComponentDescription ( UGUID class_guid , int slot )

Sets which component is animated: its class and the slot it occupies on the node.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **class_guid** - GUID of the component class.
- *int* **slot** - Slot of the component on the node.

## Node GetTargetResolvedNode ( int i )

Returns the node the specified target of the binding resolves to in the loaded scene.
### Arguments

- *int* **i** - Target number.

### Return value

Node the target resolves to, or NULL (null in C#) if it resolves to none.
## static AnimationBindComponent.KIND GetComponentClassKind ( UGUID property_guid )

Returns the language a component class is written in, given the GUID of the property that declares it. It is how a property can be told to be a C++ component class, a C# one, or no component class whatsoever.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **property_guid** - GUID of the property to be asked about.

### Return value

Language of the component class, or [KIND_UNKNOWN](#KIND_UNKNOWN) if the property is not a component class at all.
## static UGUID FindComponentClass ( UGUID property_guid )

Walks up the property hierarchy from the specified property and returns the component class it descends from. A property assigned to a node is an instance of such a class, and this is what turns it back into the class the channel names.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **property_guid** - GUID of the property to start from.

### Return value

GUID of the component class the property descends from, or an empty GUID if it descends from none.
