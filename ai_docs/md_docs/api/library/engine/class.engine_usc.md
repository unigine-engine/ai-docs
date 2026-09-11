# Unigine::Engine Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The Engine class is required for the engine [initialization](../../../code/fundamentals/execution_sequence/init.md) and executing the [main loop](../../../code/fundamentals/execution_sequence/main_loop.md) of the program. Also, you can get the engine [startup options](../../../code/command_line.md) through this class.


### See Also


Analogues of C++ *runWorldFunction()* methods are described in the *[engine.world](../../../api/library/engine/class.world_usc.md)* class reference.


Analogues of C++ *runEditorFunction()* methods are described in the *[engine.editor](../../../api/library/engine/class.editor_usc.md)* class reference.


Analogues of C++ *runSystemFunction()* methods are described in the *[engine.system](../../../api/library/common/class.system_usc.md)* class reference.


## Engine Class

### Members

## static bool isInitialized () const

Returns the current value indicating whether the engine is initialized.
### Return value

**true** if the Engine is initialized; otherwise **false**.
## static getAppPath () const

Returns the current path to a directory where binary executable file is stored.
### Return value

Current path to a directory where binary executable file is stored.
## static getDataPath () const

Returns the current path to the data directory.
### Return value

Current path to the data directory.
## static getHomePath () const

Returns the current path to the user's home directory.
### Return value

Current path to the user's home directory.
## static getSavePath () const

Returns the current path to a directory with the default configuration file, saved files, etc.
### Return value

Current path to a directory with the default configuration file, saved files, etc.
## static getCachePath () const

Returns the current path to the directory with cached files.
### Return value

Current path to the directory with cached files.
## static int getNumPluginPaths () const

