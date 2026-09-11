# Matrix Functions


This documentation article contains the information on the UUSL matrix functions. This information can be used as the reference document for writing shaders.


To start using the UUSL matrix functionality, include the `core/materials/shaders/api/common.h` and `core/materials/shaders/api/matrix.h` files.


```glsl
#include <core/materials/shaders/api/common.h>
#include <core/materials/shaders/api/matrix.h>

```


### Implementation of the API-dependent functions


The implementation of the API-dependent functions is available in the corresponding header file for your reference:


- `core/materials/shaders/api/wrapper/directx11.h`


## Matrix Functions


## float3 mul3 ( float3x3 a , float3 b )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *float3x3* **a** - Matrix.
- *float3* **b** - Vector.

### Return value

Return value.
## float3 mul3 ( float3 a , float3x3 b )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *float3* **a** - Vector.
- *float3x3* **b** - Matrix.

### Return value

Return value.
## float3 mul3 ( float4x4 a , float3 b )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *float4x4* **a** - Matrix.
- *float3* **b** - Vector.

### Return value

Return value.
## float3 mul3 ( float3 a , float4x4 b )

Returns the result of multiplication of three components of the specified arguments.
### Arguments

- *float3* **a** - Vector.
- *float4x4* **b** - Matrix.

### Return value

Return value.
## float3x3 mul3 ( float3x3 a , float3x3 b )

Returns the result of multiplication of the specified arguments.
### Arguments

- *float3x3* **a** - Matrix.
- *float3x3* **b** - Matrix.

### Return value

Return matrix.
## float4 mul4 ( float4x4 a , float4 b )

Returns the result of multiplication of the specified arguments.
### Arguments

- *float4x4* **a** - Matrix.
- *float4* **b** - Vector.

### Return value

Return value.
## float4 mul4 ( float4 a , float4x4 b )

Returns the result of multiplication of the specified arguments.
### Arguments

- *float4* **a** - Vector.
- *float4x4* **b** - Matrix.

### Return value

Return value.
## float4 mul4 ( float4x4 a , float3 b )

Returns the result of multiplication of the specified arguments. 1.0f is added as the fourth component of the vector argument.
### Arguments

- *float4x4* **a** - Matrix.
- *float3* **b** - Vector.

### Return value

Return value.
## float4 mul4 ( float3 a , float4x4 b )

Returns the result of multiplication of the specified arguments. 1.0f is added as the fourth component of the vector argument.
### Arguments

- *float3* **a** - Vector.
- *float4x4* **b** - Matrix.

### Return value

Return value.
## float4x4 mul4 ( float4x4 a , float4x4 b )

Returns the result of multiplication of the specified arguments.
### Arguments

- *float4x4* **a** - Matrix.
- *float4x4* **b** - Matrix.

### Return value

Return value.
## float4x4 mul4 ( float3x3 a , float4x4 b )

Returns the result of multiplication of the specified arguments.
### Arguments

- *float3x3* **a** - Matrix.
- *float4x4* **b** - Matrix.

### Return value

Return value.
## float4x4 mul4 ( float4x4 a , float3x3 b )

Returns the result of multiplication of the specified arguments.
### Arguments

- *float4x4* **a** - Matrix.
- *float3x3* **b** - Matrix.

### Return value

Return value.
## float3x3 matrix3Col ( float3 coll_0 , float3 coll_1 , float3 coll_2 )

Returns the matrix created using the arguments.
### Arguments

- *float3* **coll_0** - Values for the first column.
- *float3* **coll_1** - Values for the second column.
- *float3* **coll_2** - Values for the third column.

### Return value

Return matrix.
## float4x4 matrix4Col ( float3 coll_0 , float3 coll_1 , float3 coll_2 , float3 coll_3 )

Returns the matrix created using the arguments and filling the extra cells with 0 and the element on the main diagonal � with 1.
### Arguments

- *float3* **coll_0** - Values for the first column.
- *float3* **coll_1** - Values for the second column.
- *float3* **coll_2** - Values for the third column.
- *float3* **coll_3** - Values for the fourth column.

### Return value

Return matrix.
## float4x4 matrix4Col ( float3 coll_0 , float3 coll_1 , float3 coll_2 )

Returns the matrix created using the arguments and filling the extra cells with 0 and the element on the main diagonal � with 1.
### Arguments

