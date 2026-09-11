# Unigine::Plugins::Syncker::Slave Class (CS)


This class represents the slave interface of the Syncker.


> **Notice:** [Syncker](../../../../code/plugins/syncker/index.md) plugin must be loaded.


## Slave Class

### Enums

## CALLBACK_INDEX

| Name | Description |
|---|---|
| **SESSION_STARTED** = 0 | Callback function to be fired on starting a session. Callback signature: ```text callback_function_name(void) ``` |
| **SESSION_FINISHED** = 1 | Callback function to be fired on closing a session. Callback signature: ```text callback_function_name(void) ``` |
| **MASTER_CONNECTED** = 2 | Callback function to be fired on successful connection to the Master. Callback signature: ```text callback_function_name(void) ``` |
| **MASTER_DISCONNECTED** = 3 | Callback function to be fired on disconnecting from the Master. The reason for disconnection specified in string format ("disconnected by master", "timeout", etc.) Callback signature: ```text callback_function_name(const char *reason) ``` |
| **NODE_LOADED** = 4 | Callback function to be fired on creating a node by the Master on the Slave via *loadNode() / loadNodeReference() / createNode()*. Callback signature: ```text callback_function_name(const NodePtr &node) ``` |
| **NODE_CLONED** = 5 | Callback function to be fired on cloning a node by the Master on the Slave via *cloneNode()*. Callback signature: ```text callback_function_name(const NodePtr &node) ``` |

## SKIP_FLAGS

