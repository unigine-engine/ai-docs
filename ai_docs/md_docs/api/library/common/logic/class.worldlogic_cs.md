# Unigine::WorldLogic Class (CS)


The *WorldLogic* class is used to control the logic of the world. Methods of this class are called after corresponding methods of the world script **only if the world is loaded**.


> **Notice:** Instances of the WorldLogic class should not be added or removed via the corresponding methods of the Engine class (*[addWorldLogic()](../../../../api/library/engine/class.engine_cs.md#addWorldLogic_WorldLogic_ptr_bool) / [removeWorldLogic()](../../../../api/library/engine/class.engine_cs.md#removeWorldLogic_WorldLogic_ptr_bool)*) while the world is loaded and the world script is being executed (as you can't change a world script while the world is loaded). In such a case **there's no guarantee that *init() / shutdown()* methods shall be called**:
>
>
> - the ***init()*** method shall not be called if the WorldLogic is added after opening the world;
> - the ***shutdown()*** method shall not be called if the WorldLogic is removed before closing the world.


### See Also


- Example on [Sharing Data between the Logic System Components](../../../../code/usage/sharing_data/index_cs.md)
- Example on [Splitting Logic Between Several WorldLogic Classes](../../../../code/usage/multiple_worldlogic/index_cs.md)


## WorldLogic Class

### Members

---

## virtual bool Init ( )

 Engine calls this function on world initialization and initializes resources for a world scene during the world start.
### Return value

Returns true if there were no errors; otherwise, false.
## virtual bool Shutdown ( )

Engine calls this function on world shutdown. Here you can delete resources that were created during world script execution to avoid memory leaks.
### Return value

Returns true if there were no errors; otherwise, false.
## virtual bool Update ( )

Engine calls this function before updating each render frame. You can specify here all logic-related functions you want to be called every frame while your application executes.
### Return value

Returns true if there were no errors; otherwise, false.
## virtual void UpdateSyncThread ( int id , int size )

Engine calls this function before the [*update()*](#update_int) and the [*postUpdate()*](#postUpdate_int).
 Limitations: you should not create or modify nodes unless you're absolutely sure that no other thread can do the same. This function is called **size** times each frame and executed in parallel threads. Each time the function is called with an index in the range [0; size), i.e.: 0, 1, ..., size-1. This function **blocks the Main Thread** until all **size** calls are completed.
 Unlike the [*SyncThread()*](#updateAsyncThread_int_int_void) this function has got less time for execution, but it is more secure and is suitable for complex calculations to be applied to the current node.
### Arguments

- *int* **id** - Index of the current thread, that called this function in the [0; size) range.
- *int* **size** - Number of threads for execution. The function is called **size** times each frame and executed in parallel threads. Each time the function is called with an index in the range [0; size), i.e.: 0, 1, ..., size-1.

## virtual void UpdateAsyncThread ( int id , int size )

 Engine calls this function before the execution of all [*updateSyncThread()*](#updateSyncThread_int_int_void) functions. Like the *updateSyncThread()* it is called **size** times each frame and executed in parallel with user's [*postUpdate()*](#postUpdate_int) and [*updatePhysics()*](#updatePhysics_int) functions, but **does not block the Main Thread** until the Engine reaches the *doSwap()* stage (similar to the [*updatePhysics()*](#updatePhysics_int) function).
 This function is the smoothest and does not cause spikes, it has a lot of time for execution. But it also has a lot of limitations.
 It is suitable for certain heavy resource-consuming calculations calculations that should be performed each frame, such as pathfinding, generation of procedural textures, and so on.
### Arguments

- *int* **id** - Index of the current thread, that called this function in the [0; size) range.
- *int* **size** - Number of threads for execution. The function is called **size** times each frame and executed in parallel threads. Each time the function is called with an index in the range [0; size), i.e.: 0, 1, ..., size-1.

## virtual bool PostUpdate ( )

Engine calls this function before rendering each render frame. You can correct behavior after the state of the node has been updated. Similar to the world script's [*postUpdate()*](../../../../code/fundamentals/execution_sequence/code_update.md#code_postUpdate) function.
### Return value

Returns true if there were no errors; otherwise, false.
## virtual bool UpdatePhysics ( )

Engine calls this function before updating each physics frame. This function is used to control physics in your application. The engine calls *updatePhysics()* with the fixed rate (60 times per second by default) regardless of the fps number. Similar to the world script's [*updatePhysics()*](../../../../code/fundamentals/execution_sequence/code_update.md#code_updatePhysics) function.
### Return value

Returns true if there were no errors; otherwise, false.
## virtual bool Swap ( )


Engine calls this function after the following processes are completed: rendering (CPU portion), physics calculations and pathfinding, GUI rendering, and all Async threads. The function is designed to operate with the results of the *UpdateAsyncThread()* method � all other methods (threads) have already been performed and are ilde. After this function, only two actions occur:


- All objects that are queued for deletion are deleted.
- Profiler is rendered.


This function is similar to the world script's [*Swap()*](../../../../code/fundamentals/execution_sequence/code_update.md#code_update) function.

### Return value

Returns true if there were no errors; otherwise, false.
