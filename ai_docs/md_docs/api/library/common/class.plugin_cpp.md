# Unigine::Plugin Class (CPP)

**Header:** #include <UniginePlugin.h>


Unigine *Plugin* class allows loading a custom library dynamically at Unigine runtime.


## Plugin Class

### Members

---

## virtual void * get_data ( )

Returns the plugin data.
### Return value

Plugin data.
## virtual const char * get_name ( )

Returns the name of the plugin.
### Return value

Plugin name.
## int get_order ( )


Returns the execution order of the plugin. Each plugin has its execution order, which determines the sequence in which plugin�s functions (*[update](#update_void) / [postUpdate](#postUpdate_void) / [render](#render_const_EngineWindowViewportPtr_ref_void) / [shutdown](#shutdown_int)*) will be executed. The only exception is the [*init*](#init_int) function as it is called just after loading the plugin.


> **Notice:** Remember, when [writing your own plugin](../../../code/cpp/plugin.md), that requires interaction with other ones, specifying correct order value is required to avoid issues and ensure proper execution sequence. If in your case the order doesn't matter, set the default 0 value.


### Return value

Plugin execution order.
## virtual int getCompilationFlags ( ) const

Returns the UNIGINE compilation flags.
### Return value

UNIGINE compilation flags.
## virtual void updatePhysics ( )

Engine calls this function before updating each physics frame.
## virtual void gui ( EngineWindowViewportPtr& window )

Engine calls this function before GUI each render frame for the specified engine window viewport.
### Arguments

- *EngineWindowViewportPtr&* **window** - Target Engine window viewport.

## virtual int init ( )

Engine calls this function on plugin initialization.
### Return value

true on success, or false if an error has occurred.
## virtual bool loadWorld ( const Xml Ptr & xml )

Engine calls this function on world loading.
### Arguments

- *const [Xml](../../../api/library/common/class.xml_cpp.md)Ptr &* **xml** - Xml instance from which the data is to be loaded.

### Return value

true on success; otherwise, false.
## virtual void render ( const EngineWindowViewportPtr& window )

Engine calls this function before rendering each render frame for the specified Engine window viewport.
### Arguments

- *const EngineWindowViewportPtr&* **window** - Target Engine window viewport.

## virtual int saveWorld ( const Xml Ptr & xml )

Engine calls this function on world saving.
### Arguments

- *const [Xml](../../../api/library/common/class.xml_cpp.md)Ptr &* **xml** - Xml instance to which the data is to be saved.

### Return value

true on success, or false if an error has occurred.
## virtual int shutdown ( )

Engine calls this function on plugin shutdown.
### Return value

true on success, or false if an error has occurred.
## virtual void swap ( )

Engine calls this function before swapping each render frame.
## virtual void update ( )

Engine calls this function before updating each render frame.
## void postUpdate ( )

Engine calls this function after updating each render frame.
