# Widget Dialog


This article describes the sample located in the `<UnigineSDK>/source/csharp/samples/Api/Widgets/WidgetDialog/` directory. By using the [WidgetDialog](../../../api/library/gui/class.widgetdialog_cpp.md) class you can create dialog windows. The article also explains how to pass user data to a callback.


### See also


- An example can be found in the `<UnigineSDK>/source/csharp/samples/Api/Widgets/WidgetDialog/` directory.
- [WidgetDialog Class API reference](../../../api/library/gui/class.widgetdialog_cpp.md).
- Articles on [UI containers](../../../code/gui/ui/ui_containers.md#dialog) and [UI Widgets](../../../code/gui/ui/ui_widgets.md)


## WidgetDialog Class Usage Example


Let's see how the example works:


```csharp
private WidgetWindow window;
private WidgetButton button_0;
private WidgetButton button_1;
private WidgetButton button_2;
private WidgetButton button_3;

/*
	* Instances for each type of WidgetDialog window
*/
private WidgetDialogMessage dialog_message;
private WidgetDialogFile dialog_file;
private WidgetDialogColor dialog_color;
private WidgetDialogImage dialog_image;

private void Init()
{
	// create the main window
	window = new WidgetWindow("Dialogs", 4, 4);

	// create buttons
	button_0 = new WidgetButton("Message");
	button_0.EventClicked.Connect(() => button_message_clicked("DialogMessage", "Message"));
	window.AddChild(button_0, Gui.ALIGN_EXPAND);

	button_1 = new WidgetButton("File");
	button_1.EventClicked.Connect(() => button_file_clicked("DialogFile", "./"));
	window.AddChild(button_1, Gui.ALIGN_EXPAND);

	button_2 = new WidgetButton("Color");
	button_2.EventClicked.Connect(() => button_color_clicked("DialogColor", new vec4(1.0f)));
	window.AddChild(button_2, Gui.ALIGN_EXPAND);

	button_3 = new WidgetButton("Image");
	button_3.EventClicked.Connect(() => button_image_clicked("DialogImage", "data/widget_dialog.png"));
	window.AddChild(button_3, Gui.ALIGN_EXPAND);

	// arrange window
	window.Arrange();
	Gui.GetCurrent().AddChild(window, Gui.ALIGN_OVERLAP | Gui.ALIGN_CENTER);

}

private void dialog_ok_clicked(WidgetDialog dialog, int type)
{
	Log.Message("{0} ok clicked\n", dialog.Text);
	if (type == 1)
		Log.Message("{0}\n", (dialog as WidgetDialogFile).File);
	if (type == 2)
		Log.Message("{0}\n", (dialog as WidgetDialogColor).WebColor);
	Gui.GetCurrent().RemoveChild(dialog);
}

private void dialog_cancel_clicked(Widget widget, WidgetDialog dialog)
{
	Log.Message("{0} cancel clicked\n", dialog.Text);
	Gui.GetCurrent().RemoveChild(dialog);
}

private void dialog_show(WidgetDialog dialog, int type)
{
	dialog.GetOkButton().EventClicked.Connect(() => dialog_ok_clicked(dialog, type));
	dialog.GetCancelButton().EventClicked.Connect(widget => dialog_cancel_clicked(widget, dialog));
	Gui.GetCurrent().AddChild(dialog, Gui.ALIGN_OVERLAP | Gui.ALIGN_CENTER);
	dialog.SetPermanentFocus();
}

/*
	* Event handlers for buttons
*/
private void button_message_clicked(string str, string message)
{
	dialog_message = new WidgetDialogMessage(Gui.GetCurrent(), str);
	dialog_message.MessageText = message;
	dialog_show(dialog_message, 0);
}

private void button_file_clicked(string str, string path)
{
	dialog_file = new WidgetDialogFile(Gui.GetCurrent(), str);
	dialog_file.Path = path;
	dialog_show(dialog_file, 1);
}

private void button_color_clicked(string str, vec4 color)
{
	dialog_color = new WidgetDialogColor(Gui.GetCurrent(), str);
	dialog_color.Color = color;
	dialog_show(dialog_color, 2);
}

private void button_image_clicked(string str, string name)
{
	dialog_image = new WidgetDialogImage(Gui.GetCurrent(), str);
	dialog_image.Texture = name;
	dialog_show(dialog_image, 3);
}


```


In this sample we do the following:


- Create 4 different *Widget Dialog* windows (all these classes inherit from the *WidgetDialog* class) (*dialog_message, dialog_file, dialog_color, dialog_image*).
- In the *Init()* method, create the main window and add 4 buttons to it.
- Set a callback for each button, which is executed when the button is clicked (*button_message_clicked(), button_file_clicked(), button_color_clicked(), button_image_clicked()*).
- To display the dialog, create the *dialog_show()* method which receives a *WidgetDialog* object and an integer variable called **type** (from 0 to 3) as arguments.
- In the *dialog_show()* method we set callbacks for *Ok* and *Cancel* buttons and pass the integer variable called **type** as user data to the callback to handle specific window. Callbacks *dialog_ok_clicked()* and *dialog_cancel_clicked()* receive the type variable as an argument. According to the value of the variable the specified method is performed.


### Output


As you run the application, you'll see the following:


![](widget_dialog_output.png)
