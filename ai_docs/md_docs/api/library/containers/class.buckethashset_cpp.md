# Unigine::BucketHashSet Class (CPP)

**Header:** #include <UnigineHashSet.h>


A hash set container template. The hash set stores keys in an *unspecified* order. It allows for fast lookup of the keys. For example, you can implement fast searching among nodes by their IDs.


Data are stored in the following way:


![](buckethashset_data_storage.png)


> **Notice:** This approach to data storage may deem appropriate only in case you need the hash set address to remain unchanged. For a more performance-friendly way to store hash set data, use *[HashSet](../../../api/library/containers/class.hashset_cpp.md)* class.


To create a new hash set, you can use the [default constructor](#BucketHashSet) or one of the following ways:


- Create a hash set using an initializer list: ```cpp // constructor that takes an initializer list const BucketHashSet<int> hashSet{ 4,7,2 }; // check the result for (const auto &it : hashSet) Log::message("%d ", it.key); ```
- Create a hash set using a copy constructor: ```cpp // constructor that takes an initializer list const BucketHashSet<String> initial{ "a", "e" }; // copy constructor const BucketHashSet<String> copied(initial); // check the result for (const auto &it : copied) Log::message("%s ", it.key.get()); ```
- Create a new hash set by appending a vector of keys to it by using the *[fromKeys()](#fromKeys_Vector_ref_BucketHashSet)* function: ```cpp // create a vector of keys Vector<String> keys{ "1", "2", "3" }; // append keys to an empty hash set BucketHashSet<String> hashSet = BucketHashSet<String>::fromKeys(keys); // check the result for (const auto &it : hashSet) Log::message("%s ", it.key.get()); ```


You can change the created hash set by using the class member functions described in the article. Check some of the usage examples:


- To add keys to the current hash set, you can use one of the *[append()](#append_Key_rvref_void)* or *[insert()](#insert_Key_rvref_void)* functions: ```cpp // create hash sets using initializer lists BucketHashSet<String> initial{ "a", "b", "c", "d", "e" }; BucketHashSet<String> to_add{ "m", "n", "o" }; // append keys of the "to_add" hash set to the "initial" hash set initial.append(to_add); // insert a key into the "initial" hash set initial.insert("s"); // check the result for (const auto &it : initial) Log::message("%s ", it.key.get()); ``` Also it is possible to insert keys by using *[operator+=](#operator_addassign_const_Key_ref_BucketHashSet_ref)*: ```cpp // create hash sets using initializer lists BucketHashSet<String> initial{ "a", "e" }; const BucketHashSet<String> to_add{ "b", "c", "d" }; const BucketHashSet<String> expected{ "a", "b", "c", "d", "e" }; // add one hash set to another initial += to_add; // check the result if (initial == expected) Log::message("The hash set has been added successfully\n"); ``` > **Notice:** If the key already exists in the hash set, it won't be added. ```cpp // create a hash set BucketHashSet<String> set{ "s" }; // assign one hash set to another const BucketHashSet<String> original = set; // insert the hash set into the same hash set set.insert(set); // check the result - the hash set remains the same if (set == original) Log::message("Sets are equal\n"); ``` ```cpp // create an empty hash set BucketHashSet<String> set; // create two equal strings const char *initial_str = "aaa"; const String aaa0(initial_str), aaa1(initial_str); // add one of the strings as a key to the hash set set.insert(aaa0); // check the result if (set.contains(initial_str)) Log::message("The hash set contains the recently added key\n"); Log::message("The size is %d\n", set.size()); // add the duplicate string as a key to the hash set set.insert(aaa1); // check the result - the size of the hash set remains the same Log::message("The size is %d\n", set.size()); ```
- To remove keys from the hash set, you can use the *[subtract()](#subtract_const_BucketHashSet_ref_void)* or *[remove()](#remove_const_BucketHashSet_ref_void)* function: ```cpp // create hash sets BucketHashSet<String> initial{ "a", "b", "c", "d", "e" }; const BucketHashSet<String> to_subtract{ "a", "c", "e" }; const BucketHashSet<String> expected{ "b", "d" }; // remove keys of one hash set from another initial.subtract(to_subtract); // check if the hash sets are equal if (initial == expected)  Log::message("Sets are equal\n"); ``` ```cpp // create hash sets BucketHashSet<String> set{ "1", "2", "3", "4", "5" }; BucketHashSet<String> to_remove{ "3", "5" }; // remove keys of one hash set from another set.remove(to_remove); // check the result for (const auto &it : set) Log::message("%s ", it.key.get()); ``` Also the *[operator-=](#operator_subassign_const_Key_ref_BucketBucketHashSet_ref)* can be used: ```cpp // create hash sets BucketHashSet<String> initial{ "a", "b", "c", "d", "e" }; const BucketHashSet<String> to_subtract{ "a", "c", "e" }; const BucketHashSet<String> expected{ "b", "d" }; // remove keys of one hash set from another initial -= to_subtract; // check if the hash sets are equal if (initial == expected)  Log::message("Sets are equal\n"); ```
- To clear the hash set, use the *[clear()](#clear_void)* function: ```cpp // create a hash set BucketHashSet<String> set{ "1", "2", "3", "4", "5" }; // remove all keys from the hash set set.clear(); // check if the set is empty if (set.empty()) Log::message("The set is empty\n"); ```


## BucketHashSet Class

### Members

---

## BucketHashSet ( )

Default constructor that produces an empty hash set.
## BucketHashSet ( const BucketHashSet& o )

Constructor. Creates a hash set by copying a source hash set.
### Arguments

- *const BucketHashSet&* **o** - Hash set.

## BucketHashSet ( BucketHashSet&& o )

Constructor. Creates a hash set by moving a source hash set.
### Arguments

- *BucketHashSet&&* **o** - Hash set.

## BucketHashSet ( std::initializer_list<Key> list )

Constructor. Creates a hash set from given list of keys.
### Arguments

- *std::initializer_list<Key>* **list** - List of keys.

## void append ( const Key& key )

Appends a key to the hash set by copying the argument.
### Arguments

- *const Key&* **key** - Key.

## void append ( Key&& key )

Appends a key to the hash set by moving the argument.
### Arguments

- *Key&&* **key** - Key.

## void append ( const BucketHashSet& o )

Appends items with all available keys from the argument hash set to the current hash set.
### Arguments

- *const BucketHashSet&* **o** - Hash set to be appended.

## void append ( BucketHashSet&& o )

Appends items with all available keys by moving the argument hash set to the current hash set.
### Arguments

- *BucketHashSet&&* **o** - Hash set to be appended.

## void append ( const Vector& vector )

Appends items with all available keys from the argument vector to the current hash set.
### Arguments

- *const Vector&* **vector** - Vector containing the key (or keys) to be appended.

## void append ( Vector&& vector )

Appends items with all available keys by moving the argument vector to the current hash set.
### Arguments

- *Vector&&* **vector** - Vector containing the key (or keys) to be appended.

## void insert ( const Key& key )

Inserts a key into the hash set by copying the argument.
### Arguments

- *const Key&* **key** - Key.

## void insert ( Key&& key )

Inserts a key into the hash set by moving the argument.
### Arguments

- *Key&&* **key** - Key.

## BucketHashSet & operator+= ( const Key& k )

Appends a given key to this hash set and returns this hash set.
### Arguments

- *const Key&* **k** - Key.

### Return value

Updated hash set.
## BucketHashSet & operator+= ( const BucketHashSet& o )

Appends a given hash set to this hash set and returns this hash set.
### Arguments

- *const BucketHashSet&* **o**

### Return value

Updated hash set.
## BucketHashSet & operator-= ( const Key& k )

Removes a given key from this hash set and returns this hash set.
### Arguments

- *const Key&* **k** - Key.

### Return value

Updated hash set.
## BucketHashSet & operator-= ( const BucketHashSet& o )

Removes a given hash set from this hash set and returns this hash set.
### Arguments

- *const BucketHashSet&* **o**

### Return value

Updated hash set.
## static BucketHashSet fromKeys ( const Key* keys , size_t size )

Appends keys to the hash set and returns the updated set.
### Arguments

- *const Key** **keys** - Pointer to the keys.
- *size_t* **size** - Keys size.

### Return value

Updated hash set.
## static BucketHashSet fromKeys ( const Vector <Key>& keys )

Appends keys to the hash set and returns the updated set.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<Key>&* **keys** - Vector of keys.

### Return value

Updated hash set.
## static BucketHashSet fromKeys ( Vector <Key>& keys )

Appends keys to the hash set and returns the updated set.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<Key>&* **keys** - Vector of keys.

### Return value

Updated hash set.
## void insert ( const BucketHashSet& o )

Inserts items with all available keys by copying the argument hash to the current hash set.
### Arguments

- *const BucketHashSet&* **o** - Hash set containing the key (or keys) to be inserted.

## void insert ( HashSet&& o )

Inserts items with all available keys by moving the argument hash to the current hash set.
### Arguments

- *HashSet&&* **o** - Hash set containing the key (or keys) to be inserted.

## void insert ( const Vector& vector )

Inserts items with all available keys by copying the argument vector to the current hash set.
### Arguments

- *const Vector&* **vector** - Vector containing the key (or keys) to be inserted.

## void insert ( Vector&& vector )

Inserts items with all available keys by moving the argument vector to the current hash set.
### Arguments

- *Vector&&* **vector** - Vector containing the key (or keys) to be inserted.

## HashSet & operator= ( const BucketHashSet & o )

Assigns the specified hash set by copying it.
### Arguments

- *const [BucketHashSet](../../../api/library/containers/class.buckethashset_cpp.md) &* **o** - Hash set.

### Return value

Hash set.
## HashSet & operator= ( HashSet&& o )

Assigns the specified hash set by moving it.
### Arguments

- *HashSet&&* **o** - Hash set.

### Return value

Hash set.
## emplaceRange ( InputIt first , InputIt last )

Inserts the range of values specified by the argument iterators into the hash set.
### Arguments

- *InputIt* **first** - Iterator that identifies the beginning of the range.
- *InputIt* **last** - Iterator that identifies the end of the range.

## bool contains ( const Key & k ) const

Checks if the given key is present in the hash set.
### Arguments

- *const Key &* **k** - Key to be checked.

### Return value

**true** if the hash set contains the specified key; otherwise, **false**.
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

Pointer to the hash set item.
## Vector <Key> keys ( ) const

Returns a vector containing all keys in the hash set.
### Return value

Vector of keys.
## void getKeys ( Vector <Key>& keys ) const

Adds keys of the hash to the specified vector.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<Key>&* **keys** - Vector to store the keys.

## const Key & getKey ( size_t index ) const

Returns the key by its index.
### Arguments

- *size_t* **index** - Index number of the key in the hash set.

### Return value

Key.
## bool remove ( const Key& k )

Removes the specified key from the hash set.
### Arguments

- *const Key&* **k** - Key to be removed.

### Return value

**true** if the key is removed successfully; otherwise, **false**.
## void remove ( Iterator it )

Removes an element currently pointed to by the iterator from the hash set.
### Arguments

- *Iterator* **it** - Iterator pointing to an element to be removed.

## void remove ( ConstIterator it )

Removes an element currently pointed to by the iterator from the hash set.
### Arguments

- *ConstIterator* **it** - Iterator pointing to an element to be removed.

## void remove ( const BucketHashSet& o )

Removes the specified hash set from the current hash set.
### Arguments

- *const BucketHashSet&* **o** - Hash set.

## void remove ( const Vector <Key>& v )

Removes the specified keys from the hash set.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<Key>&* **v** - Vector storing the keys.

## bool erase ( const ConstIterator & it )

Removes an element currently pointed to by the iterator from the hash set.
### Arguments

- *const ConstIterator &* **it** - Iterator pointing to the element to be removed.

### Return value

true on success, otherwise false.
## bool erase ( const Iterator & it )

Removes an element currently pointed to by the iterator from the hash set.
### Arguments

- *const Iterator &* **it** - Iterator pointing to the element to be removed.

### Return value

true on success, otherwise false.
## bool erase ( const Key& k )

Removes an element having the specified key from the hash set.
### Arguments

- *const Key&* **k** - Key of the element to be removed.

### Return value

true on success, otherwise false.
## void erase ( const BucketHashSet& o )

Removes the specified hash set from the current hash set.
### Arguments

- *const BucketHashSet&* **o** - Hash set to be removed.

## void erase ( const Vector <Key>& v )

Removes the specified keys from the hash set.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<Key>&* **v** - Vector storing the keys.

## void subtract ( const Vector <Key>& vector )

Removes the specified keys from the hash set.
### Arguments

- *const [Vector](../../../api/library/containers/vector/class.vector_cpp.md)<Key>&* **vector** - Vector storing the keys.

## void subtract ( const BucketHashSet & o )

Removes the specified hash set from the current hash set.
### Arguments

- *const [BucketHashSet](../../../api/library/containers/class.buckethashset_cpp.md) &* **o** - Hash set to be removed.

## void clear ( )

Removes all key-value pairs from the hash set.
## void destroy ( )

Removes all key-value pairs from the hash set and releases the memory.
## void reserve ( size_t size )

Reserves storage to avoid repeated reallocation.
### Arguments

- *size_t* **size** - Hash size to be reserved.

## void shrink ( )

Removes unused capacity.
## Iterator begin ( ) const

Returns an iterator that points to the first element in the hash set.
### Return value

Iterator pointing to the first element.
## Iterator end ( ) const

Returns an iterator that points to the location succeeding the last element in the hash set.
### Return value

Iterator pointing to the last element.
## ConstIterator cbegin ( ) const

Returns a const iterator that points to the first element in the hash set.
### Return value

ConstIterator pointing to the first element.
## ConstIterator cend ( ) const

Returns a const iterator that points to the location succeeding the last element in the hash set.
### Return value

ConstIterator pointing to the last element.
## Counter size ( ) const

Returns the number of key-value pairs in the hash set.
### Return value

Number of key-value pairs in the hash set.
## Counter space ( ) const

Returns the current capacity (number of elements the hash can currently contain).
### Return value

Number of elements the hash can currently contain.
## size_t getMemoryUsage ( ) const

Shows the amount of memory used by the hash set in bytes.
### Return value

Used memory in bytes.
## bool empty ( ) const

Checks if the hash set is empty.
### Return value

**true** if the hash set is empty, otherwise **false**
## void swap ( HashSet & o )

Swaps this hash set with the hash set specified as the argument.
### Arguments

- *[HashSet](../../../api/library/containers/class.hashset_cpp.md) &* **o** - Hash set.
