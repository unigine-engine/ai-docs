# ARTTracker Plugin

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


The **ARTTracker** plugin provides integration with ARTTRACK systems (optical motion capture hardware) from ART.


*ARTTracker* guarantees a high reliability especially in big tracking volumes. It is the best solution for interaction with the *ART Fingertracking* and *Motion Capture* applications.


The plugin can receive the following types of data:


- Single marker data
- Standard body data
- Inertial body data
- *A.R.T.* flystick data
- Measurement tool data
- *A.R.T.* fingertracking hand data
- *A.R.T.* human joint model data


When the plugin is loaded, the *engine.dtrack* class with a bunch of functions is added to UnigineScript.


> **Notice:** For more details see the *ARTTracker* [plugin sample](#using) and visit the [official website](https://ar-tracking.com).


![](index.png)


### See Also


- The sample `<UnigineSDK>/data/samples/plugins/arttracker`


## Using the Plugin


To **add the plugin to a new project**, start by [creating a project](../../../sdk/projects/index_cpp.md#creation) from a template. In the project creation dialog, open *Advanced Settings > Plugins*, enable the *ARTTracker* plugin, click *Add*, then select *Create New Project*.


![](add_plugin.png)


For **existing projects**, in the SDK Browser, open the *My Projects* tab, and click the three-dot menu on the project card. Select *Configure*, then click *Plugins*, enable the required plugin, click *Add*, and finish with *Configure Project*.


![](../../../sdk/projects/other_actions.png)


To open the world containing a sample do the following:


- Specify the `extern_plugin` command line option on the application start-up: ```bash main_x64 -extern_plugin "UnigineARTTracker" ```
- Click *File -> Open World* (**Ctrl + O**) or open the [Asset Browser](../../../editor2/assets_workflow/index.md#asset_browser) window, go to the `samples/plugins` folder and choose the `arttracker.world` file.


## System Requirements


- *DTrack2* software should be installed in your network or PC.
