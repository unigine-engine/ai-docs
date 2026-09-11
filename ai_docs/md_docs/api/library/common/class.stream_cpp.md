# Unigine::Stream Class (CPP)

**Header:** #include <UnigineStreams.h>


This class cannot be instantiated. It is a base class for:


- *[File](../../../api/library/filesystem/class.file_cpp.md)* class
- *[Blob](../../../api/library/common/class.blob_cpp.md)* class
- *[Socket](../../../api/library/networking/class.socket_cpp.md)* class


*Stream* class allows you to write data into a stream, that is into files (stored on the disk), blobs (stored in system memory) and sockets (to be sent over the network), as well as read data from a stream.


## Stream Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **BLOB** = 0 | A stream for blobs. |
| **FILE** = 1 | A stream for files. |
| **SOCKET** = 2 | A stream for sockets. |
| **SSL_SOCKET** = 3 | A stream for [SSL sockets](../../../api/library/networking/class.sslsocket_cpp.md). |
| **USER** = 4 | A user stream inherited from StreamBase. |
| **NUM_STREAMS** = 5 | Number of stream types. |

### Members

## void setByteOrder ( int order )

Sets a new value indicating the endianness of the stream: **0** value is for LSB (least significant), **1** is for MSB (most significant).
### Arguments

- *int* **order** - The value indicating the endianness of the stream: **0** value is for LSB (least significant), **1** is for MSB (most significant).

## int getByteOrder () const

Returns the current value indicating the endianness of the stream: **0** value is for LSB (least significant), **1** is for MSB (most significant).
### Return value

Current value indicating the endianness of the stream: **0** value is for LSB (least significant), **1** is for MSB (most significant).
## bool isAvailable () const

Returns the current value indicating if stream data is available.
### Return value

**true** if stream data is available; otherwise **false**.
## bool isOpened () const

Returns the current value indicating if the stream is opened.
### Return value

**true** if the stream is opened; otherwise **false**.
## Stream::TYPE getType () const

