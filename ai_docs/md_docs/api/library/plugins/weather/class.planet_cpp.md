# Unigine::Plugins::Weather::Planet Class (CPP)

**Header:** #include <plugins/Unigine/Weather/UnigineWeather.h>


This class provides a read-only run-time view of the round-planet subsystem of the *[Weather](../../../../ig/weather/index.md)* plugin. The values are configured in the *Planet* group of the weather configuration file and apply only when the world is rendered on a round planet (as with the *Cesium* plugin); on a flat map none of them has any effect.


When enabled, the subsystem drives the round-planet corrections every frame: it ramps the rounded-clouds planet radius with the observer's altitude, offsets the sky altitude, vetoes haze if it is not allowed, and keeps the weather regions, sky map, and cloud noise consistent across floating-origin rebases.


The *Planet* interface is obtained via the *[Weather::Manager](../../../../api/library/plugins/weather/class.weather_manager_cpp.md)* class.


## Planet Class

### Members

## bool isEnabled () const

Returns the current value indicating if the round-planet corrections are enabled: the altitude-driven cloud rounding, the sky offset that holds the horizon still across a floating-origin rebase, the haze veto, and the cloud noise continuity fixup. Configured via the *Planet.enabled* item of the weather configuration file; disabled by default. On a flat map the setting has no effect.
### Return value

**true** if the round-planet corrections are enabled; otherwise **false**.
## bool isHazeEnabled () const

Returns the current value indicating if haze is allowed to be rendered on the round planet. Haze is off by default because the flat-world haze is drawn as a hard band across the horizon once the horizon is curved; enable it only if the camera stays low enough for that not to show. Configured via the *Planet.haze_enabled* item of the weather configuration file.
### Return value

**true** if haze is allowed on the round planet; otherwise **false**.
## float getCloudsRadius () const

Returns the current radius, in meters, the cloud layers are currently bent to. The value is interpolated between the configured minimum and maximum radii by the observer's geodetic altitude. The cloud radius is deliberately far smaller than the real radius of the Earth and is a rendering parameter rather than a physical one: ramping it with altitude keeps the curvature plausible both from the ground and from orbit.
### Return value

Current radius the cloud layers are currently bent to, in meters
