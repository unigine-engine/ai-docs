# Unigine::HashMap Class (CPP)

**Header:** #include <UnigineHashMap.h>


A hash map container template. The hash map stores items represented by key-value pairs in an *unspecified* order. Data are stored in the memory linearly, i.e. as a vector:


![](hashmap_data_storage.png)


> **Notice:** Key and Value address may change throughout the hashmap existense. This way of storing hash map data is more performance-friendly, but if you need the hashmap address to remain unchanged, use *[BucketHashMap](../../../api/library/containers/class.buckethashmap_cpp.md)* class.


Hash map can be used, for example, for searching among nodes by their names.


To create a new hash map, you can use the [default constructor](#HashMap) or one of the following ways:


- Create a hash map using an initializer list: ```cpp // create a hash map using an initializer list const HashMap<String, int> hashMap_0{ { "a", 1 },	{ "b", 2 },	{ "c", 3 },	}; // check the result for (const auto &k : hashMap_0) Log::message("%s : %d \n", k.key.get(), k.data); ``` The hash map that stores values of a custom type can be created as follows: ```cpp // declare an enumeration enum class MyEnum { One, Two, Three, }; // create a hash map using an initializer list const HashMap<String, MyEnum> hashMap_1 { { "One", MyEnum::One }, { "Two", MyEnum::Two }, { "Three", MyEnum::Three }, }; // check the result for (const auto &k : hashMap_1) Log::message("%s : %d \n", k.key.get(), k.data); ```
- Create a hash set using a copy constructor: ```cpp // create a hash map using an initializer list const HashMap<String, int> initial{ { "a", 1 },{ "b", 2 },{ "c", 3 },{ "d", 4 }, }; // copy constructor HashMap<String, int> copied(initial); //check the result for (const auto &k : copied) Log::message("%s : %d \n", k.key.get(), k.data); ```


You can change the created hash map by using the class member functions described in the article. Check some of the usage examples:


- To add items to the current hash map, you can use one of the *[append()](#append_const_HashMap_ref_void)* or *[insert()](#insert_const_HashMap_ref_void)* functions: ```cpp // create hash maps using initializer lists HashMap<String, int> initial{ { "a", 1 }, { "b", 2 }, { "c", 3 }, }; const HashMap<String, int> to_append{ { "m", 7 }, { "n", 8 }, { "o", 9 }, }; // append items of one hash map to another initial.append(to_append); // insert an item into the "initial" hash map initial.insert("s", 10); // check the result for (const auto &k : initial) Log::message("%s : %d \n", k.key.get(), k.data); ```
- Get a value by the key from the hash map and insert an item if there is no such key: ```cpp // creare an empty hash map HashMap<int, int> hashMap{ { 1, 10 } }; // try to get values by the specified keys Log::message("Value %d\n", hashMap[1]); // if there is no such key, it will be added to the hash map with the default value Log::message("Value %d\n", hashMap[2]); // check the result - the new item with the default value is added to the hash map for (const auto &k: hashMap) Log::message("%d : %d \n", k.key, k.data); ```
- Take an item from the hash map: ```cpp // create a hash map HashMap<int, int> hashMap { {1, 1}, {2, 2}, {3, 3}, }; // declare a key and a value const int key = 0; const int value = 4; // append a new item to the hash map hashMap.append(key,value); // get an item iterator by its key auto it = hashMap.find(key); // take the item from the hash map int c = hashMap.take(it); // check the result - the taken item is removed from the hash map for (const auto &k : hashMap) Log::message("%d : %d \n", k.key, k.data); ```
- Remove an item from the hash map: ```cpp // create a hash map HashMap<int, int> hashMap{ { 1, 1 },{ 2, 2 },{ 3, 3 }, }; // get an item iterator by its key auto it = hashMap.find(2); // remove the item from the hash map hashMap.remove(it); // check the result for (const auto &k: hashMap) Log::message("%d : %d \n", k.key, k.data); ```
- Get items by the values from the hash map: ```cpp // create a hash map HashMap<String, int> hashMap{ { "a", 1 }, { "b", 2 }, { "c", 3 }, }; // get an item iterator by its value auto it = hashMap.findData(2); // check the result Log::message("%s \n", it->key.get()); ```
- Get a value/values from the hash map: ```cpp // create a hash map HashMap<String, int> hashMap{ { "a", 1 },{ "b", 2 },{ "c", 3 }, }; // get a key by its value Log::message("%d \n", hashMap.value("a")); // get a vector of all values of the hash map Vector<int> ret = hashMap.values(); for (int i = 0; i < ret.size(); i++) Log::message("%d \n",ret[i]); ```


## HashMap Class

### Members

---

## HashMap ( )

Default constructor that produces an empty hash map.
## HashMap ( std::initializer_list< Pair <Key,Value>> list )

Constructor. Creates a hash map from given key-value pairs.
### Arguments

- *std::initializer_list<[Pair](../../../api/library/containers/class.pair_cpp.md)<Key,Value>>* **list** - List of pairs.

## HashMap ( const HashMap& o )

Constructor. Creates a hash map by copying a source hash map.
### Arguments

- *const HashMap&* **o** - Hash map.

## HashMap ( HashMap&& o )

Constructor. Creates a hash map by moving a source hash map into it.
### Arguments

- *HashMap&&* **o** - Hash map.

## Iterator append ( const Key& key , const Value& value )

Appends an item with a given key and value to the hash map.
### Arguments

- *const Key&* **key** - Key.
- *const Value&* **value** - Value.

### Return value

Item iterator.
## Iterator append ( const Key& key , Value&& value )

Appends an item with a given key and value to the hash map.
### Arguments

- *const Key&* **key** - Key to be copied to the hash map.
- *Value&&* **value** - Value to be moved to the hash map.

### Return value

Item iterator.
## Iterator append ( Key&& key , const Value& value )

Appends an item with a given key and value to the hash map.
### Arguments

- *Key&&* **key** - Key to be moved to the hash map.
- *const Value&* **value** - Value to be copied to the hash map.

### Return value

Item iterator.
## Iterator append ( Key&& key , Value&& value )

Appends an item with a given key and value to the hash map.
### Arguments

- *Key&&* **key** - Key to be moved to the hash map.
- *Value&&* **value** - Value to be moved to the hash map.

### Return value

Item iterator.
## Value& append ( const Key& key )

Appends an item with a given key to the hash map.
### Arguments

- *const Key&* **key** - Key.

### Return value

Value.
## Value& append ( Key&& key )

Appends an item with a given key to the hash map.
### Arguments

- *Key&&* **key** - Key to be moved to the hash map.

### Return value

Value.
## void append ( const HashMap& o )

Appends items with all available keys from the argument hash to the hash map.
### Arguments

- *const HashMap&* **o** - Hash map to be appended.

## void append ( HashMap&& o )

Appends items with all available keys by moving the argument hash to the hash map.
### Arguments

- *HashMap&&* **o** - Hash map to be appended.

## void append ( const Vector& vector )

Appends items with all available keys from the argument vector to the hash map.
### Arguments

- *const Vector&* **vector** - Vector containing the key (or keys) to be appended.

## void append ( Vector&& vector )

Appends items with all available keys by moving the argument vector to the hash map.
### Arguments

- *Vector&&* **vector** - Vector containing the key (or keys) to be appended.

## Iterator insert ( const Key& key , const Value& value )

Inserts an item with a given key and value into the hash map.
### Arguments

- *const Key&* **key** - Key.
- *const Value&* **value** - Value.

### Return value

Item iterator.
## Iterator insert ( const Key& key , Value&& value )

Inserts an item with a given key and value into the hash map.
### Arguments

- *const Key&* **key** - Key to be copied to the hash map.
- *Value&&* **value** - Value to be moved to the hash map.

### Return value

Item iterator.
## Iterator insert ( Key&& key , const Value& value )

Inserts an item with a given key and value into the hash map.
### Arguments

- *Key&&* **key** - Key to be moved to the hash map.
- *const Value&* **value** - Value to be copied to the hash map.

### Return value

Item iterator.
## Iterator insert ( Key&& key , Value&& value )

Inserts an item with a given key and value into the hash map.
### Arguments

- *Key&&* **key** - Key to be moved to the hash map.
- *Value&&* **value** - Value to be moved to the hash map.

### Return value

Item iterator.
## Value& insert ( const Key& key )

Inserts an item with a given key into the hash map.
### Arguments

- *const Key&* **key** - Key to be copied to the hash map.

### Return value

Value.
## Value& insert ( Key&& key )

Inserts an item with a given key into the hash map.
### Arguments

- *Key&&* **key** - Key to be moved to the hash map.

### Return value

Value.
## void insert ( const HashMap& o )

Inserts items with all available keys by copying the argument hash to the hash map.
### Arguments

- *const HashMap&* **o** - Hash map containing the key (or keys) to be inserted.

## void insert ( HashMap&& o )

Inserts items with all available keys by moving the argument hash to the hash map.
### Arguments

- *HashMap&&* **o** - Hash map containing the key (or keys) to be inserted.

## void insert ( const Vector& vector )

Inserts items with all available keys by copying the argument vector to the hash map.
### Arguments

- *const Vector&* **vector** - Vector containing the key (or keys) to be inserted.

## void insert ( Vector&& vector )

Inserts items with all available keys by moving the argument vector to the hash map.
### Arguments

- *Vector&&* **vector** - Vector containing the key (or keys) to be inserted.

## Value take ( const Key& key , const Value& def )

Removes an item from the hash map by its key and returns an item value. If there is no such item, the value set as default is returned.
### Arguments

- *const Key&* **key** - Key.
- *const Value&* **def**

### Return value

Removed item value.
## Value take ( const Key& key )

Removes an item from the hash map by its key and returns an item value. If there is no such item, a default-constructed value is returned.
### Arguments

- *const Key&* **key** - Key.

### Return value

Removed item value.
## Value take ( Iterator it )

Removes an item from the hash map by its iterator and returns an item value. If there is no such item, a default-constructed value is returned.
### Arguments

- *Iterator* **it** - Item iterator.

### Return value

Removed item value.
## Value take ( ConstIterator it )

Removes an item from the hash map by its iterator and returns an item value. If there is no such item, a default-constructed value is returned.
### Arguments

- *ConstIterator* **it** - Item iterator.

### Return value

Removed item value.
## bool contains ( const Key& key , const Value& value ) const

Checks if an item with a specified key and value exists in the hash map.
### Arguments

- *const Key&* **key** - Key.
- *const Value&* **value** - Value.

### Return value

**true** if an item exists; otherwise, **false**.
## Iterator findData ( const Value& value )

Searches for an item with a specified value in the hash map.
### Arguments

- *const Value&* **value** - Value.

### Return value

Item iterator.
## ConstIterator findData ( const Value& value ) const

Searches for an item with a specified value in the hash map.
### Arguments

- *const Value&* **value** - Value.

### Return value

Item iterator.
## void removeData ( const Value& value )

Removes the first occurrence of the specified value from the hash map.
### Arguments

- *const Value&* **value** - Value.

## Value& get ( Key&& key )

Returns a value by a specified key.
### Arguments

- *Key&&* **key** - Key.

### Return value

Value.
## const Value& get ( const Key& key ) const

Returns a value by a specified key.
### Arguments

- *const Key&* **key** - Key.

### Return value

Value.
## const Value& get ( const Key& key , const Value& value ) const

Returns a value by a specified key. If there is no item with the key, the default value is returned.
### Arguments

- *const Key&* **key** - Key.
- *const Value&* **value** - Default value.

### Return value

Value.
## Value& operator[] ( Key&& key )

Hash map item access. The value is returned if it is available by the key; if the item is unavailable, a new (Key,Value) pair is added.
### Arguments

- *Key&&* **key** - Key.

### Return value

Accessed item value, if available.
## Value& operator[] ( const Key& key ) const

Hash map item access.
### Arguments

- *const Key&* **key** - Key.

### Return value

Accessed item value.
## Value value ( const Key& key ) const

Returns a value with a specified key from the hash map. If there is no such key, returns a default-constructed value.
### Arguments

- *const Key&* **key** - Key.

### Return value

Accessed item value.
## Value value ( const Key& key , const Value& value ) const

Returns a value with a specified key from the hash map. If there is no such key, returns the specified default value.
### Arguments

- *const Key&* **key** - Key.
- *const Value&* **value** - Default value.

### Return value

Accessed item value.
## const Value& valueRef ( const Key& key ) const

Returns a reference to the value with a specified key from the hash map. If there is no such key, returns a default-constructed valuee.
### Arguments

- *const Key&* **key** - Key.

### Return value

Accessed item value.
## const Value& valueRef ( const Key& key , const Value& value ) const

Returns a reference to the value with a specified key from the hash map. If there is no such key, returns a default value.
### Arguments

- *const Key&* **key**
- *const Value&* **value** - Default value.

### Return value

Accessed item value.
## Vector <Value> values ( ) const

Returns a vector of all values of the hash map.
### Return value

Vector of hash map values.
## void getValues ( Vector <Value>& values ) const

Appends hash map values to a given vector.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<Value>&* **values** - Vector of hash map values.

## HashMap & operator= ( const HashMap & o )

Assigns the specified hash map by copying it.
### Arguments

- *const [HashMap](../../../api/library/containers/class.hashmap_cpp.md) &* **o** - Hash map.

### Return value

Hash map.
## HashMap & operator= ( HashMap&& o )

Assigns the specified hash map by moving it.
### Arguments

- *HashMap&&* **o** - Hash map.

### Return value

Hash map.
## emplaceRange ( InputIt first , InputIt last )

Inserts the range of values specified by the argument iterators into the hash map.
### Arguments

- *InputIt* **first** - Iterator that identifies the beginning of the range.
- *InputIt* **last** - Iterator that identifies the end of the range.

## bool contains ( const Key & k ) const

Checks if the given key is present in the hash map.
### Arguments

- *const Key &* **k** - Key to be checked.

### Return value

**true** if the hash map contains the specified key; otherwise, **false**.
## Iterator find ( const Key & k ) const

Returns the iterator of the specified key.
### Arguments

- *const Key &* **k** - Key to be checked.

### Return value

Item iterator.
## ConstIterator find ( const Key & k ) const

Returns the iterator of the specified key.
### Arguments

- *const Key &* **k** - Key to be checked.

### Return value

Item iterator.
## Item * findFast ( const Key & key ) const

Finds an element with a specified key.
### Arguments

- *const Key &* **key** - Key to look for.

### Return value

Pointer to the hash map item.
## Vector <Key> keys ( ) const

Returns a vector containing all keys in the hash map.
### Return value

Vector of keys.
## void getKeys ( Vector <Key>& keys ) const

Adds keys of the hash to the specified vector.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<Key>&* **keys** - Vector to store the keys.

## const Key & getKey ( size_t index ) const

Returns the key by its index.
### Arguments

- *size_t* **index** - Index number of the key in the hash map.

### Return value

Key.
## bool remove ( const Key& k )

Removes the specified key from the hash map.
### Arguments

- *const Key&* **k** - Key to be removed.

### Return value

**true** if the key is removed successfully; otherwise, **false**.
## void remove ( Iterator it )

Removes an element currently pointed to by the iterator from the hash map.
### Arguments

- *Iterator* **it** - Iterator pointing to an element to be removed.

## void remove ( ConstIterator it )

Removes an element currently pointed to by the iterator from the hash map.
### Arguments

- *ConstIterator* **it** - Iterator pointing to an element to be removed.

## void remove ( const HashMap& o )

Removes the specified hash map from the current hash map.
### Arguments

- *const HashMap&* **o** - Hash map.

## void remove ( const Vector <Key>& v )

Removes the specified keys from the hash map.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<Key>&* **v** - Vector storing the keys.

## bool erase ( const ConstIterator & it )

Removes an element currently pointed to by the iterator from the hash map.
### Arguments

- *const ConstIterator &* **it** - Iterator pointing to the element to be removed.

### Return value

true on success, otherwise false.
## bool erase ( const Iterator & it )

Removes an element currently pointed to by the iterator from the hash map.
### Arguments

- *const Iterator &* **it** - Iterator pointing to the element to be removed.

### Return value

true on success, otherwise false.
## bool erase ( const Key& k )

Removes an element having the specified key from the hash map.
### Arguments

- *const Key&* **k** - Key of the element to be removed.

### Return value

true on success, otherwise false.
## void erase ( const HashMap& o )

Removes the specified hash map from the current hash map.
### Arguments

- *const HashMap&* **o** - Hash map to be removed.

## void erase ( const Vector <Key>& v )

Removes the specified keys from the hash map.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<Key>&* **v** - Vector storing the keys.

## void subtract ( const Vector <Key>& vector )

Removes the specified keys from the hash map.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<Key>&* **vector** - Vector storing the keys.

## void subtract ( const HashMap & o )

Removes the specified hash map from the current hash map.
### Arguments

- *const [HashMap](../../../api/library/containers/class.hashmap_cpp.md) &* **o** - Hash map to be removed.

## void clear ( )

Removes all key-value pairs from the hash map.
## void destroy ( )

Removes all key-value pairs from the hash map and releases the memory.
## void reserve ( size_t size )

Reserves storage to avoid repeated reallocation.
### Arguments

- *size_t* **size** - Hash size to be reserved.

## void shrink ( )

Removes unused capacity.
## Iterator begin ( ) const

Returns an iterator that points to the first element in the hash map.
### Return value

Iterator pointing to the first element.
## Iterator end ( ) const

Returns an iterator that points to the location succeeding the last element in the hash map.
### Return value

Iterator pointing to the last element.
## ConstIterator cbegin ( ) const

Returns a const iterator that points to the first element in the hash map.
### Return value

ConstIterator pointing to the first element.
## ConstIterator cend ( ) const

Returns a const iterator that points to the location succeeding the last element in the hash map.
### Return value

ConstIterator pointing to the last element.
## Counter size ( ) const

Returns the number of key-value pairs in the hash map.
### Return value

Number of key-value pairs in the hash map.
## Counter space ( ) const

Returns the current capacity (number of elements the hash can currently contain).
### Return value

Number of elements the hash can currently contain.
## size_t getMemoryUsage ( ) const

Shows the amount of memory used by the hash map in bytes.
### Return value

Used memory in bytes.
## bool empty ( ) const

Checks if the hash map is empty.
### Return value

**true** if the hash map is empty, otherwise **false**
## void swap ( HashMap & o )

Swaps this hash map with the hash map specified as the argument.
### Arguments

- *[HashMap](../../../api/library/containers/class.hashmap_cpp.md) &* **o** - Hash map.
