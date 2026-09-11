# Unigine::Plugins::IG::SymbolsController Class (CS)


This class represents the *IG Symbols Controller* interface. A symbol is a single drawing primitive or a group of drawing primitives that may be drawn on a symbol surface (plane) within a particular [view](../../../../../api/library/plugins/ig/api/class.view_cs.md) or placed in 3D space relative to a particular [entity](../../../../../api/library/plugins/ig/api/class.entity_cs.md).


The following symbol types are available: Polyline, Text, Circle.


> **Notice:** IG plugin must be loaded.


## SymbolsController Class

### Enums

## SYMBOL_TYPE

| Name | Description |
|---|---|
| **POLYLINE** = 0 | Polyline. |
| **TEXT** = 1 | Text. |
| **CIRCLE** = 2 | Circle. |

### Members

---

## Symbol CreateSymbol ( int symbol_id )

Creates a new [symbol](../../../../../api/library/plugins/ig/api/class.symbol_cs.md).
> **Notice:** Symbol must be immediately added to SymbolsPlane.


### Arguments

- *int* **symbol_id** - ID of the symbol.

### Return value

New created symbol interface instance.
## Symbol CloneSymbol ( int symbol_id , int new_symbol_id )

Clones a [symbol](../../../../../api/library/plugins/ig/api/class.symbol_cs.md) with the specified ID.
### Arguments

- *int* **symbol_id** - ID of the symbol to be cloned.
- *int* **new_symbol_id** - ID of the new symbol.

### Return value

New cloned symbol interface instance.
## SymbolsPlane CreatePlane ( int plane_id , View * view )

Creates a new [symbols surface](../../../../../api/library/plugins/ig/api/class.symbolsplane_cs.md) (a virtual plane on which symbols are drawn).A new surface is placed in 3D space coincident with the near clipping plane of the specified [view](../../../../../api/library/plugins/ig/api/class.view_cs.md).
### Arguments

- *int* **plane_id** - ID of the symbol.
- *[View](../../../../../api/library/plugins/ig/api/class.view_cs.md) ** **view** - View relative to which a new symbols surface is to be placed.

### Return value

New created symbols surface interface instance.
## SymbolsPlane * CreatePlane ( int plane_id , Entity entity )

Creates a new [symbols surface](../../../../../api/library/plugins/ig/api/class.symbolsplane_cs.md) (a virtual plane on which symbols are drawn). A new surface is placed in 3D space relative to the specified [entity](../../../../../api/library/plugins/ig/api/class.entity_cs.md).
### Arguments

- *int* **plane_id** - ID of the symbol.
- *[Entity](../../../../../api/library/plugins/ig/api/class.entity_cs.md)* **entity** - Entity relative to which a new symbols surface is to be placed.

### Return value

## Symbol GetSymbol ( int symbol_id )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.symbol_cs.md) of the specified symbol.
### Arguments

- *int* **symbol_id** - ID of the symbol.

### Return value

New created symbol interface instance.
## SymbolsPlane GetPlane ( int plane_id )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.symbolsplane_cs.md) of the specified symbols surface (a virtual plane on which symbols are drawn).
### Arguments

- *int* **plane_id** - ID of the symbols surface.

### Return value

New created symbols surface interface instance.
## void RemoveSymbol ( int symbol_id )

Removes the symbol with the specified ID.
### Arguments

- *int* **symbol_id** - ID of the symbol to be removed.

## void RemovePlane ( int plane_id )

Removes the symbols surface (plane) with the specified ID, and all symbols related to it.
### Arguments

- *int* **plane_id** - ID of the symbols surface (plane) to be removed.

## void Clear ( )

Removes all symbols and planes.
