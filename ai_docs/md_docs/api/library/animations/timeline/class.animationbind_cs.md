# Unigine::AnimationBind Class (CS)


A binding is what points a [channel](../../../../api/library/animations/timeline/class.animationchannel_cs.md) at the object it animates. The channel says which parameter is animated, and the binding says whose parameter it is: a node, a material, a property parameter, a component field or a runtime object. This class is the base of them all, and each kind has a subclass of its own.


A binding holds a list of **targets**. A target either names one object directly or describes a query that is resolved when the sequence is played, such as every node whose name fits a pattern or every node that carries a certain property. Adding several targets makes one curve drive them all, which is what a fan-out is, and direct targets may be mixed with queries in one binding.


The binding authored in the file works as it is. A player can also replace it for one instance only, so the same `*.seq` drives different objects in different players. See the [Targets and Binding](../../../../editor2/tools/sequencer/targets/index.md) and the [Runtime Playback](../../../../editor2/tools/sequencer/runtime/index_cs.md) articles.


## AnimationBind Class

### Enums

## TYPE

Binding type. It tells what kind of object the channel is pointed at.
| Name | Description |
|---|---|
| **ANIMATION_BIND** = 0 | Generic binding. |
| **ANIMATION_BIND_NODE** = 1 | Binding to a node (see the *[AnimationBindNode](../../../../api/library/animations/timeline/class.animationbindnode_cs.md)* class). |
| **ANIMATION_BIND_PROPERTY_PARAMETER** = 2 | Binding to a property parameter (see the *[AnimationBindPropertyParameter](../../../../api/library/animations/timeline/class.animationbindpropertyparameter_cs.md)* class). |
| **ANIMATION_BIND_MATERIAL** = 3 | Binding to a material (see the *[AnimationBindMaterial](../../../../api/library/animations/timeline/class.animationbindmaterial_cs.md)* class). |
| **ANIMATION_BIND_RUNTIME** = 4 | Binding to a runtime object such as a widget or a camera (see the *[AnimationBindRuntime](../../../../api/library/animations/timeline/class.animationbindruntime_cs.md)* class). |
| **ANIMATION_BIND_COMPONENT** = 5 | Binding to a field of a component (see the *[AnimationBindComponent](../../../../api/library/animations/timeline/class.animationbindcomponent_cs.md)* class). |

## NODE_ACCESS

Way a node is looked up in the scene.
| Name | Description |
|---|---|
| **BY_ID** = 0 | The node is looked up by its identifier, which is exact but does not survive a scene rebuilt from scratch. |
| **BY_NAME** = 1 | The node is looked up by its name, which survives a rebuilt scene but picks the first node that carries the name. |
| **INNER_BY_NAME** = 2 | The node sits inside a [Node Reference](../../../../objects/nodes/reference/index.md) and is looked up by its name within it, while the stored identifier names the reference that contains it. |

## ASSET_ACCESS

Way an asset target, such as a material, is looked up.
| Name | Description |
|---|---|
| **BY_GUID** = 0 | The asset is looked up by its GUID, which names one file exactly. |
| **BY_NAME** = 1 | The asset is looked up by its name, which lets the same binding reach a different file of that name, such as a material carried by another project. |

## QUERY_SCOPE

Part of the scene a query target is looked for in.
| Name | Description |
|---|---|
| **ALL_NODES** = 0 | The whole scene is searched. |
| **SUBTREE_NODES** = 1 | Only the branch that grows from the given node is searched. |
| **NODES_FROM_REFERENCE** = 2 | Only the nodes that come from a certain node reference are searched. |
| **ASSET_INHERITANCE** = 3 | Only the assets inherited from a certain one are searched. |

## MATCH_BY

Rule that decides which objects a target resolves to.
| Name | Description |
|---|---|
| **TARGET** = 0 | The target names one object directly, so it resolves to that object and to nothing else. |
| **NAME_PATTERN** = 1 | The target resolves to every node whose name fits the pattern. |
| **PROPERTY** = 2 | The target resolves to every node the given property is assigned to. |
| **COMPONENT** = 3 | The target resolves to every node the given component is assigned to. |
| **NODE_TYPE** = 4 | The target resolves to every node of the given type. |

## NODE_TYPE_GROUP

Family of node types a query target can match.
| Name | Description |
|---|---|
| **OBJECT** = 0 | Objects. |
| **LIGHT** = 1 | Light sources. |
| **DECAL** = 2 | Decals. |
| **WORLD** = 3 | World nodes. |
| **FIELD** = 4 | Fields. |
| **PLAYER** = 5 | Players. |
| **PHYSICAL** = 6 | Physical nodes. |
| **NAVIGATION** = 7 | Navigation nodes. |
| **OBSTACLE** = 8 | Obstacles. |
| **SOUND** = 9 | Sound nodes. |

