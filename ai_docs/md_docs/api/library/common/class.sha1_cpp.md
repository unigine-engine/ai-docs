# Unigine::SHA1 Class (CPP)

**Header:** #include <UnigineChecksum.h>


## SHA1 Class

### Members

---

## static SHA1Ptr create ( )

Default constructor that creates an empty instance.
## void begin ( )

Initializes a 160-bit SHA1 checksum with an initial value.
## void update ( const void* data , int size )

Updates a 160-bit SHA1 checksum.
### Arguments

- *const void** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.

## void end ( unsigned int* value , bool big_endian )

Finalizes the checksum value by inverting all bits.
### Arguments

- *unsigned int** **value** - 160-bit SHA1 checksum (array of 5 unsigned int elements).
- *bool* **big_endian** - Byte ordering flag. Set true to use the big-endian order; **false** � to use the little-endian order.

## int calculate ( const void* data , int size , bool big_endian )

Calculates a 160-bit SHA1 checksum.
### Arguments

- *const void** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.
- *bool* **big_endian** - Byte ordering flag. Set true to use the big-endian order; **false** � to use the little-endian order.

### Return value

160-bit SHA1 checksum.
## void calculate ( unsigned int* value , const void* data , int size , bool big_endian )

Calculates a 160-bit SHA1 checksum.
### Arguments

- *unsigned int** **value** - 160-bit SHA1 checksum (array of 5 unsigned int elements).
- *const void** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.
- *bool* **big_endian** - Byte ordering flag. Set true to use the big-endian order; **false** � to use the little-endian order.
