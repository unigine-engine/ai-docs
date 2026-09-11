# Unigine::WidgetDialogColor Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WidgetDialog


This class creates a dialog with clickable color field, RGB value sliders, color parameters and a predefined palette. There are two color formats available:

- Standard format, which represents colors as four-component vectors.
- Web format, which allows these variants: *RRGGBB*, *RRGGBBAA*, *#RRGGBB*, *#RRGGBBAA*.


## WidgetDialogColor Class

### Members

## void setPaletteColors ( string colors )

Sets a new palette colors of the dialog, as a list of colors in the web format separated with semicolons.
### Arguments

- *string* **colors** - The palette colors of the dialog, as a list of colors in the web format separated with semicolons

## const char * getPaletteColors () const

Returns the current palette colors of the dialog, as a list of colors in the web format separated with semicolons.
### Return value

Current palette colors of the dialog, as a list of colors in the web format separated with semicolons
## void setWebColor ( string color )

Sets a new color selected in the dialog, in the web (hexadecimal) format.
### Arguments

- *string* **color** - The color selected in the dialog, in the web (hexadecimal) format

## const char * getWebColor () const

Returns the current color selected in the dialog, in the web (hexadecimal) format.
### Return value

Current color selected in the dialog, in the web (hexadecimal) format
## void setColor ( vec4 color )

Sets a new color selected in the dialog.
### Arguments

- *vec4* **color** - The color selected in the dialog

## vec4 getColor () const

Returns the current color selected in the dialog.
### Return value

Current color selected in the dialog
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
