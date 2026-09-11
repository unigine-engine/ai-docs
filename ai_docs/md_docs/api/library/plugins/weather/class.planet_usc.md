# Unigine::Plugins::Weather::Planet Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class provides a read-only run-time view of the round-planet subsystem of the *[Weather](../../../../ig/weather/index.md)* plugin. The values are configured in the *Planet* group of the weather configuration file and apply only when the world is rendered on a round planet (as with the *Cesium* plugin); on a flat map none of them has any effect.


When enabled, the subsystem drives the round-planet corrections every frame: it ramps the rounded-clouds planet radius with the observer's altitude, offsets the sky altitude, vetoes haze if it is not allowed, and keeps the weather regions, sky map, and cloud noise consistent across floating-origin rebases.


The *Planet* interface is obtained via the *[Weather::Manager](../../../../api/library/plugins/weather/class.weather_manager_usc.md)* class.


## Planet Class

### Members

## int isEnabled () const

Returns the current value indicating if the round-planet corrections are enabled: the altitude-driven cloud rounding, the sky offset that holds the horizon still across a floating-origin rebase, the haze veto, and the cloud noise continuity fixup. Configured via the *Planet.enabled* item of the weather configuration file; disabled by default. On a flat map the setting has no effect.
### Return value

Current the round-planet corrections are enabled
## int isHazeEnabled () const

Returns the current value indicating if haze is allowed to be rendered on the round planet. Haze is off by default because the flat-world haze is drawn as a hard band across the horizon once the horizon is curved; enable it only if the camera stays low enough for that not to show. Configured via the *Planet.haze_enabled* item of the weather configuration file.
### Return value

Current haze is allowed on the round planet
## float getCloudsRadius () const

Returns the current radius, in meters, the cloud layers are currently bent to. The value is interpolated between the configured minimum and maximum radii by the observer's geodetic altitude. The cloud radius is deliberately far smaller than the real radius of the Earth and is a rendering parameter rather than a physical one: ramping it with altitude keeps the curvature plausible both from the ground and from orbit.
### Return value

Current radius the cloud layers are currently bent to, in meters
