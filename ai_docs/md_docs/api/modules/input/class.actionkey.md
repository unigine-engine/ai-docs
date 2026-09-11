# InputModule::ActionKey Class

**Inherits from:** Action


ActionKey represents a digital (on/off) input action. It tracks button/key states and provides down, pressed, and up events similar to standard input APIs.


The action aggregates input from all its bindings using OR logic - if any binding is pressed, the action is pressed.


State queries: **isDown()** returns true on the first frame when the action becomes pressed, **isPressed()** returns true while the action is held down, **isUp()** returns true on the frame when the action is released, and **getValue()** is the same as isPressed().


### See Also


- **[Action](../../../api/modules/input/class.action.md)**
- **[KeyBind](../../../api/modules/input/class.keybind.md)**
- **[KeySettings](../../../api/modules/input/struct.keysettings.md)**


## InputModule::ActionKey Class

---

## ActionKey ( )

Constructs a key action with the specified name and ID.
### Arguments

## addBinding ( )

Adds a binding with specific key settings.
### Arguments

### Return value

ID of the created binding.
## void setBindingSettings ( )

Updates the settings for an existing binding.
### Arguments

## getValue ( )

Returns whether the action is currently pressed.
### Return value

True if pressed.
## isDown ( )

Returns true on the frame when the action was first pressed.
### Return value

True on first press frame.
## isPressed ( )

Returns true while the action is held down.
### Return value

True while held.
## isUp ( )

Returns true on the frame when the action was released.
### Return value

True on release frame.
