# Baking Navigation Meshes


The *Experimental Navigation* window lists every navigation mesh of the world and bakes any number of them at once. Both node types are listed together: *[Experimental Navigation Mesh](../../objects/navigations/experimental/navigation_mesh/index.md)* and *[Navigation Mesh](../../objects/navigations/navigation/navigation_mesh/index.md)*. This is the only place where the two stand side by side, and the only way to bake several meshes in one run.


The same parameters and the same *Bake* button are available in the *Bake* section of these nodes.


![](navigation_baking_window.png)

*The Experimental Navigation window*


> **Notice:** Open the window by choosing *Tools -> Experimental Navigation* in the Menu Bar.


### See Also


- The *[Experimental Navigation Mesh](../../objects/navigations/experimental/navigation_mesh/index.md)* node, built by this bake and streamed by tiles
- The *[Navigation Mesh](../../objects/navigations/navigation/navigation_mesh/index.md)* node, which the same bake fills with geometry instead of a mesh made by hand
- The [Navigation Settings](../../editor2/settings/navigation/index.md) section, where the budgets and the worker count of a bake are set
- The *[ExperimentalBakeNavigation](../../api/library/pathfinding/class.experimentalbakenavigation_cpp.md)* class to bake via API
- The *[ExperimentalNavigationBakeSettings](../../api/library/pathfinding/class.experimentalnavigationbakesettings_cpp.md)* class holding the parameters below


## Baking Workflow


A bake traces the ground an agent of a given size can walk on, out of the geometry the world offers it. Nothing is offered by default, so a bake over an untouched scene finishes without an error and leaves the navigation mesh empty.


### Mark the Geometry


Select an object and enable the *Experimental Navigation* section for every surface the navigation mesh has to be built over.


![](experimental_navigation_checkbox.png)

*The Experimental Navigation section of a surface*


The section holds two more fields:


