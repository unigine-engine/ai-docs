# Unigine::Tree::Iterator Class (CPP)

**Header:** #include <UnigineTree.h>


## Tree::Iterator Class

### Members

---

## Node * get ( )

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

1 if iterators are not the same; otherwise 0.
## int operator!= ( const typename Tree < Key, Data >::ConstIterator & it ) const

Check if two iterators are not the same.
### Arguments

- *const typename [Tree](../../../../api/library/containers/tree/class.tree_cpp.md)< Key, Data >::ConstIterator &* **it** - The second iterator.

### Return value

1 if iterators are not the same; otherwise 0.
## Node & operator* ( )

Returns iterator's node reference.
### Return value

The iterator's node reference.
## Iterator & operator++ ( )

Increases the iterator position.
### Return value

The iterator referring to the next element.
## Iterator operator++ ( )

Increases the iterator position.
### Return value

The iterator referring to the current element.
## Iterator & operator-- ( )

Decreases the iterator position.
### Return value

The iterator referring to the prev element.
## Iterator operator-- ( )

Decreases the iterator position.
### Return value

The iterator referring to the current element.
## Node * operator-> ( )

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

1 if iterators are the same; otherwise 0.
## int operator== ( const typename Tree < Key, Data >::ConstIterator & it ) const

Check if two iterators are actually the same.
### Arguments

- *const typename [Tree](../../../../api/library/containers/tree/class.tree_cpp.md)< Key, Data >::ConstIterator &* **it** - The second iterator.

### Return value

1 if iterators are the same; otherwise 0.
## ~Iterator ( )

Destructor.
