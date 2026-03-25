# Unigine::Bits Class (CPP)

**Header:** #include <UnigineMathLibCommon.h>


This class represents an auxiliary structure for storing data in the bit format regardless of the original type of data (template class). Data is copied bitwise into the structure.


## Bits Class

### Members

---

## static BitsPtr create ( )

Constructor. Initializes the bit structure.
## static BitsPtr create ( Type data_ )

Constructor. Initializes the bit structure with the data of the specified type.
### Arguments

- *Type* **data_** - Data of the particular type used for the initialization.

## void set ( int index , int value )

Sets the value to the bit with a given index.
### Arguments

- *int* **index** - Bit index.
- *int* **value** - Value to be set.

## void set ( int index , bool value )

Sets the value to the bit with a given index.
### Arguments

- *int* **index** - Bit index.
- *bool* **value** - Value to be set.

## bool get ( int index ) const

Returns the value of the bit with a given index.
### Arguments

- *int* **index** - Bit index.

### Return value

Bit value.
## bool operator[] ( int index ) const

Returns the value of the bit with a given index.
### Arguments

- *int* **index** - Bit index.

### Return value

Bit value.
## void set ( Type mask )

Sets the bit structure using the specified mask.
### Arguments

- *Type* **mask** - Any value used as a bit mask.

## Type get ( ) const

Returns the bit structure as a variable of the original type.
### Return value

Variable of the original type.
## int size ( ) const

Returns the capacity of the structure in bits.
### Return value

Capacity of the structure.
## void clear ( )

Clears the structure.
