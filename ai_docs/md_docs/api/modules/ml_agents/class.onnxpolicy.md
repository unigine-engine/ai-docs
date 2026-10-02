# MLAgents::OnnxPolicy Class

**Inherits from:** IPolicy


OnnxPolicy runs a trained model: it loads an `.onnx` file, checks that the shapes the model expects match the behavior it is asked to drive, and produces the actions with no trainer involved.


This is what an agent runs once the training is over. Assign the file to the *ONNX Model* parameter of the behavior's **[BehaviorConfig](../../../api/modules/ml_agents/class.behaviorconfig.md)** and the session creates the policy on its own - the class is rarely constructed by hand.


A trained model does not depend on the environment it was trained in: the layout, the routes and the starting positions can all differ, as the observations are relative to the agent. What it does depend on is the shape of those observations and actions, which is fixed at training time.


### See Also


- **[MLAgents::IPolicy](../../../api/modules/ml_agents/class.ipolicy.md)**
- **[MLAgents::BehaviorConfig](../../../api/modules/ml_agents/class.behaviorconfig.md)**


## OnnxPolicy Class

---

## static create ( )

Loads a trained model and checks it against the behavior specification. A mismatch between what the model expects and what the behavior produces is reported in the console and leaves the behavior on its heuristic.
### Arguments

### Return value

The created policy, or nullptr if the file cannot be loaded or does not match the behavior.
## virtual getName ( )

Returns the name of the policy kind.
### Return value

Always onnx.
## virtual getSource ( )

Returns the path of the model driving the behavior. The on-screen banner shows it, which is how you tell at a glance which model a scene is actually running.
### Return value

Path of the loaded model file.
## virtual void decide ( )

Runs the model over the observations of the batch and writes the actions it produces.
### Arguments
