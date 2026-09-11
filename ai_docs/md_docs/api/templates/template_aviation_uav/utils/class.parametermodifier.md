# ParameterModifier Class


ParameterModifier is an abstract interface for managing various parameters with normalized values and scale. Concrete implementations provide parameter modification for decals, field heights, and particle systems.


### See Also


- **[DecalParameterModifier](../../../../api/templates/template_aviation_uav/utils/class.decalparametermodifier.md)**
- **[FieldHeightParameterModifier](../../../../api/templates/template_aviation_uav/utils/class.fieldheigthparametermodifier.md)**
- **[ParticlesParameterModifier](../../../../api/templates/template_aviation_uav/utils/class.particlesparametermodifier.md)**
- **[VelocityParticlesParam](../../../../api/templates/template_aviation_uav/utils/class.velocityparticlesparam.md)**


## ParameterModifier Class

### Description

Abstract interface for managing various parameters. Values and scale are normalized (0.0 to 1.0).Abstract interface for managing various parameters. Values and scale are normalized (0.0 to 1.0).
---

## virtual void setValue ( ) =0

Sets the parameter value.
### Arguments

## virtual getValue ( ) =0

Returns the current parameter value.
### Return value

Current normalized value.
## virtual void setScale ( )

Sets the scale multiplier for the parameter.
### Arguments

## virtual getScale ( )

Returns the current scale multiplier.
### Return value

Current scale value.
