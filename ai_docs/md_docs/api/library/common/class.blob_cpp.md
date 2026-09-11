# Unigine::Blob Class (CPP)

**Header:** #include <UnigineStreams.h>

**Inherits from:** Stream


This class is used to store data in the memory (unlike *[File](../../../api/library/filesystem/class.file_cpp.md)* which is stored on the disk). The blob uses either an Unigine allocator (if `#define USE_MEMORY` is set, by default) or a system allocator.


### Example


The code below illustrates the following process:


- Packing data to a blob and saving compressed data to a [file](../../../api/library/filesystem/class.file_cpp.md)
- Reading and uncompressing data from the file to the destination blob
- Reading data from the destination blob


```cpp
// creating a source blob to store data
BlobPtr blob1 = Blob::create();

// creating a file to save our blob's data to
FilePtr file = File::create("test.dat", "w+");

// clearing a blob
blob1->clear();

// writing data to a blob (prefix, vector and postfix)
blob1->writeChar('B');
blob1->writeVec3(Math::vec3(0.1f, 0.2f, 0.3f));
blob1->writeChar('E');

// compressing blob's data with low compression and saving it to the file
blob1->compress(file, 0);

// closing the file
file->close();

// clearing a blob
blob1.clear();

// opening the data file for reading
file->open("test.dat", "r");

// creating a second blob
BlobPtr blob2 = Blob::create();

// reading and decompressing data from the file
blob2->decompress(file);

// closing the file
file->close();

// setting current position to the beginning of the blob
blob2->seekSet(0);

// reading data from a blob (prefix, vector and postfix)
char pref = blob2->readChar();
Math::vec3 v = blob2->readVec3();
char postf = blob2->readChar();

// reporting the decoded blob data and SHA1 checksum
Log::message("\nDESTINATION: [%c] vec(%f, %f, %f) [%c] - SHA1 checksum (%s)", pref, v.x, v.y, v.z, postf, blob2->getSHA1().get());

// clearing a blob
blob2.clear();


```


## Blob Class

---

## static BlobPtr create ( size_t size = 0 )

Constructor. Creates a new blob of the specified size.
### Arguments

- *size_t* **size** - Blob size.

## void set ( size_t offset , unsigned char value )

Sets the value of the specified byte in the blob.
### Arguments

- *size_t* **offset** - The offset in the blob.
- *unsigned char* **value** - The byte value.

## unsigned char get ( size_t offset )

Returns the value of the specified byte in the blob.
### Arguments

- *size_t* **offset** - The offset, in bytes.

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
## void setData ( unsigned char * OUT_data , size_t size )


Sets new data to the Blob instance.


> **Notice:** You should manage the previously stored data manually.


### Arguments

- *unsigned char ** **OUT_data** - Data to set to the Blob instance. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *size_t* **size** - The size of the blob.

## unsigned char * getData ( )

Returns the current blob data.
### Return value

Blob data.
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
## size_t getSize ( )

Returns the current size of the blob.
### Return value

Blob size.
## void allocate ( size_t size )


Allocates the required memory without resizing the blob.


> **Notice:** The blob will be resized dynamically when the allocated memory is filled.


### Arguments

- *size_t* **size** - Size of the allocated memory, in bytes.

## void clear ( )

Clears the size of the blob to **0**.
## int compress ( const Ptr < Stream > & dest , int quality )


Compresses the blob and writes it into the given stream.


> **Notice:** This method uses zlib compression which is better than Lz4 (see the *[compressLz4()](#compressLz4_Stream_int_int)* method), but significantly slower.


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **dest** - Destination stream.
- *int* **quality** - Compression quality (**0** is for a fast compression, **1** is for a small size).

### Return value

**1** if the data is compressed successfully; otherwise, **0**.
## int compressLz4 ( const Ptr < Stream > & dest , int quality )

Compresses the blob with Lz4 algorithm and writes it into the given stream.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **dest** - Destination stream.
- *int* **quality** - Compression quality (**0** is for a fast compression, **1** is for a small size).

### Return value

**1** if the data is successfully compressed; otherwise, **0**.
## int decode ( const char * src )

Decodes a base64 encoded string into the blob.
### Arguments

- *const char ** **src** - Source base64 encoded string.

### Return value

**1** if the data is decoded successfully; otherwise, **0**.
## int decodeZBase32 ( const char * src )

Decodes a Zbase32 encoded string into the blob.
### Arguments

- *const char ** **src** - Source Zbase32 encoded string.

### Return value

Returns **1** if the data is decoded successfully; otherwise, **0**.
## int decompress ( const Ptr < Stream > & src )

Reads and decompresses a previously [compressed](#compress_Stream_int_int) blob from a given stream.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **src** - Source stream to read data from.

### Return value

**1** if the blob is decompressed successfully; otherwise, **0**.
## int decompressLz4 ( const Ptr < Stream > & src )

Reads and decompresses a previously [compressed](#compressLz4_Stream_int_int) blob with Lz4 algorithm from a given stream.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Stream](../../../api/library/common/class.stream_cpp.md)> &* **src** - Source stream to read data from.

### Return value

**1** if the blob is successfully decompressed; otherwise, **0**.
## String encode ( )

Encodes the blob into the base64 encoded string.
### Return value

Base64 encoded string.
## String encodeZBase32 ( )

Encodes the blob into the ZBase32 encoded string.
### Return value

ZBase32 encoded string.
## int eof ( )

Checks if the end of the blob has been reached.
### Return value

**1** if the end of blob is reached; otherwise, **0**.
## int flush ( )

Flushes the blob. This function has an empty body; it is created for *Blob* class to have the same number of methods as the *[File](../../../api/library/filesystem/class.file_cpp.md)* class has.
### Return value

**1** if the blob is successfully flushed; otherwise, **0**.
## void reserve ( size_t size )

Reserves the blob, i.e. allocates *(size * 1.5)* bytes without resizing the blob.
> **Notice:** The blob will be resized dynamically when the allocated memory is filled.


### Arguments

- *size_t* **size** - Size of the allocated memory, in bytes.

## void resize ( size_t size )

Allocates the required memory and resizes the blob.
### Arguments

- *size_t* **size** - Size of the blob, in bytes.

## int seekCur ( size_t offset )

Seeks the position relative to the current offset.
### Arguments

- *size_t* **offset** - Offset from the current position of the indicator, in bytes.

### Return value

**1** if the blob position indicator is set successfully; otherwise, 0.
## int seekEnd ( size_t offset )

Seeks to position relative to the end of the blob.
### Arguments

- *size_t* **offset** - Offset from the end of the blob, in bytes.

### Return value

**1** if the blob position indicator is set successfully; otherwise, **0**.
## int seekSet ( size_t offset )

Seeks to position relative to the start of the blob.
### Arguments

- *size_t* **offset** - Offset from the beginning of the blob, in bytes.

### Return value

**1** if the blob position indicator is successfully set; otherwise, **0**.
## size_t tell ( )

Returns the current blob offset position indicator.
### Return value

Current blob offset.
