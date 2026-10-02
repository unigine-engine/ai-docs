# MLAgents::Session Class

**Inherits from:** ComponentBase


Session drives the decision loop shared by all agents of the world: it keeps the behavior registry, owns the connection to the trainer, and decides what drives each behavior - the trainer, an ONNX model, or the agents' own heuristic.


Every world has exactly one Session and it is mandatory: without it the agents switch themselves off and log an error. The node carrying the component can sit anywhere in the hierarchy, under any name.


```cpp
#include <ml_agents/Session.h>

// the session is a singleton reachable from anywhere
if (MLAgents::Session *session = MLAgents::Session::get())
{
    float width = session->getEnvParam("goal_width", 5.0f);
}

```


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Seed | *Int* | 0 | Seed set at initialization for reproducible runs. 0 keeps the engine default |
| Time Scale | *Float* | 1.0 | Game and physics time scale. A connected trainer may override it |
| Stepping | *Switch* | PHYSICS_TICK | Clock driving the decision loop. *PHYSICS_TICK* uses the fixed physics rate and suits physical agents; *UPDATE* steps once per frame, for purely kinematic worlds |
| Fixed Frame Time | *Float* | 0.0166667 | Seconds of game time one rendered frame advances, for *Stepping* = *UPDATE*. Without it a decision advances the world by however long the frame happened to take, so the same policy behaves differently on a different machine. 0 uses the real frame time |
| Show HUD | *Toggle* | 0 | On-screen per-agent debug overlay |
| Show Banner | *Toggle* | 1 | Large caption at the top of the screen naming what is driving the agents right now: the trainer, an ONNX file (with its path), or the hand-written heuristic |
| Show Agent Debug | *Toggle* | 1 | Starting state of the 3D overlay drawn around every agent: its running reward, plus whatever its class draws about what it is doing. *Agent Debug Key* flips it at runtime |
| Agent Debug Distance | *Float* | 0.0 | Draw the overlay only for agents within this many meters of the camera, which keeps the picture readable when all training areas draw at once. 0 means no limit |
| Agent Debug Clip | *Float* | 0.0 | Visualizer clip distance (m) applied while the overlay is on. Set it at or above *Agent Debug Distance*, or it clips agents the distance filter was happy to keep. 0 leaves the render setting alone |
| Agent Label Depth Test | *Toggle* | 0 | Hide an agent's reward label while something stands between it and the camera. Costs a physics intersection per drawn label, so keep it behind *Agent Debug Distance* |
| Agent Label Depth Mask | *Mask* | physics_intersection | The [bit mask](../../../principles/bit_masking/index.md#intersection_mask) the label occlusion ray tests against. Walls have to be in it, or nothing ever hides a label |
| Agent Debug Key | *String* | F2 | Key toggling the 3D overlay while the world runs, by name (f2, g, ...). Empty means no hotkey |
| Trainer Port | *Int* | 5004 | Trainer connection port used when *--trainer-port* is passed without a value |


### See Also


- **[MLAgents::Agent](../../../api/modules/ml_agents/class.agent.md)**
- **[MLAgents::BehaviorConfig](../../../api/modules/ml_agents/class.behaviorconfig.md)**
- **[MLAgents::TrainingArea](../../../api/modules/ml_agents/class.trainingarea.md)**


## Session Class

---

## static get ( )

Returns the single Session instance of the loaded world.
### Return value

The session of the current world, or nullptr if the world has none.
## isTrainerConnected ( )

Returns a value indicating if an external trainer is currently connected and driving the behaviors.
### Return value

true if a trainer is connected; otherwise, false.
## void setCommunicator ( )

Sets the communicator the session exchanges decisions through. Use it to plug in a transport of your own instead of the built-in **[TrainerCommunicator](../../../api/modules/ml_agents/class.trainercommunicator.md)**.
### Arguments

## getEnvParam ( )

Returns a curriculum parameter sent by the trainer. The default value keeps the world runnable on its own, as a scene reading curriculum parameters still starts with no trainer attached. Read these on the episode reset rather than every tick: a value that changes mid-episode moves the task while the agent is still solving it.
### Arguments

### Return value

Current value of the environment parameter.
## void setEnvParam ( )

Sets a curriculum parameter value.
### Arguments

## getStepping ( )

Returns the clock currently driving the decision loop.
### Return value

0 for *PHYSICS_TICK*, 1 for *UPDATE*.
## void applyTimeScale ( )

Applies the given scale to both the game and the physics clock. On a session stepping on the frame clock (*Stepping* = *UPDATE*) the scale is clamped to 1, as there it would not run the world faster but make every decision cover more of it.
### Arguments

## isLabelOccluded ( )

Checks if a debug label is hidden by the geometry. Always returns false when *Agent Label Depth Test* is off.
### Arguments

### Return value

true if something stands between the label and the camera; otherwise, false.
## isDebugVisible ( )

Returns a value indicating if the 3D debug overlay is currently drawn.
### Return value

true if the 3D agent overlay is on; otherwise, false.
## static isDebugVisibleGlobally ( )

Checks the overlay state without holding a Session pointer. Safe to call when the world has no session.
### Return value

true if a session exists and its overlay is on; otherwise, false.
## void setDebugVisible ( )

Sets the visibility of the 3D agent overlay.
### Arguments

## isHudVisible ( )

Returns a value indicating if the on-screen statistics window is shown.
### Return value

true if the HUD window is shown; otherwise, false.
## void setHudVisible ( )

Sets the visibility of the on-screen statistics window.
### Arguments

## isBannerVisible ( )

Returns a value indicating if the caption naming the current policy source is shown.
### Return value

true if the banner is shown; otherwise, false.
## void setBannerVisible ( )

Sets the visibility of the policy source caption.
### Arguments

## isLabelDepthTested ( )

Returns a value indicating if reward labels are hidden by the geometry standing in front of them.
### Return value

true if labels are occlusion-tested; otherwise, false.
## void setLabelDepthTested ( )

Sets whether reward labels are occlusion-tested.
### Arguments

## getAgents ( )

Returns the list of all agents registered in the session, across all behaviors and training areas.
### Return value

All agents registered in the session.
## getBehaviors ( )

Returns the behavior registry: every distinct behavior key the registered agents have produced, each with its specification, its agents and the policy driving them.
### Return value

Behaviors by name.
## getTickCount ( )

Returns the number of decision loop steps taken since the world was loaded.
### Return value

Number of steps since the world was loaded.
