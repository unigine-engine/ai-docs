# Engine Shutdown


This article describes in detail the steps performed by the UNIGINE Engine during shutdown.


During shutdown, the Engine sequentially terminates logics, stops rendering, shuts down plugins and threads, and releases resources.


For other steps and general information about execution sequence, see the [Execution Sequence](../../../code/fundamentals/execution_sequence/index.md) article.


| Engine Shutdown |  |
|---|---|
| 1. | [Editor Logics](../../../code/fundamentals/execution_sequence/app_logic_system.md#editor_logic) *shutdown()* method is called. - Editor Script *[shutdown()](../../../code/fundamentals/execution_sequence/app_logic_system.md#editorlogic_shutdown)* method is called. - EditorLogic *[shutdown()](../../../code/fundamentals/execution_sequence/app_logic_system.md#editorlogic_shutdown)* method is called. |
| 2. | [World Logics](../../../code/fundamentals/execution_sequence/app_logic_system.md#world_logic) *shutdown()* method is called. - World Scrpit *[shutdown()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_shutdown)* method is called. - WorldLogic *[shutdown()](../../../code/fundamentals/execution_sequence/app_logic_system.md#worldlogic_shutdown)* method is called (Components *shutdown()* method is called You can define components execution order: see the component class description for *[C++](../../../api/library/common/logic/component_system/cpp/class.componentbase_cpp.md#methods_order)* or for *[C#](../../../api/library/common/logic/component_system/cs/class.component.md#methods)*). |
| 3. | [System Logics](../../../code/fundamentals/execution_sequence/app_logic_system.md#system_logic) *shutdown()* method is called. - System Scrpit *[shutdown()](../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic_shutdown)* method is called. - SystemLogic *[shutdown()](../../../code/fundamentals/execution_sequence/app_logic_system.md#systemlogic_shutdown)* method is called. |
| 4. | VR systems are shut down and their resources are released. |
| 5. | The [Memory profiler](../../../tools/profiling/profiler/index.md) is shut down. |
| 6. | Plugins *[shutdown()](../../../api/library/common/class.plugin_cpp.md#shutdown_int)* method is called. Use *[get_order()](../../../api/library/common/class.plugin_cpp.md#get_order_int)* to set each plugin's shutdown priority. |
| 7. | The rendering process stops and shuts down. |
| 8. | *Landscape* files are closed. |
| 9. | Console history is saved. |
| 10. | All Engine threads are shut down. |
| 11. | The sound system is shut down. |
| 12. | The *SystemProxy* is shut down. |
| 13. | [Procedural mesh caches](../../../code/console/index.md#mesh_procedural_path) are cleared and removed. |
| 14. | The total shutdown time is printed to the log. |
| 15. | All resources allocated by UNIGINE are released. |
| 16. | [Memory Allocator](../../../principles/allocator/index.md) is shut down. |
