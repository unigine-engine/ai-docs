# GPUMonitor Plugin

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


The **GPUMonitor** plugin allows monitoring the graphics card temperature and per-frame information on the chip frequency (if available).


The information provided by the plugin is displayed in the upper right corner.


![](gpu_monitor.png)

*GPUMonitorinfo*


### See Also


- *[GPUMonitor Plugin](../../../api/library/plugins/gpumonitor/index.md)* classes
- UnigineScript API sample:


To run the plugin sample from the UNIGINE SDK Browser, go to *Samples -> UnigineScript -> Plugin* and run the **gpu_monitor_00** sample.


## GPU Information


The following information is available for GPU:


| Graphics | Core clock, i.e. frequency, at which the GPU is running. |
|---|---|
| Memory | Memory clock, i.e. how fast the GPU memory is running. |
| Processor | Shader clock, i.e. how fast the shaders operate. |
| Temperature | GPU temperature. |


The table below demonstrates which information is shown for different GPUs:


| GPU | Graphics | Memory | Processor | Temperature |
|---|---|---|---|---|
| **NVIDIA** | ![](dialog_ok.png) | ![](dialog_ok.png) | ![](dialog_ok.png) | ![](dialog_ok.png) |
| **AMD** | ![](dialog_ok.png) | ![](dialog_ok.png) | ![](dialog_cancel.png) | ![](dialog_ok.png) |
| **Intel** | *not supported* | *not supported* | *not supported* | *not supported* |


## Launching GPUMonitor


To use the plugin, check the **[GPU Monitor](../../../sdk/projects/index_cpp.md#general_settings)** setting in UNIGINE SDK Browser on project creation and then specify the `extern_plugin` command line option on the start-up:


```bash
main_x64d -extern_plugin "UnigineGPUMonitor"
```


> **Notice:** For an existing project, go to *Other Actions -> Configure Project -> Video Output Options*, check **GPU Monitor** and click **[Update Configuration](../../../sdk/projects/index_cpp.md#update_config)**.


To hide or show the *GPUMonitor* plugin information while running the application, use the `show_gpu` console command: pass 1 to show the information, 0 to hide it.
