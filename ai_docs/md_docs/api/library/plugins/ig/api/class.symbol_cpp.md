# Unigine::Plugins::IG::Symbol Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


This class represents the *IG Symbol* interface. A symbol is a single drawing primitive or a group of drawing primitives that may be drawn on a [symbol surface (plane)](../../../../../api/library/plugins/ig/api/class.symbolsplane_cpp.md) within a particular [view](../../../../../api/library/plugins/ig/api/class.view_cpp.md) or placed relative to a particular [entity](../../../../../api/library/plugins/ig/api/class.entity_cpp.md).


> **Notice:** IG plugin must be loaded.


## Symbol Class

### Members

---

## int getID ( ) const

Returns the ID of the symbol.
## void setParent ( Symbol * symbol )

Sets a new parent for the symbol.
### Arguments

- *[Symbol](../../../../../api/library/plugins/ig/api/class.symbol_cpp.md) ** **symbol** - Symbol to be set as parent for the symbol.

## Symbol * getParent ( ) const

Returns the parent of the symbol.
### Return value

Parent of the symbol.
## void setVisible ( bool value )

Toggles visibility of the symbol on and off.
### Arguments

- *bool* **value** - true to make the symbol visible, otherwise false.

## bool isVisible ( ) const

Checks if the symbol is visible.
### Return value

true if the symbol is visible, otherwise false.
## void setOrder ( int value )

Sets rendering order (Z-order) for the symbol. The higher the value, the later the symbol is rendered atop other elements.
### Arguments

- *int* **value** - Order of the symbol.

## void setOffset ( float x , float y )

Sets the symbol's position relevant to the parent plane or symbol.
### Arguments

- *float* **x** - Horizontal offset from the parent.
- *float* **y** - Vertical offset from the parent.

## vec2 getOffset ( ) const

Returns the symbol's position relevant to the parent plane or symbol.
### Return value

Offset from the parent.
## void setScale ( float scale_x , float scale_y )

Sets the symbol's scale.
### Arguments

- *float* **scale_x** - The symbol's scale along the X axis.
- *float* **scale_y** - The symbol's scale along the Y axis.

## vec2 getScale ( ) const

Returns the symbol's scale.
### Return value

Symbol's scale.
## void setRotation ( float angle_anticlockwise )

Sets the rotation angle for the symbol.
### Arguments

- *float* **angle_anticlockwise** - Angle of rotation in counter-clockwise direction.

## float getRotation ( ) const

Returns the rotation angle for the symbol.
### Return value

Angle of rotation in counter-clockwise direction.
## void setFlashProgram ( const Unigine:: Vector <float> & data )

Sets the flash program for the symbol. The program uses a sequence of indicated time periods in seconds to consecutively enable and disable the symbol starting from the Enabled state. For example, a sequence 0.3;0.05;0.1 means that a symbol is enabled for 0.3 seconds, then disabled for 0.05 seconds, enabled for 0.1 seconds, and then continues to be enabled for 0.3 seconds, etc. To disable the program, the array should be empty.
### Arguments

- *const  Unigine::[Vector](../../../../../api/library/containers/vector/class.vector_cpp.md)<float> &* **data** - Flash program for the symbol.

## void resetFlashProgram ( )

Starts the flash program anew.
## void setColor ( const vec4 & color )

Sets the color of the symbol.
### Arguments

- *const [vec4](../../../../../api/library/math/class.vec4_cpp.md) &* **color** - Color of the symbol in the RGBA range.

## void setColorInherit ( bool value )

Toggles inheritance of the color from the parent symbol on and off.
### Arguments

- *bool* **value** - true to inherit the color from the parent symbol, otherwise false.

## void setLineWidth ( float value )

Sets the width of lines the symbol is drawn of.
### Arguments

- *float* **value** - Width of the line.

## int getType ( ) const

Returns the type of the symbol.
### Return value

Symbol type.
