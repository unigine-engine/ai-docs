# Unigine::WidgetScrollBox Class (CS)

**Inherits from:** Widget


This class creates a [scroll box](../../../code/gui/ui/ui_containers.md#scrollbox).


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/scrollbox.png)


### See Also


- C++ sample
- C# Component sample
- UnigineScript sample


## WidgetScrollBox Class

### Enums

## SCROLL_RENDER_MODE

| Name | Description |
|---|---|
| **ALWAYS_RENDER** = 0 | Scroll bar is always rendered. |
| **AUTO_HIDE** = 1 | Scroll bar is automatically hidden when necessary. For example, if the container area is big enough to show all elements, the scroll bar is not rendered. And vice versa, if not all elements can be shown at once, a scroll bar is rendered. |
| **ALWAYS_HIDE** = 2 | Scroll bar is always hidden. In this mode, though a bar itself is not rendered, the scroll bar bounds are still taken into account when the widget bounds are calculated. |
| **ALWAYS_HIDE_NO_BOUNDS** = 3 | Scroll bar is always hidden and its size is not added to widget bounds. |

### Properties

## 🔒︎ WidgetScroll HScroll

The horizontal scroller object.
## int HScrollValue

The position (and also automatically the size) of the horizontal scroller. That is, it returns the width of the currently invisible area that determines the size of the slider. The minimum value is 0, the maximum value is the difference between the object width and the frame width.
## 🔒︎ int HScrollStepSize

The step of the horizontal scroller. This step is used to increment the scroll position.
## 🔒︎ int HScrollFrameSize

The width of the currently visible area.
## 🔒︎ int HScrollObjectSize

The width of the whole object that should be scrolled.
## WidgetScrollBox.SCROLL_RENDER_MODE HScrollHidden

The flag indicating if a horizontal scroll bar is hidden, disabled or always rendered. One of the *[SCROLL_RENDER_MODE](#SCROLL_RENDER_MODE)* values.
## bool HScrollEnabled

The value indicating if horizontal scrolling is enabled.
## 🔒︎ WidgetScroll VScroll

The vertical scroller object.
## int VScrollValue

The position (and also the size) of the vertical scroller. That is, it returns the height of the currently invisible area that determines the size of the slider. The minimum value is 0, the maximum value is the difference between the object height and the frame height.
## 🔒︎ int VScrollStepSize

The step of the vertical scroller. This step is used to increment the scroll position.
## 🔒︎ int VScrollFrameSize

The height of the currently visible area.
## 🔒︎ int VScrollObjectSize

The height of the whole object that should be scrolled.
## WidgetScrollBox.SCROLL_RENDER_MODE VScrollHidden

The flag indicating if a vertical scroll bar is hidden, disabled or always rendered. One of the *[SCROLL_RENDER_MODE](#SCROLL_RENDER_MODE)* values.
## bool VScrollEnabled

The value indicating if vertical scrolling is enabled.
## 🔒︎ int ScrollScale

The divisor used to convert integer values into floating point values.
## int Background

The value indicating if the background is rendered.
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
## vec4 VscrollColor

The color used for the widget's vertical scroll.
## vec4 HscrollColor

The color used for the widget's horizontal scroll.
## vec4 BackgroundColor

The background color used for the widget.
## vec4 BorderColor

The border color for the widget.
## 🔒︎ int SpaceY

The vertical space between the widgets in the box and between them and the box border.
## 🔒︎ int SpaceX

The horizontal space between the widgets in the box and between them and the box border.
### Members

---

## WidgetScrollBox ( Gui gui , int x = 0 , int y = 0 )

Constructor. Creates a box with scrolling based on given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new box will belong.
- *int* **x** - Horizontal space between the widgets in the box and between them and the box border. This is an optional parameter.
- *int* **y** - Vertical space between the widgets in the box and between them and the box border. This is an optional parameter.

## WidgetScrollBox ( int x = 0 , int y = 0 )

Constructor. Creates a box with scrolling based on given parameters and adds it to the Engine GUI.
### Arguments

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

- *int* **x** - Horizontal space. If a negative value is specified, 0 will be used instead.
- *int* **y** - Vertical space. If a negative value is specified, 0 will be used instead.