Returns the current [the type](#BLOB) of the stream.
### Return value

Current [value](#BLOB) indicating the type of the stream.
---

## bool isError ( ) const

Returns the status of the stream.
### Return value

true if there is a read/write error; otherwise, false.
## String gets ( )

Reads the stream data from the current position.
### Return value

Stream data starting from the current position.
## int puts ( const char * str )

Writes a non-binary string of characters to the stream.
### Arguments

- *const char ** **str** - String to write.

### Return value

1 if a string of characters is written successfully; otherwise, 0.
## size_t read ( void * ptr , size_t size )

Reads the number of bytes from the stream.
### Arguments

- *void ** **ptr** - Destination buffer pointer.
- *size_t* **size** - Size of the buffer, in bytes.

### Return value

The number of read bytes.
## void read ( char & value ) const

Reads a ASCII character in a binary format (1 byte) from the stream.
### Arguments

- *char &* **value** - Variable to which the read value is saved.

## void read ( short & value ) const

Reads a signed short integer from the stream in accordance with the little-endian order.
### Arguments

- *short &* **value** - Variable to which the read value is saved.

## void read ( unsigned short & value ) const

Reads a unsigned short integer from the stream in accordance with the little-endian order.
### Arguments

- *unsigned short &* **value** - Variable to which the read value is saved.

## void read ( bool & value ) const

Reads a boolean value from the stream.
### Arguments

- *bool &* **value** - Variable to which the read value is saved.

## void read ( int & value ) const

Reads a signed integer from the stream in accordance with the little-endian order.
### Arguments

- *int &* **value** - Variable to which the read value is saved.

## void read ( unsigned int & value ) const

Reads a unsigned integer from the stream in accordance with the little-endian order.
### Arguments

- *unsigned int &* **value** - Variable to which the read value is saved.

## void read ( long long & value ) const

Reads a signed long from the stream in accordance with the little-endian order.
### Arguments

- *long long &* **value** - Variable to which the read value is saved.

## void read ( float & value ) const

Reads a floating-point number from the stream in accordance with the little-endian order.
### Arguments

- *float &* **value** - Variable to which the read value is saved.

## void read ( double & value ) const

Reads a double floating-point number from the stream in accordance with the little-endian order.
### Arguments

- *double &* **value** - Variable to which the read value is saved.

## void read ( Math:: vec2 & value ) const

Reads a 2-component vector from the stream in accordance with the little-endian order.
### Arguments

- *Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Variable to which the read value is saved.

## void read ( Math:: vec3 & value ) const

Reads a 3-component vector from the stream in accordance with the little-endian order.
### Arguments

- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Variable to which the read value is saved.

## void read ( Math:: vec4 & value ) const

Reads a 4-component vector from the stream in accordance with the little-endian order.
### Arguments

- *Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Variable to which the read value is saved.

## void read ( Math:: dvec2 & value ) const

Reads a 2-component double vector from the stream in accordance with the little-endian order.
### Arguments

- *Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **value** - Variable to which the read value is saved.

## void read ( Math:: dvec3 & value ) const

Reads a 3-component double vector from the stream in accordance with the little-endian order.
### Arguments

- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **value** - Variable to which the read value is saved.

## void read ( Math:: dvec4 & value ) const

Reads a 4-component double vector from the stream in accordance with the little-endian order.
### Arguments

- *Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Variable to which the read value is saved.

## void read ( Math:: ivec2 & value ) const

Reads a 2-component integer vector from the stream in accordance with the little-endian order.
### Arguments

- *Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **value** - Variable to which the read value is saved.

## void read ( Math:: ivec3 & value ) const

Reads a 3-component integer vector from the stream in accordance with the little-endian order.
### Arguments

- *Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **value** - Variable to which the read value is saved.

## void read ( Math:: ivec4 & value ) const

Reads a 4-component integer vector from the stream in accordance with the little-endian order.
### Arguments

- *Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **value** - Variable to which the read value is saved.

## void read ( Math:: mat4 & value ) const

Reads a matrix from the stream in accordance with the little-endian order.
### Arguments

- *Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **value** - Variable to which the read value is saved.

## void read ( Math:: dmat4 & value ) const

Reads a double matrix from the stream in accordance with the little-endian order.
### Arguments

- *Math::[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **value** - Variable to which the read value is saved.

## void read ( Math:: quat & value ) const

Reads a quaternion from the stream in accordance with the little-endian order.
### Arguments

- *Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **value** - Variable to which the read value is saved.

## bool readBool ( )

Reads a boolean value from the stream.
### Return value

Data value.
## char readChar ( )

Reads a ASCII character in a binary format (1 byte) from the stream.
### Return value

Received character.
## Math:: dmat4 readDMat4 ( )

Reads a double matrix from the stream in accordance with the little-endian order.
### Return value

Vector value.
## double readDouble ( )

Reads a double floating-point number from the stream in accordance with the little-endian order.
### Return value

Data value.
## int readDoubleArray ( const double* dest , int dest_size )

Reads an array of double floating-point numbers from the stream in accordance with the little-endian order.
### Arguments

- *const double** **dest** - Pointer to the array to store elements. Ensure that the array has enough space to hold at least 'dest_size' elements of the given type.
- *int* **dest_size** - Size of the array.

### Return value

1 if the operation was successful; otherwise, 0.
## Math:: dvec2 readDVec2 ( )

Reads a 2-component double vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## Math:: dvec3 readDVec3 ( )

Reads a 3-component double vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## Math:: dvec4 readDVec4 ( )

Reads a 4-component double vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## float readFloat ( )

Reads a floating-point number from the stream in accordance with the little-endian order.
### Return value

Data value.
## int readFloatArray ( const float* dest , int dest_size )

Reads an array of floating-point numbers from the stream in accordance with the little-endian order.
### Arguments

- *const float** **dest** - Pointer to the array to store elements. Ensure that the array has enough space to hold at least 'dest_size' elements of the given type.
- *int* **dest_size** - Size of the array.

### Return value

1 if the operation was successful; otherwise, 0.
## int readInt ( )

Reads a signed integer from the stream in accordance with the little-endian order.
### Return value

Data value.
## int readInt2 ( )

Reads a compact signed integer from the stream.
### Return value

Data value.
## int readIntArray ( const int* dest , int dest_size )

Reads an array of signed integers from the stream in accordance with the little-endian order.
### Arguments

- *const int** **dest** - Pointer to the array to store elements. Ensure that the array has enough space to hold at least 'dest_size' elements of the given type.
- *int* **dest_size** - Size of the array.

### Return value

1 if the operation was successful; otherwise, 0.
## Math:: ivec2 readIVec2 ( )

Reads a 2-component integer vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## Math:: ivec3 readIVec3 ( )

Reads a 3-component integer vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## Math:: ivec4 readIVec4 ( )

Reads a 4-component integer vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## int readLine ( const char* str , int str_size )

Reads a line from the stream.
### Arguments

- *const char** **str** - Target buffer to read a line to.
- *int* **str_size** - Line length.

### Return value

1 if the operation was successful; otherwise, 0.
## String readLine ( )

Reads a line of non-binary characters from the stream: starting from the current position until the end of line is reached ("\n"). The maximum length of the line is 4096 bytes.
### Return value

Received line.
## long long readLong ( )

Reads a signed long from the stream in accordance with the little-endian order.
### Return value

Data value.
## int readLongArray ( const llong* dest , int dest_size )

Reads an array of signed longs from the stream in accordance with the little-endian order.
### Arguments

- *const llong** **dest** - Pointer to the array to store elements. Ensure that the array has enough space to hold at least 'dest_size' elements of the given type.
- *int* **dest_size** - Size of the array.

### Return value

1 if the operation was successful; otherwise, 0.
## Math:: mat4 readMat4 ( )

Reads a matrix from the stream in accordance with the little-endian order.
### Return value

Vector value.
## Math:: mat4 readMat44 ( )

Reads the first 12 elements of 4x4 matrix from the current stream. The last 4 elements of the matrix are discarded.
### Return value

4x4 matrix with 12 read elements (the last four elements are equal to 0 0 0 1).
## Palette readPalette ( )

Reads a palette from the current stream.
### Return value

Palette value.
## Math:: quat readQuat ( )

Reads a quaternion from the stream in accordance with the little-endian order.
### Return value

Vector value.
## short readShort ( )

Reads a signed short integer from the stream in accordance with the little-endian order.
### Return value

Data value.
## int readShortArray ( const short* dest , int dest_size )

Reads an array of signed short integers from the stream in accordance with the little-endian order.
### Arguments

- *const short** **dest** - Pointer to the array to store elements. Ensure that the array has enough space to hold at least 'dest_size' elements of the given type.
- *int* **dest_size** - Size of the array.

### Return value

1 if the operation was successful; otherwise, 0.
## size_t readStream ( const Ptr < Stream > & dest , size_t size )

Reads the number of bytes directly from the stream.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **dest** - Destination stream pointer.
- *size_t* **size** - Size of the data in bytes.

### Return value

The number of read bytes.
## int readString ( const char* str , int str_size )

Reads a compact string in a binary format from the stream and puts it to the specified target buffer. Each binary string should be preceded by its length (the string length + the string itself). The string length is written as the compact signed integer.
### Arguments

- *const char** **str** - Target buffer to reand a string to.
- *int* **str_size** - Target buffer size, in bytes.

### Return value

1 if the operation was successful; otherwise, 0.
## String readString ( )

Reads a compact string in a binary format from the stream. Each binary string should be preceded by its length (the string length + the string itself). The string length is written as the compact signed integer.
### Return value

Received string.
## int readString2 ( const char* str , int str_size )

Reads a string from the stream in accordance with the big-endian order.
### Arguments

- *const char** **str**
- *int* **str_size** - String length.

### Return value

1 if the operation was successful; otherwise, 0.
## String readString2 ( )

### Return value

Received string.
## String readToken ( )

Reads a token from the stream. A token is a single word delimited by white space or a string in quotes, for example, "word" or "many words". A token is read starting from the current position up to the white space or line feed ("\n"), or if the first character is a double quote mark (") up to the second double quote mark (returned token will not contain any quotes). The maximum length of the string is 4096 bytes.
### Return value

Received token.
## int readToken ( char * OUT_str , int size )

### Arguments

- *char ** **OUT_str**
- *int* **size**

## unsigned char readUChar ( )

Reads an unsigned character in a binary format from the stream.
### Return value

Unsigned character in a binary format.
## unsigned int readUInt ( )

Reads a unsigned integer from the stream in accordance with the little-endian order.
### Return value

Data value.
## unsigned int readUInt2 ( )

Reads a compact unsigned integer from the stream.
### Return value

Data value.
## int readUIntArray ( const uint* dest , int dest_size )

Reads an array of unsigned integers from the stream in accordance with the little-endian order.
### Arguments

- *const uint** **dest** - Pointer to the array to store elements. Ensure that the array has enough space to hold at least 'dest_size' elements of the given type.
- *int* **dest_size** - Size of the array.

### Return value

1 if the operation was successful; otherwise, 0.
## unsigned short readUShort ( )

Reads a unsigned short integer from the stream in accordance with the little-endian order.
### Return value

Data value.
## int readUShortArray ( const ushort* dest , int dest_size )

Reads an array of unsigned short integers from the stream in accordance with the little-endian order.
### Arguments

- *const ushort** **dest** - Pointer to the array to store elements. Ensure that the array has enough space to hold at least 'dest_size' elements of the given type.
- *int* **dest_size** - Size of the array.

### Return value

1 if the operation was successful; otherwise, 0.
## Math:: vec2 readVec2 ( )

Reads a 2-component vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## Math:: vec3 readVec3 ( )

Reads a 3-component vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## Math:: vec4 readVec4 ( )

Reads a 4-component vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## size_t write ( const void * ptr , size_t size )

Writes the number of bytes to the stream.
### Arguments

- *const void ** **ptr** - Source buffer pointer.
- *size_t* **size** - Size of the buffer in bytes.

### Return value

The number of written bytes.
## bool write ( char value ) const

Writes an ASCII character in a binary format (1 byte) to the stream.
### Arguments

- *char* **value** - ASCII code of a character to write.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( short value ) const

Writes a signed short integer to the stream in accordance with the little-endian order.
### Arguments

- *short* **value** - A short integer value to write.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( unsigned short value ) const

Writes a unsigned short integer to the stream in accordance with the little-endian order.
### Arguments

- *unsigned short* **value** - Unsigned short integer to write.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( bool value ) const

Writes the specified boolean value to the stream.
### Arguments

- *bool* **value** - Data value to be written.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( int value ) const

Writes a signed integer to the stream in accordance with the little-endian order.
### Arguments

- *int* **value** - An integer value to write.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( unsigned int value ) const

Writes a unsigned integer to the stream in accordance with the little-endian order.
### Arguments

- *unsigned int* **value** - Data value.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( long long value ) const

Writes a signed long to the stream in accordance with the little-endian order.
### Arguments

- *long long* **value** - A *long* value to write.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( float value ) const

Writes a floating-point number to the stream in accordance with the little-endian order.
### Arguments

- *float* **value** - A *float* value to write.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( double value ) const

Writes a double floating-point number to the stream in accordance with the little-endian order.
### Arguments

- *double* **value** - A *double* value to write.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( const char * value ) const

Writes a string in a binary format to the stream. Each binary string should be preceded by its length (4 bytes defining the length of string + the string itself).
### Arguments

- *const char ** **value** - String to write.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( const Math:: vec2 & value ) const

Writes a 2-component vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( const Math:: vec3 & value ) const

Writes a 3-component vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( const Math:: vec4 & value ) const

Writes a 4-component vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( const Math:: dvec2 & value ) const

Writes a 2-component double vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( const Math:: dvec3 & value ) const

Writes a 3-component double vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( const Math:: dvec4 & value ) const

Writes a 4-component double vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( const Math:: ivec2 & value ) const

Writes a 2-component integer vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( const Math:: ivec3 & value ) const

Writes a 3-component integer vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( const Math:: ivec4 & value ) const

Writes a 4-component integer vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( const Math:: mat4 & value ) const

Writes a matrix to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **value** - A matrix to write.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( const Math:: dmat4 & value ) const

Writes a double matrix to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **value** - A matrix to write.

### Return value

true if a character is written successfully; otherwise false.
## bool write ( const Math:: quat & value ) const

Writes a quaternion to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **value** - A quaternion to write.

### Return value

true if a character is written successfully; otherwise false.
## bool writeBool ( bool value )

Writes the specified boolean value to the stream.
### Arguments

- *bool* **value** - Data value to be written.

### Return value

true if the operation was successful; otherwise, false.
## bool writeChar ( char value )

Writes an ASCII character in a binary format (1 byte) to the stream.
### Arguments

- *char* **value** - ASCII code of a character to write.

### Return value

true if a character is written successfully; otherwise false.
## bool writeDMat4 ( const Math:: dmat4 & value )

Writes a double matrix to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **value** - A matrix to write.

### Return value

true if the matrix is written successfully; otherwise, false.
## bool writeDouble ( double value )

Writes a *double* floating-point number to the stream in accordance with the little-endian order.
### Arguments

- *double* **value** - Data value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeDoubleArray ( double* OUT_src , int src_size )

Writes an array of *double* floating-point numbers to the stream in accordance with the little-endian order.
### Arguments

- *double** **OUT_src**
- *int* **src_size** - Size of the array.

### Return value

true if the operation was successful; otherwise, false.
## bool writeDVec2 ( const Math:: dvec2 & value )

Writes a 2-component *double* vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[dvec2](../../../api/library/math/class.dvec2_cpp.md) &* **value** - Vector value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeDVec3 ( const Math:: dvec3 & value )

Writes a 3-component *double* vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **value** - Vector value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeDVec4 ( const Math:: dvec4 & value )

Writes a 4-component *double* vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[dvec4](../../../api/library/math/class.dvec4_cpp.md) &* **value** - Vector value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeFloat ( float value )

Writes a floating-point number to the stream in accordance with the little-endian order.
### Arguments

- *float* **value** - Data value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeFloatArray ( float* OUT_src , int src_size )

Writes an array of floating-point numbers to the stream in accordance with the little-endian order.
### Arguments

- *float** **OUT_src**
- *int* **src_size** - Size of the array.

### Return value

true if the operation was successful; otherwise, false.
## bool writeInt ( int value )

Writes a signed integer to the stream in accordance with the little-endian order.
### Arguments

- *int* **value** - Data value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeInt2 ( int value )

Writes a compact signed integer to the stream.
### Arguments

- *int* **value** - Data value.

### Return value

true if the compact integer is written successfully; otherwise, false.
## bool writeIntArray ( int* OUT_src , int src_size )

Writes an array of signed integers to the stream in accordance with the little-endian order.
### Arguments

- *int** **OUT_src**
- *int* **src_size** - Size of the array.

### Return value

true if the operation was successful; otherwise, false.
## bool writeIVec2 ( const Math:: ivec2 & value )

Writes a 2-component integer vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[ivec2](../../../api/library/math/class.ivec2_cpp.md) &* **value** - Vector value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeIVec3 ( const Math:: ivec3 & value )

Writes a 3-component integer vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[ivec3](../../../api/library/math/class.ivec3_cpp.md) &* **value** - Vector value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeIVec4 ( const Math:: ivec4 & value )

Writes a 4-component integer vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[ivec4](../../../api/library/math/class.ivec4_cpp.md) &* **value** - Vector value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeLong ( long long value )

Writes a signed long to the stream in accordance with the little-endian order.
### Arguments

- *long long* **value** - Data value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeLongArray ( llong* OUT_src , int src_size )

Writes an array of signed longs to the stream in accordance with the little-endian order.
### Arguments

- *llong** **OUT_src**
- *int* **src_size** - Size of the array.

### Return value

true if the operation was successful; otherwise, false.
## bool writeMat4 ( const Math:: mat4 & value )

Writes a *[mat4](../../../code/uniginescript/language/data_types.md#mat4)* (a matrix of float values, 4*16 bytes) to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **value** - A matrix to write.

### Return value

true if the operation was successful; otherwise, false.
## bool writeMat44 ( const Math:: mat4 & value )

Writes the first 12 elements of 4x4 matrix in a binary format into the current stream. The last 4 elements of the matrix are discarded.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **value** - A 4x4 matrix.

### Return value

true if data is written successfully; otherwise, false.
## int writePalette ( const Palette & value )

Writes the palette to the stream.
### Arguments

- *const [Palette](../../../api/library/common/class.palette_cpp.md) &* **value** - Palette value.

## bool writeQuat ( const Math:: quat & value )

Writes a quaternion to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[quat](../../../api/library/math/class.quat_cpp.md) &* **value** - Vector value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeShort ( short value )

Writes a signed short integer to the stream in accordance with the little-endian order.
### Arguments

- *short* **value** - Data value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeShortArray ( short* OUT_src , int src_size )

Writes an array of signed short integers to the stream in accordance with the little-endian order.
### Arguments

- *short** **OUT_src**
- *int* **src_size** - Size of the array.

### Return value

true if the operation was successful; otherwise, false.
## size_t writeStream ( const Ptr < Stream > & src , size_t size )

Returns the number of bytes successfully read from the argument stream.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **src** - Source stream pointer.
- *size_t* **size** - Size of the data in bytes.

### Return value

The number of bytes successfully read from the argument `src` stream.
## bool writeString ( const char * str )

Writes a string in a binary format to the stream. Each binary string should be preceded by its length (4 bytes defining the length of string + the string itself).
### Arguments

- *const char ** **str** - String to write.

### Return value

true if the string is written successfully; otherwise, false.
## bool writeString2 ( const char * str )

Writes a compact string in a binary format to the stream. Each binary string should be preceded by its length (the string length + the string itself). The string length is written as the compact signed integer.
### Arguments

- *const char ** **str** - String to write.

### Return value

true if the string is written successfully; otherwise, false.
## bool writeUChar ( unsigned char value )

Writes an unsigned character to the stream.
### Arguments

- *unsigned char* **value** - Unsigned character to write.

### Return value

true if the unsigned character is written successfully; otherwise, false.
## bool writeUInt ( unsigned int value )

Writes a unsigned integer to the stream in accordance with the little-endian order.
### Arguments

- *unsigned int* **value** - Data value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeUInt2 ( unsigned int value )

Writes a compact unsigned integer to the stream.
### Arguments

- *unsigned int* **value** - Data value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeUIntArray ( uint* OUT_src , int src_size )

Writes an array of unsigned integers to the stream in accordance with the little-endian order.
### Arguments

- *uint** **OUT_src**
- *int* **src_size** - Size of the array.

### Return value

true if the operation was successful; otherwise, false.
## bool writeUShort ( unsigned short value )

Writes a unsigned short integer to the stream in accordance with the little-endian order.
### Arguments

- *unsigned short* **value** - Data value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeUShortArray ( ushort* OUT_src , int src_size )

Writes an array of unsigned short integers to the stream in accordance with the little-endian order.
### Arguments

- *ushort** **OUT_src**
- *int* **src_size** - Size of the array.

### Return value

true if the operation was successful; otherwise, false.
## bool writeVec2 ( const Math:: vec2 & value )

Writes a 2-component vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[vec2](../../../api/library/math/class.vec2_cpp.md) &* **value** - Vector value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeVec3 ( const Math:: vec3 & value )

Writes a 3-component vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **value** - Vector value.

### Return value

true if the operation was successful; otherwise, false.
## bool writeVec4 ( const Math:: vec4 & value )

Writes a 4-component vector to the stream in accordance with the little-endian order.
### Arguments

- *const  Math::[vec4](../../../api/library/math/class.vec4_cpp.md) &* **value** - Vector value.

### Return value

true if the operation was successful; otherwise, false.
