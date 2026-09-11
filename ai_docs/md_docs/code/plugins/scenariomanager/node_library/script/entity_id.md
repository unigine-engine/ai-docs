# Get Entity ID


![](../img/get_entity_id.png)

### Description

Outputs the identifier of the entity the script is attached to.


The same graph can run for several entities at once, each with its own copy of the script. This node tells the copies apart, which makes it useful for building per-entity variable names or reporting which entity produced a log entry.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/string.png) | **Entity ID** | The identifier of the entity, empty if the script is not attached to one. |


## See Also


- [Get My Script ID](../../../../../code/plugins/scenariomanager/node_library/script/my_script_id.md)
- [Get My Script Name](../../../../../code/plugins/scenariomanager/node_library/script/my_script_name.md)
