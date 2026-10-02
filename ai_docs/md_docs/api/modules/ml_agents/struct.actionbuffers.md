# MLAgents::ActionBuffers Struct


ActionBuffers is the storage behind a decision: a **continuous** vector of floats and a **discrete** vector of choices, sized from an **[ActionSpec](../../../api/modules/ml_agents/struct.actionspec.md)**.


Agents do not touch it directly - they read and write the decision through **[Actions](../../../api/modules/ml_agents/class.actions.md)**, which is a view onto these buffers. The structure matters when a policy of your own fills in the decisions of a batch.


### See Also


- **[MLAgents::Actions](../../../api/modules/ml_agents/class.actions.md)**
- **[MLAgents::ActionSpec](../../../api/modules/ml_agents/struct.actionspec.md)**
- **[MLAgents::IPolicy](../../../api/modules/ml_agents/class.ipolicy.md)**


## ActionBuffers Class

---

## void resize ( )

Resizes both buffers to hold one decision of the given action space.
### Arguments

## void clear ( )

Zeroes the stored values without changing the size of the buffers.
