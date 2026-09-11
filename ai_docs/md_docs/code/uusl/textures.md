# UUSL Textures and Buffers


This documentation article contains information on the UUSL texture functions. This information can be used as the reference document for writing shaders.


To start using common UUSL functionality, include the `core/materials/shaders/api/common.h` and `core/materials/shaders/api/texture.h` files.


```glsl
#include <core/materials/shaders/api/common.h>
#include <core/materials/shaders/api/texture.h>

```


### Implementation of the API-dependent functions


The implementation of the API-dependent functions is available in the corresponding header file for your reference:


- `core/materials/shaders/api/wrapper/directx11.h`


## Texture Initialization Functions


> **Notice:** The implementation of the SAMPLER(NUM) function in Direct3D is the following:
>
>
> ```glsl
> SamplerState s_sampler_ ## NAME : register(s ## NUM);
> SamplerComparisonState s_sampler_compare_ ## NAME : register(s ## NUM);
>
> ```


## INIT_TEXTURE ( value NUM , value NAME )


Initializes a sampler with the 2D texture.


**Equivalent**


```glsl
Texture2D s_texture_ ## NAME : register(t ## NUM); SAMPLER(NUM,NAME)
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.


## INIT_TEXTURE_INT ( value NUM , value NAME )


Initializes a sampler with the 2D texture of int type.


**Equivalent**


```glsl
Texture2D<int> s_texture_ ## NAME : register(t ## NUM); SAMPLER(NUM,NAME)
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.


## INIT_TEXTURE_UINT ( value NUM , value NAME )


Initializes a sampler with the 2D texture of uint type.


**Equivalent**


```glsl
Texture2D<uint> s_texture_ ## NAME : register(t ## NUM); SAMPLER(NUM,NAME)
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.


## INIT_TEXTURE_CUBE ( value NUM , value NAME )


Initializes a sampler with the cubemap texture.


**Equivalent**


```glsl
TextureCube s_texture_ ## NAME : register(t ## NUM); SAMPLER(NUM,NAME)
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.


## INIT_TEXTURE_MSAA ( value NUM , value NAME )


Initializes a sampler with the multi-sampled texture.


**Equivalent**


```glsl
Texture2DMS<float4> s_texture_ ## NAME : register(t ## NUM);
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.


## INIT_TEXTURE_3D ( value NUM , value NAME )


Initializes a sampler with the texture3D.


**Equivalent**


```glsl
Texture3D s_texture_ ## NAME : register(t ## NUM); SAMPLER(NUM,NAME)
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.


## INIT_TEXTURE_ARRAY ( value NUM , value NAME )


Initializes a sampler with the array of 2D textures.


**Equivalent**


```glsl
Texture2DArray s_texture_ ## NAME : register(t ## NUM); SAMPLER(NUM,NAME)
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.


## INIT_TEXTURE_ARRAY_INT2 ( value NUM , value NAME )


Initializes a sampler with the array of 2D textures of int2 type.


**Equivalent**


```glsl
Texture2DArray<int2> s_texture_ ## NAME : register(t ## NUM); SAMPLER(NUM,NAME)
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.


## INIT_TEXTURE_ARRAY_UINT2 ( value NUM , value NAME )


Initializes a sampler with the array of 2D textures of uint2 type.


**Equivalent**


```glsl
Texture2DArray<uint2> s_texture_ ## NAME : register(t ## NUM); SAMPLER(NUM,NAME)
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.


## INIT_W_TEXTURE ( value NUM , value NAME , value TYPE , value FORMAT )


Initializes input 2D write texture.


**Equivalent**


```glsl
RWTexture2D<FORMAT> s_rw_texture_ ## NAME : register(u ## NUM);
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.
- *value* **TYPE** - Type of the texture (RGBA8, RGBA32F, etc.).
- *value* **FORMAT** - Format of the texture (float, float2, float3, float4, int).


## INIT_W_TEXTURE_INT ( value NUM , value NAME , value TYPE , value FORMAT )


Initializes input 2D write int texture.


**Equivalent**


