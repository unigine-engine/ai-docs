# DecalParameterModifier Component

**Inherits from:** ComponentBase, ParameterModifier


DecalParameterModifier controls the visibility of a decal by modifying its material's albedo_visible parameter. The value interpolates from 0 (invisible) to the decal's initial albedo value (fully visible).


This is commonly used for effects like rotor wash ground disturbance decals, where the intensity needs to vary based on helicopter altitude or rotor speed.


### See Also


- **[ParameterModifier](../../../api/modules/ig_aviation/class.parametermodifier.md)**
- **[RotorWash](../../../api/modules/ig_aviation/class.rotorwash.md)**
