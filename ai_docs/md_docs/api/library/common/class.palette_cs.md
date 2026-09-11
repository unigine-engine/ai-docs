# Palette Class (CS)


This structure represents a set of values for 12 major colors of the color spectre used to define [saturation and hue adjustment](../../../editor2/settings/render_settings/color/index.md#saturation_palette).


The following code snippet shows a usage example:


```csharp
Palette p = new Palette(0.5f);
Render.ColorCorrectionHueShift = p;

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
## Palette ( Palette palette )

Constructor. Initializes the structure using the given Palette.
### Arguments

- *[Palette](../../../api/library/common/class.palette_cs.md)* **palette** - Source Palette.

## Palette ( float value )

Constructor. Initializes the structure using the given float for all values.
### Arguments

- *float* **value** - value to be set for all color values.

## Palette operator= ( Palette palette )

Performs structure assignment. Destination palette = source palette.
### Arguments

- *[Palette](../../../api/library/common/class.palette_cs.md)* **palette** - Source palette.

### Return value

Result.
## bool Equals ( Palette palette )

Check if two palettes are the same.
### Arguments

- *[Palette](../../../api/library/common/class.palette_cs.md)* **palette** - The second palette.

### Return value

true if the palettes are the same; otherwise, false.
## bool Equals ( float value )

Check if all values of the palette are equal to the given value.
### Arguments

- *float* **value** - The value to check.

### Return value

true if all values of the palette are equal to the given value; otherwise, false.
## bool NotEquals ( Palette palette )

Check if two palettes are not the same.
### Arguments

- *[Palette](../../../api/library/common/class.palette_cs.md)* **palette** - The second palette.

### Return value

true if the palettes are not the same; otherwise, false.
## bool NotEquals ( float value )

Check if all values of the palette are not equal to the given value.
### Arguments

- *float* **value** - The value to check.

### Return value

true if any value of the palette is not equal to the given value; otherwise, false.
## void Clear ( float value = 0.0f )

Sets all color values to the given value.
### Arguments

- *float* **value** - The new value.

## void Copy ( Palette src )

Copies all values from the given palette.
### Arguments

- *[Palette](../../../api/library/common/class.palette_cs.md)* **src** - The source palette.

## void SetColor ( Palette.Color color , float value )

Sets the given color to the given value.
### Arguments

- *[Palette.Color](../../../api/library/common/class.palette_cs.md#Color)* **color** - One of [Palette.Color](#Color) values.
- *float* **value** - The color value.

## void GetColor ( Palette.Color src )

Returns the color value.
### Arguments

- *[Palette.Color](../../../api/library/common/class.palette_cs.md#Color)* **src** - One of [Palette.Color](#Color) values.
