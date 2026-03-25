# Unigine::Plugins::Weather::Meteo Class (CS)


This class is used to manage global meteo conditions (visibility range, wind speed and direction).

> **Notice:** Weather plugin must be loaded.


## Meteo Class

### Properties

## 🔒︎ MeteoCameraEffects CameraEffects

The [camera effects](../../../../api/library/plugins/weather/class.meteocameraeffects_cs.md) instance used to create dynamic effects for precipitation rendering when changing camera position and speed.
## 🔒︎ Region GlobalRegion

The main global [weather region](../../../../api/library/plugins/weather/class.region_cs.md).
## 🔒︎ int NumRegions

The total number of [weather regions](../../../../api/library/plugins/weather/class.region_cs.md).
## 🔒︎ double CloudBottom

The height of the bottom (lower bound) of the lowest cloud layer among all [weather regions](../../../../api/library/plugins/weather/class.region_cs.md).
### Members

---

## Region GetRegion ( long id , bool auto_create )

Returns the interface of a [weather region/layer](../../../../api/library/plugins/weather/class.region_cs.md) by its identifier. If no weather region/layer with such id exists, it will be created.
### Arguments

- *long* **id** - Weather region identifier .
- *bool* **auto_create** - true to automatically create the region with the specified ID if it doesn't exist yet; false - to return nullptr in case the region doesn't exist.

### Return value

[Weather region](../../../../api/library/plugins/weather/class.region_cs.md) interface if it exists; otherwise - nullptr.
## bool RemoveRegion ( long id )

Removes a [weather region](../../../../api/library/plugins/weather/class.region_cs.md) with a given identifier.
### Arguments

- *long* **id** - Identifier of the weather region to be removed .

### Return value

true if a region with a given identifier is removed successfully; otherwise, false.
## void ClearRegions ( )

Removes all [weather regions and layers](../../../../api/library/plugins/weather/class.region_cs.md).
## vec3 GetMeanWindVelocityGeodetic ( dvec3 geo_pos )

Returns an average wind velocity at the specified geodetic location. This method combines wind parameter of all [weather regions and layers](../../../../api/library/plugins/weather/class.region_cs.md) affecting this point.
### Arguments

- *dvec3* **geo_pos** - Geodetic coordinates of a point (lat, lon, alt), for which an average wind speed and direction are to be calculated.

### Return value

Vector defining average wind velocity (in meters per second) in all directions for the given location.
## vec3 GetMeanWindVelocityWorld ( vec3 world_pos )

Returns an average wind velocity at the specified world location. This method combines wind parameter of all [weather regions and layers](../../../../api/library/plugins/weather/class.region_cs.md) affecting this point.
### Arguments

- *vec3* **world_pos** - World coordinates of a point (lat, lon, alt), for which an average wind speed and direction are to be calculated.

### Return value

Vector defining average wind velocity (in meters per second) in all directions for the given location.
## IntPtr AddOnCreateRegionCallback ( OnCreateRegionDelegate func )

Sets a callback function to be fired when a new [weather region](../../../../api/library/plugins/weather/class.region_cs.md) is created.
### Arguments

- *OnCreateRegionDelegate* **func** - Callback function with the following signature: void OnCreateRegion(*Region* **region**)

### Return value

ID of the last added Create Region callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnCreateRegionCallback_void_ptr_bool) this callback when necessary.
## bool RemoveOnCreateRegionCallback ( IntPtr id )

Removes the specified callback from the list of Create Region callbacks.
### Arguments

- *IntPtr* **id** - Create Region callback ID obtained when [adding](#addOnCreateRegionCallback_CallbackBase1_ptr_void_ptr) it.

### Return value

true if the Create Region callback with the given ID was removed successfully; otherwise false.
## void ClearOnCreateRegionCallbacks ( )

Clears all [added](#addOnCreateRegionCallback_CallbackBase1_ptr_void_ptr) Create Region callbacks.
## IntPtr AddOnRemoveRegionCallback ( OnRemoveRegionDelegate func )

Sets a callback function to be fired when a [weather region](../../../../api/library/plugins/weather/class.region_cs.md) is removed.
### Arguments

- *OnRemoveRegionDelegate* **func** - Callback function with the following signature: void OnRemoveRegion(*Region* **region**)

### Return value

ID of the last added Remove Region callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnRemoveRegionCallback_void_ptr_bool) this callback when necessary.
## bool RemoveOnRemoveRegionCallback ( IntPtr id )

Removes the specified callback from the list of Remove Region callbacks.
### Arguments

- *IntPtr* **id** - Remove Region callback ID obtained when [adding](#addOnRemoveRegionCallback_CallbackBase1_ptr_void_ptr) it.

### Return value

true if the Remove Region callback with the given ID was removed successfully; otherwise false.
## void ClearOnRemoveRegionCallbacks ( )

Clears all [added](#addOnRemoveRegionCallback_CallbackBase1_ptr_void_ptr) Remove Region callbacks.
## IntPtr AddOnLightningStrikeCallback ( OnLightningStrikeDelegate func )

Sets a callback function to be fired when a lightning strikes.
### Arguments

- *OnLightningStrikeDelegate* **func** - Callback function with the following signature: void OnLightningStrike(*Vec3* **geo_pos**, *int* **type**)

### Return value

ID of the last added Lightning Strike callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnLightningStrikeCallback_void_ptr_bool) this callback when necessary.
## bool RemoveOnLightningStrikeCallback ( IntPtr id )

Removes the specified callback from the list of Lightning Strike callbacks.
### Arguments

- *IntPtr* **id** - Lightning Strike callback ID obtained when [adding](#addOnLightningStrikeCallback_CallbackBase2_ptr_void_ptr) it.

### Return value

true if the Lightning Strike callback with the given ID was removed successfully; otherwise false.
## void ClearOnLightningStrikeCallbacks ( )

Clears all [added](#addOnLightningStrikeCallback_CallbackBase2_ptr_void_ptr) Lightning Strike callbacks.
## IntPtr AddOnMeteoChangedCallback ( OnMeteoChangedDelegate callback )

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

- *OnMeteoChangedDelegate* **callback** - Callback function with the following signature: void OnMeteoChangedDelegate()

### Return value

Callback subscriber ID. This ID can be used to [remove](#removeOnMeteoChangedCallback_void_ptr_bool) this callback when necessary.
## void RemoveOnMeteoChangedCallback ( IntPtr subscriber )

Removes a callback on changing global meteo conditions for the specified subscriber.
### Arguments

- *IntPtr* **subscriber** - Callback subscriber ID specified when [adding](#addOnMeteoChangedCallback_CallbackBase_ptr_void_ptr) it.

## void ClearOnMeteoChangedCallbacks ( )

Clears all [added](#addOnMeteoChangedCallback_CallbackBase_ptr_void_ptr) callbacks on changing global meteo conditions.
## void LightningStrikeGeodetic ( dvec3 geo_pos , int type = -1 )

Generates a lightning strike effect at the specified geodetic location.
### Arguments

- *dvec3* **geo_pos** - Geocoordinates of the lightning strike location.
- *int* **type**

## void LightningStrikeWorld ( vec3 world_pos , int type = -1 )

Generates a lightning strike effect at the specified world location.
### Arguments

- *vec3* **world_pos** - World coordinates of the lightning strike location.
- *int* **type**

## Region GetRegionByIndex ( int index )

Returns a [weather region](../../../../api/library/plugins/weather/class.region_cs.md) by its index.
### Arguments

- *int* **index** - Weather region index in the range from 0 to the [total number of regions.](#getNumRegions_int)

### Return value

Weather region with the specified index if it exists, otherwise nullptr.
