# Unigine::ExperimentalNavigationAvoidance Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Keeps agents from walking into each other. A path tells an agent where to go and a corridor keeps it on route, but neither knows that another agent is about to step into the same spot; local avoidance is what resolves that, by adjusting the velocity an agent was going to use this frame.


It works on a batch rather than on one agent: crowd behaviour depends on what the neighbours do, so the whole group is solved at once. Fill in the agents, call [compute()](#compute_float_void), then read back the corrected velocities and apply them to your nodes. The class moves nothing by itself.


The method samples candidate velocities and scores them, so its behaviour is shaped by the five weights below rather than by a hard geometric rule. Raise [WeightSeparation](#WeightSeparation) and use [separateOverlappingAgents()](#separateOverlappingAgents_int_void) for dense crowds, where the default weights let agents press into one another.


## ExperimentalNavigationAvoidance Class

### Members

## void setDensityCellSize ( float size )

Sets a new size of a cell of the density map. It controls how finely crowding is measured � too coarse and a tight knot of agents disappears into the average, too fine and the map costs memory for nothing.
### Arguments

- *float* **size** - The density cell size, in units. The default value is 30.

## float getDensityCellSize () const

Returns the current size of a cell of the density map. It controls how finely crowding is measured � too coarse and a tight knot of agents disappears into the average, too fine and the map costs memory for nothing.
### Return value

Current density cell size, in units. The default value is 30.
## void setDensityEnabled ( int enabled )

Sets a new value indicating if the density map is built. It costs extra work per frame and is only worth enabling when something actually reads the density � steering a crowd away from a jam, for instance.
### Arguments

- *int* **enabled** - The building of the density map

## int isDensityEnabled () const

Returns the current value indicating if the density map is built. It costs extra work per frame and is only worth enabling when something actually reads the density � steering a crowd away from a jam, for instance.
### Return value

Current building of the density map
## void setMaxNeighbors ( int neighbors )

Sets a new largest number of neighbours a single agent takes into account. In a dense crowd only the nearest few matter, and capping the count is what keeps the cost per agent bounded.
### Arguments

- *int* **neighbors** - The maximum number of neighbours. The default value is 6.

## int getMaxNeighbors () const

Returns the current largest number of neighbours a single agent takes into account. In a dense crowd only the nearest few matter, and capping the count is what keeps the cost per agent bounded.
### Return value

Current maximum number of neighbours. The default value is 6.
## void setNavigationMask ( int mask )

Sets a new mask that selects the navigation meshes whose boundaries the agents are kept inside. Without it, avoidance can push an agent off the walkable surface while dodging a neighbour.
### Arguments

- *int* **mask** - The navigation mask. The default value is 0, so the walkable surface is not taken into account.

## int getNavigationMask () const

Returns the current mask that selects the navigation meshes whose boundaries the agents are kept inside. Without it, avoidance can push an agent off the walkable surface while dodging a neighbour.
### Return value

Current navigation mask. The default value is 0, so the walkable surface is not taken into account.
## void setNeighborRange ( float range )

Sets a new distance within which another agent counts as a neighbour. It should cover roughly how far an agent travels during the prediction time � anything further away cannot reach it in time to matter.
### Arguments

- *float* **range** - The neighbour range, in units. The default value is 6.

## float getNeighborRange () const

Returns the current distance within which another agent counts as a neighbour. It should cover roughly how far an agent travels during the prediction time � anything further away cannot reach it in time to matter.
### Return value

Current neighbour range, in units. The default value is 6.
## void setNumAgents ( int agents )

Sets a new number of agents in the batch. Changing it resizes the internal arrays, so it is set once for a crowd rather than every frame.
### Arguments

- *int* **agents** - The number of agents.

## int getNumAgents () const

Returns the current number of agents in the batch. Changing it resizes the internal arrays, so it is set once for a crowd rather than every frame.
### Return value

Current number of agents.
## void setObstacleMask ( int mask )

Sets a new mask of the [Obstacle](../../../api/library/pathfinding/class.obstacle_usc.md) nodes the agents steer around. The value 0 makes avoidance ignore obstacles and take only other agents into account.
### Arguments

- *int* **mask** - The obstacle mask. The default value is 0.

## int getObstacleMask () const

Returns the current mask of the [Obstacle](../../../api/library/pathfinding/class.obstacle_usc.md) nodes the agents steer around. The value 0 makes avoidance ignore obstacles and take only other agents into account.
### Return value

Current obstacle mask. The default value is 0.
## void setPredictionTime ( float time )

Sets a new how far ahead a possible collision is looked for. A short horizon makes agents react late and sharply, a long one makes them swerve around neighbours they would never have met.
### Arguments

- *float* **time** - The prediction horizon, in seconds. The default value is 2.5.

## float getPredictionTime () const

Returns the current how far ahead a possible collision is looked for. A short horizon makes agents react late and sharply, a long one makes them swerve around neighbours they would never have met.
### Return value

Current prediction horizon, in seconds. The default value is 2.5.
## void setWeightCurrentVelocity ( float velocity )

Sets a new weight of staying close to the velocity the agent already had. It buys smooth motion at the price of a slower reaction.
### Arguments

- *float* **velocity** - The weight of the current velocity. The default value is 0.75.

## float getWeightCurrentVelocity () const

Returns the current weight of staying close to the velocity the agent already had. It buys smooth motion at the price of a slower reaction.
### Return value

Current weight of the current velocity. The default value is 0.75.
## void setWeightDesiredVelocity ( float velocity )

Sets a new weight of following the velocity the agent asked for. The higher it is, the more stubbornly the agent holds its own course instead of yielding.
### Arguments

- *float* **velocity** - The weight of the desired velocity. The default value is 2.

## float getWeightDesiredVelocity () const

Returns the current weight of following the velocity the agent asked for. The higher it is, the more stubbornly the agent holds its own course instead of yielding.
### Return value

Current weight of the desired velocity. The default value is 2.
## void setWeightSeparation ( float separation )

Sets a new weight of keeping clear of neighbours even when no collision is predicted. Raising it is the first thing to try when a dense crowd packs too tightly.
### Arguments

- *float* **separation** - The weight of separation. The default value is 0.

## float getWeightSeparation () const

Returns the current weight of keeping clear of neighbours even when no collision is predicted. Raising it is the first thing to try when a dense crowd packs too tightly.
### Return value

Current weight of separation. The default value is 0.
## void setWeightSide ( float side )

Sets a new weight of preferring a sideways dodge over slowing down. It is what makes oncoming agents step around each other instead of stopping nose to nose.
### Arguments

- *float* **side** - The weight of sideways motion. The default value is 0.75.

## float getWeightSide () const

Returns the current weight of preferring a sideways dodge over slowing down. It is what makes oncoming agents step around each other instead of stopping nose to nose.
### Return value

Current weight of sideways motion. The default value is 0.75.
## void setWeightTimeToImpact ( float impact )

Sets a new weight of postponing the moment of collision. The higher it is, the earlier and more cautiously an agent reacts to what is coming.
### Arguments

- *float* **impact** - The weight of the time to impact. The default value is 2.5.

## float getWeightTimeToImpact () const

Returns the current weight of postponing the moment of collision. The higher it is, the earlier and more cautiously an agent reacts to what is coming.
### Return value

Current weight of the time to impact. The default value is 2.5.
---

## static ExperimentalNavigationAvoidance ( )

The ExperimentalNavigationAvoidance constructor. Creates an empty solver with no agents.
## void compute ( float ifps )

Solves the batch and leaves the corrected velocity of every agent ready to be read. Call it once a frame, after every agent has been filled in.
### Arguments

- *float* **ifps** - Length of the frame the solve is made for, in seconds.

## float getAgentDensity ( Vec3 position )

Returns how crowded a place is according to the density map. Requires [DensityEnabled](#DensityEnabled); use it to route agents around a jam instead of into it.
### Arguments

- *Vec3* **position** - Position to sample, in world coordinates.

### Return value

Crowd density at the position.
## Vec3 getAgentPosition ( int num )

Returns the position of an agent as the solver holds it. It differs from what was passed in only after [separateOverlappingAgents()](#separateOverlappingAgents_int_void) has pushed agents apart.
### Arguments

- *int* **num** - Agent number.

### Return value

Agent position in world coordinates.
## vec3 getAgentVelocity ( int num )

Returns the corrected velocity of an agent � the result of the solve, and what the agent should actually be moved with this frame.
### Arguments

- *int* **num** - Agent number.

### Return value

Velocity the agent should use this frame.
## void separateOverlappingAgents ( int iterations = 4 )

Pushes agents that already overlap apart. Avoidance prevents collisions but cannot undo the ones that are already there � agents spawned on top of each other, or squeezed together by a moving wall. Read the results back with [getAgentPosition()](#getAgentPosition_int_Vec3).
### Arguments

- *int* **iterations** - Number of passes to make. More passes separate a dense knot better and cost more.

## void setAgent ( int num , Vec3 position , float radius , float height , vec3 velocity , vec3 desired_velocity , float max_speed , float max_acceleration )

Fills in an agent of the batch. Call it for every agent each frame before solving � the solver keeps no state between frames beyond what is passed here.
### Arguments

- *int* **num** - Agent number.
- *Vec3* **position** - Current position of the agent, in world coordinates.
- *float* **radius** - Radius of the agent, in units.
- *float* **height** - Height of the agent, in units.
- *vec3* **velocity** - Velocity the agent is moving with right now.
- *vec3* **desired_velocity** - Velocity the agent would use if nothing were in the way � usually the direction to the next corner of its corridor, scaled to its speed.
- *float* **max_speed** - Highest speed the agent may be given, in units per second.
- *float* **max_acceleration** - Highest change of velocity allowed per second. It keeps the corrected velocity from jumping and the motion from looking abrupt.

## void setAgentExcludeAgent ( int num , int other )

Makes an agent ignore one specific neighbour. Use it for a pair that is meant to converge, such as a unit walking up to the character it is escorting.
### Arguments

- *int* **num** - Agent number.
- *int* **other** - Number of the agent to be ignored.

## void setAgentExcludeObstacle ( int num , Obstacle obstacle )

Makes an agent ignore one specific obstacle � typically the obstacle attached to the agent itself, which it would otherwise try to escape.
### Arguments

- *int* **num** - Agent number.
- *[Obstacle](../../../api/library/pathfinding/class.obstacle_usc.md)* **obstacle** - Obstacle to be ignored.

## void setAgentInteractionMask ( int num , int mask )

Sets which other agents this one has to avoid. Two agents take each other into account only when their masks share a bit, which is how groups are made to pass through one another � allies and enemies, ground units and flyers.
### Arguments

- *int* **num** - Agent number.
- *int* **mask** - Mask of the agents this one avoids.

## void setAgentPriority ( int num , float priority )

Sets how much of the dodging an agent leaves to the others. Where two agents meet, the one with the lower priority does most of the yielding, which is how a leader keeps its line while its followers step aside.
### Arguments

- *int* **num** - Agent number.
- *float* **priority** - Priority of the agent. The higher it is, the more the neighbours give way.
