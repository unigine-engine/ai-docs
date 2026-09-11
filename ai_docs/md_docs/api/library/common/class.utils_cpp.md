# Unigine::Utils Class (CPP)

**Header:** #include <UnigineUtils.h>


This class contains the helper functions.


## Utils Class

### Members

---

## int convertHeightsToNormals ( Image Ptr & out , const Image Ptr & heights , float step_size )

Converts the elevation (height) map to the normal map.
### Arguments

- *[Image](../../../api/library/common/class.image_cpp.md)Ptr &* **out** - Pointer to the target normal map.
- *const [Image](../../../api/library/common/class.image_cpp.md)Ptr &* **heights** - Source elevation (height) map.
- *float* **step_size** - Grid cell step.

### Return value

1 if the converting was successful; otherwise, 0.
## void convertNodesToMesh ( Mesh Ptr & out , const Vector < Node Ptr > & nodes )

Creates a mesh out of the node array.
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cpp.md)Ptr &* **out** - Pointer to the target mesh.
- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)Ptr > &* **nodes** - Array of the node pointers.

## String date ( const char * format , long long time )

Returns given time as a string. The content of *format string* with format specifiers expanded with the corresponding values that represent the time described in *time*.
### Arguments

- *const char ** **format** - Format string containing any combination of regular characters and special format specifiers. These format specifiers are replaced by the function to the corresponding values to represent the time specified in timeptr. They all begin with a percentage (%) sign, and are as follows: | Specifier | Replaced by | Example | |---|---|---| | %a | Abbreviated weekday name | Thu | | %b | Abbreviated month name | Aug | | %d | Date and time representation equivalent to %a %b %D, %h:%m | Thu Aug 23, 14:55 | | %s | Second (00-61) | 15 | | %m | Minute (00-59) | 55 | | %h | Hour (00-24) | 14 | | %D | Month day (1-31) | 25 | | %M | Month (1-12) | 11 | | %Y | Year | 2016 | | %W | Week day (1-7) | 5 | | % | A % sign | % |
- *long long* **time** - Time value.

## String date ( const char * format )

Returns current time as a string. The content of *format string* with format specifiers expanded with the corresponding values that represent the current time.
### Arguments

- *const char ** **format** - Format string containing any combination of regular characters and special format specifiers. These format specifiers are replaced by the function to the corresponding values to represent the time specified in timeptr. They all begin with a percentage (%) sign, and are as follows: | Specifier | Replaced by | Example | |---|---|---| | %a | Abbreviated weekday name | Thu | | %b | Abbreviated month name | Aug | | %d | Date and time representation equivalent to %a %b %D, %h:%m | Thu Aug 23, 14:55 | | %s | Second (00-61) | 15 | | %m | Minute (00-59) | 55 | | %h | Hour (00-24) | 14 | | %D | Month day (1-31) | 25 | | %M | Month (1-12) | 11 | | %Y | Year | 2016 | | %W | Week day (1-7) | 5 | | % | A % sign | % |

## Node Ptr loadObjectMesh ( const char * name )

Loads a mesh from a file. If the mesh is loaded successfully, its node does not belong to any node hierarchy, so be careful and make sure to handle it properly, when it is no longer needed.
### Arguments

- *const char ** **name** - Path to the mesh.

### Return value

Pointer to the node corresponding to the loaded mesh; **0** if the mesh cannot be loaded.
## int makeNodeCurved ( const Ptr < Node > & node )


Curves a given node using its *Geodetic Pivot*.


> **Notice:** The node must be a child of a [*Geodetic Pivot*](../../../api/library/geodetics/class.geodeticpivot_cpp.md) node.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Pointer to the node to be made curved.

### Return value

1 if the node was curved successfully; othervise, 0.
## int makeNodeFlat ( const Ptr < Node > & node )


Flattens a given node using its *Geodetic Pivot*.


> **Notice:** The node must be a child of a [*Geodetic Pivot*](../../../api/library/geodetics/class.geodeticpivot_cpp.md) node.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Pointer to the node to be made flat.

### Return value

1 if the node was flattened successfully; othervise, 0.
