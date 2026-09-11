# Unigine::CRC32 Class (CPP)

**Header:** #include <UnigineChecksum.h>


## CRC32 Class

### Members

---

## static CRC32Ptr create ( )

Default constructor that creates an empty instance.
## void begin ( )

Initializes a 32-bit CRC checksum with an initial value.
## void update ( const void* data , int size )

Updates a 32-bit CRC checksum.
### Arguments

- *const void** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.

## int end ( )

Finalizes the checksum value by inverting all bits.
## int calculate ( const void* data , int size , bool big_endian )

Calculates a 32-bit CRC checksum.
### Arguments

- *const void** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.
- *bool* **big_endian** - Byte ordering flag. Set true to use the big-endian order; false � to use the little-endian order.

### Return value

32-bit CRC checksum.
## unsigned int calcCrc32 ( const void* data , int size )

Calculates a 32-bit CRC checksum.
### Arguments

- *const void** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.

### Return value

32-bit CRC checksum.
