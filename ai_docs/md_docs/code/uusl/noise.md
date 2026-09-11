# Noise Functions


This documentation article contains information functions of the UUSL. This information can be used as the reference document for writing shaders.


To start using common UUSL functionality, include the `core/materials/shaders/api/noise.h` file.


```glsl
#include <core/materials/shaders/api/noise.h>
```


## Noise Functions


## float4 blueNoise ( uint2 coord )

Returns blue noise based on the source coordinates using a 16x16 constant blue noise array.
### Arguments

- *uint2* **coord** - Unnormalized coordinates.

### Return value

Blue noise.
## float4 blueNoise ( float2 coord )

Returns blue noise based on the source coordinates using a 16x16 constant blue noise array.
### Arguments

- *float2* **coord** - Unnormalized coordinates.

### Return value

Blue noise.
## float4 blueNoiseTemporal ( uint2 coord , uint num_frame )

Returns blue noise based on source coordinates using a 16x16 constant blue noise array. You can specify the number of frames for the noise to change. It is a constant blue noise array with a frame-to-frame offset calculated using Golden Ratio.
### Arguments

- *uint2* **coord** - Unnormalized coordinates.
- *uint* **num_frame** - Number of frames for the noise to change.

### Return value

Blue noise.
## float4 blueNoiseTAA ( uint2 coord , uint num_frame )

Returns blue noise based on source coordinates using a 16x16 constant blue noise array. You can specify the number of frames for the noise to change. It is a constant blue noise array with a frame-to-frame offset calculated using Golden Ratio.


The *TAA* postfix means that noise pattern changes from frame to frame when [TAA](../../principles/render/antialiasing/taa.md) is enabled, and remains constant when TAA is disabled.

### Arguments

- *uint2* **coord** - Unnormalized coordinates.
- *uint* **num_frame** - Number of frames for the noise to change.

### Return value

Blue noise.
## float4 blueNoiseTAA ( float2 coord , uint num_frame )

Returns blue noise based on source coordinates using a 16x16 constant blue noise array. You can specify the number of frames for the noise to change. It is a constant blue noise array with a frame-to-frame offset calculated using Golden Ratio.


The *TAA* postfix means that noise pattern changes from frame to frame when [TAA](../../principles/render/antialiasing/taa.md) is enabled, and remains constant when TAA is disabled.

### Arguments

- *float2* **coord** - Unnormalized coordinates.
- *uint* **num_frame** - Number of frames for the noise to change.

### Return value

Blue noise.
## float4 blueNoiseTemporal ( float2 coord , uint num_frame )

Returns blue noise based on source coordinates using a 16x16 constant blue noise array. You can specify the number of frames for the noise to change. It is a constant blue noise array with a frame-to-frame offset calculated using Golden Ratio.
### Arguments

- *float2* **coord** - Unnormalized coordinates.
- *uint* **num_frame** - Number of frames for the noise to change.

### Return value

Blue noise.
## float bayerNoise ( uint2 coord )

Returns Bayer noise generated based on the source coordinates using a 4x4 constant Bayer pattern.
### Arguments

- *uint2* **coord** - Unnormalized coordinates.

### Return value

Bayer noise.
## float bayerNoise ( float2 coord )

Returns Bayer noise generated based on the source coordinates using a 4x4 constant Bayer pattern.
### Arguments

- *float2* **coord** - Unnormalized coordinates.

### Return value

Bayer noise.
## float2 vogelDisk ( uint i , uint count , float noise )

Returns a generated set of points with X and Y coordinates in the [-1; 1] range that describe a circle with uniform distribution of samples inside. This method is suitable for getting uniform distribution of coordinates for a circle. For example you can use it is a loop to generate UV coordinates offset for making the uniform circular blur effect. You can use the current loop iteration index as the i argument and the maximum number of iterations � as count.
### Arguments

- *uint* **i** - Index of the current point for the disk.
- *uint* **count** - Number of points.
- *float* **noise** - Normalized noise.

### Return value

Set of points with X and Y coordinates in the [-1; 1] range that describe a circle with uniform distribution of samples inside.
## float2 vogelDisk ( uint i , uint count )

Returns a generated set of points with X and Y coordinates in the [-1; 1] range that describe a circle with uniform distribution of samples inside. This method is suitable for getting uniform distribution of coordinates for a circle. For example you can use it is a loop to generate UV coordinates offset for making the uniform circular blur effect. You can use the current loop iteration index as the i argument and the maximum number of iterations � as count.
### Arguments

- *uint* **i** - Index of the current point for the disk.
- *uint* **count** - Number of points.

### Return value

Set of points with X and Y coordinates in the [-1; 1] range that describe a circle with uniform distribution of samples inside.
## float2 hammersley ( uint i , uint N )

Returns a generated set of points with X and Y coordinates in the [0; 1] range that describe uniform distribution of samples inside a square (Hammersley Point Set).
### Arguments

- *uint* **i** - index of the current point.
- *uint* **N** - Number of points.

### Return value

Set of points with X and Y coordinates in the [-1; 1] range that describe uniform distribution of samples inside a square.
