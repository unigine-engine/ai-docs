# Unigine::Blob Class (CS)

**Inherits from:** Stream


This class is used to store data in the memory (unlike *[File](../../../api/library/filesystem/class.file_cs.md)* which is stored on the disk). The blob uses either an Unigine allocator (if `#define USE_MEMORY` is set, by default) or a system allocator.


### Example


The code below illustrates the following process:


- Packing data to a blob and saving compressed data to a [file](../../../api/library/filesystem/class.file_cs.md)
- Reading and uncompressing data from the file to the destination blob
- Reading data from the destination blob


```csharp
// creating a source blob to store data
Blob blob1 = new Blob();

// creating a file to save our blob's data to
File file = new File("test.dat", "w+");

// clearing a blob
blob1.Clear();

// writing data to a blob (prefix, vector, and postfix)
blob1.WriteChar((byte)'B');
blob1.WriteVec3(new vec3(0.1f, 0.2f, 0.3f));
blob1.WriteChar((byte)'E');

// compressing blob's data with low compression and saving it to the file
blob1.Compress(file, 0);

// closing the file
file.Close();

// clearing a blob
blob1.Clear();

// opening the data file for reading
file.Open("test.dat", "r");

// creating a second blob
Blob blob2 = new Blob();

// reading and decompressing data from the file
blob2.Decompress(file);

// closing the file
file.Close();

// setting current position to the beginning of the blob
blob2.SeekSet(0);

// reading data from a blob (prefix, vector and postfix)
char pref = (char)blob2.ReadChar();
vec3 v = blob2.ReadVec3();
char postf = (char)blob2.ReadChar();

// reporting the decoded blob data and SHA1 checksum
Log.Message("\nDESTINATION: [{0}] vec({1}, {2}, {3}) [{4}] - SHA1 checksum ({5})", pref, v.x, v.y, v.z, postf, blob2.GetSHA1());

// clearing a blob
blob2.Clear();


```


## Blob Class

### Members

---

## Blob ( uint size = 0 )

Constructor. Creates a new blob of the specified size.
### Arguments

- *uint* **size** - Blob size.

## void Set ( uint offset , byte value )

Sets the value of the specified byte in the blob.
### Arguments

- *uint* **offset** - The offset in the blob.
- *byte* **value** - The byte value.

## byte get ( uint offset )

Returns the value of the specified byte in the blob.
### Arguments

- *uint* **offset** - The offset, in bytes.

### Return value

The byte value.
## int Getc ( )

Returns the next symbol from the blob.
### Return value

Character read from the blob.
## string GetCRC32 ( )

Returns the 32-bit CRC checksum.
### Return value

The 32-bit CRC checksum.
## void SetData ( byte[] OUT_data , uint size )


Sets new data to the Blob instance.


> **Notice:** You should manage the previously stored data manually.


### Arguments

- *byte[]* **OUT_data** - Data to set to the Blob instance. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *uint* **size** - The size of the blob.

## IntPtr GetData ( )

Returns the current blob data.
### Return value

Blob data.
## string GetMD5 ( )

Returns a 128-bit MD5 checksum.
### Return value

128-bit MD5 checksum.
## string GetSHA1 ( )

Returns a 160-bit SHA1 checksum.
### Return value

160-bit SHA1 checksum.
## string GetSHA256 ( )

Returns a 256-bit SHA256 checksum.
### Return value

256-bit SHA256 checksum.
## uint GetSize ( )

Returns the current size of the blob.
### Return value

Blob size.
## void Allocate ( uint size )


Allocates the required memory without resizing the blob.


> **Notice:** The blob will be resized dynamically when the allocated memory is filled.


### Arguments

- *uint* **size** - Size of the allocated memory, in bytes.

## void Clear ( )

Clears the size of the blob to **0**.
## int Compress ( Stream dest , int quality )


Compresses the blob and writes it into the given stream.


> **Notice:** This method uses zlib compression which is better than Lz4 (see the *[compressLz4()](#compressLz4_Stream_int_int)* method), but significantly slower.


### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **dest** - Destination stream.
- *int* **quality** - Compression quality (**0** is for a fast compression, **1** is for a small size).

### Return value

**1** if the data is compressed successfully; otherwise, **0**.
## int CompressLz4 ( Stream dest , int quality )

Compresses the blob with Lz4 algorithm and writes it into the given stream.
### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **dest** - Destination stream.
- *int* **quality** - Compression quality (**0** is for a fast compression, **1** is for a small size).

### Return value

**1** if the data is successfully compressed; otherwise, **0**.
## int Decode ( string src )

Decodes a base64 encoded string into the blob.
### Arguments

- *string* **src** - Source base64 encoded string.

### Return value

**1** if the data is decoded successfully; otherwise, **0**.
## int DecodeZBase32 ( string src )

Decodes a Zbase32 encoded string into the blob.
### Arguments

- *string* **src** - Source Zbase32 encoded string.

### Return value

Returns **1** if the data is decoded successfully; otherwise, **0**.
## int Decompress ( Stream src )

Reads and decompresses a previously [compressed](#compress_Stream_int_int) blob from a given stream.
### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **src** - Source stream to read data from.

### Return value

**1** if the blob is decompressed successfully; otherwise, **0**.
## int DecompressLz4 ( Stream src )

Reads and decompresses a previously [compressed](#compressLz4_Stream_int_int) blob with Lz4 algorithm from a given stream.
### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **src** - Source stream to read data from.

### Return value

**1** if the blob is successfully decompressed; otherwise, **0**.
## string Encode ( )

Encodes the blob into the base64 encoded string.
### Return value

Base64 encoded string.
## string EncodeZBase32 ( )

Encodes the blob into the ZBase32 encoded string.
### Return value

ZBase32 encoded string.
## int Eof ( )

Checks if the end of the blob has been reached.
### Return value

**1** if the end of blob is reached; otherwise, **0**.
## int Flush ( )

Flushes the blob. This function has an empty body; it is created for *Blob* class to have the same number of methods as the *[File](../../../api/library/filesystem/class.file_cs.md)* class has.
### Return value

**1** if the blob is successfully flushed; otherwise, **0**.
## void Reserve ( uint size )

Reserves the blob, i.e. allocates *(size * 1.5)* bytes without resizing the blob.
> **Notice:** The blob will be resized dynamically when the allocated memory is filled.


### Arguments

- *uint* **size** - Size of the allocated memory, in bytes.

## void Resize ( uint size )

Allocates the required memory and resizes the blob.
### Arguments

- *uint* **size** - Size of the blob, in bytes.

## int SeekCur ( uint offset )

Seeks the position relative to the current offset.
### Arguments

- *uint* **offset** - Offset from the current position of the indicator, in bytes.

### Return value

**1** if the blob position indicator is set successfully; otherwise, 0.
## int SeekEnd ( uint offset )

Seeks to position relative to the end of the blob.
### Arguments

- *uint* **offset** - Offset from the end of the blob, in bytes.

### Return value

**1** if the blob position indicator is set successfully; otherwise, **0**.
## int SeekSet ( uint offset )

Seeks to position relative to the start of the blob.
### Arguments

- *uint* **offset** - Offset from the beginning of the blob, in bytes.

### Return value

**1** if the blob position indicator is successfully set; otherwise, **0**.
## uint Tell ( )

Returns the current blob offset position indicator.
### Return value

Current blob offset.
