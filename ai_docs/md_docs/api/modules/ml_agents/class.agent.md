# MLAgents::Agent Class

**Inherits from:** ComponentBase


Agent is the base class for everything that learns. It is never used as it is: your own component inherits from it and overrides the protected hooks that define the task - what the agent perceives, what it can do, and what it is paid for.


The agent registers itself with the **[Session](../../../api/modules/ml_agents/class.session.md)** at initialization and reports the shape of its observations and actions. Agents sharing a behavior name share one brain, and the **[BehaviorConfig](../../../api/modules/ml_agents/class.behaviorconfig.md)** component carrying that name configures it.


```cpp
#include <ml_agents/Agent.h>

class MyAgent: public MLAgents::Agent
{
public:
    COMPONENT_DEFINE(MyAgent, MLAgents::Agent);

protected:
    void configure(MLAgents::AgentSetup &setup) override
    {
        setup.actions = MLAgents::ActionSpec::continuous(2);
    }

    void observe(MLAgents::ObservationWriter &obs) override
    {
        obs.write(node->getWorldPosition().toFloat());
    }

    void act(const MLAgents::Actions &actions) override
    {
        float throttle = actions.continuous(0);
        float steer = actions.continuous(1);
        // drive the body here
    }
};

```


### Overridable Hooks


These protected methods are what a derived class implements. All of them are optional except **configure()**, which an agent needs in order to declare its actions.


| Method | Called | Purpose |
|---|---|---|
| configure() | Once, at initialization | Declare the action space and attach any sensors created in code. The observation size is measured right after by running **observe()** against a probe writer |
| onEpisodeBegin() | At the start of every episode | Put the agent back into a starting state: position, velocity, and whatever the task randomizes |
| observe() | On every decision | Write the observation vector. It has to write the same number of values every time, in the same order |
| act() | On every step | Apply the actions and pay out the rewards. On steps without a fresh decision the actions are whatever *Between Decisions* says |
| heuristic() | Instead of the policy, when no trainer and no model drive the behavior | Fill in the actions by hand. It keeps the scene alive without a trained model, and is the fastest way to check that the task is physically solvable at all |
| isDebugDrawEnabled() | Before drawing the overlay | Exclude this agent from the 3D debug overlay. Returns true unless overridden |
| onDebugDraw() | Every frame the overlay is on | Draw whatever explains what the agent is doing right now: applied forces, targets, lines of sight |


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Behavior Name | *String* |  | Agents sharing a name share one brain, and a **[BehaviorConfig](../../../api/modules/ml_agents/class.behaviorconfig.md)** with this name configures it. Empty uses the component class name |
| Max Episode Steps | *Int* | 0 | Physics ticks before the episode is interrupted (truncation). 0 means unlimited |
| Decision Interval | *Int* | 5 | Ask the brain for a new action every N physics ticks. 0 asks only on **requestDecision()** |
| Decision Offset | *Int* | 0 | Shifts this agent's decision ticks to spread the load across agents |
| Between Decisions | *Switch* | REPEAT_LAST_ACTION | What **act()** receives on ticks without a fresh decision: the last action again, or zeros |
| Debug Label Height | *Float* | 1.2 | How far (m) above the agent origin the running-reward label floats. The label is switched on session-wide by *Show Agent Debug*, and per agent by that agent's own debug draw flag |
| Debug Vector Height | *Float* | 1.0 | How far (m) above the agent origin its action arrows start. Drawn from the origin they would end up buried inside the body whenever they point along it |


### See Also


- **[MLAgents::AgentSetup](../../../api/modules/ml_agents/struct.agentsetup.md)**
- **[MLAgents::ObservationWriter](../../../api/modules/ml_agents/class.observationwriter.md)**
- **[MLAgents::Actions](../../../api/modules/ml_agents/class.actions.md)**
- **[MLAgents::Sensor](../../../api/modules/ml_agents/class.sensor.md)**


## Agent Class

---

## protected virtual void configure ( )

Declares what the agent can do. Called once at initialization, before the observation size is measured. Override it to set the action space; an agent that declares none is refused by the session.
### Arguments

