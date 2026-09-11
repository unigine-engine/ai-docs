# Unigine::Plugins::GPUMonitor Class (CS)


## GPUMonitor Class

### Properties

## 🔒︎ int NumAdapters

The number of adapters on the system.
## 🔒︎ string Name

The name of the currently used GPU.
### Members

---

## string GetAdapterName ( int num )

Returns the display adapter name based on its ordinal number.
### Arguments

- *int* **num** - Ordinal number that denotes the display adapter. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumAdapters()](#getNumAdapters_int)*.

### Return value

Display adapter name
## float GetCoreClock ( int num )

Returns core clock of the selected adapter.
### Arguments

- *int* **num** - Ordinal number that denotes the display adapter. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumAdapters()](#getNumAdapters_int)*.

### Return value

Core clock, i.e. frequency, at which the GPU is running.
## float GetMemoryClock ( int num )

Returns memory clock of the selected adapter.
### Arguments

- *int* **num** - Ordinal number that denotes the display adapter. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumAdapters()](#getNumAdapters_int)*.

### Return value

Memory clock, i.e. how fast the GPU memory is running
## float GetShaderClock ( int num )

Returns shader clock of the selected adapter.
### Arguments

- *int* **num** - Ordinal number that denotes the display adapter. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumAdapters()](#getNumAdapters_int)*.

### Return value

Shader clock, i.e. frequency, at which shader processing units operate
## float GetTemperature ( int num )

Returns the GPU temperature of the selected adapter.
### Arguments

- *int* **num** - Ordinal number that denotes the display adapter. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumAdapters()](#getNumAdapters_int)*.

### Return value

GPU temperature
## float GetUtilization ( int num )

Returns the rate of GPU utilization, in percent, of the selected adapter.
### Arguments

- *int* **num** - Ordinal number that denotes the display adapter. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumAdapters()](#getNumAdapters_int)*.

### Return value

GPU utilization rate, in percent
## float GetMaxTemperature ( )

Returns maximum GPU temperature.
### Return value

Maximum GPU temperature
