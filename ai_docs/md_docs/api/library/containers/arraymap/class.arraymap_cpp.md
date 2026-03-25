# Unigine::ArrayMap Class (CPP)

**Header:** #include <UnigineInterpreter.h>


Allows using UnigineScript [maps](../../../../code/uniginescript/language/containers/index.md#maps).


## ArrayMap Class

### Members

---

## ArrayMap ( const ArrayMap & map )

Copy constructor.
### Arguments

- *const [ArrayMap](../../../../api/library/containers/arraymap/class.arraymap_cpp.md) &* **map** - Map.

## void set ( const Variable & key , const Variable & v ) const

Set an item by key.
### Arguments

- *const [Variable](../../../../api/library/common/class.variable_cpp.md) &* **key** - Item key.
- *const [Variable](../../../../api/library/common/class.variable_cpp.md) &* **v** - Item to set.

## static ArrayMap get ( void * interpreter , const Variable & id )

Return a map from UnigineScript.
### Arguments

- *void ** **interpreter** - Interpreter pointer.
- *const [Variable](../../../../api/library/common/class.variable_cpp.md) &* **id** - Map ID.

### Return value

The map.
## const Variable & get ( const Variable & key ) const

Return an item by key.
### Arguments

- *const [Variable](../../../../api/library/common/class.variable_cpp.md) &* **key** - Item key.

### Return value

The item.
## int size ( ) const

Return map length.
### Return value

Map length.
## void clear ( ) const

Clear all items of the map.
## void append ( const Variable & key , const Variable & v ) const

Append an item with a given key to the map.
### Arguments

- *const [Variable](../../../../api/library/common/class.variable_cpp.md) &* **key** - Item key.
- *const [Variable](../../../../api/library/common/class.variable_cpp.md) &* **v** - Item.

## void remove ( const Variable & key ) const

Remove an item with a given key from the map.
### Arguments

- *const [Variable](../../../../api/library/common/class.variable_cpp.md) &* **key** - Item key.

## Iterator back ( )

Return an iterator referring to the back element.
### Return value

Back iterator.
## Iterator begin ( )

Return an iterator referring to the first element.
### Return value

Begin iterator.
## Iterator end ( )

Return an iterator referring to the end element.
### Return value

End iterator.
## Iterator find ( const Variable & key ) const

Find an item by a given key.
### Arguments

- *const [Variable](../../../../api/library/common/class.variable_cpp.md) &* **key** - Item key.

### Return value

Iterator to it if found; otherwise returns an iterator to end.
## ArrayMap & operator= ( const ArrayMap & map )

Assignment operator for the map.
### Arguments

- *const [ArrayMap](../../../../api/library/containers/arraymap/class.arraymap_cpp.md) &* **map** - Map to be assigned.

## const Variable & operator[] ( const Variable & key ) const

Map access.
### Arguments

- *const [Variable](../../../../api/library/common/class.variable_cpp.md) &* **key** - Item key.

### Return value

The item.
