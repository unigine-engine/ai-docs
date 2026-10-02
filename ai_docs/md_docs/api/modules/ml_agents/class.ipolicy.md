# MLAgents::IPolicy Class


IPolicy is the interface behind everything that turns observations into actions. A behavior has exactly one policy at a time, and which one it gets is decided by the session and the **[BehaviorConfig](../../../api/modules/ml_agents/class.behaviorconfig.md)**: the remote trainer when one is connected, otherwise the ONNX model if a file is assigned, otherwise the heuristic.


The demo ships two implementations. **HeuristicPolicy** forwards the decision to each agent's own **[heuristic()](../../../api/modules/ml_agents/class.agent.md)**, which is what keeps a scene alive with no model and no trainer. **[OnnxPolicy](../../../api/modules/ml_agents/class.onnxpolicy.md)** runs a trained model.


Implement the interface to drive a behavior some other way - a scripted opponent, a recorded trajectory, or a model served by something other than ONNX.


### See Also


- **[MLAgents::OnnxPolicy](../../../api/modules/ml_agents/class.onnxpolicy.md)**
- **[MLAgents::BehaviorConfig](../../../api/modules/ml_agents/class.behaviorconfig.md)**


## IPolicy Class

---

## virtual getName ( ) =0

Returns the name of the policy kind. It is what the on-screen banner names as the thing currently driving the agents.
### Return value

Short name of the policy kind, such as heuristic or onnx.
## virtual getSource ( )

Returns the specific source behind the policy - the path of the model file, for instance, rather than just the word onnx.
### Return value

Where the decisions come from. Returns the policy name unless overridden.
## virtual void decide ( ) =0

Produces the actions for every agent of the batch that asked for a decision. The observations come in with the batch, and the actions are written into its output buffers in the same order.
### Arguments
