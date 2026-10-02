# RouteFollowAgent Class

**Inherits from:** MLAgents::Agent


RouteFollowAgent is the agent of the Route Follow world: a cube that has to visit a chain of waypoints in order. It is the simplest complete task in the demo - no sensors, a handful of numbers as the observation, and a reward made of one dense term and two sparse ones.


The route is generated anew for every episode, with a random number of waypoints in random places, so the policy has to learn how to reach a target rather than one memorized path.


The actions are two continuous values driving an XY thrust. The dense signal pays per meter of approach to the current waypoint, which is what makes the task learnable: reaching a waypoint by chance is far too rare to learn from on its own.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Min Waypoints | *Int* | 3 | Fewest waypoints spawned per episode |
| Max Waypoints | *Int* | 6 | Most waypoints spawned per episode |
| Area Size X | *Float* | 12.0 | Full width (X) of the random spawn box, centered on the start position |
| Area Size Y | *Float* | 12.0 | Full depth (Y) of the random spawn box |
| Max Force | *Float* | 40.0 | Thrust force scale (N). The two actions are an XY force, so this depends on the mass of the cube |
| Max Speed | *Float* | 3.0 | Top-speed cap (m/s), so continuous thrust does not accelerate without bound |
| Reach Distance | *Float* | 0.7 | Horizontal distance at which a waypoint counts as reached |
| Fall Depth | *Float* | 2.0 | How far below the start height (m) counts as fallen off the platform, which ends the episode |
| Progress Reward | *Float* | 0.05 | Reward per meter of approach to the current waypoint |
| Debug Draw | *Toggle* | 1 | Visualize the spawn box, the waypoints (green for the current target, grey for the visited ones), the path and the line to the target |
| Debug Vector Scale | *Float* | 1.0 | Length (m) of the drive arrow at full deflection |


### See Also


- **[MLAgents::Agent](../../../../api/modules/ml_agents/class.agent.md)**
- **[MLAgents::TrainingArea](../../../../api/modules/ml_agents/class.trainingarea.md)**


## RouteFollowAgent Class

---

## protected virtual void configure ( )

Declares two continuous actions driving an XY thrust.
### Arguments

## protected virtual void onEpisodeBegin ( )

Puts the cube back at its start position and rolls a new route: a random number of waypoints in random places inside the spawn box.
## protected virtual void observe ( )

Writes the offset to the current waypoint, the agent's own XY velocity, and how far through the route it is. The offset is relative to the agent, which is what lets a trained model work on a route it has never seen.
### Arguments

## protected virtual void act ( )

Applies the thrust, pays the progress reward per meter of approach, advances to the next waypoint once the current one is within *Reach Distance*, and ends the episode when the route is finished or the cube falls off the platform.
### Arguments

## protected virtual void heuristic ( )

Drives straight at the current waypoint, which keeps the world running without a trained model.
### Arguments

## protected virtual void onDebugDraw ( )

Draws the spawn box, the route with the visited and pending waypoints, and the line from the agent to its current target.
