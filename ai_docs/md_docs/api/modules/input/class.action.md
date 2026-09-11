# InputModule::Action Class


Action is the abstract base class for named input actions. Actions decouple game logic from specific input devices - your code queries "Jump" rather than "Space key".


Each action can have multiple bindings, allowing the same action to be triggered by different inputs (e.g., both keyboard and gamepad). The action aggregates input from all its bindings.


Two concrete action types are provided: **[ActionKey](../../../api/modules/input/class.actionkey.md)** for digital inputs (pressed/released) and **[ActionAxis](../../../api/modules/input/class.actionaxis.md)** for analog inputs (continuous values).


### See Also


- **[ActionKey](../../../api/modules/input/class.actionkey.md)**
- **[ActionAxis](../../../api/modules/input/class.actionaxis.md)**
- **[Bind](../../../api/modules/input/class.bind.md)**


## InputModule::Action Class

---

## addBinding ( )

Adds a new binding to this action for the specified device type.
### Arguments

### Return value

ID of the created binding.
## void removeBinding ( )

Removes a binding by ID.
### Arguments

## getBinding ( )

Returns a binding by ID.
### Arguments

### Return value

The binding, or nullptr if not found.
## getBindingByIndex ( )

Returns a binding by its index in the internal array.
### Arguments

### Return value

The binding.
## getNumBindings ( )

Returns the number of bindings attached to this action.
### Return value

Number of bindings.
## void clearBindings ( )

Removes all bindings from this action.
## void clearBindingsByDeviceType ( )

Removes all bindings of a specific device type.
### Arguments

## void setEnable ( )

Enables or disables this action.
### Arguments

## isEnable ( )

Returns whether this action is enabled.
### Return value

True if enabled.
## getType ( )

Returns the type of this action.
### Return value

The action type (KEY or AXIS).
## getID ( )

Returns the unique ID of this action.
### Return value

The action ID.
## getName ( )

Returns the name of this action.
### Return value

The action name.
## void update ( )

Updates the action state from all bindings.
