# Unigine::Plugin Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Unigine *Plugin* class allows loading a custom library dynamically at Unigine runtime.


## Plugin Class

### Members

---

## virtual void gui ( )

Engine calls this function before GUI each render frame for the specified engine window viewport.
### Arguments

## virtual void render ( )

Engine calls this function before rendering each render frame for the specified Engine window viewport.
### Arguments
