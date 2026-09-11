# Unigine::Plugins::Weather::Manager Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class represents the Weather Manager interface.

> **Notice:** Weather plugin must be loaded.


## Weather::Manager Class

### Members

## void setEnabled ( bool enabled )

Sets a new value indicating if the Weather Manager is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable the Weather Manager; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if the Weather Manager is enabled.
### Return value

**true** if the Weather Manager is enabled ; otherwise **false**.
## void setDebug ( bool debug )

Sets a new value indicating if Debug mode is enabled for the Weather Manager. This mode allows you to inspect the application at runtime.
### Arguments

- *bool* **debug** - Set **true** to enable Debug mode; **false** - to disable it.

## bool isDebug () const

Returns the current value indicating if Debug mode is enabled for the Weather Manager. This mode allows you to inspect the application at runtime.
### Return value

**true** if Debug mode is enabled ; otherwise **false**.
## float getIFps () const

Returns the current inverse FPS value (the time in seconds it took to complete the last frame). This method is similar to the [*Game::getIFps()*](../../../../api/library/engine/class.game_usc.md#getIFps_float) but it is more preferred for multi-channel systems as it implements more accurate frame time calculation (including spike-periods).
### Return value

Current inverse FPS value (1/FPS) - the time in seconds it took to complete the last frame, in seconds.
## void setPlayer ( )

Sets a new player instance used by the WeatherManager.
### Arguments

- **player** - The player instance used by the WeatherManager.

## getPlayer () const

Returns the current player instance used by the WeatherManager.
### Return value

Current player instance used by the WeatherManager.
## getConfig () const

Returns the current weather configuration interface.
### Return value

Current weather configuration interface.
## getSkyMap () const

Returns the current sky map interface.
### Return value

Current sky map interface.
## getMeteo () const

Returns the current meteo interface.
### Return value

Current meteo interface.
## getWater () const

Returns the current water control interface.
### Return value

Current water control interface.
## Planet getPlanet () const

Returns the current interface of the round-planet subsystem of the Weather plugin, providing read access to the round-planet state configured in the weather configuration file (see the *[Planet](../../../../api/library/plugins/weather/class.planet_usc.md)* class).
### Return value

Current round-planet subsystem interface
---

## void saveState ( )

Saves the state of the Weather Manager into a binary stream.
### Arguments

## void restoreState ( )

Restores the state of the Weather Manager from the binary stream.
### Arguments
