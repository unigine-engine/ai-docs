# ParticlesWind Component

**Inherits from:** ComponentBase


ParticlesWind automatically adjusts particle system gravity based on **IG** meteorological wind conditions. This creates realistic environmental effects where smoke, dust, and other particles are affected by wind.


The component can work recursively, finding and updating all particle systems in child nodes. When weather conditions change in the **IG** system, the component recalculates particle gravity to simulate wind influence.


The wind influence can be scaled using a curve, allowing non-linear mapping between wind speed and particle response.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Settings Group |  |  |
| Recursive | *Toggle* | Search for particle systems in child nodes (*default: true*). |
| Wind Scale | *Curve2d* | Curve mapping wind speed to particle effect intensity. |
| Gravity Vertical | *Float* | Vertical gravity component multiplier (*default: 1.0*). |


### See Also


- **[EffectAircraft](../../../api/modules/ig_aviation/class.effectaircraft.md)**
