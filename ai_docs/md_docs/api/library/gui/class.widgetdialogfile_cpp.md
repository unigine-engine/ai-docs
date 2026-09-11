# Unigine::WidgetDialogFile Class (CPP)

**Header:** #include <UnigineWidgets.h>

**Inherits from:** WidgetDialog


This class creates dialog window where a file is selected. On the left side file-related information or an image preview is displayed.


### Example


The following code illustrates how to create a file selection dialog widget and use it to select files. Add the code below to the corresponding files of your project (`AppWorldLogic.h` and `AppWorldLogic.cpp`).


<details>
<summary>AppWorldLogic.h | Close</summary>

`AppWorldLogic.h`


```cpp
class AppWorldLogic : public Unigine::WorldLogic
{

	// ... //

private:
	// declaring widgets to be used and callback functions for them
	Unigine::WidgetLabelPtr file_name;
	Unigine::WidgetButtonPtr open_button;
	Unigine::WidgetDialogFilePtr file_dialog;
	void on_button_clicked(const Unigine::WidgetPtr & widget,  int mouse_buttons);
	void dialog_ok_clicked();
	void dialog_cancel_clicked();

	Unigine::EventConnections connection;
};


```

</details>


<details>
<summary>AppWorldLogic.cpp | Close</summary>

`AppWorldLogic.cpp`


```cpp
#include "AppWorldLogic.h"
#include <UnigineFileSystem.h>

using namespace Unigine;

// callback to be fired on clicking the button displaying the file dialog
void AppWorldLogic::on_button_clicked(const WidgetPtr & widget, int mouse_buttons)
{
	// resetting file selection, showing the dialog and setting permanent focus to it
	file_dialog->setFile("");
	file_dialog->setHidden(0);
	file_dialog->setPermanentFocus();
}

// callback to be fired on clicking the Ok button of the file dialog
void AppWorldLogic::dialog_ok_clicked()
{
	// getting the current path selection fron the dialog and checking if the file exists
	String path = file_dialog->getFile();
	if (!FileSystem::isFileExist(path))
		return;

	// if the file exists hiding the dialog, displaying the selected file on the "file_name" label and removing focus
	file_dialog->setHidden(1);
	file_name->setText(path);
	file_dialog->removeFocus();
}

// callback to be fired on clicking the Cancel button of the file dialog
void AppWorldLogic::dialog_cancel_clicked()
{
	file_dialog->setHidden(1);
	file_dialog->removeFocus();
}

int AppWorldLogic::init()
{
	// getting a pointer to the system GUI
	GuiPtr gui = Gui::getCurrent();

	// creating a label widget to display the file selected via the dialog
	file_name = WidgetLabel::create(gui, "No file selected yet");
	gui->addChild(file_name, Gui::ALIGN_TOP | Gui::ALIGN_BACKGROUND);

	// creating a button widget to display the file dialog
	open_button = WidgetButton::create(gui, "Select an image file on disk");
	gui->addChild(open_button, Gui::ALIGN_TOP | Gui::ALIGN_BACKGROUND);


	// setting "on_button_clicked" function to handle CLICKED event for the button
	open_button->getEventClicked().connect(connection, this, &AppWorldLogic::on_button_clicked);

	// creating a file dialog widget and setting its caption, default path and file extensions filter to display only *.png and *.jpeg files
	file_dialog = WidgetDialogFile::create(gui, "File open dialog");
	file_dialog->setPath("./");
	file_dialog->setFilter(".png.jpeg");

	// setting "dialog_ok_clicked" function to handle CLICKED event for dialog Ok button
	file_dialog->getOkButton()->getEventClicked().connect(connection, this, &AppWorldLogic::dialog_ok_clicked);

	// setting "dialog_cancel_clicked" function to handle CLICKED event for dialog Cancel button
	file_dialog->getCancelButton()->getEventClicked().connect(connection, this, &AppWorldLogic::dialog_cancel_clicked);

	// adding the created file dialog widget to the system GUI and hiding it
	file_dialog->setHidden(1);
	gui->addChild(file_dialog, Gui::ALIGN_OVERLAP | Gui::ALIGN_CENTER);

	return 1;
}


```

</details>


## WidgetDialogFile Class

### Members

## void setFilter ( const char * filter )

Sets a new file name filter used in the dialog (a list of file extensions with leading dots and without additional separators, for example: .mesh.smesh).
### Arguments

- *const char ** **filter** - The file name filter used in the dialog

## const char * getFilter () const

Returns the current file name filter used in the dialog (a list of file extensions with leading dots and without additional separators, for example: .mesh.smesh).
### Return value

Current file name filter used in the dialog
## void setTabs ( const char * tabs )

Sets a new list of tabs in the file picker dialog. The tabs allow the user to interact with several folders at once. The value is a list of paths separated with semicolons, where each path corresponds to a tab.
### Arguments

- *const char ** **tabs** - The list of tabs in the file picker dialog

## const char * getTabs () const

Returns the current list of tabs in the file picker dialog. The tabs allow the user to interact with several folders at once. The value is a list of paths separated with semicolons, where each path corresponds to a tab.
### Return value

Current list of tabs in the file picker dialog
## void setFile ( const char * file )

Sets a new file selected in the dialog (an absolute or relative path to the file).
### Arguments

- *const char ** **file** - The file selected in the dialog

## const char * getFile () const

Returns the current file selected in the dialog (an absolute or relative path to the file).
### Return value

Current file selected in the dialog
## void setPath ( const char * path )

Sets a new path to the folder whose contents are displayed in the file picker (an absolute or relative path).
### Arguments

- *const char ** **path** - The path to the folder whose contents are displayed in the file picker

## const char * getPath () const

Returns the current path to the folder whose contents are displayed in the file picker (an absolute or relative path).
### Return value

Current path to the folder whose contents are displayed in the file picker
---

## static WidgetDialogFilePtr create ( const Ptr < Gui > & gui , const char * str = 0 )

Constructor. Creates a file picker dialog with given parameters and adds it to the specified GUI.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Gui](../../../api/library/gui/class.gui_cpp.md)> &* **gui** - [GUI](../../../api/library/gui/class.gui_cpp.md), to which the dialog will belong.
- *const char ** **str** - Dialog title. This is an optional parameter.

## static WidgetDialogFilePtr create ( const char * str = 0 )

Constructor. Creates a file picker dialog with given parameters and adds it to the Engine GUI.
### Arguments

- *const char ** **str** - Dialog title. This is an optional parameter.
