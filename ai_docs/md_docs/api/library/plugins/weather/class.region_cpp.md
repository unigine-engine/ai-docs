# Unigine::Plugins::Weather::Region Class (CPP)

**Header:** #include <plugins/Unigine/Weather/UnigineWeather.h>


This class is used to manage weather regions. Each region contains one or multiple [layers](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md) each comprising a vertical profile. The [main layer](#getMainLayer_WeatherLayer) always exists in the region and cannot be deleted. It is a base layer used to define weather parameters for the region, such as [visibility range](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md#setVisibility_float_void), [temperature](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md#setTemperature_float_void), [humidity](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md#setHumidity_float_void), etc.


> **Notice:** IG plugin must be loaded.


There are three [types](#getRegionType_int) of weather regions available:

- **Global** - representing atmospheric layers, which have no distinct horizontal boundaries. Atmospheric effects are observed anywhere within the vertical range.
- **Local Rectangle** - they have the same set of parameters (visibility, coverage, wind) as *Global* ones but atmospheric effects for them are restricted to a certain area defined by a rectangle.
- **Local Polygon** - they have the same set of parameters (visibility, coverage, wind) as *Global* ones but atmospheric effects for them are restricted to a certain area defined by a polygon.


Global meteo conditions are managed via the [Meteo](../../../../api/library/plugins/weather/class.meteo_cpp.md) class.


## Region Class

### Enums

## REGION_TYPE

| Name | Description |
|---|---|
| **REGION_TYPE_GLOBAL** = 0 | Global region type (atmospheric layers, which have no distinct horizontal boundaries). |
| **REGION_TYPE_RECTANGLE** = 1 | Local rectangle region type: regional weather with atmospheric effects restricted to a certain area defined by a rectangle. |
| **REGION_TYPE_POLYGON** = 2 | Local polygon region type: regional weather with atmospheric effects restricted to a certain area defined by a polygon. |

### Members

## void setRotation ( float rotation )

Sets a new angle of rotation of the weather region around the Z axis.
### Arguments

- *float* **rotation** - The current rotation angle, in degrees within the [-360; 360] range.

## float getRotation () const

Returns the current angle of rotation of the weather region around the Z axis.
### Return value

Current current rotation angle, in degrees within the [-360; 360] range.
## void setWorldPosition ( const Math:: dvec2 & position )

Sets a new world coordinates of the weather region's position.
### Arguments

- *const  Math::[dvec2](../../../../api/library/math/class.dvec2_cpp.md)&* **position** - The Cartesian coordinates of the weather region's position (X, Y).

## Math:: dvec2 getWorldPosition () const

Returns the current world coordinates of the weather region's position.
### Return value

Current Cartesian coordinates of the weather region's position (X, Y).
## void setTransitionSize ( double size )

Sets a new width of the transition area around the borders of the weather region. The effects of the region fade out gradually within this area.
### Arguments

- *double* **size** - The width of the transition area around the borders of the weather region, in meters.

## double getTransitionSize () const

Returns the current width of the transition area around the borders of the weather region. The effects of the region fade out gradually within this area.
### Return value

Current width of the transition area around the borders of the weather region, in meters.
## double getShapeRectangleRadius () const

Returns the current corner radius of the rectangle. This parameter defines the shape of a rounded rectangle.
### Return value

Current corner radius of the rectangle, in units.
## Math:: dvec2 getShapeSize () const

Returns the current size of the rectangle that defines or encloses the shape of the weather region as a two-component vector.
### Return value

Current Two-component vector (W, L) containing width and length of the rectangle (in meters) that defines or encloses the shape of the weather region depending on its type:
- **Global** - *(inf, inf)*
- **Rectangle** - *(rectangle_width, rectangle_length)*
- **Polygon** - *(boundbox_width, boundbox_length)*


## int getNumLayers () const

Returns the current total number of layers of the region.
### Return value

Current number of layers.
## WeatherLayer * getMainLayer () const

Returns the current main weather layer of the region. It is a base layer, that is used to define weather parameters, such as [visibility range](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md#setVisibility_float_void), [temperature](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md#setTemperature_float_void), [humidity](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md#setHumidity_float_void), etc. The main layer always exists in the region and cannot be deleted.
### Return value

Current main weather layer of the region.
## void setEnabled ( bool enabled )

Sets a new value indicating if the weather region is currently enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable the weather region is currently; **false** - to disable it.

## bool isEnabled () const

Returns the current value indicating if the weather region is currently enabled.
### Return value

**true** if the weather region is currently is enabled ; otherwise **false**.
## long long getID () const

Returns the current ID of the region.
### Return value

Current Region ID.
---

## WeatherLayer * createLayer ( long long layer_id , WeatherLayerType type )

Creates a new weather layer for the region. In case a layer with the specified ID exists and has a different type, it will be replaced with the new one.
### Arguments

- *long long* **layer_id** - ID of the layer to be created.
- *WeatherLayerType* **type** - Type of the layer to be created, one of the following values:

  - *Plugins::IG::WeatherLayerType::LAYER_BASE* - base layer.
  - *Plugins::IG::WeatherLayerType::LAYER_CLOUD* - [cloud layer](../../../../api/library/plugins/weather/class.weatherlayercloud_cpp.md).
  - *Plugins::IG::WeatherLayerType::LAYER_PRECIPITATION* - [precipitation layer](../../../../api/library/plugins/weather/class.weatherlayerprecipitation_cpp.md).

### Return value

New weather layer if it is created successfully; otherwise, nullptr.
## WeatherLayer * getLayer ( long long layer_id )

Returns a weather layer by its ID.
### Arguments

- *long long* **layer_id** - Weather layer ID.

### Return value

Weather layer with the specified ID if it exists, otherwise nullptr.
## bool removeLayer ( long long layer_id )

Removes a weather layer with the specified ID.
### Arguments

- *long long* **layer_id** - Weather layer ID.

### Return value

true if the weather layer is created successfully; otherwise, false.
## void getLayers ( Vector <WeatherLayer*>& vec ) const

Returns the list of all [layers](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md) (base, clouds, precipitation) contained in the weather region.
### Arguments

- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<WeatherLayer*>&* **vec** - The list of all [layers](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md) in the weather region.

## void findWeatherLayersGeodetic ( const Math::dvec3& geo_pos , Vector <MeteoPositionParam>& vector ) const

Returns the list of all [layers](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md) (base, clouds, precipitation) of the weather region containing the specified position (and thus affecting it) along with their corresponding [impact](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md#getImpact_double_float) factors (as *[MeteoPositionParam](../../../../api/library/plugins/weather/class.meteopositionparam_cpp.md)* structure).
### Arguments

- *const  Math::dvec3&* **geo_pos** - Geocoordinates of the point for which all affecting layers are to be found.
- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<MeteoPositionParam>&* **vector** - The list of all [layers](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md) in the weather region containing the specified position (and thus affecting it) along with their corresponding [impact](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md#getImpact_double_float) factors (as *[MeteoPositionParam](../../../../api/library/plugins/weather/class.meteopositionparam_cpp.md)* structure).

## void findWeatherLayersWorld ( const Math::Vec3& world_pos , Vector <MeteoPositionParam>& vector ) const

Returns the list of all [layers](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md) (base, clouds, precipitation) of the weather region containing the specified position (and thus affecting it) along with their corresponding [impact](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md#getImpact_double_float) factors (as *[MeteoPositionParam](../../../../api/library/plugins/weather/class.meteopositionparam_cpp.md)* structure).
### Arguments

- *const  Math::Vec3&* **world_pos** - World coordinates of the point for which all affecting layers are to be found.
- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<MeteoPositionParam>&* **vector** - The list of all [layers](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md) in the weather region containing the specified position (and thus affecting it) along with their corresponding [impact](../../../../api/library/plugins/weather/class.weatherlayer_cpp.md#getImpact_double_float) factors (as *[MeteoPositionParam](../../../../api/library/plugins/weather/class.meteopositionparam_cpp.md)* structure).

## bool setShapeAsRectangle ( const Math::dvec2& size , double corner_radius = 0 )

Sets the shape of a [rectangle](#REGION_TYPE_RECTANGLE) weather region using the specified width, height, and corner radius.
### Arguments

- *const  Math::dvec2&* **size** - Vector combining width and height of the rectangle, in units (W, H).
- *double* **corner_radius** - Corner radius of the rectangle, in units. This parameter enables you to create a rounded rectangle. > **Notice:** This value cannot be greater than half size.

### Return value

true if the shape of the region is set successfully; otherwise, false.
## bool setShapeAsPolygon ( const Vector < Math:: vec2 > & points , const Vector < unsigned short > & indices )

Sets the shape of a [polygon](#REGION_TYPE_POLYGON) weather region using the specified sets of vertex coordinates and their indices.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[vec2](../../../../api/library/math/class.vec2_cpp.md) > &* **points** - Array of polygon vertex coordinates.
- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< unsigned short > &* **indices** - Array of vertex indices defining a polygon.

### Return value

true if the shape of the region is set successfully; otherwise, false.
## bool setShapeAsPolygonGeodetic ( const Vector < Math:: dvec2 > & geo_points )

Sets the shape of a [polygon](#REGION_TYPE_POLYGON) weather region as a set of geocoordinates of points.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[dvec2](../../../../api/library/math/class.dvec2_cpp.md) > &* **geo_points** - Array of geocoordinates of points forming a polygon.

### Return value

true if the shape of the region is set successfully; otherwise, false.
## bool setShapeAsPolygonWorld ( const Vector < Math:: Vec3 > & geo_points )

Sets the shape of a [polygon](#REGION_TYPE_POLYGON) weather region as a set of world coordinates of points.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<  Math::[Vec3](../../../../api/library/math/class.vec3_cpp.md) > &* **geo_points** - Array of world coordinates of points forming a polygon.

### Return value

true if the shape of the region is set successfully; otherwise, false.
## Region::REGION_TYPE getRegionType ( ) const

Sets the type of the weather region's shape.
### Return value

Weather region type, one of the following:
- **GLOBAL** - global (atmospheric layers, which have no distinct horizontal boundaries)
- **RECTANGLE** - local (regional weather with atmospheric effects restricted to a certain area defined by a rectangle)
- **POLYGON** - local (regional weather with atmospheric effects restricted to a certain area defined by a polygon)


## void setGeodeticPosition ( const Math::dvec2& geo_pos )

Sets new geocoordinates for the weather region's position.
### Arguments

- *const  Math::dvec2&* **geo_pos** - Geocoordinates of the weather region's position (Lat, Lon).

## float getImpact ( const Math::dvec2& world_pos ) const

Returns a value indicating the degree of impact of the region at the specified point depending on whether it is completely inside, outside, or somewhere within the [transition area](#setTransitionSize_double_void).
### Arguments

- *const  Math::dvec2&* **world_pos** - World coordinates (Cartesian) of the point to be ckecked.

### Return value

Value indicating the degree of impact of the region at the specified point:
- 0 - completely outside the region (and transition area)
- 1 - inside the region
- (0 < x < 1) - within the transition area


## void * addOnChangedCallback ( CallbackBase * callback )

Adds a callback on changing region parameters.
```cpp
/// callback function to be called when region parameters change
void SomeClass::my_region_callback()
{
	// actions to be performed on changing region parameters
}

// ...
// somewhere in code
void SomeClass::init()
{
	// adding "my_region_callback" to be called on changing weather conditions
	ig_manager->getMeteo()->getRegion(1)->addOnChangedCallback(this, Unigine::MakeCallback(this, &SomeClass::my_region_callback );
}

```


### Arguments

- *[CallbackBase](../../../../api/library/common/callbacks/class.callbackbase_cpp.md) ** **callback** - Callback pointer.

### Return value

Callback subscriber ID. This ID can be used to [remove](#removeOnChangedCallback_void_ptr_bool) this callback when necessary.
## bool removeOnChangedCallback ( void * id )

Removes a callback on changing region parameters for the specified subscriber.
### Arguments

- *void ** **id** - Callback subscriber ID specified when [adding](#addOnChangedCallback_CallbackBase_ptr_void_ptr) it.

### Return value

true if the callback for the specified subscriber is removed successfully; otherwise, false.
