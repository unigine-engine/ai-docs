# InputModule::Context Class


Context groups related input actions together and allows enabling/disabling them as a set. This is useful for different game states where different controls are active.


Common use cases include a Menu context for UI navigation, selection, and back; a Gameplay context for movement, camera, and actions; a Vehicle context for throttle, steering, and weapons; and a Pause context for resume and quit.


When a context is disabled, its actions stop updating and return default values. This prevents input conflicts between different game states.


### See Also


- **[InputManager](../../../api/modules/input/class.inputmanager.md)**
- **[Action](../../../api/modules/input/class.action.md)**
- **[ActionKey](../../../api/modules/input/class.actionkey.md)**
- **[ActionAxis](../../../api/modules/input/class.actionaxis.md)**


## InputModule::Context Class

---

## Context ( )

Constructs a context with the specified name.
### Arguments

## void setEnabled ( )

Enables or disables the context.
### Arguments

## isEnabled ( )

Returns whether the context is enabled.
### Return value

True if the context is enabled.
## getID ( )

Returns the unique ID of this context.
### Return value

The context ID.
## getName ( )

Returns the name of this context.
### Return value

The context name.
## addAction ( )

Adds a new action to this context.
### Arguments

### Return value

The created action.
## addKeyAction ( )

Adds a new key (button/digital) action to this context.
### Arguments

### Return value

The created key action.
## addAxisAction ( )

Adds a new axis (analog) action to this context.
### Arguments

### Return value

The created axis action.
## getAction ( )

Returns an action by ID.
### Arguments

### Return value

The action, or nullptr if not found.
## getAction ( )

Returns an action by name.
### Arguments

### Return value

The action, or nullptr if not found.
## getAxisAction ( )

Returns an axis action by ID.
### Arguments

### Return value

The axis action, or nullptr if not found.
## getAxisAction ( )

Returns an axis action by name.
### Arguments

### Return value

The axis action, or nullptr if not found.
## getKeyAction ( )

Returns a key action by ID.
### Arguments

### Return value

The key action, or nullptr if not found.
## getKeyAction ( )

Returns a key action by name.
### Arguments

### Return value

The key action, or nullptr if not found.
## hasAction ( )

Checks if an action with the specified ID exists.
### Arguments

### Return value

True if the action exists.
## hasAction ( )

Checks if an action with the specified name exists.
### Arguments

### Return value

True if the action exists.
## void getAllActions ( )

Fills the vector with all actions in this context.
### Arguments

## void update ( )

Updates all actions in this context. Called automatically by InputManager.
## void clear ( )

Removes all actions from this context.