Flags defining data from the Master to be ignored by the Slave.
| Name | Description |
|---|---|
| **WORLD_LOAD** = 1 | Loading worlds. |
| **GAME** = 1 << 1 | Game class (time and speed), for particles � ifps and seed. |
| **PLAYER** = 1 << 2 | Current Master camera synchronization (every frame). |
| **RENDER** = 1 << 3 | Render and post-effects settings. |
| **NODES** = 1 << 4 | Nodes. |
| **MATERIALS** = 1 << 5 | Materials. |
| **SET_PLAYER** = 1 << 6 | Ignoring *[setCustomPlayer()](../../../../api/library/plugins/syncker/class.syncker_master_cs.md#setCustomPlayer_cstr_Player_void)* calls by the Master. |
| **VIEW_OFFSET** = 1 << 7 | Changing view offset parameters. |
| **USER_DATA** = 1 << 8 | Processing user packets sent via [*sendMessage()*](../../../../api/library/plugins/syncker/class.syncker_syncker_cs.md#sendMessage_cstr_Blob_int_bool). |
| **NODE_LOAD** = 1 << 9 | Loading nodes from `*.node` files. |
| **NODEREF_LOAD** = 1 << 10 | Loading node references from `*.node` files. |
| **NODE_CREATE** = 1 << 11 | Node creation. |
| **NODE_ID_REGISTER** = 1 << 12 | Links between dynamic nodes of the Master and Slaves (via ID) created via *loadNode()*, *createNode()*, etc. |
| **NODE_DELETE** = 1 << 13 | Node removal. |
| **RUN_CONSOLE** = 1 << 14 | Running console commands. |
| **PROJECTIONS** = 1 << 15 | Projections configuration. |
| **NODE_CLONE** = 1 << 16 | Node cloning. |

### Properties

## int SkipFlags

The [skip flags](#SKIP_FLAGS) enabling you to ignore certain information from the Master.
## 🔒︎ long ID

The ID of the Slave.
### Members

---

## int GetMasterNodeID ( int slave_node_id )

Returns the ID of a dynamic node on the Master by its local ID on the Slave. A Slave does not create an exact copy of a node created on the Master, their IDs do not match. So, knowing an ID of a local copy of a node created on the Master, you can easily find its original on the Master. This can be used in [user messages](../../../../api/library/plugins/syncker/class.syncker_syncker_cs.md#sendMessage_cstr_Blob_int_bool), when you need to apply some specific modifications to source node on the Master.
### Arguments

- *int* **slave_node_id** - Node's ID on the Slave.

### Return value

ID of the node on the Master.
## int GetSlaveNodeID ( int master_node_id )

Returns the local ID of a dynamic node on the Slave by its ID on the Master. A Slave does not create an exact copy of a node created on the Master, their IDs do not match. So, if you created a node on the Master and then called the [*Syncker::Master::createNode()*](../../../../api/library/plugins/syncker/class.syncker_master_cs.md#createNode_Node_uchar_bool) method, you can easily find its copy on the current Slave. This can be used in [user messages](../../../../api/library/plugins/syncker/class.syncker_syncker_cs.md#sendMessage_cstr_Blob_int_bool), when you need to apply some specific modifications to a Slave's copy of a node, that was created on the Master.
### Arguments

- *int* **master_node_id** - Node's ID on the Master.

### Return value

ID of the node on the Slave.
## void AddSyncNode ( Node node , int master_node_id )


Enables synchronization of parameters of the given node via the UDP protocol.


> **Notice:** Scene nodes are not synchronized by default, this method is used to add a particular node to the synchronization queue.


### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node** - Node to synchronize.
- *int* **master_node_id** - ID of the node on the Master.

## void AddSyncNodeID ( int slave_node_id , int master_node_id )


Enables synchronization of parameters of the given node via the UDP protocol.


> **Notice:** Scene nodes are not synchronized by default, this method is used to add a particular node (by its id) to the synchronization queue.


### Arguments

- *int* **slave_node_id** - ID of the node on the Slave.
- *int* **master_node_id** - ID of the node on the Master.

## bool RemoveSyncNode ( Node node )

Removes the specified node from the synchronization queue.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_cs.md)* **node** - Node to be removed.

### Return value

true if the node was successfully removed from the synchronization queue; otherwise, false.
## bool RemoveSyncNodeID ( int slave_node_id )

Removes the node with the given number from the synchronization queue.
### Arguments

- *int* **slave_node_id** - Node number in the synchronization queue.

### Return value

true if the node was successfully removed from the synchronization queue; otherwise, false.
## IntPtr addCallback ( Slave.CALLBACK_INDEX callback , CallbackDelegate func )

Adds a callback of the specified type. Callback functions can be used to determine actions to be performed when sending or receiving user messages, as well as when changing settings on the Master or a Slave. The signature of the callback function can be one of the following:
```csharp
// for the Syncker.Slave.SESSION_STARTED type
void callback_function_name(void);

// for the Syncker.Slave.SESSION_FINISHED type
void callback_function_name(void);

// for the Syncker.Slave.MASTER_CONNECTED type
void callback_function_name(void);

// for the Syncker.Slave.MASTER_DISCONNECTED type
void callback_function_name(string reason);

// for the Syncker.Slave.NODE_LOADED type
void callback_function_name(Node node);

// for the Syncker.Slave.NODE_CLONED type
void callback_function_name(Node node);

```


### Arguments

- *Slave.CALLBACK_INDEX* **callback** - Callback type. One of the following values:

  - [SESSION_STARTED](#SESSION_STARTED)
  - [SESSION_FINISHED](#SESSION_FINISHED)
  - [MASTER_CONNECTED](#MASTER_CONNECTED)
  - [MASTER_DISCONNECTED](#MASTER_DISCONNECTED)
  - [NODE_LOADED](#NODE_LOADED)
  - [NODE_CLONED](#NODE_CLONED)
- *CallbackDelegate* **func** - Callback function.

### Return value

Number of the last added callback of the specified type, if the callback was added successfully; otherwise, **-1**.
## bool removeCallback ( Slave.CALLBACK_INDEX callback )

Removes a given callback from the list of callbacks of the specified type. Callback functions can be used to determine actions to be performed when sending or receiving user messages, as well as when changing settings on the Master or a Slave.
### Arguments

- *Slave.CALLBACK_INDEX* **callback** - Callback type. One of the following values:

  - [SESSION_STARTED](#SESSION_STARTED)
  - [SESSION_FINISHED](#SESSION_FINISHED)
  - [MASTER_CONNECTED](#MASTER_CONNECTED)
  - [MASTER_DISCONNECTED](#MASTER_DISCONNECTED)
  - [NODE_LOADED](#NODE_LOADED)
  - [NODE_CLONED](#NODE_CLONED)

### Return value

true if the position callback with the given ID was removed successfully; otherwise false.
## void clearCallbacks ( Slave.CALLBACK_INDEX callback )

Clears all added callbacks of the specified type. Callback functions can be used to determine actions to be performed when sending or receiving user messages, as well as when changing settings on the Master or a Slave.
### Arguments

- *Slave.CALLBACK_INDEX* **callback** - Callback type. One of the following values:

  - [SESSION_STARTED](#SESSION_STARTED)
  - [SESSION_FINISHED](#SESSION_FINISHED)
  - [MASTER_CONNECTED](#MASTER_CONNECTED)
  - [MASTER_DISCONNECTED](#MASTER_DISCONNECTED)
  - [NODE_LOADED](#NODE_LOADED)
  - [NODE_CLONED](#NODE_CLONED)

## void Reconnect ( )

Allows the disconnected slave computer reconnect to the master computer.


> **Notice:** To ensure the correct operation of this method, [SetAllowExtraSlaves](../../../../api/library/plugins/syncker/class.syncker_master_cs.md#setAllowExtraSlaves_int_void) should be set to false.
