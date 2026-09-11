# Unigine::Plugins::Syncker::Master Class (CS)

**Inherits from:** Syncker


This class represents the master interface of the Syncker.


> **Notice:** [Syncker](../../../../code/plugins/syncker/index.md) plugin must be loaded.


## Master Class

### Enums

## CALLBACK_INDEX

Callback types.
| Name | Description |
|---|---|
| **SESSION_STARTED** = 0 | Callback function to be fired on starting a session (all Slaves are connected, MTU is determined). Callback signature: ```text callback_function_name(void) ``` |
| **SESSION_CONTINUED** = | Callback function to be fired on continuing a session. Callback signature: ```text callback_function_name(Vector <long long> slaves_id) ``` |
| **SESSION_FINISHED** = 2 | Callback function to be fired on closing a session. Callback signature: ```text callback_function_name(void) ``` |
| **SLAVE_CONNECTED** = 3 | Callback function to be fired on successful connection of a new Slave. Callback signature: ```text callback_function_name(int slave_num) ``` |
| **SLAVE_DISCONNECTED** = 4 | Callback function to be fired before disconnecting a Slave. The reason for disconnection specified in string format ("disconnected by slave", "timeout", etc.) Callback signature: ```text callback_function_name(int slave_num, const char *reason) ``` |
| **MASTER_SETUP_CHANGED** = 5 | Callback to be fired on changing settings on the Master. Callback signature: ```text void callback_function_name(void); ``` |
| **SLAVE_SETUP_CHANGED** = 6 | Callback to be fired on changing settings on a Slave. Callback signature: ```text void callback_function_name(int slave_num); ``` |

## SYNC_MASK

Node synchronization mask.
| Name | Description |
|---|---|
| **NODE_FLAGS** = 1 | Update only simple node flag (*enabled*, *immovable*, etc.) |
| **TRANSFORM** = 1 << 1 | Update node transform (with interpolation). |
| **BASE** = 3 | Update base information *NODEFLAGS & TRANSFORM*. |
| **DERIVED** = 31 << 3 | Update information of derived class (11111000 - without the first 3 bits). This mask allows synchronizing the node subtype (such as player, light, decal, etc.) parameters. |
| **OBJECT** = 1 << 3 | Update object parameters. All other parameters of objects except for *NODE_FLAGS* and *TRANSFORM* (particles trasform for object particles, bones transform for object skinned) |
| **OBJECT_SURFACE** = 1 << 4 | Update all parameters of surfaces (surface flags and information about inherited materials for each surface). |

## DEFAULT_SYNC_NODES

Types of nodes that will be synchronized automatically after world loading.
| Name | Description |
|---|---|
| **LIGHT_WORLD** = 1 | World light. See the [LightWorld](../../../../api/library/lights/class.lightworld_cs.md) class. |
| **WATER_GLOBAL** = 1 << 1 | Global water. See the [ObjectWaterGlobal](../../../../api/library/objects/class.objectwaterglobal_cs.md) class. |
| **CLOUD_LAYER** = 1 << 2 | Cloud layer. See the [ObjectCloudLayer](../../../../api/library/objects/class.objectcloudlayer_cs.md) class. |
| **OBJECT_PARTICLES** = 1 << 3 | Particle system. See the [ObjectParticles](../../../../api/library/objects/class.objectparticles_cs.md) class. |

### Properties

## 🔒︎ int NumSyncMaterials

The total number of materials in the synchronization queue.
## 🔒︎ int NumSyncNodes

The total number of nodes in the synchronization queue.
## byte DefaultSyncNodes

The mask defining types of nodes that will be synchronized automatically after world loading. This mask can be used for optimization reasons limiting the number of nodes to be synchronized and thus reducing network load. For example, you can restrict automatic synchronization to global water, and clouds only:
```csharp
master.SetDefaultSyncNodes(Unigine.Plugins.Syncker.Master.DEFAULT_SYNC_NODES.WATER_GLOBAL | Unigine.Plugins.Syncker.Master.DEFAULT_SYNC_NODES.CLOUD_LAYER);
```


## bool SyncWorldLoad

The value indicating whether synchronization of world loading via the UDP protocol is enabled.
## bool SyncRender

The A value indicating if synchronization of all render parameters via the UDP protocol (light scattering, occlusion, etc.) is enabled.
> **Notice:** When all slaves use the same rendering settings, synchronization of render parameters can be disabled.


## bool SyncViewOffset

The value indicating whether synchronization of view offset for projections is enabled.
## bool SyncPlayer

