# Unigine::Tree Class (CPP)

**Header:** #include <UnigineTree.h>


A tree container template.


## Tree Class

### Members

---

## Iterator back ( )

Returns the back iterator.
### Return value

Back iterator.
## ConstIterator back ( ) const

Returns the back const iterator.
### Return value

Back const iterator.
## Iterator begin ( )

Returns the begin iterator.
### Return value

Begin iterator.
## ConstIterator begin ( ) const

Returns the begin const iterator.
### Return value

Begin const iterator.
## void clear ( )

Clears a tree.
## int empty ( ) const

1 if the tree is empty; otherwise, 0.
### Return value

The empty flag.
## Iterator end ( )

Returns the end iterator.
### Return value

End iterator.
## ConstIterator end ( ) const

Returns the end const iterator.
### Return value

End const iterator.
## Iterator find ( const T & key )

Finds an item in the tree.
### Arguments

- *const T &* **key** - Key.

### Return value

The iterator.
## ConstIterator find ( const T & key ) const

Finds an item in the tree.
### Arguments

- *const T &* **key** - Key.

### Return value

The const iterator.
## Tree < Key, Data > & operator= ( const Tree < Key, Data > & tree )

Assignment operator for the tree.
### Arguments

- *const [Tree](../../../../api/library/containers/tree/class.tree_cpp.md)< Key, Data > &* **tree** - Tree.

## void remove ( const Key & key )

Removes an item from the tree.
### Arguments

- *const Key &* **key** - Key.

## int size ( ) const

Returns the size of the tree.
### Return value

The size of the tree.
## Tree ( )

Default constructor that produces an empty tree.
## Tree ( const Tree < Key, Data > & tree )

Copy constructor.
### Arguments

- *const [Tree](../../../../api/library/containers/tree/class.tree_cpp.md)< Key, Data > &* **tree** - tree.

## ~Tree ( )

Destructor.
