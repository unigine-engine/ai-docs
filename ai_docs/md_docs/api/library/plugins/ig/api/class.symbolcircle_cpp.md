# Unigine::Plugins::IG::SymbolCircle Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


## SymbolCircle Class

### Members

---

## void setFill ( bool value )

Toggles filling of the circle symbol on and off.
### Arguments

- *bool* **value** - true to make the circle symbol filled, otherwise false.

## void setCenter ( float x , float y )

Sets the circle symbol center relative to the plane in the [plane's UV coordinates](../../../../../api/library/plugins/ig/api/class.symbolsplane_cpp.md#setUVSize_float_float_float_float_void).
### Arguments

- *float* **x** - Horizontal offset from the plane's reference point in UV coordinates.
- *float* **y** - Vertical offset from the plane's reference point in UV coordinates.

## void setRadius ( float value )

Sets the circle symbol radius in the [plane's UV coordinates](../../../../../api/library/plugins/ig/api/class.symbolsplane_cpp.md#setUVSize_float_float_float_float_void).
### Arguments

- *float* **value** - Radius of the circle in UV coordinates.

## void setInnerRadius ( float value )

Sets the inner radius of the circle symbol in the [plane's UV coordinates](../../../../../api/library/plugins/ig/api/class.symbolsplane_cpp.md#setUVSize_float_float_float_float_void).
### Arguments

- *float* **value** - Inner radius of the circle in UV coordinates.

## void setSector ( float start_angle , float end_angle )

Creates a circle sector (an arc) by setting two angles that define its limits.
### Arguments

- *float* **start_angle** - Starting angle of the sector.
- *float* **end_angle** - Ending angle of the sector.
