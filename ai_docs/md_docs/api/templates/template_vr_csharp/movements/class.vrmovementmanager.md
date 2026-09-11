# VRMovementManager Component

**Inherits from:** Component


VRMovementManager initializes and updates all registered **[VRBaseMovement](../../../../api/templates/template_vr_csharp/base/class.vrbasemovement.md)** components, collects their input contributions, and feeds them into the **[PlayerMotor](../../../../api/templates/template_vr_csharp/movements/class.playermotor.md)**. Manages head collision detection against obstacle geometry.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Player | *VRPlayer* | The VR player to drive. |
| Movements | *List<VRBaseMovement>* | List of movement components contributing input. |
| Obstacles | *Node* | Node whose geometry is used for head collision detection. |


### See Also


- **[VRBaseMovement](../../../../api/templates/template_vr_csharp/base/class.vrbasemovement.md)**
- **[PlayerMotor](../../../../api/templates/template_vr_csharp/movements/class.playermotor.md)**
- **[VRPlayer](../../../../api/templates/template_vr_csharp/class.vrplayer.md)**


## VRMovementManager Class
