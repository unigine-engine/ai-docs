# MLAgents::AgentSetup Struct


AgentSetup is what an agent fills in from its **[configure()](../../../api/modules/ml_agents/class.agent.md)** method to declare what it can do.


The **actions** field holds the **[ActionSpec](../../../api/modules/ml_agents/struct.actionspec.md)** describing the action space. An agent that leaves it empty is refused by the session, as there would be nothing for a policy to decide.


Sensors sitting on the agent node or below it are found automatically and need no mention here. Use **addSensor()** only for a sensor created in code, which has no node of its own to be discovered on.


```cpp
void MyAgent::configure(MLAgents::AgentSetup &setup)
{
    // two continuous actions: throttle and steering
    setup.actions = MLAgents::ActionSpec::continuous(2);

    // or a pair of discrete branches with 3 choices each
    // setup.actions = MLAgents::ActionSpec::discrete({3, 3});
}

```


### See Also


- **[MLAgents::Agent](../../../api/modules/ml_agents/class.agent.md)**
- **[MLAgents::ActionSpec](../../../api/modules/ml_agents/struct.actionspec.md)**
- **[MLAgents::Sensor](../../../api/modules/ml_agents/class.sensor.md)**


## AgentSetup Class

---

## void addSensor ( )

Attaches a sensor created in code. Sensors placed on nodes are collected automatically and must not be added this way.
### Arguments