```glsl
RWTexture2D<FORMAT> s_rw_texture_ ## NAME : register(u ## NUM);
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.
- *value* **TYPE** - Type of the texture (RGBA8, RGBA32F, etc.).
- *value* **FORMAT** - Format of the texture (float, float2, float3, float4, int).


## INIT_W_TEXTURE_3D ( value NUM , value NAME , value TYPE , value FORMAT )


Initializes input 3D write texture.


**Equivalent**


```glsl
RWTexture3D<FORMAT> s_rw_texture_ ## NAME : register(u ## NUM);
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.
- *value* **TYPE** - A type of the texture (rgba8,rgba32f,etc.).
- *value* **FORMAT** - A format of the texture (float,float2,float3,float4,int).


## INIT_RW_TEXTURE_R32U ( value NUM , value NAME )


Initializes a 2D input read-write texture that has R32U format type.


**Equivalent**


```glsl
RWTexture2D<uint> s_rw_texture_ ## NAME : register(u ## NUM);
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.


## INIT_RW_TEXTURE_R32F ( value NUM , value NAME )


Initializes a 2D input read-write texture that has R32F format type.


**Equivalent**


```glsl
RWTexture2D<float> s_rw_texture_ ## NAME : register(u ## NUM);
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.


## INIT_RW_TEXTURE_RGBA8 ( value NUM , value NAME )


Initializes a 2D input read-write texture that has RGBA8 format type.


**Equivalent**


```glsl
RWTexture2D<rgba8> s_rw_texture_ ## NAME : register(u ## NUM);
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.


## INIT_RW_TEXTURE_R32U_3D ( value NUM , value NAME )


Initializes a 3D input read-write texture that has R32U format type.


**Equivalent**


```glsl
RWTexture3D<uint> s_rw_texture_ ## NAME : register(u ## NUM);
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.


## INIT_RW_TEXTURE_R32F_3D ( value NUM , value NAME )


Initializes a 3D input read-write texture that has R32F format type.


**Equivalent**


```glsl
RWTexture3D<float> s_rw_texture_ ## NAME : register(u ## NUM);
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.


## INIT_RW_TEXTURE_RGBA8_3D ( value NUM , value NAME )


Initializes a 3D input read-write texture that has RGBA8 format type.


**Equivalent**


```glsl
RWTexture3D<rgba8> s_rw_texture_ ## NAME : register(u ## NUM);
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **NAME** - Name of the texture slot.


## INIT_RW_STRUCTURED_BUFFER ( value NUM , value STRUCTURE , value NAME )


Initializes a read-write structured buffer.


**Equivalent**


