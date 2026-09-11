# Unigine::Editor Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


This class provides functionality for the [editor script](../../../code/fundamentals/execution_sequence/app_logic_system.md#editor_logic) that loads and manages the hierarchy of nodes displayed in the editor.


> **Notice:** C++ methods running editor script functions are described in the *[Engine](../../../api/library/engine/class.engine_usc.md)* class reference.


## Editor Class

### Members

## void setPlayer ( Player player )

Sets a new player used in the Editor mode at the moment.
> **Notice:** Editor player is handled differently than in-game players. Parameters set directly for the player are ignored; instead, *Editor* player uses [Camera](../../../editor2/camera_settings/index.md) parameters set via the interface. (See Editor scripts in `data/core/editor` folder for implementation.)


### Arguments

- *[Player](../../../api/library/players/class.player_usc.md)* **player** - The editor player.

## Player getPlayer () const

Returns the current player used in the Editor mode at the moment.
> **Notice:** Editor player is handled differently than in-game players. Parameters set directly for the player are ignored; instead, *Editor* player uses [Camera](../../../editor2/camera_settings/index.md) parameters set via the interface. (See Editor scripts in `data/core/editor` folder for implementation.)


### Return value

Current editor player.
## void setVRPlayer ( )

Sets a new player used to render VR in the Editor mode at the moment.
If VR Player has not been set, VR is rendered to the [Editor Player](#getPlayer_Player); if the *Editor* Player hasn't been set either, the [Game Player](../../../api/library/engine/class.game_usc.md#getPlayer_Player) is used for rendering.


> **Notice:** Editor player is handled differently than in-game players. Parameters set directly for the player are ignored; instead, Editor player uses [Camera](../../../editor2/camera_settings/index.md) parameters set via the interface. (See Editor scripts in `data/core/editor` folder for implementation.)


### Arguments

- **vrplayer** - The player to render VR.

## getVRPlayer () const

Returns the current player used to render VR in the Editor mode at the moment.
If VR Player has not been set, VR is rendered to the [Editor Player](#getPlayer_Player); if the *Editor* Player hasn't been set either, the [Game Player](../../../api/library/engine/class.game_usc.md#getPlayer_Player) is used for rendering.


> **Notice:** Editor player is handled differently than in-game players. Parameters set directly for the player are ignored; instead, Editor player uses [Camera](../../../editor2/camera_settings/index.md) parameters set via the interface. (See Editor scripts in `data/core/editor` folder for implementation.)


### Return value

Current player to render VR.
## void setData ( string data )

Sets a new
### Arguments

- *string* **data** - The user string data.

## const char * getData () const

Returns the current
### Return value

Current user string data.
## void setEnabled ( int enabled )

Sets a new value of the *Enabled* parameter. The *Enabled* parameter controls all internal additional engine processing (for example, reloading of textures when their recording time is changed and so on). For example, the *Enabled* parameter can be set to 0 when using Syncker in order to increase engine performance (as Syncker operates inside the editor environment and can reduce engine performance).
### Arguments

- *int* **enabled** - The the *Enabled* parameter

## int isEnabled () const

Returns the current value of the *Enabled* parameter. The *Enabled* parameter controls all internal additional engine processing (for example, reloading of textures when their recording time is changed and so on). For example, the *Enabled* parameter can be set to 0 when using Syncker in order to increase engine performance (as Syncker operates inside the editor environment and can reduce engine performance).
### Return value

Current the *Enabled* parameter
## int isLoaded () const

Returns the current value indicating if the editor is already loaded.
### Return value

Current the editor is loaded
---

## void engine.editor. reload ( )

Reloads the Unigine Editor. This functions updates node hierarchy, updates loaded textures if they were modified, etc.
## int engine.editor. needReload ( )

Returns a value indicating if Unigine Editor should be reloaded.
### Return value

**1** if the editor should be reloaded; otherwise, **0**.
## void engine.editor. addEditorPlayer ( Player player )

Adds another editor player.
### Arguments

- *[Player](../../../api/library/players/class.player_usc.md)* **player** - Player instance.

## void engine.editor. removeEditorPlayer ( Player player )

Removes a given player from the editor.
### Arguments

- *[Player](../../../api/library/players/class.player_usc.md)* **player** - Player instance.

## int engine.editor. isEditorPlayer ( Player player )

Returns a value indicating if the given player is an Editor player.
### Arguments

- *[Player](../../../api/library/players/class.player_usc.md)* **player** - Player instance.

### Return value

**1** if the *Player* is an Editor player; otherwise, **0**.
## Node engine.editor. getIntersection ( Vec3 p0 , Vec3 p1 , int[] exclude , Variable v )


Traces a line from one point to another to find an object located on that line, skipping objects from a given list. This function takes into account editor-only objects (object handlers). Intersection does not work for disabled objects.


> **Notice:** World space coordinates are used for this function.


Depending on the variable, passed as an argument, the intersection result will be presented as follows:


- WorldIntersection intersection � The WorldIntersection node.
- WorldIntersectionNormal normal � The WorldIntersectionNormal node.
- WorldIntersectionTexCoord texcoord � The WorldIntersectionTexCoord node.


### Arguments

- *Vec3* **p0** - Start point of the line.
- *Vec3* **p1** - End point of the line.
- *int[]* **exclude** - Array of the nodes to exclude; all these nodes will be skipped while checking for intersection.
- *Variable* **v** - Variable into which information on the intersection will be saved.

### Return value

The first node found along the line; 0 if there was no intersection.
## Node engine.editor. getIntersection ( Vec3 p0 , Vec3 p1 , Variable v )


Traces a line from one point to another to find an object located on that line. This function takes into account editor-only objects (object handlers). Intersection does not work for disabled objects.


> **Notice:** World space coordinates are used for this function.


Depending on the variable, passed as an argument, the intersection result will be presented as follows:


- WorldIntersection intersection � The WorldIntersection node.
- WorldIntersectionNormal normal � The WorldIntersectionNormal node.
- WorldIntersectionTexCoord texcoord � The WorldIntersectionTexCoord node.


### Arguments

- *Vec3* **p0** - Start point of the line.
- *Vec3* **p1** - End point of the line.
- *Variable* **v** - Variable into which information on the intersection will be saved.

### Return value

The first node found along the line; 0 if there was no intersection.
## int engine.editor. isVariable ( string name )

Returns a value indicating if the given variable exists in the editor script.
### Arguments

- *string* **name** - Variable name.

### Return value

1 if the variable exists; otherwise, 0.
## int engine.editor. isFunction ( string name , int num_args )

Returns a value indicating if the given function with the specified number of arguments exists in the editor script.
### Arguments

- *string* **name** - Function name.
- *int* **num_args** - Number of function arguments.

### Return value

1 if the function exists; otherwise, 0.
## void engine.editor. set ( string function , Variable value )

Sets a variable in a editor script (this function can be called directly from any other script).
### Arguments

- *string* **function** - Variable name.
- *Variable* **value** - Value of the variable.

## Variable engine.editor. get ( string function )

Returns a variable from the editor script. Instances of user-defined classes cannot be requested in such a manner.
### Arguments

- *string* **function** - Variable name with a namespace, if needed.

### Return value

Requested instance.
## Variable engine.editor. call ( Variable function )

Executes a function of the editor script from an external script. The function should not take any arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.

### Return value

Value returned by the function.
## Variable engine.editor. call ( Variable function , Variable arg0 )

Executes a function of the editor script from an external script. The function should take one argument.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.editor. call ( Variable function , Variable arg0 , Variable arg1 )

Executes a function of the editor script from an external script. The function should take two arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.
- *Variable* **arg1** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.editor. call ( Variable function , Variable arg0 , Variable arg1 , Variable arg2 )

Executes a function of the editor script from an external script. The function should take three arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.
- *Variable* **arg1** - Argument of the function.
- *Variable* **arg2** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.editor. call ( Variable function , Variable arg0 , Variable arg1 , Variable arg2 , Variable arg3 )

Executes a function of the editor script from an external script. The function should take four arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.
- *Variable* **arg1** - Argument of the function.
- *Variable* **arg2** - Argument of the function.
- *Variable* **arg3** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.editor. call ( Variable function , Variable arg0 , Variable arg1 , Variable arg2 , Variable arg3 , Variable arg4 )

Executes a function of the editor script from an external script. The function should take five arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.
- *Variable* **arg1** - Argument of the function.
- *Variable* **arg2** - Argument of the function.
- *Variable* **arg3** - Argument of the function.
- *Variable* **arg4** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.editor. call ( Variable function , Variable arg0 , Variable arg1 , Variable arg2 , Variable arg3 , Variable arg4 , Variable arg5 )

Executes a function of the editor script from an external script. The function should take six arguments.
### Arguments

- *Variable* **function** - Name of the function to execute.
- *Variable* **arg0** - Argument of the function.
- *Variable* **arg1** - Argument of the function.
- *Variable* **arg2** - Argument of the function.
- *Variable* **arg3** - Argument of the function.
- *Variable* **arg4** - Argument of the function.
- *Variable* **arg5** - Argument of the function.

### Return value

Value returned by the function.
## Variable engine.editor. call ( Variable function , int id = [] )

Executes a function of the editor script from an external script. The function takes an array of arguments (up to 8 arguments are supported).
### Arguments

- *Variable* **function** - Name of the function to execute.
- *int* **id** - Array of up to 8 arguments.

### Return value

Value returned by the function.
