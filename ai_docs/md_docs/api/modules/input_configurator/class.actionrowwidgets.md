# ActionRowWidgets Class


ActionRowWidgets manages a single row in the input configurator, representing one action with all its bindings across different device types (keyboard, joystick, gamepad).


Each row contains an action name label, a keyboard bindings column with add button, a joystick bindings column with add button, and a gamepad bindings column with add button.


The row automatically creates **[BindWidget](../../../api/modules/input_configurator/class.bindwidget.md)** instances for each binding and updates when bindings are added or removed from the action.


### See Also


- **[WidgetInputConfigurator](../../../api/modules/input_configurator/class.widgetinputconfigurator.md)**
- **[BindWidget](../../../api/modules/input_configurator/class.bindwidget.md)**


## ActionRowWidgets Class

---

## ActionRowWidgets ( )

Constructs an action row for the specified action.
### Arguments

## void setColor ( )

Sets the background color of this row.
### Arguments

## void setPresentMode ( )

Sets the presentation mode for all bindings in this row.
### Arguments

## getEventDetectClicked ( )

Returns the event that fires when any binding starts detection.
### Return value

Reference to the detect clicked event.
## isDetecting ( )

Returns whether any binding in this row is in detection mode.
### Return value

True if any binding is detecting.
## void startDetect ( )

Starts detection on the pending binding.
## void stopDetect ( )

Stops detection on all bindings in this row.
## void update ( )

Updates all bindings in this row.
