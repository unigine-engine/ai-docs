# User Interfaces for Unigine::Widgets

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


You can use [user interface files](../../../../../code/gui/ui/index.md) (*.ui) to describe how widgets are laid out. Such UI files are created manually in [Unigine UI syntax](../../../../../code/gui/ui/index.md#syntax). They are handled by using **Unigine::Widgets::UserInterface** class.


## How to Load Unigine UI


To load a Unigine-native user interface file, take the following steps:


1. Include the UserInterface header. All other Unigine::Widgets headers are already included in it. ```cpp #include <core/systems/widgets/widget_interface.h> ```
2. Declare UserInterface and the root widgets from the UI file in the global scope. ```cpp #include <core/systems/widgets/widget_interface.h> Unigine::Widgets::UserInterface ui; Unigine::Widgets::Window window; ```
3. Load the user interface file. You also need to add root widgets to the rendered GUI for them to become visible. ```cpp int init() { // You can declare the namespace for convenience using Unigine::Widgets; // Load UI file in Unigine syntax ui = new UserInterface("samples/systems/widgets/widgets_01.ui"); // Render the root widget addChild(window,ALIGN_OVERLAP | ALIGN_CENTER); return 1; } int shutdown() { // Delete UserInterface with all widgets loaded from it delete ui; return 1; } ```
