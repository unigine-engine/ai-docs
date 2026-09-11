# Unigine::Widgets

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Unigine::Widgets are user classes that allow to code user interface only once and use them for both internal GUI (in-app) and external one (rendered in separate windows):


- If the Unigine-based application is run without the Interface plugin, widgets will be created inside the window, in the same way as default GUI is usually rendered.
- If the Interface plugin is loaded on the application start-up (via [`extern_plugin`](../../../../../code/command_line.md#extern_plugin) console command), widgets will be automatically created in separate windows in addition to the main application window.


## Available Widgets


Unigine::Widgets act identical to [UnigineScript widgets](../../../../../api/library/gui/index.md) and support completely the same interface:


- **Unigine::Widgets::Button** � the same as [WidgetButton](../../../../../api/library/gui/class.widgetbutton_cpp.md)
- **Unigine::Widgets::Canvas** � the same as [WidgetCanvas](../../../../../api/library/gui/class.widgetcanvas_cpp.md)
- **Unigine::Widgets::CheckBox** � the same as [WidgetCheckBox](../../../../../api/library/gui/class.widgetcheckbox_cpp.md)
- **Unigine::Widgets::ComboBox** � the same as [WidgetComboBox](../../../../../api/library/gui/class.widgetcombobox_cpp.md)
- **Unigine::Widgets::Dialog** � the same as [WidgetDialog](../../../../../api/library/gui/class.widgetdialog_cpp.md)
- **Unigine::Widgets::DialogColor** � the same as [WidgetDialogColor](../../../../../api/library/gui/class.widgetdialogcolor_cpp.md)
- **Unigine::Widgets::DialogFile** � the same as [WidgetDialogFile](../../../../../api/library/gui/class.widgetdialogfile_cpp.md)
- **Unigine::Widgets::DialogImage** � the same as [WidgetDialogImage](../../../../../api/library/gui/class.widgetdialogimage_cpp.md)
- **Unigine::Widgets::DialogMessage** � the same as [WidgetDialogMessage](../../../../../api/library/gui/class.widgetdialogmessage_cpp.md)
- **Unigine::Widgets::EditLine** � the same as [WidgetEditLine](../../../../../api/library/gui/class.widgeteditline_cpp.md)
- **Unigine::Widgets::EditText** � the same as [WidgetEditText](../../../../../api/library/gui/class.widgetedittext_cpp.md)
- **Unigine::Widgets::GridBox** � the same as [WidgetGridBox](../../../../../api/library/gui/class.widgetgridbox_cpp.md)
- **Unigine::Widgets::GroupBox** � the same as [WidgetGroupBox](../../../../../api/library/gui/class.widgetgroupbox_cpp.md)
- **Unigine::Widgets::HBox** � the same as [WidgetHBox](../../../../../api/library/gui/class.widgethbox_cpp.md)
- **Unigine::Widgets::HPaned** � the same as [WidgetHPaned](../../../../../api/library/gui/class.widgethpaned_cpp.md)
- **Unigine::Widgets::Icon** � the same as [WidgetIcon](../../../../../api/library/gui/class.widgeticon_cpp.md)
- **Unigine::Widgets::Label** � the same as [WidgetLabel](../../../../../api/library/gui/class.widgetlabel_cpp.md)
- **Unigine::Widgets::ListBox** � the same as [WidgetListBox](../../../../../api/library/gui/class.widgetlistbox_cpp.md)
- **Unigine::Widgets::ScrollBox** � the same as [WidgetScrollBox](../../../../../api/library/gui/class.widgetscrollbox_cpp.md)
- **Unigine::Widgets::Slider** � the same as [WidgetSlider](../../../../../api/library/gui/class.widgetslider_cpp.md)
- **Unigine::Widgets::Spacer** � the same as [WidgetSpacer](../../../../../api/library/gui/class.widgetspacer_cpp.md)
- **Unigine::Widgets::Sprite** � the same as [WidgetSprite](../../../../../api/library/gui/class.widgetsprite_cpp.md)
- **Unigine::Widgets::TabBox** � the same as [WidgetTabBox](../../../../../api/library/gui/class.widgettabbox_cpp.md)
- **Unigine::Widgets::TreeBox** � the same as [WidgetTreeBox](../../../../../api/library/gui/class.widgettreebox_cpp.md)
- **Unigine::Widgets::VBox** � the same as [WidgetVBox](../../../../../api/library/gui/class.widgetvbox_cpp.md)
- **Unigine::Widgets::VPaned** � the same as [WidgetVPaned](../../../../../api/library/gui/class.widgetvpaned_cpp.md)
- **Unigine::Widgets::Window** � the same as [WidgetWindow](../../../../../api/library/gui/class.widgetwindow_cpp.md)


Also, there are three additional widgets available:


- **Unigine::Widgets::DockBox** � a widget that can be dragged and docked inside a window.
- **Unigine::Widgets::Graph** � a widget to create flow graphs.
- **Unigine::Widgets::MdiBox** � a widget to create multiple windows inside other windows


## How to Use Unigine::Widgets Widgets


1. Include the necessary headers for widgets you are going to create in your script: ```cpp #include <core/systems/widgets/widget.h> #include <core/systems/widgets/widget_window.h> ```
2. Create a widget: ```cpp int init() { // You can declare the namespace for convenience using Unigine::Widgets; // Create Unigine::Widgets::Window Window window = new Window("Unigine::Widgets::Window"); // Add the widget to the rendered GUI addChild(window,ALIGN_OVERLAP | ALIGN_CENTER); return 1; } ``` When the application is run, either internal WidgetWindow or external InterfaceWidgetWindow will be automatically created depending on whether the Interface plugin is used or not.
