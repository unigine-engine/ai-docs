# MLAgents::ActionSpec Struct


ActionSpec describes the action space of a behavior: how many continuous actions it has, and how many choices each of its discrete branches offers. An agent declares it in **[configure()](../../../api/modules/ml_agents/class.agent.md)**, and every agent sharing a behavior must declare the same one.


The **continuous_count** field holds the number of continuous actions, each arriving in the [-1, 1] range. The **discrete_branches** field holds one entry per branch, giving the number of choices in it. The two kinds can be combined in one spec.


A continuous action suits anything that varies smoothly, such as a throttle or a steering angle. A discrete branch suits a choice between alternatives that have no order to them. Each branch is independent: three branches of two choices are three yes-or-no decisions taken at once, not one choice out of six.


```cpp
// two continuous actions
setup.actions = MLAgents::ActionSpec::continuous(2);

// two independent discrete branches, 3 choices each
setup.actions = MLAgents::ActionSpec::discrete({3, 3});

// one continuous action plus one branch of 2 choices
setup.actions = MLAgents::ActionSpec::continuous(1).addDiscreteBranch(2);

```


> **Notice:** Once a model is trained, the action space is fixed: the model produces exactly the outputs it was trained with, so adding an action means training again from scratch.


### See Also


- **[MLAgents::Actions](../../../api/modules/ml_agents/class.actions.md)**
- **[MLAgents::AgentSetup](../../../api/modules/ml_agents/struct.agentsetup.md)**


## ActionSpec Class

---

## static continuous ( )

Creates a specification with the given number of continuous actions and no discrete branches.
### Arguments

### Return value

Specification of a purely continuous action space.
## static discrete ( )

Creates a specification with the given discrete branches and no continuous actions.
### Arguments

### Return value

Specification of a purely discrete action space.
## addDiscreteBranch ( )

Appends one discrete branch to the specification.
### Arguments

### Return value

Reference to the same specification, so the calls can be chained.
## isEmpty ( )

Returns a value indicating if the action space is empty. An agent declaring an empty one is refused by the session.
### Return value

true if the specification declares no actions at all; otherwise, false.
## toString ( )

Returns the action space in a readable form. This is what the session prints when it logs the specifications of the registered behaviors.
### Return value

Readable description of the action space, such as continuous(2) or discrete(3,3).
