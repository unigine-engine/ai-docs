# Unigine::UGUID Class (CPP)

**Header:** #include <UnigineGUID.h>


This class represents a globally unique identifier (a 40-byte hash value). The [SHA1](http://www.faqs.org/rfcs/rfc3174.html) algorithm is used for hash generation.


## UGUID Class

### Members

---

## UGUID ( )

Default constructor. Creates an empty 0-filled UGUID.
## UGUID ( const char * str )

Constructor. Creates a UGUID from the given source string. UGUID is generated using the [SHA1](http://www.faqs.org/rfcs/rfc3174.html) algorithm.
### Arguments

- *const char ** **str** - Source string.

## UGUID ( unsigned char(& value_ )[VALUE_SIZE] )

Constructor. Creates a UGUID from the given source value. UGUID is generated using the [SHA1](http://www.faqs.org/rfcs/rfc3174.html) algorithm.
### Arguments

## UGUID ( unsigned int(& value_ )[NUM_VALUE_INT] )

Constructor. Creates a UGUID from the given source value. UGUID is generated using the [SHA1](http://www.faqs.org/rfcs/rfc3174.html) algorithm.
### Arguments

## UGUID ( const String & str )

Constructor. Creates a UGUID from the given source string. UGUID is generated using the [SHA1](http://www.faqs.org/rfcs/rfc3174.html) algorithm.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **str** - Source string.

## UGUID ( const UGUID & guid )

Copy constructor. Creates a UGUID by copying a source UGUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **guid** - Source UGUID.

## void generate ( )

Generates a new random UGUID value.
## void generate ( const char * str )

Generates a UGUID value from the given source string using the [SHA1](http://www.faqs.org/rfcs/rfc3174.html) algorithm.
### Arguments

- *const char ** **str** - Source string.

## void generate ( int& seed_ )

Generates a random UGUID value using the seed value.
### Arguments

- *int&* **seed_** - Seed value.

## void generate ( const void* data , int size )

Generates a UGUID value from the given source byte array of the specified size using the [SHA1](http://www.faqs.org/rfcs/rfc3174.html) algorithm.
### Arguments

- *const void** **data** - Source byte array.
- *int* **size** - Number of bytes to be taken from the byte array for UGUID generation.

## unsigned int hash ( )

Returns a hash for the UGUID value.
### Return value

Hash generated for the UGUID value.
## static bool lexicographicalLess ( const UGUID & left , const UGUID & right )

Compares two values and returns a value indicating whether the first one goes before the second one. The order is the same on every platform, so it can be used to sort values into a stable sequence - when writing them to a file, for example.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **left** - First value to be compared.
- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **right** - Second value to be compared.

### Return value

true if the first value goes before the second one; otherwise, false.
## void clear ( )

Clears the UGUID value. All 40 bytes are set to 0.
## bool isEmpty ( ) const

Returns a value indicating if the UGUID is empty (all 40 bytes are equal to 0).
### Return value

**true** if the UGUID is empty; otherwise, false.
## bool isValid ( ) const

Returns a value indicating if the UGUID has a valid value.
### Return value

**true** if the value is valid; otherwise, false.
## void setString ( const char * str )

Sets the UGUID value equal to a given 40-character hexadecimal string.
### Arguments

- *const char ** **str** - 40-character hexadecimal string representing the UGUID value.

## UGUID & operator= ( const char * str )

Performs UGUID assignment. The value of the destination UGUID is set equal to the source hexadecimal string.
### Arguments

- *const char ** **str** - Source string. A 40-character hexadecimal string representing the UGUID value.

### Return value

Result.
## UGUID & operator= ( const String & str )

Performs UGUID assignment. The value of the destination UGUID is set equal to the source string.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **str** - Source string.

### Return value

Result.
## UGUID & operator= ( const UGUID & g )

Performs UGUID assignment. Destination UGUID = Source UGUID.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **g** - Source UGUID.

### Return value

Result.
## int operator> ( const UGUID & g )

Indicates whether the UGUID value is greater than the source UGUID value.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **g** - Source UGUID.

### Return value

**1** if the UGUID value is greater than the source UGUID value; otherwise, 0.
## int operator>= ( const UGUID & g )

Indicates whether the UGUID value is greater than or equal to the source UGUID value.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **g** - Source UGUID.

### Return value

**1** if the UGUID value is greater than or equal to the source UGUID value; otherwise, 0.
## int operator< ( const UGUID & g )

Indicates whether the UGUID value is less than the source UGUID value.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **g** - Source UGUID.

### Return value

**1** if the UGUID value is less than or equal to the source UGUID value; otherwise, 0.
## int operator<= ( const UGUID & g )

Indicates whether the UGUID value is less than or equal to the source UGUID value.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **g** - Source UGUID.

### Return value

**1** if the UGUID value is less than or equal to the source UGUID value; otherwise, 0.
## int operator== ( const UGUID & g )

Equality. Indicates whether the UGUID value is equal to the source UGUID value.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **g** - Source UGUID.

### Return value

**1** if the UGUID value is equal to the source UGUID value; otherwise, 0.
## int operator!= ( const UGUID & g )

Inequality. Indicates whether the UGUID value is not equal to the source UGUID value.
### Arguments

- *const [UGUID](../../../api/library/filesystem/class.uguid_cpp.md) &* **g** - Source UGUID.

### Return value

**1** if the UGUID value is not equal to the source UGUID value; otherwise, 0.
## const char * get ( )

Returns the UGUID value as a string.
### Return value

String.
## char & get ( int index )

Returns a UGUID character by index.
### Arguments

- *int* **index** - Index of the character

### Return value

Character of UGUID
## char get ( int index )

Constant array access.
### Arguments

- *int* **index** - Array item index

### Return value

Array item
## const unsigned char * getValue ( ) const

Returns the pointer to the internal data buffer.
### Return value

Pointer to the internal data buffer.
## char & operator[] ( int index )

Array access.
### Arguments

- *int* **index** - Array item index

### Return value

Array item
## char operator[] ( int index )

Item access by index.
### Arguments

- *int* **index** - Array item index

### Return value

Array item
## const char * operator const char * ( )

Returns the pointer to the current string.
### Return value

Pointer to the current string
## const void * operator const void * ( )

Returns the pointer to the current string.
## GUIDString makeString ( ) const

Creates a 40-character hexadecimal string representing the GUID value.
### Return value

40-character hexadecimal string representing the GUID value.
