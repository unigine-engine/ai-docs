# Steam Plugin


The *Steam* plugin relies on methods provided by the *[Steam](../../../api/library/plugins/steam/class.steam_cpp.md)* class to interact with the *[Steamworks API](https://partner.steamgames.com/doc/api)*, enabling features such as user authentication, leaderboard management, friend lists, and in-game overlay functionality.


> **Notice:** To function properly, the plugin requires that the *Steam* client is running and a `steam_appid.txt` file containing the application's *App ID* is placed in the `bin/` directory of your project.


The following sample demonstrate how to integrate *Steam* services into your application:


- `<UnigineSDK>/data/samples/plugins/steam_00`


To run the plugin samples from the UNIGINE SDK Browser, go to *Samples -> UnigineScript -> Plugins* and run the corresponding sample.


## Launching Steam


To **add the plugin to a new project**, start by [creating a project](../../../sdk/projects/index_cpp.md#creation) from a template. In the project creation dialog, open *Advanced Settings > Plugins*, enable the *Steam* plugin, click *Add*, then select *Create New Project*.


![](add_plugin.png)


For **existing projects**, in the SDK Browser, open the *My Projects* tab, and click the three-dot menu on the project card. Select *Configure*, then click *Plugins*, enable the required plugin, click *Add*, and finish with *Configure Project*.


![](../../../sdk/projects/other_actions.png)


To use the plugin, specify the `extern_plugin` command line option on the application start-up:


```bash
main_x64d -extern_plugin UnigineSteam
```
