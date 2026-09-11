# Palette Class (CPP)

**Header:** #include <UniginePalette.h>


This structure represents a set of values for 12 major colors of the color spectre used to define [saturation and hue adjustment](../../../editor2/settings/render_settings/color/index.md#saturation_palette).


The following code snippet shows a usage example:


```cpp
#include <UniginePalette.h>

Palette p = Palette(0.5f);
Render::setColorCorrectionHueShift(p);

```


## Palette Class

### Enums

## Color

| Name | Description |
|---|---|
| **RED** = 0 | Red color. |
| **ORANGE** = 1 | Orange color. |
| **YELLOW** = 2 | Yellow color. |
| **CHARTREUSE** = 3 | Chartreuse color. |
| **GREEN** = 4 | Green color. |
| **SPRINGGREEN** = 5 | Spring Green color. |
| **CYAN** = 6 | Cyan color. |
| **AZURE** = 7 | Azure color. |
| **BLUE** = 8 | Blue color. |
| **VIOLET** = 9 | Violet color. |
| **MAGENTA** = 10 | Magenta color. |
| **ROSE** = 11 | Rose color. |
| **SIZE** = 12 | The number of colors. |

### Members

---

## Palette ( )

Constructor. Initializes the structure with zero values.
## Palette ( const Palette & palette )

Constructor. Initializes the structure using the given Palette.
### Arguments

- *const [Palette](../../../api/library/common/class.palette_cpp.md) &* **palette** - Source Palette.

## Palette ( const float (&)[12] palette )

Constructor. Initializes the structure using the given array of floats.
### Arguments

- *const float (&)[12]* **palette** - Source array of 12 float values.

## Palette ( float value )

Constructor. Initializes the structure using the given float for all values.
### Arguments

- *float* **value** - value to be set for all color values.

## Palette & operator= ( const Palette & palette )

Performs structure assignment. Destination palette = source palette.
### Arguments

- *const [Palette](../../../api/library/common/class.palette_cpp.md) &* **palette** - Source palette.

### Return value

Result.
## bool operator== ( const Palette & palette ) const

Check if two palettes are the same.
### Arguments

- *const [Palette](../../../api/library/common/class.palette_cpp.md) &* **palette** - The second palette.

### Return value

true if the palettes are the same; otherwise, false.
## bool operator== ( const float (&)[12] palette ) const

Check if two palettes are the same.
### Arguments

- *const float (&)[12]* **palette** - The second palette represented by an array of 12 float values.

### Return value

true if the palettes are the same; otherwise, false.
## bool operator== ( float value ) const

Check if all values of the palette are equal to the given value.
### Arguments

- *float* **value** - The value to check.

### Return value

true if all values of the palette are equal to the given value; otherwise, false.
## bool operator!= ( const Palette & palette ) const

Check if two palettes are not the same.
### Arguments

- *const [Palette](../../../api/library/common/class.palette_cpp.md) &* **palette** - The second palette.

### Return value

true if the palettes are not the same; otherwise, false.
## bool operator!= ( const float (&)[12] palette ) const

Check if two palettes are not the same.
### Arguments

- *const float (&)[12]* **palette** - The second palette represented by an array of 12 float values.

### Return value

true if the palettes are not the same; otherwise, false.
## bool operator!= ( float value ) const

Check if all values of the palette are not equal to the given value.
### Arguments

- *float* **value** - The value to check.

### Return value

true if any value of the palette is not equal to the given value; otherwise, false.
## void clear ( float value = 0.0f )

Sets all color values to the given value.
### Arguments

- *float* **value** - The new value.

## void copy ( const Palette & src )

Copies all values from the given palette.
### Arguments

- *const [Palette](../../../api/library/common/class.palette_cpp.md) &* **src** - The source palette.
