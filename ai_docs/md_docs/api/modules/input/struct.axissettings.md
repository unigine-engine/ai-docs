# InputModule::AxisSettings Struct


AxisSettings configures how an axis binding processes input values. It supports hardware axes, fake axes from digital inputs, and various value transformations.


Configuration options include **axis** (hardware axis index to read), **axis_clamp** (value range mode: FULL, POSITIVE_RANGE, NEGATIVE_RANGE, etc.), **axis_inverse** (invert the axis value), and **dead_zone** (ignore values below this threshold).


Fake axis options for digital-to-analog conversion include **use_fake_axis** (enable fake axis from keys), **positive_key** / **negative_key** (keys for positive/negative direction), **sensitivity** (how fast the value changes when key is pressed), and **gravity** (how fast the value returns to zero when key is released).


**POV** options for joysticks include **use_pov** (use POV hat directions as fake axis) and **positive_pov** / **negative_pov** (POV directions for positive/negative).


### See Also


- **[AxisBind](../../../api/modules/input/class.axisbind.md)**
- **[ActionAxis](../../../api/modules/input/class.actionaxis.md)**