```glsl
RWStructuredBuffer<STRUCTURE> NAME : register(u ## NUM);
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **STRUCTURE** - A structure to be stored in buffer.
- *value* **NAME** - Name of the texture slot.


## INIT_STRUCTURED_BUFFER ( value NUM , value STRUCTURE , value NAME )


Initializes a structure buffer.


**Equivalent**


```glsl
StructuredBuffer<STRUCTURE> NAME : register(t[NUM_TEXTURES+NUM]);
```


### Arguments

- *value* **NUM** - Number of the texture slot.
- *value* **STRUCTURE** - A structure to be stored in buffer.
- *value* **NAME** - Name of the texture slot.


## Reading and Sampling a Texture


## float4 TEXTURE_2D_MANUAL_LINEAR ( Texture2D TEX_VALUE , float2 uv )

Returns a linearly interpolated value of the specified 2D texture.
### Arguments

- *Texture2D* **TEX_VALUE** - 2D Texture.
- *float2* **uv** - Texture coordinates.

### Return value

Linearly interpolated value.
## float TEXTURE_2D_GATHER_MANUAL_LINEAR ( Texture2D TEX_VALUE , float2 uv )

Returns a linearly interpolated value of four samples (Red channel only) surrounding the specified UV of the 2D texture.
### Arguments

- *Texture2D* **TEX_VALUE** - 2D Texture.
- *float2* **uv** - Texture coordinates.

### Return value

Linearly interpolated value of four samples (Red channel only).
## float4 TEXTURE_2D_ARRAY_MANUAL_LINEAR ( Texture2DArray TEX_VALUE , float2 uv , float index )

Returns a linearly interpolated value of the specified texture in the Texture 2D array.
### Arguments

- *Texture2DArray* **TEX_VALUE** - 2D Texture array.
- *float2* **uv** - Texture coordinates.
- *float* **index** - Index of the texture in the array.

### Return value

Linearly interpolated value.
## float3 texture_2d_cubic_filter ( float x )

Returns calculated weights for the bicubic interpolation.
### Arguments

- *float* **x** - Value to be filtered.

### Return value

Vector containing weights for the bicubic interpolation.
## float4 TEXTURE_2D_CUBIC ( Texture2D TEX_VALUE , float2 uv )

Returns the bicubically interpolated value of the specified 2D texture.
### Arguments

- *Texture2D* **TEX_VALUE** - 2D texture.
- *float2* **uv** - Texture coordinates.

### Return value

Bicubically interpolated value of the specified 2D texture.
## float4 TEXTURE_2D_CUBIC_BIAS ( Texture2D TEX_VALUE , float2 uv , int mip )

Returns the bicubically interpolated value of the specified 2D texture.
### Arguments

- *Texture2D* **TEX_VALUE** - 2D texture.
- *float2* **uv** - Texture coordinates.
- *int* **mip** - Mipmap level.

### Return value

Bicubically interpolated value of the specified 2D texture for the specified mipmap-level offset (performs a texture lookup with explicit level-of-detail).
## float4 TEXTURE_2D_ARRAY_CUBIC ( Texture2DArray TEX_VALUE , float2 uv , float index )

Returns the bicubically interpolated value of the specified 2D texture in the 2D texture array.
### Arguments

- *Texture2DArray* **TEX_VALUE** - 2D texture array.
- *float2* **uv** - Texture coordinates.
- *float* **index** - Index of the texture in the array.

### Return value

Bicubically interpolated value of the specified 2D texture.
## float4 TEXTURE_2D_CATMULL ( Texture2D TEX_VALUE , float2 uv )

Returns the Catmull interpolated value of the specified 2D texture.
### Arguments

- *Texture2D* **TEX_VALUE** - 2D texture.
- *float2* **uv** - Texture coordinates.

### Return value

Catmull interpolated value of the specified 2D texture.
## float4 TEXTURE_2D_ARRAY_CATMULL ( Texture2DArray TEX_VALUE , float2 uv , float index )

Returns the Catmull interpolated value of the specified 2D texture in the 2D texture array.
### Arguments

- *Texture2DArray* **TEX_VALUE** - 2D texture array.
- *float2* **uv** - Texture coordinates.
- *float* **index** - Index of the texture in the array.

### Return value

Catmull interpolated value of the specified 2D texture.
## float4 TEXTURE_3D_CUBIC ( Texture3D TEX_VALUE , float3 uv )

Returns the cubically interpolated value of the specified 3D texture.
### Arguments

- *Texture3D* **TEX_VALUE** - 3D texture.
- *float3* **uv** - 3D texture coordinates (UVW).

### Return value

Cubically interpolated value of 3D texture.
## TEXTURE ( value NAME , value COORD )


Samples a texture.


**Equivalent**


```glsl
s_texture_ ## NAME.Sample(s_sampler_ ## NAME ,COORD)
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.


## TEXTURE_BIAS ( value NAME , value COORD , value BIAS )


Samples a texture using a mipmap-level offset (performs a texture lookup with explicit level-of-detail).


**Equivalent**


```glsl
s_texture_ ## NAME.SampleLevel(s_sampler_ ## NAME,COORD,BIAS)
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.
- *value* **BIAS** - Mipmap level.


## TEXTURE_OFFSET_BIAS ( value NAME , value COORD , value OFFSET , value BIAS )


Samples a texture using a mipmap-level offset.


**Equivalent**


```glsl
s_texture_ ## NAME.SampleLevel(s_sampler_ ## NAME,COORD,BIAS,OFFSET)
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.
- *value* **OFFSET** - Offset.
- *value* **BIAS** - Mipmap level.


## TEXTURE_BIAS_ZERO ( value NAME , value COORDS )


Samples a texture using a mipmap-level offset on mipmap level 0 only.


**Equivalent**


