# Steam Plugin


The *Steam* plugin relies on methods provided by the *[Steam](../../../api/library/plugins/steam/class.steam_cpp.md)* class to interact with the *[Steamworks API](https://partner.steamgames.com/doc/api)*, enabling features such as user authentication, leaderboard management, friend lists, and in-game overlay functionality.


> **Notice:** To function properly, the plugin requires that the *Steam* client is running and a `steam_appid.txt` file containing the application's *App ID* is placed in the `bin/` directory of your project.


The following sample demonstrate how to integrate *Steam* services into your application:


- `<UnigineSDK>/data/samples/plugins/steam_00`


To run the plugin samples from the UNIGINE SDK Browser, go to *Samples -> UnigineScript -> Plugins* and run the corresponding sample.


## Launching Steam


To use the plugin, specify the `extern_plugin` command line option on the application start-up:


```bash
main_x64d -extern_plugin UnigineSteam
```
