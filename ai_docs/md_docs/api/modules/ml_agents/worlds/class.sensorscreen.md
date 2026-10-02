# SensorScreen Class

**Inherits from:** ComponentBase


SensorScreen shows what a **[CameraSensor](../../../../api/modules/ml_agents/class.camerasensor.md)** sees on a surface in the scene. It is a debugging aid rather than a part of any task: the Line Follow world uses it to put the agent's own view on a panel beside the track, so what the policy is steering from can be watched directly.


The render goes into a texture slot of the surface material. The material is inherited per node first, or every screen in the world would end up showing the same camera.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Screen Node | *Node* |  | Mesh whose surface shows the render. Empty uses the node the component sits on. Set it to drive a panel that cannot host the component itself |
| Sensor Node | *Node* |  | Node carrying the **[CameraSensor](../../../../api/modules/ml_agents/class.camerasensor.md)** whose view this screen shows. Leave it empty to take the first camera sensor found under this node's training area |
| Surface | *String* |  | Name of the surface the render goes on. Empty takes the only surface, which is an error if the object has more than one |
| Texture Slot | *String* | emission | Texture slot of the surface material the render is written into. On a billboard, emission is the slot to use rather than diffuse: diffuse is multiplied by the light reaching the panel, which leaves the render unreadable from any angle the light does not come from. On a miss, the log names every slot the material actually has |


### See Also


- **[MLAgents::CameraSensor](../../../../api/modules/ml_agents/class.camerasensor.md)**
- **[LineFollowerAgent](../../../../api/modules/ml_agents/worlds/class.linefolloweragent.md)**
