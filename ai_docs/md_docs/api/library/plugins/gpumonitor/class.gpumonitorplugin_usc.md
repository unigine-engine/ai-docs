# Unigine::Plugins::GPUMonitorPlugin Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


## GPUMonitorPlugin Class

### Members

## int getNumMonitors () const

Returns the current number of monitors.
### Return value

Current number of monitors.
---

## int engine.gpumonitor. getUpdateRate ( int num )

Returns the number of updates per second for the selected monitor.
### Arguments

- *int* **num** - Ordinal number that denotes the monitor. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumMonitors()](#getNumMonitors_int)*.

### Return value

Number of updates per second for the selected monitor.
## void engine.gpumonitor. setUpdateRate ( int rate )

Sets the number of updates per second.
### Arguments

- *int* **rate** - Number of updates per second

## GPUMonitor engine.gpumonitor. getMonitor ( int num )

Returns the interface of the selected GPUMonitor.
### Arguments

- *int* **num** - Ordinal number that denotes the monitor. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumMonitors()](#getNumMonitors_int)*.

### Return value

Interface of the selected GPUMonitor