- *[Bake Mask](../../principles/bit_masking/index.md#bake_mask)* decides which navigation meshes take this surface. A navigation mesh bakes a surface only while the two masks share a bit.
- *[Area](../../editor2/settings/navigation/index.md#areas)* sets the area the ground traced over this surface is marked with. An area carries the cost of walking it and the rights a unit needs to enter it.


Terrains are baked into a navigation mesh as well, and the two kinds of terrain are marked differently.


- *[Global Terrain](../../objects/objects/terrain/terrain_global/index.md)* carries one area over its entire surface. Enable the *Experimental Navigation* section for its surface, the same way as for a mesh, and set the *Area* the terrain is baked with.
- *[Landscape Terrain](../../objects/objects/terrain/landscape_terrain/index.md)* enters a bake the same way, by the section on the terrain itself, and the *Area* set there covers the whole terrain just as well. What it adds is a section of its own on every detail mask: the ground painted with a detail takes the *Area* of that detail. This is how a terrain is split into zones, with roads that are quick to cross and rough ground that costs more to walk. With the section on the terrain switched off, no detail mask brings it into a navigation mesh. ![](experimental_navigation_landscape_terrain.png) *The section on the terrain and the section on a detail mask*


> **Notice:** Areas are used by an *Experimental Navigation Mesh* only. A *Navigation Mesh* keeps the shape of the walkable ground and nothing else, so the areas the surfaces are marked with change nothing in it.


### Refine What the Agents Get


[Area Volume](../../objects/navigations/experimental/area_volume/index.md) nodes change the ground a bake produces without touching the geometry of the scene. A volume marks the ground under it with the *Area* it carries, and what that gives depends on the navigation mesh it is baked into.


![](area_volume_cut.png)

*An area volume carrying the Cut area*


- In a *Navigation Mesh* only the *Cut* area has an effect. The ground under such a volume is left out of the mesh, and a volume carrying any other area changes nothing. ![](area_volume_with_navigation_mesh.png) *A Cut volume takes the ground out of a Navigation Mesh*
- In an *Experimental Navigation Mesh* the *Cut* area does the same, and a volume carrying any other area marks the ground instead, which makes it cost more to walk or closes it to a part of the units. | ![](area_volume_with_exp_navigation_mesh.png) *The Cut area takes the ground out* | ![](area_volume_with_exp_navigation_mesh_mark.png) *Any other area marks the ground instead* | |---|---|


A volume reaches a navigation mesh only while their bake masks share a bit, the same way a surface does.


### Add the Navigation Mesh


Use the buttons at the top of this window, or the *Create* menu. Put the node in the middle of the area the agents are going to walk.


![](create_mesh.png)

*The buttons that create a navigation mesh of either kind*


### Adjust the Volume


[Size](#bake_size) sets the box the bake looks inside. The box is centered on the node and follows its axes, so a rotated node bakes a rotated box.


Geometry outside the box is not baked, and a box larger than the level costs tiles that hold nothing. Fit it to the ground the agents need.


![](navmesh_edit_volume.png)

*The bake volume around the ground the agents need*


### Adjust the Bake Parameters


The defaults are a starting point. Start with the agent the ground is carved for: the grid the bake traces along is set from its radius, and everything else is easier to judge once the grid holds the agent. The other thing that usually needs a pass is how closely the trace follows the geometry: the finer it is, the more the navigation mesh holds and the longer the bake takes. All of the parameters are described [below](#bake_parameters).


The section warns when the settings cannot give what they promise, and the warning names the values that would. It is worth reading before the bake rather than after.


### Bake


Select the navigation meshes in the list and press **Bake**. A single navigation mesh is also baked from the *Bake* section of the node itself. The work runs in the background and the editor stays usable while it goes on: the list and the filter are locked, the button turns into **Cancel**, and the tiles built before a cancel are kept. A running bake reports the stage it is at, the meshes and the tiles it has done, and the time it has spent.


![](baking_process.png)

*The progress of a running bake*


The result goes into an asset named after the world and the node, with the `.navmesh` extension for an *Experimental Navigation Mesh* and `.mesh` for a *Navigation Mesh*. A node that has no asset yet gets one created for it and assigned, which is undoable, and the file is imported into the project once the bake is over. A bake that failed is reported to the console, and so is the number of tiles that failed to build while the rest of the mesh went through.


### Check the Result


Select the navigation mesh in the world hierarchy, and its visualizer draws what the bake produced over the scene.


![](experimental_navmesh_result.png) ![](navmesh_result.png)


*The same scene baked into a navigation mesh of either kind*


Two things are worth looking at: the ground the agents need is covered, and the gaps the agents have to pass through are still open. A gap narrower than the agent, or narrower than one cell of the bake grid, is not there after the bake.


This is where the work in the editor ends. Spawning agents, asking for a route and moving anyone along it is done from code, and which classes to reach for depends on the navigation mesh that was baked: *[ExperimentalNavigationPathFetch](../../api/library/pathfinding/class.experimentalnavigationpathfetch_cpp.md)* with *[ExperimentalNavigationMeshCorridor](../../api/library/pathfinding/class.experimentalnavigationmeshcorridor_cpp.md)* for an *Experimental Navigation Mesh*, and *[PathRoute](../../api/library/pathfinding/class.pathroute_cpp.md)* for a *Navigation Mesh*.


## Bake Parameters


These parameters control how the navigation mesh is built. Changes take effect only after you bake it again, and the section shows a warning until you do.


The navigation system is built on the [Recast & Detour](https://github.com/recastnavigation/recastnavigation) library, and a bake is its Recast half. The parameters below carry the names and the meaning they have there, so material written about Recast applies to them as it is.


Four of them describe the agent the ground is carved for. The agent is a cylinder, and the bake knows two things about it: *Agent Radius* and *Agent Height*. It is not a node in the world and the bake does not create one � it is the shape the bake carries over the geometry to decide what stays walkable.


![A side view of the ground with the agent cylinder standing on it: the radius keeps the navigation mesh away from the wall, the height decides what fits under an overhang, the step height is the rise the mesh carries over, and the slope angle is where it stops](bake_agent_size.svg)

*The agent cylinder, one cell of the grid it is measured in, and what the two leave as walkable ground*


The agent comes first and the grid follows from it, not the other way round: *Cell Size* is a fraction of the agent radius, and *Cell Height* is about half of the cell size. How small a fraction depends on how tight the geometry the agent moves through is.


| Geometry | Cell Size | For an agent radius of 0.6 units |
|---|---|---|
| **Open landscapes, terrains, large bake volumes** | Half the agent radius | A cell size of 0.3 units and a cell height of 0.15 |
| **Levels mixing open ground with buildings** | A third of the agent radius | A cell size of 0.2 units and a cell height of 0.1 |
| **Tight interiors, doorways, stairs** | A quarter of the agent radius | A cell size of 0.15 units and a cell height of 0.075 |


The defaults sit on the first row: an agent radius of 0.6 units on a cell size of 0.3, two cells to the radius. Their cell height of 0.2 units is a little coarser than half of that cell size.


> **Notice:** A bake into a [Navigation Mesh](../../objects/navigations/navigation/navigation_mesh/index.md) does not use all of them. It always runs as a static bake, whatever the mode of the node says, and it builds no detail mesh, so *Detail Sample Distance* and *Detail Sample Error* are left out. *Simplification Elevation Ratio* kept at zero is replaced with a value of its own instead of being taken as it is.


| Mask | A surface, a terrain or an area volume takes part in the bake of this navigation mesh only if its [Bake](../../principles/bit_masking/index.md#bake_mask) mask shares a bit with this one. |
|---|---|
| Size | Size of the bake volume along the node-local axes, in units. The volume is centered on the node, and only the geometry inside it is baked. |
| Cell Size | Size of the grid the bake works on, in units. The bake traces the navigation mesh along this grid, so the cell size sets the smallest detail it can pick up: a gap narrower than one cell is lost. The value comes from *Agent Radius*, as [above](#bake_parameters). What decides the result is not the size itself but the number of cells the radius comes out to, which the label under it shows. Below two cells the trace no longer holds the shapes the agent has to fit through, and far above eight the bake takes long for little in return. Smaller cells give a more detailed navigation mesh and cost more. The count grows with the square: halve the cell size and the bake has four times as many cells to go through. > **Notice:** *Max Edge Error* and *Detail Sample Distance* are multipliers of this size, and *Tile Size* is a whole number of these cells, so changing it moves all three. ![](cell_size_1.png) ![](cell_size_2.png) *A smaller cell size follows the geometry closer, at the price of a longer bake* |
| Cell Height | Height of a cell of the same grid, in units. *Cell Size* sets how wide a cell is, this one sets how tall, and about half the cell size is where to start. Heights are counted in whole cells, so this value sets how precisely *Agent Height* and *Max Step Height* are applied, and how closely the navigation mesh follows the ground up and down. *Max Step Height* is rounded down to whole cells. With a coarse cell height the agent gets a lower step than the value you set, and surfaces that should connect can stop connecting. > **Notice:** *Detail Sample Error* is a multiplier of this height. |
| Agent Radius | Radius of the agent the navigation mesh is baked for, in units. The walkable surface is pulled back from walls and ledges by this much, so an agent that follows the navigation mesh keeps clear of them. The value is rounded up to whole cells of *Cell Size*, so the gap can come out a little wider than the value you set. The label shows how many cells that comes out to, as in *Agent Radius (3 cells)*. > **Notice:** The size is baked in and cannot be changed afterwards. A navigation mesh serves every agent up to the size it was baked for, and where a scene holds several, the engine gives each agent the closest fit by itself. Only agents **larger** than the size baked here need a navigation mesh of their own. ![](agent_radius_1.png) ![](agent_radius_2.png) *A larger agent radius pulls the walkable ground further back from the walls, and the same doorway comes out narrower* |
| Agent Height | Height of the agent the navigation mesh is baked for, in units. Ground with less clearance above it is left out of the navigation mesh. Low tunnels and doorways the agent does not fit through are dropped this way. The value is rounded up to whole cells of *Cell Height*, and the label shows how many cells that comes out to. ![](agent_height_1.png) ![](agent_height_2.png) *Ground with less clearance above it than the agent needs is left out, so the canopy is passable for the shorter one only* |
| Max Slope Angle | How steep the ground may be and still count as walkable, in degrees. Anything steeper is thrown out at the very start of the bake. The angle is measured from the up direction of the node, not of the world. Turn the node on its side, and a wall becomes the floor while the floor becomes a wall. A surface exactly at this angle is thrown out along with the steeper ones, so a ramp of 45 degrees needs a value above 45. > **Notice:** The angle alone does not make a slope walkable. The rise a slope gains over one cell has to fit into *Max Step Height* as well, otherwise the slope breaks into steps too tall to walk down and is dropped. The section warns when the two do not agree and names the angle the current settings really reach. ![](max_slope_angle_1.png) ![](max_slope_angle_2.png) *A ramp steeper than the angle allows is dropped, and what it leads to stays unreachable* |
| Max Step Height | How high a step the agent can climb, in units. Two neighboring pieces of ground stay connected while the height difference between them is smaller than this, so the agent can walk from one onto the other. This is what makes stairs walkable. Small things standing on walkable ground work the same way. A kerb or a plank low enough to step onto becomes part of the navigation mesh instead of a hole in it. Slopes are held to the same rule. A slope climbs a little with every cell it crosses, and that rise has to fit into the step as well, otherwise the slope is dropped. See [Max Slope Angle](#max_slope_angle). The value is rounded down to whole cells of *Cell Height*, and the label shows how many cells that comes out to. > **Notice:** A step lower than one *Cell Height* rounds down to zero cells. Nothing at different heights is connected any more, the walkable ground falls apart into tiny patches, and the bake slows to a crawl. The section warns about this and names the lowest value that still works. *A step higher than the agent can climb is left out, and the walkable ground ends at its foot* |
| Tile Size | Side of one tile, in units. The bake volume is cut into square tiles of this size, and each tile is built on its own: the geometry inside it becomes cells, and the cells become polygons. A tile is also the unit of everything that comes after. Tiles are stored in the asset one by one, streaming loads and unloads whole tiles, and a rebuild redoes whole tiles. A tile is a whole number of cells, so the value snaps to *Cell Size* and moves with it. The label shows how many cells that comes out to. Smaller tiles give finer streaming and cheaper rebuilds, and let the bake spread more work over the worker threads. They cost more as well: every tile is built with a margin of neighboring geometry around it, and with small tiles most of the work goes into those margins. Larger tiles carry less of that overhead and cut the polygons in fewer places, but each load and each rebuild takes longer, and streaming brings in more ground than anyone needs. ![](tile_size_1.png) ![](tile_size_2.png) *A smaller tile size cuts the navigation mesh into more tiles, each of them quicker to rebuild, and a larger one into fewer and heavier ones* |
| Partitioning | Inside a tile the walkable ground is one continuous patch. It has to be cut into smaller pieces before polygons can be made, and this setting picks how it is cut. The pieces become the polygons, and agents walk from polygon to polygon, so long thin pieces make paths cling to walls and turn more often than they should. - **Watershed** cuts the ground into the most even pieces and gives the best paths. It is the slowest of the three and the usual choice when the navigation mesh is baked once. - **Monotone** cuts the ground line by line. It is the fastest, but the pieces stretch across the whole tile and come out long and thin. - **Chunky** goes line by line as well, but the tile is first cut into squares and no piece may cross from one square into the next. Almost as fast as monotone, and the pieces stay compact. The two faster ones are worth taking where tiles are rebuilt while the application runs. |
| Region Min Size | Minimum side of a square walkable region, in units. Regions with a smaller area than this side squared are dropped from the navigation mesh, which removes the islands too small to stand on. |
| Region Merge Size | Side of a square walkable region, in units. Regions with a smaller area than this side squared are merged into a neighbor, which lowers the polygon count. > **Notice:** Only *Watershed* partitioning uses this value, and the parameter is shown for it only. |
| Region Chunk Size | Side of the square chunk a tile is split into, in cells. Smaller values keep the polygons more compact and make more of them. > **Notice:** Only *Chunky* partitioning uses this value, and the parameter is shown for it only. |
| Max Edge Error | Maximum deviation of a simplified navigation mesh border from the raw outline of the walkable surface, as a multiplier of *Cell Size* and not in units. Larger values give fewer polygons and a rougher border. |
| Simplification Elevation Ratio | Weight of the vertical deviation when a navigation mesh border is simplified, as a dimensionless ratio. Larger values keep more vertices on slopes, so that a border running over a slope is not simplified into a flat chord that cuts through the geometry. > **Notice:** 0 does not turn the simplification off: it makes it ignore the elevation and follow the outline of the walkable surface in plan only. |
| Detail Sample Distance | Step of the height sampling inside navigation mesh polygons, as a multiplier of *Cell Size* and not in units. Values below 0.9 turn the sampling off, and the interiors of the polygons keep no height detail. |
| Detail Sample Error | Maximum height deviation of the sampled polygon interiors from the walkable surface, as a multiplier of *Cell Height* and not in units. |
| Terrain Sample Scale | Step of the height sampling of terrains, as a multiplier of *Cell Size* and not in units. Lower values follow the relief more closely and cost more samples and more memory. > **Notice:** It affects [Landscape Terrain](../../objects/objects/terrain/landscape_terrain/index.md) and [Global Terrain](../../objects/objects/terrain/terrain_global/index.md) only: meshes are baked from their triangles and ignore it. |
