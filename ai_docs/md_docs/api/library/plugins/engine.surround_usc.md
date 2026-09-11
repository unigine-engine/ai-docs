# engine.surround Functions (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This set of functions is available when the [Surround](../../../principles/render/output/multi_monitor/appsurround/index.md) plugin is loaded.


> **Notice:** This plugin cannot be used in a Qt-based application


If the plugin are loaded together with the engine, the following definition is set:


- `HAS_SURROUND` for the Surround plugin


This definition can be used, for example, to avoid errors if the plugin is not loaded: the code in which the plugin functions are executed can be wrapped around as follows:


```cpp
#ifdef HAS_SURROUND
	// engine.surround functions
#endif


```


### See also


UnigineScript API sample:


## engine.surround Class

### Members

---

## Gui engine.surround. getGui ( int num )

Returns a GUI instance to draw interface on the specified monitor.
### Arguments

- *int* **num** - Monitor number.

### Return value

GUI instance.
## void engine.surround. getModelview ( int num )

Gets the current modelview matrix used for the specified monitor.
### Arguments

- *int* **num** - Monitor number from 0 (the left monitor) to 2 (the right monitor).

## void engine.surround. getProjection ( int num )

Gets the current projection matrix used for the specified monitor.
### Arguments

- *int* **num** - Monitor number from 0 (the left monitor) to 2 (the right monitor).

## int engine.surround. isEnabled ( int num )

Returns a value indicating if the specified monitor is enabled for viewport rendering.
### Arguments

- *int* **num** - Monitor number from 0 (the left monitor) to 2 (the right monitor).

### Return value

Returns 1 if the monitor is enabled for rendering; otherwise, 0.
## void engine.surround. setEnabled ( int num , int enable )

Enables the specified monitor for viewport rendering.
### Arguments

- *int* **num** - Monitor number from 0 (the left monitor) to 2 (the right monitor).
- *int* **enable** - 1 to enable the monitor for rendering; 0 to disable it.

## void engine.surround. setMaterials ( int num , string materials )

Sets postprocess materials to be applied to the specified monitor.
### Arguments

- *int* **num** - Monitor number from 0 (the left monitor) to 2 (the right monitor).
- *string* **materials** - Postprocess materials (comma-separated list).

## void engine.surround. setModelview ( int num , mat4 modelview )

Sets the modelview matrix for the specified monitor.
### Arguments

- *int* **num** - Monitor number from 0 (the left monitor) to 2 (the right monitor).
- *mat4* **modelview** - Modelview matrix.

## void engine.surround. setProjection ( int num , mat4 projection )

Sets the projection matrix for the specified monitor.
### Arguments

- *int* **num** - Monitor number from 0 (the left monitor) to 2 (the right monitor).
- *mat4* **projection** - Projection matrix.

## void engine.surround. setReflectionMask ( int num , int mask )

Sets a bit mask for rendering reflections on the specified monitor. Reflections are rendered in the viewport if masks of reflective materials match this one (one matching bit is enough).
### Arguments

- *int* **num** - Monitor number from 0 (the left monitor) to 2 (the right monitor).
- *int* **mask** - Integer, each bit of which is a mask.

## void engine.surround. setViewportMask ( int num , int mask )

Sets a viewport bit mask for the specified monitor. Object surfaces, materials, decals, lights and GUI objects will be rendered into this viewport only if their viewport mask matches this one (one matching bit is enough).
### Arguments

- *int* **num** - Monitor number from 0 (the left monitor) to 2 (the right monitor).
- *int* **mask** - Integer, each bit of which is a mask.
