# Unigine::ExperimentalNavigationAvoidance Class (CS)


Keeps agents from walking into each other. A path tells an agent where to go and a corridor keeps it on route, but neither knows that another agent is about to step into the same spot; local avoidance is what resolves that, by adjusting the velocity an agent was going to use this frame.


It works on a batch rather than on one agent: crowd behaviour depends on what the neighbours do, so the whole group is solved at once. Fill in the agents, call [compute()](#compute_float_void), then read back the corrected velocities and apply them to your nodes. The class moves nothing by itself.


The method samples candidate velocities and scores them, so its behaviour is shaped by the five weights below rather than by a hard geometric rule. Raise [WeightSeparation](#WeightSeparation) and use [separateOverlappingAgents()](#separateOverlappingAgents_int_void) for dense crowds, where the default weights let agents press into one another.


## ExperimentalNavigationAvoidance Class

### Properties

## float DensityCellSize

The size of a cell of the density map. It controls how finely crowding is measured � too coarse and a tight knot of agents disappears into the average, too fine and the map costs memory for nothing.
## bool DensityEnabled

The value indicating if the density map is built. It costs extra work per frame and is only worth enabling when something actually reads the density � steering a crowd away from a jam, for instance.
## int MaxNeighbors

The largest number of neighbours a single agent takes into account. In a dense crowd only the nearest few matter, and capping the count is what keeps the cost per agent bounded.
## int NavigationMask

The mask that selects the navigation meshes whose boundaries the agents are kept inside. Without it, avoidance can push an agent off the walkable surface while dodging a neighbour.
## float NeighborRange

The distance within which another agent counts as a neighbour. It should cover roughly how far an agent travels during the prediction time � anything further away cannot reach it in time to matter.
## int NumAgents

The number of agents in the batch. Changing it resizes the internal arrays, so it is set once for a crowd rather than every frame.
## int ObstacleMask

The mask of the [Obstacle](../../../api/library/pathfinding/class.obstacle_cs.md) nodes the agents steer around. The value 0 makes avoidance ignore obstacles and take only other agents into account.
## float PredictionTime

The how far ahead a possible collision is looked for. A short horizon makes agents react late and sharply, a long one makes them swerve around neighbours they would never have met.
## float WeightCurrentVelocity

The weight of staying close to the velocity the agent already had. It buys smooth motion at the price of a slower reaction.
## float WeightDesiredVelocity

The weight of following the velocity the agent asked for. The higher it is, the more stubbornly the agent holds its own course instead of yielding.
## float WeightSeparation

The weight of keeping clear of neighbours even when no collision is predicted. Raising it is the first thing to try when a dense crowd packs too tightly.
## float WeightSide

The weight of preferring a sideways dodge over slowing down. It is what makes oncoming agents step around each other instead of stopping nose to nose.
## float WeightTimeToImpact

The weight of postponing the moment of collision. The higher it is, the earlier and more cautiously an agent reacts to what is coming.
### Members

---

## ExperimentalNavigationAvoidance ( )

The ExperimentalNavigationAvoidance constructor. Creates an empty solver with no agents.
## void Compute ( float ifps )

Solves the batch and leaves the corrected velocity of every agent ready to be read. Call it once a frame, after every agent has been filled in.
### Arguments

- *float* **ifps** - Length of the frame the solve is made for, in seconds.

## float GetAgentDensity ( vec3 position )

Returns how crowded a place is according to the density map. Requires [DensityEnabled](#DensityEnabled); use it to route agents around a jam instead of into it.
### Arguments

- *vec3* **position** - Position to sample, in world coordinates.

### Return value

Crowd density at the position.
## vec3 GetAgentPosition ( int num )

Returns the position of an agent as the solver holds it. It differs from what was passed in only after [separateOverlappingAgents()](#separateOverlappingAgents_int_void) has pushed agents apart.
### Arguments

- *int* **num** - Agent number.

### Return value

Agent position in world coordinates.
## vec3 GetAgentVelocity ( int num )

Returns the corrected velocity of an agent � the result of the solve, and what the agent should actually be moved with this frame.
### Arguments

- *int* **num** - Agent number.

### Return value

Velocity the agent should use this frame.
## void SeparateOverlappingAgents ( int iterations = 4 )

Pushes agents that already overlap apart. Avoidance prevents collisions but cannot undo the ones that are already there � agents spawned on top of each other, or squeezed together by a moving wall. Read the results back with [getAgentPosition()](#getAgentPosition_int_Vec3).
### Arguments

- *int* **iterations** - Number of passes to make. More passes separate a dense knot better and cost more.

## void SetAgent ( int num , vec3 position , float radius , float height , vec3 velocity , vec3 desired_velocity , float max_speed , float max_acceleration )

Fills in an agent of the batch. Call it for every agent each frame before solving � the solver keeps no state between frames beyond what is passed here.
### Arguments

- *int* **num** - Agent number.
- *vec3* **position** - Current position of the agent, in world coordinates.
- *float* **radius** - Radius of the agent, in units.
- *float* **height** - Height of the agent, in units.
- *vec3* **velocity** - Velocity the agent is moving with right now.
- *vec3* **desired_velocity** - Velocity the agent would use if nothing were in the way � usually the direction to the next corner of its corridor, scaled to its speed.
- *float* **max_speed** - Highest speed the agent may be given, in units per second.
- *float* **max_acceleration** - Highest change of velocity allowed per second. It keeps the corrected velocity from jumping and the motion from looking abrupt.

## void SetAgentExcludeAgent ( int num , int other )

Makes an agent ignore one specific neighbour. Use it for a pair that is meant to converge, such as a unit walking up to the character it is escorting.
### Arguments

- *int* **num** - Agent number.
- *int* **other** - Number of the agent to be ignored.

## void SetAgentExcludeObstacle ( int num , Obstacle obstacle )

Makes an agent ignore one specific obstacle � typically the obstacle attached to the agent itself, which it would otherwise try to escape.
### Arguments

- *int* **num** - Agent number.
- *[Obstacle](../../../api/library/pathfinding/class.obstacle_cs.md)* **obstacle** - Obstacle to be ignored.

## void SetAgentInteractionMask ( int num , int mask )

Sets which other agents this one has to avoid. Two agents take each other into account only when their masks share a bit, which is how groups are made to pass through one another � allies and enemies, ground units and flyers.
### Arguments

- *int* **num** - Agent number.
- *int* **mask** - Mask of the agents this one avoids.

## void SetAgentPriority ( int num , float priority )

Sets how much of the dodging an agent leaves to the others. Where two agents meet, the one with the lower priority does most of the yielding, which is how a leader keeps its line while its followers step aside.
### Arguments

- *int* **num** - Agent number.
- *float* **priority** - Priority of the agent. The higher it is, the more the neighbours give way.