```glsl
s_texture_ ## NAME.SampleLevel(s_sampler_ ## NAME,COORDS,0.0f)
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORDS** - UV coordinates.


## TEXTURE_OFFSET ( value NAME , value COORD , value OFFSET )


Samples a texture using a offset on mipmap level 0 only (performs a texture lookup with offset).


**Equivalent**


```glsl
s_texture_ ## NAME.SampleLevel(s_sampler_ ## NAME,COORD,0,OFFSET)
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.
- *value* **OFFSET** - Offset.


## TEXTURE_GRAD ( value NAME , value COORD , value DDX , value DDY )


Samples a texture using a gradient to influence the way the sample location is calculated.


**Equivalent**


```glsl
s_texture_ ## NAME.SampleGrad(s_sampler_ ## NAME,COORD,DDX,DDY)
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.
- *value* **DDX** - The rate of change of the surface geometry in the x direction.
- *value* **DDY** - The rate of change of the surface geometry in the y direction.


## TEXTURE_MIP_OFFSET ( value NAME , value COORD , value OFFSET )


Samples a texture using a negative mipmap offset.


**Equivalent**


```glsl
s_texture_ ## NAME.SampleBias(s_sampler_ ## NAME, COORD, -OFFSET)
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.
- *value* **OFFSET** - Offset.


## TEXTURE_FETCH ( value NAME , value COORD )


Reads texel data from the first level-of-detail without any filtering or sampling.


**Equivalent**


```glsl
s_texture_ ## NAME.Load(uint3(COORD, 0))
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.


## TEXTURE_FETCH_LOD ( value NAME , value COORD , value LOD )


Reads texel data without any filtering or sampling.


**Equivalent**


```glsl
s_texture_ ## NAME.Load(uint3(COORD, LOD))
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.
- *value* **LOD** - Level-of-detail within the texture from which the texel will be fetched.


## TEXTURE_ARRAY ( value NAME , value COORDS , value LAYER , value LOD )


Samples a texture array using a mipmap-level.


**Equivalent**


```glsl
s_texture_ ## NAME.SampleLevel(s_sampler_ ## NAME,float3(COORDS,LAYER),LOD)
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORDS** - UV coordinates.
- *value* **LAYER** - Layer value.
- *value* **LOD** - Level-of-detail within the texture from which the texel will be fetched.


## TEXTURE_ARRAY_FETCH ( value NAME , value COORD , value INDEX )


Reads texel data from a texture array from the first level-of-detail without any filtering or sampling.


**Equivalent**


```glsl
s_texture_ ## NAME.Load(uint4(COORD, INDEX, 0))
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.
- *value* **INDEX** - Texture index.


## TEXTURE_ARRAY_FETCH_LOD ( value NAME , value COORD , value INDEX , value LOD )


Reads texel data from a texture array without any filtering or sampling.


**Equivalent**


```glsl
s_texture_ ## NAME.Load(uint4(COORD, INDEX, LOD))
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.
- *value* **INDEX** - Texture index.
- *value* **LOD** - Level-of-detail within the texture from which the texel will be fetched.


## TEXTURE_ARRAY_LOAD ( value NAME , value COORD , value INDEX )


Reads texel data without any filtering or sampling with zero offset.


**Equivalent**


```glsl
s_texture_ ## NAME.Load(uint3(COORD,0))
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.
- *value* **INDEX** - Texture index.


## TEXTURE_ARRAY_LOAD_LOD ( value NAME , value COORD , value INDEX , value LOD )


Reads texel data without any filtering or sampling.


**Equivalent**


```glsl
TEXTURE_ARRAY_FETCH_LOD(NAME, (COORD) * textureResolution(NAME).xy * (1.0f / pow(2, LOD)), INDEX, LOD)
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.
- *value* **INDEX** - Texture index.
- *value* **LOD** - Level-of-detail within the texture from which the texel will be fetched.


## TEXTURE_LOAD ( value NAME , value COORD )


Reads texel data without any filtering or sampling with zero offset.


**Equivalent**


```glsl
s_texture_ ## NAME.Load(uint3(COORD,0))
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.


## TEXTURE_LOAD_LOD ( value NAME , value COORD , value LOD )


Reads texel data without any filtering or sampling.


**Equivalent**


