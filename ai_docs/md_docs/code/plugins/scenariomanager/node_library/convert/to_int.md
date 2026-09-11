# To Int


![](../img/to_int.png)

### Description

Converts a value to an integer. A fractional part is discarded rather than rounded, so 2.7 gives 2 and -2.7 gives -2.


The input port is shown as Float, but a value of any type may be connected to it - a boolean gives 1 or 0, a string is read as a number, and an array gives the number of its elements.


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **Value** | The value to convert. |
| ![](../img/types/int.png) | **Result** | The value as an integer. |


## See Also


- [To Float](../../../../../code/plugins/scenariomanager/node_library/convert/to_float.md)
- [Float to Int](../../../../../code/plugins/scenariomanager/node_library/convert/float_to_int.md)
- [String to Int](../../../../../code/plugins/scenariomanager/node_library/string/string_to_int.md)
