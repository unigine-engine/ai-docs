# Unigine::Checksum Class (CPP)

**Header:** #include <UnigineChecksum.h>


## Checksum Class

### Members

---

## int CRC32 ( const void * data , int size , bool big_endian )

Calculates a 32-bit CRC checksum.
### Arguments

- *const void ** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.
- *bool* **big_endian** - Byte ordering flag. true if a big-endian order is used; false a little-endian order is used.

### Return value

32-bit CRC checksum.
## void MD5 ( unsigned int * value , const void * data , int size , bool big_endian )

Calculates a 128-bit MD5 checksum.
### Arguments

- *unsigned int ** **value** - 128-bit MD5 checksum (array of 4 unsigned int elements).
- *const void ** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.
- *bool* **big_endian** - Byte ordering flag. true if a big-endian order is used; false a little-endian order is used.

## int MD5 ( const void * data , int size , bool big_endian )

Calculates a 32-bit MD5 checksum.
### Arguments

- *const void ** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.
- *bool* **big_endian** - Byte ordering flag. true if a big-endian order is used; false a little-endian order is used.

### Return value

32-bit MD5 checksum.
## unsigned long long MD5_64 ( const void* data , int size , bool big_endian )

Calculates a 64-bit MD5 checksum.
### Arguments

- *const void** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.
- *bool* **big_endian** - Byte ordering flag. true if a big-endian order is used; false a little-endian order is used.

### Return value

64-bit MD5 checksum.
## void SHA1 ( unsigned int * value , const void * data , int size , bool big_endian )

Calculates a 160-bit SHA1 checksum.
### Arguments

- *unsigned int ** **value** - 160-bit SHA1 checksum (array of 5 unsigned int elements).
- *const void ** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.
- *bool* **big_endian** - Byte ordering flag. true if a big-endian order is used; false a little-endian order is used.

## int SHA1 ( const void * data , int size , bool big_endian )

Calculates a 32-bit SHA1 checksum.
### Arguments

- *const void ** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.
- *bool* **big_endian** - Byte ordering flag. true if a big-endian order is used; false a little-endian order is used.

### Return value

32-bit SHA1 checksum.
## void SHA256 ( unsigned int * value , const void * data , int size , bool big_endian )

Calculates a 256-bit SHA256 checksum.
### Arguments

- *unsigned int ** **value** - 256-bit SHA256 checksum (array of 8 unsigned int elements).
- *const void ** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.
- *bool* **big_endian** - Byte ordering flag. true if a big-endian order is used; false if a little-endian order is used.

## bool SHA256 ( const void * data , int size , int big_endian )

Calculates a 32-bit SHA256 checksum.
### Arguments

- *const void ** **data** - Input data pointer.
- *int* **size** - Input data size, in bytes.
- *int* **big_endian** - Byte ordering flag. true if a big-endian order is used; false a little-endian order is used.

### Return value

32-bit SHA256 checksum.
