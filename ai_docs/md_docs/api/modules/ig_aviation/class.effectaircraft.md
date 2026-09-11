# EffectAircraft Component

**Inherits from:** NetworkComponentBase


EffectAircraft controls a single visual effect on an aircraft, such as engine fire, smoke trails, contrails, or burning effects. Each instance manages one particle system and can be enabled/disabled at runtime.


The component supports network synchronization through the **IG** Network system, allowing effect states to be synchronized across multiple displays in a distributed simulation environment.


Available effect types include engine fires (1-4), landing gear fires (front and back), tail fire, smoke trail, contrail (condensation trail), and general burning.


Effects can optionally respond to wind, adjusting particle direction and behavior based on the current meteorological conditions in the **IG** system.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Settings Group |  |  |
| Enable Node | *Node* | Node to enable/disable when the effect is active. |
| Emiter Node | *Node* | Node containing the particle system emitter. |
| Default Enable | *Toggle* | Whether the effect is enabled by default. |
| Effect Type | *Switch* | Type of the effect (fire, smoke, contrail, etc.). |
| Wind Depend | *Toggle* | Whether the effect responds to wind conditions. |


### See Also


- **[EffectAircraftController](../../../api/modules/ig_aviation/class.effectaircraftcontroller.md)**
- **[ParticlesWind](../../../api/modules/ig_aviation/class.particleswind.md)**


## EffectAircraft Class

---

## void setEnable ( )

Enables or disables the effect.
### Arguments

## isEnable ( )

Returns whether the effect is currently enabled.
### Return value

True if the effect is currently enabled.
## getType ( )

Returns the type of this effect.
### Return value

The effect type.
## void setWindSpeed ( )

Sets the wind speed affecting the effect particles.
### Arguments
