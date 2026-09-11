# Unigine::Plugins::IG::SymbolsPlane Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


This class represents the *IG Symbols Plane* interface. A symbol surface (plane) is a rectangular, two-dimensional drawing region on a virtual plane on which [symbols](../../../../../api/library/plugins/ig/api/class.symbol_cpp.md) may be drawn. Such plane is placed in 3D space relative to a particular entity or coincident with the near clipping plane of a particular view.


> **Notice:** IG plugin must be loaded.


## SymbolsPlane Class

### Enums

## SYMBOLS_PLANE_TYPE

| Name | Description |
|---|---|
| **SYMBOLS_PLANE_TYPE_ENTITY** = 0 | The symbols plane is placed relative to a particular entity. |
| **SYMBOLS_PLANE_TYPE_VIEW** = 1 | The symbols plane is coincident with the near clipping plane of a particular view. |

### Members

---

## int getID ( ) const

Returns the plane identifier.
### Return value

Identifier of the plane.
## void addSymbol ( Symbol * symbol )

Adds the specified [symbol](../../../../../api/library/plugins/ig/api/class.symbol_cpp.md) to the plane.
### Arguments

- *[Symbol](../../../../../api/library/plugins/ig/api/class.symbol_cpp.md) ** **symbol** - Symbol to be added.

## void setBillboard ( bool enable , bool fixed_scale )

Toggles on and off the plane orientation to the viewer and fixing the plane size regardless of the distance to it.
### Arguments

- *bool* **enable** - true to make the plane a billboard (always oriented to the viewer), false to disable orientation to the viewer.
- *bool* **fixed_scale** - true to make the billboard size unchanged regardless of its distance from the viewer, false � to disable.

## bool isBillboard ( ) const

Checks if a node is a billboard (always oriented to the viewer).
### Return value

true if a node is a billboard, otherwise false.
## bool isFixedBillboardScale ( ) const

Checks if the billboard size is fixed relative to the viewer regardless of the distance.
### Return value

true if the billboard scale is fixed, otherwise false.
## void setPosition ( const Math:: vec3 & value )

Sets the plane position relative to the entity, if the plane has a parent entity.
### Arguments

- *const  Math::[vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **value** - Position in the coordinate system of a parent entity.

## void setRotation ( const Math:: quat & rotate )

Sets the plane rotation relative to the parent entity. The method is not applicable to billboards.
### Arguments

- *const  Math::[quat](../../../../../api/library/math/class.quat_cpp.md) &* **rotate** - Rotation quaternion for the plane

## void setPhysicalSize ( float width , float height )

Sets the plane size for planes that have a parent entity.
### Arguments

- *float* **width** - Width of the symbols plane, in units
- *float* **height** - Height of the symbols plane, in units

## vec2 getPhysicalSize ( ) const

Returns the physical size of the symbols plane, in units.
### Return value

Vector containing physical size of the symbols plane (width, height), in units.
## void setUVSize ( float minU , float minV , float maxU , float maxV )

Sets the symbol surface 2D coordinate system.
### Arguments

- *float* **minU** - Minimum U value of the symbol surface.
- *float* **minV** - Minimum V value of the symbol surface.
- *float* **maxU** - Maximum U value of the symbol surface.
- *float* **maxV** - Maximum V value of the symbol surface.

## vec4 getUVSize ( ) const

Returns the current symbol surface 2D coordinate system.
### Return value

Vector containing the following values: (Minimum U, Minimum V, Maximum U, Maximum V).
## void setScreenSize ( float width , float height , float offsetX , float offsetY )

Sets the screen plane resolution and offset in pixels.
### Arguments

- *float* **width** - Width of the screen plane, in pixels.
- *float* **height** - Height of the screen plane, in pixels.
- *float* **offsetX** - Horizontal offset of the screen plane.
- *float* **offsetY** - Vertical offset of the screen plane.

## vec4 getScreenSize ( ) const

Returns the screen plane resolution and offset in pixels.
### Return value

Vector containing screen dimensions of the symbols plane (screen_width, screen_height, offset_z, offset_y), in pixels.
## SymbolsPlane::SYMBOLS_PLANE_TYPE getType ( ) const

Returns the type of the symbols plane.
### Return value

Symbols plane type.
## Unigine:: Vector < Symbol * > getRootSymbols ( ) const

Returns all root symbols attached to the plane.
### Return value

Vector containing all root symbols attached to the plane.
## Unigine:: Vector < Symbol *> getSymbols ( ) const

Returns all symbols attached to the plane (roots and all their children).
### Return value

Vector containing all symbols attached to the plane.
## vec3 getPosition ( ) const

Returns the current position of the symbols plane.
### Return value

Vector containing coordinates of the symbols plane position.
## quat getRotation ( ) const

Returns the current rotation of the symbols plane.
### Return value

Quaternion representing rotation of the symbols plane position.
## int getPixelsPerUnitV ( ) const

Returns the number of pixels per single vertical unit of the symbol surface.
### Return value

Size of the the vertical unit in pixels.
