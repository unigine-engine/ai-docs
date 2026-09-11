# Unigine::WidgetDialogFile Class (CS)

**Inherits from:** WidgetDialog


This class creates dialog window where a file is selected. On the left side file-related information or an image preview is displayed.


### Example


The following *C# component* illustrates how to create a file selection dialog widget and use it to select files.


<details>
<summary>CFileDialog.cs | Close</summary>

`CFileDialog.cs`


```csharp
// widgets to be used and callback functions for them
WidgetLabel file_name;
WidgetButton open_button;
WidgetDialogFile file_dialog;
// callback to be fired on clicking the button displaying the file dialog
void on_button_clicked()
{
	// resetting file sepection, showing the dialog and setting permanent focus to it
	file_dialog.File = "";
	file_dialog.Hidden = false;
	file_dialog.SetPermanentFocus();
}

// callback to be fired on clicking the Ok button of the file dialog
void dialog_ok_clicked()
{
	// getting the current path selection fron the dialog and checking if the file exists
	string path = file_dialog.File;
	if(!FileSystem.IsFileExist(path))
		return;

	// if the file exists hiding the dialog, displaying the selected file on the "file_name" label and removing focus
	file_dialog.Hidden = true;
	file_name.Text = path;
	file_dialog.RemoveFocus();
}

// callback to be fired on clicking the Cancel button of the file dialog
void dialog_cancel_clicked()
{
	file_dialog.Hidden = true;
	file_dialog.RemoveFocus();
}

EventConnections connections = new EventConnections();

void Init()
{
	// getting a pointer to the system GUI
	Gui gui = Gui.GetCurrent();

	// creating a label widget to display the file selected via the dialog
	file_name = new WidgetLabel(gui, "No file selected yet");
	gui.AddChild(file_name, Gui.ALIGN_TOP | Gui.ALIGN_BACKGROUND);

	// creating a button widget to display the file dialog
	open_button = new WidgetButton(gui, "Select an image file on disk");
	gui.AddChild(open_button, Gui.ALIGN_TOP | Gui.ALIGN_BACKGROUND);

	// setting "on_button_clicked" function to handle CLICKED event for the button
	open_button.EventClicked.Connect(connections, on_button_clicked);

	// creating a file dialog widget and setting its caption, default path and file extensions filter to display only *.png and *.jpeg files
	file_dialog = new WidgetDialogFile(gui, "File open dialog");
	file_dialog.Path = "./";
	file_dialog.Filter = ".png.jpeg";

	// setting "dialog_ok_clicked" function to handle CLICKED event for dialog Ok button
	file_dialog.GetOkButton().EventClicked.Connect(connections, dialog_ok_clicked);

	// setting "dialog_cancel_clicked" function to handle CLICKED event for dialog Cancel button
	file_dialog.GetCancelButton().EventClicked.Connect(connections,dialog_cancel_clicked);

	// adding the created file dialog widget to the system GUI and hiding it
	file_dialog.Hidden = true;
	gui.AddChild(file_dialog, Gui.ALIGN_OVERLAP | Gui.ALIGN_CENTER);

}


```

</details>


## WidgetDialogFile Class

### Properties

## string Filter

The file name filter used in the dialog (a list of file extensions with leading dots and without additional separators, for example: .mesh.smesh).
## string Tabs

The list of tabs in the file picker dialog. The tabs allow the user to interact with several folders at once. The value is a list of paths separated with semicolons, where each path corresponds to a tab.
## string File

The file selected in the dialog (an absolute or relative path to the file).
## string Path

The path to the folder whose contents are displayed in the file picker (an absolute or relative path).
### Members

---

## WidgetDialogFile ( Gui gui , string str = 0 )

Constructor. Creates a file picker dialog with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_cs.md)* **gui** - [GUI](../../../api/library/gui/class.gui_cs.md), to which the dialog will belong.
- *string* **str** - Dialog title. This is an optional parameter.

## WidgetDialogFile ( string str = 0 )

Constructor. Creates a file picker dialog with given parameters and adds it to the Engine GUI.
### Arguments

- *string* **str** - Dialog title. This is an optional parameter.
