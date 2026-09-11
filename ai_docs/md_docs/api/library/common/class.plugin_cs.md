# Unigine::Plugin Class (CS)


Unigine *Plugin* class allows loading a custom library dynamically at Unigine runtime.


## Plugin Class

### Members

---

## virtual IntPtr GetData ( )

Returns the plugin data.
### Return value

Plugin data.
## virtual string GetName ( )

Returns the name of the plugin.
### Return value

Plugin name.
## int GetOrder ( )


Returns the execution order of the plugin. Each plugin has its execution order, which determines the sequence in which plugin�s functions (*[update](#update_void) / [postUpdate](#postUpdate_void) / [render](#render_const_EngineWindowViewportPtr_ref_void) / [shutdown](#shutdown_int)*) will be executed. The only exception is the [*init*](#init_int) function as it is called just after loading the plugin.


> **Notice:** Remember, when [writing your own plugin](../../../code/cpp/plugin.md), that requires interaction with other ones, specifying correct order value is required to avoid issues and ensure proper execution sequence. If in your case the order doesn't matter, set the default 0 value.


### Return value

Plugin execution order.
## virtual void UpdatePhysics ( )

Engine calls this function before updating each physics frame.
## virtual void Gui ( EngineWindowViewport window )

Engine calls this function before GUI each render frame for the specified engine window viewport.
### Arguments

- *[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cs.md)* **window** - Target Engine window viewport.

## virtual bool Init ( )

Engine calls this function on plugin initialization.
### Return value

true on success, or false if an error has occurred.
## virtual bool LoadWorld ( Xml xml )

Engine calls this function on world loading.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Xml instance from which the data is to be loaded.

### Return value

true on success; otherwise, false.
## virtual void Render ( EngineWindowViewport window )

Engine calls this function before rendering each render frame for the specified Engine window viewport.
### Arguments

- *[EngineWindowViewport](../../../api/library/gui/class.enginewindowviewport_cs.md)* **window** - Target Engine window viewport.

## virtual bool SaveWorld ( Xml xml )

Engine calls this function on world saving.
### Arguments

- *[Xml](../../../api/library/common/class.xml_cs.md)* **xml** - Xml instance to which the data is to be saved.

### Return value

true on success, or false if an error has occurred.
## virtual bool Shutdown ( )

Engine calls this function on plugin shutdown.
### Return value

true on success, or false if an error has occurred.
## virtual void Swap ( )

Engine calls this function before swapping each render frame.
## virtual void Update ( )

Engine calls this function before updating each render frame.
