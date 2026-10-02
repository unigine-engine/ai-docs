# ChaseAgent Class

**Inherits from:** MLAgents::Agent


ChaseAgent is the agent of the Chase world, where two agents of the same class play opposite roles: the chaser closes on its opponent, the runner keeps the gap open. The *Role* parameter picks which, and the two are trained against each other in the same run.


The world is the demo's example of a task where the target has to be found rather than simply approached. Both agents perceive the arena through a **[RaySensor](../../../../api/modules/ml_agents/class.raysensor.md)** covering the full 360 degrees, and the exact position of the opponent is deliberately kept out of the observation: the chaser has to spot the runner with its rays, and it remembers where it last saw it for *Memory Time* seconds. The exact position is used only by the reward, which pays the chaser for every meter it closes whether or not it has seen where the runner is.


The reward is zero-sum on the catch and on the line of sight, which is what turns the pair into opponents rather than two agents solving separate tasks. Two terms exist purely to defeat local optima: the chaser is paid while the runner is in sight, so searching is worth the effort, and charged for idling, so standing still stops being free.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Role | *Switch* | CHASER | *CHASER* closes on the opponent and is rewarded on touch; *RUNNER* keeps the gap open |
| Max Force | *Float* | 40.0 | XY thrust scale (N). Depends on the body mass, so tune it together with *Max Speed* |
| Max Speed | *Float* | 4.0 | Top-speed cap (m/s), so continuous thrust does not accelerate without bound |
| Runner Agility | *Float* | 0.9 | The runner's speed and force multiplier over the chaser. Keep it below 1: a runner that is simply faster can never be caught in the open, the catch reward becomes unreachable and the chaser learns nothing. Its edge should come from obstacles and cover rather than raw speed |
| Arena Size | *Vec2* | 40.0, 40.0 | Full XY extents (m) of the arena, used only when there is no **[ChaseArenaBlocks](../../../../api/modules/ml_agents/worlds/class.chasearenablocks.md)** on the training area - that component measures the floor and is the authority when present |
| Spawn Clearance | *Float* | 1.0 | Free radius (m) required around a spawn point - at least the body half-width plus a margin |
| Vision Range | *Float* | 40.0 | How far the line-of-sight check reaches (m). Beyond it the opponent counts as unseen even in the open |
| Vision Mask | *Mask* | physics_intersection | The [bit mask](../../../../principles/bit_masking/index.md#intersection_mask) the line-of-sight ray tests against. Walls and blocks must be in it, or nothing ever blocks sight |
| Memory Time | *Float* | 6.0 | Seconds a sighting stays useful. Its age is fed to the policy normalized by this, so an old memory is visibly old; the memory is dropped when the agent reaches the remembered spot and finds nothing |
| Catch Reward | *Float* | 3.0 | Terminal reward the chaser gains and the runner loses on a catch (zero-sum) |
| Approach Reward | *Float* | 0.03 | Per-meter shaping: the chaser is rewarded for closing the gap, the runner for opening it |
| Sight Reward | *Float* | 0.0015 | Paid per tick while the line of sight is clear: the chaser gains it, the runner loses it. This is the dense signal that makes searching worthwhile and cover worth using - without it the chaser's only gradient is a gap it cannot see |
| Idle Penalty | *Float* | 0.001 | Per-tick penalty for the chaser, scaled by how far below *Max Speed* it is. Breaks the "stand still and lose nothing" local optimum a blind chaser falls into |
| Step Reward | *Float* | 0.0005 | Per tick: the runner gains it for staying alive, the chaser pays it, which creates urgency |
| Fall Depth | *Float* | 2.0 | Meters below the start height that count as fallen off the platform, which ends the episode with a penalty for either role |
| Debug Draw | *Toggle* | 1 | Visualize the arena bounds, a marker on each agent, the line to its opponent (solid while in sight) and the remembered position |
| Debug Vector Scale | *Float* | 1.0 | Length (m) of the drive arrow at full deflection |


### See Also


- **[MLAgents::Agent](../../../../api/modules/ml_agents/class.agent.md)**
- **[ChaseArenaBlocks](../../../../api/modules/ml_agents/worlds/class.chasearenablocks.md)**
- **[MLAgents::RaySensor](../../../../api/modules/ml_agents/class.raysensor.md)**


## ChaseAgent Class

---

## protected virtual void configure ( )

Declares two continuous actions driving an XY thrust, and finds the opponent and the arena the agent belongs to.
### Arguments

## protected virtual void onEpisodeBegin ( )

Drops the agent at a free spawn point, clears its memory of the opponent and resets the velocity.
## protected virtual void observe ( )

Writes what the agent knows: its own velocity and place in the arena, whether the opponent is in sight right now, and the remembered sighting with its age. The exact position of an unseen opponent is deliberately left out - finding it is the task.
### Arguments

## protected virtual void act ( )

Applies the thrust, updates the line of sight and the remembered sighting, pays out the approach, sight, idle and step terms according to the role, and ends the episode on a catch or a fall.
### Arguments

## protected virtual void heuristic ( )

Drives towards the opponent as the chaser and away from it as the runner, patrolling towards the remembered position when the opponent is out of sight.
### Arguments

## protected virtual void onDebugDraw ( )

Draws the arena bounds, the line to the opponent - solid while it is in sight - the remembered position, and the applied drive force.
