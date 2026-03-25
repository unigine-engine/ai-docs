# Unigine::ImportSkeleton Class (CPP)

**Header:** #include <UnigineImport.h>


This class is an intermediate representation of a skeleton from a source file. It stores the joint hierarchy as a list of [ImportNode](../../../../api/library/common/import/class.importnode_cpp.md) elements, where each node defines a joint's name, parent-child relationship, and bind pose transform. During import, it is converted to a Skeleton asset (.skeleton file).


## ImportSkeleton Class

### Members

## void setData ( void * data )

Sets a new metadata of the imported skeleton.
### Arguments

- *void ** **data** - The skeleton metadata.

## void * getData () const

Returns the current metadata of the imported skeleton.
### Return value

Current skeleton metadata.
## void setName ( const char * name )

Sets a new name of the skeleton.
### Arguments

- *const char ** **name** - The skeleton name.

## const char * getName () const

Returns the current name of the skeleton.
### Return value

Current skeleton name.
## void setFilepath ( const char * filepath )

Sets a new path to the output skeleton file.
### Arguments

- *const char ** **filepath** - The output skeleton file path.

## const char * getFilepath () const

Returns the current path to the output skeleton file.
### Return value

Current output skeleton file path.
---

## static ImportSkeletonPtr create ( )

Constructor. Creates an empty *ImportSkeleton* instance.
## int getNumJointNodes ( ) const

Returns the number of joint nodes in the skeleton.
### Return value

Number of joint nodes in the skeleton.
## Ptr < ImportNode > addJointNode ( )

Adds a new joint node to the skeleton and returns the corresponding [ImportNode](../../../../api/library/common/import/class.importnode_cpp.md) instance.
### Return value

New joint node added to the skeleton.
## Ptr < ImportNode > getJointNode ( int index ) const

Returns a joint node with the specified index.
### Arguments

- *int* **index** - Index of the joint node.

### Return value

Joint node with the specified index.
## int getJointNodeIndex ( const Ptr < ImportNode > & node ) const

Returns the index of the specified joint node in the skeleton.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[ImportNode](../../../../api/library/common/import/class.importnode_cpp.md)> &* **node** - Joint node to find.

### Return value

Index of the specified joint node, or -1 if it is not found.
## void createSortedJointsHierarchy ( )

Sorts the joint nodes into a proper parent-child hierarchy order. This ensures that parent joints always precede their children in the joint list, which is required for correct skeleton processing during import.
