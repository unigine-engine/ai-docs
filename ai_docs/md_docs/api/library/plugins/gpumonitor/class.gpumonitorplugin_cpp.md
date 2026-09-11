# Unigine::Plugins::GPUMonitorPlugin Class (CPP)

**Header:** #include <plugins/Unigine/GPUMonitor/UnigineGPUMonitor.h>

> **Notice:** This class is a singleton.


## GPUMonitorPlugin Class

### Members

## int getNumMonitors () const

Returns the current number of monitors.
### Return value

Current number of monitors.
---

## int getUpdateRate ( int num ) const

Returns the number of updates per second for the selected monitor.
### Arguments

- *int* **num** - Ordinal number that denotes the monitor. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumMonitors()](#getNumMonitors_int)*.

### Return value

Number of updates per second for the selected monitor.
## void setUpdateRate ( int rate )

Sets the number of updates per second.
### Arguments

- *int* **rate** - Number of updates per second

## GPUMonitor * getMonitor ( int num ) const

Returns the interface of the selected GPUMonitor.
### Arguments

- *int* **num** - Ordinal number that denotes the monitor. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumMonitors()](#getNumMonitors_int)*.

### Return value

Interface of the selected GPUMonitor
