# Unigine::Plugins::Weather::Region Class (CS)


This class is used to manage weather regions. Each region contains one or multiple [layers](../../../../api/library/plugins/weather/class.weatherlayer_cs.md) each comprising a vertical profile. The [main layer](#getMainLayer_WeatherLayer) always exists in the region and cannot be deleted. It is a base layer used to define weather parameters for the region, such as [visibility range](../../../../api/library/plugins/weather/class.weatherlayer_cs.md#setVisibility_float_void), [temperature](../../../../api/library/plugins/weather/class.weatherlayer_cs.md#setTemperature_float_void), [humidity](../../../../api/library/plugins/weather/class.weatherlayer_cs.md#setHumidity_float_void), etc.


> **Notice:** IG plugin must be loaded.


There are three [types](#getRegionType_int) of weather regions available:

- **Global** - representing atmospheric layers, which have no distinct horizontal boundaries. Atmospheric effects are observed anywhere within the vertical range.
- **Local Rectangle** - they have the same set of parameters (visibility, coverage, wind) as *Global* ones but atmospheric effects for them are restricted to a certain area defined by a rectangle.
- **Local Polygon** - they have the same set of parameters (visibility, coverage, wind) as *Global* ones but atmospheric effects for them are restricted to a certain area defined by a polygon.


Global meteo conditions are managed via the [Meteo](../../../../api/library/plugins/weather/class.meteo_cs.md) class.


## Region Class

### Enums

## REGION_TYPE

| Name | Description |
|---|---|
| **GLOBAL** = 0 | Global region type (atmospheric layers, which have no distinct horizontal boundaries). |
| **RECTANGLE** = 1 | Local rectangle region type: regional weather with atmospheric effects restricted to a certain area defined by a rectangle. |
| **POLYGON** = 2 | Local polygon region type: regional weather with atmospheric effects restricted to a certain area defined by a polygon. |

### Properties

## float Rotation

The angle of rotation of the weather region around the Z axis.
## dvec2 WorldPosition

The world coordinates of the weather region's position.
## double TransitionSize

The width of the transition area around the borders of the weather region. The effects of the region fade out gradually within this area.
## 🔒︎ double ShapeRectangleRadius

The corner radius of the rectangle. This parameter defines the shape of a rounded rectangle.
## 🔒︎ dvec2 ShapeSize

The size of the rectangle that defines or encloses the shape of the weather region as a two-component vector.
## 🔒︎ int NumLayers

The total number of layers of the region.
## 🔒︎ WeatherLayer MainLayer

The main weather layer of the region. It is a base layer, that is used to define weather parameters, such as [visibility range](../../../../api/library/plugins/weather/class.weatherlayer_cs.md#setVisibility_float_void), [temperature](../../../../api/library/plugins/weather/class.weatherlayer_cs.md#setTemperature_float_void), [humidity](../../../../api/library/plugins/weather/class.weatherlayer_cs.md#setHumidity_float_void), etc. The main layer always exists in the region and cannot be deleted.
## bool Enabled

The value indicating if the weather region is currently enabled.
## 🔒︎ long ID

The ID of the region.
### Members

---

## WeatherLayer * CreateLayer ( long layer_id , WeatherLayerType type )

Creates a new weather layer for the region. In case a layer with the specified ID exists and has a different type, it will be replaced with the new one.
### Arguments

- *long* **layer_id** - ID of the layer to be created.
- *WeatherLayerType* **type** - Type of the layer to be created, one of the following values:

  - *Plugins::IG::WeatherLayerType::LAYER_BASE* - base layer.
  - *Plugins::IG::WeatherLayerType::LAYER_CLOUD* - [cloud layer](../../../../api/library/plugins/weather/class.weatherlayercloud_cs.md).
  - *Plugins::IG::WeatherLayerType::LAYER_PRECIPITATION* - [precipitation layer](../../../../api/library/plugins/weather/class.weatherlayerprecipitation_cs.md).

### Return value

New weather layer if it is created successfully; otherwise, nullptr.
## WeatherLayer GetLayer ( long layer_id )

Returns a weather layer by its ID.
### Arguments

- *long* **layer_id** - Weather layer ID.

### Return value

Weather layer with the specified ID if it exists, otherwise nullptr.
## bool RemoveLayer ( long layer_id )

Removes a weather layer with the specified ID.
### Arguments

- *long* **layer_id** - Weather layer ID.

### Return value

true if the weather layer is created successfully; otherwise, false.
## bool SetShapeAsRectangle ( dvec2 size , double corner_radius = 0 )

Sets the shape of a [rectangle](#REGION_TYPE_RECTANGLE) weather region using the specified width, height, and corner radius.
### Arguments

- *dvec2* **size** - Vector combining width and height of the rectangle, in units (W, H).
- *double* **corner_radius** - Corner radius of the rectangle, in units. This parameter enables you to create a rounded rectangle. > **Notice:** This value cannot be greater than half size.

### Return value

true if the shape of the region is set successfully; otherwise, false.
## bool SetShapeAsPolygon ( vec2[] points , ushort[] indices )

Sets the shape of a [polygon](#REGION_TYPE_POLYGON) weather region using the specified sets of vertex coordinates and their indices.
### Arguments

- *vec2[]* **points** - Array of polygon vertex coordinates.
- *ushort[]* **indices** - Array of vertex indices defining a polygon.

### Return value

true if the shape of the region is set successfully; otherwise, false.
## bool SetShapeAsPolygonGeodetic ( dvec2[] geo_points )

Sets the shape of a [polygon](#REGION_TYPE_POLYGON) weather region as a set of geocoordinates of points.
### Arguments

- *dvec2[]* **geo_points** - Array of geocoordinates of points forming a polygon.

### Return value

true if the shape of the region is set successfully; otherwise, false.
## bool SetShapeAsPolygonWorld ( vec3[] geo_points )

Sets the shape of a [polygon](#REGION_TYPE_POLYGON) weather region as a set of world coordinates of points.
### Arguments

- *vec3[]* **geo_points** - Array of world coordinates of points forming a polygon.

### Return value

true if the shape of the region is set successfully; otherwise, false.
## Region.REGION_TYPE GetRegionType ( )

Sets the type of the weather region's shape.
### Return value

Weather region type, one of the following:
- **GLOBAL** - global (atmospheric layers, which have no distinct horizontal boundaries)
- **RECTANGLE** - local (regional weather with atmospheric effects restricted to a certain area defined by a rectangle)
- **POLYGON** - local (regional weather with atmospheric effects restricted to a certain area defined by a polygon)


## void SetGeodeticPosition ( dvec2 geo_pos )

Sets new geocoordinates for the weather region's position.
### Arguments

- *dvec2* **geo_pos** - Geocoordinates of the weather region's position (Lat, Lon).

## float GetImpact ( dvec2 world_pos )

Returns a value indicating the degree of impact of the region at the specified point depending on whether it is completely inside, outside, or somewhere within the [transition area](#setTransitionSize_double_void).
### Arguments

- *dvec2* **world_pos** - World coordinates (Cartesian) of the point to be ckecked.

### Return value

Value indicating the degree of impact of the region at the specified point:
- 0 - completely outside the region (and transition area)
- 1 - inside the region
- (0 < x < 1) - within the transition area