```glsl
s_texture_ ## NAME.Load(uint3(COORD,LOD))
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.
- *value* **LOD** - Level-of-detail within the texture from which the texel will be fetched.


## TEXTURE_3D_FETCH ( value NAME , value COORD , value INDEX )


Reads texel data from a texture array from the first level-of-detail without any filtering or sampling.


**Equivalent**


```glsl
s_texture_ ## NAME.Load(uint4(COORD, INDEX, 0))
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.
- *value* **INDEX** - Texture index.


## TEXTURE_3D_FETCH_LOD ( value NAME , value COORD , value INDEX , value LOD )


Reads texel data from a texture array without any filtering or sampling.


**Equivalent**


```glsl
s_texture_ ## NAME.Load(uint4(COORD, INDEX, LOD))
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.
- *value* **INDEX** - Texture index.
- *value* **LOD** - Level-of-detail within the texture from which the texel will be fetched.


## TEXTURE_3D_LOAD ( value NAME , value COORD )


Reads texel data of a 3D texture without any filtering or sampling with zero offset.


**Equivalent**


```glsl
TEXTURE_3D_LOAD_LOD(NAME, COORD, 0)
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.


## TEXTURE_3D_LOAD_LOD ( value NAME , value COORD , value LOD )


Reads texel data of a single level of detail of a 3D texture without any filtering or sampling.


**Equivalent**


