# Engine Version (CS)


Information about the current version of Engine, Editor and core might be useful in many cases (e.g., writing own Engine and Editor plugins, checking compatibility in your custom tools, etc.). Version is represented as a four-component number - **A . B . C . D** , where:


- **A** - major version number (backward-incompatible conceptual changes, new implementation of majority of subsystems).
- **B** - minor version number (new UI, lots of new features, etc. keeping backward compatibility).
- **C** - patch version number (stabilization/bugfix release).
- **D** - additional revision number.


At runtime you can always get this information via API using the corresponding member of the *Engine* class: *[Engine.Version](../api/library/engine/class.engine_cs.md#getVersion_const_char_ptr)*


```csharp
Log.Message("Current Engine version is: {0}",Engine.Version);
```


In case you need version information when compiling your application or any other purpose **without having the Engine running**, you can:


- take it from the `data/core/version` file as a string (e.g., **"2.16.0.2"**)
