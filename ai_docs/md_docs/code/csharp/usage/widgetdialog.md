# Widget Dialog


This article describes the sample located in in **C# Component Samples** (sample ). By using the [WidgetDialog](../../../api/library/gui/class.widgetdialog_cpp.md) class you can create dialog windows. The article also explains how to pass user data to an event handler.


### See also


- An example can be found in **C# Component Samples**: sample .
- [WidgetDialog Class API reference](../../../api/library/gui/class.widgetdialog_cpp.md).
- Articles on [UI containers](../../../code/gui/ui/ui_containers.md#dialog) and [UI Widgets](../../../code/gui/ui/ui_widgets.md)


## WidgetDialog Class Usage Example


Let's see how the example works:


```csharp
using System.Collections;
using System.Collections.Generic;
using Unigine;

// UI sample showcasing various dialog widget types.
public partial class Dialog : Component
{
	// Image asset for the image dialog demonstration
	public AssetLink image;

	private WidgetWindow window;

	// Creates a window with buttons to launch different dialog types.
	void Init()
	{
		Gui gui = Gui.GetCurrent();

		window = new WidgetWindow(gui, "Dialogs", 4, 4);
		window.Flags = Gui.ALIGN_OVERLAP | Gui.ALIGN_CENTER;

		// Simple message dialog - displays text with OK/Cancel
		var button_0 = new WidgetButton(gui, "Message");
		button_0.Flags = Gui.ALIGN_EXPAND;
		button_0.EventClicked.Connect(() => button_message_clicked("DialogMessage", "Message"));
		window.AddChild(button_0);

		// File browser dialog - lets user select files/directories
		var button_1 = new WidgetButton(gui, "File");
		button_1.Flags = Gui.ALIGN_EXPAND;
		button_1.EventClicked.Connect(() => button_file_clicked("DialogFile", "./"));
		window.AddChild(button_1);

		// Color picker dialog - interactive color selection
		var button_2 = new WidgetButton(gui, "Color");
		button_2.Flags = Gui.ALIGN_EXPAND;
		button_2.EventClicked.Connect(() => button_color_clicked("DialogColor", new vec4(1.0f)));
		window.AddChild(button_2);

		// Image viewer dialog - displays a texture
		if (image.Path.Length > 0)
		{
			var button_3 = new WidgetButton(gui, "Image");
			button_3.Flags = Gui.ALIGN_EXPAND;
			button_3.EventClicked.Connect(() => button_image_clicked("DialogImage", image.Path));
			window.AddChild(button_3);
		}
		else
			Log.Warning("Dialogs.Init(): image parameter not specified.");

		window.Arrange();
		gui.AddChild(window);

		// Enable on-screen console to see dialog result logs
		Console.Onscreen = true;
	}

	void Shutdown()
	{
		window.DeleteLater();

		Console.Onscreen = false;
	}

	// Handles OK button click - logs result and extracts dialog-specific data.
	private void dialog_ok_clicked(WidgetDialog dialog, int type)
	{
		Log.Message("{0} ok clicked\n", dialog.Text);
		// Log file path for file dialog
		if (type == 1)
			Log.Message("{0}\n", (dialog as WidgetDialogFile).File);
		// Log web color format for color dialog
		if (type == 2)
			Log.Message("{0}\n", (dialog as WidgetDialogColor).WebColor);
		Gui.GetCurrent().RemoveChild(dialog);
	}

	// Handles Cancel button click - just removes the dialog.
	private void dialog_cancel_clicked(Widget widget, WidgetDialog dialog)
	{
		Log.Message("{0} cancel clicked\n", dialog.Text);
		Gui.GetCurrent().RemoveChild(dialog);
	}

	// Wires up OK/Cancel events and displays the dialog centered on screen.
	private void dialog_show(WidgetDialog dialog, int type)
	{
		dialog.GetOkButton().EventClicked.Connect(() => dialog_ok_clicked(dialog, type));
		dialog.GetCancelButton().EventClicked.Connect(widget => dialog_cancel_clicked(widget, dialog));
		Gui.GetCurrent().AddChild(dialog, Gui.ALIGN_OVERLAP | Gui.ALIGN_CENTER);
		dialog.SetPermanentFocus();
	}

	// Creates and shows a simple message dialog.
	private void button_message_clicked(string str, string message)
	{
		var dialog_message = new WidgetDialogMessage(Gui.GetCurrent(), str);
		dialog_message.MessageText = message;
		dialog_show(dialog_message, 0);
	}

	// Creates and shows a file browser dialog.
	private void button_file_clicked(string str, string path)
	{
		var dialog_file = new WidgetDialogFile(Gui.GetCurrent(), str);
		dialog_file.Path = path;
		dialog_show(dialog_file, 1);
	}

	// Creates and shows a color picker dialog.
	private void button_color_clicked(string str, vec4 color)
	{
		var dialog_color = new WidgetDialogColor(Gui.GetCurrent(), str);
		dialog_color.Color = color;
		dialog_show(dialog_color, 2);
	}

	// Creates and shows an image viewer dialog.
	private void button_image_clicked(string str, string name)
	{
		var dialog_image = new WidgetDialogImage(Gui.GetCurrent(), str);
		dialog_image.Texture = name;
		dialog_show(dialog_image, 3);
	}
}


```


In this sample we do the following:


- Create 4 different *Widget Dialog* windows (all these classes inherit from the *WidgetDialog* class) (*dialog_message, dialog_file, dialog_color, dialog_image*).
- In the *Init()* method, create the main window and add 4 buttons to it.
- Set an event handler for each button, which is executed when the button is clicked (*button_message_clicked(), button_file_clicked(), button_color_clicked(), button_image_clicked()*).
- To display the dialog, create the *dialog_show()* method which receives a *WidgetDialog* object and an integer variable called **type** (from 0 to 3) as arguments.
- In the *dialog_show()* method we process events for *Ok* and *Cancel* buttons and pass the integer variable called **type** as user data to the handler to handle specific window. Event handlers *dialog_ok_clicked()* and *dialog_cancel_clicked()* receive the type variable as an argument. According to the value of the variable the specified method is performed.


### Output


As you run the application, you'll see the following:


![](widget_dialog_output.png)
