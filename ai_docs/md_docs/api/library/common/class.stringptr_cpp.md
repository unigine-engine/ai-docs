# Unigine::StringPtr class (CPP)

**Header:** #include <UnigineString.h>


## StringPtr Class

### Members

---

## static StringPtrPtr create ( )

Default constructor that creates an string.
## static StringPtrPtr create ( const String & s )

Copy constructor.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s** - String to be copied.

## static StringPtrPtr create ( const String Ptr & s )

Copy constructor.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md)Ptr &* **s** - String to be copied.

## static StringPtrPtr create ( const char * s )

Copy constructor.
### Arguments

- *const char ** **s** - String to be copied.

## String Ptr & operator= ( const String Ptr & s )

Assignment operator for the string.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md)Ptr &* **s** - The value of the string.

## String Ptr & operator= ( const char * s )

Assignment operator for the string.
### Arguments

- *const char ** **s** - The value of the string.

## String Ptr & operator= ( const String & s )

Assignment operator for the string.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s** - The value of the string.

## void clear ( )

Clears the pointer to the string.
## int empty ( )

Returns an empty flag.
### Return value

1 if the string is empty; otherwise, 0.
## int size ( )

Returns the size of the string.
### Return value

The size of the string.
## String Ptr & operator+= ( const String & s )

String addition.
### Arguments

- *const [String](../../../api/library/common/class.string_cpp.md) &* **s** - The second string.

## String Ptr & operator+= ( const char * s )

String addition.
### Arguments

- *const char ** **s** - The symbol.

## void swap ( String Ptr & s )

Swaps contents of the current string and the given one.
### Arguments

- *[String](../../../api/library/common/class.string_cpp.md)Ptr &* **s** - The second string.

## const char * get ( )

Returns the pointer to the null-terminated string.
### Return value

The null-terminated string.
## const void * operator const void * ( )

Returns the pointer to the current string.
### Return value

Pointer to the string.
## const char * operator const char * ( )

Returns the pointer to the current string.
### Return value

Pointer to the string.
## const String & getString ( )

Returns the string.
### Return value

String.