- *float3* **coll_0** - Values for the first column.
- *float3* **coll_1** - Values for the second column.
- *float3* **coll_2** - Values for the third column.

### Return value

Return matrix.
## float4x4 matrix4Col ( float4 coll_0 , float4 coll_1 , float4 coll_2 , float4 coll_3 )

Returns the matrix created using the arguments.
### Arguments

- *float4* **coll_0** - Values for the first column.
- *float4* **coll_1** - Values for the second column.
- *float4* **coll_2** - Values for the third column.
- *float4* **coll_3** - Values for the fourth column.

### Return value

Return matrix.
## float3 col ( float3x3 mat , int column )

 Returns the elements located in the specified column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *int* **column** - Column index.

### Return value

Elements of the column.
## float4 col ( float4x4 mat , int column )

 Returns the elements located in the specified column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *int* **column** - Column index.

### Return value

Elements of the column.
## void col ( float4x4 mat , int column , float4 value )

 Adds the value elements to the specified column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *int* **column** - Column index.
- *float4* **value** - Elements to be added.


## void col ( float4x4 mat , int column , float3 value )

 Adds the value as the first three elements to the specified column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *int* **column** - Column index.
- *float3* **value** - Elements to be added.


## void col ( float4x4 mat , int column , float2 value )

 Adds the value as the first two elements to the specified column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *int* **column** - Column index.
- *float2* **value** - Elements to be added.


## void col ( float4x4 mat , int column , float value )

 Adds the value as the first element to the specified column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *int* **column** - Column index.
- *float* **value** - Element to be added.


## void col ( float3x3 mat , int column , float3 value )

 Adds the value elements to the specified column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *int* **column** - Column index.
- *float3* **value** - Elements to be added.


## void col ( float3x3 mat , int column , float2 value )

 Adds the value as the first two elements to the specified column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *int* **column** - Column index.
- *float2* **value** - Elements to be added.


## void col ( float3x3 mat , int column , float value )

 Adds the value as the first element to the specified column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *int* **column** - Column index.
- *float* **value** - Element to be added.


## float3 colX ( float3x3 mat )

 Returns the elements located in the first column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.

### Return value

Elements of the column.
## void colX ( float3x3 mat , float3 column )

 Adds the value elements to the first column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float3* **column** - Elements to be added.


## void colX ( float3x3 mat , float2 column )

 Adds the value as the first two elements to the first column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float2* **column**


## void colX ( float3x3 mat , float column )

 Adds the value as the first element to the first column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float* **column** - Element to be added.


## float4 colX ( float4x4 mat )

 Returns the elements located in the first column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Elements of the column.
## void colX ( float4x4 mat , float4 value )

 Adds the value elements to the first column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float4* **value** - Elements to be added.


## void colX ( float4x4 mat , float3 value )

 Adds the value as the first three elements to the first column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float3* **value** - Elements to be added.


## void colX ( float4x4 mat , float2 value )

 Adds the value as the first two elements to the first column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float2* **value** - Elements to be added.


## void colX ( float4x4 mat , float value )

 Adds the value as the first element to the first column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Element to be added.


## float3 colY ( float3x3 mat )

 Returns the elements located in the second column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.

### Return value

Elements of the column.
## void colY ( float3x3 mat , float3 column )

 Adds the value elements to the second column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float3* **column** - Elements to be added.


## void colY ( float3x3 mat , float2 column )

 Adds the value as the first two elements to the second column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float2* **column** - Elements to be added.


## void colY ( float3x3 mat , float column )

 Adds the value as the first element to the second column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float* **column** - Element to be added.


## float4 colY ( float4x4 mat )

 Returns the elements located in the second column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Elements of the column.
## void colY ( float4x4 mat , float4 value )

 Adds the value elements to the second column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float4* **value** - Elements to be added.


## void colY ( float4x4 mat , float3 value )

 Adds the value as the first three elements to the second column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float3* **value** - Elements to be added.


## void colY ( float4x4 mat , float2 value )

 Adds the value as the first two elements to the second column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float2* **value** - Elements to be added.


## void colY ( float4x4 mat , float value )

 Adds the value as the first element to the second column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Element to be added.


## float3 colZ ( float3x3 mat )

 Returns the elements located in the third column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.

### Return value

Elements of the column.
## void colZ ( float3x3 mat , float3 column )

 Adds the value elements to the third column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float3* **column** - Elements to be added.


