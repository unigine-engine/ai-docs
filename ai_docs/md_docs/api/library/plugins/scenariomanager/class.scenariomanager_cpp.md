# Unigine::Plugins::ScenarioManager::ScenarioManager Class (CPP)

**Header:** #include <plugins/Unigine/ScenarioManager/UnigineScenarioManager.h>


This class is the entry point of the *[Scenario Manager](../../../../code/plugins/scenariomanager/index.md)* visual scripting plugin. A scenario is a node graph executed by the engine: graphs are authored in the plugin's built-in web editor and stored in the project's data directory as `*.sgraph` files. The plugin is loaded as an external plugin library named *UnigineScenarioManager*.


Use the load functions to start a graph as a running script and address it by the returned script ID: fire named custom events into running graphs via **[fireEvent()](../../../...md#fireEvent_String_void)**, query script states, and observe the lifecycle via the **[getEventScriptLoaded()](../../../...md#getEventScriptLoaded_Event)**, **[getEventScriptUnloaded()](../../../...md#getEventScriptUnloaded_Event)**, and **[getEventFired()](../../../...md#getEventFired_Event)** events. Scripts can also be started from the command line and from the web editor.


> **Notice:** The public event callbacks run inside the plugin's update lock. From these callbacks, call only the deferred mutator methods (**[loadScriptDeferred()](../../../...md#loadScriptDeferred_String_void)**, **[unloadScriptDeferred()](../../../...md#unloadScriptDeferred_int_void)**, **[unloadAllScriptsDeferred()](../../../...md#unloadAllScriptsDeferred_void)**); calling the direct load and unload methods there results in a deadlock.


## ScenarioManager Class

### Enums

## SCRIPT_STATE

State of a loaded scenario script.
| Name | Description |
|---|---|
| **SCRIPT_STATE_LOADING** = 0 | The script is being loaded. This is the initial state; load functions switch the script to the running state before returning, so it is rarely observed. |
| **SCRIPT_STATE_RUNNING** = 1 | The script is loaded and executing. Only running scripts receive custom events. |
| **SCRIPT_STATE_PAUSED** = 2 | The script is halted on a debugger breakpoint. |
| **SCRIPT_STATE_ERROR** = 3 | The script has stopped due to an execution error. |
| **SCRIPT_STATE_STOPPED** = 4 | The script has finished or was unloaded. This state is also reported for an unknown script ID. |

### Members

## int getNumScripts () const

Returns the current number of currently loaded top-level scripts. Use **[getScriptId()](../../../...md#getScriptId_int_int)** to enumerate them. Event-subgraph children are not counted.
### Return value

Current number of loaded top-level scripts
## Event<const char *> getEventFired () const

Returns the current event triggered once per custom-event dispatch, from both the API and the event-sending graph nodes, after the matching event handler chains in the graphs have run. The callback receives the event name. From the callback, call only the deferred mutator methods (**[loadScriptDeferred()](../../../...md#loadScriptDeferred_String_void)**, **[unloadScriptDeferred()](../../../...md#unloadScriptDeferred_int_void)**, **[unloadAllScriptsDeferred()](../../../...md#unloadAllScriptsDeferred_void)**).
### Return value

Current event triggered on a custom event dispatch
## Event<int> getEventScriptLoaded () const

Returns the current event triggered when a script is loaded, covering every path that creates a script. The callback receives the script ID; it fires before the script's initialization chain runs, so the script is already addressable by ID. From the callback, call only the deferred mutator methods.
### Return value

Current event triggered when a script is loaded
## Event<int> getEventScriptUnloaded () const

Returns the current event triggered when a script is unloaded, covering every unload path. The callback receives the script ID and fires before teardown, so the ID still resolves. From the callback, call only the deferred mutator methods.
### Return value

Current event triggered when a script is unloaded
## void setLogEnabled ( bool enabled )

Sets a new value indicating if the plugin writes its messages, warnings, and errors to the engine log. Enabled by default.
### Arguments

- *bool* **enabled** - Set **true** to enable log output of the plugin; **false** - to disable it.

## bool isLogEnabled () const

Returns the current value indicating if the plugin writes its messages, warnings, and errors to the engine log. Enabled by default.
### Return value

**true** if log output of the plugin is enabled ; otherwise **false**.
---

## int loadScript ( const char * path )

Loads a scenario graph file and starts it immediately: the script is switched to the running state, its initialization chain is executed, and the script-loaded event is fired. Not safe to call from the public event callbacks; use **[loadScriptDeferred()](../../../...md#loadScriptDeferred_String_void)** there.
### Arguments

- *const char ** **path** - Path to the graph file relative to the data directory, or a graph GUID.

### Return value

ID of the new script (1 or greater), or -1 on failure (the failure reason is logged).
## int loadScriptForEntity ( const char * path , const char * entity_id )

Loads a scenario graph like **[loadScript()](../../../...md#loadScript_String_int)** and binds the new script to the given entity identifier, which the graph can read and **[findScriptIdByEntity()](../../../...md#findScriptIdByEntity_String_int)** can search for.
### Arguments

- *const char ** **path** - Path to the graph file relative to the data directory, or a graph GUID.
- *const char ** **entity_id** - Entity identifier string the new script is bound to.

### Return value

ID of the new script, or -1 on failure.
## int loadScriptFromJson ( const char * json , const char * source = "" )

Loads a scenario graph directly from a JSON string instead of a file (this is how the plugin's web editor runs a graph).
### Arguments

- *const char ** **json** - Graph description as a JSON string.
- *const char ** **source** - Name assigned to the script; if empty, an automatic editor-graph name is generated.

### Return value

ID of the new script, or -1 if the JSON cannot be parsed.
## void unloadScript ( int id )

Stops and destroys the script with the given ID: its shutdown chain runs, the script-unloaded event is fired, and the script is torn down. An unknown ID is silently ignored. Not safe to call from the public event callbacks; use **[unloadScriptDeferred()](../../../...md#unloadScriptDeferred_int_void)** there.
### Arguments

- *int* **id** - ID of the script to unload.

## void unloadAllScripts ( )

Unloads every loaded top-level script, applying the same teardown order as **[unloadScript()](../../../...md#unloadScript_int_void)** to each. Not safe to call from the public event callbacks; use **[unloadAllScriptsDeferred()](../../../...md#unloadAllScriptsDeferred_void)** there.
## void loadScriptDeferred ( const char * path )

Queues loading of a scenario graph: the operation executes on the main thread at the start of the next update. This is the load variant that is safe to call from the public event callbacks; since the work happens later, no script ID is returned.
### Arguments

- *const char ** **path** - Path to the graph file relative to the data directory, or a graph GUID.

## void unloadScriptDeferred ( int id )

Queues unloading of the script with the given ID: the operation executes on the main thread at the start of the next update. This is the unload variant that is safe to call from the public event callbacks.
### Arguments

- *int* **id** - ID of the script to unload; values of 0 and below are ignored.

## void unloadAllScriptsDeferred ( )

Queues unloading of all scripts: the operation executes on the main thread at the start of the next update. This is the variant that is safe to call from the public event callbacks.
## int findScriptIdByName ( const char * name )

Searches the loaded top-level scripts for the first one with the given name.
### Arguments

- *const char ** **name** - Name of the script (the graph name for file loads, or the source name for JSON loads).

### Return value

ID of the first matching script, or -1 if none is found.
## int findScriptIdByEntity ( const char * entity_id )

Searches the loaded scripts for the first one bound to the given entity identifier (via **[loadScriptForEntity()](../../../...md#loadScriptForEntity_String_String_int)** or the *EntityScript* component).
### Arguments

- *const char ** **entity_id** - Entity identifier to search for. An empty value returns -1.

### Return value

ID of the first script bound to the given entity, or -1 if none is found.
## int getScriptId ( int num )

Converts an enumeration index into a script ID. Enumeration walks the top-level scripts only.
### Arguments

- *int* **num** - Enumeration index, in the [0; **[getNumScripts()](../../../...md#getNumScripts_int)**) range.

### Return value

ID of the script with the given index, or -1 if the index is out of range.
## String getScriptName ( int id )

Returns the display name of the script with the given ID.
### Arguments

- *int* **id** - ID of the script.

### Return value

Name of the script, or an empty string for an unknown ID.
## String getScriptPath ( int id )

Returns the current path of the script's graph file, following renames and moves of the source file.
### Arguments

- *int* **id** - ID of the script.

### Return value

Current path of the graph file, or an empty string for an unknown ID or a deleted source file.
## String getScriptEntityId ( int id )

Returns the entity identifier the script with the given ID was bound to.
### Arguments

- *int* **id** - ID of the script.

### Return value

Entity identifier of the script, or an empty string if the script is not bound or the ID is unknown.
## ScenarioManager::SCRIPT_STATE getScriptState ( int id )

Returns the current state of the script with the given ID. A script halted on a debugger breakpoint is reported as paused.
### Arguments

- *int* **id** - ID of the script.

### Return value

Current state of the script, one of the *SCRIPT_STATE_** values; *SCRIPT_STATE_STOPPED* for an unknown ID.
## void fireEvent ( const char * name )

Dispatches a named custom event to all running scripts, triggering every matching event handler node in every running graph, and then fires the public *[EventFired](#getEventFired_Event)* event.
### Arguments

- *const char ** **name** - Name of the custom event. An empty name does nothing.
