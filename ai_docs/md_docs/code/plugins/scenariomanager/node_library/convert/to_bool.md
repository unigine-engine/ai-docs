# To Bool


![](../img/to_bool.png)

### Description

Converts a value to a boolean.


A number gives false when it is zero and true otherwise. A string gives true when it is not empty, whatever it contains - the text false also gives true. An array gives true when it has at least one element.


The input port is shown as Float, but a value of any type may be connected to it.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **Value** | The value to convert. |
| ![](../img/types/bool.png) | **Result** | The value as a boolean. |


## See Also


- [To Int](../../../../../code/plugins/scenariomanager/node_library/convert/to_int.md)
- [To Float](../../../../../code/plugins/scenariomanager/node_library/convert/to_float.md)
- [Branch](../../../../../code/plugins/scenariomanager/node_library/flow/branch.md)
