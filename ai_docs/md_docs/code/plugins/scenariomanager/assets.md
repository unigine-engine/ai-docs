# Preparing Assets


Scenario Manager communicates with objects in the world exclusively through the ***DataBridge*** system. To make an asset visible to Scenario Manager, you need to attach a ****DataBridge* wrapper*** component to it.


## How It Works


DataBridge wrapper component is a C++ component that exposes specific properties and states of an object to DataBridge. It defines one or more ***topics*** - hierarchical paths under which data is published.


![DataBridge Topic](img/sm_db_wrapper.png)


When you add a wrapper component to an object in the UnigineEditor, you specify a topic name for that object (e.g., `plane_grounding_hook_socket`). The component then automatically creates one or more data paths under that name, for instance:


- *db_topic/id* - the object's unique identifier.
- *db_topic/item* - the item connected to this object.


Each component defines its own set of data paths depending on what information it exposes. The exact paths are listed in the component description.


### Available Wrapper Components


The following components are currently available in the **[MRO Template](../../../sdk/templates/maintenance/index.md)**, along with the parameters they expose:


- `VRSocketObjectDB` - Publishes socket occupancy:

  - *{db_topic}/id* - object ID (int)
  - *{db_topic}/item* - connected item ID; -1 if empty (int)
- `VRPluggableDB` - Publishes pluggable object state:

  - *{db_topic}/id*- object ID (int)
  - *{db_topic}/grab* - whether the object is grabbed by the player (bool)
  - *{db_topic}/connected_to* - ID of the socket this object is connected to; -1 if not connected (int)
- `VRInventoryDB` - Publishes inventory item presence:

  - {base_topic}/{alias}/present - whether the item is present in inventory (bool)
- `TooltipDB` - Controls tooltip visibility:

  - {db_topic}/tooltip - whether the tooltip is visible (bool)
- `NodeSwitchDB` - Enables/disables specified nodes based on a value:

  - *{db_topic}* - the topic itself holds the value
- `FuelCap` - Publishes fuel cap state. *FuelCap* is not a separate DataBridge wrapper component, it publishes its state directly from its own component logic. The topics become available once the *FuelCap* component is added to an object and its *db_topic* parameter is set:

  - *{db_topic}/closed* - whether the object is closed (bool)
  - *{db_topic}/inserted* - whether the object is inserted (bool)
  - *{db_topic}/grab* - whether the object is grabbed by the player (bool)
  - *{db_topic}/in_inventory* - whether the object is in inventory (bool)


> **Notice:** Each component requires a DataBridge topic parameter to be set in the UnigineEditor. This defines the root path under which all topics for that component are published.


### Using Topics in Scenarios


Once a wrapper component is added to an object, its data paths become available in the Scenario Manager editor. You can:


1. Read values using the *DataBridge **Get Parameter*** node
2. Write values using the *DataBridge **Set Parameter*** node
3. React to changes using the *DataBridge **On Parameter Changed*** event node


These nodes are described in the *[DataBridge](../../../code/plugins/scenariomanager/node_library/databridge/index.md)* section of the node reference.


Simply specify the full data path (e.g., `plane_grounding_hook_socket/item`) in the node's parameters.


![DataBridge Topic](img/sm_db_topic.png)

*Comparing DataBridge values: the graph checks if the grounding clamp is connected to the correct socket by comparing grounding_clamp/id and plane_grounding_hook_socket/item. If the values match, the action is considered complete*
