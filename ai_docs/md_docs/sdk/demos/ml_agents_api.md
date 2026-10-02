# Unigine ML Integration API


API reference for the **[Unigine ML Integration](../../sdk/demos/ml_agents.md)** demo.


The **MLAgents** namespace is the framework itself - the base classes an environment of your own is built from, and the types they exchange. The demo worlds below are examples of applying it, and the **Common** module holds the auxiliary components they share.


## MLAgents

- [MLAgents::Session Class](../../api/modules/ml_agents/class.session.md)
- [MLAgents::Agent Class](../../api/modules/ml_agents/class.agent.md)
- [MLAgents::AgentSetup Struct](../../api/modules/ml_agents/struct.agentsetup.md)
- [MLAgents::TrainingArea Class](../../api/modules/ml_agents/class.trainingarea.md)
- [MLAgents::BehaviorConfig Class](../../api/modules/ml_agents/class.behaviorconfig.md)
- [MLAgents::Sensor Class](../../api/modules/ml_agents/class.sensor.md)
- [MLAgents::RaySensor Class](../../api/modules/ml_agents/class.raysensor.md)
- [MLAgents::CameraSensor Class](../../api/modules/ml_agents/class.camerasensor.md)
- [MLAgents::ObservationWriter Class](../../api/modules/ml_agents/class.observationwriter.md)
- [MLAgents::Actions Class](../../api/modules/ml_agents/class.actions.md)
- [MLAgents::ActionSpec Struct](../../api/modules/ml_agents/struct.actionspec.md)
- [MLAgents::ActionBuffers Struct](../../api/modules/ml_agents/struct.actionbuffers.md)
- [MLAgents::ObservationSpec Struct](../../api/modules/ml_agents/struct.observationspec.md)
- [MLAgents::BehaviorSpec Struct](../../api/modules/ml_agents/struct.behaviorspec.md)
- [MLAgents::IPolicy Class](../../api/modules/ml_agents/class.ipolicy.md)
- [MLAgents::OnnxPolicy Class](../../api/modules/ml_agents/class.onnxpolicy.md)
- [MLAgents::ICommunicator Class](../../api/modules/ml_agents/class.icommunicator.md)
- [MLAgents::TrainerCommunicator Class](../../api/modules/ml_agents/class.trainercommunicator.md)
- [LineFollowerAgent Class](../../api/modules/ml_agents/worlds/class.linefolloweragent.md)
- [LineTrack Class](../../api/modules/ml_agents/worlds/class.linetrack.md)
- [RouteFollowAgent Class](../../api/modules/ml_agents/worlds/class.routefollowagent.md)
- [ChaseAgent Class](../../api/modules/ml_agents/worlds/class.chaseagent.md)
- [ChaseArenaBlocks Class](../../api/modules/ml_agents/worlds/class.chasearenablocks.md)
- [SoccerAgent Class](../../api/modules/ml_agents/worlds/class.socceragent.md)
- [SoccerField Class](../../api/modules/ml_agents/worlds/class.soccerfield.md)
- [SensorScreen Class](../../api/modules/ml_agents/worlds/class.sensorscreen.md)


## Common

- [MuteEventScoped Class](../../api/modules/common/class.muteeventscoped.md)
- [Tag Class](../../api/modules/common/class.tag.md)
- [Utils Namespace](../../api/modules/common/class.utils.namespace.md)


## Accessing Demo Source Code

You can study and modify the source code of this demo to create your own projects. To access the source code do the following:

1. Find the **Unigine ML Integration API** demo in the *Demos* section and click **[Install](/sdk/#samples)** (if you haven't installed it yet).
2. After successful installation the demo will appear in the *Installed* section, and you can click **Copy as Project** to create a project based on this demo. ![](../../sdk/demos/copy_as_project_gen.png)
3. In the **Create New Project** window, that opens, enter the name for your new project in the corresponding field and click **Create New Project**. ![](../../sdk/projects/create_project_cpp.png)
4. Now you can click **Open Code IDE** to check and modify source code in your default IDE, or click **Open Editor** to open the project in the [UnigineEditor](/editor2/). ![](../../sdk/projects/edit_code.png)
