# InputModule::InputManager Class


InputManager is the central singleton for the input system. It manages input contexts, handles initialization and updates, and provides save/load functionality for input configurations.


The input system is built around the concept of Actions and Bindings. Actions are named inputs like "Jump", "Fire", or "Throttle" that your game logic queries. Bindings are connections between physical inputs (keys, buttons, axes) and actions. Contexts are groups of actions that can be enabled or disabled together (e.g., "Menu", "Gameplay", "Vehicle").


Typical usage involves getting the singleton via **InputManager::get()**, creating contexts for different input modes, adding actions to contexts, adding bindings to actions, calling **update()** each frame, and querying action states in your game logic.


Input configurations can be saved to and loaded from **XML** files, allowing user-customizable controls.


### See Also


- **[Context](../../../api/modules/input/class.context.md)**
- **[Action](../../../api/modules/input/class.action.md)**
- **[DeviceManager](../../../api/modules/input/class.devicemanager.md)**


## InputModule::InputManager Class

---

## static get ( )

Returns the singleton instance of InputManager.
### Return value

The singleton instance.
## createContext ( )

Creates a new input context with the specified name.
### Arguments

### Return value

The created context.
## hasContext ( )

Checks if a context with the specified ID exists.
### Arguments

### Return value

True if the context exists.
## hasContext ( )

Checks if a context with the specified name exists.
### Arguments

### Return value

True if the context exists.
## getContext ( )

Returns the context with the specified ID.
### Arguments

### Return value

The context, or nullptr if not found.
## getContext ( )

Returns the context with the specified name.
### Arguments

### Return value

The context, or nullptr if not found.
## getDefaultContext ( )

Returns the default input context.
### Return value

The default context.
## getContextIDs ( )

Returns IDs of all registered contexts.
### Return value

Vector of all context IDs.
## void setContextEnabled ( )

Enables or disables a context by ID.
### Arguments

## void init ( )

Initializes the input manager.
## void update ( )

Updates all enabled contexts and their actions. Call this every frame.
## void shutdown ( )

Shuts down the input manager and releases resources.
## loadSettings ( )

Loads input configuration from an XML file.
### Arguments

### Return value

True if loading succeeded.
## void saveSettings ( )

Saves current input configuration to an XML file.
### Arguments

## getEventLoad ( )

Returns the event that fires when settings are loaded.
### Return value

Reference to the load event.
