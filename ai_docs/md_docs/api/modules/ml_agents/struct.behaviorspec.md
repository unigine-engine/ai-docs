# MLAgents::BehaviorSpec Struct


BehaviorSpec is the full description of one brain: its **name**, the list of **observations** blocks its agents produce, and the **actions** they expect back.


The session builds it from the first agent that registers under a behavior name, and checks every agent that follows against it. Agents sharing a name must agree on the whole specification - a mismatch is refused, as one model cannot serve two different input or output shapes.


This is also what a trainer is offered when it connects, and what a configuration file has to have a matching section for. A behavior offered to a trainer with no section of its own still waits for decisions that never come, and the run ends on the exchange timeout with nothing trained.


### See Also


- **[MLAgents::ObservationSpec](../../../api/modules/ml_agents/struct.observationspec.md)**
- **[MLAgents::ActionSpec](../../../api/modules/ml_agents/struct.actionspec.md)**
- **[MLAgents::BehaviorConfig](../../../api/modules/ml_agents/class.behaviorconfig.md)**


## BehaviorSpec Class

---

## getObservationSize ( )

Returns the combined size of every observation block of the behavior.
### Return value

Total number of values across all observation blocks.
