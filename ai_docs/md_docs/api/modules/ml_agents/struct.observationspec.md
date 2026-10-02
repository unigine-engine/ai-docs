# MLAgents::ObservationSpec Struct


ObservationSpec describes one block of an observation: its **name**, its **shape** as a list of dimensions, and its **dtype**.


An agent produces one such block for what its own **[observe()](../../../api/modules/ml_agents/class.agent.md)** writes, and one more for every sensor attached to it. Together they make up the **[BehaviorSpec](../../../api/modules/ml_agents/struct.behaviorspec.md)** the trainer is told about.


A block of ObsDataType::FLOAT32 with a single dimension is an ordinary vector observation. A three-dimensional block of ObsDataType::UINT8 is a visual one, and that is what makes the trainer put a convolutional network in front of it.


### See Also


- **[MLAgents::BehaviorSpec](../../../api/modules/ml_agents/struct.behaviorspec.md)**
- **[MLAgents::Sensor](../../../api/modules/ml_agents/class.sensor.md)**


## ObservationSpec Class

---

## getSize ( )

Returns how many values the block holds.
### Return value

Number of values in the block: the product of its dimensions, or 0 if it has none.
## isVisual ( )

Returns a value indicating if the block is a visual observation.
### Return value

true for a three-dimensional block of bytes; otherwise, false.
## toString ( )

Returns the shape of the block in a readable form. This is what the session prints when it logs the specifications of the registered behaviors.
### Return value

Readable description of the shape, such as 12 or 64x64x3 u8.
