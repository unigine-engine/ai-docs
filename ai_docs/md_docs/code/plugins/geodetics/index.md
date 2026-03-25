# Geodetics Plugin


A world created in UNIGINE uses Cartesian coordinates, whereas real-world simulators normally use geospatial data. To make these two universes match, UNIGINE provides **Geodetics** plugin.


This plugin allows translating GPS latitude, longitude, and altitude coordinates to X, Y, and Z and vice versa. The solution is applicable for both flat rectangular terrain areas and the planet-shaped *Terrain Global*.


### See also


- *[Converter](../../../api/library/geodetics/geodetics_plugin/class.converter_cpp.md)* class
- *[Transformer](../../../api/library/geodetics/geodetics_plugin/class.transformer_cpp.md)* class


## Launching Geodetics Plugin


To use *Geodetics* plugin, specify the `extern_plugin` command line option on the application start-up:


```bash
main_x64 -extern_plugin "UnigineGeodetics"
```


## Using Geodetics Plugin


Here is an example code that illustrates how to position an object in a georeferenced world (that is a world having an enabled [Geodetic Pivot](../../../objects/geodetics/geodeticpivot/index.md) or a [Sandworm](../../../editor2/sandworm/index.md)-generated terrain) using geodetic coordinates:


```cpp
#include <plugins/Unigine/Geodetics/UnigineGeodetics.h>

int AppWorldLogic::init()
{
    Unigine::Math::dvec3 original_geo_pos = Unigine::Math::dvec3(35.105580, -89.966775, 0.0);
    Unigine::Math::dvec3 world_pos, geo_pos;

    world_pos = Unigine::Plugins::Geodetics::Converter::get()->geodeticToWorld(original_geo_pos);
    geo_pos = Unigine::Plugins::Geodetics::Converter::get()->worldToGeodetic(world_pos);

    Unigine::Log::message("original geo_pos %f %f %f \n", original_geo_pos.x, original_geo_pos.y, original_geo_pos.z);
    Unigine::Log::message("world_pos %f %f %f \n", world_pos.x, world_pos.y, world_pos.z);
    Unigine::Log::message("geo_pos %f %f %f \n", geo_pos.x, geo_pos.y, geo_pos.z);

    return 1;
}

```
