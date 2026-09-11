# Unigine::WidgetSpacer Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Widget


This class creates a [line spacer](../../../code/gui/ui/ui_widgets.md#hspacer): [horizontal](../../../code/gui/ui/ui_widgets.md#hspacer) or [vertical](../../../code/gui/ui/ui_widgets.md#vspacer) one.


The object of this class may look as follows:


![Horizontal spacer](../../../code/gui/ui/widgets/hspacer.png)

*Horizontal spacer*


![Vertical spacer](../../../code/gui/ui/widgets/vspacer.png)

*Vertical spacer*


## WidgetSpacer Class

### Members

## void setOrientation ( int orientation )

Sets a new orientation of the spacer: horizontal or vertical.
### Arguments

- *int* **orientation** - The orientation of the spacer (horizontal or vertical)

## int getOrientation () const

Returns the current orientation of the spacer: horizontal or vertical.
### Return value

Current orientation of the spacer (horizontal or vertical)
---

## static WidgetSpacer ( Gui gui )

Constructor. Creates a spacer and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the spacer will belong.

## static WidgetSpacer ( )

Constructor. Creates a spacer and adds it to the Engine GUI.
