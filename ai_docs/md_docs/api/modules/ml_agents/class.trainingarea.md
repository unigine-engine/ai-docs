# MLAgents::TrainingArea Class

**Inherits from:** ComponentBase


TrainingArea marks one self-contained copy of the task and puts everything back where it started when an episode ends. At initialization it walks its own hierarchy and remembers the transformation of every movable node below it, so a reset needs no code of its own for the common case.


Copying the area is how training is made faster: every copy runs the same task with its own agents, and they all feed the same brain, so one run collects several times the experience per second. The agents of an area reach the rest of their own copy through **[Agent::getTrainingArea()](../../../api/modules/ml_agents/class.agent.md)** rather than by node name, which is what keeps a copy from reaching into its neighbor.


Anything a reset has to do beyond restoring transformations - rolling a new layout, moving a target, clearing accumulated state - is hooked to the reset event.


```cpp
#include <ml_agents/TrainingArea.h>

void MyLayout::init()
{
    // the layout component sits on the training area node itself
    MLAgents::TrainingArea *area = getComponent<MLAgents::TrainingArea>(node);
    if (area)
    {
        area->getEventReset().connect(event_connections, [this]() { onReset(); });
    }
}

```


### See Also


- **[MLAgents::Agent](../../../api/modules/ml_agents/class.agent.md)**
- **[MLAgents::Session](../../../api/modules/ml_agents/class.session.md)**


## TrainingArea Class

---

## void reset ( )

Puts every remembered node back to the transformation it had at initialization and fires the reset event. Called when the episode of an agent inside the area ends.
## getEventReset ( )

Returns the event fired on every reset of the area. Subscribe to it to do whatever restoring the transformations does not cover: rolling a new layout, moving a target, or clearing accumulated state.
### Return value

Event fired after the node transformations have been restored.
## getNumSavedNodes ( )

Returns how many movable nodes the area found below itself at initialization.
### Return value

Number of nodes whose transformation is restored on a reset.
