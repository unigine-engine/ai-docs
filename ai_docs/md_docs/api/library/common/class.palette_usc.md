# Palette Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This structure represents a set of values for 12 major colors of the color spectre used to define [saturation and hue adjustment](../../../editor2/settings/render_settings/color/index.md#saturation_palette).


The following code snippet shows a usage example:


```cpp
Palette p = new Palette();
p.setAzure(0.5f);
engine.render.setColorCorrectionHueShift(p);

```


## Palette Class

### Members

---

## Palette ( )

Constructor. Initializes the structure with zero values.
## Palette ( Palette palette )

Constructor. Initializes the structure using the given Palette.
### Arguments

- *[Palette](../../../api/library/common/class.palette_usc.md)* **palette** - Source Palette.

## void clear ( float value = 0.0f )

Sets all color values to the given value.
### Arguments

- *float* **value** - The new value.

## void copy ( Palette src )

Copies all values from the given palette.
### Arguments

- *[Palette](../../../api/library/common/class.palette_usc.md)* **src** - The source palette.

## void setRed ( float value )

Sets the Red color value.
### Arguments

- *float* **value** - Color value.

## float getRed ( )

Returns the Red color value.
### Return value

Color value.
## void setOrange ( float value )

Sets the Orange color value.
### Arguments

- *float* **value** - Color value.

## float getOrange ( )

Returns the Orange color value.
### Return value

Color value.
## void setYellow ( float value )

Sets the Yellow color value.
### Arguments

- *float* **value** - Color value.

## float getYellow ( )

Returns the Yellow color value.
### Return value

Color value.
## void setChartreuse ( float value )

Sets the Chartreuse color value.
### Arguments

- *float* **value** - Color value.

## float getChartreuse ( )

Returns the Chartreuse color value.
### Return value

Color value.
## void setGreen ( float value )

Sets the Green color value.
### Arguments

- *float* **value** - Color value.

## float getGreen ( )

Returns the Green color value.
### Return value

Color value.
## void setSpringGreen ( float value )

Sets the Spring Green color value.
### Arguments

- *float* **value** - Color value.

## float getSpringGreen ( )

Returns the Spring Green color value.
### Return value

Color value.
## void setCyan ( float value )

Sets the Cyan color value.
### Arguments

- *float* **value** - Color value.

## float getCyan ( )

Returns the Cyan color value.
### Return value

Color value.
## void setAzure ( float value )

Sets the Azure color value.
### Arguments

- *float* **value** - Color value.

## float getAzure ( )

Returns the Azure color value.
### Return value

Color value.
## void setBlue ( float value )

Sets the Blue color value.
### Arguments

- *float* **value** - Color value.

## float getBlue ( )

Returns the Blue color value.
### Return value

Color value.
## void setViolet ( float value )

Sets the Violet color value.
### Arguments

- *float* **value** - Color value.

## float getViolet ( )

Returns the Violet color value.
### Return value

Color value.
## void setMagenta ( float value )

Sets the Magenta color value.
### Arguments

- *float* **value** - Color value.

## float getMagenta ( )

Returns the Magenta color value.
### Return value

Color value.
## void setRose ( float value )

Sets the Rose color value.
### Arguments

- *float* **value** - Color value.

## float getRose ( )

Returns the Rose color value.
### Return value

Color value.
