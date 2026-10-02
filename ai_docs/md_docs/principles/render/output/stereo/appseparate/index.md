# Separate Images Output with Separate Plugin

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


The *Separate* plugin is used to create a separate window for each eye. It can be used with any devices that support separate images output, e.g. for 3D video glasses or helmets (HMD)


The windows are borderless and are placed on the first and the second display respectively. If a single display is available, both windows are placed on it.


> **Notice:** - The *Separate* plugin can be used under Windows only.
> - This plugin cannot be used in a Qt-based application.


[![](separate_images_sm.png)](separate_images.png)


## Launching Separate


To use the plugin, specify the `extern_plugin` command line option on the start-up:


```bash
main_x64d -extern_plugin "UnigineSeparate"
```


Also you can create a new project with the Separate plugin support by checking the *Dual output stereo 3D* option on the *[New Project](../../../../../sdk/projects/index_cpp.md#creation)* tab of the UNIGINE SDK Browser.


The engine automatically loads the appropriate version of the library depending on the specified main application. So you can use 64-bit debug or release version of the library.


> **Notice:** The Separate plugin cannot be used with:
> - Multi-monitor plugins (*[SpiderVision](../../../../../principles/render/output/multi_monitor/spidervision_plugin/index.md)*)
> - [Panoramic rendering](../../../../../principles/render/output/apppanorama/index.md)
> - The other stereo 3D plugins


## Customizing Separate


A UNIGINE-based application can be used with any custom device that supports an output of separate image pairs.


Implement the input device interface using an extensible [C++ API](../../../../../api/index.md).


Stereo settings that control the eye separation distance and the distance to the zero parallax plane are [set globally](../../../../../principles/render/output/stereo/index.md#customizing): the plugin applies the current values to its viewport each frame.
