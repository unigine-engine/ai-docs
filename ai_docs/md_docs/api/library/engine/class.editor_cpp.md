# Unigine::Editor Class (CPP)

**Header:** #include <UnigineEditor.h>

> **Notice:** This class is a singleton.


This class provides functionality for the [editor script](../../../code/fundamentals/execution_sequence/app_logic_system.md#editor_logic) that loads and manages the hierarchy of nodes displayed in the editor.


> **Notice:** C++ methods running editor script functions are described in the *[Engine](../../../api/library/engine/class.engine_cpp.md)* class reference.


## Editor Class

### Members

## void setPlayer ( const Ptr < Player >& player )

Sets a new player used in the Editor mode at the moment.
> **Notice:** Editor player is handled differently than in-game players. Parameters set directly for the player are ignored; instead, *Editor* player uses [Camera](../../../editor2/camera_settings/index.md) parameters set via the interface. (See Editor scripts in `data/core/editor` folder for implementation.)


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Player](../../../api/library/players/class.player_cpp.md)>&* **player** - The editor player.

## Ptr < Player > getPlayer () const

Returns the current player used in the Editor mode at the moment.
> **Notice:** Editor player is handled differently than in-game players. Parameters set directly for the player are ignored; instead, *Editor* player uses [Camera](../../../editor2/camera_settings/index.md) parameters set via the interface. (See Editor scripts in `data/core/editor` folder for implementation.)


### Return value

Current editor player.
## void setVRPlayer ( const Ptr < Player >& vrplayer )

Sets a new player used to render VR in the Editor mode at the moment.
If VR Player has not been set, VR is rendered to the [Editor Player](#getPlayer_Player); if the *Editor* Player hasn't been set either, the [Game Player](../../../api/library/engine/class.game_cpp.md#getPlayer_Player) is used for rendering.


> **Notice:** Editor player is handled differently than in-game players. Parameters set directly for the player are ignored; instead, Editor player uses [Camera](../../../editor2/camera_settings/index.md) parameters set via the interface. (See Editor scripts in `data/core/editor` folder for implementation.)


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Player](../../../api/library/players/class.player_cpp.md)>&* **vrplayer** - The player to render VR.

## Ptr < Player > getVRPlayer () const

Returns the current player used to render VR in the Editor mode at the moment.
If VR Player has not been set, VR is rendered to the [Editor Player](#getPlayer_Player); if the *Editor* Player hasn't been set either, the [Game Player](../../../api/library/engine/class.game_cpp.md#getPlayer_Player) is used for rendering.


> **Notice:** Editor player is handled differently than in-game players. Parameters set directly for the player are ignored; instead, Editor player uses [Camera](../../../editor2/camera_settings/index.md) parameters set via the interface. (See Editor scripts in `data/core/editor` folder for implementation.)


### Return value

Current player to render VR.
## void setData ( const char * data )

Sets a new user string data associated with the world. this string is written directly into the data tag of the `*.world` file.
### Arguments

- *const char ** **data** - The user string data.

## const char * getData () const

Returns the current user string data associated with the world. this string is written directly into the data tag of the `*.world` file.
### Return value

Current user string data.
## void setEnabled ( bool enabled )

Sets a new value of the *Enabled* parameter. The *Enabled* parameter controls all internal additional engine processing (for example, reloading of textures when their recording time is changed and so on). For example, the *Enabled* parameter can be set to 0 when using Syncker in order to increase engine performance (as Syncker operates inside the editor environment and can reduce engine performance).
### Arguments

- *bool* **enabled** - Set **true** to enable the *Enabled* parameter; **false** - to disable it.

## bool isEnabled () const

Returns the current value of the *Enabled* parameter. The *Enabled* parameter controls all internal additional engine processing (for example, reloading of textures when their recording time is changed and so on). For example, the *Enabled* parameter can be set to 0 when using Syncker in order to increase engine performance (as Syncker operates inside the editor environment and can reduce engine performance).
### Return value

**true** if the *Enabled* parameter is enabled ; otherwise **false**.
## bool isLoaded () const

Returns the current value indicating if the editor is already loaded.
### Return value

**true** if the editor is loaded; otherwise **false**.
---

## void load ( const char * script = "editor/editor.usc" )

Loads the editor from the specified script.
### Arguments

- *const char ** **script** - Path to the script.

## void quit ( )

Quit the editor.
## void reload ( )

Reloads the Unigine Editor. This functions updates node hierarchy, updates loaded textures if they were modified, etc.
## int needReload ( )

Returns a value indicating if Unigine Editor should be reloaded.
### Return value

**1** if the editor should be reloaded; otherwise, **0**.
## void addEditorPlayer ( const Ptr < Player > & player )

Adds another editor player.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Player](../../../api/library/players/class.player_cpp.md)> &* **player** - Pointer to Player.

