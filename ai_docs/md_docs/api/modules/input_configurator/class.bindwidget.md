# BindWidget Class


BindWidget is the abstract base class for UI widgets that display and edit input bindings. It provides common functionality for showing control names, handling detection mode, and managing the binding lifecycle.


Two presentation modes are available: **ControlName** (shows only the bound control name in compact form) and **Setup** (shows all configuration options in expanded form).


Detection mode allows users to press/move a physical input to automatically assign it to the binding.


### See Also


- **[AxisBindWidget](../../../api/modules/input_configurator/class.axisbindwidget.md)**
- **[KeyBindWidget](../../../api/modules/input_configurator/class.keybindwidget.md)**


## BindWidget Class

---

## BindWidget ( )

Constructs a bind widget for the specified action and binding.
### Arguments

## getWidget ( )

Returns the root widget for adding to the UI hierarchy.
### Return value

The root widget.
## void setPresentMode ( )

Sets the presentation mode for this widget.
### Arguments

## getEventDetectClicked ( )

Returns the event that fires when the detect button is clicked.
### Return value

Reference to the detect clicked event.
## isDetecting ( )

Returns whether this widget is currently in input detection mode.
### Return value

True if in detection mode.
## void startDetect ( )

Starts input detection mode. Abstract method implemented by subclasses.
## void stopDetect ( )

Stops input detection mode.
## void update ( )

Updates the widget state. Call each frame while the configurator is active.
