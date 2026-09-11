# Unigine::Plugins::IG::SymbolsController Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


This class represents the *IG Symbols Controller* interface. A symbol is a single drawing primitive or a group of drawing primitives that may be drawn on a symbol surface (plane) within a particular [view](../../../../../api/library/plugins/ig/api/class.view_cpp.md) or placed in 3D space relative to a particular [entity](../../../../../api/library/plugins/ig/api/class.entity_cpp.md).


The following symbol types are available: Polyline, Text, Circle.


> **Notice:** IG plugin must be loaded.


## SymbolsController Class

### Enums

## SYMBOL_TYPE

| Name | Description |
|---|---|
| **SYMBOL_TYPE_POLYLINE** = 0 | Polyline. |
| **SYMBOL_TYPE_TEXT** = 1 | Text. |
| **SYMBOL_TYPE_CIRCLE** = 2 | Circle. |

### Members

---

## Symbol * createSymbol ( SymbolsController::SYMBOL_TYPE type , int symbol_id )

Creates a new [symbol](../../../../../api/library/plugins/ig/api/class.symbol_cpp.md).
> **Notice:** Symbol must be immediately added to SymbolsPlane.


### Arguments

- *[SymbolsController::SYMBOL_TYPE](../../../../../api/library/plugins/ig/api/class.symbolscontroller_cpp.md#SYMBOL_TYPE)* **type** - Type of the symbol:

  - POLYLINE
  - TEXT
  - CIRCLE
- *int* **symbol_id** - ID of the symbol.

### Return value

Pointer to the new created symbol interface.
## Symbol * cloneSymbol ( int symbol_id , int new_symbol_id )

Clones a [symbol](../../../../../api/library/plugins/ig/api/class.symbol_cpp.md) with the specified ID.
### Arguments

- *int* **symbol_id** - ID of the symbol to be cloned.
- *int* **new_symbol_id** - ID of the new symbol.

### Return value

Pointer to the new cloned symbol interface.
## SymbolsPlane * createPlane ( int plane_id , View * view )

Creates a new [symbols surface](../../../../../api/library/plugins/ig/api/class.symbolsplane_cpp.md) (a virtual plane on which symbols are drawn).A new surface is placed in 3D space coincident with the near clipping plane of the specified [view](../../../../../api/library/plugins/ig/api/class.view_cpp.md).
### Arguments

- *int* **plane_id** - ID of the symbol.
- *[View](../../../../../api/library/plugins/ig/api/class.view_cpp.md) ** **view** - View relative to which a new symbols surface is to be placed.

### Return value

Pointer to the new created symbols surface interface.
## SymbolsPlane * createPlane ( int plane_id , Entity * entity )

Creates a new [symbols surface](../../../../../api/library/plugins/ig/api/class.symbolsplane_cpp.md) (a virtual plane on which symbols are drawn). A new surface is placed in 3D space relative to the specified [entity](../../../../../api/library/plugins/ig/api/class.entity_cpp.md).
### Arguments

- *int* **plane_id** - ID of the symbol.
- *[Entity](../../../../../api/library/plugins/ig/api/class.entity_cpp.md) ** **entity** - Entity relative to which a new symbols surface is to be placed.

### Return value

Pointer to the new created symbols surface interface.
## Symbol * getSymbol ( int symbol_id ) const

Returns the [interface](../../../../../api/library/plugins/ig/api/class.symbol_cpp.md) of the specified symbol.
### Arguments

- *int* **symbol_id** - ID of the symbol.

### Return value

Pointer to the new created symbol interface.
## SymbolsPlane * getPlane ( int plane_id ) const

Returns the [interface](../../../../../api/library/plugins/ig/api/class.symbolsplane_cpp.md) of the specified symbols surface (a virtual plane on which symbols are drawn).
### Arguments

- *int* **plane_id** - ID of the symbols surface.

### Return value

Pointer to the new created symbols surface interface.
## void removeSymbol ( int symbol_id )

Removes the symbol with the specified ID.
### Arguments

- *int* **symbol_id** - ID of the symbol to be removed.

## void removePlane ( int plane_id )

Removes the symbols surface (plane) with the specified ID, and all symbols related to it.
### Arguments

- *int* **plane_id** - ID of the symbols surface (plane) to be removed.

## void clear ( )

Removes all symbols and planes.
