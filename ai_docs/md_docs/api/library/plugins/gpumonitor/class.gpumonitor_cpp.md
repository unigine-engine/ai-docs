# Unigine::Plugins::GPUMonitor Class (CPP)

**Header:** #include <plugins/Unigine/GPUMonitor/UnigineGPUMonitor.h>


## GPUMonitor Class

### Members

## int getNumAdapters () const

Returns the current number of adapters on the system.
### Return value

Current number of adapters on the system.
## const char * getName () const

Returns the current name of the currently used GPU.
### Return value

Current name of the currently used GPU.
---

## const char * getAdapterName ( int num ) const

Returns the display adapter name based on its ordinal number.
### Arguments

- *int* **num** - Ordinal number that denotes the display adapter. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumAdapters()](#getNumAdapters_int)*.

### Return value

Display adapter name
## float getCoreClock ( int num ) const

Returns core clock of the selected adapter.
### Arguments

- *int* **num** - Ordinal number that denotes the display adapter. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumAdapters()](#getNumAdapters_int)*.

### Return value

Core clock, i.e. frequency, at which the GPU is running.
## float getMemoryClock ( int num ) const

Returns memory clock of the selected adapter.
### Arguments

- *int* **num** - Ordinal number that denotes the display adapter. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumAdapters()](#getNumAdapters_int)*.

### Return value

Memory clock, i.e. how fast the GPU memory is running
## float getShaderClock ( int num ) const

Returns shader clock of the selected adapter.
### Arguments

- *int* **num** - Ordinal number that denotes the display adapter. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumAdapters()](#getNumAdapters_int)*.

### Return value

Shader clock, i.e. frequency, at which shader processing units operate
## float getTemperature ( int num ) const

Returns the GPU temperature of the selected adapter.
### Arguments

- *int* **num** - Ordinal number that denotes the display adapter. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumAdapters()](#getNumAdapters_int)*.

### Return value

GPU temperature
## float getUtilization ( int num ) const

Returns the rate of GPU utilization, in percent, of the selected adapter.
### Arguments

- *int* **num** - Ordinal number that denotes the display adapter. The minimum value for this parameter is 0, and the maximum value for this parameter is one less than the value returned by *[getNumAdapters()](#getNumAdapters_int)*.

### Return value

GPU utilization rate, in percent
## float getMaxTemperature ( )

Returns maximum GPU temperature.
### Return value

Maximum GPU temperature
