# Unigine::Vector::ConstIterator Class (CPP)

**Header:** #include <UnigineVector.h>


## Vector::ConstIterator Class

### Members

---

## DataTypeType Definition

### Description

Full declaration:
 *typedef Type Unigine::Vector< Type >::ConstIterator::DataType*


### Return value

 Type
---

## const Type & get ( ) const

Returns iterator's node pointer.
### Return value

The iterator's node pointer.
## ConstIterator ( )

Default constructor.
## ConstIterator ( const Iterator & it )

Copy constructor.
### Arguments

- *const Iterator &* **it** - Iterator.

## int operator!= ( const typename Vector < Type >::Iterator & it ) const

Check if two iterators are not the same.
### Arguments

- *const typename [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Type >::Iterator &* **it** - The second iterator.

### Return value

1 if iterators are not the same; otherwise, 0.
## int operator!= ( const ConstIterator & it ) const

Check if two iterators are not the same.
### Arguments

- *const ConstIterator &* **it** - The second iterator.

### Return value

1 if iterators are not the same; otherwise, 0.
## const Type & operator* ( ) const

Returns iterator's node reference.
### Return value

The iterator's node reference.
## ConstIterator operator+ ( int n ) const

Increases the iterator position.
### Arguments

- *int* **n** - The iterator increment.

### Return value

The iterator referring to the next element.
## ConstIterator & operator++ ( )

Increases the iterator position.
### Return value

The iterator referring to the next element.
## ConstIterator operator++ ( )

Increases the iterator position.
### Return value

The iterator referring to the current element.
## ConstIterator & operator+= ( int n )

Increases the iterator position.
### Arguments

- *int* **n** - The iterator increment.

### Return value

The iterator referring to the next element.
## ConstIterator operator- ( int n ) const

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
## ConstIterator & operator-= ( int n )

Decreases the iterator position.
### Arguments

- *int* **n** - The iterator decrement.

### Return value

The iterator referring to the prev element.
## const Type * operator-> ( ) const

Returns iterator's node pointer.
### Return value

The iterator's node.
## ConstIterator & operator= ( const ConstIterator & it )

Assignment operator for the iterator.
### Arguments

- *const ConstIterator &* **it** - Iterator.

## int operator== ( const typename Vector < Type >::Iterator & it ) const

Check if two iterators are actually the same.
### Arguments

- *const typename [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Type >::Iterator &* **it** - The second iterator.

### Return value

1 if iterators are the same; otherwise, 0.
## int operator== ( const ConstIterator & it ) const

Check if two iterators are actually the same.
### Arguments

- *const ConstIterator &* **it** - The second iterator.

### Return value

1 if iterators are the same; otherwise, 0.
## ~ConstIterator ( )

Destructor.
