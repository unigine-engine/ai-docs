# Get Element


![](../img/get_element.png)

### Description

Reads the element stored at the given position in the array.


The index is checked before the element is read. If it falls outside the array, **Valid** is false and **Value** keeps whatever it held before, so check **Valid** before using the result.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/array.png) | **Array** | The array to read from. |
| ![](../img/types/int.png) | **Index** | The position of the element, counted from 0. |
| ![](../img/types/any.png) | **Value** | The element at the given position. |
| ![](../img/types/bool.png) | **Valid** | true if the index is within the array, false otherwise. |


## See Also


- [Set Element](../../../../../code/plugins/scenariomanager/node_library/array/set.md)
- [Array Length](../../../../../code/plugins/scenariomanager/node_library/array/length.md)
- [For Each](../../../../../code/plugins/scenariomanager/node_library/array/for_each.md)
