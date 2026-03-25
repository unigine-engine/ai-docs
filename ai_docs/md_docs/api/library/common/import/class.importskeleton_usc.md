# Unigine::ImportSkeleton Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is an intermediate representation of a skeleton from a source file. It stores the joint hierarchy as a list of [ImportNode](../../../../api/library/common/import/class.importnode_usc.md) elements, where each node defines a joint's name, parent-child relationship, and bind pose transform. During import, it is converted to a Skeleton asset (.skeleton file).


## ImportSkeleton Class

### Members

## void setData ( vptr data )

Sets a new metadata of the imported skeleton.
### Arguments

- *vptr* **data** - The skeleton metadata.

## vptr getData () const

Returns the current metadata of the imported skeleton.
### Return value

Current skeleton metadata.
## void setName ( string name )

Sets a new name of the skeleton.
### Arguments

- *string* **name** - The skeleton name.

## const char * getName () const

Returns the current name of the skeleton.
### Return value

Current skeleton name.
## void setFilepath ( string filepath )

Sets a new path to the output skeleton file.
### Arguments

- *string* **filepath** - The output skeleton file path.

## const char * getFilepath () const

Returns the current path to the output skeleton file.
### Return value

Current output skeleton file path.
---

## static ImportSkeleton ( )

Constructor. Creates an empty *ImportSkeleton* instance.
## int getNumJointNodes ( )

Returns the number of joint nodes in the skeleton.
### Return value

Number of joint nodes in the skeleton.
## ImportNode addJointNode ( )

Adds a new joint node to the skeleton and returns the corresponding [ImportNode](../../../../api/library/common/import/class.importnode_usc.md) instance.
### Return value

New joint node added to the skeleton.
## ImportNode getJointNode ( int index )

Returns a joint node with the specified index.
### Arguments

- *int* **index** - Index of the joint node.

### Return value

Joint node with the specified index.
## int getJointNodeIndex ( ImportNode node )

Returns the index of the specified joint node in the skeleton.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_usc.md)* **node** - Joint node to find.

### Return value

Index of the specified joint node, or -1 if it is not found.
## void createSortedJointsHierarchy ( )

Sorts the joint nodes into a proper parent-child hierarchy order. This ensures that parent joints always precede their children in the joint list, which is required for correct skeleton processing during import.