## void colZ ( float3x3 mat , float2 column )

 Adds the value as the first two elements to the third column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float2* **column** - Elements to be added.


## void colZ ( float3x3 mat , float column )

 Adds the value as the first element to the third column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float* **column** - Element to be added.


## float4 colZ ( float4x4 mat )

 Returns the elements located in the third column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Elements of the column.
## void colZ ( float4x4 mat , float4 value )

 Adds the value elements to the third column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float4* **value** - Elements to be added.


## void colZ ( float4x4 mat , float3 value )

 Adds the value as the first three elements to the third column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float3* **value** - Elements to be added.


## void colZ ( float4x4 mat , float2 value )

 Adds the value as the first two elements to the third column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float2* **value** - Elements to be added.


## void colZ ( float4x4 mat , float value )

 Adds the value as the first element to the third column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Element to be added.


## float4 colW ( float4x4 mat )

 Returns the elements located in the fourth column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Elements of the column.
## void colW ( float4x4 mat , float4 value )

 Adds the value elements to the fourth column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float4* **value** - Elements to be added.


## void colW ( float4x4 mat , float3 value )

 Adds the value as the first three elements to the fourth column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float3* **value** - Elements to be added.


## void colW ( float4x4 mat , float2 value )

 Adds the value as the first two elements to the fourth column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float2* **value** - Elements to be added.


## void colW ( float4x4 mat , float value )

 Adds the value as the first element to the fourth column of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value**


## float3x3 matrix3Row ( float3 row_0 , float3 row_1 , float3 row_2 )

Returns the matrix created using the arguments.
### Arguments

- *float3* **row_0** - Values for the first row.
- *float3* **row_1** - Values for the second row.
- *float3* **row_2** - Values for the third row.

### Return value

Return matrix.
## float4x4 matrix4Row ( float4 row_0 , float4 row_1 , float4 row_2 , float4 row_3 )

Returns the matrix created using the arguments.
### Arguments

- *float4* **row_0** - Values for the first row.
- *float4* **row_1** - Values for the second row.
- *float4* **row_2** - Values for the third row.
- *float4* **row_3** - Values for the fourth row.

### Return value

Return matrix.
## float4x4 matrix4Row ( float4 row_0 , float4 row_1 , float4 row_2 )

Returns the matrix created using the arguments and filling the extra cells with 0 and the element on the main diagonal � with 1.
### Arguments

- *float4* **row_0** - Values for the first row.
- *float4* **row_1** - Values for the second row.
- *float4* **row_2** - Values for the third row.

### Return value

Return matrix.
## float4x4 matrix4Row ( float3 row_0 , float3 row_1 , float3 row_2 )

Returns the matrix created using the arguments and filling the extra cells with 0 and the element on the main diagonal � with 1.
### Arguments

- *float3* **row_0** - Values for the first row.
- *float3* **row_1** - Values for the second row.
- *float3* **row_2** - Values for the third row.

### Return value

Return matrix.
## float4x4 matrix4Row ( float3 row_0 , float3 row_1 , float3 row_2 , float3 row_3 )

Returns the matrix created using the arguments and filling the extra cells with 0 and the element on the main diagonal � with 1.
### Arguments

- *float3* **row_0** - Values for the first row.
- *float3* **row_1** - Values for the second row.
- *float3* **row_2** - Values for the third row.
- *float3* **row_3** - Values for the fourth row.

### Return value

Return matrix.
## float3 row ( float3x3 mat , int row )

 Returns the elements located in the specified row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *int* **row** - Row index.

### Return value

Elements of the row.
## void row ( float3x3 mat , int row , float3 value )

 Adds the value elements to the specified row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *int* **row** - Row index.
- *float3* **value** - Elements to be added.


## void row ( float3x3 mat , int row , float2 value )

 Adds the value as the first two elements to the specified row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *int* **row** - Row index.
- *float2* **value** - Elements to be added.


## void row ( float3x3 mat , int row , float value )

 Adds the value as the first element to the specified row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *int* **row** - Row index.
- *float* **value** - Element to be added.


## float4 row ( float4x4 mat , int row )

 Returns the elements located in the specified row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *int* **row** - Row index.

### Return value

Elements of the row.
## void row ( float4x4 mat , int row , float4 value )

 Adds the value elements to the specified row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *int* **row** - Row index.
