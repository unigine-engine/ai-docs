# Unigine::CPUTask Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


**CPUTask** is a single-threaded task that can be dispatched to any of the Engine's thread pools. Unlike **[CPUShader](../../../../api/library/common/mt/class.cpushader_usc.md)**, which distributes work across multiple threads, a CPUTask runs its *process()* method once on a single worker thread within the chosen pool.


Inherit from this class and override the pure virtual *process()* method to define your task logic, then call one of the *run*Thread()* methods to submit it to a specific pool.


## CPUTask Class

### Members

---

## CPUTask ( )

Default constructor.
