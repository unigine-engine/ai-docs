# Unigine::Stream Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class cannot be instantiated. It is a base class for:


- *[File](../../../api/library/filesystem/class.file_usc.md)* class
- *[Blob](../../../api/library/common/class.blob_usc.md)* class
- *[Socket](../../../api/library/networking/class.socket_usc.md)* class


*Stream* class allows you to write data into a stream, that is into files (stored on the disk), blobs (stored in system memory) and sockets (to be sent over the network), as well as read data from a stream.


## Stream Class

### Members

## void setByteOrder ( int order )

Sets a new value indicating the endianness of the stream: **0** value is for LSB (least significant), **1** is for MSB (most significant).
### Arguments

- *int* **order** - The value indicating the endianness of the stream: **0** value is for LSB (least significant), **1** is for MSB (most significant).

## int getByteOrder () const

Returns the current value indicating the endianness of the stream: **0** value is for LSB (least significant), **1** is for MSB (most significant).
### Return value

Current value indicating the endianness of the stream: **0** value is for LSB (least significant), **1** is for MSB (most significant).
## int isAvailable () const

Returns the current value indicating if stream data is available.
### Return value

Current stream data is available
## int isOpened () const

Returns the current value indicating if the stream is opened.
### Return value

Current there is a read/write error
## int getType () const

