# Unigine::Tree::ConstIterator Class (CPP)

**Header:** #include <UnigineTree.h>


## Tree::ConstIterator Class

### Members

---

## const Node * get ( ) const

Returns iterator's node pointer.
### Return value

The const iterator's node pointer.
## ConstIterator ( )

Default constructor.
## ConstIterator ( const ConstIterator & it )

Copy constructor.
### Arguments

- *const ConstIterator &* **it** - ConstIterator.

## int operator!= ( const typename Tree < Key, Data >::Iterator & it ) const

Check if two iterators are not the same.
### Arguments

- *const typename [Tree](../../../../api/library/containers/tree/class.tree_cpp.md)< Key, Data >::Iterator &* **it** - The second iterator.

### Return value

1 if iterators are not the same; otherwise, 0.
## int operator!= ( const ConstIterator & it ) const

Check if two iterators are not the same.
### Arguments

- *const ConstIterator &* **it** - The second iterator.

### Return value

1 if iterators are not the same; otherwise, 0.
## const Node & operator* ( ) const

Returns iterator's node reference.
### Return value

The const iterator's node reference.
## ConstIterator & operator++ ( )

Increases the iterator position.
### Return value

The const iterator referring to the next element.
## ConstIterator operator++ ( )

Increases the iterator position.
### Return value

The const iterator referring to the next element.
## ConstIterator & operator-- ( )

Decreases the iterator position.
### Return value

The const iterator referring to the prev element.
## ConstIterator operator-- ( )

Decreases the iterator position.
### Return value

The const iterator referring to the prev element.
## const Node * operator-> ( ) const

Returns iterator's node pointer.
### Return value

The const iterator's node pointer.
## ConstIterator & operator= ( const ConstIterator & it )

Assignment operator for the iterator.
### Arguments

- *const ConstIterator &* **it** - ConstIterator.

## int operator== ( const typename Tree < Key, Data >::Iterator & it ) const

Check if two iterators are actually the same.
### Arguments

- *const typename [Tree](../../../../api/library/containers/tree/class.tree_cpp.md)< Key, Data >::Iterator &* **it** - The second iterator.

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
