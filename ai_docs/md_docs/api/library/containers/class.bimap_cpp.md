# Unigine::BiMap Class (CPP)

**Header:** #include <UnigineBiMap.h>


A bidirectional map container template that contains the *key-value* pairs of one-to-one correspondence. The bimap allows fast bidirectional lookup between keys and values.


## BiMap Class

### Members

---

## BiMap ( )

Default constructor that produces an empty bimap.
## BiMap ( std::initializer_list< Pair <Key,Type>> list )

Constructor. Creates a bimap from the given key-value pairs.
### Arguments

- *std::initializer_list<[Pair](../../../api/library/containers/class.pair_cpp.md)<Key,Type>>* **list** - List of pairs.

## BiMap ( const BiMap& o )

Constructor. Creates a bimap by copying a source bimap.
### Arguments

- *const BiMap&* **o** - Bimap.

## BiMap ( BiMap&& o )

Constructor. Creates a bimap by copying a source bimap.
### Arguments

- *BiMap&&* **o** - Bimap.

## BiMap <Key, Type, Allocator> & operator= ( const BiMap& o )

Assignment operator for the bimap.
### Arguments

- *const BiMap&* **o** - Bimap.

## BiMap <Key, Type, Allocator> & operator= ( BiMap&& o )

Assignment operator for the bimap.
### Arguments

- *BiMap&&* **o** - Bimap.

## void swap ( BiMap& o )

Swaps contents of the current bimap and the given one.
### Arguments

- *BiMap&* **o** - Bimap.

## void clear ( )

Deletes all contents of the bimap.
## size_t getMemoryUsage ( ) const

Shows the amount of memory used by the bimap in bytes.
### Return value

Used memory in bytes.
## Iterator insert ( const Key& key , const Type& value )

Inserts an item with a given key and value into the bimap. If the item with the given key already exists and its value differs from the given one, the value is replaced.
### Arguments

- *const Key&* **key** - Key.
- *const Type&* **value** - Value.

### Return value

Item iterator. If the item with the given key and value already exists in the bimap, its iterator will be returned.
## Iterator insert ( Key&& key , const Type& value )

Inserts an item with a given key and value into the bimap. If the item with the given key already exists and its value differs from the given one, the value is replaced.
### Arguments

- *Key&&* **key** - Key.
- *const Type&* **value** - Value.

### Return value

Item iterator. If the item with the given key and value already exists in the bimap, its iterator will be returned.
## Iterator insert ( const Key& key , Type&& value )

Inserts an item with a given key and value into the bimap. If the item with the given key already exists and its value differs from the given one, the value is replaced.
### Arguments

- *const Key&* **key** - Key.
- *Type&&* **value** - Value.

### Return value

Item iterator. If the item with the given key and value already exists in the bimap, its iterator will be returned.
## Iterator insert ( Key&& key , Type&& value )

Inserts an item with a given key and value into the bimap. If the item with the given key already exists and its value differs from the given one, the value is replaced.
### Arguments

- *Key&&* **key** - Key.
- *Type&&* **value** - Value.

### Return value

Item iterator. If the item with the given key and value already exists in the bimap, its iterator will be returned.
## void insert ( const BiMap& m )

Inserts a given bimap into the current one. If the item with the given key already exists in the current bimap and its value differs from the given one, the value is replaced.
### Arguments

- *const BiMap&* **m** - Bimap.

## void insert ( BiMap&& m )

Inserts a given bimap into the current one. If the item with the given key already exists in the current bimap and its value differs from the given one, the value is replaced.
### Arguments

- *BiMap&&* **m** - Bimap.

## Iterator append ( const Key& key , const Type& value )

Appends an item with a given key and value to the bimap. If the item with the given key already exists and its value differs from the given one, the value is replaced.
### Arguments

- *const Key&* **key** - Key.
- *const Type&* **value** - Value.

### Return value

Added item iterator. If the item with the given key and value already exists in the bimap, its iterator will be returned.
## Iterator append ( Key&& key , const Type& value )

Appends an item with a given key and value to the bimap. If the item with the given key already exists and its value differs from the given one, the value is replaced.
### Arguments

- *Key&&* **key** - Key.
- *const Type&* **value** - Value.

### Return value

Added item iterator. If the item with the given key and value already exists in the bimap, its iterator will be returned.
## Iterator append ( const Key& key , Type&& value )

Appends an item with a given key and value to the bimap. If the item with the given key already exists and its value differs from the given one, the value is replaced.
### Arguments

- *const Key&* **key** - Key.
- *Type&&* **value** - Value.

### Return value

Added item iterator. If the item with the given key and value already exists in the bimap, its iterator will be returned.
## Iterator append ( Key&& key , Type&& value )

Appends an item with a given key and value to the bimap. If the item with the given key already exists and its value differs from the given one, the value is replaced.
### Arguments

- *Key&&* **key** - Key.
- *Type&&* **value** - Value.

### Return value

Added item iterator. If the item with the given key and value already exists in the bimap, its iterator will be returned.
## void append ( const BiMap& m )

