# Unigine::ArrayVector Class (CPP)

**Header:** #include <UnigineInterpreter.h>


Allows using UnigineScript [vectors](../../../code/uniginescript/language/containers/index.md#vector).


## ArrayVector Class

### Members

---

## ArrayVector ( const ArrayVector & vector )

Copy constructor.
### Arguments

- *const [ArrayVector](../../../api/library/containers/class.arrayvector_cpp.md) &* **vector** - Vector.

## void set ( int index , const Variable & v ) const

Sets an item by index.
### Arguments

- *int* **index** - Item index.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - Item to set.

## static ArrayVector get ( void * interpreter , const Variable & id )

Returns a vector from UnigineScript.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **id** - Vector ID.

### Return value

The vector.
## const Variable & get ( int index ) const

Returns an item by index.
### Arguments

- *int* **index** - Item index.

### Return value

The item.
## void append ( const Variable & v ) const

Appends an item to the vector.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - Item.

## void append ( int pos , const Variable & v ) const

Appends an item to the vector at a given position.
### Arguments

- *int* **pos** - Position index.
- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - Item.

## void clear ( ) const

Clears all items of the vector.
## int find ( const Variable & v ) const

Returns an index of a given item.
### Arguments

- *const [Variable](../../../api/library/common/class.variable_cpp.md) &* **v** - Item.

### Return value

Index, if found; otherwise, -1.
## ArrayVector & operator= ( const ArrayVector & vector )

Assignment operator for the vector.
### Arguments

- *const [ArrayVector](../../../api/library/containers/class.arrayvector_cpp.md) &* **vector** - Vector to be assigned.

## const Variable & operator[] ( int index ) const

Vector access.
### Arguments

- *int* **index** - Item index.

### Return value

The item.
## void remove ( int pos ) const

Removes an item from a given position of the vector.
### Arguments

- *int* **pos** - Position index.

## void resize ( int size ) const

Resizes a vector.
### Arguments

- *int* **size** - New vector capacity.

## int size ( ) const

Returns vector length.
### Return value

Vector length.
