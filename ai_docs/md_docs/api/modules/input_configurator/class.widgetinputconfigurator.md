# WidgetInputConfigurator Component

**Inherits from:** ComponentBase


WidgetInputConfigurator provides a complete UI for configuring input bindings at runtime. It displays all actions from the InputModule system and allows users to add, remove, and modify bindings for keyboard, joystick, and gamepad devices.


The configurator creates a window with a context selector to switch between different input contexts, an action list showing all actions in the selected context, binding columns providing separate columns for keyboard, joystick, and gamepad bindings, add/remove controls with buttons to add new bindings or remove existing ones, detection mode to click and detect physical inputs, and save/load to persist configuration to **XML** files.


Two presentation modes are available: Control Name (compact view showing just the bound control names) and Setup (expanded view with all configuration options like dead zones, sensitivity, etc.).


To use the configurator, add the component to a node. The widget will automatically display and update based on the InputManager state.


### See Also


- **[ActionRowWidgets](../../../api/modules/input_configurator/class.actionrowwidgets.md)**
- **[BindWidget](../../../api/modules/input_configurator/class.bindwidget.md)**
- **[InputManager](../../../api/modules/input/class.inputmanager.md)**


## WidgetInputConfigurator Class

---

## void setColumnWidths ( )

Sets the column widths for the configurator layout.
### Arguments
