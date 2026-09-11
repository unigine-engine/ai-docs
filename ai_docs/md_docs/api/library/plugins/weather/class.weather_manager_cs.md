# Unigine::Plugins::Weather::Manager Class (CS)


This class represents the Weather Manager interface.

> **Notice:** Weather plugin must be loaded.


## Weather::Manager Class

### Properties

## bool Enabled

The value indicating if the Weather Manager is enabled.
## bool Debug

The value indicating if Debug mode is enabled for the Weather Manager. This mode allows you to inspect the application at runtime.
## 🔒︎ float IFps

The inverse FPS value (the time in seconds it took to complete the last frame). This method is similar to the [*Game::getIFps()*](../../../../api/library/engine/class.game_cs.md#getIFps_float) but it is more preferred for multi-channel systems as it implements more accurate frame time calculation (including spike-periods).
## Player Player

The player instance used by the WeatherManager.
## 🔒︎ Config Config

The weather configuration interface.
## 🔒︎ SkyMap SkyMap

The sky map interface.
## 🔒︎ Meteo Meteo

The meteo interface.
## 🔒︎ Water Water

The water control interface.
## 🔒︎ Planet Planet

The interface of the round-planet subsystem of the Weather plugin, providing read access to the round-planet state configured in the weather configuration file (see the *[Planet](../../../../api/library/plugins/weather/class.planet_cs.md)* class).
### Members

---

## void SaveState ( Stream blob )

Saves the state of the Weather Manager into a binary stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **blob** - The stream to save the weather data.

## void RestoreState ( Stream blob )

Restores the state of the Weather Manager from the binary stream.
### Arguments

- *[Stream](../../../../api/library/common/class.stream_cs.md)* **blob** - The stream that stores the weather data.