## void removeEditorPlayer ( const Ptr < Player > & player )

Removes a given player from the editor.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Player](../../../api/library/players/class.player_cpp.md)> &* **player** - Pointer to Player.

## bool isEditorPlayer ( const Ptr < Player > & player ) const

Returns a value indicating if the given player is an Editor player.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Player](../../../api/library/players/class.player_cpp.md)> &* **player** - A smart pointer to the *Player*.Player instance.

### Return value

true if the *Player* is an Editor player; otherwise, false.
## Ptr < Node > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , bool use_handlers = true )

Searches for all of the nodes intersected by the line traced from p0 to p1. The node closest to the start point is returned.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point coordinates
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point coordinates
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

The first intersected node found along the line; otherwise, *nullptr*, if there was no intersection.
## Ptr < Node > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , const Ptr < WorldIntersection > & intersection , bool use_handlers = true )

Searches for all of the nodes intersecting the line. The node closest to the start point is returned. The intersection result will be presented as a *WorldIntersection* instance.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point coordinates.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point coordinates.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[WorldIntersection](../../../api/library/worlds/class.worldintersection_cpp.md)> &* **intersection** - *WorldIntersection* class instance containing the intersection information.
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

The first intersected node found along the line; otherwise, *nullptr*, if there was no intersection.
## Ptr < Node > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , const Ptr < WorldIntersectionNormal > & intersection , bool use_handlers = true )

Searches for all of the nodes intersecting the line. The node closest to the start point is returned. The intersection result will be presented as a *WorldIntersectionNormal* instance.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point coordinates.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point coordinates.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[WorldIntersectionNormal](../../../api/library/worlds/class.worldintersectionnormal_cpp.md)> &* **intersection** - *WorldIntersectionNormal* class instance containing the intersection information.
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

The first intersected node found along the line; otherwise, *nullptr*, if there was no intersection.
## Ptr < Node > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , const Ptr < WorldIntersectionTexCoord > & intersection , bool use_handlers = true )

Searches for all of the nodes intersecting the line. The node closest to the start point is returned. The intersection result will be presented as a *WorldIntersectionTexCoord* node.
### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Start point of the line.
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - End point of the line.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[WorldIntersectionTexCoord](../../../api/library/worlds/class.worldintersectiontexcoord_cpp.md)> &* **intersection** - *WorldIntersectionTexCoord* class instance containing the intersection information.
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

The first intersected node found along the line; otherwise, *nullptr*, if there was no intersection.
## bool getIntersection ( const Math:: WorldBoundFrustum & bs , Vector < Ptr < Node >> & OUT_nodes , bool use_handlers )

Finds all nodes intersected by the specified bound frustum and puts them to the specified output buffer. By default this method gets editor-only objects (node handlers) along with nodes, to ignore them just set use_handlers to false.
### Arguments

