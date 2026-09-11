# Engine Main Loop


This article describes in detail the steps performed by the UNIGINE Engine each frame: **Update**, **Render**, and **Swap**.


At almost every stage of execution, the Engine **emits events**. You can subscribe to this events and run your own code when they occur, enabling flexible customization of application logic beyond the default lifecycle methods.


The total time the main loop has taken is displayed by the ***Total*** counter in the [Performance Profiler](../../../tools/profiling/profiler/index.md).


For other steps and general information about execution sequence, see the [Execution Sequence](../../../code/fundamentals/execution_sequence/index.md) article.


## Update Stage


The ***Update*** stage is the preparation phase for rendering the next frame and the core stage where application logic is executed.


During this stage, the Engine:


<details>
<summary>Update Steps</summary>

| Update Prepare | Related Event |
|---|---|
| 1. The process priority in the operating system is adjusted. |  |
| 2. [Input](../../../api/library/controls/class.input_cpp.md), including standard and VR, is updated. | *[EventBeginInputUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginInputUpdate_Event) [EventEndInputUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndInputUpdate_Event)* |
| 3. The Engine wakes up worker threads in the [thread pools](../../../code/fundamentals/thread_system/index.md#thread_pools) to process any pending tasks. |  |
| 4. If a world was unloaded in the previous frame and a new world must be loaded, the Engine loads it with all settings applied. |  |
| 5. The [Console](../../../code/console/index.md) is updated. All pending console commands that were called during the previous frame are executed. The commands are executed in the beginning of the Update Stage, but before the scripts are updated, because otherwise they may violate the current process of rendering or physical calculations. |  |
| 6. The Engine prepares for the next frame rendering. |  |
| Main Update | *[EventBeginUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginUpdate_Event)* |
| 1. The Engine updates [properties](../../../principles/properties/index.md). This step is independent of the component system and handles cases such as property reparenting. | *[EventBeginPropertiesUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginPropertiesUpdate_Event) [EventEndPropertiesUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndPropertiesUpdate_Event)* |
| 2. [Controls](../../../api/library/controls/class.controls_cpp.md) are updated. | *[EventBeginControlsUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginControlsUpdate_Event) [EventEndControlsUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndControlsUpdate_Event)* |
| 3. World Manager, which is responsible for image and mesh streaming resources is updated. | *[EventBeginWorldManagerUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginWorldManagerUpdate_Event) [EventEndWorldManagerUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndWorldManagerUpdate_Event)* |
| 4. Sound Manager, which is responsible responsible for sound streaming resources is updated. | *[EventBeginSoundManagerUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginSoundManagerUpdate_Event) [EventEndSoundManagerUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndSoundManagerUpdate_Event)* |
| 5. The Engine updates the *[Game](../../../api/library/engine/class.game_cpp.md)* class state and recalculates [Time](../../../api/library/engine/class.game_cpp.md#getTime_float). | *[EventBeginGameUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginGameUpdate_Event) [EventEndGameUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndGameUpdate_Event)* |
| 6. *[Render](../../../api/library/rendering/class.render_cpp.md)* class is updated. It includes light baking, animation timing, materials, and camera positions. | *[EventBeginRenderUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginRenderUpdate_Event) [EventEndRenderUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndRenderUpdate_Event)* |
| 7. The Engine updates [Expressions](../../../api/library/common/class.expression_cpp.md) and sets the new game time for correct RNG. | *[EventBeginExpressionUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginExpressionUpdate_Event) [EventEndExpressionUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndExpressionUpdate_Event)* |
| 8. [Sound](../../../api/library/engine/class.sound_cpp.md) is updated and all streamed audio starts playing. | *[EventBeginSoundsUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginSoundsUpdate_Event) [EventEndSoundsUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndSoundsUpdate_Event)* |
| 9. [World Logics](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic) and [Editor Logics](../../../code/fundamentals/execution_sequence/app_logic_system.md#editorlogic) are initialized. This means if a new world was loaded (either at application start or when switching worlds), its world script and logic are initialized here. The *[init()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_init)* method of all your components is also called, since the Component system inherits from the WorldLogic. This includes both components that already existed in the world and those that were added in runtime - all of them receive their *init()* call at this stage. - World Script *[init()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_init)* method is called. - WorldLogic *[init()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_init)* method is called (Components *init()* method is called. You can define components initialization order: see the component class description for *[C++](../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md#methods_order)* or for *[C#](../../../api/library/common/logic/component_system/cs/class.component.md#methods)*). - Editor Script *[worldInit()](../../../code/fundamentals/execution_sequence/app_logic_system.md#editorlogic_worldInit)* method is called. - EditorLogic *[worldInit()](../../../code/fundamentals/execution_sequence/app_logic_system.md#editorlogic_worldInit)* method is called. |  |
| 10. [Plugins](../../../api/library/common/class.plugin_cpp.md) are updated. The *[update()](../../../api/library/common/class.plugin_cpp.md#update_void)* method of all plugins is called. Use *[get_order()](../../../api/library/common/class.plugin_cpp.md#get_order_int)* to set each plugin's update priority. | *[EventBeginPluginsUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginPluginsUpdate_Event) [EventEndPluginsUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndPluginsUpdate_Event)* |
| 11. [VR](../../../api/library/vr/class.vr_cpp.md) is updated, configuring internal rendering settings and applying parsed console commands. | *[EventBeginVRUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginVRUpdate_Event) [EventEndVRUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndVRUpdate_Event)* |
| 12. [Editor Logics](../../../code/fundamentals/execution_sequence/app_logic_system.md#editor_logic) are updated. - Editor Scrpit *[update()](../../../code/fundamentals/execution_sequence/app_logic_system.md#editorlogic_update)* method is called. - EditorLogic *[update()](../../../code/fundamentals/execution_sequence/app_logic_system.md#editorlogic_update)* method is called. | *[EventBeginEditorUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginEditorUpdate_Event) [EventEndEditorUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndEditorUpdate_Event)* |
| 13. [System Logics](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic) are updated. - System Scrpit *[update()](../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic_update)* method is called. - SystemLogic *[update()](../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic_update)* method is called. | *[EventBeginSystemScriptUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginSystemScriptUpdate_Event) [EventEndSystemScriptUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndSystemScriptUpdate_Event) [EventBeginSystemLogicUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginSystemLogicUpdate_Event) [EventEndSystemScriptUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndSystemScriptUpdate_Event)* |
| 14. [World Logics](../../../code/fundamentals/execution_sequence/app_logic_system.md#world_logic) are updated. - [World Expressions](../../../objects/worlds/world_expression/index.md) are executed. - [Node References](../../../objects/nodes/reference/index.md) are scheduled for loading. - World Logic *[updateAsyncThread()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_updateAsyncThread)* is called (Components *updateAsyncThread()* method is called. You can define components execution order: see the component class description for *[C++](../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md#methods_order)* or for *[C#](../../../api/library/common/logic/component_system/cs/class.component.md#methods)*) - World Logic [*updateSyncThread()*](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_updateSyncThread) is called (Components *updateSyncThread()* method is called) - World Scrpit *[update()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_update)* method is called. - World Logic *[update()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_update)* is called (Components *update()* method is called) - The state of nodes existing in the world is updated (mostly for visible nodes): skinned animation is played, particle systems spawn new particles, players are repositioned, and so on. - Nodes are pre-rendered - *[World Clutter](../../../objects/worlds/world_clutter/index.md)* nodes are updated (or spawned if necessary) - *[Node Trigger](../../../objects/nodes/trigger/index.md)* events are invoked (see the *[NodeTrigger](../../../api/library/nodes/class.nodetrigger_cpp.md)* class) - *[World Trigger](../../../objects/worlds/world_trigger/index.md)* events are invoked (see the *[WorldTrigger](../../../api/library/worlds/class.worldtrigger_cpp.md)* class) | *[EventBeginWorldUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginWorldUpdate_Event) [EventEndWorldUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndWorldUpdate_Event)* |
| 15. [Animations](../../../principles/animations/index.md) are updated based on a new time. | *[EventBeginAnimationManagerUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginAnimationManagerUpdate_Event)* *[EventEndAnimationManagerUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndAnimationManagerUpdate_Event)* |
| 16. Engine GUI is updated. |  |
| PostUpdate Stage |  |
| 1. [World Logics](../../../code/fundamentals/execution_sequence/app_logic_system.md#world_logic) are post-updated. - World Scrpit *[postUpdate()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_postUpdate)* method is called. - WorldLogic *[postUpdate()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_postUpdate)* method is called (Components *postUpdate()* method is called. You can define components execution order: see the component class description for *[C++](../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md#methods_order)* or for *[C#](../../../api/library/common/logic/component_system/cs/class.component.md#methods)*). - World spatial tree is rendered. | *[EventBeginWorldPostUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginWorldPostUpdate_Event)* *[EventEndWorldPostUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndWorldPostUpdate_Event)* |
| 2. [System Logics](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic) are post-updated. - System Scrpit *[postUpdate()](../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic_postUpdate)* method is called. - SystemLogic *[postUpdate()](../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic_postUpdate)* method is called. | *[EventBeginSystemScriptPostUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginSystemScriptPostUpdate_Event)* *[EventEndSystemScriptPostUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndSystemScriptPostUpdate_Event)* *[EventBeginSystemLogicPostUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginSystemLogicPostUpdate_Event)* *[EventEndSystemLogicPostUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndSystemLogicPostUpdate_Event)* |
| 3. [Editor Logics](../../../code/fundamentals/execution_sequence/app_logic_system.md#editor_logic) are post-updated. - Editor Scrpit *[postUpdate()](../../../code/fundamentals/execution_sequence/app_logic_system.md#editorlogic_postUpdate)* method is called. - EditorLogic *[postUpdate()](../../../code/fundamentals/execution_sequence/app_logic_system.md#editorlogic_postUpdate)* method is called. | *[EventBeginEditorPostUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginEditorPostUpdate_Event)* *[EventEndEditorPostUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndEditorPostUpdate_Event)* |
| 4. [Plugins](../../../api/library/common/class.plugin_cpp.md) are post-updated. The *[postUpdate()](../../../api/library/common/class.plugin_cpp.md#postUpdate_void)* method of all plugins is called. Use *[get_order()](../../../api/library/common/class.plugin_cpp.md#get_order_int)* to set each plugin's post-update priority. | *[EventBeginPluginsPostUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginPluginsPostUpdate_Event)* *[EventEndPluginsPostUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndPluginsPostUpdate_Event)* |
| 5. [File System](../../../principles/filesystem/index_cpp.md) is processed, triggering the corresponding events (see *[FileSystem](../../../api/library/filesystem/class.filesystem_cpp.md) class*) | *[EventBeginFilesystemUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginFilesystemUpdate_Event)* *[EventEndFilesystemUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndFilesystemUpdate_Event)* |
| 6. The internal queue of Engine asynchronous tasks is updated. New tasks are added for later execution, such as [data streaming](../../../principles/data_streaming/index.md) tasks. |  |
| 7. A batch of asynchronous tasks is executed in separate threads taken from the Engine's internal thread pool: - World Spatial Tree is scheduled for updating. - Buffers used for particles are updated (Vulkan API only). - *AsyncQueue* loading of files/meshes/nodes on demand is performed. - *Landscape* async operations are performed. - Async tasks updated on step **6** are executed. - Unused skinned meshes are unloaded. | *[EventBeginSpatialUpdate](../../../api/library/engine/class.engine_cpp.md#getEventBeginSpatialUpdate_Event)* |
| 8. *[Landscape](../../../api/library/objects/landscape_terrain/class.landscape_cpp.md)* operations and textures are updated for proper execution. |  |
| 9. [Mesh Decals](../../../objects/decals/mesh/index.md) are updated. |  |
| 10. *WindowManager* is updated (GUI is refreshed). |  |
| 11. Now the Engine waits until all tasks started at step **7** are finished. |  |
| 12. The Pathfinding thread is executed. | *[EventBeginPathfinding](../../../api/library/engine/class.engine_cpp.md#getEventBeginPathfinding_Event)* *[EventEndSpatialUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndSpatialUpdate_Event)* |
| 13. If physics update mode is set to run before rendering, the Engine starts the **[physics simulation](#physics)** and waits until it completes. | *[EventEndUpdate](../../../api/library/engine/class.engine_cpp.md#getEventEndUpdate_Event)* |

</details>


## Render Stage


The ***Render*** stage is the phase of the main loop where the current world is drawn and the final image is prepared for presentation.


This stage executes the rendering pipeline, updates visual resources, and produces the frame that will be displayed on screen.


Rendering is performed differently depending on the application mode. If VR is enabled, a preliminary render pass for the VR device is performed first. This pass includes the following steps:


<details>
<summary>VR Rendering Steps</summary>

| VR Render Stage | Related Event |
|---|---|
| 1.The player camera is updated according to the HMD pose in the real world, including position, orientation, and VR-specific parameters |  |
| 2. Rendering is prepared with API-specific tasks: configuring or reusing VR swapchains and setting up per-eye viewports and projection matrices. | *[EventBeginVRRender](../../../api/library/engine/class.engine_cpp.md#getEventBeginVRRender_Event)* |
| 3. The scene is rendered separately for each eye into the corresponding swapchain buffers, using VR view and projection parameters. |  |
| 4. Device-dependent steps are applied (e.g. a Motion Prediction). |  |
| 5. Additional overlay or quad layers (if any) are composed, and the completed frame(s) are submitted to the VR runtime. |  |
| 6. The VR rendering stage is completed. | *[EventEndVRRender](../../../api/library/engine/class.engine_cpp.md#getEventEndVRRender_Event)* |

</details>


After VR rendering is completed (or VR mode is disabled), the Engine executes the main rendering sequence for the application window. A detailed description of the rendering pipeline is beyond the scope of this article and is provided in the **[Rendering Sequence](../../../principles/render/sequence/index.md)** article.


<details>
<summary>Regular Rendering Steps</summary>

| Regular Render Stage | Related Event |
|---|---|
| 1. The windows to be rendered are configured | *[EventBeginRender](../../../api/library/engine/class.engine_cpp.md#getEventBeginRender_Event)* |
| 2. If required, GUI elements are rendered. |  |
| 3. UNIGINE renders the graphics scene (the world). The graphics scene is sent to GPU. As soon as the CPU finishes preparation of data and feeds rendering commands to the GPU, the GPU becomes busy with rendering the frame. The total time of [rendering stage](../../../principles/render/sequence/index.md) is displayed by the Render CPU counter in the Performance Profiler. After that, the CPU is free, so we can load it with calculations we need. | *[EventBeginRenderWorld](../../../api/library/engine/class.engine_cpp.md#getEventBeginRenderWorld_Event)* *[EventEndRenderWorld](../../../api/library/engine/class.engine_cpp.md#getEventEndRenderWorld_Event)* |
| 4. [Editor Logics](../../../code/fundamentals/execution_sequence/app_logic_system.md#editor_logic) *render()* method is called. - Editor Scrpit *[render()](../../../code/fundamentals/execution_sequence/app_logic_system.md#editorlogic_render)* method is called. - EditorLogic *[render()](../../../code/fundamentals/execution_sequence/app_logic_system.md#editorlogic_render)* method is called. | *[EventBeginEditorRender](../../../api/library/engine/class.engine_cpp.md#getEventBeginEditorRender_Event)* *[EventEndEditorRender](../../../api/library/engine/class.engine_cpp.md#getEventEndEditorRender_Event)* |
| 5. Plugins *[render()](../../../api/library/common/class.plugin_cpp.md#render_const_EngineWindowViewportPtr_ref_void)* method is called. Use *[get_order()](../../../api/library/common/class.plugin_cpp.md#get_order_int)* to set each plugin's render priority. | *[EventBeginPluginsRender](../../../api/library/engine/class.engine_cpp.md#getEventBeginPluginsRender_Event)* *[EventEndPluginsRender](../../../api/library/engine/class.engine_cpp.md#getEventEndPluginsRender_Event)* |
| 6. Plugins *[gui()](../../../api/library/common/class.plugin_cpp.md#gui_const_EngineWindowViewportPtr_ref_void)* method is called. Use *[get_order()](../../../api/library/common/class.plugin_cpp.md#get_order_int)* to set each plugin's gui priority. | *[EventBeginPluginsGui](../../../api/library/engine/class.engine_cpp.md#getEventBeginPluginsGui_Event)* *[EventEndPluginsGui](../../../api/library/engine/class.engine_cpp.md#getEventEndPluginsGui_Event)* |
| 7. [Visualizer](../../../api/library/engine/class.visualizer_cpp.md) is rendered. | *[EventBeginPostRender](../../../api/library/engine/class.engine_cpp.md#getEventBeginPostRender_Event)* *[EventEndPostRender](../../../api/library/engine/class.engine_cpp.md#getEventEndPostRender_Event)* |
| 8. The rendering stage is completed. | *[EventEndRender](../../../api/library/engine/class.engine_cpp.md#getEventEndRender_Event)* |

</details>


## Swap Stage


The ***Swap*** stage is the final phase of the main loop.


Here the Engine completes all pending tasks for the current frame, performs cleanup of resources, calls *swap()* methods of user logic and plugins, and finalizes the state before starting the next update cycle.


<details>
<summary>Swap Steps</summary>

| Swap Stage | Related Event |
|---|---|
| The *Swap* stage begins. | *[EventBeginSwap](../../../api/library/engine/class.engine_cpp.md#getEventBeginSwap_Event)* |
| 1. If the physics update mode is set to update asynchronously with rendering, the Engine pauses execution until the physics simulation is completed. (Unlike [the end of the Post-Update stage](#physics_before), where physics is executed synchronously before rendering). |  |
| 2. The Engine pauses execution until the pathfinding thread completes. | *[EventEndPathfinding](../../../api/library/engine/class.engine_cpp.md#getEventEndPathfinding_Event)* |
| 3. On this step, the Engine finalizes rendering the current frame. Temporary textures are released, internal states are cleared an so on. |  |
| 4. The Engine performs [frame synchronization](../../../code/fundamentals/thread_system/index.md#frame_sync): all tasks with *FrameSyncMode::Swap* must finish before the frame continues. At this stage, the Engine also waits for the *[updateAsyncThread()](#world_update)* method to complete (it runs on the internal thread pool). |  |
| 5. GUI events (if any) are dispatched and GUI resources are released. The complete list of related events is provided in the *[Widget](../../../api/library/gui/class.widget_cpp.md)* class. |  |
| 6. *[World Logic](../../../code/fundamentals/execution_sequence/app_logic_system.md#world_logic) swap()* is called: - WorldLogic *[swap()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_swap)* method is called (Components *swap()* method is called. You can define components execution order: see the component class description for *[C++](../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md#methods_order)* or for *[C#](../../../api/library/common/logic/component_system/cs/class.component.md#methods)*). | *[EventEndPathfinding](../../../api/library/engine/class.engine_cpp.md#getEventEndPathfinding_Event)* |
| 7. Plugins *[swap()](../../../api/library/common/class.plugin_cpp.md#swap_void)* method is called. Use *[get_order()](../../../api/library/common/class.plugin_cpp.md#get_order_int)* to set each plugin's swap priority. | *[EventBeginPluginsSwap](../../../api/library/engine/class.engine_cpp.md#getEventBeginPluginsSwap_Event)* *[EventEndPluginsSwap](../../../api/library/engine/class.engine_cpp.md#getEventEndPluginsSwap_Event)* |
| 8. If you requested the Engine to quit the current world or load another world (e.g. via [*world_quit*](../../../code/console/index.md#world_quit)) within the current frame, the Engine will do it here, this includes: - Editor Script *[worldShutdown()](../../../code/fundamentals/execution_sequence/app_logic_system.md#editorlogic_worldShutdown)* method is called. - EditorLogic *[worldShutdown()](../../../code/fundamentals/execution_sequence/app_logic_system.md#editorlogic_worldShutdown)* method is called. - World script *[shutdown()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_shutdown)* method is called. - WorldLogic *[shutdown()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_shutdown)* method is called (Components *shutdown()* method is called. You can define components execution order: see the component class description for *[C++](../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md#methods_order)* or for *[C#](../../../api/library/common/logic/component_system/cs/class.component.md#methods)*). |  |
| 9. All of the [Profiling Metrics](../../../tools/profiling/profiler/index.md) are updated. |  |
| 10. Asynchronous data streaming tasks are executed. |  |
| 11. If FPS synchronization between the Engine and the physics is enabled, the Engine delays the frame to match the physics update rate. |  |
| 12. All of the objects marked for deletion via *[deleteLater()](../../../code/fundamentals/smartpointers.md#delete)* are deleted. | *[EventBeginDeleteObjects](../../../api/library/engine/class.engine_cpp.md#getEventBeginDeleteObjects_Event)* *[EventEndDeleteObjects](../../../api/library/engine/class.engine_cpp.md#getEventEndDeleteObjects_Event)* |
| 13. CPU and GPU are synchronized. See *[Waiting GPU](../../../code/fundamentals/execution_sequence/index.md#waiting_gpu)* to learn more. |  |
| 14. *[Microprofiler](../../../tools/profiling/microprofile/index_cpp.md)* writes values for this frame. |  |
| 15. Application framerate is updated. |  |
| 16. The Engine updates frame statistics and goes to *[Update](#update)* stage. | *[EventEndSwap](../../../api/library/engine/class.engine_cpp.md#getEventEndSwap_Event)* |

</details>


## Physics Update


Depending on the [selected settings](../../../editor2/settings/physics_global/index.md), physics can be updated either synchronously [at the end of the *Update* stage](#physics_before) or asynchronously [during the *Render* stage](#physics_async).


Also note that physics is not necessarily updated every frame along with the main update-render-swap cycle as it has its own framerate.


For details on configuration and execution modes, see: **[Simulation of Physics](../../../principles/physics/simulation.md)**


Regardless of the chosen mode, the physics update cycle remains the same and includes the following steps:


<details>
<summary>Physics Update Steps</summary>

| Physics Update | Related Event |  |
|---|---|---|
| 1. | The timer to store physics simulation time is set. | *[EventSyncBeginFramePhysics](../../../api/library/engine/class.engine_cpp.md#getEventSyncBeginFramePhysics_Event)* |
| 2. | Plugins *[updatePhysics()](../../../api/library/common/class.plugin_cpp.md#updatePhysics_void)* is called. |  |
| 3. | *[World Logic](../../../code/fundamentals/execution_sequence/app_logic_system.md#world_logic) updatePhysics()* are called. - World Scrpit *[updatePhysics()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_updatePhysics)* method is called. - WorldLogic *[updatePhysics()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_updatePhysics)* method is called (Components *updatePhysics()* method is called. You can define components execution order: see the component class description for *[C++](../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md#methods_order)* or for *[C#](../../../api/library/common/logic/component_system/cs/class.component.md#methods)*). |  |
| 4. | The spatial tree is flushed to apply all pending physics changes. |  |
| 6. | The collision detection stage is performed. During the collision detection stage, the Engine finds active bodies, builds islands, detects contacts, and prepares data for collision resolution. | *[EventAsyncBeginFramePhysics](../../../api/library/engine/class.engine_cpp.md#getEventAsyncBeginFramePhysics_Event)* |
| 7. | The simulation stage is performed. During the simulation stage, the Engine computes collision responses and joint constraints, accumulates the results, and applies new velocities and positions to bodies. |  |
| 8. | The physics scene is being updated. | *[EventAsyncEndFramePhysics](../../../api/library/engine/class.engine_cpp.md#getEventAsyncEndFramePhysics_Event)* |
| 9. | Events associated with [bodies and joints](../../../code/fundamentals/events/index_cpp.md#physics), and [physical triggers](../../../objects/effects/physicals/physical_trigger/index.md), are triggered. |  |
| 10. | The physics update timer is stopped and the result is recorded for display in the Profiler. | *[EventSyncEndFramePhysics](../../../api/library/engine/class.engine_cpp.md#getEventSyncEndFramePhysics_Event)* |

</details>
