# Unigine::Stream Class (CS)


This class cannot be instantiated. It is a base class for:


- *[File](../../../api/library/filesystem/class.file_cs.md)* class
- *[Blob](../../../api/library/common/class.blob_cs.md)* class
- *[Socket](../../../api/library/networking/class.socket_cs.md)* class


*Stream* class allows you to write data into a stream, that is into files (stored on the disk), blobs (stored in system memory) and sockets (to be sent over the network), as well as read data from a stream.


## Stream Class

### Enums

## TYPE

| Name | Description |
|---|---|
| **BLOB** = 0 | A stream for blobs. |
| **FILE** = 1 | A stream for files. |
| **SOCKET** = 2 | A stream for sockets. |
| **SSL_SOCKET** = 3 | A stream for [SSL sockets](../../../api/library/networking/class.sslsocket_cs.md). |
| **USER** = 4 | A user stream inherited from StreamBase. |
| **NUM_STREAMS** = 5 | Number of stream types. |

### Properties

## int ByteOrder

The value indicating the endianness of the stream: **0** value is for LSB (least significant), **1** is for MSB (most significant).
## 🔒︎ bool IsAvailable

The value indicating if stream data is available.
## 🔒︎ bool IsOpened

The value indicating if the stream is opened.
## 🔒︎ Stream.TYPE Type

