# Unigine::ArrayVector Class (CS)


Allows using UnigineScript [vectors](../../../code/uniginescript/language/containers/index.md#vector).


## ArrayVector Class

### Members

---

## ArrayVector ( ArrayVector vector )

Copy constructor.
### Arguments

- *[ArrayVector](../../../api/library/containers/class.arrayvector_cs.md)* **vector** - Vector.

## void Append ( Variable v )

Appends an item to the vector.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - Item.

## void Append ( int pos , Variable v )

Appends an item to the vector at a given position.
### Arguments

- *int* **pos** - Position index.
- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - Item.

## void Clear ( )

Clears all items of the vector.
## int Find ( Variable v )

Returns an index of a given item.
### Arguments

- *[Variable](../../../api/library/common/class.variable_cs.md)* **v** - Item.

### Return value

Index, if found; otherwise, -1.
## void Remove ( int pos )

Removes an item from a given position of the vector.
### Arguments

- *int* **pos** - Position index.

## void Resize ( int size )

Resizes a vector.
### Arguments

- *int* **size** - New vector capacity.

## int Size ( )

Returns vector length.
### Return value

Vector length.
