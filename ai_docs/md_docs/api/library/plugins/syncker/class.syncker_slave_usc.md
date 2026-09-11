# Unigine::Plugins::Syncker::Slave Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class represents the slave interface of the Syncker.


> **Notice:** [Syncker](../../../../code/plugins/syncker/index.md) plugin must be loaded.


## Slave Class

### Members

## void setSkipFlags ( int flags )

Sets a new [skip flags](#SKIP_FLAGS) enabling you to ignore certain information from the Master.
### Arguments

- *int* **flags** - The combination of [skip flags](#SKIP_FLAGS) to be used, for example: ```cpp slave.setSkipFlags(SLAVE_GAME | SLAVE_WORLD_LOAD | SLAVE_USER_DATA); ```

## int getSkipFlags () const

Returns the current [skip flags](#SKIP_FLAGS) enabling you to ignore certain information from the Master.
### Return value

Current combination of [skip flags](#SKIP_FLAGS) to be used, for example:
```cpp
slave.setSkipFlags(SLAVE_GAME | SLAVE_WORLD_LOAD | SLAVE_USER_DATA);
```

## long getID () const

Returns the current ID of the Slave.
### Return value

Current ID of the Slave combined as follows: IP address (32 bits) + port number (16 bits).
---

## int getMasterNodeID ( int slave_node_id )

Returns the ID of a dynamic node on the Master by its local ID on the Slave. A Slave does not create an exact copy of a node created on the Master, their IDs do not match. So, knowing an ID of a local copy of a node created on the Master, you can easily find its original on the Master. This can be used in [user messages](../../../../api/library/plugins/syncker/class.syncker_syncker_usc.md#sendMessage_cstr_Blob_int_bool), when you need to apply some specific modifications to source node on the Master.
### Arguments

- *int* **slave_node_id** - Node's ID on the Slave.

### Return value

ID of the node on the Master.
## int getSlaveNodeID ( int master_node_id )

Returns the local ID of a dynamic node on the Slave by its ID on the Master. A Slave does not create an exact copy of a node created on the Master, their IDs do not match. So, if you created a node on the Master and then called the [*Syncker::Master::createNode()*](../../../../api/library/plugins/syncker/class.syncker_master_usc.md#createNode_Node_uchar_bool) method, you can easily find its copy on the current Slave. This can be used in [user messages](../../../../api/library/plugins/syncker/class.syncker_syncker_usc.md#sendMessage_cstr_Blob_int_bool), when you need to apply some specific modifications to a Slave's copy of a node, that was created on the Master.
### Arguments

- *int* **master_node_id** - Node's ID on the Master.

### Return value

ID of the node on the Slave.
## void addSyncNode ( Node node , int master_node_id )


Enables synchronization of parameters of the given node via the UDP protocol.


> **Notice:** Scene nodes are not synchronized by default, this method is used to add a particular node to the synchronization queue.


### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to synchronize.
- *int* **master_node_id** - ID of the node on the Master.

## void addSyncNodeID ( int slave_node_id , int master_node_id )


Enables synchronization of parameters of the given node via the UDP protocol.


> **Notice:** Scene nodes are not synchronized by default, this method is used to add a particular node (by its id) to the synchronization queue.


### Arguments

- *int* **slave_node_id** - ID of the node on the Slave.
- *int* **master_node_id** - ID of the node on the Master.

## bool removeSyncNode ( Node node )

Removes the specified node from the synchronization queue.
### Arguments

- *[Node](../../../../api/library/nodes/class.node_usc.md)* **node** - Node to be removed.

### Return value

true if the node was successfully removed from the synchronization queue; otherwise, false.
## bool removeSyncNodeID ( int slave_node_id )

Removes the node with the given number from the synchronization queue.
### Arguments

- *int* **slave_node_id** - Node number in the synchronization queue.

### Return value

true if the node was successfully removed from the synchronization queue; otherwise, false.
## Variable addCallback ( int callback , Variable func )

Adds a callback of the specified type. Callback functions can be used to determine actions to be performed when sending or receiving user messages, as well as when changing settings on the Master or a Slave. The signature of the callback function can be one of the following:
```cpp
// for the Syncker.Slave.SESSION_STARTED type
void callback_function_name(void);

// for the Syncker.Slave::SESSION_FINISHED type
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

- *int* **callback** - Callback type. One of the following values:

  - [SESSION_STARTED](#SESSION_STARTED)
  - [SESSION_FINISHED](#SESSION_FINISHED)
  - [MASTER_CONNECTED](#MASTER_CONNECTED)
  - [MASTER_DISCONNECTED](#MASTER_DISCONNECTED)
  - [NODE_LOADED](#NODE_LOADED)
  - [NODE_CLONED](#NODE_CLONED)
- *Variable* **func** - There are two ways you can specify a callback function:

  - **by name** - when you call a function, declared globally.
  - **by ID** - when you call a member function of a certain class. > **Notice:** An ID can be obtained via *[functionid()](../../../../api/library/common/class.system_usc.md#functionid_variable_int)*.

### Return value

Number of the last added callback of the specified type, if the callback was added successfully; otherwise, **-1**.
## bool removeCallback ( int callback , Variable func )

Removes a given callback from the list of callbacks of the specified type. Callback functions can be used to determine actions to be performed when sending or receiving user messages, as well as when changing settings on the Master or a Slave.
### Arguments

- *int* **callback** - Callback type. One of the following values:

  - [SESSION_STARTED](#SESSION_STARTED)
  - [SESSION_FINISHED](#SESSION_FINISHED)
  - [MASTER_CONNECTED](#MASTER_CONNECTED)
  - [MASTER_DISCONNECTED](#MASTER_DISCONNECTED)
  - [NODE_LOADED](#NODE_LOADED)
  - [NODE_CLONED](#NODE_CLONED)
- *Variable* **func** - There are two ways you can specify a callback function:

  - **by name** - when you call a function, declared globally.
  - **by ID** - when you call a member function of a certain class. > **Notice:** An ID can be obtained via *[functionid()](../../../../api/library/common/class.system_usc.md#functionid_variable_int)*.

### Return value

true if the position callback with the given ID was removed successfully; otherwise false.
## void clearCallbacks ( int callback )

Clears all added callbacks of the specified type. Callback functions can be used to determine actions to be performed when sending or receiving user messages, as well as when changing settings on the Master or a Slave.
### Arguments

- *int* **callback** - Callback type. One of the following values:

  - [SESSION_STARTED](#SESSION_STARTED)
  - [SESSION_FINISHED](#SESSION_FINISHED)
  - [MASTER_CONNECTED](#MASTER_CONNECTED)
  - [MASTER_DISCONNECTED](#MASTER_DISCONNECTED)
  - [NODE_LOADED](#NODE_LOADED)
  - [NODE_CLONED](#NODE_CLONED)

## void reconnect ( )
