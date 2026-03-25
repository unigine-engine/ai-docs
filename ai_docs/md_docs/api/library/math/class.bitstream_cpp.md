# Unigine::BitStream Class (CPP)

**Header:** #include <UnigineMathLibCommon.h>


This class represents an auxiliary structure for the fixed-size buffer and it's bitwise read/write operations. You can specify the size for the structure (template class). The default size is 128 bits.


## BitStream Class

### Members

---

## static BitStreamPtr create ( )

Constructor. Initializes the bit buffer.
## const unsigned char * get ( ) const

Returns the pointer to the constant bit buffer.
### Return value

Pointer to the constant bit buffer.
## unsigned char * get ( )

Returns the pointer to the bit buffer.
### Return value

Pointer to the bit buffer.
## int size ( ) const

Returns the size of the structure in bytes.
### Return value

Size of the structure in bytes.
## void clear ( )

Clears the buffer.
## void align ( )

Aligns the buffer.
## int readUBits ( int num )

Returns the unsigned data from the buffer.
### Arguments

- *int* **num** - Number of bits to return.

### Return value

Unsigned data.
## void writeUBits ( int value , int num )

Sets the unsigned data to the buffer.
### Arguments

- *int* **value** - Data to set.
- *int* **num** - Number of bits to set.

## int readBits ( int num )

Returns the signed data from the buffer.
### Arguments

- *int* **num** - Number of bits to return.

### Return value

Signed data.
## void writeBits ( int value , int num )

Sets the signed data to the buffer.
### Arguments

- *int* **value** - Data to set.
- *int* **num** - Number of bits to set.
