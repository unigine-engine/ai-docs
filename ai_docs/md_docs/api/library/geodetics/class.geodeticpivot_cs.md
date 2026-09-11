# Unigine::GeodeticPivot Class (CS)

**Inherits from:** Node


This class is used to create and modify a *[Geodetic Pivot](../../../objects/geodetics/geodeticpivot/index.md)* object that is used to place world objects on their real world positions (latitude, longitude and altitude). The geodetic pivot contains an ellipsoid with a pivot point.


> **Notice:** In UNIGINE SDK editions other than Academic and Sim, the geodetic pivot object is equivalent to [NodeDummy](../../../api/library/nodes/class.nodedummy_cs.md).


**Important:**


If you for any reason need to obtain the entity transforms (such as the position and rotation of your plane) to use them for configuring a camera on this entity or any beam emitted by this entity back to the ground, or anything similar, you need to consider the following while using *Geodetic Pivot*:


- The "Up" axis starts at the estimated center of the ellipsoid Earth model and is directed outwards. ![](pivot_model.png)
- When the object is shifted upwards along this axis, its world coordinates X and Y will also change relative to the projected terrain (expected direction - grey line, actual direction - orange line). ![](surface_fragment.png) Thus, if we use directly the transforms obtained from the engine (for example, the world coordinates of the plane to orient the camera), the result will differ from what is expected.
- To obtain the corrected (and expected) transformations, you need to set the normal **to Geodetic** in the corresponding method (*[toWorld()](#toWorld_dvec3_int_dmat4), [toWorldPreserveRotation()](#toWorldPreserveRotation_mat4_dvec3_int_mat4)*), the requried recalculations will be performed automatically.


Here is an example of a simple converter that allows transforming geodetic coordinates to world coordinates and vice versa:


```cpp
class Converter
{
public:
	static Converter *get()
	{
		static Converter instance;
		return &instance;
	}

	void init()
	{
		geodetic_pivot = static_ptr_cast<Unigine::GeodeticPivot>(Unigine::World::getNodeByType(Unigine::Node::GEODETIC_PIVOT));
		if (geodetic_pivot)
		{
			Unigine::ObjectTerrainGlobalPtr terrain_global = static_ptr_cast<Unigine::ObjectTerrainGlobal>(Unigine::World::getNodeByType(Unigine::Node::OBJECT_TERRAIN_GLOBAL));
			is_curved_terrain = terrain_global && terrain_global->findAncestor(Unigine::Node::GEODETIC_PIVOT) != -1;
		}

		inited = geodetic_pivot.isValid();
	}

	Unigine::Math::dvec3 worldToGeodetic(const Unigine::Math::Vec3 &world_pos) const
	{
		UNIGINE_ASSERT(inited && "Converter is not initialized!");

		if (is_curved_terrain)
			return geodetic_pivot->toGeodetic(translate(world_pos));
		return geodetic_pivot->mapFlatToGeodetic(world_pos);
	}

	Unigine::Math::Vec3 geodeticToWorld(const Unigine::Math::dvec3 &geo_pos) const
	{
		UNIGINE_ASSERT(inited && "Converter is not initialized!");

		if (is_curved_terrain)
			return Unigine::Math::Vec3(geodetic_pivot->toWorld(geo_pos).getTranslate());
		return Unigine::Math::Vec3(geodetic_pivot->mapGeodeticToFlat(geo_pos));
	}

	Unigine::Math::Mat4 getZeroBasis(const Unigine::Math::dvec3 &geo_pos) const
	{
		UNIGINE_ASSERT(inited && "Converter is not initialized!");

		if (is_curved_terrain)
			return geodetic_pivot->toWorld(geo_pos, Unigine::GeodeticPivot::UP_AXIS_GEODETIC_NORMAL);

		// convert curved rotation to flat (forward.z = 0)
		Unigine::Math::dmat4 transform = geodetic_pivot->toWorld(geo_pos, Unigine::GeodeticPivot::UP_AXIS_GEODETIC_NORMAL);
		Unigine::Math::dvec3 up = Unigine::Math::dvec3_up;
		Unigine::Math::dvec3 forward = transform.getColumn3(1);
		forward.z = 0;
		forward = normalize(forward);
		Unigine::Math::dvec3 right = cross(forward, up);
		transform.setColumn3(0, right);
		transform.setColumn3(1, forward);
		transform.setColumn3(2, up);
		return Unigine::Math::Mat4(transform);
	}

private:
	Converter() = default;
	~Converter() = default;

	bool inited = false;
	bool is_curved_terrain = false;
	Unigine::GeodeticPivotPtr geodetic_pivot;
};

```


To use this *Converter* class:


```cpp
Converter::get()->init(); // called in world::init

// anywhere in code
Conveter::get()->worldToGeodetic ...

```


### See also


UnigineScript sample


## GeodeticPivot Class

### Enums

## UP_AXIS

| Name | Description |
|---|---|
| **GEOCENTRIC_NORMAL** = 0 | The up axis is aligned with the line starting from the center of the Earth. |
| **GEODETIC_NORMAL** = 1 | The up axis is aligned with the normal to the surface. Switching to this type of axis is required if the obtained coordinates will be used to set the transforms of anything relative to the entity (such as camera on the plane or a laser beam from the plane). |

### Properties

## int OriginBasis

The origin basis set for the GeodeticPivot object:
- If [ORIGIN_BASIS_LOCAL](#ORIGIN_BASIS_LOCAL) is set, the binding to geo-coordinates is disabled. *GeodeticPivot* can be placed everywhere.
- If [ORIGIN_BASIS_ENU](#ORIGIN_BASIS_ENU) is set, *GeodeticPivot* is placed to the world ECF position with ENU (East - North - Up) orientation according to the given latitude / longitude / altitude. The *GeodeticPivot* position is blocked. > **Notice:** The Up-axis (Z+) direction in ENU points upward along the ellipsoid normal, while in UNIGINE implementation of ENU it goes from the Earth's center.


## dvec3 Origin

The position (latitude, longitude and altitude) on the ellipsoid.
```csharp
// the GeodeticPivot will use WGS84 reference ellipsoid by default
GeodeticPivot pivot = new GeodeticPivot();
// update the origin
dvec3 new_york_origin = dvec3(40.71427,-74.00597,57.0);
pivot.setOrigin(new_york_origin);
ObjectMeshStatic flat_new_york_ground = new ObjectMeshStatic("flat_new_york_ground.mesh");
pivot.addChild(flat_new_york_ground); // the mesh will be bent once ObjectMeshStatic become a child of GeodeticPivot

```


### Members

---

## GeodeticPivot ( )

GeodeticPivot constructor. Creates a GeodeticPivot instance with the default settings:


- The origin is set to dvec3(0.0,0.0,0.0).
- The size of the curving region is 2048000�2048000 km.
- The resolution of the region texture is 2048.


## void SetEllipsoid ( Ellipsoid ellipsoid )

Sets an Ellipsoid to be used for the *Geodetic Pivot*.
> **Notice:** Modifying the ellipsoid of the *Geodetic Pivot* directly makes the pivot's state inconsistent. You should force the GeodeticPivot node to update its internal state according to the modified ellipsoid by setting it via the *setEllipsoid()* method.


```csharp
// Creating a new geodetic pivot
GeodeticPivot pivot = new GeodeticPivot();

// setting the local (X - Y - Z) origin basis for it
pivot.setOriginBasis(GeodeticPivot.ORIGIN_BASIS_LOCAL);

// getting an ellipsoid currently used by the geodetic pivot
Ellipsoid ellipsoid = pivot.getEllipsoid();

// setting a fast calculation mode for the ellipsoid
ellipsoid.setMode(Ellipsoid.MODE_FAST);

// setting a new semimajor axis for the ellipsoid
ellipsoid.setSemimajorAxis(6378137.0f - 500.0f);

/* ... */

// force updating the geodetic pivot according to the modified ellipsoid
pivot.setEllipsoid(ellipsoid);

```


### Arguments

- *[Ellipsoid](../../../api/library/geodetics/class.ellipsoid_cs.md)* **ellipsoid** - Ellipsoid to be set.

## Ellipsoid GetEllipsoid ( )

Returns the Ellipsoid currently used by the *Geodetic Pivot*.
> **Notice:** Modifying the ellipsoid of the *Geodetic Pivot* directly makes the pivot's state inconsistent. You should force the GeodeticPivot node to update its internal state according to the modified ellipsoid by setting it via the [*setEllipsoid()*](#setEllipsoid_Ellipsoid_void) method.


```csharp
// Creating a new geodetic pivot
GeodeticPivot pivot = new GeodeticPivot();

// setting the local (X - Y - Z) origin basis for it
pivot.setOriginBasis(GeodeticPivot.ORIGIN_BASIS_LOCAL);

// getting an ellipsoid currently used by the geodetic pivot
Ellipsoid ellipsoid = pivot.getEllipsoid();

// setting a fast calculation mode for the ellipsoid
ellipsoid.setMode(Ellipsoid.MODE_FAST);

// setting a new semimajor axis for the ellipsoid
ellipsoid.setSemimajorAxis(6378137.0f - 500.0f);

/* ... */

// force updating the geodetic pivot according to the modified ellipsoid
pivot.setEllipsoid(ellipsoid);

```


### Return value

Ellipsoid currently used by the *Geodetic Pivot*.
## void MapEllipsoidToFlat ( vec3 ellipsoid_point , out vec3 ret_flat_point , out vec3 ret_ellipsoid_normal )

Maps ellipsoid coordinates of a point to flat plane coordinates (using latitude and longitude as X and Y coordinates and altitude as Z).
### Arguments

- *vec3* **ellipsoid_point** - Ellipsoid coordinates of the point
- *out vec3* **ret_flat_point** - Flat plane coordinates of the point.
- *out vec3* **ret_ellipsoid_normal** - Ellipsoid point normal coordinates.

## void MapEllipsoidToFlat ( dvec3 ellipsoid_point , out dvec3 ret_flat_point , out dvec3 ret_ellipsoid_normal )

Maps ellipsoid coordinates of a point to flat plane coordinates (using latitude and longitude as X and Y coordinates and altitude as Z).
### Arguments

- *dvec3* **ellipsoid_point** - Ellipsoid coordinates of the point
- *out dvec3* **ret_flat_point** - Flat plane coordinates of the point.
- *out dvec3* **ret_ellipsoid_normal** - Ellipsoid point normal coordinates.

## mat4 MapEllipsoidToFlat ( mat4 ellipsoid_transform )

Maps ellipsoid transformation to the flat plane transformation (using latitude and longitude as X and Y coordinates and altitude as Z).
### Arguments

- *mat4* **ellipsoid_transform** - Ellipsoid transformation.

### Return value

Flat plane transformation.
## dmat4 MapEllipsoidToFlat ( dmat4 ellipsoid_transform )

Maps ellipsoid transformation to the flat plane transformation (using latitude and longitude as X and Y coordinates and altitude as Z).
### Arguments

- *dmat4* **ellipsoid_transform** - Ellipsoid transformation.

### Return value

Flat plane transformation.
## void MapFlatToEllipsoid ( vec3 flat_point , out vec3 ret_ellipsoid_point , out vec3 ret_ellipsoid_normal )

Maps flat plane coordinates to the ellipsoid (uses X and Y coordinates as latitude and longitude, and Z as altitude).
### Arguments

- *vec3* **flat_point** - Flat plane coordinates of the point.
- *out vec3* **ret_ellipsoid_point** - Ellipsoid coordinates of the point
- *out vec3* **ret_ellipsoid_normal** - Ellipsoid point normal coordinates.

## void MapFlatToEllipsoid ( dvec3 flat_point , out dvec3 ret_ellipsoid_point , out dvec3 ret_ellipsoid_normal )

Maps flat plane coordinates to the ellipsoid (uses X and Y coordinates as latitude and longitude, and Z as altitude).
### Arguments

- *dvec3* **flat_point** - Flat plane coordinates of the point.
- *out dvec3* **ret_ellipsoid_point** - Ellipsoid coordinates of the point
- *out dvec3* **ret_ellipsoid_normal** - Ellipsoid point normal coordinates.

## mat4 MapFlatToEllipsoid ( mat4 flat_transform )

Maps flat plane transformation to the ellipsoid transformation (uses X and Y coordinates as latitude and longitude, and Z as altitude).
### Arguments

- *mat4* **flat_transform** - Flat plane transformation.

### Return value

Ellipsoid transformation.
## dmat4 MapFlatToEllipsoid ( dmat4 flat_transform )

Maps flat plane transformation to the ellipsoid transformation (uses X and Y coordinates as latitude and longitude, and Z as altitude).
### Arguments

- *dmat4* **flat_transform** - Flat plane transformation.

### Return value

Ellipsoid transformation.
## dvec3 MapFlatToGeodetic ( dvec3 flat_point )

Maps flat plane coordinates to geodetic latitude / longitude / altitude coordinates according to pivot's origin.
### Arguments

- *dvec3* **flat_point** - Flat plane coordinates.

### Return value

Geodetic coordinates.
## dvec3 MapFlatToGeodetic ( vec3 flat_point )

Maps flat plane coordinates to geodetic latitude / longitude / altitude coordinates according to pivot's origin.
### Arguments

- *vec3* **flat_point** - Flat plane coordinates.

### Return value

Geodetic coordinates.
## void MapFlatsToGeodetic ( double[] src_x , double[] src_y , int size , double[] OUT_ret_lat , double[] OUT_ret_lon )

Pefrorms batch mapping of flat plane coordinates to geodetic latitude / longitude coordinates according to pivot's origin and puts the result to the corresponding output arrays.
### Arguments

- *double[]* **src_x** - Array of flat plane X coordinates.
- *double[]* **src_y** - Array of flat plane Y coordinates.
- *int* **size** - Array size.
- *double[]* **OUT_ret_lat** - Output array of geodetic latitude coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *double[]* **OUT_ret_lon** - Output array of geodetic longitude coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## dvec3 MapGeodeticToFlat ( dvec3 geodetic_coords )

Maps geodetic latitude / longitude / altitude coordinates to flat plane coordinates according to pivot's latitude / longitude / altitude origin.
### Arguments

- *dvec3* **geodetic_coords** - Geodetic coordinates.

### Return value

Flat plane coordinates.
## void MapGeodeticsToFlat ( double[] lat , double[] lon , int size , double[] OUT_ret_x , double[] OUT_ret_y )

Pefrorms batch mapping of geodetic latitude / longitude coordinates to flat plane coordinates according to pivot's latitude / longitude origin and puts the result to the corresponding output arrays.
### Arguments

- *double[]* **lat** - Array of geodetic latitude coordinates.
- *double[]* **lon** - Array of geodetic longitude coordinates.
- *int* **size** - Array size.
- *double[]* **OUT_ret_x** - Output array of flat plane X coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *double[]* **OUT_ret_y** - Output array of flat plane Y coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## mat4 MapMeshEllipsoidToFlat ( Mesh mesh , mat4 ellipsoid_transform )

Maps a curved mesh to the flat plane (using latitude / longitude / altitude as X / Y / Z coordinates).
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Mesh to be mapped.
- *mat4* **ellipsoid_transform** - Mesh ellipsoid transformation.

### Return value

Position on the flat plane, where the node is to be placed.
## dmat4 MapMeshEllipsoidToFlat ( Mesh mesh , dmat4 ellipsoid_transform )

Maps a curved mesh to the flat plane (using latitude / longitude / altitude as X / Y / Z coordinates).
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Mesh to be mapped.
- *dmat4* **ellipsoid_transform** - Mesh ellipsoid transformation.

### Return value

Position on the flat plane, where the node is to be placed.
## mat4 MapMeshFlatToEllipsoid ( Mesh mesh , mat4 flat_transform )

Maps a flat mesh to the ellipsoid (uses X and Y coordinates as latitude and longitude, and Z as altitude).
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Mesh to be mapped.
- *mat4* **flat_transform** - Mesh flat plane transformation.

### Return value

Position on the ellipsoid, where the node is to be placed.
## dmat4 MapMeshFlatToEllipsoid ( Mesh mesh , dmat4 flat_transform )

Maps a flat mesh to the ellipsoid (uses X and Y coordinates as latitude and longitude, and Z as altitude).
### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_cs.md)* **mesh** - Mesh to be mapped.
- *dmat4* **flat_transform** - Mesh flat plane transformation.

### Return value

Position on the ellipsoid, where the node is to be placed.
## dvec3 ToGeodetic ( mat4 world_transform )

Returns geodetic coordinates for a given world transformation matrix.
### Arguments

- *mat4* **world_transform** - World transformation.

### Return value

Geodetic coordinates.
## dvec3 ToGeodetic ( dmat4 world_transform )

Returns geodetic coordinates for a given world transformation matrix.
### Arguments

- *dmat4* **world_transform** - World transformation.

### Return value

Geodetic coordinates.
## dmat4 ToWorld ( dvec3 geodetic_coords , GeodeticPivot.UP_AXIS up_axis = Enum.GeodeticPivot.UP_AXIS.GEOCENTRIC_NORMAL )


Returns world transformation matrix for given geodetic coordinates.


> **Notice:** If the obtained coordinates will be used to set the transforms for anything relative to the entity (such as camera on the plane or a laser beam from the plane), switch the up axis type to [geodetic normal](#UP_AXIS_GEODETIC_NORMAL).


### Arguments

- *dvec3* **geodetic_coords** - Geodetic coordinates.
- *[GeodeticPivot.UP_AXIS](../../../api/library/geodetics/class.geodeticpivot_cs.md#UP_AXIS)* **up_axis** - Type of the [UP axis](#up_axis). If the obtained coordinates will be used to set the transforms for anything relative to the entity (such as camera on the plane or a laser beam from the plane), switch the up axis type to [geodetic normal](#UP_AXIS_GEODETIC_NORMAL).

### Return value

World transformation.
## mat4 ToWorldPreserveRotation ( mat4 world_transform , dvec3 geodetic_coords , GeodeticPivot.UP_AXIS up_axis = Enum.GeodeticPivot.UP_AXIS.GEOCENTRIC_NORMAL )


Returns new world transformation matrix preserving rotation relative to normal.


> **Notice:** If the obtained coordinates will be used to set the transforms for anything relative to the entity (such as camera on the plane or a laser beam from the plane), switch the up axis type to [geodetic normal](#UP_AXIS_GEODETIC_NORMAL).


### Arguments

- *mat4* **world_transform** - World transformation.
- *dvec3* **geodetic_coords** - Geodetic coordinates.
- *[GeodeticPivot.UP_AXIS](../../../api/library/geodetics/class.geodeticpivot_cs.md#UP_AXIS)* **up_axis** - Type of the [UP axis](#up_axis). If the obtained coordinates will be used to set the transforms for anything relative to the entity (such as camera on the plane or a laser beam from the plane), switch the up axis type to [geodetic normal](#UP_AXIS_GEODETIC_NORMAL).

### Return value

New world transformation.
## dmat4 ToWorldPreserveRotation ( dmat4 world_transform , dvec3 geodetic_coords , GeodeticPivot.UP_AXIS up_axis = Enum.GeodeticPivot.UP_AXIS.GEOCENTRIC_NORMAL )


Returns new world transformation matrix preserving rotation relative to normal.


> **Notice:** If the obtained coordinates will be used to set the transforms for anything relative to the entity (such as camera on the plane or a laser beam from the plane), switch the up axis type to [geodetic normal](#UP_AXIS_GEODETIC_NORMAL).


### Arguments

- *dmat4* **world_transform** - World transformation.
- *dvec3* **geodetic_coords** - Geodetic coordinates.
- *[GeodeticPivot.UP_AXIS](../../../api/library/geodetics/class.geodeticpivot_cs.md#UP_AXIS)* **up_axis** - Type of the [UP axis](#up_axis). If the obtained coordinates will be used to set the transforms for anything relative to the entity (such as camera on the plane or a laser beam from the plane), switch the up axis type to [geodetic normal](#UP_AXIS_GEODETIC_NORMAL).

### Return value

New world transformation.
## static int type ( )

Returns the type of the object.
### Return value

[GeodeticPivot](../../../api/library/nodes/class.node_cs.md#GEODETIC_PIVOT) type identifier.
