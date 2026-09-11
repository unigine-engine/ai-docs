# InputModule::KeySettings Struct


KeySettings configures how a key binding detects input. It supports direct key/button binding, axis-as-button, and POV hat directions.


Configuration options include **key** (key or button index to bind) and **use_with_console** (allow input even when console is open).


Axis-as-button options include **use_axis** (detect axis threshold as button press), **axis** (axis index to monitor), **axis_inverse** (trigger on negative values instead of positive), and **threshold** (axis value that triggers the "press", default: 0.5).


**POV** options for joysticks include **use_pov** (use POV hat direction as button) and **pov** (POV direction: UP, DOWN, LEFT, RIGHT).


### See Also


- **[KeyBind](../../../api/modules/input/class.keybind.md)**
- **[ActionKey](../../../api/modules/input/class.actionkey.md)**
