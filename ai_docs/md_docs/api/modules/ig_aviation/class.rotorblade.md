# RotorBlade Component

**Inherits from:** NetworkComponentBase


RotorBlade handles helicopter rotor visualization, including blade rotation, coning effects, and the smooth transition from individual blade geometry to a blurred disk at high RPM values.


The component requires specially prepared content: a single blade mesh sample (the component clones it for all blades), a blade material supporting the coning angle parameter, a disk mesh representing the blurred rotor at high speed, and a disk material with blur animation and coning parameters.


Key features include blade cloning (automatically creates the specified number of blades from a sample), coning simulation (supports beta_0 for collective coning, beta_cos for longitudinal flapping, and beta_sin for lateral flapping), smooth transition (blades fade out while the disk fades in as RPM increases, controlled by threshold values and alpha curves), and network synchronization (rotation state is synchronized across distributed displays).


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Input Group |  |  |
| Rotor Speed | *Float* | Rotor rotation speed in RPM. |
| Beta 0 | *Float* | Coning angle parameter. |
| Beta Cos | *Float* | Longitudinal flapping parameter. |
| Beta Sin | *Float* | Lateral flapping parameter. |
| Rotor Group |  |  |
| Rotation Direction | *Switch* | CW (clockwise) or CCW (counter-clockwise). |
| Pivot | *Node* | Node to rotate with the rotor. |
| Axis | *Vec3* | Rotation axis. |
| Blade Group |  |  |
| Blade Sample | *Node* | Single blade mesh to clone. |
| Total Count | *Int* | Number of blades (*default: 4*). |
| Length | *Float* | Blade length in meters (*default: 6.0*). |
| Material Beta 0 Parameter | *String* | Material parameter name for coning. |
| Material Blade Length Parameter | *String* | Material parameter name for length. |
| Circle Group |  |  |
| Node | *Node* | Blurred disk mesh. |
| Material Beta 0/Cos/Sin Parameters | *String* | Material parameter names for coning. |
| Material UV Animation Parameter | *String* | Parameter for disk animation. |
| RPM To Time Coefficient | *Float* | RPM to animation speed multiplier. |
| Blurring Group |  |  |
| Threshold Blade Speed | *Float* | RPM where blades start to fade. |
| Threshold Disk Speed | *Float* | RPM where only disk is visible. |
| Blade Alpha | *Curve2d* | Blade transparency curve during transition. |
| Circle Alpha | *Curve2d* | Disk transparency curve during transition. |


### See Also


- **[TransparentHelper](../../../api/modules/ig_aviation/class.transparenthelper.md)**
- **[RotorWash](../../../api/modules/ig_aviation/class.rotorwash.md)**
