# Unigine::AnimationBindPropertyParameter Class (CPP)

**Header:** #include <UnigineAnimation.h>

**Inherits from:** AnimationBind


This binding points a channel at a parameter of a property, which is how a [sequence](../../../../api/library/animations/timeline/class.animationsequence_cpp.md) animates the data your project keeps on its nodes and surfaces.


The property is reached from an asset, from a node or from a surface, and the animated parameter inside it is addressed by its path.


## AnimationBindPropertyParameter Class

### Enums

## ACCESS

Access mode. It decides the way the animated property is obtained.
| Name | Description |
|---|---|
| **ACCESS_UNKNOWN** = -1 | The way to obtain the property is not set. |
| **ACCESS_FROM_ASSET** = 0 | The property is taken from a property asset, so the animation writes into the asset itself and reaches everything that uses it. |
| **ACCESS_FROM_NODE** = 1 | The property is taken from a node it is assigned to. |
| **ACCESS_FROM_SURFACE** = 2 | The property is taken from a surface it is assigned to. |

### Members

## void setAccess ( AnimationBindPropertyParameter::ACCESS access )

Sets a new access mode of the binding. It decides the way the animated property is obtained.
### Arguments

- *[AnimationBindPropertyParameter::ACCESS](../../../../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md#ACCESS)* **access** - The access mode of the binding

## AnimationBindPropertyParameter::ACCESS getAccess () const

Returns the current access mode of the binding. It decides the way the animated property is obtained.
### Return value

Current access mode of the binding
## const char * getNodePropertyDescriptionName () const

Returns the current name of the property the binding looks for on the node.
### Return value

Current name of the property on the node
## int getNodePropertyDescriptionIndex () const

Returns the current slot of the property on the node, which tells apart several properties assigned to one node.
### Return value

Current slot of the property on the node
## void setSurfacePattern ( const char * pattern )

Sets a new pattern the surface names are matched against. It picks the surfaces the binding works on inside every object the target resolves to.
### Arguments

- *const char ** **pattern** - The pattern the surface names are matched against

## const char * getSurfacePattern () const

Returns the current pattern the surface names are matched against. It picks the surfaces the binding works on inside every object the target resolves to.
### Return value

Current pattern the surface names are matched against
## void setParameterPath ( const char * path )

Sets a new path to the animated parameter inside the property.
### Arguments

- *const char ** **path** - The path to the animated parameter inside the property

## const char * getParameterPath () const

Returns the current path to the animated parameter inside the property.
### Return value

Current path to the animated parameter inside the property
---

## AnimationBindPropertyParameter ( )

Constructor. Creates an empty property parameter binding.
## void setNodes ( Vector < Ptr < Node >> OUT_nodes )

Points the binding at a set of nodes at once, so that one channel drives every one of them.
### Arguments

- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Node](../../../../api/library/nodes/class.node_cpp.md)>>* **OUT_nodes** - Nodes the binding is to point at. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void setAssets ( Vector < UGUID > OUT_file_guids )

Points the binding at a set of assets at once.
### Arguments

- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[UGUID](../../../../api/library/filesystem/class.uguid_cpp.md)>* **OUT_file_guids** - File GUIDs of the assets. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## void setNodePropertyDescription ( const char * name , int index )

Sets which property of the node is animated, by its name and the slot it takes.
### Arguments

- *const char ** **name** - Name of the property on the node.
- *int* **index** - Slot of the property on the node.

## int getNumTargetSurfaceMatches ( int i ) const

Returns how many surfaces the specified target resolves to, which is what tells a surface pattern that found nothing from one that found many.
### Arguments

- *int* **i** - Target number.

### Return value

Number of surfaces the target resolves to.
## Ptr < Node > getTargetResolvedNode ( int i ) const

Returns the node the specified target of the binding resolves to in the loaded scene.
### Arguments

- *int* **i** - Target number.

### Return value

Node the target resolves to, or NULL (null in C#) if it resolves to none.
## Ptr < Property > getTargetResolvedProperty ( int i ) const

Returns the property the specified target of the binding resolves to, that is, the property instance carried by the node the target names. This is the object the animated parameter is written into.
### Arguments

- *int* **i** - Target number.

### Return value

Property the target resolves to, or NULL (null in C#) if it resolves to none.