The [the type](#BLOB) of the stream.
### Members

---

## bool IsError ( )

Returns the status of the stream.
### Return value

true if there is a read/write error; otherwise, false.
## string Gets ( )

Reads the stream data from the current position.
### Return value

Stream data starting from the current position.
## int Puts ( string str )

Writes a non-binary string of characters to the stream.
### Arguments

- *string* **str** - String to write.

### Return value

1 if a string of characters is written successfully; otherwise, 0.
## ulong Read ( IntPtr ptr , ulong size )

Reads the number of bytes from the stream.
### Arguments

- *IntPtr* **ptr** - Vector, into which data will be read.
- *ulong* **size** - Size of data to read.

### Return value

The number of read bytes.
## void Read ( out byte value )

Reads a ASCII character in a binary format (1 byte) from the stream.
### Arguments

- *out byte* **value** - Variable to which the read value is saved.

## void Read ( out short value )

Reads a signed short integer from the stream in accordance with the little-endian order.
### Arguments

- *out short* **value** - Variable to which the read value is saved.

## void Read ( out ushort value )

Reads a unsigned short integer from the stream in accordance with the little-endian order.
### Arguments

- *out ushort* **value** - Variable to which the read value is saved.

## void Read ( out bool value )

Reads a boolean value from the stream.
### Arguments

- *out bool* **value** - Variable to which the read value is saved.

## void Read ( out int value )

Reads a signed integer from the stream in accordance with the little-endian order.
### Arguments

- *out int* **value** - Variable to which the read value is saved.

## void Read ( out uint value )

Reads a unsigned integer from the stream in accordance with the little-endian order.
### Arguments

- *out uint* **value** - Variable to which the read value is saved.

## void Read ( out long value )

Reads a signed long from the stream in accordance with the little-endian order.
### Arguments

- *out long* **value** - Variable to which the read value is saved.

## void Read ( out float value )

Reads a floating-point number from the stream in accordance with the little-endian order.
### Arguments

- *out float* **value** - Variable to which the read value is saved.

## void Read ( out double value )

Reads a double floating-point number from the stream in accordance with the little-endian order.
### Arguments

- *out double* **value** - Variable to which the read value is saved.

## void Read ( out vec2 value )

Reads a 2-component vector from the stream in accordance with the little-endian order.
### Arguments

- *out vec2* **value** - Variable to which the read value is saved.

## void Read ( out vec3 value )

Reads a 3-component vector from the stream in accordance with the little-endian order.
### Arguments

- *out vec3* **value** - Variable to which the read value is saved.

## void Read ( out vec4 value )

Reads a 4-component vector from the stream in accordance with the little-endian order.
### Arguments

- *out vec4* **value** - Variable to which the read value is saved.

## void Read ( out dvec2 value )

Reads a 2-component double vector from the stream in accordance with the little-endian order.
### Arguments

- *out dvec2* **value** - Variable to which the read value is saved.

## void Read ( out dvec3 value )

Reads a 3-component double vector from the stream in accordance with the little-endian order.
### Arguments

- *out dvec3* **value** - Variable to which the read value is saved.

## void Read ( out dvec4 value )

Reads a 4-component double vector from the stream in accordance with the little-endian order.
### Arguments

- *out dvec4* **value** - Variable to which the read value is saved.

## void Read ( out ivec2 value )

Reads a 2-component integer vector from the stream in accordance with the little-endian order.
### Arguments

- *out ivec2* **value** - Variable to which the read value is saved.

## void Read ( out ivec3 value )

Reads a 3-component integer vector from the stream in accordance with the little-endian order.
### Arguments

- *out ivec3* **value** - Variable to which the read value is saved.

## void Read ( out ivec4 value )

Reads a 4-component integer vector from the stream in accordance with the little-endian order.
### Arguments

- *out ivec4* **value** - Variable to which the read value is saved.

## void Read ( out mat4 value )

Reads a matrix from the stream in accordance with the little-endian order.
### Arguments

- *out mat4* **value** - Variable to which the read value is saved.

## void Read ( out dmat4 value )

Reads a double matrix from the stream in accordance with the little-endian order.
### Arguments

- *out dmat4* **value** - Variable to which the read value is saved.

## void Read ( out quat value )

Reads a quaternion from the stream in accordance with the little-endian order.
### Arguments

- *out quat* **value** - Variable to which the read value is saved.

## bool ReadBool ( )

Reads a boolean value from the stream.
### Return value

Data value.
## byte ReadChar ( )

Reads a ASCII character in a binary format (1 byte) from the stream.
### Return value

Received character.
## dmat4 ReadDMat4 ( )

Reads a double matrix from the stream in accordance with the little-endian order.
### Return value

Vector value.
## double ReadDouble ( )

Reads a double floating-point number from the stream in accordance with the little-endian order.
### Return value

Data value.
## int ReadDoubleArray ( ref double[] dest , int dest_size )

Reads an array of double floating-point numbers from the stream in accordance with the little-endian order.
### Arguments

- *ref double[]* **dest** - Array to store elements. Ensure that the array has enough space to hold at least 'dest_size' elements of the given type.
- *int* **dest_size** - Size of the array.

### Return value

1 if the operation was successful; otherwise, 0.
## dvec2 ReadDVec2 ( )

Reads a 2-component double vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## dvec3 ReadDVec3 ( )

Reads a 3-component double vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## dvec4 ReadDVec4 ( )

Reads a 4-component double vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## float ReadFloat ( )

Reads a floating-point number from the stream in accordance with the little-endian order.
### Return value

Data value.
## int ReadFloatArray ( ref float[] dest , int dest_size )

Reads an array of floating-point numbers from the stream in accordance with the little-endian order.
### Arguments

- *ref float[]* **dest** - Array to store elements. Ensure that the array has enough space to hold at least 'dest_size' elements of the given type.
- *int* **dest_size** - Size of the array.

### Return value

1 if the operation was successful; otherwise, 0.
## int ReadInt ( )

Reads a signed integer from the stream in accordance with the little-endian order.
### Return value

Data value.
## int ReadInt2 ( )

Reads a compact signed integer from the stream.
### Return value

Data value.
## int ReadIntArray ( ref int[] dest , int dest_size )

Reads an array of signed integers from the stream in accordance with the little-endian order.
### Arguments

- *ref int[]* **dest** - Array to store elements. Ensure that the array has enough space to hold at least 'dest_size' elements of the given type.
- *int* **dest_size** - Size of the array.

### Return value

1 if the operation was successful; otherwise, 0.
## ivec2 ReadIVec2 ( )

Reads a 2-component integer vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## ivec3 ReadIVec3 ( )

Reads a 3-component integer vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## ivec4 ReadIVec4 ( )

Reads a 4-component integer vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## int ReadLine ( ref byte[] str , int str_size )

Reads a line from the stream.
### Arguments

- *ref byte[]* **str** - Target buffer to read a line to.
- *int* **str_size** - Line length.

### Return value

1 if the operation was successful; otherwise, 0.
## string ReadLine ( )

Reads a line of non-binary characters from the stream: starting from the current position until the end of line is reached ("\n"). The maximum length of the line is 4096 bytes.
### Return value

Received line.
## long ReadLong ( )

Reads a signed long from the stream in accordance with the little-endian order.
### Return value

Data value.
## int ReadLongArray ( ref llong[] dest , int dest_size )

Reads an array of signed longs from the stream in accordance with the little-endian order.
### Arguments

- *ref llong[]* **dest** - Array to store elements. Ensure that the array has enough space to hold at least 'dest_size' elements of the given type.
- *int* **dest_size** - Size of the array.

### Return value

1 if the operation was successful; otherwise, 0.
## mat4 ReadMat4 ( )

Reads a matrix from the stream in accordance with the little-endian order.
### Return value

Vector value.
## mat4 ReadMat44 ( )

Reads the first 12 elements of 4x4 matrix from the current stream. The last 4 elements of the matrix are discarded.
### Return value

4x4 matrix with 12 read elements (the last four elements are equal to 0 0 0 1).
## Palette ReadPalette ( )

Reads a palette from the current stream.
### Return value

Palette value.
## quat ReadQuat ( )

Reads a quaternion from the stream in accordance with the little-endian order.
### Return value

Vector value.
## short ReadShort ( )

Reads a signed short integer from the stream in accordance with the little-endian order.
### Return value

Data value.
## int ReadShortArray ( ref short[] dest , int dest_size )

Reads an array of signed short integers from the stream in accordance with the little-endian order.
### Arguments

- *ref short[]* **dest** - Array to store elements. Ensure that the array has enough space to hold at least 'dest_size' elements of the given type.
- *int* **dest_size** - Size of the array.

### Return value

1 if the operation was successful; otherwise, 0.
## ulong ReadStream ( Stream dest , ulong size )

Reads the number of bytes directly from the stream.
### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **dest** - Stream to write data into.
- *ulong* **size** - Size of data to be read from the current stream.

### Return value

The number of read bytes.
## int ReadString ( ref byte[] str )

Reads a compact string in a binary format from the stream and puts it to the specified target buffer. Each binary string should be preceded by its length (the string length + the string itself). The string length is written as the compact signed integer.
### Arguments

- *ref byte[]* **str** - Target buffer to reand a string to.

### Return value

1 if the operation was successful; otherwise, 0.
## string ReadString ( )

Reads a compact string in a binary format from the stream. Each binary string should be preceded by its length (the string length + the string itself). The string length is written as the compact signed integer.
### Return value

Received string.
## int ReadString2 ( ref byte[] str , int str_size )

Reads a string from the stream in accordance with the big-endian order.
### Arguments

- *ref byte[]* **str**
- *int* **str_size** - String length.

### Return value

1 if the operation was successful; otherwise, 0.
## string ReadString2 ( )

### Return value

Received string.
## string ReadToken ( )

Reads a token from the stream. A token is a single word delimited by white space or a string in quotes, for example, "word" or "many words". A token is read starting from the current position up to the white space or line feed ("\n"), or if the first character is a double quote mark (") up to the second double quote mark (returned token will not contain any quotes). The maximum length of the string is 4096 bytes.
### Return value

Received token.
## int ReadToken ( char[] OUT_str , int size )

### Arguments

- *char[]* **OUT_str**
- *int* **size**

## byte ReadUChar ( )

Reads an unsigned character in a binary format from the stream.
### Return value

Unsigned character in a binary format.
## uint ReadUInt ( )

Reads a unsigned integer from the stream in accordance with the little-endian order.
### Return value

Data value.
## uint ReadUInt2 ( )

Reads a compact unsigned integer from the stream.
### Return value

Data value.
## int ReadUIntArray ( ref uint[] dest , int dest_size )

Reads an array of unsigned integers from the stream in accordance with the little-endian order.
### Arguments

- *ref uint[]* **dest** - Array to store elements. Ensure that the array has enough space to hold at least 'dest_size' elements of the given type.
- *int* **dest_size** - Size of the array.

### Return value

1 if the operation was successful; otherwise, 0.
## ushort ReadUShort ( )

Reads a unsigned short integer from the stream in accordance with the little-endian order.
### Return value

Data value.
## int ReadUShortArray ( ref ushort[] dest , int dest_size )

Reads an array of unsigned short integers from the stream in accordance with the little-endian order.
### Arguments

- *ref ushort[]* **dest** - Array to store elements. Ensure that the array has enough space to hold at least 'dest_size' elements of the given type.
- *int* **dest_size** - Size of the array.

### Return value

1 if the operation was successful; otherwise, 0.
## vec2 ReadVec2 ( )

Reads a 2-component vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## vec3 ReadVec3 ( )

Reads a 3-component vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## vec4 ReadVec4 ( )

Reads a 4-component vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## ulong Write ( IntPtr ptr , ulong size )

Writes the number of bytes to the stream.
### Arguments

- *IntPtr* **ptr** - Buffer, from which data will be written.
- *ulong* **size** - Size of data to write.

### Return value

The number of written bytes.
## bool Write ( byte value )

Writes an ASCII character in a binary format (1 byte) to the stream.
### Arguments

- *byte* **value** - ASCII code of a character to write.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( short value )

Writes a signed short integer to the stream in accordance with the little-endian order.
### Arguments

- *short* **value** - A short integer value to write.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( ushort value )

Writes a unsigned short integer to the stream in accordance with the little-endian order.
### Arguments

- *ushort* **value** - Unsigned short integer to write.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( bool value )

Writes the specified boolean value to the stream.
### Arguments

- *bool* **value** - Data value to be written.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( int value )

Writes a signed integer to the stream in accordance with the little-endian order.
### Arguments

- *int* **value** - An integer value to write.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( uint value )

Writes a unsigned integer to the stream in accordance with the little-endian order.
### Arguments

- *uint* **value** - Data value.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( long value )

Writes a signed long to the stream in accordance with the little-endian order.
### Arguments

- *long* **value** - A *long* value to write.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( float value )

Writes a floating-point number to the stream in accordance with the little-endian order.
### Arguments

- *float* **value** - A *float* value to write.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( double value )

Writes a double floating-point number to the stream in accordance with the little-endian order.
### Arguments

- *double* **value** - A *double* value to write.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( string value )

Writes a string in a binary format to the stream. Each binary string should be preceded by its length (4 bytes defining the length of string + the string itself).
### Arguments

- *string* **value** - String to write.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( vec2 value )

Writes a 2-component vector to the stream in accordance with the little-endian order.
### Arguments

- *vec2* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( vec3 value )

Writes a 3-component vector to the stream in accordance with the little-endian order.
### Arguments

- *vec3* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( vec4 value )

Writes a 4-component vector to the stream in accordance with the little-endian order.
### Arguments

- *vec4* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( dvec2 value )

Writes a 2-component double vector to the stream in accordance with the little-endian order.
### Arguments

- *dvec2* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( dvec3 value )

Writes a 3-component double vector to the stream in accordance with the little-endian order.
### Arguments

- *dvec3* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( dvec4 value )

Writes a 4-component double vector to the stream in accordance with the little-endian order.
### Arguments

- *dvec4* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( ivec2 value )

Writes a 2-component integer vector to the stream in accordance with the little-endian order.
### Arguments

- *ivec2* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( ivec3 value )

Writes a 3-component integer vector to the stream in accordance with the little-endian order.
### Arguments

- *ivec3* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( ivec4 value )

Writes a 4-component integer vector to the stream in accordance with the little-endian order.
### Arguments

- *ivec4* **value** - Vector value.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( mat4 value )

Writes a matrix to the stream in accordance with the little-endian order.
### Arguments

- *mat4* **value** - A matrix to write.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( dmat4 value )

Writes a double matrix to the stream in accordance with the little-endian order.
### Arguments

- *dmat4* **value** - A matrix to write.

### Return value

true if a character is written successfully; otherwise false.
## bool Write ( quat value )

Writes a quaternion to the stream in accordance with the little-endian order.
### Arguments

- *quat* **value** - A quaternion to write.

### Return value

true if a character is written successfully; otherwise false.
## bool WriteBool ( bool value )

Writes the specified boolean value to the stream.
### Arguments

- *bool* **value** - Data value to be written.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteChar ( byte value )

Writes an ASCII character in a binary format (1 byte) to the stream.
### Arguments

- *byte* **value** - ASCII code of a character to write.

### Return value

true if a character is written successfully; otherwise false.
## bool WriteDMat4 ( dmat4 value )

Writes a double matrix to the stream in accordance with the little-endian order.
### Arguments

- *dmat4* **value** - A matrix to write.

### Return value

true if the matrix is written successfully; otherwise, false.
## bool WriteDouble ( double value )

Writes a *double* floating-point number to the stream in accordance with the little-endian order.
### Arguments

- *double* **value** - A *double* value to write.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteDoubleArray ( double[] OUT_src )

Writes an array of *double* floating-point numbers to the stream in accordance with the little-endian order.
### Arguments

- *double[]* **OUT_src**

### Return value

true if the operation was successful; otherwise, false.
## bool WriteDVec2 ( dvec2 value )

Writes a 2-component *double* vector to the stream in accordance with the little-endian order.
### Arguments

- *dvec2* **value** - Vector value.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteDVec3 ( dvec3 value )

Writes a 3-component *double* vector to the stream in accordance with the little-endian order.
### Arguments

- *dvec3* **value** - A *dvec3* value to write.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteDVec4 ( dvec4 value )

Writes a 4-component *double* vector to the stream in accordance with the little-endian order.
### Arguments

- *dvec4* **value** - A *dvec4* value to write.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteFloat ( float value )

Writes a floating-point number to the stream in accordance with the little-endian order.
### Arguments

- *float* **value** - A *float* value to write.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteFloatArray ( float[] OUT_src )

Writes an array of floating-point numbers to the stream in accordance with the little-endian order.
### Arguments

- *float[]* **OUT_src**

### Return value

true if the operation was successful; otherwise, false.
## bool WriteInt ( int value )

Writes a signed integer to the stream in accordance with the little-endian order.
### Arguments

- *int* **value** - An integer value to write.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteInt2 ( int value )

Writes a compact signed integer to the stream.
### Arguments

- *int* **value** - A compact signed integer to write.

### Return value

true if the compact integer is written successfully; otherwise, false.
## bool WriteIntArray ( int[] OUT_src )

Writes an array of signed integers to the stream in accordance with the little-endian order.
### Arguments

- *int[]* **OUT_src**

### Return value

true if the operation was successful; otherwise, false.
## bool WriteIVec2 ( ivec2 value )

Writes a 2-component integer vector to the stream in accordance with the little-endian order.
### Arguments

- *ivec2* **value** - Vector value.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteIVec3 ( ivec3 value )

Writes a 3-component integer vector to the stream in accordance with the little-endian order.
### Arguments

- *ivec3* **value** - An *ivec3* value to write.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteIVec4 ( ivec4 value )

Writes a 4-component integer vector to the stream in accordance with the little-endian order.
### Arguments

- *ivec4* **value** - An *ivec4* to write.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteLong ( long value )

Writes a signed long to the stream in accordance with the little-endian order.
### Arguments

- *long* **value** - A *long* value to write.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteLongArray ( llong[] OUT_src )

Writes an array of signed longs to the stream in accordance with the little-endian order.
### Arguments

- *llong[]* **OUT_src**

### Return value

true if the operation was successful; otherwise, false.
## bool WriteMat4 ( mat4 value )

Writes a *[mat4](../../../code/uniginescript/language/data_types.md#mat4)* (a matrix of float values, 4*16 bytes) to the stream in accordance with the little-endian order.
### Arguments

- *mat4* **value** - A matrix to write.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteMat44 ( mat4 value )

Writes the first 12 elements of 4x4 matrix in a binary format into the current stream. The last 4 elements of the matrix are discarded.
### Arguments

- *mat4* **value** - A 4x4 matrix.

### Return value

true if data is written successfully; otherwise, false.
## int WritePalette ( Palette value )

Writes the palette to the stream.
### Arguments

- *[Palette](../../../api/library/common/class.palette_cs.md)* **value** - Palette value.

## bool WriteQuat ( quat value )

Writes a quaternion to the stream in accordance with the little-endian order.
### Arguments

- *quat* **value** - A quaternion to write.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteShort ( short value )

Writes a signed short integer to the stream in accordance with the little-endian order.
### Arguments

- *short* **value** - A short integer value to write.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteShortArray ( short[] OUT_src )

Writes an array of signed short integers to the stream in accordance with the little-endian order.
### Arguments

- *short[]* **OUT_src**

### Return value

true if the operation was successful; otherwise, false.
## uint WriteStream ( Stream src , uint size )

Returns the number of bytes successfully read from the argument stream.
### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **src** - Stream to read data from.
- *uint* **size** - Size of data to be read from the stream.

### Return value

The number of bytes successfully read from the argument `src` stream.
## bool WriteString ( string str )

Writes a string in a binary format to the stream. Each binary string should be preceded by its length (4 bytes defining the length of string + the string itself).
### Arguments

- *string* **str** - String to write.

### Return value

true if the string is written successfully; otherwise, false.
## bool WriteString2 ( string str )

Writes a compact string in a binary format to the stream. Each binary string should be preceded by its length (the string length + the string itself). The string length is written as the compact signed integer.
### Arguments

- *string* **str** - String to write.

### Return value

true if the string is written successfully; otherwise, false.
## bool WriteUChar ( byte value )

Writes an unsigned character to the stream.
### Arguments

- *byte* **value** - Unsigned character to write.

### Return value

true if the unsigned character is written successfully; otherwise, false.
## bool WriteUInt ( uint value )

Writes a unsigned integer to the stream in accordance with the little-endian order.
### Arguments

- *uint* **value** - Data value.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteUInt2 ( uint value )

Writes a compact unsigned integer to the stream.
### Arguments

- *uint* **value** - Data value.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteUIntArray ( uint[] OUT_src )

Writes an array of unsigned integers to the stream in accordance with the little-endian order.
### Arguments

- *uint[]* **OUT_src**

### Return value

true if the operation was successful; otherwise, false.
## bool WriteUShort ( ushort value )

Writes a unsigned short integer to the stream in accordance with the little-endian order.
### Arguments

- *ushort* **value** - Unsigned short integer to write.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteUShortArray ( ushort[] OUT_src )

Writes an array of unsigned short integers to the stream in accordance with the little-endian order.
### Arguments

- *ushort[]* **OUT_src**

### Return value

true if the operation was successful; otherwise, false.
## bool WriteVec2 ( vec2 value )

Writes a 2-component vector to the stream in accordance with the little-endian order.
### Arguments

- *vec2* **value** - Vector value.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteVec3 ( vec3 value )

Writes a 3-component vector to the stream in accordance with the little-endian order.
### Arguments

- *vec3* **value** - A *vec3* to write.

### Return value

true if the operation was successful; otherwise, false.
## bool WriteVec4 ( vec4 value )

Writes a 4-component vector to the stream in accordance with the little-endian order.
### Arguments

- *vec4* **value** - A *vec4* to write.

### Return value

true if the operation was successful; otherwise, false.
