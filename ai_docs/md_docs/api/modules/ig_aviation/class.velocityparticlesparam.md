# VelocityParticlesParam Component

**Inherits from:** ComponentBase


VelocityParticlesParam automatically adjusts **[ParameterModifier](../../../api/modules/ig_aviation/class.parametermodifier.md)** values based on the node's movement speed. When the speed increases, the parameter values approach 1; when stationary, they approach 0.


This is useful for motion-dependent effects such as dust trails that appear when a vehicle is moving, wake effects that intensify with boat speed, or wind effects on particles at higher aircraft speeds.


The component calculates velocity by tracking position changes between frames and normalizes the result based on the max velocity parameter.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Settings Group |  |  |
| Max Velocity | *Float* | Speed at which parameter values reach 1 (*default: 10.0*). |
| Parameter Modifiers | *Array* | Nodes containing **[ParameterModifier](../../../api/modules/ig_aviation/class.parametermodifier.md)** components to control. |


### See Also


- **[ParameterModifier](../../../api/modules/ig_aviation/class.parametermodifier.md)**
