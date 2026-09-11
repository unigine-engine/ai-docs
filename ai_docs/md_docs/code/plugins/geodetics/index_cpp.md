# Geodetics Plugin (CPP)


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


## Anchor: a Moving Local Origin


A georeference does not have to be static. On a globe it cannot be: floating-point coordinates lose precision with distance from the origin, and every point on the Earth's surface is some 6378 km away from the centre of the planet. The way out is a local frame whose origin sits near the camera and moves with it � the **anchor** � which is what the *[Cesium](../../../code/plugins/cesium/index_cpp.md)* plugin drives while it streams a globe.


Which of the four georeferencing modes is in force is reported by *[Converter::getGeodeticMode()](../../../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#GeodeticMode)*:


| Mode | The frame comes from |
|---|---|
| GEODETIC_MODE_NOT_AVAILABLE | Nothing: the world is not georeferenced |
| GEODETIC_MODE_GEODETIC_PIVOT | A [Geodetic Pivot](../../../objects/geodetics/geodeticpivot/index.md) node in the world |
| GEODETIC_MODE_PROJECTED | A projected terrain, described by an EPSG code or a WKT2 string |
| GEODETIC_MODE_ANCHOR | The anchor, moved at run time by whoever drives it |


The anchor itself is reached through *[Converter::getAnchor()](../../../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#getAnchor_Anchor)*. The object always exists, so its change event can be connected at initialization time whatever the world turns out to be georeferenced by, and it carries:


- *[getMode()](../../../api/library/geodetics/geodetics_plugin/class.anchor_cpp.md#Mode)* � ANCHOR_MODE_GEOPOSITION for a tangent ENU frame at a geodetic point, or ANCHOR_MODE_GEOCENTRIC where world space is the geocentric space itself
- *[setGeoPosition()](../../../api/library/geodetics/geodetics_plugin/class.anchor_cpp.md#GeoPosition)* and *[getGeoPosition()](../../../api/library/geodetics/geodetics_plugin/class.anchor_cpp.md#GeoPosition)* � the geodetic coordinate the local frame is currently pinned to
- *[reset()](../../../api/library/geodetics/geodetics_plugin/class.anchor_cpp.md#reset_void)* � drop the frame back to geocentric
- *[getGeocentricToWorld()](../../../api/library/geodetics/geodetics_plugin/class.anchor_cpp.md#GeocentricToWorld)* and *[getWorldToGeocentric()](../../../api/library/geodetics/geodetics_plugin/class.anchor_cpp.md#WorldToGeocentric)* � the frame as a matrix pair, with *[getOldGeocentricToWorld()](../../../api/library/geodetics/geodetics_plugin/class.anchor_cpp.md#OldGeocentricToWorld)* and *[getOldWorldToGeocentric()](../../../api/library/geodetics/geodetics_plugin/class.anchor_cpp.md#OldWorldToGeocentric)* holding the pair that was in force before the last change, for anything that needs the delta across a move
- *[getEventChanged()](../../../api/library/geodetics/geodetics_plugin/class.anchor_cpp.md#EventChanged)* � fires on every frame change and means "the anchor moved, rebase now". Not to be confused with *[Converter::getEventInitialized()](../../../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#EventInitialized)*, which means the georeference itself was redefined


```cpp
#include <plugins/Unigine/Geodetics/UnigineGeodetics.h>

using namespace Unigine;

void MyLogic::init()
{
    auto *converter = Plugins::Geodetics::Converter::get();
    if (!converter)
        return;

    // The anchor object is always there, so this connection can be made before
    // any world is loaded and whatever georeference that world brings.
    converter->getAnchor()->getEventChanged().connect(connections, this, &MyLogic::rebase);
}

void MyLogic::rebase()
{
    auto *converter = Plugins::Geodetics::Converter::get();

    // Everything that lives in the local frame is placed from its geodetic
    // coordinates again - the numbers it held are relative to the old origin.
    node->setWorldPosition(converter->geodeticToWorld(geo_position));
}

```


> **Warning:** Whatever is placed in the local frame and does not follow the anchor drifts away from the ground, or jumps, as soon as the world rebases.


> **Notice:** The anchor is not a read-only view of the georeference: calling *[setGeoPosition()](../../../api/library/geodetics/geodetics_plugin/class.anchor_cpp.md#GeoPosition)* moves the converter into GEODETIC_MODE_ANCHOR. While the world is georeferenced some other way, the anchor reports ANCHOR_MODE_GEOCENTRIC with identity matrices, so *[getGeodeticMode()](../../../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#GeodeticMode)* == GEODETIC_MODE_ANCHOR is the way to ask whether the anchor is what actually drives the frame.


> **Notice:** *[getGeoPosition()](../../../api/library/geodetics/geodetics_plugin/class.anchor_cpp.md#GeoPosition)* is only meaningful in ANCHOR_MODE_GEOPOSITION � check *[getMode()](../../../api/library/geodetics/geodetics_plugin/class.anchor_cpp.md#Mode)* first. The geocentric frame has no geodetic coordinate to report, and (0, 0, 0) is not it: that is a real tangent frame in the Gulf of Guinea.


### Disabling the Automatic World Georeference


On world load the plugin scans the world and georeferences it from what it finds � a [Geodetic Pivot](../../../objects/geodetics/geodeticpivot/index.md), or a projected terrain. That scan would overwrite a frame that something else is driving, so an application whose anchor is driven at run time has to switch it off:


```cpp
Plugins::Geodetics::Converter::get()->setAutoWorldInit(false);
```


> **Warning:** Switch it off only when something really does drive the anchor. An application without such a driver that disables the scan never georeferences its worlds at all.
