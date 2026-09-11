# Unigine::WidgetDialogFile Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WidgetDialog


This class creates dialog window where a file is selected. On the left side file-related information or an image preview is displayed.


## WidgetDialogFile Class

### Members

## void setFilter ( string filter )

Sets a new file name filter used in the dialog (a list of file extensions with leading dots and without additional separators, for example: .mesh.smesh).
### Arguments

- *string* **filter** - The file name filter used in the dialog

## const char * getFilter () const

Returns the current file name filter used in the dialog (a list of file extensions with leading dots and without additional separators, for example: .mesh.smesh).
### Return value

Current file name filter used in the dialog
## void setTabs ( string tabs )

Sets a new list of tabs in the file picker dialog. The tabs allow the user to interact with several folders at once. The value is a list of paths separated with semicolons, where each path corresponds to a tab.
### Arguments

- *string* **tabs** - The list of tabs in the file picker dialog

## const char * getTabs () const

Returns the current list of tabs in the file picker dialog. The tabs allow the user to interact with several folders at once. The value is a list of paths separated with semicolons, where each path corresponds to a tab.
### Return value

Current list of tabs in the file picker dialog
## void setFile ( string file )

Sets a new file selected in the dialog (an absolute or relative path to the file).
### Arguments

- *string* **file** - The file selected in the dialog

## const char * getFile () const

Returns the current file selected in the dialog (an absolute or relative path to the file).
### Return value

Current file selected in the dialog
## void setPath ( string path )

Sets a new path to the folder whose contents are displayed in the file picker (an absolute or relative path).
### Arguments

- *string* **path** - The path to the folder whose contents are displayed in the file picker

## const char * getPath () const

Returns the current path to the folder whose contents are displayed in the file picker (an absolute or relative path).
### Return value

Current path to the folder whose contents are displayed in the file picker
---

## static WidgetDialogFile ( Gui gui , string str = 0 )

Constructor. Creates a file picker dialog with given parameters and adds it to the specified GUI.
### Arguments

- *[Gui](../../../api/library/gui/class.gui_usc.md)* **gui** - [GUI](../../../api/library/gui/class.gui_usc.md), to which the dialog will belong.
- *string* **str** - Dialog title. This is an optional parameter.

## static WidgetDialogFile ( string str = 0 )

Constructor. Creates a file picker dialog with given parameters and adds it to the Engine GUI.
### Arguments

- *string* **str** - Dialog title. This is an optional parameter.
