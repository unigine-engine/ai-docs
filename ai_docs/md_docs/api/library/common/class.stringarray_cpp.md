# Unigine::StringArray class (CPP)

**Header:** #include <UnigineString.h>


An array of strings.


## StringArray Class

### Members

---

## static StringArrayPtr create ( int size )

Constructor. Creates an empty string array of the given size.
### Arguments

- *int* **size** - Array size.

## static StringArrayPtr create ( const StringArray <Capacity> & s )

Copy constructor.
### Arguments

- *const [StringArray](../../../api/library/common/class.stringarray_cpp.md)<Capacity> &* **s** - Array of strings.

## int empty ( )

Returns a value indicating if the array of strings is empty.
### Return value

1 if the array is empty, otherwise 0.
## const char * operator[] ( int index )

Array access.
### Arguments

- *int* **index** - The array item index.

### Return value

The array item.
## int size ( )

Returns the size of the array of strings.
### Return value

Array size.
