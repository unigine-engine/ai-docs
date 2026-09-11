# Unigine::MD5 Class (CPP)

**Header:** #include <UnigineChecksum.h>


## MD5 Class

### Members

---

## static MD5Ptr create ( )

Default constructor that creates an empty instance.
## void begin ( )

Initializes a 128-bit MD5 checksum with an initial value.
## void update ( const void* data , int size )

Updates a 128-bit MD5 checksum.
### Arguments

- *const void** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.

## void endMD5 ( unsigned int* value , bool big_endian )

Finalizes the checksum value by inverting all bits.
### Arguments

- *unsigned int** **value** - 128-bit MD5 checksum (array of 4 unsigned int elements).
- *bool* **big_endian** - Byte ordering flag. Set true to use the big-endian order; false � to use the little-endian order.

## void endD3D ( unsigned int* value )

Finalizes the 128-bit MD5 checksum (DXBC version).
### Arguments

- *unsigned int** **value** - 128-bit MD5 checksum (array of 4 unsigned int elements).

## int calculate ( const void* data , int size , bool big_endian )

Calculates a 128-bit MD5 checksum.
### Arguments

- *const void** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.
- *bool* **big_endian** - Byte ordering flag. Set true to use the big-endian order; false � to use the little-endian order.

### Return value

128-bit MD5 checksum.
## void calculate ( unsigned int* value , const void* data , int size , bool big_endian )

Calculates a 128-bit MD5 checksum.
### Arguments

- *unsigned int** **value** - 128-bit MD5 checksum (array of 4 unsigned int elements).
- *const void** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.
- *bool* **big_endian** - Byte ordering flag. Set true to use the big-endian order; false � to use the little-endian order.

## void calculateD3D ( unsigned int* value , const void* data , int size )

Calculates a 128-bit MD5 checksum (DXBC version).
### Arguments

- *unsigned int** **value** - 128-bit MD5 checksum (array of 4 unsigned int elements).
- *const void** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.