Appends a given bimap to the current one. If the item with the given key already exists in the current bimap and its value differs from the given one, the value is replaced.
### Arguments

- *const BiMap&* **m** - Bimap.

## void append ( BiMap&& m )

Appends a given bimap to the current one. If the item with the given key already exists in the current bimap and its value differs from the given one, the value is replaced.
### Arguments

- *BiMap&&* **m** - Bimap.

## const Type & emplace ( const Key& key , Args&& args )

Inserts an item with a specified key into the bimap. The new item value is constructed in-place with the given arguments avoiding unnecessary copying. If the item with the given key already exists and its value differs from the constructed one, the value is replaced.
### Arguments

- *const Key&* **key** - Key.
- *Args&&* **args** - Arguments for an item value constructor.

### Return value

Inserted item value. If the item already exists in the bimap, its iterator will be returned.
## const Type & emplace ( Key&& key , Args&& args )

Inserts an item with a specified key into the bimap. The new item value is constructed in-place with the given arguments avoiding unnecessary copying. If the item with the given key already exists and its value differs from the constructed one, the value is replaced.
### Arguments

- *Key&&* **key** - Key.
- *Args&&* **args** - Arguments for an item value constructor.

### Return value

Inserted item value. If the item already exists in the bimap, its iterator will be returned.
## Iterator appendFast ( const Key& key , const Type& value )

Appends an item with a given key and value to the bimap.
### Arguments

- *const Key&* **key** - Key.
- *const Type&* **value** - Value.

### Return value

Added item iterator.
## Iterator appendFast ( Key&& key , const Type& value )

Appends an item with a given key and value to the bimap.
### Arguments

- *Key&&* **key** - Key.
- *const Type&* **value** - Value.

### Return value

Added item iterator.
## Iterator appendFast ( const Key& key , Type&& value )

Appends an item with a given key and value to the bimap.
### Arguments

- *const Key&* **key** - Key.
- *Type&&* **value** - Value.

### Return value

Added item iterator.
## Iterator appendFast ( Key&& key , Type&& value )

Appends an item with a given key and value to the bimap.
### Arguments

- *Key&&* **key** - Key.
- *Type&&* **value** - Value.

### Return value

Added item iterator.
## void appendFast ( const BiMap& m )

Appends a given bimap to the current one.
### Arguments

- *const BiMap&* **m** - Bimap.

## void appendFast ( BiMap&& m )

Appends a given bimap to the current one.
### Arguments

- *BiMap&&* **m** - Bimap.

## const Type & emplaceFast ( const Key& key , Args&& args )

Inserts an item with a specified key into the bimap. The new item value is constructed in-place with the given arguments avoiding unnecessary copying.
### Arguments

- *const Key&* **key** - Key.
- *Args&&* **args** - Arguments for an item value constructor.

### Return value

Inserted item value.
## const Type & emplaceFast ( Key&& key , Args&& args )

Inserts an item with a specified key into the bimap. The new item value is constructed in-place with the given arguments avoiding unnecessary copying.
### Arguments

- *Key&&* **key** - Key.
- *Args&&* **args** - Arguments for an item value constructor.

### Return value

Inserted item value.
## bool contains ( const T& key ) const

Checks if an item with a given key exists in the bimap.
### Arguments

- *const T&* **key** - Key.

### Return value

Returns **1** if the item exists; otherwise, **0** is returned.
## bool contains ( const TypeKey& key , const Type& value ) const

Checks if an item with a given key and value exists in the bimap.
### Arguments

- *const TypeKey&* **key** - Key.
- *const Type&* **value** - Value.

### Return value

Returns **1** if the item exists; otherwise, **0** is returned.
## Iterator replace ( TypeKey&& key , TypeValue&& value )

Searches for an item with a given key in the bimap and replaces its value with a given one.
### Arguments

- *TypeKey&&* **key** - Key.
- *TypeValue&&* **value** - Value.

### Return value

Item iterator.
## Iterator replaceData ( TypeKey&& key , TypeValue&& value )

Searches for an item with a given value in the bimap and replaces its key with a given one.
### Arguments

- *TypeKey&&* **key** - Key.
- *TypeValue&&* **value** - Value.

### Return value

Item iterator.
## const Type & operator[] ( const Key& key ) const

Bimap item access.
### Arguments

- *const Key&* **key** - Key.

### Return value

Accessed item value.
## const Type & get ( const Key& key ) const

Returns a value by a given key.
### Arguments

- *const Key&* **key** - Key.

### Return value

Value.
## const Key & getKey ( const Type& value ) const

Returns a key by a given value.
### Arguments

- *const Type&* **value** - Value.

### Return value

Key.
## Iterator findData ( const T& v )

Searches for an item with a given value in the bimap.
### Arguments

- *const T&* **v** - Value.

### Return value

Item iterator.
## ConstIterator findData ( const T& v ) const

Searches for an item with a given value in the bimap.
### Arguments

- *const T&* **v** - Value.

### Return value

Item iterator.
## bool containsData ( const T& v ) const

Checks if an item with a specified value exists in the bimap.
### Arguments

