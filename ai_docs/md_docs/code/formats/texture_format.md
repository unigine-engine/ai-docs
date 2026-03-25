# Texture File Format


**TEXTURE** is a native UNIGINE file format for storing image data. It supports a wide range of pixel formats (from 8-bit integer to 32-bit float, including compressed DXT/BC formats), multiple image types (2D, 3D, Cube, arrays), mipmaps, and optional file-level compression (*ZLib* or *LZ4*). The format is used for all textures in the Engine - diffuse maps, normal maps, environment cubemaps, etc.


The `*.texture` file stores its data using the [Image](../../api/library/common/class.image_cpp.md) class.


Here are some general notes on the format:


- All data is in the little-endian notation.
- *char* is a signed 8-bit integer.
- *unsigned char* is an unsigned 8-bit integer.
- *unsigned short* is an unsigned 16-bit integer. It has a range of **0** to **65,535**.
- *int32* is a signed 32-bit integer.
- *int64* is a signed 64-bit integer.


## Storing Textures


The `*.texture` file consists of a magic number, a compact 12-byte header, and pixel data that may be optionally compressed per mipmap level.


The header stores the image type (one of [IMAGE_*](../../api/library/common/class.image_cpp.md#IMAGE_2D) values), pixel format (one of [FORMAT_*](../../api/library/common/class.image_cpp.md#FORMAT_R8) values), and file compression mode (one of [FILE_COMPRESSION_*](../../api/library/common/class.image_cpp.md#FILE_COMPRESSION_DISABLE) values). File compression is an additional layer of lossless compression (*ZLib* or *LZ4*) applied to the serialized pixel data, independent from block compression formats like DXT/ATI.


> **Notice:** Block-compressed pixel formats (DXT/ATI) require texture width and height to be aligned to 4 pixels.


### TEXTURE File Format


1. File format identifier (*int32* **"tx11"** (**'t'** | (**'x' << 8**) | (**'1' << 16**) | (**'1' << 24**)))
2. Image header (12 bytes): <details> <summary>View Data | Show</summary> - Image type (*char*). One of [IMAGE_*](../../api/library/common/class.image_cpp.md#IMAGE_2D) values. - Pixel format (*char*). One of [FORMAT_*](../../api/library/common/class.image_cpp.md#FORMAT_R8) values. - File compression mode (*char*). One of [FILE_COMPRESSION_*](../../api/library/common/class.image_cpp.md#FILE_COMPRESSION_DISABLE) values. - Number of mipmap levels (*unsigned char*). Minimum value is 1 (base level only). - Number of layers (*unsigned short*). For non-array types this is 1. - Image width in pixels (*unsigned short*) - Image height in pixels (*unsigned short*) - Image depth (*unsigned short*). For 2D and cubemap types this is 1. </details>
3. Pixel data. The layout depends on the file compression mode:

  - **Uncompressed** (file compression = 0): Raw pixel data for all layers, faces, and mipmap levels stored contiguously. The data is organized in the following order: for each layer, for each face (1 for 2D/3D, 6 for cubemaps), all mipmap levels from the largest (level 0) to the smallest. The total size equals the sum of all mipmap level sizes across all layers and faces.
  - **Compressed** (file compression = 1-4): For each layer, for each face, for each mipmap level: Each mipmap level is compressed independently using the method specified in the header (*ZLib* or *LZ4*). Decompression yields the raw pixel data for that mipmap level.

    - Compressed data size in bytes (*int64*)
    - Compressed pixel data of the specified size
