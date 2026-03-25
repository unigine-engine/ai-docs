# GUI


The current article describes the native GUI, which includes the following:


- [UI Files](../../code/gui/ui/index.md)
- [RC files](../../code/gui/rc.md)
- [Skin layout](../../code/gui/skin/index.md)


## General info


Unigine provides flexible Graphic User Interface (GUI), its main features are:


- Various widgets and containers
- Dialog windows
- 3D effects
- Activation animation
- Easy skin changing
- UI files in XML format
- Localization support
- True Type fonts support
- Unicode (UTF8) support
- IME input support


## How to Create GUI Layout


There are 2 ways to create the GUI layout:


- Directly from a script via [GUI-related classes](../../api/library/gui/index.md)
- By using [User interface](../../code/gui/ui/index.md) (UI) files


### By Scripting


To create widgets directly from a script, perform the following steps:


1. Declare all of the widgets as global variables in the script.
2. Create the corresponding object for each widget.
3. Define necessary properties for each object (height, width, etc.) by using functions of the corresponding [GUI-related classes](../../api/library/gui/index.md).
4. Add root widgets to be rendered in the GUI interface via *[Gui::addChild()](../../api/library/gui/class.gui_cpp.md#addChild_Widget_int_void)*.
5. Add children of the root widgets to be rendered in the GUI interface via *[Gui::addChild()](../../api/library/gui/class.gui_cpp.md#addChild_Widget_int_void)*.


### By Using UI files


To create widgets and describe the layout by using [User interface](../../code/gui/ui/index.md) (UI) files, perform the following:


1. Create `*.ui` file that describes what widgets should be drawn and how they are laid out (see [more details](../../code/gui/ui/index.md)).
2. Declare root widgets (or containers) as global variables in the script.
3. Load User interface by using the [*UserInterface()*](../../api/library/gui/class.userinterface_cpp.md#UserInterface_constPtrGui_constchar_constchar) constructor.
4. Add root widgets to be rendered in the GUI interface via *[Gui::addChild()](../../api/library/gui/class.gui_cpp.md#addChild_Widget_int_void)*.


This is faster and more convenient way to create a GUI.


## How to Create Custom GUI Skin


1. Create all required GUI textures (see details on [Skin Layout](../../code/gui/skin/index.md)).
2. If necessary, create [Resource file](../../code/gui/rc.md) (RC) where global settings for GUI interface are described.
3. Use custom skin:

  - If you need to change the system GUI skin (2D GUI), replace files under `data/core/gui` folder.
  - If [ObjectGui](../../api/library/objects/class.objectgui_cpp.md) or [ObjectGuiMesh](../../api/library/objects/class.objectguimesh_cpp.md) (that is, monitors positioned in the world) is used, specify a folder with all textures, RC file and the default font in the constructor.