- *float4* **value** - Elements to be added.


## void row ( float4x4 mat , int row , float3 value )

 Adds the value as the first three elements to the specified row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *int* **row** - Row index.
- *float3* **value** - Elements to be added.


## void row ( float4x4 mat , int row , float2 value )

 Adds the value as the first two elements to the specified row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *int* **row** - Row index.
- *float2* **value** - Elements to be added.


## void row ( float4x4 mat , int row , float value )

 Adds the value as the first element to the specified row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *int* **row** - Row index.
- *float* **value** - Element to be added.


## float3 rowX ( float3x3 mat )

 Returns the first row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.

### Return value

Elements of the row.
## void rowX ( float3x3 mat , float3 value )

 Adds the value elements to the first row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float3* **value** - Elements to be added.


## void rowX ( float3x3 mat , float2 value )

 Adds the value as the first two elements to the first row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float2* **value** - Elements to be added.


## void rowX ( float3x3 mat , float value )

 Adds the value as the first element to the first row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float* **value** - Element to be added.


## float4 rowX ( float4x4 mat )

 Returns the first row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Elements of the row.
## void rowX ( float4x4 mat , float4 value )

 Adds the value elements to the first row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float4* **value** - Elements to be added.


## void rowX ( float4x4 mat , float3 value )

 Adds the value as the first three elements to the first row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float3* **value** - Elements to be added.


## void rowX ( float4x4 mat , float2 value )

 Adds the value as the first two elements to the first row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float2* **value** - Elements to be added.


## void rowX ( float4x4 mat , float value )

 Adds the value as the first element to the first row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Element to be added.


## float3 rowY ( float3x3 mat )

 Returns the second row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.

### Return value

Elements of the row.
## void rowY ( float3x3 mat , float3 value )

 Adds the value elements to the second row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float3* **value** - Elements to be added.


## void rowY ( float3x3 mat , float2 value )

 Adds the value as the first two elements to the second row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float2* **value** - Elements to be added.


## void rowY ( float3x3 mat , float value )

 Adds the value as the first element to the second row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float* **value** - Element to be added.


## float4 rowY ( float4x4 mat )

 Returns the second row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Elements of the row.
## void rowY ( float4x4 mat , float4 value )

 Adds the value elements to the second row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float4* **value** - Elements to be added.


## void rowY ( float4x4 mat , float3 value )

 Adds the value as the first three elements to the second row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float3* **value** - Elements to be added.


## void rowY ( float4x4 mat , float2 value )

 Adds the value as the first two elements to the second row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float2* **value** - Elements to be added.


## void rowY ( float4x4 mat , float value )

 Adds the value as the first element to the second row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Element to be added.


## float3 rowZ ( float3x3 mat )

 Returns the third row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.

### Return value

Elements of the row.
## void rowZ ( float3x3 mat , float3 value )

 Adds the value elements to the third row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float3* **value** - Elements to be added.


## void rowZ ( float3x3 mat , float2 value )

 Adds the value as the first two elements to the third row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float2* **value** - Elements to be added.


## void rowZ ( float3x3 mat , float value )

 Adds the value as the first element to the third row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float* **value** - Element to be added.


## float4 rowZ ( float4x4 mat )

 Returns the third row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Elements of the row.
## void rowZ ( float4x4 mat , float4 value )

 Adds the value elements to the third row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float4* **value** - Elements to be added.


## void rowZ ( float4x4 mat , float3 value )

 Adds the value as the first three elements to the third row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float3* **value** - Elements to be added.


## void rowZ ( float4x4 mat , float2 value )

 Adds the value as the first two elements to the third row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float2* **value** - Elements to be added.


## void rowZ ( float4x4 mat , float value )

 Adds the value as the first element to the third row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Element to be added.


## float4 rowW ( float4x4 mat )

 Returns the fourth row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Elements of the row.
## void rowW ( float4x4 mat , float4 value )

 Adds the value elements to the fourth row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float4* **value** - Elements to be added.


## void rowW ( float4x4 mat , float3 value )

 Adds the value as the first three elements to the fourth row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float3* **value** - Elements to be added.


## void rowW ( float4x4 mat , float2 value )

 Adds the value as the first two elements to the fourth row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float2* **value** - Elements to be added.


## void rowW ( float4x4 mat , float value )

 Adds the value as the first element to the fourth row of the matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Element to be added.