- *const T&* **v** - Value.

### Return value

Returns 1 if the item exists; otherwise, 0 is returned.
## bool remove ( const Key& key )

Removes an item with a given key from the bimap.
### Arguments

- *const Key&* **key** - Key.

### Return value

Returns 1 if the item is removed successfully; otherwise, 0 is returned.
## bool remove ( const Iterator& it )

Removes a given item from the bimap.
### Arguments

- *const Iterator&* **it** - Item iterator.

### Return value

Returns 1 if the item is removed successfully; otherwise, 0 is returned.
## bool remove ( const ConstIterator& it )

Removes a given item from the bimap.
### Arguments

- *const ConstIterator&* **it** - Item iterator.

### Return value

Returns 1 if the item is removed successfully; otherwise, 0 is returned.
## bool erase ( const Key& key )

Removes an item by the given key from the bimap.
### Arguments

- *const Key&* **key** - Key.

### Return value

Returns 1 if the item is deleted successfully; otherwise, 0 is returned.
## Iterator erase ( const Iterator& it )

Removes a given item from the bimap.
### Arguments

- *const Iterator&* **it** - Item iterator.

### Return value

Iterator of the item following the removed one.
## ConstIterator erase ( const ConstIterator& it )

Removes a given item from the bimap.
### Arguments

- *const ConstIterator&* **it** - Item iterator.

### Return value

Iterator of the item following the removed one.
## bool removeData ( const Type& value )

Removes an item with a given value from the bimap.
### Arguments

- *const Type&* **value** - Value.

### Return value

Returns 1 if the item is removed successfully; otherwise, 0 is returned.
## Type take ( const Key& key )

Removes an item with a given key from the bimap and returns its value.
### Arguments

- *const Key&* **key** - Key.

### Return value

Removed item value.
## bool take ( const Key& key , Type& ret )

Removes an item with a given key from the bimap and writes the item value to the second argument.
### Arguments

- *const Key&* **key** - Key.
- *Type&* **ret** - Removed item value.

### Return value

Returns 1 if the item is removed successfully; otherwise, 0 is returned.
## Key takeData ( const Type& value )

Removes an item with a given value from the bimap and returns its key.
### Arguments

- *const Type&* **value** - Value.

### Return value

Removed item key.
## bool takeData ( const Type& value , Key& ret )

Removes an item with a given value from the bimap and writes the item key to the second argument.
### Arguments

- *const Type&* **value** - Value.
- *Key&* **ret** - Removed item key.

### Return value

Returns 1 if the item is removed successfully; otherwise, 0 is returned.
## Type value ( const Key& key ) const

Returns a value mapped to a given key in the bimap. If there is no such key, returns a default-constructed value.
### Arguments

- *const Key&* **key** - Key.

### Return value

Value.
## Type value ( const Key& key , const Type& def ) const

Returns a value mapped to a given key in the bimap. If there is no such key, returns a default value.
### Arguments

- *const Key&* **key** - Key.
- *const Type&* **def** - Default value.

### Return value

Value.
## const Type & valueRef ( const Key& key , const Type& def ) const

Returns a value mapped to a given key in the bimap. If there is no such key, returns a default value.
### Arguments

- *const Key&* **key** - Key.
- *const Type&* **def** - Default value.

### Return value

Value.
## Key key ( const Type& value ) const

Returns a key mapped to a given value in the bimap. If there is no such value, returns a default-constructed key.
### Arguments

- *const Type&* **value** - Value.

### Return value

Key.
## Key key ( const Type& value , const Key& def ) const

Returns a key mapped to a given value in the bimap. If there is no such value, returns a default key.
### Arguments

- *const Type&* **value** - Value.
- *const Key&* **def** - Default key.

### Return value

Key.
## const Key & keyRef ( const Type& value , const Key& def ) const

Returns a key mapped to a specified value in the bimap. If there is no such value, returns a default key.
### Arguments

- *const Type&* **value** - Value.
- *const Key&* **def** - Default key.

### Return value

Key.
## int values ( ) const

Returns a vector of all values of the bimap.
### Return value

Vector of bimap values.
## void getValues ( Vector <Type>& values ) const

Appends the bimap values to a given vector.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<Type>&* **values** - Vector of bimap values.

## void getPairs ( Vector < Pair <Key,Type >>& pairs ) const

Appends the bimap key-value pairs to a given vector.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Pair](../../../api/library/containers/class.pair_cpp.md)<Key,Type >>&* **pairs** - Vector of bimap key-value pairs.

## bool operator== ( const BiMap& o ) const

Checks if two bimaps are equal. The bimaps are considered equal if their key-value pairs are the same.
### Arguments

- *const BiMap&* **o** - Bimap.

### Return value

Returns **1** if bimaps are equal; otherwise, **0** is returned.
## bool operator!= ( const BiMap& o ) const

Checks if two bimaps are not equal. The bimaps are considered equal if their key-value pairs are the same.
### Arguments

- *const BiMap&* **o** - Bimap.

### Return value

Returns **1** if bimaps are not equal; otherwise, **0** is returned.
