# Unigine::ImportSkeleton Class (CS)


This class is an intermediate representation of a skeleton from a source file. It stores the joint hierarchy as a list of [ImportNode](../../../../api/library/common/import/class.importnode_cs.md) elements, where each node defines a joint's name, parent-child relationship, and bind pose transform. During import, it is converted to a Skeleton asset (.skeleton file).


## ImportSkeleton Class

### Properties

## IntPtr Data

The metadata of the imported skeleton.
## string Name

The name of the skeleton.
## string Filepath

The path to the output skeleton file.
### Members

---

## ImportSkeleton ( )

Constructor. Creates an empty *ImportSkeleton* instance.
## int NumJointNodes ( )

Returns the number of joint nodes in the skeleton.
### Return value

Number of joint nodes in the skeleton.
## ImportNode AddJointNode ( )

Adds a new joint node to the skeleton and returns the corresponding [ImportNode](../../../../api/library/common/import/class.importnode_cs.md) instance.
### Return value

New joint node added to the skeleton.
## ImportNode GetJointNode ( int index )

Returns a joint node with the specified index.
### Arguments

- *int* **index** - Index of the joint node.

### Return value

Joint node with the specified index.
## int GetJointNodeIndex ( ImportNode node )

Returns the index of the specified joint node in the skeleton.
### Arguments

- *[ImportNode](../../../../api/library/common/import/class.importnode_cs.md)* **node** - Joint node to find.

### Return value

Index of the specified joint node, or -1 if it is not found.
## void CreateSortedJointsHierarchy ( )

Sorts the joint nodes into a proper parent-child hierarchy order. This ensures that parent joints always precede their children in the joint list, which is required for correct skeleton processing during import.