## float get ( float3x3 mat , int x , int y )

 Returns the value from the matrix using its index.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *int* **x** - Row index.
- *int* **y** - Column index.

### Return value

Value.
## float get ( float4x4 mat , int x , int y )

 Returns the value from the matrix using its index.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *int* **x** - Row index.
- *int* **y** - Column index.

### Return value

Value.
## float set ( float3x3 mat , int x , int y , float value )

 Sets the matrix value using its index.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *int* **x** - Row index.
- *int* **y** - Column index.
- *float* **value** - Value.


## float set ( float4x4 mat , int x , int y , float value )

 Sets the matrix value using its index.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *int* **x** - Row index.
- *int* **y** - Column index.
- *float* **value** - Value.


## float m00 ( float3x3 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.

### Return value

Value.
## float m00 ( float4x4 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.


## void m00 ( float3x3 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float* **value** - Value to be set.


## void m00 ( float4x4 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Value to be set.


## float m01 ( float3x3 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.

### Return value

Value.
## float m01 ( float4x4 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Value.
## void m01 ( float3x3 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float* **value** - Value to be set.


## void m01 ( float4x4 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Value to be set.


## float m02 ( float3x3 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.

### Return value

Value.
## float m02 ( float4x4 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Value.
## void m02 ( float3x3 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float* **value** - Value to be set.


## void m02 ( float4x4 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Value to be set.


## float m03 ( float4x4 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Value.
## void m03 ( float4x4 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Value to be set.


## float m10 ( float3x3 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.

### Return value

Value.
## float m10 ( float4x4 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Value.
## void m10 ( float3x3 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float* **value** - Value to be set.


## void m10 ( float4x4 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Value to be set.


## float m11 ( float3x3 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.

### Return value

Value.
## float m11 ( float4x4 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Value.
## void m11 ( float3x3 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float* **value** - Value to be set.


## void m11 ( float4x4 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Value to be set.


## float m12 ( float3x3 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.

### Return value

Value.
## float m12 ( float4x4 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Value.
## void m12 ( float3x3 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float* **value** - Value to be set.


## void m12 ( float4x4 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Value to be set.


## float m13 ( float4x4 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Value.
## void m13 ( float4x4 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Value to be set.


## float m20 ( float3x3 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.

### Return value

Value.
## float m20 ( float4x4 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Value.
## void m20 ( float3x3 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float* **value** - Value to be set.


## void m20 ( float4x4 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Value to be set.


## float m21 ( float3x3 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.

### Return value

Value.
## float m21 ( float4x4 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Value.
## void m21 ( float3x3 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float* **value** - Value to be set.


## void m21 ( float4x4 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Value to be set.


## float m22 ( float3x3 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.

### Return value

Value.
## float m22 ( float4x4 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Value.
## void m22 ( float3x3 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float3x3* **mat** - 3x3 matrix.
- *float* **value** - Value to be set.


## void m22 ( float4x4 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Value to be set.


## float m23 ( float4x4 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Value.
## void m23 ( float4x4 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Value to be set.


## float m30 ( float4x4 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Value.
## void m30 ( float4x4 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Value to be set.


## float m31 ( float4x4 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Value.
## void m31 ( float4x4 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Value to be set.


## float m32 ( float4x4 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Value.
## void m32 ( float4x4 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Value to be set.


## float m33 ( float4x4 mat )

 Returns the corresponding matrix value.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Value.
## void m33 ( float4x4 mat , float value )

 Sets the argument value as the corresponding matrix element.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.
- *float* **value** - Value to be set.


## float3x3 matrix3 ( float m00 , float m10 , float m20 , float m01 , float m11 , float m21 , float m02 , float m12 , float m22 )

 Returns the matrix with the argument values set as its elements.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **m00** - Value to be set.
- *float* **m10** - Value to be set.
- *float* **m20** - Value to be set.
- *float* **m01** - Value to be set.
- *float* **m11** - Value to be set.
- *float* **m21** - Value to be set.
- *float* **m02** - Value to be set.
- *float* **m12** - Value to be set.
- *float* **m22** - Value to be set.

### Return value

3x3 matrix.
## float4x4 matrix4 ( float m00 , float m10 , float m20 , float m30 , float m01 , float m11 , float m21 , float m31 , float m02 , float m12 , float m22 , float m32 , float m03 , float m13 , float m23 , float m33 )

 Returns the matrix with the argument values set as its elements.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float* **m00** - Value to be set.
