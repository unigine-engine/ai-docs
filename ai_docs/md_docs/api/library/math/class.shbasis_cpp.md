# Unigine::SHBasis Class (CPP)

**Header:** #include <UnigineMathLibSHBasis.h>


This class is used to calclulate spherical harmonics coefficients.


## SHBasis Class

### Members

---

## static SHBasisPtr create ( )

Constructor. Initializes spherical harmonics.
## double factorial ( int x ) const

Returns the factorial of the argument.
### Arguments

- *int* **x** - Argument.

### Return value

Factorial.
## double get ( int l , int m , const float* dir ) const

Returns the spherical harmonics coefficient using the direction.
### Arguments

- *int* **l** - Degree.
- *int* **m** - Order.
- *const float** **dir** - Direction.

### Return value

Spherical harmonics coefficient.
## double get ( int l , int m , double phi , double theta ) const

Returns the spherical harmonics coefficient using spherical coordinates.
### Arguments

- *int* **l** - Degree.
- *int* **m** - Order.
- *double* **phi** - Phi coordinate.
- *double* **theta** - Theta coordinate.

### Return value

Spherical harmonics coefficient.
