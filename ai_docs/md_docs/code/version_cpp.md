# Engine Version (CPP)


Information about the current version of Engine, Editor and core might be useful in many cases (e.g., writing own Engine and Editor plugins, checking compatibility in your custom tools, etc.). Version is represented as a four-component number - **A . B . C . D** , where:


- **A** - major version number (backward-incompatible conceptual changes, new implementation of majority of subsystems).
- **B** - minor version number (new UI, lots of new features, etc. keeping backward compatibility).
- **C** - patch version number (stabilization/bugfix release).
- **D** - additional revision number.


At runtime you can always get this information via API using the corresponding member of the *Engine* class: *[Engine::getVersion()](../api/library/engine/class.engine_cpp.md#getVersion_const_char_ptr)*


```cpp
Log::message("Current Engine version is: %s", Engine::getVersion());
```


In case you need version information when compiling your application or any other purpose **without having the Engine running**, you can:


- take it from the `data/core/version` file as a string (e.g., **"2.16.0.2"**)


- or, if you're using C++, include the `UnigineVersion.h` header and use the following constants:


| Name | Description |
|---|---|
| **UNIGINE_VERSION_MAJOR** | Major version of the Engine (backward-incompatible conceptual changes, new implementation of majority of subsystems). It is the first component of the version number: ***MAJOR**.MINOR.PATCH.REVISION*. |
| **UNIGINE_VERSION_MINOR** | Minor version of the Engine (new UI, lots of new features, etc. keeping backward compatibility). It is the second component of the version number: *MAJOR.**MINOR**.PATCH.REVISION*. |
| **UNIGINE_VERSION_PATCH** | Patch version of the Engine (stabilization/bugfix release). It is the third component of the version number: *MAJOR.MINOR.**PATCH**.REVISION*. |
| **UNIGINE_VERSION_REVISION** | Revision number (the fourth component of the version number): *MAJOR.MINOR.PATCH.**REVISION***. |
| **UNIGINE_VERSION** | Full version of the Engine (as well as core and UnigineEditor): ***MAJOR.MINOR.PATCH.REVISION*** (e.g., **"2.16.0.2"**) |
