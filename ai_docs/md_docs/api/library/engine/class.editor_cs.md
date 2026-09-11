# Unigine::Editor Class (CS)

> **Notice:** This class is a singleton.


This class provides functionality for the [editor script](../../../code/fundamentals/execution_sequence/app_logic_system.md#editor_logic) that loads and manages the hierarchy of nodes displayed in the editor.


> **Notice:** C++ methods running editor script functions are described in the *[Engine](../../../api/library/engine/class.engine_cs.md)* class reference.


## Editor Class

### Properties

## Player Player

The player used in the Editor mode at the moment.
> **Notice:** Editor player is handled differently than in-game players. Parameters set directly for the player are ignored; instead, *Editor* player uses [Camera](../../../editor2/camera_settings/index.md) parameters set via the interface. (See Editor scripts in `data/core/editor` folder for implementation.)


## Player VRPlayer

The player used to render VR in the Editor mode at the moment.
If VR Player has not been set, VR is rendered to the [Editor Player](#getPlayer_Player); if the *Editor* Player hasn't been set either, the [Game Player](../../../api/library/engine/class.game_cs.md#getPlayer_Player) is used for rendering.


> **Notice:** Editor player is handled differently than in-game players. Parameters set directly for the player are ignored; instead, Editor player uses [Camera](../../../editor2/camera_settings/index.md) parameters set via the interface. (See Editor scripts in `data/core/editor` folder for implementation.)


## string Data

The user string data associated with the world. this string is written directly into the data tag of the `*.world` file.
## bool Enabled

The value of the *Enabled* parameter. The *Enabled* parameter controls all internal additional engine processing (for example, reloading of textures when their recording time is changed and so on). For example, the *Enabled* parameter can be set to 0 when using Syncker in order to increase engine performance (as Syncker operates inside the editor environment and can reduce engine performance).
## 🔒︎ bool IsLoaded

The value indicating if the editor is already loaded.
### Members

---

## void Load ( string script = "editor/editor.usc" )

Loads the editor from the specified script.
### Arguments

- *string* **script** - Path to the script.

## void Quit ( )

Quit the editor.
## void Reload ( )

Reloads the Unigine Editor. This functions updates node hierarchy, updates loaded textures if they were modified, etc.
## int NeedReload ( )

Returns a value indicating if Unigine Editor should be reloaded.
### Return value

**1** if the editor should be reloaded; otherwise, **0**.
## void AddEditorPlayer ( Player player )

Adds another editor player.
### Arguments

- *[Player](../../../api/library/players/class.player_cs.md)* **player** - Player instance.

## void RemoveEditorPlayer ( Player player )

Removes a given player from the editor.
### Arguments

- *[Player](../../../api/library/players/class.player_cs.md)* **player** - Player instance.

## bool IsEditorPlayer ( Player player )

Returns a value indicating if the given player is an Editor player.
### Arguments

- *[Player](../../../api/library/players/class.player_cs.md)* **player** - Player instance.

### Return value

true if the *Player* is an Editor player; otherwise, false.
## Node GetIntersection ( vec3 p0 , vec3 p1 , bool use_handlers = true )

Searches for all of the nodes intersected by the line traced from p0 to p1. The node closest to the start point is returned.
### Arguments

- *vec3* **p0** - Line start point coordinates
- *vec3* **p1** - Line end point coordinates
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

The first intersected node found along the line; otherwise, *null*, if there was no intersection.
## Node GetIntersection ( vec3 p0 , vec3 p1 , WorldIntersection intersection , bool use_handlers = true )

Searches for all of the nodes intersecting the line. The node closest to the start point is returned. The intersection result will be presented as a *WorldIntersection* instance.
### Arguments

- *vec3* **p0** - Line start point coordinates.
- *vec3* **p1** - Line end point coordinates.
- *[WorldIntersection](../../../api/library/worlds/class.worldintersection_cs.md)* **intersection** - *WorldIntersection* class instance containing the intersection information.
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

The first intersected node found along the line; otherwise, *null*, if there was no intersection.
## Node GetIntersection ( vec3 p0 , vec3 p1 , WorldIntersectionNormal intersection , bool use_handlers = true )

Searches for all of the nodes intersecting the line. The node closest to the start point is returned. The intersection result will be presented as a *WorldIntersectionNormal* instance.
### Arguments

- *vec3* **p0** - Line start point coordinates.
- *vec3* **p1** - Line end point coordinates.
- *[WorldIntersectionNormal](../../../api/library/worlds/class.worldintersectionnormal_cs.md)* **intersection** - *WorldIntersectionNormal* class instance containing the intersection information.
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

The first intersected node found along the line; otherwise, *null*, if there was no intersection.
## Node GetIntersection ( vec3 p0 , vec3 p1 , WorldIntersectionTexCoord intersection , bool use_handlers = true )

Searches for all of the nodes intersecting the line. The node closest to the start point is returned. The intersection result will be presented as a *WorldIntersectionTexCoord* node.
### Arguments

- *vec3* **p0** - Start point of the line.
- *vec3* **p1** - End point of the line.
- *[WorldIntersectionTexCoord](../../../api/library/worlds/class.worldintersectiontexcoord_cs.md)* **intersection** - *WorldIntersectionTexCoord* class instance containing the intersection information.
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

The first intersected node found along the line; otherwise, *null*, if there was no intersection.
## bool GetIntersection ( WorldBoundFrustum bs , Node [] OUT_nodes , bool use_handlers )

Finds all nodes intersected by the specified bound frustum and puts them to the specified output buffer. By default this method gets editor-only objects (node handlers) along with nodes, to ignore them just set use_handlers to false.
### Arguments

- *[WorldBoundFrustum](../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bs** - Bounding frustum where intersection search is to be performed.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_nodes** - Output buffer to store the list of intersected nodes (if any). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

true if intersected nodes are found; otherwise, false.
## bool GetIntersection ( WorldBoundFrustum bf , Node [] OUT_bound_nodes , Node [] OUT_handler_nodes )

Performs a frustum selection query returning two kinds of hits separately: nodes whose bounds intersect the given frustum, and nodes whose visualizer handler points fall inside it.
### Arguments

- *[WorldBoundFrustum](../../../api/library/math/cs/bounds/worldboundfrustum_cs.md)* **bf** - Bounding frustum where intersection search is to be performed.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_bound_nodes** - Output vector filled with all nodes whose bounds intersect the frustum. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[Node](../../../api/library/nodes/class.node_cs.md)[]* **OUT_handler_nodes** - Output vector filled with nodes whose visualizer handler point (the on-screen node icon) lies inside the frustum. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if at least one node was found in either list; otherwise, false.
## Node GetIntersection ( vec3 p0 , vec3 p1 , IntersectionNodeFilter node_filter , IntersectionSurfaceFilter surface_filter , bool use_handlers = true )

Searches for all nodes intersected by the line traced from **p0** to **p1**, ignoring the ones defined by the specified **filters**. The node closest to the start point is returned (if any).
```csharp
// list of nodes to be excluded
HashSet<Node> excludes = new HashSet<Node>();

// custom function that determines whether the specified node is excluded
bool ExcludeNode(Node node)
{
	// ...
	return result;
}

// custom function that determines whether the specified surface is excluded
// depending on the given viewport mask
bool TestViewportMask(Unigine.Object obj, int surface, int viewport_mask)
{
	// ...
	return result;
}

// ...

// callback that determines whether a node is to be excluded (skipped)
Editor.IntersectionNodeFilterDelegate ExcludeCallback =
	(Node node, ref bool excluded) =>
	{
		excluded = !node.Enabled ||
				excludes.Contains(node) ||
				ExcludeNode(node);
	};

// callback that determines whether a surface of an object is to be excluded (skipped)
Editor.IntersectionSurfaceFilterDelegate ExcludeSurface =
	(Object obj, int surface, ref bool excluded) =>
	{
		excluded = TestViewportMask(obj, surface, viewport_mask) == false;
	};

// searching for intersection applying callback-based filters for nodes
// and for surfaces (when the corresponding flag is set)
Node node = Unigine.Editor.GetIntersection(p0, p1, ExcludeCallback,
	use_viewport_mask ? ExcludeSurface : null, true);

```


### Arguments

- *vec3* **p0** - Line start point coordinates
- *vec3* **p1** - Line end point coordinates
- *IntersectionNodeFilter* **node_filter** - Callback function to be used to filter out (ignore) certain nodes during the intersection tests. Pass *null*, if you don't need any node exceptions (nothing to exclude). The callback function must have the following signature: *FilterCallback(**Node** node, **ref bool** excluded)*
- *IntersectionSurfaceFilter* **surface_filter** - Callback function to be used to filter out (ignore) certain surfaces during the intersection tests. Pass *null*, if you don't need any surface exceptions (nothing to exclude). The callback function must have the following signature: *FilterCallback(**Object** obj, **int** num_surface, **ref bool** excluded)*
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

## Node GetIntersection ( vec3 p0 , vec3 p1 , IntersectionNodeFilter node_filter , IntersectionSurfaceFilter surface_filter , WorldIntersection intersection , bool use_handlers = true )

Searches for all nodes intersected by the line traced from **p0** to **p1**, ignoring the ones defined by the specified **filters**. The node closest to the start point is returned (if any).
```csharp
// list of nodes to be excluded
HashSet<Node> excludes = new HashSet<Node>();

// custom function that determines whether the specified node is excluded
bool ExcludeNode(Node node)
{
	// ...
	return result;
}

// custom function that determines whether the specified surface is excluded
// depending on the given viewport mask
bool TestViewportMask(Unigine.Object obj, int surface, int viewport_mask)
{
	// ...
	return result;
}

// ...

WorldIntersection intersection = new WorldIntersection();

// callback that determines whether a node is to be excluded (skipped)
Editor.IntersectionNodeFilterDelegate ExcludeCallback =
	(Node node, ref bool excluded) =>
	{
		excluded = !node.Enabled ||
				excludes.Contains(node) ||
				ExcludeNode(node);
	};

// callback that determines whether a surface of an object is to be excluded (skipped)
Editor.IntersectionSurfaceFilterDelegate ExcludeSurface =
	(Object obj, int surface, ref bool excluded) =>
	{
		excluded = TestViewportMask(obj, surface, viewport_mask) == false;
	};

// searching for intersection applying callback-based filters for nodes
// and for surfaces (when the corresponding flag is set)
Node node = Unigine.Editor.GetIntersection(p0, p1, ExcludeCallback,
	use_viewport_mask ? ExcludeSurface : null, intersection, true);

```


### Arguments

- *vec3* **p0** - Line start point coordinates
- *vec3* **p1** - Line end point coordinates
- *IntersectionNodeFilter* **node_filter** - Callback function to be used to filter out (ignore) certain nodes during the intersection tests. Pass *null*, if you don't need any node exceptions (nothing to exclude). The callback function must have the following signature: *FilterCallback(**Node** node, **ref bool** excluded)*
- *IntersectionSurfaceFilter* **surface_filter** - Callback function to be used to filter out (ignore) certain surfaces during the intersection tests. Pass *null*, if you don't need any surface exceptions (nothing to exclude). The callback function must have the following signature: *FilterCallback(**Object** obj, **int** num_surface, **ref bool** excluded)*
- *[WorldIntersection](../../../api/library/worlds/class.worldintersection_cs.md)* **intersection** - *WorldIntersection* class instance containing the intersection information.
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

## Node GetIntersection ( vec3 p0 , vec3 p1 , IntersectionNodeFilter node_filter , IntersectionSurfaceFilter surface_filter , WorldIntersectionNormal intersection , bool use_handlers = true )

Searches for all nodes intersected by the line traced from **p0** to **p1**, ignoring the ones defined by the specified **filters**. The node closest to the start point is returned (if any).
```csharp
// list of nodes to be excluded
HashSet<Node> excludes = new HashSet<Node>();

// custom function that determines whether the specified node is excluded
bool ExcludeNode(Node node)
{
	// ...
	return result;
}

// custom function that determines whether the specified surface is excluded
// depending on the given viewport mask
bool TestViewportMask(Unigine.Object obj, int surface, int viewport_mask)
{
	// ...
	return result;
}

// ...

WorldIntersectionNormal intersection = new WorldIntersectionNormal();

// callback that determines whether a node is to be excluded (skipped)
Editor.IntersectionNodeFilterDelegate ExcludeCallback =
	(Node node, ref bool excluded) =>
	{
		excluded = !node.Enabled ||
				excludes.Contains(node) ||
				ExcludeNode(node);
	};

// callback that determines whether a surface of an object is to be excluded (skipped)
Editor.IntersectionSurfaceFilterDelegate ExcludeSurface =
	(Object obj, int surface, ref bool excluded) =>
	{
		excluded = TestViewportMask(obj, surface, viewport_mask) == false;
	};

// searching for intersection applying callback-based filters for nodes
// and for surfaces (when the corresponding flag is set)
Node node = Unigine.Editor.GetIntersection(p0, p1, ExcludeCallback,
	use_viewport_mask ? ExcludeSurface : null, intersection, true);

```


### Arguments

- *vec3* **p0** - Line start point coordinates
- *vec3* **p1** - Line end point coordinates
- *IntersectionNodeFilter* **node_filter** - Callback function to be used to filter out (ignore) certain nodes during the intersection tests. Pass *null*, if you don't need any node exceptions (nothing to exclude). The callback function must have the following signature: *FilterCallback(**Node** node, **ref bool** excluded)*
- *IntersectionSurfaceFilter* **surface_filter** - Callback function to be used to filter out (ignore) certain surfaces during the intersection tests. Pass *null*, if you don't need any surface exceptions (nothing to exclude). The callback function must have the following signature: *FilterCallback(**Object** obj, **int** num_surface, **ref bool** excluded)*
- *[WorldIntersectionNormal](../../../api/library/worlds/class.worldintersectionnormal_cs.md)* **intersection** - *WorldIntersectionNormal* class instance containing the intersection information.
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

## Node GetIntersection ( vec3 p0 , vec3 p1 , IntersectionNodeFilter node_filter , IntersectionSurfaceFilter surface_filter , WorldIntersectionTexCoord intersection , bool use_handlers = true )

Searches for all nodes intersected by the line traced from **p0** to **p1**, ignoring the ones defined by the specified **filters**. The node closest to the start point is returned (if any).
### Arguments

- *vec3* **p0** - Line start point coordinates
- *vec3* **p1** - Line end point coordinates
- *IntersectionNodeFilter* **node_filter** - Callback function to be used to filter out (ignore) certain nodes during the intersection tests. Pass *null*, if you don't need any node exceptions (nothing to exclude). The callback function must have the following signature: *FilterCallback(**Node** node, **ref bool** excluded)*
- *IntersectionSurfaceFilter* **surface_filter** - Callback function to be used to filter out (ignore) certain surfaces during the intersection tests. Pass *null*, if you don't need any surface exceptions (nothing to exclude). The callback function must have the following signature: *FilterCallback(**Object** obj, **int** num_surface, **ref bool** excluded)*
- *[WorldIntersectionTexCoord](../../../api/library/worlds/class.worldintersectiontexcoord_cs.md)* **intersection** - *WorldIntersectionTexCoord* class instance containing the intersection information.
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value
