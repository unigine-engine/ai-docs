# Unigine::Map Class (CPP)

**Header:** #include <UnigineMap.h>


A map container template.


> **Warning:** In UnigineScript, a map is a type that maps values to keys. See [Containers](../../../code/uniginescript/language/containers/index.md#maps) article for the details.


## Map Class

### Members

---

## Map ( )

Default constructor that produces an empty map.
## Type & get ( const Key & key )

Return an item by key.
### Arguments

- *const Key &* **key** - Item key.

### Return value

The item.
## void append ( const Key & key , const Type & t )

Appends an item.
### Arguments

- *const Key &* **key** - Key.
- *const Type &* **t** - Item.

## void append ( const Map <Key, Type> & m )

Appends a map.
### Arguments

- *const [Map](../../../api/library/containers/class.map_cpp.md)<Key, Type> &* **m** - Map.

## Map < Key, Type >::Iterator findData ( const Type & t ) const

Finds an item in the map.
### Arguments

- *const Type &* **t** - Item.

### Return value

The iterator.
## Type & operator[] ( const Key & key )

Map access.
### Arguments

- *const Key &* **key** - Item key.

### Return value

The item.
