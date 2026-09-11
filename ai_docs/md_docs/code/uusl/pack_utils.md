# Packing Utils


This documentation article contains information on the UUSL packing functions. This information can be used as the reference document for writing shaders.


To start using common UUSL functionality, include the `core/materials/shaders/api/common.h` and `core/materials/shaders/api/pack_utils.h` files.


```glsl
#include <core/materials/shaders/api/common.h>
#include <core/materials/shaders/api/pack_utils.h>

```


### Implementation of the API-dependent functions


The implementation of the API-dependent functions is available in the corresponding header files for your reference:


- `core/materials/shaders/api/wrapper/directx11.h`


## Packing Utils


## float2 packUnitVectorToOctahedron ( float3 normal )

Encodes a normal (unit) vector into two-component one using octahedron encoding.
### Arguments

- *float3* **normal** - Normal (unit) vector.

### Return value

Two-component vector.
## float3 unpackOctahedronToUnitVector ( float2 octahedron )

Decodes an octahedron vector into three-component normal (unit) one.
### Arguments

- *float2* **octahedron** - Two-component vector.

### Return value

Normal (unit) vector.
## float3 pack1212To888 ( float2 value )

Packs RG12 to RGB8.
### Arguments

- *float2* **value** - RG12 value.

### Return value

RGB8 value.
## float2 pack888To1212 ( float3 value )

Packs RG12 to RGB8.
### Arguments

- *float3* **value** - RGB8 value.

### Return value

RG12 value.
## float pack88To16 ( float2 value )

Packs RG8 into R16.
### Arguments

- *float2* **value** - RG8 value.

### Return value

R16 value.
## float2 pack16To88 ( float value )

Packs R16 into RG8.
### Arguments

- *float* **value** - R16 value.

### Return value

RG8 value.
## float pack44To8 ( float a , float b )

Packs two 4-bit values into an 8-bit one.
### Arguments

- *float* **a** - 4-bit value.
- *float* **b** - 4-bit value.

### Return value

Output 8-bit value.
## float2 pack8To44 ( float value )

Unpacks 8-bit value into two 4-bit values.
### Arguments

- *float* **value** - 8-bit value.

### Return value

Vector of two 4-bit values.
## float2 pack8888To1616 ( float4 value )

Packs normalized RGBA8 into R16G16.
### Arguments

- *float4* **value** - RGBA8 value.

### Return value

R16G16 value.
## float4 pack1616To8888 ( float2 value )

Unpacks R16G16 into RGBA8.
### Arguments

- *float2* **value** - R16G16 value.

### Return value

RGBA8 value.
## uint pack8888To32 ( float4 data )


Packs RGBA8 to a 32-bit value.


**This function is [API-dependent](#api_dependent).**


### Arguments

- *float4* **data** - RGBA8 value to pack.

### Return value

Packed 32-bit value.
## float4 pack32To8888 ( uint data )


Unpacks a 32-bit value to RGBA8 value.


**This function is [API-dependent](#api_dependent).**


### Arguments

- *uint* **data** - 32-bit value.

### Return value

RGBA8 value.
## float2 pack32To1616 ( uint data )


Unpacks 32-bit value into two 16-bit values.


**This function is [API-dependent](#api_dependent).**


### Arguments

- *uint* **data** - 32-bit value.

### Return value

Vector of two 16-bit values.
## float2 pack32To1616 ( float data )


Unpacks 32-bit value into two 16-bit values.


**This function is [API-dependent](#api_dependent).**


### Arguments

- *float* **data** - 32-bit value.

### Return value

Vector of two 16-bit values.
## float pack1616To32 ( float2 data )


Packs two 16-bit values into a 32-bit one.


**This function is [API-dependent](#api_dependent).**


### Arguments

- *float2* **data** - Vector of two 16-bit values.

### Return value

32-bit value.
