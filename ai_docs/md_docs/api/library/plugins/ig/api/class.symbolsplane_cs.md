# Unigine::Plugins::IG::SymbolsPlane Class (CS)


This class represents the *IG Symbols Plane* interface. A symbol surface (plane) is a rectangular, two-dimensional drawing region on a virtual plane on which [symbols](../../../../../api/library/plugins/ig/api/class.symbol_cs.md) may be drawn. Such plane is placed in 3D space relative to a particular entity or coincident with the near clipping plane of a particular view.


> **Notice:** IG plugin must be loaded.


## SymbolsPlane Class

### Enums

## SYMBOLS_PLANE_TYPE

| Name | Description |
|---|---|
| **ENTITY** = 0 | The symbols plane is placed relative to a particular entity. |
| **VIEW** = 1 | The symbols plane is coincident with the near clipping plane of a particular view. |

### Members

---

## int GetID ( )

Returns the plane identifier.
### Return value

Identifier of the plane.
## void AddSymbol ( Symbol symbol )

Adds the specified [symbol](../../../../../api/library/plugins/ig/api/class.symbol_cs.md) to the plane.
### Arguments

- *Symbol* **symbol** - Symbol to be added.

## void SetBillboard ( bool enable , bool fixed_scale )

Toggles on and off the plane orientation to the viewer and fixing the plane size regardless of the distance to it.
### Arguments

- *bool* **enable** - true to make the plane a billboard (always oriented to the viewer), false to disable orientation to the viewer.
- *bool* **fixed_scale** - true to make the billboard size unchanged regardless of its distance from the viewer, false � to disable.

## bool IsBillboard ( )

Checks if a node is a billboard (always oriented to the viewer).
### Return value

true if a node is a billboard, otherwise false.
## bool IsFixedBillboardScale ( )

Checks if the billboard size is fixed relative to the viewer regardless of the distance.
### Return value

true if the billboard scale is fixed, otherwise false.
## void SetPosition ( vec3 value )

Sets the plane position relative to the entity, if the plane has a parent entity.
### Arguments

- *vec3* **value** - Position in the coordinate system of a parent entity.

## void SetRotation ( quat rotate )

Sets the plane rotation relative to the parent entity. The method is not applicable to billboards.
### Arguments

- *quat* **rotate** - Rotation quaternion for the plane

## void SetPhysicalSize ( float width , float height )

Sets the plane size for planes that have a parent entity.
### Arguments

- *float* **width** - Width of the symbols plane, in units
- *float* **height** - Height of the symbols plane, in units

## vec2 GetPhysicalSize ( )

Returns the physical size of the symbols plane, in units.
### Return value

Vector containing physical size of the symbols plane (width, height), in units.
## void SetUVSize ( float minU , float minV , float maxU , float maxV )

Sets the symbol surface 2D coordinate system.
### Arguments

- *float* **minU** - Minimum U value of the symbol surface.
- *float* **minV** - Minimum V value of the symbol surface.
- *float* **maxU** - Maximum U value of the symbol surface.
- *float* **maxV** - Maximum V value of the symbol surface.

## vec4 GetUVSize ( )

Returns the current symbol surface 2D coordinate system.
### Return value

Vector containing the following values: (Minimum U, Minimum V, Maximum U, Maximum V).
## void SetScreenSize ( float width , float height , float offsetX , float offsetY )

Sets the screen plane resolution and offset in pixels.
### Arguments

- *float* **width** - Width of the screen plane, in pixels.
- *float* **height** - Height of the screen plane, in pixels.
- *float* **offsetX** - Horizontal offset of the screen plane.
- *float* **offsetY** - Vertical offset of the screen plane.

## vec4 GetScreenSize ( )

Returns the screen plane resolution and offset in pixels.
### Return value

Vector containing screen dimensions of the symbols plane (screen_width, screen_height, offset_z, offset_y), in pixels.
## SymbolsPlane.SYMBOLS_PLANE_TYPE GetType ( )

Returns the type of the symbols plane.
### Return value

Symbols plane type.
## vec3 GetPosition ( )

Returns the current position of the symbols plane.
### Return value

Vector containing coordinates of the symbols plane position.
## quat GetRotation ( )

Returns the current rotation of the symbols plane.
### Return value

Quaternion representing rotation of the symbols plane position.
## int GetPixelsPerUnitV ( )

Returns the number of pixels per single vertical unit of the symbol surface.
### Return value

Size of the the vertical unit in pixels.
