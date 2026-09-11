# Unigine::Plugins::ScenarioManager::ScenarioManager Class (CS)


This class is the entry point of the *[Scenario Manager](../../../../code/plugins/scenariomanager/index.md)* visual scripting plugin. A scenario is a node graph executed by the engine: graphs are authored in the plugin's built-in web editor and stored in the project's data directory as `*.sgraph` files. The plugin is loaded as an external plugin library named *UnigineScenarioManager*.


Use the load functions to start a graph as a running script and address it by the returned script ID: fire named custom events into running graphs via **[FireEvent()](../../../...md#fireEvent_String_void)**, query script states, and observe the lifecycle via the **[EventScriptLoaded](../../../...md#getEventScriptLoaded_Event)**, **[EventScriptUnloaded](../../../...md#getEventScriptUnloaded_Event)**, and **[EventFired](../../../...md#getEventFired_Event)** events. Scripts can also be started from the command line and from the web editor.


> **Notice:** The public event callbacks run inside the plugin's update lock. From these callbacks, call only the deferred mutator methods (**[LoadScriptDeferred()](../../../...md#loadScriptDeferred_String_void)**, **[UnloadScriptDeferred()](../../../...md#unloadScriptDeferred_int_void)**, **[UnloadAllScriptsDeferred()](../../../...md#unloadAllScriptsDeferred_void)**); calling the direct load and unload methods there results in a deadlock.


## ScenarioManager Class

### Enums

## SCRIPT_STATE

State of a loaded scenario script.
| Name | Description |
|---|---|
| **LOADING** = 0 | The script is being loaded. This is the initial state; load functions switch the script to the running state before returning, so it is rarely observed. |
| **RUNNING** = 1 | The script is loaded and executing. Only running scripts receive custom events. |
| **PAUSED** = 2 | The script is halted on a debugger breakpoint. |
| **ERROR** = 3 | The script has stopped due to an execution error. |
| **STOPPED** = 4 | The script has finished or was unloaded. This state is also reported for an unknown script ID. |

### Properties

## 🔒︎ int NumScripts

The number of currently loaded top-level scripts. Use **[GetScriptId()](../../../...md#getScriptId_int_int)** to enumerate them. Event-subgraph children are not counted.
## 🔒︎ Event<string> EventFired

The event triggered once per custom-event dispatch, from both the API and the event-sending graph nodes, after the matching event handler chains in the graphs have run. The callback receives the event name. From the callback, call only the deferred mutator methods (**[LoadScriptDeferred()](../../../...md#loadScriptDeferred_String_void)**, **[UnloadScriptDeferred()](../../../...md#unloadScriptDeferred_int_void)**, **[UnloadAllScriptsDeferred()](../../../...md#unloadAllScriptsDeferred_void)**).
## 🔒︎ Event<int> EventScriptLoaded

The event triggered when a script is loaded, covering every path that creates a script. The callback receives the script ID; it fires before the script's initialization chain runs, so the script is already addressable by ID. From the callback, call only the deferred mutator methods.
## 🔒︎ Event<int> EventScriptUnloaded

The event triggered when a script is unloaded, covering every unload path. The callback receives the script ID and fires before teardown, so the ID still resolves. From the callback, call only the deferred mutator methods.
## bool LogEnabled

The value indicating if the plugin writes its messages, warnings, and errors to the engine log. Enabled by default.
### Members

---

## int LoadScript ( string path )

Loads a scenario graph file and starts it immediately: the script is switched to the running state, its initialization chain is executed, and the script-loaded event is fired. Not safe to call from the public event callbacks; use **[LoadScriptDeferred()](../../../...md#loadScriptDeferred_String_void)** there.
### Arguments

- *string* **path** - Path to the graph file relative to the data directory, or a graph GUID.

### Return value

ID of the new script (1 or greater), or -1 on failure (the failure reason is logged).
## int LoadScriptForEntity ( string path , string entity_id )

Loads a scenario graph like **[LoadScript()](../../../...md#loadScript_String_int)** and binds the new script to the given entity identifier, which the graph can read and **[FindScriptIdByEntity()](../../../...md#findScriptIdByEntity_String_int)** can search for.
### Arguments

- *string* **path** - Path to the graph file relative to the data directory, or a graph GUID.
- *string* **entity_id** - Entity identifier string the new script is bound to.

### Return value

ID of the new script, or -1 on failure.
## int LoadScriptFromJson ( string json , string source = "" )

Loads a scenario graph directly from a JSON string instead of a file (this is how the plugin's web editor runs a graph).
### Arguments

- *string* **json** - Graph description as a JSON string.
- *string* **source** - Name assigned to the script; if empty, an automatic editor-graph name is generated.

### Return value

ID of the new script, or -1 if the JSON cannot be parsed.
## void UnloadScript ( int id )

Stops and destroys the script with the given ID: its shutdown chain runs, the script-unloaded event is fired, and the script is torn down. An unknown ID is silently ignored. Not safe to call from the public event callbacks; use **[UnloadScriptDeferred()](../../../...md#unloadScriptDeferred_int_void)** there.
### Arguments

- *int* **id** - ID of the script to unload.

## void UnloadAllScripts ( )

Unloads every loaded top-level script, applying the same teardown order as **[UnloadScript()](../../../...md#unloadScript_int_void)** to each. Not safe to call from the public event callbacks; use **[UnloadAllScriptsDeferred()](../../../...md#unloadAllScriptsDeferred_void)** there.
## void LoadScriptDeferred ( string path )

Queues loading of a scenario graph: the operation executes on the main thread at the start of the next update. This is the load variant that is safe to call from the public event callbacks; since the work happens later, no script ID is returned.
### Arguments

- *string* **path** - Path to the graph file relative to the data directory, or a graph GUID.

## void UnloadScriptDeferred ( int id )

Queues unloading of the script with the given ID: the operation executes on the main thread at the start of the next update. This is the unload variant that is safe to call from the public event callbacks.
### Arguments

- *int* **id** - ID of the script to unload; values of 0 and below are ignored.

## void UnloadAllScriptsDeferred ( )

Queues unloading of all scripts: the operation executes on the main thread at the start of the next update. This is the variant that is safe to call from the public event callbacks.
## int FindScriptIdByName ( string name )

Searches the loaded top-level scripts for the first one with the given name.
### Arguments

- *string* **name** - Name of the script (the graph name for file loads, or the source name for JSON loads).

### Return value

ID of the first matching script, or -1 if none is found.
## int FindScriptIdByEntity ( string entity_id )

Searches the loaded scripts for the first one bound to the given entity identifier (via **[LoadScriptForEntity()](../../../...md#loadScriptForEntity_String_String_int)** or the *EntityScript* component).
### Arguments

- *string* **entity_id** - Entity identifier to search for. An empty value returns -1.

### Return value

ID of the first script bound to the given entity, or -1 if none is found.
## int GetScriptId ( int num )

Converts an enumeration index into a script ID. Enumeration walks the top-level scripts only.
### Arguments

- *int* **num** - Enumeration index, in the [0; **[NumScripts](../../../...md#getNumScripts_int)**) range.

### Return value

ID of the script with the given index, or -1 if the index is out of range.
## string GetScriptName ( int id )

Returns the display name of the script with the given ID.
### Arguments

- *int* **id** - ID of the script.

### Return value

Name of the script, or an empty string for an unknown ID.
## string GetScriptPath ( int id )

Returns the current path of the script's graph file, following renames and moves of the source file.
### Arguments

- *int* **id** - ID of the script.

### Return value

Current path of the graph file, or an empty string for an unknown ID or a deleted source file.
## string GetScriptEntityId ( int id )

Returns the entity identifier the script with the given ID was bound to.
### Arguments

- *int* **id** - ID of the script.

### Return value

Entity identifier of the script, or an empty string if the script is not bound or the ID is unknown.
## ScenarioManager.SCRIPT_STATE GetScriptState ( int id )

Returns the current state of the script with the given ID. A script halted on a debugger breakpoint is reported as paused.
### Arguments

- *int* **id** - ID of the script.

### Return value

Current state of the script, one of the *SCRIPT_STATE_** values; *SCRIPT_STATE_STOPPED* for an unknown ID.
## void FireEvent ( string name )

Dispatches a named custom event to all running scripts, triggering every matching event handler node in every running graph, and then fires the public *[EventFired](#getEventFired_Event)* event.
### Arguments

- *string* **name** - Name of the custom event. An empty name does nothing.
