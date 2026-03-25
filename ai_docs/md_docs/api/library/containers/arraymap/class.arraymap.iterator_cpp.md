# Unigine::ArrayMap::Iterator Class (CPP)

**Header:** #include <UnigineInterpreter.h>


## ArrayMap::Iterator Class

### Members

---

## Iterator ( )

Iterator default constructor.
## Iterator ( const ArrayMap::Iterator & it )

Iterator copy constructor.
### Arguments

- *const ArrayMap::Iterator &* **it** - Iterator instance to be copied.

## const Variable & get ( )

Returns iterator's data.
### Return value

The iterator's data.
## const Variable & key ( )

Returns iterator's key.
### Return value

The iterator's key.
## int operator!= ( const ArrayMap::Iterator & it )

Iterator not equal comparison.
### Arguments

- *const ArrayMap::Iterator &* **it** - The second iterator to be compared with.

### Return value

The result of operation.
## ArrayMap::Iterator & operator++ ( )

Increases the iterator position (performs pre-increment operation: *++iterator*).
### Return value

The result of operation.
## ArrayMap::Iterator operator++ ( int )

Increases the iterator position (performs post-increment operation: *iterator++*)
### Arguments

- *int*

### Return value

The result of operation.
## ArrayMap::Iterator operator-- ( int )

Decreases the iterator position (performs post-decrement operation: *iterator--*).
### Arguments

- *int*

### Return value

The result of operation.
## ArrayMap::Iterator & operator-- ( )

Decreases the iterator position (performs pre-decrement operation: *--iterator*)
### Return value

The result of operation.
## ArrayMap::Iterator & operator= ( const ArrayMap::Iterator & it )

Assignment operator for the iterator.
### Arguments

- *const ArrayMap::Iterator &* **it** - Assignment operator for the iterator.

### Return value

The assigned iterator.
## int operator== ( const ArrayMap::Iterator & it )

Iterator equal comparison.
### Arguments

- *const ArrayMap::Iterator &* **it** - The second iterator.

### Return value

The result.
