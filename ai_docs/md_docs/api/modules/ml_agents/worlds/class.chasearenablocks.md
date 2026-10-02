# ChaseArenaBlocks Class

**Inherits from:** ComponentBase


ChaseArenaBlocks builds the obstacle field of the Chase world: it measures the arena floor, scatters a new set of blocks on a grid at the start of every episode, and hands out spawn points clear of them.


Randomizing the layout is what the cover in that world is for. With a fixed field the pair would learn one arrangement of walls; with a new one each episode the runner has to use cover it has not seen before and the chaser has to search it.


The obstacle pool is loaded from node assets rather than authored into the scene, so its size is not baked into the world and a curriculum can ask for more clutter than anyone placed by hand. The component goes on the training area node itself, next to **[TrainingArea](../../../../api/modules/ml_agents/class.trainingarea.md)**.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Arena Size | *Vec2* | 0.0, 0.0 | Full XY extents (m) of the arena. 0 measures them from the bound box of the `floor` children, which is the normal setup - resize the floor and everything follows |
| Block Assets | *File* array |  | Node assets the obstacle pool is loaded from at initialization, cycled in order. Leave it empty to use blocks authored as children instead |
| Pool Size | *Int* | 36 | How many obstacles to load from *Block Assets*. This is the ceiling *Max Active* is clamped to, not the count placed in an episode |
| Cell | *Float* | 1.0 | Grid step (m). Blocks and spawns snap to this grid, and block footprints are rounded up to whole cells |
| Border | *Float* | 1.5 | Keep-clear band (m) along the walls: no block and no spawn lands inside it |
| Block Gap | *Float* | 2.0 | Free space (m) kept between two placed blocks, so the field never grows a solid clump the agents cannot walk through |
| Min Active | *Int* | 14 | Fewest blocks placed in an episode, the rest being hidden. Varies the clutter |
| Max Active | *Int* | 30 | Most blocks placed in an episode, clamped to the pool size |
| Rotate Blocks | *Toggle* | 1 | Also roll a random 90-degree yaw per block, so non-square blocks vary their orientation |
| Spawn Gap | *Float* | 12.0 | Preferred distance (m) between the spawn points handed to the two agents. Relaxed gradually if the field is too crowded to honor it |
| Debug Draw | *Toggle* | 0 | Outline the placement grid, the footprint of every placed block and the spawn points |


### See Also


- **[ChaseAgent](../../../../api/modules/ml_agents/worlds/class.chaseagent.md)**
- **[MLAgents::TrainingArea](../../../../api/modules/ml_agents/class.trainingarea.md)**


## ChaseArenaBlocks Class

---

## isValid ( )

Returns a value indicating if the component has a usable placement grid.
### Return value

true if the arena was measured and a grid built; otherwise, false.
## getCenter ( )

Returns the center of the measured arena.
### Return value

World position of the arena center.
## getSize ( )

Returns the size of the arena, whether it was measured from the floor or taken from *Arena Size*.
### Return value

Full XY extents (m) of the arena.
## pickSpawn ( )

Picks a spawn point clear of the placed blocks and of the point handed out before it, keeping the two agents *Spawn Gap* apart where the layout allows.
### Arguments

### Return value

true if a point was found; otherwise, false.
## isFree ( )

Checks whether a position has enough free space around it.
### Arguments

### Return value

true if nothing is placed within the given radius; otherwise, false.
