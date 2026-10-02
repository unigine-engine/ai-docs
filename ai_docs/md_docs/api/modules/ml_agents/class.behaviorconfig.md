# MLAgents::BehaviorConfig Class

**Inherits from:** ComponentBase


BehaviorConfig configures one behavior - one brain shared by every agent carrying its name. It is where a trained model is assigned, and where a behavior is kept out of the training altogether.


The component is optional: a behavior with no config of its own falls back to the heuristic of its agents when no trainer is connected. Put it anywhere in the scene, on a node named after the behavior or with *Behavior Name* set explicitly.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Behavior Name | *String* |  | Behavior this config applies to. Empty uses the name of the node the component sits on |
| Team ID | *Int* | 0 | Team id for adversarial setups. It becomes part of the behavior key sent to the trainer, so two teams of the same agent class train as two separate policies playing against each other |
| Policy | *Switch* | AUTO | *AUTO* takes the remote trainer when one is connected, otherwise the ONNX model if assigned, otherwise the heuristic. *HEURISTIC* always runs the agents' own **[heuristic()](../../../api/modules/ml_agents/class.agent.md)**, and the behavior is hidden from the trainer - which is how a behavior is kept out of a training run |
| ONNX Model | *File* |  | Trained policy (`.onnx`) driving this behavior when no trainer is connected |


### See Also


- **[MLAgents::Agent](../../../api/modules/ml_agents/class.agent.md)**
- **[MLAgents::Session](../../../api/modules/ml_agents/class.session.md)**
- **[MLAgents::OnnxPolicy](../../../api/modules/ml_agents/class.onnxpolicy.md)**


## BehaviorConfig Class

---

## getBehaviorName ( )

Returns the *Behavior Name* parameter, or the name of the node the component sits on when it is empty.
### Return value

Name of the behavior this config applies to.
