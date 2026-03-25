# Unigine::WidgetDialogFile Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** WidgetDialog


This class creates dialog window where a file is selected. On the left side file-related information or an image preview is displayed.


## WidgetDialogFile Class

### Members

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

## void setFile ( string file )

Selects a given file in the file picker.
### Arguments

- *string* **file** - Absolute or relative path to the file.

## string getFile ( )

Returns the currently selected file.
### Return value

Path to the file.
## void setFilter ( string filter )

Sets a file name filter, which is used to display files of required types only.
### Arguments

- *string* **filter** - List of file extensions with leading dots and without additional separators, for example: .mesh.smesh.

## string getFilter ( )

Returns the currently used file name filter.
### Return value

List of file extensions with leading dots and without additional separators, for example: .mesh.smesh.
## void setPath ( string path )

Sets a path to the folder, contents of which should be displayed in the file picker.
### Arguments

- *string* **path** - Absolute or relative path.

## string getPath ( )

Returns the current path to the folder, contents of which is displayed in the file picker.
### Return value

Current path.
## void setTabs ( string tabs )

Adds a set of tabs to the file picker dialog. The tabs allow the user to interact with several folders at once.
### Arguments

- *string* **tabs** - List of paths separated with semicolons. Each path corresponds to a tab.

## string getTabs ( )

Returns a list of tabs in the file picker dialog. The tabs allow the user to interact with several folders at once.
### Return value

List of paths separated with semicolons. Each path corresponds to a tab.
