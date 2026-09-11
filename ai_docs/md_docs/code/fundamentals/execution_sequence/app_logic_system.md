# Application Logic System


Based on the API selected when [creating a project](../../../sdk/projects/index_cpp.md#application_settings), you can implement your application logic either in **C++** or **C#**. These are the primary and recommended languages for developing applications in UNIGINE.


In addition, you can combine **C++/C#** with **UnigineScript** by implementing certain parts of logic in `*.usc` scripts.


If both C++/C# and UnigineScript methods are implemented the execution order is the following:


- UnigineScript method
- C++/C# method


> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.
>
>
> While you can technically build a project entirely with UnigineScript, **this approach is not recommended**. Use C++ or C# for general application logic.


## Application Logic Structure


Application logic in UNIGINE is defined through a set of lifecycle methods provided by the Engine. These methods are grouped by different logic types and are called at specific stages of the execution sequence.


By implementing them, you define how your application behaves during world loading, system startup, Editor events, and so on.


Application logic in UNIGINE is defined in several contexts, each with its own lifecycle and purpose:


- **[World Logic](#worldlogic)** is executed only when a world is loaded. **[Component System](../../../principles/component_system/index.md)** - modular building blocks for application logic. Component System is available only for **C++** and **C#** projects. It enables you to implement your application's logic via a set of building blocks - **components**, and assign these blocks to nodes, giving them additional functionality. By combining these small and simple blocks you can create a very sophisticated logic system. > **Notice:** The [Component System](../../../principles/component_system/index.md) is also based on WorldLogic class (it inherits from it). As a result, all components provide the same lifecycle methods, as WorldLogic (such as *init(), update(), updatePhysics()*, etc.).

  - **C++/C#** World logic is implemented by inheriting from the *[WorldLogic](../../../api/library/common/logic/class.worldlogic_cpp.md)* class. By default, the Engine generates `AppWorldLogic.cpp` or `AppWorldLogic.cs` in the *source/* directory of your project. Unlike UnigineScript, world logic in C++/C# remains loaded throughout the entire engine runtime and applies to all worlds, so it cannot be assigned to a specific world.
  - **UnigineScript** World logic is implemented in world script file (`*.usc`). Each world can have its own script, and a default one is automatically created when you create a new UnigineScript project - it is named after the project and stored in the `data/` folder.
- **[System Logic](#systemlogic)** exists during the whole application life cycle, regardless of the loaded world. It is active when no world is loaded, during transitions between worlds, and while a world is running. Use system logic for tasks that must persist independently of any particular world (e.g. global application state or GUI) > **Notice:** The `unigine.usc` script containing system logic template is created by default for all project types. You can verify this by checking the console output when starting the Editor or the Engine: > > > ```text > 						---- Interpreter ---- > Version: 2.90 > > Unigine~# config_autosave 1 && world_load "UnigineProject" > Script loading "core/unigine.usc" 11ms									<- System Script is loaded > World loading "UnigineProject.world" (Time: 31.6ms, Memory: 0B) > > ``` > > > UnigineScript system logic (`unigine.usc`) is mainly intended for internal engine functionality. While it can still be used, relying on it in C++/C# development is not advised.

  - **C++/C#** System logic is implemented by inheriting from the *[SystemLogic](../../../api/library/common/logic/class.systemlogic_cpp.md)* class. By default a source file (`AppSystemLogic.cpp` or `AppSystemLogic.cs`) is generated in the *source/* directory of your project.
  - **UnigineScript** System logic is implemented in the default system script `unigine.usc`, which is stored in the data/ folder inside the core.ung archive. You can place your custom logic directly in this file.
- **[Editor logic](#editorlogic)** This logic type is to be used in case you need to implement your own Editor. It has more implemented methods providing you with clear understanding of the current Engine events (a node has been created, a property has been deleted, a material has been changed, etc.). <details> <summary>Show | Close</summary> *editor.usc* ```text #include <editor2/editor_tracker.h> #include <editor2/editor_video_grabber.h> int init() { return 1; } int update() { return 1; } int shutdown() { return 1; } ``` </details>

  - **C++/C#** Editor logic is defined by inheriting from the *[EditorLogic](../../../api/library/common/logic/class.editorlogic_cpp.md)* class.
  - **UnigineScript** Default UnigineScript logic for the Editor is loaded from the `editor2/editor.usc` file stored inside `editor2.ung`. You can override this UnigineScript logic file by creating a folder named `editor2` in your `data` folder and putting there the `editor.usc` file with the following code (you can modify this script, but do not remove existing *include* lines as they are required for Editor operation):


> **Notice:** When you create a new C++ / C# project, it has already inherited World Logic class (*AppWorldLogic*) and System Logic class (*AppSystemLogic*) with implemented methods to put your logic code inside.
>
>
> However, you can also implement your own logic by inheriting from base classes and registering it at Engine runtime.


## World Logic


The world logic works slightly differently depending on the implementation:


- If the *World Logic* is implemented in C++ or C#, it stays loaded as long as any world is loaded.
- If implemented in UnigineScript, it is loaded and unloaded together with the world itself.
- In case of the Component System the lifetime is defined by each component individually.


The *World Logic* may use the following methods, which are available for both C++/C# and UnigineScript:


<details>
<summary>AppWorldLogic methods (C++ example) | Close</summary>

```cpp
#include "AppWorldLogic.h"

AppWorldLogic::AppWorldLogic() {

}

AppWorldLogic::~AppWorldLogic() {

}

int AppWorldLogic::init() {

	return 1;
}

int AppWorldLogic::update() {

	return 1;
}

int AppWorldLogic::postUpdate() {

	return 1;
}

int AppWorldLogic::updatePhysics() {

	return 1;
}

int AppWorldLogic::shutdown() {

	return 1;
}

int AppWorldLogic::save(const Unigine::StreamPtr &stream) {
	UNIGINE_UNUSED(stream);
	return 1;
}

int AppWorldLogic::restore(const Unigine::StreamPtr &stream) {
	UNIGINE_UNUSED(stream);
	return 1;
}

```

</details>


### init() method


Engine calls this method on the world initialization. The code inside should initialize resources for your world scene during the world start.


### updateAsyncThread() method


In the *updateAsyncThread()* method, you can specify all logic method you want to be called every frame independently of the rendering thread. This method does not block the Main Thread. However, the frame is synchronized at the boundary: the engine waits for updateAsyncThread() to finish before starting the next frame (the wait happens during swap()), so overrunning your frame budget here will still delay the next frame.


> **Notice:** This method does not have protection locks, so it is not recommended to modify other components inside this method, unless you are absolutely sure, that these components won't be modified or removed elsewhere.


### updateSyncThread() method


In the *updateSyncThread()* method, you can specify any parallel logic functions to be executed before the *Update()*. This method **blocks the Main Thread** until all calls are completed.


> **Notice:** This method should be used to call only the API methods related to the current node: the node itself, its materials and properties.


### update() method


In the *update()* method, you can specify all logic-related functions you want to be called every frame while your application is executed. Engine calls this method before updating each render frame.


### postUpdate() method


This is an additional method used to correct behavior after the state of the node has been updated. Engine calls this method before rendering each render frame.


### updatePhysics() method


This method is used to control physics in your application. Engine calls this method before updating each physics frame.


### swap() method


This method is designed to operate with the results of the *updateAsyncThread()* method � all other methods (threads) have already been performed and are idle.


### shutdown() method


The method is called when the world is unloaded (or a component is deleted) and is used to release any resources allocated that were created during world or component execution to avoid memory leaks.


> **Notice:** The basic recommended workflow is to have a single *AppWorldLogic* class to process all worlds in your project. However, you can [split world-specific code between separate classes](../../../code/usage/multiple_worldlogic/index_cpp.md) inherited from *[WorldLogic](../../../api/library/common/logic/class.worldlogic_cpp.md)*.


## System Logic


The System Logic stays loaded during the whole UNIGINE Engine runtime. It may use the following methods, which are available for both C++/C# and UnigineScript:


<details>
<summary>AppSystemLogic methods (C++ example) | Close</summary>

```cpp
#include "AppSystemLogic.h"

AppSystemLogic::AppSystemLogic() {

}

AppSystemLogic::~AppSystemLogic() {

}

int AppSystemLogic::init() {
	return 1;
}

int AppSystemLogic::update() {
	return 1;
}

int AppSystemLogic::postUpdate() {
	return 1;
}

int AppSystemLogic::shutdown() {
	return 1;
}


```

</details>


### init() method


Engine calls this method on initialization. Here you should put the code that you want to be executed during the system script initialization.


### update() method


Engine calls this method before updating each render frame. Here you should put the code that you want to be updated each frame. The logic should be related to the engine job. These are the examples of operations that are performed by a default system script:


- The system script handles the mouse. It controls whether the mouse is grabbed when clicked (by default), the mouse cursor disappears when not moved for some time, or not handled by the system.
- Main menu logic is updated.
- Other system-related user input is handled.


### postUpdate() method


Engine calls this method before rendering each render frame. It can access the updated data on node states and correct the behavior accordingly in the same frame.


### shutdown() method


Engine calls this method on application shutdown. You should release all the resources that you created for system script.


## Editor Logic


This component is to be used in case you need to implement your own Editor. It has more implemented methods providing you with clear understanding of the current Engine events (a node has been created, a property has been deleted, a material has been changed, etc.).


The *Editor Logic* may use the following methods, which are available for both C++/C# and UnigineScript:


<details>
<summary>AppEditorLogic methods (C++ example) | Close</summary>

```cpp
#include "AppEditorLogic.h"

AppEditorLogic::AppEditorLogic() {

}

AppEditorLogic::~AppEditorLogic() {

}

int AppEditorLogic::init() {
	return 1;
}

int AppEditorLogic::update() {
	return 1;
}

int AppEditorLogic::postUpdate() {
	return 1;
}

int AppEditorLogic::shutdown() {
	return 1;
}

int AppEditorLogic::worldInit() {
	return 1;
}

int AppEditorLogic::worldShutdown() {
	return 1;
}

int AppEditorLogic::worldSave() {
	return 1;
}

```

</details>


### init() method


The engine calls this method on the world initialization. It initializes all belongings of UnigineEditor.


### update() method


If the editor is loaded, the engine calls this method before updating each render frame. Here you can put some editor-related logic that should be updated each frame.


### postUpdate() method


If the editor is loaded, the engine calls this method before rendering each render frame.


### shutdown() method


The engine calls this method on editor shutdown. Engine applications may continue running.


### render() method


Engine calls this method before rendering each render frame for the specified Engine window, when editor is loaded. Here, for example, you can perform any custom rendering for your editor tools.


### worldInit() method


If the editor is loaded, the Engine calls this method on the world initialization. Use this method, if you want to initialize something before the World Logic starts its *[init()](#worldlogic_init)* function.


### worldShutdown() method


If the editor is loaded, the engine calls this method on the world shutdown.


### worldSave() method


If the editor is loaded, the Engine calls this method on saving the world.
