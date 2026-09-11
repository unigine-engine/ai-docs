# Unigine::AnimationBindComponent Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationBind


This binding points a channel at a field of a component assigned to a node, which is how a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cpp.md) animates the code of your own project.


The component is addressed by the GUID of its class and the slot it takes on the node, and the animated field by its path inside the component. Everything the bindings share, such as the target list and the match rules, comes from the [AnimationBind](../../../../api/library/animations/timeline/class.animationbind_cpp.md) base class.


## AnimationBindComponent Class

### Enums

## KIND

Language the component is written in.
| Name | Description |
|---|---|
| **KIND_UNKNOWN** = -1 | The language of the component is not known yet. |
| **KIND_CPP** = 0 | The component is a C++ one. |
| **KIND_CSHARP** = 1 | The component is a C# one. |

### Members

## void setKind ( AnimationBindComponent::KIND kind )

Sets a new language the component is written in.
### Arguments

- *[AnimationBindComponent::KIND](../../../../api/library/animations/timeline/class.animationbindcomponent_cpp.md#KIND)* **kind** - The language the component is written in

## AnimationBindComponent::KIND getKind () const

Returns the current language the component is written in.
### Return value

Current language the component is written in
## UGUID getComponentClassGUID () const

Returns the current GUID of the component class the binding points at.
### Return value

Current GUID of the component class
## int getComponentSlot () const

Returns the current slot of the component on the node, which tells apart several components of one class assigned to the same node.
### Return value

Current slot of the component on the node
## void setFieldPath ( const char * path )

Sets a new path to the animated field inside the component.
### Arguments

- *const char ** **path** - The path to the animated field of the component

## const char * getFieldPath () const

Returns the current path to the animated field inside the component.
### Return value

Current path to the animated field of the component
## void setAuthoredFieldType ( const char * type )

Sets a new type the animated field had when the channel was authored. It is what a field whose type has changed since then is told apart by.
### Arguments

- *const char ** **type** - The type the field had when the channel was authored

## const char * getAuthoredFieldType () const

Returns the current type the animated field had when the channel was authored. It is what a field whose type has changed since then is told apart by.
### Return value

Current type the field had when the channel was authored
---

## AnimationBindComponent ( )

Constructor. Creates an empty component binding.
## void setNodes ( Vector < Ptr < Node >> OUT_nodes )

Points the binding at a set of nodes at once, so that one channel drives the component of each of them.
### Arguments

- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)>>* **OUT_nodes** - Nodes the component is looked for on. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void setComponentDescription ( const UGUID & class_guid , int slot )

Sets which component is animated: its class and the slot it occupies on the node.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **class_guid** - GUID of the component class.
- *int* **slot** - Slot of the component on the node.

## Ptr < Node > getTargetResolvedNode ( int i ) const

Returns the node the specified target of the binding resolves to in the loaded scene.
### Arguments

- *int* **i** - Target number.

### Return value

Node the target resolves to, or NULL (null in C#) if it resolves to none.
## static AnimationBindComponent::KIND getComponentClassKind ( const UGUID & property_guid )

Returns the language a component class is written in, given the GUID of the property that declares it. It is how a property can be told to be a C++ component class, a C# one, or no component class whatsoever.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **property_guid** - GUID of the property to be asked about.

### Return value

Language of the component class, or [KIND_UNKNOWN](#KIND_UNKNOWN) if the property is not a component class at all.
## static UGUID findComponentClass ( const UGUID & property_guid )

Walks up the property hierarchy from the specified property and returns the component class it descends from. A property assigned to a node is an instance of such a class, and this is what turns it back into the class the channel names.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **property_guid** - GUID of the property to start from.

### Return value

GUID of the component class the property descends from, or an empty GUID if it descends from none.
