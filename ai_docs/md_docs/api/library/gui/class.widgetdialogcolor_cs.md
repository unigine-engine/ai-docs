# Unigine::WidgetDialogColor Class (CS)

**Inherits from:** WidgetDialog


This class creates a dialog with clickable color field, RGB value sliders, color parameters and a predefined palette. There are two color formats available:

- Standard format, which represents colors as four-component vectors.
- Web format, which allows these variants: *RRGGBB*, *RRGGBBAA*, *#RRGGBB*, *#RRGGBBAA*.


## WidgetDialogColor Class

### Properties

## string PaletteColors

The palette colors of the dialog, as a list of colors in the web format separated with semicolons.
## string WebColor

The color selected in the dialog, in the web (hexadecimal) format.
## vec4 Color

The color selected in the dialog.
### Members

---

## WidgetDialogColor ( Gui gui , string str = 0 )

Constructor. Creates a color picker dialog with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the dialog will belong.
- *string* **str** - Dialog title. This is an optional parameter.

## WidgetDialogColor ( string str = 0 )

Constructor. Creates a color picker dialog with given parameters and adds it to the Engine GUI.
### Arguments

- *string* **str** - Dialog title. This is an optional parameter.
