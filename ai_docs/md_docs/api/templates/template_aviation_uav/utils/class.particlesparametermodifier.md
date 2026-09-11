# ParticlesParameterModifier Component

**Inherits from:** ComponentBase, ParameterModifier


ParticlesParameterModifier changes ObjectParticles lifetime, spawn rate, and velocity based on the effect intensity value.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Recursive | *Toggle* | *false* | Toggles synchronization of child particle systems. |
| Enabled by Default | *Toggle* | *true* | Toggles the node default state. If disabled, enable via code after adding to scene. |
| Sync | *Toggle* | *true* | Synchronization of particles via **Syncker**. Enable only if network sync is critical. |
| Lerp Life Time | *Toggle* | *true* | Lerp the particles life time value with the effect intensity. |
| Lerp Spawn Rate | *Toggle* | *true* | Lerp the particles spawn rate value with the effect intensity. |
| Lerp Velocity | *Toggle* | *true* | Lerp the particles velocity value with the effect intensity. |


### See Also


- **[ParameterModifier](../../../../api/templates/template_aviation_uav/utils/class.parametermodifier.md)**
- **[VelocityParticlesParam](../../../../api/templates/template_aviation_uav/utils/class.velocityparticlesparam.md)**


## ParticlesParameterModifier Class

### Description

Changes ObjectParticles lifetime, spawn rate, and velocity based on the effect intensity value.Changes ObjectParticles lifetime, spawn rate, and velocity based on the effect intensity value.
---

## void setValue ( )

Sets the particle parameter values based on effect intensity.
### Arguments

## getValue ( )

Returns the current parameter value.
### Return value

Current value.
## void setEmitterEnabled ( )

Enables or disables the particle emitter.
### Arguments

## isEmitterEnabled ( )

Returns whether the particle emitter is enabled.
### Return value

true if emitter is enabled; otherwise, false.
