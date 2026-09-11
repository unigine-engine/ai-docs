# Unigine::Compress Class (CPP)

**Header:** #include <UnigineCompress.h>


Compress class is used to compress and decompress data using the following algorithms:


- **Jackalless** � recommended. UNIGINE compression method optimized for compressing 2D and 3D textures. It provides better results than **LZ4** and **Zlib** without deteriorating the quality.
- **LZ4** � temporary option, planned to be removed in the upcoming releases.
- **Zlib** � for high compression ratio (can provide up to 2 times higher compression ratio, but takes up to 20 times longer).


## Compress Class

---

## bool zlibCompress ( void* dest , size_t& dest_size , const void* src , size_t src_size , bool quality )

Compresses the source data using the Zlib algorithm with the specified compression level and puts the result to the specified destination.
### Arguments

- *void** **dest** - Destination buffer pointer.
- *size_t&* **dest_size** - Destination data size.
- *const void** **src** - Source buffer pointer.
- *size_t* **src_size** - Source data size.
- *bool* **quality** - Compression quality; false is for faster compression, true is for higher compression (less size).

### Return value

true if the operation was successful; otherwise, false.
## bool zlibDecompress ( void* dest , size_t dest_size , const void* src , size_t src_size )

Decompresses the source data using the Zlib algorithm and puts the result to the specified destination.
### Arguments

- *void** **dest** - Destination buffer pointer.
- *size_t* **dest_size** - Destination data size.
- *const void** **src** - Source buffer pointer.
- *size_t* **src_size** - Source data size.

### Return value

true if the operation was successful; otherwise, false.
## size_t zlibSize ( size_t size )

Returns the maximum Zlib-compressed data size for the specified uncompressed size value.
### Arguments

- *size_t* **size** - Uncompressed data size.

### Return value

Maximum Zlib-compressed data size.
## size_t lz4Size ( size_t size )

Returns the maximum LZ4-compressed data size for the specified uncompressed size value.
### Arguments

- *size_t* **size** - Uncompressed data size.

### Return value

Maximum lz4-compressed data size.
## bool lz4Compress ( void* dest , size_t& dest_size , const void* src , size_t src_size , bool quality )

Compresses the source data using the LZ4 algorithm with the specified compression level and puts the result to the specified destination.
### Arguments

- *void** **dest** - Destination buffer pointer.
- *size_t&* **dest_size** - Destination data size.
- *const void** **src** - Source buffer pointer.
- *size_t* **src_size** - Source data size.
- *bool* **quality** - Compression quality; false is for faster compression, true is for higher compression (less size).

### Return value

true if the operation was successful; otherwise, false.
## bool lz4Decompress ( void* dest , size_t dest_size , const void* src , size_t src_size )

Decompresses the source data using the LZ4 algorithm and puts the result to the specified destination.
### Arguments

- *void** **dest** - Destination buffer pointer.
- *size_t* **dest_size** - Destination data size.
- *const void** **src** - Source buffer pointer.
- *size_t* **src_size** - Source data size.

### Return value

true if the operation was successful; otherwise, false.
## size_t jackallessSize ( size_t size )

Returns the maximum size of data compressed using jackalless method for the specified uncompressed size value.
### Arguments

- *size_t* **size** - Uncompressed data size.

### Return value

Maximum size of data compressed using jackalless method.
## bool jackallessCompress ( void* dest , size_t& dest_size , const void* src , size_t src_size )

Compresses the source data using jackalless method and puts the result to the specified destination.
### Arguments

- *void** **dest** - Destination buffer pointer.
- *size_t&* **dest_size** - Destination data size.
- *const void** **src** - Source buffer pointer.
- *size_t* **src_size** - Source data size.

### Return value

true if the operation was successful; otherwise, false.
## bool jackallessDecompress ( void* dest , const void* src )

Decompresses the source data using jackalless method and puts the result to the specified destination.
### Arguments

- *void** **dest** - Destination buffer pointer.
- *const void** **src** - Source buffer pointer.

### Return value

true if the operation was successful; otherwise, false.
## bool jackallessCompressFloat ( void* dest , size_t& dest_size , const float* src , size_t src_length )

Compresses the source data using jackalless method and puts the result to the specified destination.
### Arguments

- *void** **dest** - Destination buffer pointer.
- *size_t&* **dest_size** - Destination data size.
- *const float** **src** - Source buffer pointer.
- *size_t* **src_length** - Source data length.

### Return value

true if the operation was successful; otherwise, false.
## bool jackallessDecompressFloat ( float* dest , size_t dest_length , const void* src )

Decompresses the source data using jackalless method and puts the result to the specified destination.
### Arguments

- *float** **dest** - Destination buffer pointer.
- *size_t* **dest_length** - Destination data length.
- *const void** **src** - Source buffer pointer.

### Return value

true if the operation was successful; otherwise, false.
## size_t jackallessRawSize ( void* compressed_data )

Returns the raw size of the compressed data.
### Arguments

- *void** **compressed_data** - Compressed data pointer.

### Return value

Raw data size.
## size_t jackallessCompressedSize ( void* compressed_data )

Returns the compressed size of the compressed data.
### Arguments

- *void** **compressed_data** - Compressed data pointer.

### Return value

Compressed data size.
