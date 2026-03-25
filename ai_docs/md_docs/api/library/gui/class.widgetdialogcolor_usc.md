# Unigine::WidgetDialogColor Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WidgetDialog


This class creates a dialog with clickable color field, RGB value sliders, color parameters and a predefined palette. There are two color formats available:

- Standard format, which represents colors as four-component vectors.
- Web format, which allows these variants: *RRGGBB*, *RRGGBBAA*, *#RRGGBB*, *#RRGGBBAA*.


## WidgetDialogColor Class

### Members

---

## static WidgetDialogColor ( Gui gui , string str = 0 )

Constructor. Creates a color picker dialog with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the dialog will belong.
- *string* **str** - Dialog title. This is an optional parameter.

## static WidgetDialogColor ( string str = 0 )

Constructor. Creates a color picker dialog with given parameters and adds it to the Engine GUI.
### Arguments

- *string* **str** - Dialog title. This is an optional parameter.

## void setColor ( vec4 color )

Selects a given color.
### Arguments

- *vec4* **color** - Color.

## vec4 getColor ( )

Returns the currently selected color.
### Return value

Current color.
## void setPaletteColors ( string colors )

Fills the palette with given colors.
### Arguments

- *string* **colors** - List of colors in the Web format separated with semicolons.

## string getPaletteColors ( )

Returns the current palette colors.
### Return value

List of colors in the Web format separated with semicolons.
## void setWebColor ( string color )

Selects a color in the Web format.
### Arguments

- *string* **color** - Color in the Web format.

## string getWebColor ( )

Returns the currently selected color in the Web format.
### Return value

Current color.
