# Unigine::Plugins::GPUMonitorPlugin Class (CS)

> **Notice:** This class is a singleton.


## GPUMonitorPlugin Class

### Properties

## 🔒︎ int NumMonitors

The number of monitors.
### Members

---

## int GetUpdateRate ( int num )

Returns the number of updates per second for the selected monitor.
### Arguments

- *int* **num** - Ordinal number that denotes the monitor. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumMonitors()](#getNumMonitors_int)*.

### Return value

Number of updates per second for the selected monitor.
## void SetUpdateRate ( int rate )

Sets the number of updates per second.
### Arguments

- *int* **rate** - Number of updates per second

## GPUMonitor GetMonitor ( int num )

Returns the interface of the selected GPUMonitor.
### Arguments

- *int* **num** - Ordinal number that denotes the monitor. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumMonitors()](#getNumMonitors_int)*.

### Return value

Interface of the selected GPUMonitor
