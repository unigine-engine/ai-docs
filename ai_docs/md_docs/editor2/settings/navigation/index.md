# Navigation Settings (Experimental)


The *ExperimentalNavigation* section of the *Settings* window holds what the experimental navigation system shares across the whole world: how much time and memory it is allowed to spend, and the list of areas the ground can be marked with.


![The Experimental Navigation section of the Settings window: the preset field, the four budgets and the list of areas](navigation_settings.png)

*The section holds the preset, the budgets and the areas of the world*


> **Notice:** Open the *Settings* window by choosing *Window -> Settings* in the main menu and select the *Runtime -> World -> Experimental Navigation* section. These are world settings: they are saved with the world.


### See Also


- The [Experimental Navigation](../../../objects/navigations/experimental/index.md) nodes the settings apply to
- The *[ExperimentalNavigation](../../../api/library/pathfinding/class.experimentalnavigation_cpp.md)* class to read and change the areas via API


## Budgets


Navigation work is spread over frames instead of being done at once. These four values set how much of it fits into a frame.


![Streaming Budget, Invalidate Budget, Streaming Memory Limit and Bake Workers with their default values](budget_settings.png)

*The four budgets at their default values*


| Streaming Budget | Time per frame given to loading and unloading the tiles of navigation meshes with streaming on, in seconds. Tiles that do not fit into the budget arrive over the following frames. |
|---|---|
| Invalidate Budget | Time per frame given to rebuilding the tiles that area volumes changed, in seconds. Tiles that do not fit into the budget wait for the following frames. |
| Streaming Memory Limit | Memory the loaded tiles of all navigation meshes are allowed to hold, in megabytes. Streaming stops loading once the limit is reached, so a low value leaves the navigation mesh with holes. 0 is no limit. |
| Bake Workers | Worker threads a navigation mesh bake is allowed to spread its tiles over. Capping it leaves room for the rest of the application while a bake runs in the background. 0 is every worker of the background pool. |


## Areas


An area is what makes a stretch of ground different from the ground next to it: mud, a road, a patch under fire. Every polygon of every navigation mesh carries one, and what stands behind it is set here, in one list shared by the whole world or a navigation preset.


There are 64 areas, numbered from 0 to 63, and two of them are reserved. Area 0 is *Cut*: ground marked with it is taken out of the navigation mesh instead of being marked, which is why the list leaves it out, although it can be picked wherever an area is chosen. Area 63 is *Default*: ground carries it until something marks it otherwise. The other 62 are free for the project.


![The list of areas with the ID, Name, Cost, Color and Flags columns, eight areas defined and the rest empty](areas_settings.png)

*Areas defined for a world, with a cost, a color and flags each. Rows with no name are not defined yet*


Marking the ground with an area is the job of the [Navigation Mesh Area Volume](../../../objects/navigations/experimental/area_volume/index.md) node, of the surfaces of objects, and of the detail masks of terrains.


| ID | Number of the area. It is what the nodes and the API refer to, and it cannot be changed. |
|---|---|
| Name | Name of the area, shown everywhere the area is picked. An area with no name is not defined: its row stays empty and it offers neither color nor flags. Giving it a name is what defines it. > **Notice:** The name of the *Default* area cannot be changed. Every polygon gets that area unless something marks it otherwise. |
| Cost | What crossing this ground costs a search, as a multiplier of the distance. 1 is ordinary ground, 3 means the search treats a meter here as three, and takes a detour of up to three times the length to avoid it. |
| Color | Color the area is drawn with by the navigation mesh visualizer. |
| Flags | Sixteen flags of the area, each with a name of its own. A flag is not a cost but a yes or no: it decides whether a query may use this ground at all. Every path query carries two sets of flags, the accepted ones and the refused ones. Ground is open to that query while it carries at least one accepted flag and not a single refused one. Until it is told otherwise, a query accepts every flag and refuses none. Mark water with a flag of its own, and a walking agent can then be told to refuse that flag while a swimming one accepts it. Both walk the same navigation mesh. > **Notice:** A newly defined area carries no flags at all, and ground with no flags is open to nobody. Give a new area at least one flag, or everything marked with it drops out of every path. The *Default* area comes with the *Walkable* flag for that reason. |


**Which** area a piece of ground carries is written into the navigation mesh while it is baked. The name, the cost, the color and the flags behind that area are not: they live in this list, and the navigation mesh picks them up as they change.


So editing the list takes effect at once and asks for no rebake. Marking different ground with an area is a change of the navigation mesh itself, and that does need one.


## Preset


The *Experimental Navigation Preset* field at the top of the section works the same way as the presets of the other settings sections. It decides where what the section holds is kept: in the current `.world` file or in a `.navigation` preset of its own, which other worlds can use as well.


![The Experimental Navigation Preset field reading From World, with the Save, Save As New and Revert buttons beside it](navigation_preset.png)


With a preset assigned, the list of areas comes from the asset and not from the world. Saving, loading and reverting a preset are described in [Settings and Preferences](../../../editor2/settings/index.md).
