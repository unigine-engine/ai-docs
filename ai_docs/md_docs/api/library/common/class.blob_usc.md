# Unigine::Blob Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Stream


This class is used to store data in the memory (unlike *[File](../../../api/library/filesystem/class.file_usc.md)* which is stored on the disk). The blob uses either an Unigine allocator (if `#define USE_MEMORY` is set, by default) or a system allocator.


### Example


The code below illustrates the following process:


- Packing data to a blob and saving compressed data to a [file](../../../api/library/filesystem/class.file_usc.md)
- Reading and uncompressing data from the file to the destination blob
- Reading data from the destination blob


```cpp
// creating a source blob to store data
Blob blob1 = new Blob();

// creating a file to save our blob's data to
File file = new File("test.dat", "w+");

// clearing a blob
blob1.clear();

// writing data to a blob (prefix, vector and postfix)
blob1.writeChar('B');
blob1.writeVec3(vec3(0.1f, 0.2f, 0.3f));
blob1.writeChar('E');

// compressing blob's data with low compression and saving it to the file
blob1.compress(file, 0);

// closing the file
file.close();

// deleting a blob
delete blob1;

// opening the data file for reading
file.open("test.dat", "r");

// creating a second blob
Blob blob2 = new Blob();

// reading and decompressing data from the file
blob2.decompress(file);

// closing the file
file.close();
delete file;

// setting current position to the beginning of the blob
blob2.seekSet(0);

// reading data from a blob (prefix, vector and postfix)
int pref = blob2.readChar();
vec3 v = blob2.readVec3();
int postf = blob2.readChar();

// reporting the decoded blob data and SHA1 checksum
log.message("\nDESTINATION: [%c] vec(%f, %f, %f) [%c] - SHA1 checksum (%s)", pref, v.x, v.y, v.z, postf, blob2.getSHA1());

// deleting a blob
delete blob2;

```


## Blob Class

---

## static Blob ( int size = 0 )

Constructor. Creates a new blob of the specified size.
### Arguments

- *int* **size** - Blob size.

## void set ( int offset , int value )

Sets the value of the specified byte in the blob.
### Arguments

- *int* **offset** - The offset in the blob.
- *int* **value** - The byte value.

## int get ( int offset )

Returns the value of the specified byte in the blob.
### Arguments

- *int* **offset** - The offset, in bytes.

### Return value

The byte value.
## int getc ( )

Returns the next symbol from the blob.
### Return value

Character read from the blob.
## String getCRC32 ( )

Returns the 32-bit CRC checksum.
### Return value

The 32-bit CRC checksum.
## String getMD5 ( )

Returns a 128-bit MD5 checksum.
### Return value

128-bit MD5 checksum.
## String getSHA1 ( )

Returns a 160-bit SHA1 checksum.
### Return value

160-bit SHA1 checksum.
## String getSHA256 ( )

Returns a 256-bit SHA256 checksum.
### Return value

256-bit SHA256 checksum.
## int getSize ( )

Returns the current size of the blob.
### Return value

Blob size.
## void allocate ( int size )


Allocates the required memory without resizing the blob.


> **Notice:** The blob will be resized dynamically when the allocated memory is filled.


### Arguments

- *int* **size** - Size of the allocated memory, in bytes.

## void clear ( )

Clears the size of the blob to **0**.
## int compress ( Stream dest , int quality )


Compresses the blob and writes it into the given stream.


> **Notice:** This method uses zlib compression which is better than Lz4 (see the *[compressLz4()](#compressLz4_Stream_int_int)* method), but significantly slower.


### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **dest** - Destination stream.
- *int* **quality** - Compression quality (**0** is for a fast compression, **1** is for a small size).

### Return value

**1** if the data is compressed successfully; otherwise, **0**.
## int compressLz4 ( Stream dest , int quality )

Compresses the blob with Lz4 algorithm and writes it into the given stream.
### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **dest** - Destination stream.
- *int* **quality** - Compression quality (**0** is for a fast compression, **1** is for a small size).

### Return value

**1** if the data is successfully compressed; otherwise, **0**.
## int decode ( string src )

Decodes a base64 encoded string into the blob.
### Arguments

- *string* **src** - Source base64 encoded string.

### Return value

**1** if the data is decoded successfully; otherwise, **0**.
## int decodeZBase32 ( string src )

Decodes a Zbase32 encoded string into the blob.
### Arguments

- *string* **src** - Source Zbase32 encoded string.

### Return value

Returns **1** if the data is decoded successfully; otherwise, **0**.
## int decompress ( Stream src )

Reads and decompresses a previously [compressed](#compress_Stream_int_int) blob from a given stream.
### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **src** - Source stream to read data from.

### Return value

**1** if the blob is decompressed successfully; otherwise, **0**.
## int decompressLz4 ( Stream src )

Reads and decompresses a previously [compressed](#compressLz4_Stream_int_int) blob with Lz4 algorithm from a given stream.
### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **src** - Source stream to read data from.

### Return value

**1** if the blob is successfully decompressed; otherwise, **0**.
## encode ( )

Encodes the blob into the base64 encoded string.
### Return value

Base64 encoded string.
## int eof ( )

Checks if the end of the blob has been reached.
### Return value

**1** if the end of blob is reached; otherwise, **0**.
## int flush ( )

Flushes the blob. This function has an empty body; it is created for *Blob* class to have the same number of methods as the *[File](../../../api/library/filesystem/class.file_usc.md)* class has.
### Return value

**1** if the blob is successfully flushed; otherwise, **0**.
## void reserve ( int size )

Reserves the blob, i.e. allocates *(size * 1.5)* bytes without resizing the blob.
> **Notice:** The blob will be resized dynamically when the allocated memory is filled.


### Arguments

- *int* **size** - Size of the allocated memory, in bytes.

## void resize ( int size )

Allocates the required memory and resizes the blob.
### Arguments

- *int* **size** - Size of the blob, in bytes.

## int seekCur ( int offset )

Seeks the position relative to the current offset.
### Arguments

- *int* **offset** - Offset from the current position of the indicator, in bytes.

### Return value

**1** if the blob position indicator is set successfully; otherwise, 0.
## int seekEnd ( int offset )

Seeks to position relative to the end of the blob.
### Arguments

- *int* **offset** - Offset from the end of the blob, in bytes.

### Return value

**1** if the blob position indicator is set successfully; otherwise, **0**.
## int seekSet ( int offset )

Seeks to position relative to the start of the blob.
### Arguments

- *int* **offset** - Offset from the beginning of the blob, in bytes.

### Return value

**1** if the blob position indicator is successfully set; otherwise, **0**.
## int tell ( )

Returns the current blob offset position indicator.
### Return value

Current blob offset.
