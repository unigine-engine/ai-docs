# Tag Component

**Inherits from:** ComponentBase


Tag is a lightweight component for labeling nodes with string identifiers. It provides a simple way to categorize and search for nodes without creating custom components for each category.


Common use cases include marking interactive objects (e.g., "pickup", "door", "enemy"), grouping nodes for batch operations, and filtering nodes in gameplay logic.


The component automatically computes a hash of the tag value on initialization for fast comparison. Use the **checkTag** utility function to test if a node has a specific tag.


Usage example:


```cpp
// Check if a node has a specific tag
if (Utils::checkTag(node, "interactive"))
{
    // Handle interactive object
}

```


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Value | *String* | The tag string identifier. |


### See Also


- **[Utils Namespace](../../../api/modules/common/class.utils.namespace.md)** � contains the **checkTag** function


## Utils::Tag Class

---

## getValue ( )

Returns the tag string value assigned to this component.
### Return value

The tag string value.
## getHash ( )

Returns the precomputed hash of the tag value. Used internally for fast comparison in **checkTag**.
### Return value

Hash of the tag value.