Returns the current number of directory paths to plugins that were set using the [-plugin_path](../../../code/command_line.md#plugin_path) startup command-line option.
### Return value

Current number of directory paths to plugins that were set using the [-plugin_path](../../../code/command_line.md#plugin_path) startup command-line option.
## static getSystemScript () const

Returns the current path to the system script.
### Return value

Current path to the system script.
## static getSystemCache () const

Returns the current path to the system script cache.
### Return value

Current path to the system script cache.
## static getEditorCache () const

Returns the current path to the editor script cache.
### Return value

Current path to the editor script cache.
## static getVideoApp () const

Returns the current graphics API used for rendering.
### Return value

Current graphics API used for rendering.
## static getSoundApp () const

Returns the current sound API used.
### Return value

Current sound API used.
## static getExternDefine () const

Returns the current list of [external definitions](../../../code/command_line.md#extern_define) specified on the application start-up.
### Return value

Current list of external definitions.
## static getFeatures () const

Returns the current list of features like Direct3D, Microprofile, Geodetic, etc.
### Return value

Current list of features like Direct3D, Microprofile, Geodetic, etc.
## static getVersion () const

Returns the current engine version info.
### Return value

Current engine version info.
## static void setBackgroundUpdate ( Engine.BACKGROUND_UPDATE update )

Sets a new value indicating whether the application window is updated when the window is hidden or out of focus (rendering frames in background). By default your UNIGINE application stops rendering frames and updating its main window, when it window goes out of focus (e.g. user switches to another window). Setting the background update mode enables constant rendering regardless of whether the application window is focused or in the background.
### Arguments

- *[Engine.BACKGROUND_UPDATE](../../../api/library/engine/class.engine_usc.md#BACKGROUND_UPDATE)* **update** - The value indicating whether the application window is updated when the window is hidden or out of focus (rendering frames in background).

## static Engine.BACKGROUND_UPDATE getBackgroundUpdate () const

Returns the current value indicating whether the application window is updated when the window is hidden or out of focus (rendering frames in background). By default your UNIGINE application stops rendering frames and updating its main window, when it window goes out of focus (e.g. user switches to another window). Setting the background update mode enables constant rendering regardless of whether the application window is focused or in the background.
### Return value

Current value indicating whether the application window is updated when the window is hidden or out of focus (rendering frames in background).
## static isActive () const

Returns the current **active** state of the Engine.
### Return value

Current the engine is active
## static isFocus () const

Returns the current value showing if any of the Engine windows is in focus.
### Return value

Current the Engine window is focused
## static isQuit () const

Returns the current **quitting** flag on engine quit.
### Return value

Current the engine is quitting
## static float getTotalTime () const

Returns the current total time (in milliseconds) that both rendering and calculating of the frame took (the duration of the [main loop](../../../code/fundamentals/execution_sequence/main_loop.md) in the application [execution sequence](../../../code/fundamentals/execution_sequence/index.md)). Includes *update, render, swap and wait GPU*.
### Return value

Current total time value, in milliseconds.
## static float getTotalCPUTime () const

Returns the current total CPU time (in milliseconds) taken to perform calculations for the frame (the duration of the [main loop](../../../code/fundamentals/execution_sequence/main_loop.md) in the application [execution sequence](../../../code/fundamentals/execution_sequence/index.md)). Includes *update, render and swap*.
### Return value

Current total CPU time value, in milliseconds.
## static float getUpdateTime () const

Returns the current duration (in milliseconds) of the [update phase](../../../code/fundamentals/execution_sequence/main_loop.md#update), during which the objects are prepared for their collision response to be calculated.
### Return value

Current update phase duration value, in milliseconds.
## static float getRenderTime () const

Returns the current time (in milliseconds) required to prepare all data to be rendered in the current frame and feed rendering commands from the CPU to the GPU. See the [Profiler](../../../tools/profiling/profiler/index.md#render_cpu) article for details.
### Return value

Current rendering time value, in milliseconds.
## static float getPresentTime () const

Returns the current total time (in milliseconds) spent on waiting for the GPU after all calculations on the CPU are completed. See the [Profiler](../../../tools/profiling/profiler/index.md#present) article for details.
### Return value

Current time value, in milliseconds.
## static float getInterfaceTime () const

Returns the current total accumulative time (in milliseconds) spent on rendering GUI widgets.
### Return value

Current time value, in milliseconds.
## static int64_t getFrame () const

Returns the current number of the current engine frame.
### Return value

Current engine frame number.
## static float getFps () const

Returns the current value of the Engine FPS counter.
### Return value

Current value of the Engine FPS counter.
## static float getIFps () const

Returns the current inverse value of the Engine FPS counter (1/FPS).
### Return value

Current inverse value of the Engine FPS counter (1/FPS).
## static float getStatisticsFpsMin () const

Returns the current minimum FPS counter value for the last 600 frames.
### Return value

Current minimum FPS counter value for the last 600 frames.
## static float getStatisticsFpsAvg () const

Returns the current average FPS counter value for the last 600 frames.
### Return value

Current average FPS counter value for the last 600 frames.
## static float getStatisticsFpsMax () const

Returns the current maximum FPS counter value for the last 600 frames.
### Return value

Current maximum FPS counter value for the last 600 frames.
## static isMainThread () const

Returns the current value indicating if the current thread is main.
### Return value

Current the current thread is main
## static Player getMainPlayer () const

Returns the current main player.
### Return value

Current main player.
## static isEvaluation () const

Returns the current value indicating if the running version of the Engine is for evaluation only.
### Return value

Current the evaluation version of the Engine is used
## static int getNumEditorLogics () const

Returns the current number of [EditorLogic](../../../api/library/common/logic/class.editorlogic_usc.md) instances.
### Return value

Current number of [EditorLogic](../../../api/library/common/logic/class.editorlogic_usc.md) instances.
## static int getNumWorldLogics () const

Returns the current number of [WorldLogic](../../../api/library/common/logic/class.worldlogic_usc.md) instances.
### Return value

Current number of [WorldLogic](../../../api/library/common/logic/class.worldlogic_usc.md) instances.
## static int getNumSystemLogics () const

Returns the current number of [SystemLogic](../../../api/library/common/logic/class.systemlogic_usc.md) instances.
### Return value

Current number of [SystemLogic](../../../api/library/common/logic/class.systemlogic_usc.md) instances.
## static int getNumArgs () const

Returns the current number of command line arguments.
### Return value

Current number of command line arguments.
## static int getNumPlugins () const

Returns the current number of loaded plugins.
### Return value

Current number of loaded plugins.
## static getPrecision () const

Returns the current precision type.
### Return value

Current precision type.
## static Event getEventBeginUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginPropertiesUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndPropertiesUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginInputUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndInputUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginControlsUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndControlsUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginWorldManagerUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndWorldManagerUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginSoundManagerUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndSoundManagerUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginGameUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndGameUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginRenderUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndRenderUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginExpressionUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndExpressionUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginSoundsUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndSoundsUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginPluginsUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndPluginsUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginVRUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndVRUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginEditorUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndEditorUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginSystemScriptUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndSystemScriptUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginSystemLogicUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndSystemLogicUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginWorldUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndWorldUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginAnimationManagerUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndAnimationManagerUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginWorldPostUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndWorldPostUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginSystemScriptPostUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndSystemScriptPostUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginSystemLogicPostUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndSystemLogicPostUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginEditorPostUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndEditorPostUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginPluginsPostUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndPluginsPostUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginSpatialUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndSpatialUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginFilesystemUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndFilesystemUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginPathfinding () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndUpdate () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventSyncBeginFramePhysics () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventSyncEndFramePhysics () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventAsyncBeginFramePhysics () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventAsyncEndFramePhysics () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginVRRender () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndVRRender () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginRender () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginEditorRender () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndEditorRender () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginPluginsRender () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndPluginsRender () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginRenderWorld () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndRenderWorld () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginPluginsGui () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndPluginsGui () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginPostRender () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndPostRender () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndRender () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginSwap () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndPathfinding () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginWorldSwap () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndWorldSwap () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginPluginsSwap () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndPluginsSwap () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventBeginDeleteObjects () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndDeleteObjects () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventEndSwap () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventFocusGained () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static Event getEventFocusLost () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPluginAdded () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventPluginRemoved () const

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

## virtual engine. getArg ( int num )

Returns a [command line](../../../code/command_line.md) argument by its index.
### Arguments

- *int* **num** - Index of the command line argument.

### Return value

Command line argument.
## static engine. getLibraryModulePath ( )

Returns a path to the Engine's dynamic library file.
### Return value

Path to the Engine's dynamic library file.
## virtual engine. getArg ( int num ) =0

Returns the command-line argument by its index.
### Arguments

- *int* **num** - Index of the argument.

### Return value

Command-line argument
## int engine. getPluginOrder ( int num )

Returns the execution order of the specified loaded plugin by calling its *[get_order()()](../../../api/library/common/class.plugin_usc.md#get_order_int)* method.
### Arguments

- *int* **num** - Index of the loaded plugin.

### Return value

Loaded plugin execution order.
## engine. getPluginPath ( int num )

Returns a path to a plugin directory specified via [-plugin_path](../../../code/command_line.md#plugin_path).
### Arguments

- *int* **num** - Plugin path number in the row of the specified plugin paths.

### Return value

Path to a plugin directory.
## engine. getPluginAbsolutePath ( int num )

Returns an absolute path to a plugin directory.
### Arguments

- *int* **num** - Plugin path number in the row of the specified plugin paths.

### Return value

Absolute path to a plugin directory.
## void engine. dialogError ( string title )

Displays a dialog window with errors set using the *[error()](#error_cstr_vargs_void)* function.
### Arguments

- *string* **title** - Title to be displayed in the error window.

## void engine. dialogMessage ( string title )

Displays a dialog window with the last message set using the *[message()](#message_cstr_vargs_void)* function.
### Arguments

- *string* **title** - Title to be displayed in the message window.

## void engine. error ( string format , ... values )

Adds a text describing an error to the list of errors.
### Arguments

- *string* **format** - Format of the error text. See the [formatting string description](../../../code/uniginescript/language/strings_global_usc.md#format_string).
- *...* **values** - Arguments, multiple allowed.

## void engine. message ( string format , ... values )

Adds a new message to the list of messages.
### Arguments

- *string* **format** - Format of the message text. See the [formatting string description](../../../code/uniginescript/language/strings_global_usc.md#format_string).
- *...* **values** - Arguments, multiple allowed.

## void engine. beginOutsideLoopRender ( )

Starts a block of code where you can call *[Render](../../../api/library/rendering/class.render_usc.md)* class methods from outside the Engine's Loop. The end of this block should be marked with a call to the **[endOutsideLoopRender()()](../../...md#endOutsideLoopRender_void)** method.
## void engine. endOutsideLoopRender ( )

Closes a block of code where you can call *[Render](../../../api/library/rendering/class.render_usc.md)* class methods from outside the Engine's Loop started with a call to the **[beginOutsideLoopRender()()](../../...md#beginOutsideLoopRender_void)** method.
## void engine. startFps ( )

Starts the FPS counter if it was stopped. All function calls are placed into a stack, so the number of calls to this function should correspond to the number of calls to the *[stopFps()](#stopFps_void)* function.
## void engine. stopFps ( )

Stops the FPS counter. This function should be called if application window is hidden or some heavy non-rendering tasks are processing. All function calls are placed into a stack, so the number of calls to this function should correspond to the number of calls to the *[startFps()](#startFps_void)* function.
## int engine. getVideoContextFlags ( )

Returns the current video context flags.
### Return value

A set of current video context flags as an integer value.
## void engine. quit ( )

The Engine requests to exit the application.