The value indicating whether synchronization of the current player's parameters via the UDP protocol is enabled.
The following parameters are synchronized:


- Its transformation
- Projection matrix
- Viewport mask
- Mask for reflections
- Applied post-materials (if any)


> **Notice:** Current player synchronization is used only when all slaves use the same camera.


## 🔒︎ int NumSlaves

The total number of the slaves connected to the master.
## bool AllowExtraSlaves

The value indicating whether new Slaves can connect to the Master after starting the session. This can be used, for example, to connect a Slave which is used as a tool for configuring projections and does not operate as an IG.
## float SendRate

The
frequency of sending packets to Slaves. Use this method when network load is too high and slows down the whole IG system. It is recommended to use this method with [interpolation](../../../../api/library/plugins/syncker/class.syncker_syncker_cs.md#setInterpolation_int_void) enabled.


```cpp
//On the Master
master->setSendRate(15.0f); // send packets 15 times per second

//Both on the Master and all Slaves
syncker->setInterpolationPeriod(0.1f); // 100 ms delay

```


### Members

---

## string GetSlaveAddress ( int num )

Returns the network address of the given slave computer.
### Arguments

- *int* **num** - Slave number.

### Return value

Network address of the slave computer.
## int GetSlavePort ( int num )

Returns the UDP port used by the slave with the specified number.
### Arguments

- *int* **num** - Slave number.

### Return value

UDP port of the specified slave computer. 0 - means any unused port available.
## long GetSlaveID ( int num )

Returns the ID of the slave with the specified number. A unique Slave ID consists of two parts: IP (32 bits) + port (16 bits)
### Arguments

- *int* **num** - Slave number.

### Return value

ID of the slave with the specified number.
## string GetSlaveWorldName ( int num )

Returns the name of the world file currently loaded on the specified slave.
### Arguments

- *int* **num** - Slave number.

### Return value

Name of the world file currently loaded on the specified slave.
## void AddSyncNode ( Node node , byte sync_mask = SYNC_MASK::NODE_FLAGS | SYNC_MASK::TRANSFORM )


Enables synchronization of parameters of the given node via the UDP protocol.


> **Notice:** Scene nodes are not synchronized by default, this method is used to add a particular node to the synchronization queue.


### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node** - Node to synchronize.
- *byte* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values. By default, only node transformation is synchronized. To sync other parameters, select the corresponding mask.

## void AddSyncNodes ( Node [] nodes , byte sync_mask = SYNC_MASK::NODE_FLAGS | SYNC_MASK::TRANSFORM )


Enables synchronization of parameters of given nodes via the UDP protocol.


> **Notice:** Scene nodes are not synchronized by default, this method is used to add particular nodes to the synchronization queue.


### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)[]* **nodes** - List of nodes to synchronize.
- *byte* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values. By default, only node transformation is synchronized. To sync other parameters, select the corresponding mask.

## void SetSyncNodeMask ( Node node , byte sync_mask )

Sets a new synchronization mask for the specified node. Synchronization mask can be used for optimization reasons limiting the amount of data to be synchronized and thus reducing network load. For example, for moving parts of a helicopter we can set a mask to synchronize only node transformations:
```csharp
master.SetSyncNodeMask(fan_small, Unigine.Plugins.Syncker.Master.SYNC_MASK.TRANSFORM);
master.SetSyncNodeMask(fan_big, Unigine.Plugins.Syncker.Master.SYNC_MASK.TRANSFORM);

```


### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node** - Node for which a new synchronization mask is to be set.
- *byte* **sync_mask** - New synchronization mask to be set for the specified node, one of the [SYNC_MASK](#SYNC_MASK) values.

## bool IsSyncNode ( Node node )

Returns a value indicating if synchronization of the given node is enabled. Using this method you can quickly check if a node is monitored by the Syncker (node's states are dispatched to Slaves over the network).
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node** - Node to be checked.

### Return value

true if synchronization of the given node is enabled; otherwise, false.
## Node GetSyncNode ( int num )

Returns the synchronized node with the given number.
### Arguments

- *int* **num** - Node number in the synchronization queue.

### Return value

Synchronized node.
## void RemoveSyncNode ( int num )

Removes the specified node from the synchronization queue.
### Arguments

- *int* **num** - Node number in the synchronization queue.

## void RemoveSyncNode ( Node node )

Removes the specified node from the synchronization queue.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node** - Node to be removed from synchronization.

## void RemoveSyncNodeID ( int node_id )

Removes the specified node from the synchronization queue by its ID.
### Arguments

- *int* **node_id** - ID of the node to be removed from the synchronization queue.

## void RemoveSyncNodes ( Node [] nodes )

Removes the specified nodes from the synchronization queue.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)[]* **nodes** - List of nodes to be removed from the synchronization queue.

## void ClearSyncNodes ( )

Removes all nodes from the synchronization queue.
## void AddSyncMaterial ( Material material )


Enables synchronization of the given material via the UDP protocol.


> **Notice:** Scene materials are not synchronized by default, this method is used to add a particular material to the synchronization queue.


### Arguments

- *[Material](../../../../api/library/rendering/class.material_cs.md)* **material** - Material to synchronize.

## void AddSyncMaterials ( Material [] materials )


Enables synchronization of given materials via the UDP protocol.


> **Notice:** Scene materials are not synchronized by default, this method is used to add particular materials to the synchronization queue.


### Arguments

- *[Material](../../../../api/library/rendering/class.material_cs.md)[]* **materials** - List of materials to synchronize.

## bool IsSyncMaterial ( Material mat )

Returns a value indicating if synchronization of the given material is enabled. Using this method you can quickly check if a material is monitored by the Syncker (material's states are dispatched to Slaves over the network).
### Arguments

- *[Material](../../../../api/library/rendering/class.material_cs.md)* **mat** - Material to be checked.

### Return value

true if synchronization of the given material is enabled; otherwise, false.
## Material GetSyncMaterial ( int num )

Returns the synchronized material with the given number.
### Arguments

- *int* **num** - Material number in the synchronization queue.

### Return value

Synchronized material.
## void RemoveSyncMaterial ( int num )

Removes the material with the given number from the synchronization queue.
### Arguments

- *int* **num** - Material number in the synchronization queue.

## void RemoveSyncMaterial ( Material material )

Removes the specified material from the synchronization queue.
### Arguments

- *[Material](../../../../api/library/rendering/class.material_cs.md)* **material** - Material to be removed from the synchronization queue.

## void RemoveSyncMaterials ( Material [] materials )

Removes the specified materials from the synchronization queue.
### Arguments

- *[Material](../../../../api/library/rendering/class.material_cs.md)[]* **materials** - List of materials to be removed from the synchronization queue.

## void ClearSyncMaterials ( )

Removes all materials from the synchronization queue.
## bool CreateNode ( Node node , byte sync_mask = 0 )


Synchronizes creation of the given node on all Slaves. This method is **to be called after node creation on the Master**.


> **Notice:** It is recommended to use the [*loadNode()*](#loadNode_cstr_uchar_Mat4_Node) or [*loadNodereference()*](#loadNodeReference_cstr_uchar_Mat4_NodeReference) methods whenever possible as this approach **allows adding nodes of all types**, unlike the [*createNode()*](#createNode_Node_uchar_bool) method that supports only a limited number of them.

 **Example:**
```csharp
Node node = new NodeDummy();
master.CreateNode(node);

```


### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node** - Node to create.
- *byte* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.

### Return value

true if the node was created successfully; otherwise, false.
## void DeleteNode ( Node node )

Synchronizes deletion of the given node (with all its children) on the Master and all Slaves. Similar to calling *deleteLater()* for the node.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node** - Node to delete.

## bool IsNodeCreatedBySyncker ( Node node )

Returns a value indicating if the given node was created via the [*createNode()*](#createNode_Node_uchar_bool) method. Using this method you can quickly check if a node is in the run-time objects creation buffer.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node** - Node to be checked.

### Return value

true if the given node was created via the [*createNode()*](#createNode_Node_uchar_bool) method; otherwise, false.
## void SetCustomPlayer ( string name , Player player )


Sets the specified player for the view, view group, or computer with the specified name.


> **Notice:** Synchronization of the [main master camera](../../../../code/plugins/syncker/index.md#main_camera) is disabled.


### Arguments

- *string* **name** - Name of a view, a view group, or a computer to set the custom player for. > **Notice:** The specified name will be checked in the following order: *view, view group, computer*. The specified player will be set for the first element found.
- *[Player](../../../../api/library/players/class.player_cs.md)* **player** - Player to be set.

## void SetViewOffset ( vec3 offset )

Sets a new player's head position on the Master.
### Arguments

- *vec3* **offset** - New player's head position coordinates to be set.

## void LoadWorld ( string name )

Loads a world from the specified file on the Master and all Slaves. Syncker is able to automatically synchronize the current world, but it works as follows: Slaves shall only start loading a new world after it is completely loaded on the Master. This method provides a 2x speedup of world loading process, as it forces all hosts to start loading the world almost simultaneously.
### Arguments

- *string* **name** - Path to the `*.world` file to be loaded.

## Node LoadNode ( string path , byte sync_mask = 0 , mat4 init_transform )

Loads a node from the specified file to the world on the Master and all Slaves and places it to the specified ititial transformation. This is a network analogue of the *[loadNode()](../../../../api/library/engine/class.world_cs.md#loadNode_cstr_int_Node)* method of the *World* class. By default, the loaded node is not synchronized, which is suitable for static objects at run time and at the same time saves performance. For dynamic objects to be synchronized, the suitable synchronization mask should be set.
### Arguments

- *string* **path** - Path to the `*.node` file.
- *byte* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.
- *mat4* **init_transform** - Initial transformation of the node.

### Return value

Loaded node or nullptr if an error has occurred.
## Node LoadNode ( string path , byte sync_mask = 0 )

Loads a node from the specified file to the world on the Master and all Slaves and places it at the origin with the default transformation. This is a network analogue of the *[loadNode()](../../../../api/library/engine/class.world_cs.md#loadNode_cstr_int_Node)* method of the *World* class. By default, the loaded node is not synchronized, which is suitable for static objects at run time and at the same time saves performance. For dynamic objects to be synchronized, the suitable synchronization mask should be set.
### Arguments

- *string* **path** - Path to the `*.node` file.
- *byte* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.

### Return value

Loaded node or nullptr if an error has occurred.
## NodeReference LoadNodeReference ( string path , byte sync_mask = 0 , mat4 init_transform )

Loads a node reference from the specified file to the world on the Master and all Slaves and places it to the specified ititial transformation. This is a network analogue of the [NodeReference class constructor](../../../../api/library/nodes/class.nodereference_cs.md#NodeReference_constchar). By default, the loaded node is not synchronized, which is suitable for static objects at run time and at the same time saves performance. For dynamic objects to be synchronized, the suitable synchronization mask should be set.
### Arguments

- *string* **path** - Path to the `*.node` file.
- *byte* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.
- *mat4* **init_transform** - Initial transformation of the node.

### Return value

Node Reference instance if it was loaded successfully; otherwise nullptr.
## NodeReference LoadNodeReference ( string path , byte sync_mask = 0 )

Loads a node reference from the specified file to the world on the Master and all Slaves and places it to the origin with default transformation. This is a network analogue of the [NodeReference class constructor](../../../../api/library/nodes/class.nodereference_cs.md#NodeReference_constchar). By default, the loaded node is not synchronized, which is suitable for static objects at run time and at the same time saves performance. For dynamic objects to be synchronized, the suitable synchronization mask should be set.
### Arguments

- *string* **path** - Path to the `*.node` file.
- *byte* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.

### Return value

Node Reference instance if it was loaded successfully; otherwise nullptr.
## bool IsNodeLoadedBySyncker ( Node node )

Returns a value indicating if the given node was loaded by the Syncker via the [*loadNode()*](#loadNode_cstr_uchar_Mat4_Node) or the [*loadNodeReference()*](#loadNodeReference_cstr_uchar_Mat4_NodeReference) method.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node** - Node to be checked.

### Return value

true if the given node was created via the [*createNode()*](#createNode_Node_uchar_bool) method; otherwise, false.
## IntPtr addCallback ( Master.CALLBACK_INDEX callback , CallbackDelegate func )

Adds a callback of the specified type. Callback functions can be used to determine actions to be performed when sending or receiving user messages, as well as when changing settings on the Master or a Slave. The signature of the callback function can be one of the following:
```csharp
// for the Syncker.Master.SESSION_STARTED type
void callback_function_name(void);

// for the Syncker.Master.SESSION_FINISHED type
void callback_function_name(void);

// for the Syncker.Master.SLAVE_CONNECTED type
void callback_function_name(int slave_num);

// for the Syncker.Master.SLAVE_DISCONNECTED type
void callback_function_name(int slave_num);

// for the Syncker.Master.MASTER_SETUP_CHANGED type
void callback_function_name(void);

// for the Syncker.Master.SLAVE_SETUP_CHANGED type
void callback_function_name(int slave_num);

```


### Arguments

- *Master.CALLBACK_INDEX* **callback** - Callback type. One of the following values:

  - [SESSION_STARTED](#SESSION_STARTED)
  - [SESSION_CONTINUED](#SESSION_CONTINUED)
  - [SESSION_FINISHED](#SESSION_FINISHED)
  - [SLAVE_CONNECTED](#SLAVE_CONNECTED)
  - [SLAVE_DISCONNECTED](#SLAVE_DISCONNECTED)
  - [MASTER_SETUP_CHANGED](#MASTER_SETUP_CHANGED)
  - [SLAVE_SETUP_CHANGED](#SLAVE_SETUP_CHANGED)
- *CallbackDelegate* **func** - Callback function.

### Return value

Number of the last added callback of the specified type, if the callback was added successfully; otherwise, **-1**.
## bool removeCallback ( Master.CALLBACK_INDEX callback )

Removes a given callback from the list of callbacks of the specified type. Callback functions can be used to determine actions to be performed when sending or receiving user messages, as well as when changing settings on the Master or a Slave.
### Arguments

- *Master.CALLBACK_INDEX* **callback** - Callback type. One of the following values:

  - [SESSION_STARTED](#SESSION_STARTED)
  - [SESSION_CONTINUED](#SESSION_CONTINUED)
  - [SESSION_FINISHED](#SESSION_FINISHED)
  - [SLAVE_CONNECTED](#SLAVE_CONNECTED)
  - [SLAVE_DISCONNECTED](#SLAVE_DISCONNECTED)
  - [MASTER_SETUP_CHANGED](#MASTER_SETUP_CHANGED)
  - [SLAVE_SETUP_CHANGED](#SLAVE_SETUP_CHANGED)

### Return value

true if the position callback with the given ID was removed successfully; otherwise false.
## void clearCallbacks ( Master.CALLBACK_INDEX callback )

Clears all added callbacks of the specified type. Callback functions can be used to determine actions to be performed when sending or receiving user messages, as well as when changing settings on the Master or a Slave.
### Arguments

- *Master.CALLBACK_INDEX* **callback** - Callback type. One of the following values:

  - [SESSION_STARTED](#SESSION_STARTED)
  - [SESSION_CONTINUED](#SESSION_CONTINUED)
  - [SESSION_FINISHED](#SESSION_FINISHED)
  - [SLAVE_CONNECTED](#SLAVE_CONNECTED)
  - [SLAVE_DISCONNECTED](#SLAVE_DISCONNECTED)
  - [MASTER_SETUP_CHANGED](#MASTER_SETUP_CHANGED)
  - [SLAVE_SETUP_CHANGED](#SLAVE_SETUP_CHANGED)

## int AddMessageToBuffer ( string channel , Blob message )

Adds a message to the buffer to be received by [additional slaves](#setAllowExtraSlaves_int_void) as soon as they connect.
### Arguments

- *string* **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.
- *[Blob](../../../../api/library/common/class.blob_cs.md)* **message** - Buffer containing the user message.

### Return value

Message ID.
## int GetNumBufferedMessages ( string channel )

Returns the total number of buffered messages.
### Arguments

- *string* **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.

### Return value

Total number of buffered messages.
## int GetBufferedMessageID ( string channel , int index )

Returns the ID of the buffered message by its index.
### Arguments

- *string* **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.
- *int* **index** - Message index number.

### Return value

Message ID.
## Blob GetBufferedMessage ( string channel , int id )

Returns the buffer containing the message.
### Arguments

- *string* **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.
- *int* **id** - Message ID.

### Return value

Buffer containing the user message.
## void RemoveBufferedMessage ( string channel , int id )

Removes the specified message from the buffer.
### Arguments

- *string* **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.
- *int* **id** - Message ID.

## void ClearBufferedMessages ( string channel )

Removes all messages from the buffer.
### Arguments

- *string* **channel** - Channel name. Multiple systems may use Syncker's network simultaneously (e.g. [IG](../../../../ig/index.md) and user's application). For convenience, all messages are sent and received via named channels.

## string GetSlaveComputerName ( int num )

Returns the name of the slave computer with the specified index. If no name has been specified for the slave computer using the `-computer_name` startup argument, the system name is returned.
### Arguments

- *int* **num** - Slave index.

### Return value

Slave computer name.
## Node CloneNode ( Node node , byte sync_mask = 0 )

Clones the specified node and synchronizes its cloning on all Slaves.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node** - Node to clone.
- *byte* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.

### Return value

Cloned node.
## Node CloneNode ( Node node , byte sync_mask , mat4 init_transform )

Clones the specified node with the specified transformation and synchronizes its cloning on all Slaves.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node** - Node to clone.
- *byte* **sync_mask** - Synchronization mask, one of the [SYNC_MASK](#SYNC_MASK) values.
- *mat4* **init_transform** - Cloned node position and rotation (if not specified, the source node transformation is used).

### Return value

Cloned node.
