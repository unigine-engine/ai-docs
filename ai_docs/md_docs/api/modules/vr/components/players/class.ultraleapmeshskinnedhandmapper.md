# UltraleapMeshSkinnedHandMapper Component


UltraleapMeshSkinnedHandMapper applies [*Ultraleap* skeletal data](../../../../../code/plugins/ultraleap/index_cpp.md#bones) to skinned hand meshes. Used together with **[VRHandTrackingControllerUltraleap](../../../../../api/modules/vr/components/players/class.vrhandtrackingcontrollerultraleap.md)** to animate hand models based on Ultraleap hand tracking input.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| left_hand | *Hand* (struct) | Left hand mapping configuration. |
| right_hand | *Hand* (struct) | Right hand mapping configuration. |


Each *Hand* struct contains bone index mappings for five fingers (thumb, index, middle, ring, pinky), each with four joints (base, first, middle, last), plus wrist, arm, and elbow indices. The *invert_direction* toggle flips the bone transform direction.
