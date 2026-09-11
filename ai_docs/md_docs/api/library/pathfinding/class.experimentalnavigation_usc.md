# Unigine::ExperimentalNavigation Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


> **Notice:** Not to be confused with the legacy [Navigation](../../../api/library/pathfinding/class.navigation_usc.md) node class: despite the similar name they are unrelated.


World-wide settings of the navigation system: the registry of areas and flags, the budgets that pace tile streaming, and the memory the navigation data is allowed to hold.


The registry is what gives numbers meaning. A polygon carries a six-bit area index and a set of flags, and nothing more; the name behind index 4, what crossing it costs, and which flags it implies all live here, in one place shared by the whole world. Areas are the traversal cost � mud is three times a road � while flags are the yes-or-no rights a query filters on. There are 64 areas and 16 flags, and two indices are reserved: one for the default area and one for the polygons cut away by obstacles.


## ExperimentalNavigation Class

### Members

## int getCutAreaIndex () const

Returns the area index reserved for the polygons cut away by obstacles and carving volumes. Such polygons stay in the data but are marked with this area, so a query can tell a hole from ordinary ground.
### Return value

reserved cut area index.
## int getDefaultAreaIndex () const

Returns the area index every polygon gets unless something assigns it another one � a surface marked on an object, a detail mask, or an area volume.
### Return value

default area index.
## void setInvalidateBudget ( float budget )

Sets a new time per frame the engine may spend rebuilding the tiles that area volumes and moved obstacles have made dirty. It bounds the frame cost of a world that keeps changing. Mapped to the *navigation_invalidate_budget* console variable.
### Arguments

- *float* **budget** - The invalidation budget, in seconds. The default value is 0.004.

## float getInvalidateBudget () const

Returns the current time per frame the engine may spend rebuilding the tiles that area volumes and moved obstacles have made dirty. It bounds the frame cost of a world that keeps changing. Mapped to the *navigation_invalidate_budget* console variable.
### Return value

Current invalidation budget, in seconds. The default value is 0.004.
## int isStreamingMemoryLimitReached () const

Returns the current value indicating if the navigation data has hit the memory limit. Once it has, tiles stop being loaded, and queries in the affected region start failing for lack of data rather than for lack of a route.
### Return value

Current the memory limit is reached
## int getNumActiveTasks () const

Returns the current number of navigation tasks the workers are running right now � path searches, tile builds, and avoidance batches alike.
### Return value

Current number of active tasks.
## int getNumAreas () const

Returns the current size of the area registry. The limit comes from the six bits a polygon has to store its area index in.
### Return value

Current number of areas. Always 64.
## int getNumFlags () const

Returns the current size of the flag registry.
### Return value

Current number of flags. Always 16.
## int getNumNavigationMeshes () const

Returns the current number of navigation meshes present in the world.
### Return value

Current number of navigation meshes.
## void setStreamingBudget ( float budget )

Sets a new time per frame the engine may spend loading and unloading navigation mesh tiles. It bounds what streaming costs when an invoker moves fast through a large world. Mapped to the *navigation_streaming_budget* console variable.
### Arguments

- *float* **budget** - The streaming budget, in seconds. The default value is 0.002.

## float getStreamingBudget () const

Returns the current time per frame the engine may spend loading and unloading navigation mesh tiles. It bounds what streaming costs when an invoker moves fast through a large world. Mapped to the *navigation_streaming_budget* console variable.
### Return value

Current streaming budget, in seconds. The default value is 0.002.
## void setStreamingMemoryLimit ( int limit )

Sets a new amount of memory the tiles and voxels of every navigation mesh together are allowed to hold. Mapped to the *navigation_streaming_memory_limit* console variable.
### Arguments

- *int* **limit** - The memory limit, in megabytes. The default value is 0, which means no limit.

## int getStreamingMemoryLimit () const

Returns the current amount of memory the tiles and voxels of every navigation mesh together are allowed to hold. Mapped to the *navigation_streaming_memory_limit* console variable.
### Return value

Current memory limit, in megabytes. The default value is 0, which means no limit.
## Event<int> getEventAreaChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## Event<int> getEventFlagChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## Event<> getEventRegistryChanged () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## vec4 engine.navigation. getAreaColor ( int area_index )

Returns the color an area is drawn with by the navigation mesh visualizer. Colors are what make areas legible on screen � mud, road, and water are told apart by eye rather than by index.
### Arguments

- *int* **area_index** - Area index.

### Return value

