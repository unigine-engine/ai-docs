# Unigine::Plugins::Weather::Meteo Class (CPP)

**Header:** #include <plugins/Unigine/Weather/UnigineWeather.h>


This class is used to manage global meteo conditions (visibility range, wind speed and direction).

> **Notice:** Weather plugin must be loaded.


## Meteo Class

### Members

## MeteoCameraEffects * getCameraEffects () const

Returns the current [camera effects](../../../../api/library/plugins/weather/class.meteocameraeffects_cpp.md) instance used to create dynamic effects for precipitation rendering when changing camera position and speed.
### Return value

Current camera effects instance.
## Region * getGlobalRegion () const

Returns the current main global [weather region](../../../../api/library/plugins/weather/class.region_cpp.md).
### Return value

Current main global [weather region](../../../../api/library/plugins/weather/class.region_cpp.md).
## int getNumRegions () const

Returns the current total number of [weather regions](../../../../api/library/plugins/weather/class.region_cpp.md).
### Return value

Current total number of [weather regions](../../../../api/library/plugins/weather/class.region_cpp.md).
## double getCloudBottom () const

Returns the current height of the bottom (lower bound) of the lowest cloud layer among all [weather regions](../../../../api/library/plugins/weather/class.region_cpp.md).
### Return value

Current height of the bottom (lower bound) of the lowest cloud layer among all weather regions.
---

## Region * getRegion ( long long id , bool auto_create )

Returns the interface of a [weather region/layer](../../../../api/library/plugins/weather/class.region_cpp.md) by its identifier. If no weather region/layer with such id exists, it will be created.
### Arguments

- *long long* **id** - Weather region identifier .
- *bool* **auto_create** - true to automatically create the region with the specified ID if it doesn't exist yet; false - to return nullptr in case the region doesn't exist.

### Return value

[Weather region](../../../../api/library/plugins/weather/class.region_cpp.md) interface if it exists; otherwise - nullptr.
## bool removeRegion ( long long id )

Removes a [weather region](../../../../api/library/plugins/weather/class.region_cpp.md) with a given identifier.
### Arguments

- *long long* **id** - Identifier of the weather region to be removed .

### Return value

true if a region with a given identifier is removed successfully; otherwise, false.
## void clearRegions ( )

Removes all [weather regions and layers](../../../../api/library/plugins/weather/class.region_cpp.md).
## Math:: vec3 getMeanWindVelocityGeodetic ( const Math::dvec3& geo_pos ) const

Returns an average wind velocity at the specified geodetic location. This method combines wind parameter of all [weather regions and layers](../../../../api/library/plugins/weather/class.region_cpp.md) affecting this point.
### Arguments

- *const  Math::dvec3&* **geo_pos** - Geodetic coordinates of a point (lat, lon, alt), for which an average wind speed and direction are to be calculated.

### Return value

Vector defining average wind velocity (in meters per second) in all directions for the given location.
## Math:: vec3 getMeanWindVelocityWorld ( const Math::Vec3& world_pos ) const

Returns an average wind velocity at the specified world location. This method combines wind parameter of all [weather regions and layers](../../../../api/library/plugins/weather/class.region_cpp.md) affecting this point.
### Arguments

- *const  Math::Vec3&* **world_pos** - World coordinates of a point (lat, lon, alt), for which an average wind speed and direction are to be calculated.

### Return value

Vector defining average wind velocity (in meters per second) in all directions for the given location.
## void * addOnCreateRegionCallback ( Unigine:: CallbackBase1 < Unigine::Plugins::IG::Region >* func )

Sets a callback function to be fired when a new [weather region](../../../../api/library/plugins/weather/class.region_cpp.md) is created.
### Arguments

- *Unigine::[CallbackBase1](../../../../api/library/common/callbacks/class.callbackbase1_cpp.md) <  Unigine::Plugins::IG::Region >** **func** - Callback pointer. The callback function must have the following signature: (*Unigine::Plugins::IG::Region* ***region**)

### Return value

ID of the last added Create Region callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnCreateRegionCallback_void_ptr_bool) this callback when necessary.
## bool removeOnCreateRegionCallback ( void * id )

Removes the specified callback from the list of Create Region callbacks.
### Arguments