## protected virtual void onEpisodeBegin ( )

Called at the start of every episode, before the first observation is taken. Override it to put the agent back into a starting state - and to randomize that state, or the policy learns one rehearsed opening instead of the task.
## protected virtual void observe ( )

Writes the agent's own observation. Called once per decision, and once at initialization against a probe writer to measure the vector size - so it must write the same number of values in the same order every time. Sensor components contribute their own blocks separately.
### Arguments

## protected virtual void act ( )

Applies the actions and pays out the rewards. Called on every step of the decision loop, not only on the ones carrying a fresh decision - use **Actions::isNewDecision()** to tell them apart.
### Arguments

## protected virtual void heuristic ( )

Produces the actions by hand when neither a trainer nor an ONNX model drives the behavior. It keeps the scene alive without a trained model, and checking that a hand-written heuristic can solve the task at all is the cheapest way to find out the task is physically impossible before spending a training run on it.
### Arguments

## protected virtual isDebugDrawEnabled ( )

Returns a value indicating if this agent is included in the 3D debug overlay. Returns true unless overridden; the usual override forwards a *Debug Draw* parameter of the derived component.
### Return value

true if this agent takes part in the overlay; otherwise, false.
## protected virtual void onDebugDraw ( )

Draws whatever explains what the agent is doing right now. Called every frame while the session overlay is on and this agent is not filtered out of it.
## protected debugVectorOrigin ( )

Returns the point the debug arrows are drawn from: the agent origin lifted by *Debug Vector Height*.
### Return value

World position the action arrows start from.
## void addReward ( )

Adds the given value to the reward accumulated since the last decision. This is how a dense signal is paid out: call it from **act()** for every bit of progress made.
### Arguments

## void setReward ( )

Replaces the reward accumulated since the last decision, discarding whatever was added before it.
### Arguments

## void endEpisode ( )

Ends the episode as terminated: the task reached an end state of its own, such as a goal scored or the agent falling off the platform. The trainer treats the return as complete and expects nothing beyond it.
## void interruptEpisode ( )

Ends the episode as interrupted: it was cut short from the outside - by a step limit or a reset - while the task itself was still unfinished. The trainer keeps bootstrapping the value of the final state instead of treating it as the end of the task.
## void requestDecision ( )

Asks for a decision on the next step. Used with *Decision Interval* set to 0, where the agent decides when it needs a new action instead of being asked on a fixed schedule.
## void renderDebug ( )

Draws this agent's part of the 3D overlay: the running-reward label and whatever **onDebugDraw()** adds. Called by the session for every agent that passes its distance filter.
## getCumulativeReward ( )

Returns the total reward the agent has collected in the current episode.
### Return value

Reward collected since the episode began.
## getEpisodeStep ( )

Returns the number of steps taken since the current episode began.
### Return value

Steps taken in the current episode.
## getEpisodeCount ( )

Returns the number of episodes this agent has been through.
### Return value

Episodes finished since the world was loaded.
## getAgentId ( )

Returns the identifier the session assigned to this agent when it registered.
### Return value

Identifier of the agent within the session.
## getBehaviorKey ( )

Returns the key identifying the brain this agent shares: the behavior name, plus the team id when a **[BehaviorConfig](../../../api/modules/ml_agents/class.behaviorconfig.md)** sets one. This is the name the trainer sees and the name a configuration file has to list.
### Return value

Behavior key of the agent.
## getActionSpec ( )

Returns the action space of this agent.
### Return value

Action space declared in **configure()**.
## getVectorObservationSize ( )

Returns the size of the agent's own observation vector, measured at initialization. Sensor blocks are not counted in it.
### Return value

Number of values **observe()** writes.
## getLastActions ( )

Returns the actions handed to the last **act()** call. Useful for drawing what the agent is doing from outside the agent itself.
### Return value

Actions last applied.
## getTrainingArea ( )

Returns the **[TrainingArea](../../../api/modules/ml_agents/class.trainingarea.md)** the agent was found under. Agents use it to reach the other components of their own copy of the scene rather than a neighboring one.
### Return value

The training area this agent belongs to, or nullptr if it is not inside one.
