# ParameterModifier Class


ParameterModifier is an abstract interface for managing various visual parameters with normalized values (0-1). It provides a common API for different modifier implementations that control decal visibility, field heights, particle systems, and other effects.


The interface supports both value control (0-1 intensity) and scale modification for fine-tuning effect strength. Concrete implementations include **[DecalParameterModifier](../../../api/modules/ig_aviation/class.decalparametermodifier.md)**, **[FieldHeigthParameterModifier](../../../api/modules/ig_aviation/class.fieldheigthparametermodifier.md)**, and **[ParticlesParameterModifier](../../../api/modules/ig_aviation/class.particlesparametermodifier.md)**.


This pattern allows systems like **[RotorWash](../../../api/modules/ig_aviation/class.rotorwash.md)** to control multiple different effect types through a single uniform interface.


### See Also


- **[DecalParameterModifier](../../../api/modules/ig_aviation/class.decalparametermodifier.md)**
- **[FieldHeigthParameterModifier](../../../api/modules/ig_aviation/class.fieldheigthparametermodifier.md)**
- **[ParticlesParameterModifier](../../../api/modules/ig_aviation/class.particlesparametermodifier.md)**
- **[VelocityParticlesParam](../../../api/modules/ig_aviation/class.velocityparticlesparam.md)**


## ParameterModifier Class

---

## void setValue ( )

Sets the modifier value. Abstract method implemented by subclasses.
### Arguments

## getValue ( )

Returns the current modifier value.
### Return value

Current normalized value.
## void setScale ( )

Sets the scale multiplier for the effect.
### Arguments

## getScale ( )

Returns the current scale multiplier.
### Return value

Current scale value.
