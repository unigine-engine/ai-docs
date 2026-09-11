# Unigine::EnginePlugins Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


## EnginePlugins Class

---

## int getNumPlugins ( )

Returns the number of loaded plugins.
### Return value

Number of loaded plugins.
## string getPluginName ( int num )

Returns the name of the loaded plugin by its index.
### Arguments

- *int* **num** - Index of the loaded plugin.

### Return value

Loaded plugin name.
## int addPlugin ( string name )

Adds a plugin in engine runtime by using a name of this plugin.
### Arguments

- *string* **name** - Plugin name.

### Return value

**1** if the plugin was successfully added, otherwise, **0**.
