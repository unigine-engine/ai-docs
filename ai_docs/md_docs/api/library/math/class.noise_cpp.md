# Unigine::Noise Class (CPP)

**Header:** #include <UnigineMathLibNoise.h>


This class is used to generate turbulence textures (supports tiling).


## Noise Class

### Members

---

## static NoisePtr create ( )

Constructor. Initializes the noise generator.
## static NoisePtr create ( unsigned int seed_ )

Constructor. Initializes the noise generator by setting a new seed.
### Arguments

- *unsigned int* **seed_** - New seed.

## void setSeed ( unsigned int seed_ )

Sets a new seed for noise generator.
### Arguments

- *unsigned int* **seed_** - New seed.

## unsigned int getSeed ( ) const

Returns the current seed.
### Return value

Current seed.
## float get1 ( float x ) const

Returns the one-dimensional white noise.
### Arguments

- *float* **x** - Seed.

### Return value

One-dimensional white noise.
## float get2 ( float x , float y ) const

Returns the two-dimensional white noise.
### Arguments

- *float* **x** - Seed 1.
- *float* **y** - Seed 2.

### Return value

Two-dimensional white noise.
## float get3 ( float x , float y , float z ) const

Returns the three-dimensional (3D) white noise.
### Arguments

- *float* **x** - Seed 1.
- *float* **y** - Seed 2.
- *float* **z** - Seed 3.

### Return value

Three-dimensional (3D) white noise.
## float getTurbulence1 ( float x , int frequency ) const

Returns the one-dimensional turbulence noise.
### Arguments

- *float* **x** - Seed.
- *int* **frequency** - Frequency.

### Return value

One-dimensional turbulence noise.
## float getTurbulence2 ( float x , float y , int frequency ) const

Returns the two-dimensional turbulence noise.
### Arguments

- *float* **x** - Seed 1.
- *float* **y** - Seed 2.
- *int* **frequency** - Frequency.

### Return value

Two-dimensional turbulence noise.
## float getTurbulence3 ( float x , float y , float z , int frequency ) const

Returns the three-dimensional (3D) turbulence noise.
### Arguments

- *float* **x** - Seed 1.
- *float* **y** - Seed 2.
- *float* **z** - Seed 3.
- *int* **frequency** - Frequency.

### Return value

Three-dimensional (3D) turbulence noise.
## float getTileable1 ( float x , float width ) const

Returns the one-dimensional tileable noise.
### Arguments

- *float* **x** - Seed.
- *float* **width** - Tile width.

### Return value

One-dimensional tileable noise.
## float getTileable2 ( float x , float y , float width , float height ) const

Returns the two-dimensional tileable noise.
### Arguments

- *float* **x** - Seed 1.
- *float* **y** - Seed 2.
- *float* **width** - Tile width.
- *float* **height** - Tile height.

### Return value

Two-dimensional tileable noise.
## float getTileable3 ( float x , float y , float z , float width , float height , float depth ) const

Returns the three-dimensional (3D) tileable noise.
### Arguments

- *float* **x** - Seed 1.
- *float* **y** - Seed 2.
- *float* **z** - Seed 3.
- *float* **width** - Tile width.
- *float* **height** - Tile height.
- *float* **depth** - Tile depth.

### Return value

Three-dimensional (3D) tileable noise.
## float getTileableTurbulence1 ( float x , float width , int frequency ) const

Returns the one-dimensional tileable turbulence noise.
### Arguments

- *float* **x** - Seed 1.
- *float* **width** - Tile width.
- *int* **frequency** - Frequency.

### Return value

One-dimensional tileable turbulence noise.
## float getTileableTurbulence2 ( float x , float y , float width , float height , int frequency ) const

Returns the two-dimensional tileable turbulence noise.
### Arguments

- *float* **x** - Seed 1.
- *float* **y** - Seed 2.
- *float* **width** - Tile width.
- *float* **height** - Tile height.
- *int* **frequency** - Frequency.

### Return value

Two-dimensional tileable turbulence noise.
## float getTileableTurbulence3 ( float x , float y , float z , float width , float height , float depth , int frequency ) const

Returns the three-dimensional (3D) tileable turbulence noise.
### Arguments

- *float* **x** - Seed 1.
- *float* **y** - Seed 2.
- *float* **z** - Seed 3.
- *float* **width** - Tile width.
- *float* **height** - Tile height.
- *float* **depth** - Tile depth.
- *int* **frequency** - Frequency.

### Return value

Three-dimensional (3D) tileable turbulence noise.
