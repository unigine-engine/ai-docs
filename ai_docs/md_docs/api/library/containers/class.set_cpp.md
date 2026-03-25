# Unigine::Set Class (CPP)

**Header:** #include <UnigineSet.h>


A set is a container template in which each element must be unique as the value of the element identifies it. The values are stored in the *ascending* order.


To create a new set, you can use the [default constructor](#Set) or one of the following ways:


- Create a new set by using the constructor with an initializer list: ```cpp const Set<int> my_set{ 1, 6, 4, 3, 7 }; // check the result for (const auto &it : my_set) Log::message("%d ", it.key); ```
- Create a new set using a copy constructor: ```cpp // constructor that takes an initializer list const Set<String> initial{ "a", "e" }; // copy constructor const Set<String> copied(initial); // check the result for (const auto &it : copied) Log::message("%s ", it.key.get()); ```


Also you can modify a set by using the *[append()](#append_const_Key_ref_void)* and *[insert()](#insert_Key_rvref_void)* class member functions. Check some of the usage examples:


- Create a new set and append elements to it one by one: ```cpp Set<int> my_set; my_set.append(1); my_set.append(10); my_set.append(4); // check the result for (const auto &it : my_set) Log::message("%d ", it.key); ```
- Create a new set and append another set to it: ```cpp // create a set using an initializer list const Set<int> my_set_0{ 1, 6, 4, 3, 7 }; // declare a new set Set<int> my_set_1; // append the "my_set_0" to it my_set_1.append(my_set_0); // check the result for (const auto &it : my_set) Log::message("%d ", it.key); ```
- Modify the existing set that already contains elements: > **Notice:** If an element already exists in the initial set, it will not be added. ```cpp // create sets using initializer lists Set<String> initial{ "a", "b", "c", "d", "e" }; Set<String> to_add{ "m", "n", "o" }; // append keys of the "to_add" set to the "initial" set initial.append(to_add); // insert a key into the "initial" set initial.insert("s"); // check the result for (const auto &it : initial) Log::message("%s ", it.key.get()); ```


## Set Class

### Members

---

## Set ( )

Default constructor that produces an empty set.
## Set ( std::initializer_list<Key> list )

Constructor. Creates a set from keys of the giving list.
### Arguments

- *std::initializer_list<Key>* **list** - List of keys.

## Set ( Set <Key, Allocator> && o )

Constructor. Creates a set by copying a source set.
### Arguments

- *[Set](../../../api/library/containers/class.set_cpp.md)<Key, Allocator> &&* **o** - Source set.

## Set ( const Set <Key, Allocator> & o )

Constructor. Creates a set by copying a source set.
### Arguments

- *const [Set](../../../api/library/containers/class.set_cpp.md)<Key, Allocator> &* **o** - Source set.

## void append ( const Key & key )

Appends a key.
### Arguments

- *const Key &* **key** - Key.

## void append ( Key && key )

Appends a key.
### Arguments

- *Key &&* **key** - Key.

## void insert ( Key && key )

Inserts a given key into the set.
### Arguments

- *Key &&* **key** - Key.

## void insert ( const Key & key )

Inserts a given key into the set.
### Arguments

- *const Key &* **key** - Key.

## Set <Key, Allocator> & operator= ( const Set <Key, Allocator> & o )

Assignment operator for the set.
### Arguments

- *const [Set](../../../api/library/containers/class.set_cpp.md)<Key, Allocator> &* **o** - Set.

## Set <Key, Allocator> & operator= ( Set <Key, Allocator> && o )

Assignment operator for the set.
### Arguments

- *[Set](../../../api/library/containers/class.set_cpp.md)<Key, Allocator> &&* **o** - Set.

## void append ( const Set <Key, Allocator> & s )

Appends a given set to the current one.
### Arguments

- *const [Set](../../../api/library/containers/class.set_cpp.md)<Key, Allocator> &* **s** - Set.

## void append ( Set <Key, Allocator> && s )

Appends a given set to the current one.
### Arguments

- *[Set](../../../api/library/containers/class.set_cpp.md)<Key, Allocator> &&* **s** - Set.

## void insert ( const Set <Key, Allocator> & o )

Inserts a given set into the current one.
### Arguments

- *const [Set](../../../api/library/containers/class.set_cpp.md)<Key, Allocator> &* **o** - Set.

## void insert ( Set <Key, Allocator> && o )

Inserts a given set into the current one.
### Arguments

- *[Set](../../../api/library/containers/class.set_cpp.md)<Key, Allocator> &&* **o** - Set.
