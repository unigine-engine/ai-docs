# ParticlesParameterModifier Component

**Inherits from:** ComponentBase, ParameterModifier


ParticlesParameterModifier controls particle system intensity by adjusting lifetime, spawn rate, and velocity based on a normalized value. This allows smooth fading of particle effects based on external conditions like altitude or speed.


The component can work recursively to find and control all particle systems in child nodes. Individual parameters (lifetime, spawn rate, velocity) can be independently enabled or disabled for fine-grained control.


Network synchronization via **Syncker** is optional and should only be enabled when cross-display synchronization is critical, as it can impact performance.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Settings Group |  |  |
| Recursive | *Toggle* | Synchronize child particle systems. |
| Enabled By Default | *Toggle* | Node default enabled state. |
| Sync | *Toggle* | Enable network synchronization via **Syncker**. |
| Interpolation Group |  |  |
| Lerp Life Time | *Toggle* | Interpolate particle lifetime with intensity. |
| Lerp Spawn Rate | *Toggle* | Interpolate spawn rate with intensity. |
| Lerp Velocity | *Toggle* | Interpolate velocity with intensity. |


### See Also


- **[ParameterModifier](../../../api/modules/ig_aviation/class.parametermodifier.md)**
- **[RotorWash](../../../api/modules/ig_aviation/class.rotorwash.md)**


## ParticlesParameterModifier Class

---

## void setEmitterEnabled ( )

Enables or disables the particle emitter.
### Arguments

## isEmitterEnabled ( )

Returns whether the particle emitter is currently enabled.
### Return value

True if the emitter is enabled.