- *float* **m10** - Value to be set.
- *float* **m20** - Value to be set.
- *float* **m30** - Value to be set.
- *float* **m01** - Value to be set.
- *float* **m11** - Value to be set.
- *float* **m21** - Value to be set.
- *float* **m31** - Value to be set.
- *float* **m02** - Value to be set.
- *float* **m12** - Value to be set.
- *float* **m22** - Value to be set.
- *float* **m32** - Value to be set.
- *float* **m03** - Value to be set.
- *float* **m13** - Value to be set.
- *float* **m23** - Value to be set.
- *float* **m33** - Value to be set.

### Return value

4x4 matrix.
## float4x4 inverse ( float4x4 mat )

 Returns the inverse matrix.
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

4x4 matrix.
## float4x4 inverseTransform ( float4x4 mat )

 Returns the inverse of the transformation matrix part (with the translation part filled with zeroes).
 **This function is [API-dependent](#api_dependent).**
### Arguments

- *float4x4* **mat** - 4x4 matrix.

### Return value

Inverse of the transformation matrix part (with the translation part filled with zeroes).
## bool isOrtho ( float4x4 projection )

Checks if the projection matrix is for orthogonal projection.
### Arguments

- *float4x4* **projection** - Projection matrix.

### Return value

True is the projection matrix is orthogonal projection matrix; otherwise, false.
## float3 basisX ( float3x3 m )


Returns the X basis of the 3x3 matrix.


**Equivalent**


```glsl
m._m00_m10_m20;
```


### Arguments

- *float3x3* **m** - 3x3 matrix.

### Return value

Matrix basis.
## float3 basisX ( float4x4 m )


Returns the X basis of the 4x4 matrix.


**Equivalent**


```glsl
m._m00_m10_m20;
```


### Arguments

- *float4x4* **m** - 4x4 matrix.

### Return value

Matrix basis.
## float3 basisY ( float3x3 m )


Returns the Y basis of the 3x3 matrix.


**Equivalent**


```glsl
m._m01_m11_m21;
```


### Arguments

- *float3x3* **m** - 3x3 matrix.

### Return value

Matrix basis.
## float3 basisY ( float4x4 m )


Returns the Y basis of the 4x4 matrix.


**Equivalent**


```glsl
m._m01_m11_m21;
```


### Arguments

- *float4x4* **m** - 4x4 matrix.

### Return value

Matrix basis.
## float3 basisZ ( float3x3 m )


Returns the Z basis of the 3x3 matrix.


**Equivalent**


```glsl
m._m02_m12_m22;
```


### Arguments

- *float3x3* **m** - 3x3 matrix.

### Return value

Matrix basis.
## float3 basisZ ( float4x4 m )


Returns the Z basis of the given 4x4 matrix.


**Equivalent**


```glsl
m._m02_m12_m22;
```


### Arguments

- *float4x4* **m** - 4x4 matrix.

### Return value

Matrix basis.
## float3x3 orthonormalize ( float3x3 mat )

Orthonormalizes a matrix.
### Arguments

- *float3x3* **mat** - Matrix to be orthonormalized.

### Return value

Orthonormal matrix.
## void orthonormalize ( float3 x , float3 y , float3 z )

### Arguments

- *float3* **x**
- *float3* **y**
- *float3* **z**


## float3x3 scale ( float3 value )


Returns scaling matrix for the specified scaling vector (X, Y, Z):


| X | 0.0 | 0.0 | 0.0 |
|---|---|---|---|
| 0.0 | Y | 0.0 | 0.0 |
| 0.0 | 0.0 | Z | 0.0 |
| 0.0 | 0.0 | 0.0 | 1.0 |


### Arguments

- *float3* **value** - Scaling vector (X,Y,Z).

### Return value

Scaling matrix.
## float3x3 scale ( float x , float y , float z )


Returns scaling matrix for the specified scaling vector (X, Y, Z):


| X | 0.0 | 0.0 | 0.0 |
|---|---|---|---|
| 0.0 | Y | 0.0 | 0.0 |
| 0.0 | 0.0 | Z | 0.0 |
| 0.0 | 0.0 | 0.0 | 1.0 |


### Arguments

- *float* **x** - X component of the scaling vector.
- *float* **y** - Y component of the scaling vector.
- *float* **z** - Z component of the scaling vector.

### Return value

Scaling matrix.
## float4x4 translate ( float3 position )


Returns the translation matrix for the specified translation vector (X, Y, Z):


| 1.0 | 0.0 | 0.0 | X |
|---|---|---|---|
| 0.0 | 1.0 | 0.0 | Y |
| 0.0 | 0.0 | 1.0 | Z |
| 0.0 | 0.0 | 0.0 | 1.0 |


### Arguments

- *float3* **position** - Translation vector (X, Y, Z).

### Return value

Translation matrix.
## float4x4 translate ( float x , float y , float z )


Returns the translation matrix for the specified translation vector (X, Y, Z):


| 1.0 | 0.0 | 0.0 | X |
|---|---|---|---|
| 0.0 | 1.0 | 0.0 | Y |
| 0.0 | 0.0 | 1.0 | Z |
| 0.0 | 0.0 | 0.0 | 1.0 |


### Arguments

- *float* **x** - X component of the translation vector.
- *float* **y** - Y component of the translation vector.
- *float* **z** - Z component of the translation vector.

### Return value

Translation matrix.
## float3 decomposeEuler ( float3x3 mat )


Decomposes the rotation matrix to the vector of Euler angles (pitch, roll, yaw).


The Euler angles are specified in the axis rotation sequence - XYZ. It is an order of the rings in the three-axis gimbal set: X axis used as the outer ring (independent ring), while Z axis as the inner one (its rotation depends on other 2 rings).


When we talk about axes in UNIGINE, we assume that:


- **X** axis points to the right giving us a **pitch** angle.
- **Y** axis points forward giving us a **roll** angle.
- **Z** axis points up giving us a **yaw** (heading) angle.


> **Notice:** Players have a different coordinate system:
>
>
> - **X** axis points to the *right* giving us a **pitch** angle.
> - **Y** axis points *up* giving us a **yaw** (heading) angle.
> - **Z** axis points *backward* giving us a **-roll** angle.


### Arguments

- *float3x3* **mat** - Rotation matrix.

### Return value

Vector of Euler angles (pitch, roll, yaw).
## float3x3 rotateEuler ( float3 euler )


Returns the rotation matrix from the vector of Euler angles (pitch, roll, yaw).


The Euler angles are specified in the axis rotation sequence - XYZ. It is an order of the rings in the three-axis gimbal set: X axis used as the outer ring (independent ring), while Z axis as the inner one (its rotation depends on other 2 rings).


When we talk about axes in UNIGINE, we assume that:


- **X** axis points to the right giving us a **pitch** angle.
- **Y** axis points forward giving us a **roll** angle.
- **Z** axis points up giving us a **yaw** (heading) angle.


> **Notice:** Players have a different coordinate system:
>
>
> - **X** axis points to the *right* giving us a **pitch** angle.
> - **Y** axis points *up* giving us a **yaw** (heading) angle.
> - **Z** axis points *backward* giving us a **-roll** angle.


### Arguments

- *float3* **euler** - Vector of Euler angles (pitch, roll, yaw).

### Return value

Rotation matrix.
## float3x3 rotateAxis ( float3 axis , float radians )

Returns the rotation matrix for the angle, in radians, around the specified axis.
### Arguments

- *float3* **axis** - Axis to rotate around.
- *float* **radians** - Rotation angle, in radians.

### Return value

Rotation matrix.
## float3x3 rotateX ( float angle )

Returns the rotation matrix for the angle, in degrees, around the X axis.
### Arguments

- *float* **angle** - Rotation angle, in degrees.

### Return value

Rotation matrix.
## float3x3 rotateY ( float angle )

Returns the rotation matrix for the angle, in degrees, around the Y axis.
### Arguments

- *float* **angle** - Rotation angle, in degrees.

### Return value

Rotation matrix.
## float3x3 rotateZ ( float angle )

Returns the rotation matrix for the angle, in degrees, around the Z axis.
### Arguments

- *float* **angle** - Rotation angle, in degrees.

### Return value

Rotation matrix.
## void decomposeTransform ( float4x4 transform , float3 position , float3x3 rotation , float3 scale )

Decomposes the transformation matrix into the position, rotation, and scale components.
### Arguments

- *float4x4* **transform** - Transformation matrix.
- *float3* **position** - Position vector.
- *float3x3* **rotation** - Rotation vector.
- *float3* **scale** - Scaling vector.


## float4x4 composeTransform ( float3 position , float3x3 rotation , float3 scale )

Returns the transformation matrix composed from the position, rotation, and scale components.
### Arguments

- *float3* **position** - Position vector.
- *float3x3* **rotation** - Rotation vector.
- *float3* **scale** - Scaling vector.

### Return value

Transformation matrix.
## float4x4 ortho ( float l , float r , float b , float t , float n , float f )


Returns the parallel projection matrix:


| 2.0 / (right - left) | 0.0 | 0.0 | -(right + left) / (right - left) |
|---|---|---|---|
| 0.0 | 2.0 / (top - bottom) | 0.0 | -(top + bottom) / (top - bottom) |
| 0.0 | 0.0 | -2.0 / (zfar - znear) | -(zfar + znear) / (zfar - znear) |
| 0.0 | 0.0 | 0.0 | 1.0 |


### Arguments

- *float* **l** - Left vertical clipping plane.
- *float* **r** - Right vertical clipping plane.
- *float* **b** - Bottom horizontal clipping plane.
- *float* **t** - Top horizontal clipping plane.
- *float* **n** - Distance to the near depth clipping plane.
- *float* **f** - Distance to the farther depth clipping plane.

### Return value

Parallel projection matrix.
## float4x4 frustum ( float l , float r , float b , float t , float n , float f )


Returns the perspective projection matrix:


| 2.0 * znear / (right - left) | 0.0 | (right + left) / (right - left) | 0.0 |
|---|---|---|---|
| 0.0 | 2.0 * znear / (top - bottom) | (top + bottom) / (top - bottom) | 0.0 |
| 0.0 | 0.0 | -(zfar + znear) / (zfar - znear) | -2.0 * zfar * znear / (zfar - znear) |
| 0.0 | 0.0 | -1.0 | 0.0 |


Coordinates of top, left, right, bottom are set relatively to center point of the znear plane.


![](../../api/library/math/frustum_desc.png)


There are two different points (A and B) on the picture above. Since the top, left, right, bottom are coordinates relatively to the center point of the znear plane, coordinates of the A point should be *A(left, bottom, znear)*. Coordinates of the B point are *B(k * left, k * bottom, zfar)*, where *k = zfar/znear.*


### Arguments

- *float* **l** - Left coordinate of the near clipping plane relatively to the center.
- *float* **r** - Right coordinate of the near clipping plane relatively to the center.
- *float* **b** - Bottom coordinate of the near clipping plane relatively to the center.
- *float* **t** - Top coordinate of the near clipping plane relatively to the center.
- *float* **n** - Distance to the near depth clipping plane.
- *float* **f** - Distance to the farther depth clipping plane.

### Return value

Perspective projection matrix.
## float4x4 perspective ( float fov , float aspect , float n , float f )

Returns the perspective projection matrix.
### Arguments

- *float* **fov** - Field of view angle.
- *float* **aspect** - Aspect ratio (the ratio of width to height).
- *float* **n** - Distance to the near depth clipping plane.
- *float* **f** - Distance to the farther depth clipping plane.

### Return value

Perspective projection matrix.
## float3x3 cubeTransform ( int face )

Outputs the cube viewing matrix for the specified cube face.
### Arguments

- *int* **face** - Cube face from 0 to 5:

  - 0 � positive X face (right)
  - 1 � negative X face (left)
  - 2 � positive Y face (front)
  - 3 � negative Y face (back)
  - 4 � positive Z face (top)
  - 5 � negative Z face (bottom)

### Return value

Cube viewing matrix for the specified cube face.
## void normalizationTBN ( float3 T , float3 B , float3 N , float sign_binormal )

Calculates normalized Tangent, Binormal, and Normal vectors.
### Arguments

- *float3* **T** - Tangent vector.
- *float3* **B** - Binormal vector.
- *float3* **N** - Normal vector.
- *float* **sign_binormal** - Binormal vector sign (ATTRIBUTE_BASIS.w)


## float3x3 normalToTBN ( float3 N )

Returns TBN matrix containing Tangent, Binormal and Normal vectors out of a Normal vector.
### Arguments

- *float3* **N** - Normal vector.

### Return value

TBN matrix.
