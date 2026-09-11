# Unigine::WidgetButton Class (CS)

**Inherits from:** Widget


Interface for widget button handling.


The object of this class looks as follows:


![](../../../code/gui/ui/widgets/button.png)


Here is an example of two buttons. Button1 has a background and image, Button2 is without them:


![](../../../code/gui/ui/examples/button.png)


> **Notice:** The button is automatically stretched or shrinked to match the size of the current texture/image. When you resize the button the size of the image does not change. In case you need to create a type of button widget with an auto-adjusted image size, or image rotation, please consider *[Widget Sprite](../../../api/library/gui/class.widgetsprite_cs.md)* instead.


#### See Also


- C++ sample
- C# Component sample
- UnigineScript sample


### Example


The following code illustrates how to create a button widget and set its parameters.


```csharp
/* .. */

// event handler function
void OnButtonClicked()
{
	/* .. */

	return;
}

/* .. */
 public override bool Init()
{
	// getting a pointer to the system GUI
	Gui gui = Gui.GetCurrent();

	// creating a button widget and setting its caption
	WidgetButton widget_button = new WidgetButton(gui, "Delete");

	// setting a tooltip
	widget_button.SetToolTip("Delete object(s)");

	// rearranging button size
	widget_button.Arrange();

	// setting button position
	widget_button.SetPosition(10, 10);

	// setting onButtonClicked function to handle CLICKED event
	widget_button.EventClicked.Connect(OnButtonClicked);

	// adding created button widget to the system GUI
	gui.AddChild(widget_button, Gui.ALIGN_OVERLAP | Gui.ALIGN_FIXED);
}

```


## WidgetButton Class

### Properties

## string StyleTexture

The path to the button skin texture.
## string Text

The button text label.
## int TextAlign

The alignment of the button label. One of the [GUI_ALIGN_*](../../../api/library/gui/class.gui_cs.md) variables.
## string Texture

The path to the button image texture.
> **Notice:** The button is automatically stretched or shrinked to match the size of the current texture. When you resize the button the size of the image does not change. In case you need to create a type of button widget with an auto-adjusted image size, or image rotation, please consider *[Widget Sprite](../../../api/library/gui/class.widgetsprite_cs.md)* instead.

## vec4 ButtonColor

The color for the button.
## bool Toggled

The value indicating if the toggle button is pressed.
## bool Toggleable

The value indicating if the button is a toggle button or a simple one. The default is 0.
## int Background

The value indicating if a background texture is rendered for the button. The default is 1.
### Members

---

## WidgetButton ( Gui gui , string str = 0 )

Constructor. Creates a button with a given label and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the new button will belong.
- *string* **str** - Button label. This is an optional parameter.

## WidgetButton ( string str = 0 )

Constructor. Creates a button with a given label and adds it to the Engine GUI.
### Arguments

- *string* **str** - Button label. This is an optional parameter.

## void SetImage ( Image image )

Sets a new image for the button.
> **Notice:** The button is automatically stretched or shrinked to match the size of the current image. When you resize the button the size of the image does not change. In case you need to create a type of button widget with an auto-adjusted image size, or image rotation, please consider *[Widget Sprite](../../../api/library/gui/class.widgetsprite_cs.md)* instead.

### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to set.

## Image GetImage ( )

Returns the current button image.
> **Notice:** The button is automatically stretched or shrinked to match the size of the current image. When you resize the button the size of the image does not change. In case you need to create a type of button widget with an auto-adjusted image size, or image rotation, please consider *[Widget Sprite](../../../api/library/gui/class.widgetsprite_cs.md)* instead.

### Return value

Button image.
## void SetStyleImage ( Image image )

Sets a button skin image.
### Arguments

- *[Image](../../../api/library/common/class.image_cs.md)* **image** - Image to set.

## Image GetStyleImage ( )

Returns the button skin image.
### Return value

Button skin image.
