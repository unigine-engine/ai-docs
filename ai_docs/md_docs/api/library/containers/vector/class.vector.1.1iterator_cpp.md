# Unigine::Vector::Iterator Class (CPP)

**Header:** #include <UnigineVector.h>


## Vector::Iterator Class

### Members

---

## Type & get ( ) const

Returns iterator's node pointer.
### Return value

The iterator's node pointer.
## Iterator ( )

Default constructor.
## Iterator ( const Iterator & it )

Copy constructor.
### Arguments

- *const Iterator &* **it** - Iterator.

## int operator!= ( const Iterator & it ) const

Check if two iterators are not the same.
### Arguments

- *const Iterator &* **it** - The second iterator.

### Return value

1 if iterators are not the same; otherwise, 0.
## int operator!= ( const typename Vector < Type >::ConstIterator & it ) const

Check if two iterators are not the same.
### Arguments

- *const typename [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Type >::ConstIterator &* **it** - The second iterator.

### Return value

1 if iterators are not the same; otherwise, 0.
## Type & operator* ( ) const

Returns iterator's node reference.
### Return value

The iterator's node reference.
## Iterator operator+ ( int n ) const

Increases the iterator position.
### Arguments

- *int* **n** - The iterator increment.

### Return value

The iterator referring to the next element.
## Iterator & operator++ ( )

Increases the iterator position.
### Return value

The iterator referring to the next element.
## Iterator operator++ ( )

Increases the iterator position.
### Return value

The iterator referring to the current element.
## Iterator & operator+= ( int n )

Increases the iterator position.
### Arguments

- *int* **n** - The iterator increment.

### Return value

The iterator referring to the next element.
## Iterator operator- ( int n ) const

Decreases the iterator position.
### Arguments

- *int* **n** - The iterator decrement.

### Return value

The iterator referring to the prev element.
## int operator- ( const Iterator & it ) const

Returns the distance between iterators.
### Arguments

- *const Iterator &* **it** - The second iterator.

### Return value

The distance between iterators.
## int operator- ( const ConstIterator & it ) const

Returns the distance between iterators.
### Arguments

- *const ConstIterator &* **it** - The second iterator.

### Return value

The distance between iterators.
## Iterator & operator-= ( int n )

Decreases the iterator position.
### Arguments

- *int* **n** - The iterator decrement.

### Return value

The iterator referring to the prev element.
## Type * operator-> ( ) const

Returns iterator's node pointer.
### Return value

The iterator's node.
## Iterator & operator= ( const Iterator & it )

Assignment operator for the iterator.
### Arguments

- *const Iterator &* **it** - Iterator.

## int operator== ( const Iterator & it ) const

Check if two iterators are actually the same.
### Arguments

- *const Iterator &* **it** - The second iterator.

### Return value

1 if iterators are the same; otherwise, 0.
## int operator== ( const typename Vector < Type >::ConstIterator & it ) const

Check if two iterators are actually the same.
### Arguments

- *const typename [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Type >::ConstIterator &* **it** - The second iterator.

### Return value

1 if iterators are the same; otherwise, 0.
## ~Iterator ( )

Destructor.