- *const  Math::[WorldBoundFrustum](../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bs** - Bounding frustum where intersection search is to be performed.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_nodes** - Output buffer to store the list of intersected nodes (if any). > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

true if intersected nodes are found; otherwise, false.
## bool getIntersection ( const Math:: WorldBoundFrustum & bf , Vector < Ptr < Node >> & OUT_bound_nodes , Vector < Ptr < Node >> & OUT_handler_nodes )

Performs a frustum selection query returning two kinds of hits separately: nodes whose bounds intersect the given frustum, and nodes whose visualizer handler points fall inside it.
### Arguments

- *const  Math::[WorldBoundFrustum](../../../api/library/math/bounds/class.worldboundfrustum_cpp.md) &* **bf** - Bounding frustum where intersection search is to be performed.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_bound_nodes** - Output vector filled with all nodes whose bounds intersect the frustum. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>> &* **OUT_handler_nodes** - Output vector filled with nodes whose visualizer handler point (the on-screen node icon) lies inside the frustum. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

true if at least one node was found in either list; otherwise, false.
## Ptr < Node > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , CallbackBase2 < Ptr < Node >, bool *> * node_filter , CallbackBase3 < Ptr < Object >, int, bool *> * surface_filter , bool use_handlers = true )

Searches for all nodes intersected by the line traced from **p0** to **p1**, ignoring the ones defined by the specified **filters**. The node closest to the start point is returned (if any).
```cpp
// list of nodes to be excluded
HashSet<NodePtr> excludes;

// custom function that determines whether the specified node is excluded
bool exclude_node(NodePtr node)
{
	// ...
	return result;
}

// custom function that determines whether the specified surface is excluded
// depending on the given viewport mask
bool test_viewport_mask(ObjectPtr object, int surface, int viewport_mask)
{
	// ...
	return result;
}

// ...

// callback that determines whether a node is to be excluded (skipped)
CallbackBase2<NodePtr, bool *> *exclude_callback = MakeCallback(
	[&](NodePtr node, bool *exclude) {
		*exclude = !node->isEnabled() || excludes.contains(node) || exclude_node(node);
	});

// callback that determines whether a surface of an object is to be excluded (skipped)
CallbackBase3<ObjectPtr, int, bool *> *exclude_surface = MakeCallback(
	[this, viewport_mask](ObjectPtr object, int surface, bool *excluded) {
		*excluded = test_viewport_mask(object, surface, viewport_mask) == false;
	});

// searching for intersection applying callback-based filters for nodes
// and for surfaces (when the corresponding flag is set)
NodePtr node = Unigine::Editor::getIntersection(p0, p1, exclude_callback,
	use_viewport_mask ? exclude_surface : nullptr, true);

```


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point coordinates
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point coordinates
- *[CallbackBase2](../../../api/library/common/callbacks/class.callbackbase2_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>, bool *> ** **node_filter** - Callback function to be used to filter out (ignore) certain nodes during the intersection tests. Pass *nullptr*, if you don't need any node exceptions (nothing to exclude). The callback function must have the following signature: *filter_callback(**NodePtr** node, **bool *** excluded)*
- *[CallbackBase3](../../../api/library/common/callbacks/class.callbackbase3_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)>, int, bool *> ** **surface_filter** - Callback function to be used to filter out (ignore) certain surfaces during the intersection tests. Pass *nullptr*, if you don't need any surface exceptions (nothing to exclude). The callback function must have the following signature: *filter_callback(**ObjectPtr** obj, **int** num_surface, **bool *** excluded)*
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

The first intersected node if found; otherwise, *nullptr*, if there was no intersection.
## Ptr < Node > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , CallbackBase2 < Ptr < Node >, bool *> * node_filter , CallbackBase3 < Ptr < Object >, int, bool *> * surface_filter , const Ptr < WorldIntersection > & intersection , bool use_handlers = true )

Searches for all nodes intersected by the line traced from **p0** to **p1**, ignoring the ones defined by the specified **filters**. The node closest to the start point is returned (if any).
```cpp
// list of nodes to be excluded
HashSet<NodePtr> excludes;

// custom function that determines whether the specified node is excluded
bool exclude_node(NodePtr node)
{
	// ...
	return result;
}

// custom function that determines whether the specified surface is excluded
// depending on the given viewport mask
bool test_viewport_mask(ObjectPtr object, int surface, int viewport_mask)
{
	// ...
	return result;
}

// ...

WorldIntersectionPtr intersection = WorldIntersection::create();

// callback that determines whether a node is to be excluded (skipped)
CallbackBase2<NodePtr, bool *> *exclude_callback = MakeCallback(
	[&](NodePtr node, bool *exclude) {
		*exclude = !node->isEnabled() || excludes.contains(node) || exclude_node(node);
	});

// callback that determines whether a surface of an object is to be excluded (skipped)
CallbackBase3<ObjectPtr, int, bool *> *exclude_surface = MakeCallback(
	[this, viewport_mask](ObjectPtr object, int surface, bool *excluded) {
		*excluded = test_viewport_mask(object, surface, viewport_mask) == false;
	});

// searching for intersection applying callback-based filters for nodes
// and for surfaces (when the corresponding flag is set)
NodePtr node = Unigine::Editor::getIntersection(p0, p1, exclude_callback,
	use_viewport_mask ? exclude_surface : nullptr, intersection, true);

```


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point coordinates
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point coordinates
- *[CallbackBase2](../../../api/library/common/callbacks/class.callbackbase2_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>, bool *> ** **node_filter** - Callback function to be used to filter out (ignore) certain nodes during the intersection tests. Pass *nullptr*, if you don't need any node exceptions (nothing to exclude). The callback function must have the following signature: *filter_callback(**NodePtr** node, **bool *** excluded)*
- *[CallbackBase3](../../../api/library/common/callbacks/class.callbackbase3_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)>, int, bool *> ** **surface_filter** - Callback function to be used to filter out (ignore) certain surfaces during the intersection tests. Pass *nullptr*, if you don't need any surface exceptions (nothing to exclude). The callback function must have the following signature: *filter_callback(**ObjectPtr** obj, **int** num_surface, **bool *** excluded)*
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[WorldIntersection](../../../api/library/worlds/class.worldintersection_cpp.md)> &* **intersection** - *WorldIntersection* class instance containing the intersection information.
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

The first intersected node if found; otherwise, *nullptr*, if there was no intersection.
## Ptr < Node > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , CallbackBase2 < Ptr < Node >, bool *> * node_filter , CallbackBase3 < Ptr < Object >, int, bool *> * surface_filter , const Ptr < WorldIntersectionNormal > & intersection , bool use_handlers = true )

Searches for all nodes intersected by the line traced from **p0** to **p1**, ignoring the ones defined by the specified **filters**. The node closest to the start point is returned (if any).
```cpp
// list of nodes to be excluded
HashSet<NodePtr> excludes;

// custom function that determines whether the specified node is excluded
bool exclude_node(NodePtr node)
{
	// ...
	return result;
}

// custom function that determines whether the specified surface is excluded
// depending on the given viewport mask
bool test_viewport_mask(ObjectPtr object, int surface, int viewport_mask)
{
	// ...
	return result;
}

// ...

WorldIntersectionNormalPtr intersection = WorldIntersectionNormal::create();

// callback that determines whether a node is to be excluded (skipped)
CallbackBase2<NodePtr, bool *> *exclude_callback = MakeCallback(
	[&](NodePtr node, bool *exclude) {
		*exclude = !node->isEnabled() || excludes.contains(node) || exclude_node(node);
	});

// callback that determines whether a surface of an object is to be excluded (skipped)
CallbackBase3<ObjectPtr, int, bool *> *exclude_surface = MakeCallback(
	[this, viewport_mask](ObjectPtr object, int surface, bool *excluded) {
		*excluded = test_viewport_mask(object, surface, viewport_mask) == false;
	});

// searching for intersection applying callback-based filters for nodes
// and for surfaces (when the corresponding flag is set)
NodePtr node = Unigine::Editor::getIntersection(p0, p1, exclude_callback,
	use_viewport_mask ? exclude_surface : nullptr, intersection, true);

```


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point coordinates
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point coordinates
- *[CallbackBase2](../../../api/library/common/callbacks/class.callbackbase2_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>, bool *> ** **node_filter** - Callback function to be used to filter out (ignore) certain nodes during the intersection tests. Pass *nullptr*, if you don't need any node exceptions (nothing to exclude). The callback function must have the following signature: *filter_callback(**NodePtr** node, **bool *** excluded)*
- *[CallbackBase3](../../../api/library/common/callbacks/class.callbackbase3_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)>, int, bool *> ** **surface_filter** - Callback function to be used to filter out (ignore) certain surfaces during the intersection tests. Pass *nullptr*, if you don't need any surface exceptions (nothing to exclude). The callback function must have the following signature: *filter_callback(**ObjectPtr** obj, **int** num_surface, **bool *** excluded)*
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[WorldIntersectionNormal](../../../api/library/worlds/class.worldintersectionnormal_cpp.md)> &* **intersection** - *WorldIntersectionNormal* class instance containing the intersection information.
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

The first intersected node if found; otherwise, *nullptr*, if there was no intersection.
## Ptr < Node > getIntersection ( const Math:: Vec3 & p0 , const Math:: Vec3 & p1 , CallbackBase2 < Ptr < Node >, bool *> * node_filter , CallbackBase3 < Ptr < Object >, int, bool *> * surface_filter , const Ptr < WorldIntersectionTexCoord > & intersection , bool use_handlers = true )

Searches for all nodes intersected by the line traced from **p0** to **p1**, ignoring the ones defined by the specified **filters**. The node closest to the start point is returned (if any).
```cpp
// list of nodes to be excluded
HashSet<NodePtr> excludes;

// custom function that determines whether the specified node is excluded
bool exclude_node(NodePtr node)
{
	// ...
}

// custom function that determines whether the specified surface is excluded
// depending on the given viewport mask
bool test_viewport_mask(ObjectPtr object, int surface, int viewport_mask)
{
	// ...
}

// ...

WorldIntersectionTexCoordPtr intersection = WorldIntersectionTexCoord::create();

// callback that determines whether a node is to be excluded (skipped)
CallbackBase2<NodePtr, bool *> *exclude_callback = MakeCallback(
	[&](NodePtr node, bool *exclude) {
		*exclude = !node->isEnabled() || excludes.contains(node) || exclude_node(node);
	});

// callback that determines whether a surface of an object is to be excluded (skipped)
CallbackBase3<ObjectPtr, int, bool *> *exclude_surface = MakeCallback(
	[this, viewport_mask](ObjectPtr object, int surface, bool *excluded) {
		*excluded = test_viewport_mask(object, surface, viewport_mask) == false;
	});

// searching for intersection applying callback-based filters for nodes
// and for surfaces (when the corresponding flag is set)
NodePtr node = Unigine::Editor::getIntersection(p0, p1, exclude_callback,
	use_viewport_mask ? exclude_surface : nullptr, intersection, true);

```


### Arguments

- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p0** - Line start point coordinates
- *const  Math::[Vec3](../../../api/library/math/class.vec3_cpp.md) &* **p1** - Line end point coordinates
- *[CallbackBase2](../../../api/library/common/callbacks/class.callbackbase2_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)>, bool *> ** **node_filter** - Callback function to be used to filter out (ignore) certain nodes during the intersection tests. Pass *nullptr*, if you don't need any node exceptions (nothing to exclude). The callback function must have the following signature: *filter_callback(**NodePtr** node, **bool *** excluded)*
- *[CallbackBase3](../../../api/library/common/callbacks/class.callbackbase3_cpp.md)<[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Object](../../../api/library/objects/class.object_cpp.md)>, int, bool *> ** **surface_filter** - Callback function to be used to filter out (ignore) certain surfaces during the intersection tests. Pass *nullptr*, if you don't need any surface exceptions (nothing to exclude). The callback function must have the following signature: *filter_callback(**ObjectPtr** obj, **int** num_surface, **bool *** excluded)*
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[WorldIntersectionTexCoord](../../../api/library/worlds/class.worldintersectiontexcoord_cpp.md)> &* **intersection** - *WorldIntersectionTexCoord* class instance containing the intersection information.
- *bool* **use_handlers** - true to include editor-only objects (node handlers) in the list of intersected nodes; false - to ignore handlers.

### Return value

The first intersected node if found; otherwise, *nullptr*, if there was no intersection found.