### Properties

## 🔒︎ AnimationBind.TYPE Type

The binding type.
## 🔒︎ string TypeName

The name of the binding type.
## int NumTargets

The number of targets held by the binding. Several targets make one channel drive them all, which is what a fan-out is.
### Members

---

## int AddTarget ( AnimationBind.MATCH_BY match_by )

Adds a target to the binding. A direct target names one object, while a query target resolves to every object that fits its rule at the moment the sequence is played.
### Arguments

- *[AnimationBind.MATCH_BY](../../../../api/library/animations/timeline/class.animationbind_cs.md#MATCH_BY)* **match_by** - Rule that decides which objects the target resolves to.

### Return value

Number of the new target.
## void RemoveTarget ( int i )

Removes the specified target from the binding.
### Arguments

- *int* **i** - Target number.

## void MoveTarget ( int from , int to )

Moves the specified target to another place in the list.
### Arguments

- *int* **from** - Number of the target to be moved.
- *int* **to** - Number the target is to take.

## void MoveTargets ( int[] OUT_indices , int insert_before )

Moves several targets at once, keeping their order among themselves.
### Arguments

- *int[]* **OUT_indices** - Numbers of the targets to be moved. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *int* **insert_before** - Number of the target the moved ones are put before.

## int DuplicateTarget ( int src )

Copies a target into a new one, carrying over everything it holds: the object or the query it names, the way that object is looked up and the scope it is searched in.
### Arguments

- *int* **src** - Number of the target to be copied.

### Return value

Number of the new target, which is appended after the existing ones, or -1 if the source number is out of range.
## AnimationBind.MATCH_BY GetTargetMatchBy ( int i )

Returns the rule the specified target resolves by.
### Arguments

- *int* **i** - Target number.

### Return value

Rule the target resolves by.
## void SetTargetMatchBy ( int i , AnimationBind.MATCH_BY match_by )

Sets the rule the specified target resolves by.
### Arguments

- *int* **i** - Target number.
- *[AnimationBind.MATCH_BY](../../../../api/library/animations/timeline/class.animationbind_cs.md#MATCH_BY)* **match_by** - Rule the target is to resolve by.

## int GetTargetNodeID ( int i )

Returns the identifier of the node stored for the specified target.
### Arguments

- *int* **i** - Target number.

### Return value

Identifier of the node stored for the target, or -1 if none is stored.
## string GetTargetNodeName ( int i )

Returns the name of the node stored for the specified target.
### Arguments

- *int* **i** - Target number.

### Return value

Name of the node stored for the target.
## int GetTargetRefInnerID ( int i )

Returns the identifier the node has inside the node reference it comes from.
### Arguments

- *int* **i** - Target number.

### Return value

Identifier of the node inside the node reference.
## UGUID GetTargetAssetFileGUID ( int i )

Returns the file GUID of the asset the specified target points at.
### Arguments

- *int* **i** - Target number.

### Return value

GUID of the asset file stored for the target.
## UGUID GetTargetAssetRuntimeGUID ( int i )

Returns the runtime GUID of the asset the specified target points at.
### Arguments

- *int* **i** - Target number.

### Return value

Runtime GUID of the asset stored for the target.
## int GetTargetLiveNodeID ( int i )

Returns the node the specified target resolves to in the scene that is loaded right now.
### Arguments

- *int* **i** - Target number.

### Return value

Identifier of the node the target resolves to in the loaded scene, or -1 if it resolves to none.
## void SetTargetNode ( int i , Node node )

Points the specified target at a node of the loaded scene.
### Arguments

- *int* **i** - Target number.
- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node** - Node the target is to point at.

## void SetTargetNodeDescription ( int i , int id , string name )

Points the specified target at a node by its identifier and name rather than by a live node, which is how a target is stored for a scene that is not loaded yet.
### Arguments

- *int* **i** - Target number.
- *int* **id** - Identifier of the node.
- *string* **name** - Name of the node.

## void SetTargetRefInnerID ( int i , int id )

Sets the identifier the node has inside the node reference it comes from.
### Arguments

- *int* **i** - Target number.
- *int* **id** - Identifier of the node inside the node reference.

## AnimationBind.NODE_ACCESS GetTargetNodeAccess ( int i )

Returns the way the node of the specified target is looked up in the scene.
### Arguments

- *int* **i** - Target number.

### Return value

Way the node of the specified target is looked up in the scene.
## void SetTargetNodeAccess ( int i , AnimationBind.NODE_ACCESS access )

Sets the way the node of the specified target is looked up in the scene: by its identifier, by its name, or by its name inside the node reference that contains it. See [NODE_ACCESS_*](#NODE_ACCESS_BY_ID).
### Arguments

- *int* **i** - Target number.
- *[AnimationBind.NODE_ACCESS](../../../../api/library/animations/timeline/class.animationbind_cs.md#NODE_ACCESS)* **access** - Way the node is to be looked up in the scene.

## void SetTargetAssetFileGUID ( int i , UGUID guid )

Points the specified target at an asset by the GUID of its file.
### Arguments

- *int* **i** - Target number.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **guid** - File GUID of the asset.

## void SetTargetAsset ( int i , UGUID runtime_guid , UGUID file_guid )

Points the specified target at an asset, giving both of the GUIDs it is addressed by.
### Arguments

- *int* **i** - Target number.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **runtime_guid** - Runtime GUID of the asset.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - File GUID of the asset.

## AnimationBind.ASSET_ACCESS GetTargetAssetAccess ( int i )

Returns the way the asset of the specified target is looked up.
### Arguments

- *int* **i** - Target number.

### Return value

Way the asset of the specified target is looked up.
## void SetTargetAssetAccess ( int i , AnimationBind.ASSET_ACCESS access )

Sets the way the asset of the specified target is looked up: by the GUID that names one file exactly, or by the name, which lets the binding reach a file of that name in another project.
### Arguments

- *int* **i** - Target number.
- *[AnimationBind.ASSET_ACCESS](../../../../api/library/animations/timeline/class.animationbind_cs.md#ASSET_ACCESS)* **access** - Way the asset is to be looked up.

## string GetTargetAssetName ( int i )

Returns the name the asset of the specified target is looked up by. It is what the target is addressed with while its access is set to name rather than GUID.
### Arguments

- *int* **i** - Target number.

### Return value

Name the asset of the specified target is looked up by.
## void SetTargetAssetName ( int i , string name )

Sets the name the asset of the specified target is looked up by.
### Arguments

- *int* **i** - Target number.
- *string* **name** - Name the asset is to be looked up by.

## AnimationBind.QUERY_SCOPE GetTargetScope ( int i )

Returns the part of the scene the specified query target is looked for in.
### Arguments

- *int* **i** - Target number.

### Return value

Part of the scene the target is looked for in.
## void SetTargetScope ( int i , AnimationBind.QUERY_SCOPE scope )

Narrows the specified query target to a part of the scene.
### Arguments

- *int* **i** - Target number.
- *[AnimationBind.QUERY_SCOPE](../../../../api/library/animations/timeline/class.animationbind_cs.md#QUERY_SCOPE)* **scope** - Part of the scene the target is to be looked for in.

## void SetTargetSubtreeRoot ( int i , int id , string name )

Sets the node whose branch the specified query target is limited to.
### Arguments

- *int* **i** - Target number.
- *int* **id** - Identifier of the node the branch grows from.
- *string* **name** - Name of the node the branch grows from.

## int GetTargetSubtreeRootID ( int i )

Returns the identifier of the node whose branch the specified query target is limited to.
### Arguments

- *int* **i** - Target number.

### Return value

Identifier of the node the branch grows from.
## string GetTargetSubtreeRootName ( int i )

Returns the name of the node whose branch the specified query target is limited to.
### Arguments

- *int* **i** - Target number.

### Return value

Name of the node the branch grows from.
## AnimationBind.NODE_ACCESS GetTargetSubtreeRootAccess ( int i )

Returns the way the node whose branch the target is limited to is looked up in the scene.
### Arguments

- *int* **i** - Target number.

### Return value

Way the node of the branch is looked up.
## void SetTargetSubtreeRootAccess ( int i , AnimationBind.NODE_ACCESS access )

Sets the way the node whose branch the target is limited to is looked up in the scene.
### Arguments

- *int* **i** - Target number.
- *[AnimationBind.NODE_ACCESS](../../../../api/library/animations/timeline/class.animationbind_cs.md#NODE_ACCESS)* **access** - Way the node of the branch is to be looked up.

## int GetTargetSubtreeRootLiveNodeID ( int i )

Returns the node the branch of the specified target grows from in the scene that is loaded right now.
### Arguments

- *int* **i** - Target number.

### Return value

Identifier of the node in the loaded scene, or -1 if it resolves to none.
## UGUID GetTargetNodeReferenceGUID ( int i )

Returns the node reference the nodes of the specified query target come from.
### Arguments

- *int* **i** - Target number.

### Return value

GUID of the node reference the nodes come from.
## void SetTargetNodeReferenceGUID ( int i , UGUID guid )

Sets the node reference the nodes of the specified query target come from.
### Arguments

- *int* **i** - Target number.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the node reference the nodes come from.

## UGUID GetTargetInheritRootGUID ( int i )

Returns the asset the assets matched by the specified query target inherit from.
### Arguments

- *int* **i** - Target number.

### Return value

GUID of the asset the matched ones inherit from.
## void SetTargetInheritRootGUID ( int i , UGUID guid )

Sets the asset the assets matched by the specified query target inherit from.
### Arguments

- *int* **i** - Target number.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the asset the matched ones inherit from.

## UGUID GetTargetPropertyGUID ( int i )

Returns the property the nodes matched by the specified query target carry.
### Arguments

- *int* **i** - Target number.

### Return value

GUID of the property the nodes carry.
## void SetTargetPropertyGUID ( int i , UGUID guid )

Sets the property the nodes matched by the specified query target carry.
### Arguments

- *int* **i** - Target number.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the property the nodes carry.

## UGUID GetTargetComponentGUID ( int i )

Returns the component the nodes matched by the specified query target carry.
### Arguments

- *int* **i** - Target number.

### Return value

GUID of the component the nodes carry.
## void SetTargetComponentGUID ( int i , UGUID guid )

Sets the component the nodes matched by the specified query target carry.
### Arguments

- *int* **i** - Target number.
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **guid** - GUID of the component the nodes carry.

## string GetTargetNamePattern ( int i )

Returns the pattern the node names are matched against by the specified query target.
### Arguments

- *int* **i** - Target number.

### Return value

Pattern the node names are matched against.
## void SetTargetNamePattern ( int i , string pattern )

Sets the pattern the node names are matched against by the specified query target, so that one channel drives every node whose name fits it.
### Arguments

- *int* **i** - Target number.
- *string* **pattern** - Pattern the node names are to be matched against.

## int GetTargetNodeType ( int i )

Returns the node type the specified query target matches.
### Arguments

- *int* **i** - Target number.

### Return value

Type of the nodes the target matches.
## void SetTargetNodeType ( int i , int type )

Sets the node type the specified query target matches.
### Arguments

- *int* **i** - Target number.
- *int* **type** - Type of the nodes to be matched.

## bool IsTargetNodeTypeIsGroup ( int i )

Returns a value indicating if the specified query target matches a whole family of node types rather than a single type.
### Arguments

- *int* **i** - Target number.

### Return value

true if the target matches a whole family of node types; otherwise, false.
## void SetTargetNodeTypeIsGroup ( int i , bool v )

Sets whether the specified query target matches a whole family of node types.
### Arguments

- *int* **i** - Target number.
- *bool* **v** - true to match a whole family of node types, false to match a single type.

## int GetNumTargetMatches ( int i )

Returns how many objects the specified target resolves to in the scene that is loaded right now, which is what tells a query that found nothing from one that found many.
### Arguments

- *int* **i** - Target number.

### Return value

Number of objects the target resolves to.
## string GetTargetMatchName ( int i , int j )

Returns the name of an object the specified target resolves to.
### Arguments

- *int* **i** - Target number.
- *int* **j** - Number of the match.

### Return value

Name of the matched object.
## int GetNumTargetInheritanceMatches ( int i )

Returns how many assets the specified target resolves to through inheritance.
### Arguments

- *int* **i** - Target number.

### Return value

Number of assets that inherit from the given one.
## int GetResolvedNodeID ( int i = 0 )

Returns the node the specified target resolves to.
### Arguments

- *int* **i** - Target number. The default value is 0.

### Return value

Identifier of the node the target resolves to, or -1 if it resolves to none.
## UGUID GetResolvedAssetGUID ( int i = 0 )

Returns the asset the specified target resolves to.
### Arguments

- *int* **i** - Target number. The default value is 0.

### Return value

GUID of the asset the target resolves to.
## void Save ( Blob blob )

Saves the binding to a blob.
### Arguments

- *[Blob](../../../../api/library/common/class.blob_cs.md)* **blob** - Blob to save the binding to.

## void Load ( Blob blob )

Loads the binding from a blob, replacing everything it currently holds.
### Arguments

- *[Blob](../../../../api/library/common/class.blob_cs.md)* **blob** - Blob to load the binding from.