Returns the current [the type](#BLOB) of the stream.
### Return value

Current [value](#BLOB) indicating the type of the stream.
---

## int isError ( )

Checks whether the stream has a read/write error.
### Return value

**1** if there is a read/write error; otherwise, **0**.
## gets ( )

Reads the stream data from the current position.
### Return value

Stream data starting from the current position.
## int puts ( )

Writes a non-binary string of characters to the stream.
### Arguments

### Return value

1 if a string of characters is written successfully; otherwise, 0.
## read ( )

Reads unsigned char data in a binary format from the stream into a [vector](../../../code/uniginescript/language/containers/index.md#vector).
### Arguments

### Return value

**1** if data is read successfully; otherwise, **0**.
## dmat4 readDMat4 ( )

Reads *[dmat4](../../../code/uniginescript/language/data_types.md#dmat4)* (a matrix of double values, 8*12 bytes) in a binary format from the stream.
### Return value

Received matrix.
## double readDouble ( )

Reads a *[double](../../../code/uniginescript/language/data_types.md#double)* in a binary format (8 bytes) from the stream.
### Return value

Received *double*.
## dvec2 readDVec2 ( )

Reads a 2-component double vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## dvec3 readDVec3 ( )

Reads a *[dvec3](../../../code/uniginescript/language/data_types.md#dvec3)* in a binary format (8*3 bytes) from the stream.
### Return value

Received *dvec3*.
## dvec4 readDVec4 ( )

Reads a *[dvec4](../../../code/uniginescript/language/data_types.md#dvec4)* in a binary format (8*4 bytes) from the stream.
### Return value

Received *dvec4*.
## float readFloat ( )

Reads a *[float](../../../code/uniginescript/language/data_types.md#float)* in a binary format (4 bytes) from the stream.
### Return value

Received *float*
## int readInt ( )

Reads an *[integer](../../../code/uniginescript/language/data_types.md#int)* in a binary format (4 bytes) from the stream.
### Return value

Received *integer*.
## int readInt2 ( )

Reads a compact signed integer in a binary format from the stream.
### Return value

Received number.
## ivec2 readIVec2 ( )

Reads a 2-component integer vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## ivec3 readIVec3 ( )

Reads an *[ivec3](../../../code/uniginescript/language/data_types.md#ivec3)* in a binary format (4*3 bytes) from the stream.
### Return value

Received *ivec3*.
## ivec4 readIVec4 ( )

Reads an *[ivec4](../../../code/uniginescript/language/data_types.md#ivec4)* in a binary format (4*4 bytes) from the stream.
### Return value

Received *ivec4*.
## readLine ( )

Reads a line of non-binary characters from the stream: starting from the current position until the end of line is reached ("\n"). The maximum length of the line is 4096 bytes.
### Return value

Received line.
## long readLong ( )

Reads a *[long integer](../../../code/uniginescript/language/data_types.md#long)* in a binary format (8 bytes) from the stream.
### Return value

Received *long integer*.
## mat4 readMat4 ( )

Reads a *[mat4](../../../code/uniginescript/language/data_types.md#mat4)* (a matrix in a binary format, 4*16 bytes) from the stream.
### Return value

Received matrix.
## mat4 readMat44 ( )

Reads the first 12 elements of 4x4 matrix from the current stream. The last 4 elements of the matrix are discarded.
### Return value

4x4 matrix with 12 read elements (the last four elements are equal to 0 0 0 1).
## Palette readPalette ( )

Reads a palette from the current stream.
### Return value

Palette value.
## quat readQuat ( )

Reads a *[quaternion](../../../code/uniginescript/language/data_types.md#quat)* in a binary format (4*4 bytes) from the stream.
### Return value

Received quaternion.
## short readShort ( )

Reads a short integer in a binary format (2 bytes) from the stream.
### Return value

Received short integer.
## readStream ( )

### Arguments

### Return value

## readString ( )

Reads a compact string in a binary format from the stream. Each binary string should be preceded by its length (the string length + the string itself). The string length is written as the compact signed integer.
### Return value

Received string.
## readToken ( )

Reads a token from the stream. A token is a single word delimited by white space or a string in quotes, for example, "word" or "many words". A token is read starting from the current position up to the white space or line feed ("\n"), or if the first character is a double quote mark (") up to the second double quote mark (returned token will not contain any quotes). The maximum length of the string is 4096 bytes.
### Return value

Received token.
## readUChar ( )

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
## int readUShort ( )

Reads an unsigned short integer from the stream.
### Return value

Received unsigned short integer.
## vec2 readVec2 ( )

Reads a 2-component vector from the stream in accordance with the little-endian order.
### Return value

Vector value.
## vec3 readVec3 ( )

Reads a *[vec3](../../../code/uniginescript/language/data_types.md#vec3)* in a binary format (4*3 bytes) from the stream.
### Return value

Received *vec3*.
## vec4 readVec4 ( )

Reads a *[vec4](../../../code/uniginescript/language/data_types.md#vec4)* in a binary format (4*4 bytes) from the stream.
### Return value

Received *vec4*.
## write ( )

Writes contents of a [vector](../../../code/uniginescript/language/containers/index.md#vector) into the stream as unsigned char data in a binary format.
### Arguments

### Return value

**1** if data is sent successfully; otherwise, **0**.
## bool writeChar ( )

Writes an ASCII character in a binary format (1 byte) to the stream.
### Arguments

### Return value

true if a character is written successfully; otherwise false.
## int writeDMat4 ( dmat4 value )

Writes a *[dmat4](../../../code/uniginescript/language/data_types.md#dmat4)* (a matrix of double values, 8*12 bytes) to the stream.
### Arguments

- *dmat4* **value** - A matrix to write.

### Return value

**1** if the matrix is written successfully; otherwise, **0**.
## int writeDouble ( double value )

Writes a *[double](../../../code/uniginescript/language/data_types.md#double)* (8 bytes) in a binary format to the stream.
### Arguments

- *double* **value** - A *double* value to write.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeDVec2 ( dvec2 value )

Writes a 2-component *double* vector to the stream in accordance with the little-endian order.
### Arguments

- *dvec2* **value** - Vector value.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeDVec3 ( dvec3 value )

Writes a *[dvec3](../../../code/uniginescript/language/data_types.md#dvec3)* in a binary format (8*3 bytes) to the stream.
### Arguments

- *dvec3* **value** - A *dvec3* value to write.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeDVec4 ( dvec4 value )

Writes a *[dvec4](../../../code/uniginescript/language/data_types.md#dvec4)* in a binary format (8*4 bytes) to the stream.
### Arguments

- *dvec4* **value** - A *dvec4* value to write.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeFloat ( float value )

Writes a *[float](../../../code/uniginescript/language/data_types.md#float)* (4 bytes) in a binary format to the stream.
### Arguments

- *float* **value** - A *float* value to write.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeInt ( int value )

Writes an *[integer](../../../code/uniginescript/language/data_types.md#int)* (4 bytes) in a binary format to the stream.
### Arguments

- *int* **value** - An integer value to write.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeInt2 ( int value )

Writes a compact signed integer in a binary format to the stream.
### Arguments

- *int* **value** - A compact signed integer to write.

### Return value

**1** if the compact integer is written successfully; otherwise, **0**.
## int writeIVec2 ( ivec2 value )

Writes a 2-component integer vector to the stream in accordance with the little-endian order.
### Arguments

- *ivec2* **value** - Vector value.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeIVec3 ( ivec3 value )

Writes a *[ivec3](../../../code/uniginescript/language/data_types.md#ivec3)* in a binary format (4*3 bytes) to the stream.
### Arguments

- *ivec3* **value** - An *ivec3* value to write.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeIVec4 ( ivec4 value )

Writes an *[ivec4](../../../code/uniginescript/language/data_types.md#ivec4)* in a binary format (4*4 bytes) to the stream.
### Arguments

- *ivec4* **value** - An *ivec4* to write.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeLong ( long value )

Writes a *[long integer](../../../code/uniginescript/language/data_types.md#long)* (8 bytes) in a binary format to the stream.
### Arguments

- *long* **value** - A *long* value to write.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeMat4 ( mat4 value )

Writes a *[mat4](../../../code/uniginescript/language/data_types.md#mat4)* (a matrix of float values, 4*16 bytes) to the stream in accordance with the little-endian order.
### Arguments

- *mat4* **value** - A matrix to write.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeMat44 ( mat4 value )

Writes the first 12 elements of 4x4 matrix in a binary format into the current stream. The last 4 elements of the matrix are discarded.
### Arguments

- *mat4* **value** - A 4x4 matrix.

### Return value

**1** if data is written successfully; otherwise, **0**.
## int writePalette ( Palette value )

Writes the palette to the stream.
### Arguments

- *[Palette](../../../api/library/common/class.palette_usc.md)* **value** - Palette value.

## int writeQuat ( quat value )

Writes a *[quaternion](../../../code/uniginescript/language/data_types.md#quat)* in a binary format (4*4 bytes) to the stream.
### Arguments

- *quat* **value** - A quaternion to write.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeShort ( short value )

Writes a short integer in a binary format (2 bytes) to the stream.
### Arguments

- *short* **value** - A short integer value to write.

### Return value

**1** if the operation was successful; otherwise, **0**.
## writeStream ( )

### Arguments

### Return value

## bool writeString ( )

Writes a string in a binary format to the stream. Each binary string should be preceded by its length (4 bytes defining the length of string + the string itself).
### Arguments

### Return value

true if the string is written successfully; otherwise, false.
## bool writeString2 ( )

Writes a compact string in a binary format to the stream. Each binary string should be preceded by its length (the string length + the string itself). The string length is written as the compact signed integer.
### Arguments

### Return value

true if the string is written successfully; otherwise, false.
## bool writeUChar ( )

Writes an unsigned character to the stream.
### Arguments

### Return value

true if the unsigned character is written successfully; otherwise, false.
## int writeUInt ( unsigned int value )

Writes a unsigned integer to the stream in accordance with the little-endian order.
### Arguments

- *unsigned int* **value** - Data value.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeUInt2 ( unsigned int value )

Writes a compact unsigned integer to the stream.
### Arguments

- *unsigned int* **value** - Data value.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeUShort ( int value )

Writes a unsigned short integer to the stream.
### Arguments

- *int* **value** - Unsigned short integer to write.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeVec2 ( vec2 value )

Writes a 2-component vector to the stream in accordance with the little-endian order.
### Arguments

- *vec2* **value** - Vector value.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeVec3 ( vec3 value )

Writes a *[vec3](../../../code/uniginescript/language/data_types.md#vec3)* in a binary format (4*3 bytes) to the stream.
### Arguments

- *vec3* **value** - A *vec3* to write.

### Return value

**1** if the operation was successful; otherwise, **0**.
## int writeVec4 ( vec4 value )

Writes a *[vec4](../../../code/uniginescript/language/data_types.md#vec4)* in a binary format (4*4 bytes) to the stream.
### Arguments

- *vec4* **value** - A *vec4* to write.

### Return value

**1** if the operation was successful; otherwise, **0**.
