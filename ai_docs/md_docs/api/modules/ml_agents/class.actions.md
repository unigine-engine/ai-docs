# MLAgents::Actions Class


Actions carries the decision of a policy into **[Agent::act()](../../../api/modules/ml_agents/class.agent.md)**, and it is also what a hand-written **[heuristic()](../../../api/modules/ml_agents/class.agent.md)** fills in. It reads the two kinds of action separately: continuous values by index, and discrete choices by branch.


Continuous actions arrive in the [-1, 1] range and are scaled by the agent into whatever the task needs - a force, a steering angle, a throttle. A discrete branch arrives as the index of the choice the policy made.


**act()** runs on every step of the loop, not only on the ones carrying a fresh decision, so use **isNewDecision()** for anything that must happen once per decision rather than once per tick.


```cpp
void MyAgent::act(const MLAgents::Actions &actions)
{
    float throttle = actions.continuous(0);     // -1 .. 1
    float steer = actions.continuous(1);

    body->addForce(node->getWorldDirection() * (throttle * max_force));
    // ...

    addReward(progress * progress_reward);
}

```


> **Notice:** Reading an index the behavior does not have is reported in the console and returns a safe zero instead of reading out of bounds. If the actions of an agent read as zeros, check that the index matches the **[ActionSpec](../../../api/modules/ml_agents/struct.actionspec.md)** declared in **configure()**.


### See Also


- **[MLAgents::ActionSpec](../../../api/modules/ml_agents/struct.actionspec.md)**
- **[MLAgents::Agent](../../../api/modules/ml_agents/class.agent.md)**


## Actions Class

---

## continuous ( )

Returns one continuous action of the decision.
### Arguments

### Return value

Value of the action, normally within [-1, 1]. An index out of range is reported in the console and returns 0.
## discrete ( )

Returns the choice made in one discrete branch of the decision.
### Arguments

### Return value

Choice the policy made in that branch. A branch out of range is reported in the console and returns 0.
## void setContinuous ( )

Sets one continuous action. Called from **heuristic()** to drive the agent without a policy.
### Arguments

## void setDiscrete ( )

Sets the choice in one discrete branch. Called from **heuristic()** to drive the agent without a policy.
### Arguments

## isNewDecision ( )

Returns a value indicating if the actions are a fresh decision rather than the ones carried over from a previous step, as *Between Decisions* specifies.
### Return value

true if these actions come from a decision taken this step; otherwise, false.
## getSpec ( )

Returns the specification of the action space, which tells how many continuous actions and discrete branches there are.
### Return value

Action space these actions belong to.