```glsl
s_texture_ ## NAME.Load(uint4((COORD) * textureResolution(NAME).xyz * (1.0f / pow(2, LOD)), LOD))
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - UV coordinates.
- *value* **LOD** - Level-of-detail within the texture from which the texel will be fetched.


## float4 TEXTURE_RW_LOAD_RGBA8 ( value NAME , value COORD )


Reads the RW RGBA8 texture and returns a float4 value.


**Equivalent**


```glsl
pack32To8888(s_rw_texture_ ## NAME[ ## COORD ## ])
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - Unnormalized pixel coordinates.

### Return value

Texture value.
## uint TEXTURE_RW_LOAD_R32U ( value NAME , value COORD )


Reads the RW R32U texture and returns a uint value.


**Equivalent**


```glsl
s_rw_texture_ ## NAME[ ## COORD ## ]
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - Unnormalized pixel coordinates.

### Return value

Texture value.
## float TEXTURE_RW_LOAD_R32F ( value NAME , value COORD )


Reads the RW R32F texture and returns a float value.


**Equivalent**


```glsl
s_rw_texture_ ## NAME[ ## COORD ## ]
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - Unnormalized pixel coordinates.

### Return value

Texture value.
## Writing to UAV Texture


## TEXTURE_RW_STORE_RGBA8 ( value NAME , value COORD , value VALUE )


Stores the value to RW RGBA8 texture.


**Equivalent**


```glsl
s_rw_texture_ ## NAME[COORD] = pack8888To32(VALUE)
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - Unnormalized pixel coordinates.
- *value* **VALUE** - A value to store.


## TEXTURE_RW_STORE_R32U ( value NAME , value COORD , value VALUE )


Stores the value to RW R32U texture.


**Equivalent**


```glsl
s_rw_texture_ ## NAME[COORD] = VALUE
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - Unnormalized pixel coordinates.
- *value* **VALUE** - A value to store.


## TEXTURE_RW_STORE_R32F ( value NAME , value COORD , value VALUE )


Stores the value to RW R32F texture.


**Equivalent**


```glsl
s_rw_texture_ ## NAME[COORD] = VALUE
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - Unnormalized pixel coordinates.
- *value* **VALUE** - A value to store.


## TEXTURE_W_STORE ( value NAME , value COORD , value VALUE )


Stores the value to W texture.


**Equivalent**


```glsl
s_rw_texture_ ## NAME[uint2(COORD)] = VALUE
```


### Arguments

- *value* **NAME** - Name of the texture slot.
- *value* **COORD** - Unnormalized pixel coordinates.
- *value* **VALUE** - A value to store.


## Passing Textures to Functions


UUSL allows you to pass textures to functions as arguments.


Here is a usage example:


```glsl
float4 func_name(float4 color,float2 uv,TEXTURE_IN_2(texture_0,texture_1)) {
	return TEXTURE(texture_0,uv) * TEXTURE_BIAS(texture_1,uv,5.0f) * color;
}

float4 new_color = func_name(color,uv,TEXTURE_OUT_2(TEX_COLOR_0,TEX_COLOR_1));

```


## TEXTURE_OUT ( value NAME )


Allows to pass a texture to function.


**Equivalent**


```glsl
s_texture_ ## NAME,s_sampler_ ## NAME
```


### Arguments

- *value* **NAME** - Name of the texture slot.


## TEXTURE_OUT_2 ( value NAME0 , value NAME1 )


Allows to pass two textures to a function.


**Equivalent**


```glsl
TEXTURE_OUT(NAME0),TEXTURE_OUT(NAME1)
```


### Arguments

- *value* **NAME0** - Name of the texture slot (for the first texture).
- *value* **NAME1** - Name of the texture slot (for the second texture).


## TEXTURE_OUT_3 ( value NAME0 , value NAME1 , value NAME2 )


Allows to pass three textures to a function.


**Equivalent**


```glsl
TEXTURE_OUT_2(NAME0,NAME1),TEXTURE_OUT(NAME2)
```


### Arguments

- *value* **NAME0** - Name of the texture slot (for the first texture).
- *value* **NAME1** - Name of the texture slot (for the second texture).
- *value* **NAME2** - Name of the texture slot (for the third texture).


## TEXTURE_OUT_4 ( value NAME0 , value NAME1 , value NAME2 , value NAME3 )


Allows to pass four textures to a function.


**Equivalent**


```glsl
TEXTURE_OUT_3(NAME0,NAME1,NAME2),TEXTURE_OUT(NAME3)
```


### Arguments

- *value* **NAME0** - Name of the texture slot (for the first texture).
- *value* **NAME1** - Name of the texture slot (for the second texture).
- *value* **NAME2** - Name of the texture slot (for the third texture).
- *value* **NAME3** - Name of the texture slot (for the fourth texture).


## TEXTURE_IN ( value NAME )


Specifies the 2D texture for passing to function.


**Equivalent**


```glsl
Texture2D s_texture_ ## NAME,SamplerState s_sampler_ ## NAME
```


### Arguments

- *value* **NAME** - Name of the texture.


## TEXTURE_IN_2 ( value NAME0 , value NAME1 )


Specifies two 2D textures for passing to function.


**Equivalent**


```glsl
TEXTURE_IN(NAME0),TEXTURE_IN(NAME1)
```


### Arguments

- *value* **NAME0** - Name of the first texture.
- *value* **NAME1** - Name of the second texture.


## TEXTURE_IN_3 ( value NAME0 , value NAME1 , value NAME2 )


Specifies three 2D textures for passing to function.


**Equivalent**


```glsl
TEXTURE_IN_2(NAME0,NAME1),TEXTURE_IN(NAME2)
```


### Arguments

- *value* **NAME0** - Name of the first texture.
- *value* **NAME1** - Name of the second texture.
- *value* **NAME2** - Name of the third texture.


## TEXTURE_IN_4 ( value NAME0 , value NAME1 , value NAME2 , value NAME3 )


Specifies four 2D textures for passing to function.


**Equivalent**


```glsl
TEXTURE_IN_3(NAME0,NAME1,NAME2),TEXTURE_IN(NAME3)
```


### Arguments

- *value* **NAME0** - Name of the first texture.
- *value* **NAME1** - Name of the second texture.
- *value* **NAME2** - Name of the third texture.
- *value* **NAME3** - Name of the fourth texture.


## TEXTURE_IN_CUBE ( value NAME )


Specifies the cube texture for passing to function.


**Equivalent**


```glsl
TextureCube s_texture_ ## NAME,SamplerState s_sampler_ ## NAME
```


### Arguments

- *value* **NAME** - Name of the texture.


## TEXTURE_IN_3D ( value NAME )


Specifies the 3D texture for passing to function.


**Equivalent**


```glsl
Texture3D s_texture_ ## NAME,SamplerState s_sampler_ ## NAME
```


### Arguments

- *value* **NAME** - Name of the texture.


## TEXTURE_IN_ARRAY ( value NAME )


Specifies the texture array for passing to function.


**Equivalent**


```glsl
Texture2DArray s_texture_ ## NAME,SamplerState s_sampler_ ## NAME
```


### Arguments

- *value* **NAME** - Name of the texture.


## TEXTURE_IN_ARRAY_INT2 ( value NAME )


Specifies the int2 texture array for passing to function.


**Equivalent**


```glsl
Texture2DArray s_texture_ ## NAME,SamplerState s_sampler_ ## NAME
```


### Arguments

- *value* **NAME** - Name of the texture.


## Texture Resolution


## int2 textureResolution ( value TEXTURE )


Returns the texture resolution in pixels of the specified texture. This function supports 2D and Cube textures only.


**This function is [API-dependent](#api_dependent).**


### Arguments

- *value* **TEXTURE** - Texture.

### Return value

Texture width and height.
## int3 textureResolution ( value TEXTURE )


Returns the texture resolution in pixels of the specified texture. This function supports 2D Array, 3D and Cube Array textures only.


**This function is [API-dependent](#api_dependent).**


### Arguments

- *value* **TEXTURE** - Texture.

### Return value

Texture width, height, and depth.
## float2 textureIResolution ( value TEXTURE )


Returns texel size of specified texture. This function supports 2D and Cube textures only.


**This function is [API-dependent](#api_dependent).**


### Arguments

- *value* **TEXTURE** - Texture.

### Return value

Texel size of specified texture.
## float3 textureIResolution ( value TEXTURE )


Returns texel size of specified texture. This function supports 2D Array, 3D and Cube Array textures only.


**This function is [API-dependent](#api_dependent).**


### Arguments

- *value* **TEXTURE** - Texture.

### Return value

Texel size of specified texture.
## int2 textureRWResolution ( value TEXTURE )


Returns texture resolution in pixels of the specified RW texture. This function supports 2D RW textures only.


**This function is [API-dependent](#api_dependent).**


### Arguments

- *value* **TEXTURE** - RW texture.

### Return value

Texture width and height.
## float2 textureRWIResolution ( value TEXTURE )


Returns texel size of specified RW texture. This function supports 2D RW textures only.


**This function is [API-dependent](#api_dependent).**


### Arguments

- *value* **TEXTURE** - RW texture.

### Return value

Texel size of specified RW texture.
## int2 textureResolutionMip ( value TEXTURE , int LOD )


Returns the resolution in pixels of the specified texture Mip level. This function supports 2D and Cube textures only.


**This function is [API-dependent](#api_dependent).**


### Arguments

- *value* **TEXTURE** - Texture.
- *int* **LOD** - Specific Mip of the texture.

### Return value

Texture width and height.
## int3 textureResolutionMip ( value TEXTURE , int LOD )


Returns the resolution in pixels of the specified texture Mip level. This function supports 2D Array, 3D and Cube Array textures only.


**This function is [API-dependent](#api_dependent).**


### Arguments

- *value* **TEXTURE** - Texture.
- *int* **LOD** - Specific Mip of the texture.

### Return value

Texture width, height, and depth.
## float2 textureIResolutionMip ( value TEXTURE , int LOD )


Returns the texel size of the specified texture Mip level. This function supports 2D and Cube textures only.


**This function is [API-dependent](#api_dependent).**


### Arguments

- *value* **TEXTURE** - Texture.
- *int* **LOD** - Specific Mip of the texture.

### Return value

Texel size of the specified texture Mip level.
## float3 textureIResolutionMip ( value TEXTURE , int LOD )


Returns the texel size of the specified texture Mip level. This function supports 2D Array, 3D and Cube Array textures only.


**This function is [API-dependent](#api_dependent).**


### Arguments

- *value* **TEXTURE** - Texture.
- *int* **LOD** - Specific Mip of the texture.

### Return value

Texel size of the specified texture Mip level.
## int textureNumberOfMips ( value TEXTURE )

Returns the total number of LODs for the specified texture. This function supports 2D, 2DArray, 3D, Cube, CubeArray textures only.
### Arguments

- *value* **TEXTURE** - Texture.

### Return value

Total number of texture Mips.