- *void ** **id** - Create Region callback ID obtained when [adding](#addOnCreateRegionCallback_CallbackBase1_ptr_void_ptr) it.

### Return value

true if the Create Region callback with the given ID was removed successfully; otherwise false.
## void clearOnCreateRegionCallbacks ( )

Clears all [added](#addOnCreateRegionCallback_CallbackBase1_ptr_void_ptr) Create Region callbacks.
## void * addOnRemoveRegionCallback ( Unigine:: CallbackBase1 < Unigine::Plugins::IG::Region >* func )

Sets a callback function to be fired when a [weather region](../../../../api/library/plugins/weather/class.region_cpp.md) is removed.
### Arguments

- *Unigine::[CallbackBase1](../../../../api/library/common/callbacks/class.callbackbase1_cpp.md) <  Unigine::Plugins::IG::Region >** **func** - Callback pointer. The callback function must have the following signature: (*Unigine::Plugins::IG::Region* ***region**)

### Return value

ID of the last added Remove Region callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnRemoveRegionCallback_void_ptr_bool) this callback when necessary.
## bool removeOnRemoveRegionCallback ( void * id )

Removes the specified callback from the list of Remove Region callbacks.
### Arguments

- *void ** **id** - Remove Region callback ID obtained when [adding](#addOnRemoveRegionCallback_CallbackBase1_ptr_void_ptr) it.

### Return value

true if the Remove Region callback with the given ID was removed successfully; otherwise false.
## void clearOnRemoveRegionCallbacks ( )

Clears all [added](#addOnRemoveRegionCallback_CallbackBase1_ptr_void_ptr) Remove Region callbacks.
## void * addOnLightningStrikeCallback ( Unigine:: CallbackBase2 < Unigine:: Math:: Vec3 , int > * func )

Sets a callback function to be fired when a lightning strikes.
### Arguments

- *Unigine::[CallbackBase2](../../../../api/library/common/callbacks/class.callbackbase2_cpp.md) <  Unigine:: Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md), int > ** **func** - Callback pointer. The callback function must have the following signature: (*Unigine::Math::Vec3* **geo_pos**, *int* **type**)

### Return value

ID of the last added Lightning Strike callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnLightningStrikeCallback_void_ptr_bool) this callback when necessary.
## bool removeOnLightningStrikeCallback ( void * id )

Removes the specified callback from the list of Lightning Strike callbacks.
### Arguments

- *void ** **id** - Lightning Strike callback ID obtained when [adding](#addOnLightningStrikeCallback_CallbackBase2_ptr_void_ptr) it.

### Return value

true if the Lightning Strike callback with the given ID was removed successfully; otherwise false.
## void clearOnLightningStrikeCallbacks ( )

Clears all [added](#addOnLightningStrikeCallback_CallbackBase2_ptr_void_ptr) Lightning Strike callbacks.
## void * addOnMeteoChangedCallback ( CallbackBase * callback )

Adds a callback on changing global meteo conditions.
```cpp
/// callback function to be called when weather conditions change
void SomeClass::my_weather_callback()
{
	// setting orientation of the vane downwind
	Vec3 geo_position = ig_manager->getConverter()->worldToGeodetic(vane_node->getWorldPosition());
	vec3 wind_direction = ig_manager->getMeteo()->getMeanWindSpeed(geo_position);
	vane_node->setWorldDirection(wind_direction, vec3_up);
}

// ...
// somewhere in code
void SomeClass::init()
{
	// adding "my_weather_callback" to be called on changing weather conditions
	ig_manager->getMeteo()->addOnMeteoChangedCallback(this, Unigine::MakeCallback(this, &SomeClass::my_weather_callback ));
}

```


### Arguments

- *[CallbackBase](../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback** - Callback pointer.

### Return value

Callback subscriber ID. This ID can be used to [remove](#removeOnMeteoChangedCallback_void_ptr_bool) this callback when necessary.
## void removeOnMeteoChangedCallback ( void * subscriber )

Removes a callback on changing global meteo conditions for the specified subscriber.
### Arguments

- *void ** **subscriber** - Callback subscriber ID specified when [adding](#addOnMeteoChangedCallback_CallbackBase_ptr_void_ptr) it.

## void clearOnMeteoChangedCallbacks ( )

Clears all [added](#addOnMeteoChangedCallback_CallbackBase_ptr_void_ptr) callbacks on changing global meteo conditions.
## void findWeatherLayersGeodetic ( const Math::dvec3& geo_pos , Vector <MeteoPositionParam>& vector ) const

Returns the list of all [weather layers](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md) (base, clouds, precipitation) of all [weather regions](../../../../api/library/plugins/weather/class.region_cpp.md) containing the specified geodetic position (and thus affecting it) along with their corresponding [impact](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md#getImpact_double_float) factors (as *[MeteoPositionParam](../../../../api/library/plugins/weather/class.meteopositionparam_cpp.md)* structure).
### Arguments

- *const  Math::dvec3&* **geo_pos** - Geocoordinates of the point for which all affecting layers of all regions are to be found.
- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<MeteoPositionParam>&* **vector** - The list of all [layers](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md) in the weather region containing the specified position (and thus affecting it) along with their corresponding [impact](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md#getImpact_double_float) factors (as *[MeteoPositionParam](../../../../api/library/plugins/weather/class.meteopositionparam_cpp.md)* structure).

## void findWeatherLayersGeodetic ( const Vec3& geo_pos , Vector <MeteoPositionParam>& vector ) const

Returns the list of all [weather layers](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md) (base, clouds, precipitation) of all [weather regions](../../../../api/library/plugins/weather/class.region_cpp.md) containing the specified world position (and thus affecting it) along with their corresponding [impact](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md#getImpact_double_float) factors (as *[MeteoPositionParam](../../../../api/library/plugins/weather/class.meteopositionparam_cpp.md)* structure).
### Arguments

- *const Vec3&* **geo_pos** - World coordinates of the point for which all affecting layers of all regions are to be found.
- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<MeteoPositionParam>&* **vector** - The list of all [layers](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md) in the weather region containing the specified position (and thus affecting it) along with their corresponding [impact](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md#getImpact_double_float) factors (as *[MeteoPositionParam](../../../../api/library/plugins/weather/class.meteopositionparam_cpp.md)* structure).

## void lightningStrikeGeodetic ( const Math::dvec3& geo_pos , int type = -1 )

Generates a lightning strike effect at the specified geodetic location.
### Arguments

- *const  Math::dvec3&* **geo_pos** - Geocoordinates of the lightning strike location.
- *int* **type**

## void lightningStrikeWorld ( const Math::Vec3& world_pos , int type = -1 )

Generates a lightning strike effect at the specified world location.
### Arguments

- *const  Math::Vec3&* **world_pos** - World coordinates of the lightning strike location.
- *int* **type**

## Region * getRegionByIndex ( int index )

Returns a [weather region](../../../../api/library/plugins/weather/class.region_cpp.md) by its index.
### Arguments

- *int* **index** - Weather region index in the range from 0 to the [total number of regions.](#getNumRegions_int)

### Return value

Weather region with the specified index if it exists, otherwise nullptr.
