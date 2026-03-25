# Unigine::Vector Class (CPP)

**Header:** #include <UnigineVector.h>


A vector container template.


> **Warning:** In UnigineScript, a vector is a sequence container which represents an array of flexible size. See [Containers](../../../../code/uniginescript/language/containers/index.md#vector) article for the details.


## Vector Class

### Members

---

## Vector ( )

Default constructor. Produces an empty vector.
## Vector ( const Vector < Type > & v )

Copy constructor.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Type > &* **v** - Vector.

## Vector ( const Type & t , size_t size )

Constructor. Produces a vector with a specified size and initialization.
### Arguments

- *const Type &* **t** - Item value.
- *size_t* **size** - Vector size.

## Vector ( const Type * v , size_t size )

Copy constructor. Produces a vector with a specified size.
### Arguments

- *const Type ** **v** - Vector pointer.
- *size_t* **size** - Vector size.

## explicit Vector ( size_t size )

Explicit constructor. Produces a vector with specified size.
### Arguments

- *size_t* **size** - Vector size.

## ~Vector ( )

Destructor.
## void set ( size_t index , const Type & t )

Sets an item with a given index.
### Arguments

- *size_t* **index** - Item index.
- *const Type &* **t** - Item to set.

## Type & get ( size_t index )

Returns an item by a given index.
### Arguments

- *size_t* **index** - Item index.

### Return value

Item.
## const Type & get ( size_t index ) const

Returns a constant item by a given index.
### Arguments

- *size_t* **index** - Item index.

### Return value

Item.
## Type * get ( )

Returns the pointer to the vector.
### Return value

Pointer to the vector.
## const Type * get ( ) const

Returns the constant pointer to the vector.
### Return value

Constant pointer to the vector.
## void allocate ( size_t size )

Reserves the exact amount of memory enough to contain the specified number of items.
### Arguments

- *size_t* **size** - Exact vector size. > **Notice:** If the specified value is greater than the current vector capacity, the method causes the container to reallocate its storage increasing capacity to the specified value. In all other cases the capacity is not affected.

## void append ( const Type & t )

Adds the item to the end of the vector.
### Arguments

- *const Type &* **t** - Item to append.

## void append ( size_t pos , const Type & t )

Appends an item at a given position.
### Arguments

- *size_t* **pos** - Position.
- *const Type &* **t** - Item to append.

## void append ( const Vector < Type > & v )

Appends a vector.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Type > &* **v** - Vector to append.

## void append ( const Type * v , size_t size )

Appends a vector with a given size.
### Arguments

- *const Type ** **v** - Pointer to the vector to append.
- *size_t* **size** - Vector size.

## void appendFast ( const Type & t )

Adds the item to the end of the vector. Using this method implies that you have enough memory allocated via the [allocate()](#allocate_int)/[reserve()](#reserve_int) methods.
### Arguments

- *const Type &* **t** - Item to append.

## void appendFast ( size_t pos , const Type & t )

Appends an item at a given position.
### Arguments

- *size_t* **pos** - Position.
- *const Type &* **t** - Item to append.

## void appendFast ( const Vector < Type > & v )

Appends a vector.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Type > &* **v** - Vector to append.

## void appendFast ( const Type * v , size_t size )

Appends a vector with a given size.
### Arguments

- *const Type ** **v** - Vector to append.
- *size_t* **size** - Vector size.

## void appendUnique ( const Type & t )

Appends the item if the vector doesn't contain it.
### Arguments

- *const Type &* **t** - Item to append.

## void at ( size_t index )

Returns a reference to the element at a specified location in the vector.
### Arguments

- *size_t* **index** - Item index.

## void at ( size_t index ) const

Returns a reference to the element at a specified location in the vector.
### Arguments

- *size_t* **index** - Item index.

## Iterator back ( )

Returns a reference to the last element in the vector. Unlike the method [end()](#end), which returns an iterator just past this element, this function returns a direct reference.
### Return value

Back iterator.
## ConstIterator back ( ) const

Returns a reference to the last element in the vector. Unlike the method [end()](#end), which returns an iterator just past this element, this function returns a direct reference.
### Return value

Back iterator.
## Iterator begin ( )

Returns an iterator pointing to the first element in the vector. Unlike the [front()](#front) method, which returns a reference to the first element, this function returns a random access iterator pointing to it.
### Return value

Begin iterator.
## ConstIterator begin ( ) const

Returns an iterator pointing to the first element in the vector. Unlike the [front()](#front) method, which returns a reference to the first element, this function returns a random access iterator pointing to it.
### Return value

Begin iterator.
## ConstIterator cbegin ( ) const

Returns the constant iterator pointing to the first element in the vector.
### Return value

Constant iterator.
## ReverseIterator rbegin ( ) const

Returns the reverse iterator pointing to the first element in the vector.
### Return value

Reverse iterator.
## ConstReverseIterator crbegin ( ) const

Returns the constant reverse iterator pointing to the first element in the vector.
### Return value

Constant reverse iterator.
## void clear ( )

Clears the vector without deallocating the memory. To clear the vector and deallocate the memory, use the [destroy()](#destroy) method.
## bool contains ( const T & t ) const

Returns a value indicating if the vector contains the specified item.
### Arguments

- *const T &* **t** - Item.

### Return value

**true** if the vector contains the specified item; otherwise, **false**.
## void destroy ( )

Clears the vector and deallocates the memory. To clear the vector without deallocating the memory, use the [clear()](#clear) method.
## bool empty ( ) const

Returns a value indicating if the vector is empty.
### Return value

**true** if the vector is empty; otherwise, **false**.
## Iterator end ( )

Returns an iterator referring to the past-the-end element in the vector container.
### Return value

End iterator.
## ConstIterator end ( ) const

Returns an iterator referring to the past-the-end element in the vector container.
### Return value

End iterator.
## ConstIterator cend ( ) const

Returns a constant iterator referring to the past-the-end element in the vector container.
### Return value

Constant iterator.
## ReverseIterator rend ( ) const

Returns a reverse iterator referring to the past-the-end element in the vector container.
### Return value

Reverse iterator.
## ConstReverseIterator crend ( ) const

Returns a constant reverse iterator referring to the past-the-end element in the vector container.
### Return value

Constant reverse iterator.
## Iterator find ( const T & t )

Finds an item in the vector.
### Arguments

- *const T &* **t** - Item.

### Return value

Iterator.
## ConstIterator find ( const T & t ) const

Finds an item in the vector.
### Arguments

- *const T &* **t** - Item.

### Return value

Const iterator.
## int findIndex ( const T & t ) const

Finds an index of a given item in the vector.
### Arguments

- *const T &* **t** - Item.

### Return value

Item index.
## int leftIndex ( const T & t ) const

Returns the index of the left neighbor of a given item.
### Arguments

- *const T &* **t** - Item.

### Return value

Left neighbor index.
## Type * first ( )

Returns the value of the first element of the vector.
### Return value

The value of the first element.
## const Type * first ( ) const

Returns the value of the first element of the vector.
### Return value

The value of the first element.
## Iterator front ( )

Returns a reference to the first element in the vector. Unlike the [begin()](#begin) method, which returns an iterator to this same element, this function returns a direct reference.
### Return value

The front iterator.
## ConstIterator front ( ) const

Returns a reference to the first element in the vector. Unlike the [begin()](#begin) method, which returns an iterator to this same element, this function returns a direct reference.
### Return value

The front iterator.
## size_t getMaxSize ( ) const

Returns the maximum number of elements that the vector can hold.
### Return value

The maximum length of the vector.
## size_t getMemoryUsage ( ) const

Shows the amount of memory used by the vector in bytes.
### Return value

Used memory in bytes.
## void insert ( size_t pos , Type * v )

Inserts an element into the vector at a specified position.
### Arguments

- *size_t* **pos** - Position.
- *Type ** **v** - Value to be inserted.

## void insert ( size_t pos , Type & v )

Inserts an element into the vector at a specified position.
### Arguments

- *size_t* **pos** - Item position.
- *Type &* **v** - Pointer to the value to be inserted.

## void insert ( size_t pos , const Type & v )

Inserts an element into the vector at a specified position.
### Arguments

- *size_t* **pos** - Item position.
- *const Type &* **v** - Value to set.

## bool isValidNum ( int num ) const

Returns a value indicating if the vector contains an item with this index.
### Arguments

- *int* **num** - Index to be checked.

### Return value

**true** if the vector contains an item with this index; otherwise, **false**.
## Type & last ( )

Returns the position of the last element beyond the range of elements to be copied.
### Return value

Position of the last element beyond the range of elements to be copied.
## const Type & last ( ) const

Returns the position of the last element beyond the range of elements to be copied.
### Return value

Position of the last element beyond the range of elements to be copied.
## void move ( size_t from , size_t to )

Moves an element in the vector from its position to a specified one, while shifting the items in between towards the initial position.
### Arguments

- *size_t* **from** - Initial position of the item to be moved.
- *size_t* **to** - Target position of the moved item.

## Vector < Type > & operator= ( const Vector < Type > & v )

Assignment operator for the vector.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Type > &* **v** - Vector.

## Type & operator[] ( size_t index )

Vector item access.
### Arguments

- *size_t* **index** - Item index.

### Return value

Vector item.
## const Type & operator[] ( size_t index ) const

Vector item access.
### Arguments

- *size_t* **index** - Item index.

### Return value

Vector item.
## void prepend ( Type & v )

Adds an item to the beginning of the vector.
### Arguments

- *Type &* **v** - Item to prepend.

## void prepend ( const Type & v )

Adds an item to the beginning of the vector.
### Arguments

- *const Type &* **v** - Item to prepend.

## void push_back ( Type & v )

Adds an item to the end of the vector.
### Arguments

- *Type &* **v** - Item to append.

## void push_back ( const Type & v )

Adds an item to the end of the vector.
### Arguments

- *const Type &* **v** - Item to append.

## void push_front ( Type & v )

Adds an item to the beginning of the vector.
### Arguments

- *Type &* **v** - Item to prepend.

## void push_front ( const Type & v )

Adds an item to the beginning of the vector.
### Arguments

- *const Type &* **v** - Item to prepend.

## Type & random ( )

Returns a pseudo-random element of the vector.
### Return value

Random element of the vector.
## const Type & random ( ) const

Returns a pseudo-random element of the vector.
### Return value

Random element of the vector.
## int randomIndex ( ) const

Returns a pseudo-random index of the vector.
### Return value

Random index.
## void remove ( )

Removes the last item.
## void remove ( size_t pos , size_t size )

Removes an item(s) at a given position.
### Arguments

- *size_t* **pos** - Position.
- *size_t* **size** - Number of items to remove.

## void remove ( const Iterator & it )

Removes an item indicated by a given iterator.
### Arguments

- *const Iterator &* **it** - Iterator.

## void removeAll ( const Type & v )

Removes all items having the specified value.
### Arguments

- *const Type &* **v** - Value to be removed.

## void removeAllFast ( const Type & v )

Removes all items having the specified value. The removed value is replaced by the value contained in the last element.
### Arguments

- *const Type &* **v** - Value to be removed.

## void removeFast ( size_t pos )

Removes an item at a given position. The removed value is replaced by the value contained in the last element.
### Arguments

- *size_t* **pos** - Position.

## void removeFast ( const Iterator & it )

Removes an item indicated by a given iterator. The removed value is replaced by the value contained in the last element.
### Arguments

- *const Iterator &* **it** - Iterator.

## void removeFirst ( )

Removes the first item in the vector.
## void removeLast ( )

Removes the last item in the vector.
## void removeOne ( const Type & v )

Removes the first encountered item having the specified value.
### Arguments

- *const Type &* **v** - Value to be removed.

## void removeOneFast ( const Type & v )

Removes the first encountered item having the specified value. The removed value is replaced by the value contained in the last element.
### Arguments

- *const Type &* **v** - Value to be removed.

## void replace ( const Type & old_value , const Type & new_value )

Replaces the specified value with the new one in all relevant vector elements.
### Arguments

- *const Type &* **old_value** - Value to be replaced.
- *const Type &* **new_value** - Value to replace the old one.

## void replaceOne ( const Type & old_value , const Type & new_value )

Replaces the specified value with the new one in the first encountered vector element.
### Arguments

- *const Type &* **old_value** - Value to be replaced.
- *const Type &* **new_value** - Value to replace the old one.

## void reserve ( size_t size )

Reserves memory at least enough to contain the specified number of items.
### Arguments

- *size_t* **size** - Minimum vector size. > **Notice:** If the specified value is greater than the current vector capacity, the method causes the container to reallocate its storage increasing capacity to the specified value (or greater). In all other cases the capacity is not affected.

## void resize ( size_t size )

Resizes a vector.
### Arguments

- *size_t* **size** - New vector size.

## int rightIndex ( const T & t ) const

Returns the index of the right neighbor of a given item.
### Arguments

- *const T &* **t** - Item.

### Return value

Right neighbor index.
## void shrink ( )

Discards excess capacity.
## int size ( ) const

Returns the size of the vector.
### Return value

Vector size.
## int space ( ) const

Returns the capacity of the vector. The value may be greater than the size.
### Return value

Vector capacity.
## swap ( Vector& v )

Swaps this vector with the specified vector.
### Arguments

- *Vector&* **v** - Vector.

## swap ( int num_0 , int num_1 )

Swaps the values at the specified positions in the vector.
### Arguments

- *int* **num_0** - Position of the item.
- *int* **num_1** - Position of the item.

## Type takeAt ( int index )

Returns the vector item taken at the specified index and removes it from the vector.
### Arguments

- *int* **index** - Index of the value.

### Return value

Vector item.
## Type takeAtFast ( int index )

Returns the vector item taken at the specified index and removes it from the vector. The removed value is replaced by the value contained in the last element.
### Arguments

- *int* **index** - Index of the value.

### Return value

Vector item.
## Type takeFirst ( )

Returns the first item of the vector and removes it from the vector.
### Return value

The first vector item.
## Type takeLast ( )

Returns the last item of the vector and removes it from the vector.
### Return value

The last vector item.
## Type value ( int index )

Returns the vector item taken at the specified index. This is a safe method that returns a default-constructed value, if the index is outside the vector range.
### Arguments

- *int* **index** - Index of the value.

### Return value

Vector item.
## Type value ( int index , const Type & def )

Returns the vector item taken at the specified index.
### Arguments

- *int* **index** - Index of the value.
- *const Type &* **def** - The reference to be returned if the index is outside the vector limits.

### Return value

Vector item.
## const Type & valueRef ( int index , const Type & def )

Returns the reference to the vector item taken at the specified index.
### Arguments

- *int* **index** - Index of the value.
- *const Type &* **def** - The reference to be returned if the index is outside the vector limits.

### Return value

Reference to the vector item.
