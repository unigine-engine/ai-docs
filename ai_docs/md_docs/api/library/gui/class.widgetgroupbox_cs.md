# Unigine::WidgetGroupBox Class (CS)

**Inherits from:** Widget


This class creates a [group box](../../../code/gui/ui/ui_containers.md#groupbox).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/groupbox.png)


## WidgetGroupBox Class

### Properties

## string Text

The box title.
## int Background

The value indicating if a background texture is rendered for the box.
## vec4 Color

The color of the global color multiplier. The default is equivalent to vec4(1,1,1,1) (white).
## int Stencil

The value indicating if a widget cuts off its children along its set [bounds](../../../api/library/gui/class.widget_cs.md#setWidth_int_void). Everything that lies outside of them is not rendered. This option works only if children have the *[ALIGN_OVERLAP](../../../api/library/gui/class.gui_cs.md#ALIGN_OVERLAP)* flag set (otherwise, they will expand the box widget bounds and no cutting will be done). The default is 0.
## int Border

The flag indicating if a one-pixel border is rendered around the widget content (in a shape of a box). The default is 1 (use a border).
## 🔒︎ int PaddingBottom

The bottom padding for the widget content.
## 🔒︎ int PaddingTop

The top padding for the widget content.
## 🔒︎ int PaddingRight

The right-side padding for the widget content.
## 🔒︎ int PaddingLeft

The left-side padding for the widget content.
## 🔒︎ int SpaceY

The vertical space between the widgets in the box and between them and the box border.
## 🔒︎ int SpaceX

The horizontal space between the widgets in the box and between them and the box border.
## vec4 BorderColor

The border color of the box.
## vec4 BackgroundColor

The background color of the box.
### Members

---

## WidgetGroupBox ( Gui gui , string str = 0 , int x = 0 , int y = 0 )

Constructor. Creates a group box with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new box will belong.
- *string* **str** - Box title. This is an optional parameter.
- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## WidgetGroupBox ( string str = 0 , int x = 0 , int y = 0 )

Constructor. Creates a group box with given parameters and adds it to the Engine GUI.
### Arguments

- *string* **str** - Box title. This is an optional parameter.
- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## void SetPadding ( int l , int r , int t , int b )

Sets widget paddings for all sides. Padding clears an area around the content of a widget (inside of it).
### Arguments

- *int* **l** - Left-side padding in pixels.
- *int* **r** - Right-side padding in pixels.
- *int* **t** - Top padding in pixels.
- *int* **b** - Bottom padding in pixels.

## void SetSpace ( int x , int y )

Sets a space between the widgets in the box and between them and the box border.
### Arguments

- *int* **x** - Horizontal space.
- *int* **y** - Vertical space.
