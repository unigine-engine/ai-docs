# Unigine::SHA256 Class (CPP)

**Header:** #include <UnigineChecksum.h>


## SHA256 Class

### Members

---

## static SHA256Ptr create ( )

Default constructor that creates an empty instance.
## void update ( const void* data , int size )

Updates a 256-bit SHA256 checksum.
### Arguments

- *const void** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.

## void end ( unsigned int* value , bool big_endian )

Finalizes the checksum value by inverting all bits.
### Arguments

- *unsigned int** **value** - 256-bit SHA256 checksum (array of 8 unsigned int elements).
- *bool* **big_endian** - Byte ordering flag. Set true to use the big-endian order; false � to use the little-endian order.

## int calculate ( const void* data , int size , bool big_endian )

Calculates a 256-bit SHA256 checksum.
### Arguments

- *const void** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.
- *bool* **big_endian** - Byte ordering flag. Set true to use the big-endian order; false � to use the little-endian order.

### Return value

256-bit SHA256 checksum.
## void calculate ( unsigned int* value , const void* data , int size , bool big_endian )

Calculates a 256-bit SHA256 checksum.
### Arguments

- *unsigned int** **value** - 256-bit SHA256 checksum (array of 8 unsigned int elements).
- *const void** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.
- *bool* **big_endian** - Byte ordering flag. Set true to use the big-endian order; false � to use the little-endian order.