Color of the area.
## float engine.navigation. getAreaCost ( int area_index )

Returns the traversal cost shared by the whole world for an area. A single query can depart from it via the area cost override of its filter.
### Arguments

- *int* **area_index** - Area index.

### Return value

Traversal cost of the area.
## int engine.navigation. getAreaFlags ( int area_index )

Returns the flags every polygon of an area carries. Tying flags to an area saves marking each polygon by hand: making an area impassable for swimmers is one setting rather than a pass over the data.
### Arguments

- *int* **area_index** - Area index.

### Return value

Flags implied by the area.
## int engine.navigation. getAreaIndex ( string name )

Returns the index of a named area. Looking the index up by name keeps game code free of the numbers the registry happens to use.
### Arguments

- *string* **name** - Area name.

### Return value

Area index, or -1 if no area carries that name.
## string engine.navigation. getAreaName ( int area_index )

Returns the name of an area. Names exist for the editor and for lookups; the engine itself only ever works with the index.
### Arguments

- *int* **area_index** - Area index.

### Return value

Area name, or an empty string if the area is unnamed.
## vec4 engine.navigation. getDefaultAreaColor ( int area_index )

Returns the color an area is given before anything overrides it.
### Arguments

- *int* **area_index** - Area index.

### Return value

Default color of the area.
## int engine.navigation. getFlagIndex ( string name )

Returns the index of a named flag.
### Arguments

- *string* **name** - Flag name.

### Return value

Flag index, or -1 if no flag carries that name.
## int engine.navigation. getFlagMask ( string name )

Returns the bit of a named flag as a ready-made mask. It is what goes into the include and exclude masks of a filter, so the shift does not have to be written out by hand.
### Arguments

- *string* **name** - Flag name.

### Return value

Mask with the bit of the flag set, or 0 if no flag carries that name.
## string engine.navigation. getFlagName ( int flag_index )

Returns the name of a flag.
### Arguments

- *int* **flag_index** - Flag index.

### Return value

Flag name, or an empty string if the flag is unnamed.
## ExperimentalNavigationMesh engine.navigation. getNavigationMesh ( int num )

Returns a navigation mesh of the world by its number. Together with the count above it lets the whole set be walked without searching the node tree.
### Arguments

- *int* **num** - Navigation mesh number.

### Return value

Navigation mesh in the world.
## int engine.navigation. loadSettings ( string path )

Loads the registry of areas and flags from a file, replacing the current one. Keeping the registry in a file lets several worlds share one set of area definitions.
### Arguments

- *string* **path** - Path to the settings file.

### Return value

true if the settings were loaded; otherwise, false.
## int engine.navigation. restoreState ( Stream stream )

Restores the state of the navigation system from a stream.
### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream to restore the state from.

### Return value

true if the state was restored; otherwise, false.
## int engine.navigation. saveSettings ( string path )

Saves the registry of areas and flags to a file.
### Arguments

- *string* **path** - Path to the settings file.

### Return value

true if the settings were saved; otherwise, false.
## int engine.navigation. saveState ( Stream stream )

Saves the state of the navigation system into a stream. Baked tiles are not part of it � they are rebuilt or reloaded rather than stored in a save.
### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream to save the state into.

### Return value

true if the state was saved; otherwise, false.
## void engine.navigation. setAreaColor ( int area_index , vec4 color )

Sets the color an area is drawn with by the navigation mesh visualizer.
### Arguments

- *int* **area_index** - Area index.
- *vec4* **color** - Color to draw the area with.

## void engine.navigation. setAreaCost ( int area_index , float cost )

Sets the traversal cost of an area for the whole world. Costs below 1 make the search prefer the area and require the heuristic scale to be adjusted, otherwise the result stops being optimal.
### Arguments

- *int* **area_index** - Area index.
- *float* **cost** - Traversal cost multiplier. The higher the cost, the more willingly the search routes around the area.

## void engine.navigation. setAreaFlags ( int area_index , int flags )

Sets the flags implied by an area.
### Arguments

- *int* **area_index** - Area index.
- *int* **flags** - Flags every polygon of the area carries.

## void engine.navigation. setAreaName ( int area_index , string name )

Gives an area a name it can be looked up by.
### Arguments

- *int* **area_index** - Area index.
- *string* **name** - Name to be given to the area.

## void engine.navigation. setFlagName ( int flag_index , string name )

Gives a flag a name it can be looked up by.
### Arguments

- *int* **flag_index** - Flag index.
- *string* **name** - Name to be given to the flag.
