# Unigine::GeodeticPivot Class (CPP)

**Header:** #include <UnigineGeodeticPivot.h>

**Inherits from:** Node


This class is used to create and modify a *[Geodetic Pivot](../../../objects/geodetics/geodeticpivot/index.md)* object that is used to place world objects on their real world positions (latitude, longitude and altitude). The geodetic pivot contains an ellipsoid with a pivot point.


> **Notice:** In UNIGINE SDK editions other than Academic and Sim, the geodetic pivot object is equivalent to [NodeDummy](../../../api/library/nodes/class.nodedummy_cpp.md).


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
| **UP_AXIS_GEOCENTRIC_NORMAL** = 0 | The up axis is aligned with the line starting from the center of the Earth. |
| **UP_AXIS_GEODETIC_NORMAL** = 1 | The up axis is aligned with the normal to the surface. Switching to this type of axis is required if the obtained coordinates will be used to set the transforms of anything relative to the entity (such as camera on the plane or a laser beam from the plane). |

### Members

## void setOriginBasis ( int basis )

Sets a new origin basis set for the GeodeticPivot object:
- If [ORIGIN_BASIS_LOCAL](#ORIGIN_BASIS_LOCAL) is set, the binding to geo-coordinates is disabled. *GeodeticPivot* can be placed everywhere.
- If [ORIGIN_BASIS_ENU](#ORIGIN_BASIS_ENU) is set, *GeodeticPivot* is placed to the world ECF position with ENU (East - North - Up) orientation according to the given latitude / longitude / altitude. The *GeodeticPivot* position is blocked. > **Notice:** The Up-axis (Z+) direction in ENU points upward along the ellipsoid normal, while in UNIGINE implementation of ENU it goes from the Earth's center.


### Arguments

- *int* **basis** - The origin basis set for the GeodeticPivot object

## int getOriginBasis () const

Returns the current origin basis set for the GeodeticPivot object:
- If [ORIGIN_BASIS_LOCAL](#ORIGIN_BASIS_LOCAL) is set, the binding to geo-coordinates is disabled. *GeodeticPivot* can be placed everywhere.
- If [ORIGIN_BASIS_ENU](#ORIGIN_BASIS_ENU) is set, *GeodeticPivot* is placed to the world ECF position with ENU (East - North - Up) orientation according to the given latitude / longitude / altitude. The *GeodeticPivot* position is blocked. > **Notice:** The Up-axis (Z+) direction in ENU points upward along the ellipsoid normal, while in UNIGINE implementation of ENU it goes from the Earth's center.


### Return value

Current origin basis set for the GeodeticPivot object
## void setOrigin ( const Math:: dvec3 & origin )

Sets a new position (latitude, longitude and altitude) on the ellipsoid.
```cpp
// the GeodeticPivot will use WGS84 reference ellipsoid by default
GeodeticPivotPtr pivot = GeodeticPivot::create();
// update the origin
dvec3 new_york_origin = dvec3(40.71427,-74.00597,57.0);
pivot->setOrigin(new_york_origin);
ObjectMeshStaticPtr flat_new_york_ground = ObjectMeshStatic::create("flat_new_york_ground.mesh");
pivot->addChild(flat_new_york_ground); // the mesh will be bent once ObjectMeshStatic become a child of GeodeticPivot

```


### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md)&* **origin** - The position (latitude, longitude and altitude) on the ellipsoid

## Math:: dvec3 getOrigin () const

Returns the current position (latitude, longitude and altitude) on the ellipsoid.
```cpp
// the GeodeticPivot will use WGS84 reference ellipsoid by default
GeodeticPivotPtr pivot = GeodeticPivot::create();
// update the origin
dvec3 new_york_origin = dvec3(40.71427,-74.00597,57.0);
pivot->setOrigin(new_york_origin);
ObjectMeshStaticPtr flat_new_york_ground = ObjectMeshStatic::create("flat_new_york_ground.mesh");
pivot->addChild(flat_new_york_ground); // the mesh will be bent once ObjectMeshStatic become a child of GeodeticPivot

```


### Return value

Current position (latitude, longitude and altitude) on the ellipsoid
---

## static GeodeticPivotPtr create ( )

GeodeticPivot constructor. Creates a GeodeticPivot instance with the default settings:


- The origin is set to dvec3(0.0,0.0,0.0).
- The size of the curving region is 2048000�2048000 km.
- The resolution of the region texture is 2048.


## void setEllipsoid ( const Ptr < Ellipsoid > & ellipsoid )

Sets an Ellipsoid to be used for the *Geodetic Pivot*.
> **Notice:** Modifying the ellipsoid of the *Geodetic Pivot* directly makes the pivot's state inconsistent. You should force the GeodeticPivot node to update its internal state according to the modified ellipsoid by setting it via the *setEllipsoid()* method.


```cpp
// Creating a new geodetic pivot
GeodeticPivotPtr pivot = GeodeticPivot::create();

// setting the local (X - Y - Z) origin basis for it
pivot->setOriginBasis(GeodeticPivot::ORIGIN_BASIS_LOCAL);

// getting an ellipsoid currently used by the geodetic pivot
EllipsoidPtr ellipsoid = pivot->getEllipsoid();

// setting a fast calculation mode for the ellipsoid
ellipsoid->setMode(Ellipsoid::MODE_FAST);

// setting a new semimajor axis for the ellipsoid
ellipsoid->setSemimajorAxis(6378137.0f - 500.0f);

/* ... */

// force updating the geodetic pivot according to the modified ellipsoid
pivot->setEllipsoid(ellipsoid);

```


### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Ellipsoid](../../../api/library/geodetics/class.ellipsoid_cpp.md)> &* **ellipsoid** - Ellipsoid to be set.

## Ptr < Ellipsoid > getEllipsoid ( )

Returns the Ellipsoid currently used by the *Geodetic Pivot*.
> **Notice:** Modifying the ellipsoid of the *Geodetic Pivot* directly makes the pivot's state inconsistent. You should force the GeodeticPivot node to update its internal state according to the modified ellipsoid by setting it via the [*setEllipsoid()*](#setEllipsoid_Ellipsoid_void) method.


```cpp
// Creating a new geodetic pivot
GeodeticPivotPtr pivot = GeodeticPivot::create();

// setting the local (X - Y - Z) origin basis for it
pivot->setOriginBasis(GeodeticPivot::ORIGIN_BASIS_LOCAL);

// getting an ellipsoid currently used by the geodetic pivot
EllipsoidPtr ellipsoid = pivot->getEllipsoid();

// setting a fast calculation mode for the ellipsoid
ellipsoid->setMode(Ellipsoid::MODE_FAST);

// setting a new semimajor axis for the ellipsoid
ellipsoid->setSemimajorAxis(6378137.0f - 500.0f);

/* ... */

// force updating the geodetic pivot according to the modified ellipsoid
pivot->setEllipsoid(ellipsoid);

```


### Return value

Ellipsoid currently used by the *Geodetic Pivot*.
## void mapEllipsoidToFlat ( const Math:: vec3 & ellipsoid_point , Math:: vec3 & ret_flat_point , Math:: vec3 & ret_ellipsoid_normal )

Maps ellipsoid coordinates of a point to flat plane coordinates (using latitude and longitude as X and Y coordinates and altitude as Z).
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ellipsoid_point** - Ellipsoid coordinates of the point
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_flat_point** - Flat plane coordinates of the point.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_ellipsoid_normal** - Ellipsoid point normal coordinates.

## void mapEllipsoidToFlat ( const Math:: dvec3 & ellipsoid_point , Math:: dvec3 & ret_flat_point , Math:: dvec3 & ret_ellipsoid_normal )

Maps ellipsoid coordinates of a point to flat plane coordinates (using latitude and longitude as X and Y coordinates and altitude as Z).
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ellipsoid_point** - Ellipsoid coordinates of the point
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret_flat_point** - Flat plane coordinates of the point.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret_ellipsoid_normal** - Ellipsoid point normal coordinates.

## Math:: mat4 mapEllipsoidToFlat ( const Math:: mat4 & ellipsoid_transform )

Maps ellipsoid transformation to the flat plane transformation (using latitude and longitude as X and Y coordinates and altitude as Z).
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **ellipsoid_transform** - Ellipsoid transformation.

### Return value

Flat plane transformation.
## Math:: dmat4 mapEllipsoidToFlat ( const Math:: dmat4 & ellipsoid_transform )

Maps ellipsoid transformation to the flat plane transformation (using latitude and longitude as X and Y coordinates and altitude as Z).
### Arguments

- *const  Math::[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **ellipsoid_transform** - Ellipsoid transformation.

### Return value

Flat plane transformation.
## void mapFlatToEllipsoid ( const Math:: vec3 & flat_point , Math:: vec3 & ret_ellipsoid_point , Math:: vec3 & ret_ellipsoid_normal )

Maps flat plane coordinates to the ellipsoid (uses X and Y coordinates as latitude and longitude, and Z as altitude).
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **flat_point** - Flat plane coordinates of the point.
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_ellipsoid_point** - Ellipsoid coordinates of the point
- *Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **ret_ellipsoid_normal** - Ellipsoid point normal coordinates.

## void mapFlatToEllipsoid ( const Math:: dvec3 & flat_point , Math:: dvec3 & ret_ellipsoid_point , Math:: dvec3 & ret_ellipsoid_normal )

Maps flat plane coordinates to the ellipsoid (uses X and Y coordinates as latitude and longitude, and Z as altitude).
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **flat_point** - Flat plane coordinates of the point.
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret_ellipsoid_point** - Ellipsoid coordinates of the point
- *Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ret_ellipsoid_normal** - Ellipsoid point normal coordinates.

## Math:: mat4 mapFlatToEllipsoid ( const Math:: mat4 & flat_transform )

Maps flat plane transformation to the ellipsoid transformation (uses X and Y coordinates as latitude and longitude, and Z as altitude).
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **flat_transform** - Flat plane transformation.

### Return value

Ellipsoid transformation.
## Math:: dmat4 mapFlatToEllipsoid ( const Math:: dmat4 & flat_transform )

Maps flat plane transformation to the ellipsoid transformation (uses X and Y coordinates as latitude and longitude, and Z as altitude).
### Arguments

- *const  Math::[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **flat_transform** - Flat plane transformation.

### Return value

Ellipsoid transformation.
## Math:: dvec3 mapFlatToGeodetic ( const Math:: dvec3 & flat_point )

Maps flat plane coordinates to geodetic latitude / longitude / altitude coordinates according to pivot's origin.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **flat_point** - Flat plane coordinates.

### Return value

Geodetic coordinates.
## Math:: dvec3 mapFlatToGeodetic ( const Math:: vec3 & flat_point )

Maps flat plane coordinates to geodetic latitude / longitude / altitude coordinates according to pivot's origin.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md) &* **flat_point** - Flat plane coordinates.

### Return value

Geodetic coordinates.
## void mapFlatsToGeodetic ( const double * src_x , const double * src_y , int size , double * OUT_ret_lat , double * OUT_ret_lon )

Pefrorms batch mapping of flat plane coordinates to geodetic latitude / longitude coordinates according to pivot's origin and puts the result to the corresponding output arrays.
### Arguments

- *const double ** **src_x** - Array of flat plane X coordinates.
- *const double ** **src_y** - Array of flat plane Y coordinates.
- *int* **size** - Array size.
- *double ** **OUT_ret_lat** - Output array of geodetic latitude coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *double ** **OUT_ret_lon** - Output array of geodetic longitude coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## Math:: dvec3 mapGeodeticToFlat ( const Math:: dvec3 & geodetic_coords )

Maps geodetic latitude / longitude / altitude coordinates to flat plane coordinates according to pivot's latitude / longitude / altitude origin.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_coords** - Geodetic coordinates.

### Return value

Flat plane coordinates.
## void mapGeodeticsToFlat ( const double * lat , const double * lon , int size , double * OUT_ret_x , double * OUT_ret_y )

Pefrorms batch mapping of geodetic latitude / longitude coordinates to flat plane coordinates according to pivot's latitude / longitude origin and puts the result to the corresponding output arrays.
### Arguments

- *const double ** **lat** - Array of geodetic latitude coordinates.
- *const double ** **lon** - Array of geodetic longitude coordinates.
- *int* **size** - Array size.
- *double ** **OUT_ret_x** - Output array of flat plane X coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
- *double ** **OUT_ret_y** - Output array of flat plane Y coordinates. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## Math:: mat4 mapMeshEllipsoidToFlat ( Ptr < Mesh > & mesh , const Math:: mat4 & ellipsoid_transform )

Maps a curved mesh to the flat plane (using latitude / longitude / altitude as X / Y / Z coordinates).
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - Mesh to be mapped.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **ellipsoid_transform** - Mesh ellipsoid transformation.

### Return value

Position on the flat plane, where the node is to be placed.
## Math:: dmat4 mapMeshEllipsoidToFlat ( Ptr < Mesh > & mesh , const Math:: dmat4 & ellipsoid_transform )

Maps a curved mesh to the flat plane (using latitude / longitude / altitude as X / Y / Z coordinates).
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - Mesh to be mapped.
- *const  Math::[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **ellipsoid_transform** - Mesh ellipsoid transformation.

### Return value

Position on the flat plane, where the node is to be placed.
## Math:: mat4 mapMeshFlatToEllipsoid ( Ptr < Mesh > & mesh , const Math:: mat4 & flat_transform )

Maps a flat mesh to the ellipsoid (uses X and Y coordinates as latitude and longitude, and Z as altitude).
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - Mesh to be mapped.
- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **flat_transform** - Mesh flat plane transformation.

### Return value

Position on the ellipsoid, where the node is to be placed.
## Math:: dmat4 mapMeshFlatToEllipsoid ( Ptr < Mesh > & mesh , const Math:: dmat4 & flat_transform )

Maps a flat mesh to the ellipsoid (uses X and Y coordinates as latitude and longitude, and Z as altitude).
### Arguments

- *[Ptr](../../../api/library/common/class.ptr_cpp.md)<[Mesh](../../../api/library/rendering/class.mesh_cpp.md)> &* **mesh** - Mesh to be mapped.
- *const  Math::[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **flat_transform** - Mesh flat plane transformation.

### Return value

Position on the ellipsoid, where the node is to be placed.
## Math:: dvec3 toGeodetic ( const Math:: mat4 & world_transform )

Returns geodetic coordinates for a given world transformation matrix.
### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **world_transform** - World transformation.

### Return value

Geodetic coordinates.
## Math:: dvec3 toGeodetic ( const Math:: dmat4 & world_transform )

Returns geodetic coordinates for a given world transformation matrix.
### Arguments

- *const  Math::[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **world_transform** - World transformation.

### Return value

Geodetic coordinates.
## Math:: dmat4 toWorld ( const Math:: dvec3 & geodetic_coords , GeodeticPivot::UP_AXIS up_axis = Enum.GeodeticPivot.UP_AXIS.GEOCENTRIC_NORMAL )


Returns world transformation matrix for given geodetic coordinates.


> **Notice:** If the obtained coordinates will be used to set the transforms for anything relative to the entity (such as camera on the plane or a laser beam from the plane), switch the up axis type to [geodetic normal](#UP_AXIS_GEODETIC_NORMAL).


### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_coords** - Geodetic coordinates.
- *[GeodeticPivot::UP_AXIS](../../../api/library/geodetics/class.geodeticpivot_cpp.md#UP_AXIS)* **up_axis** - Type of the [UP axis](#up_axis). If the obtained coordinates will be used to set the transforms for anything relative to the entity (such as camera on the plane or a laser beam from the plane), switch the up axis type to [geodetic normal](#UP_AXIS_GEODETIC_NORMAL).

### Return value

World transformation.
## Math:: mat4 toWorldPreserveRotation ( const Math:: mat4 & world_transform , const Math:: dvec3 & geodetic_coords , GeodeticPivot::UP_AXIS up_axis = Enum.GeodeticPivot.UP_AXIS.GEOCENTRIC_NORMAL )


Returns new world transformation matrix preserving rotation relative to normal.


> **Notice:** If the obtained coordinates will be used to set the transforms for anything relative to the entity (such as camera on the plane or a laser beam from the plane), switch the up axis type to [geodetic normal](#UP_AXIS_GEODETIC_NORMAL).


### Arguments

- *const  Math::[mat4](../../../api/library/math/class.mat4_cpp.md) &* **world_transform** - World transformation.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_coords** - Geodetic coordinates.
- *[GeodeticPivot::UP_AXIS](../../../api/library/geodetics/class.geodeticpivot_cpp.md#UP_AXIS)* **up_axis** - Type of the [UP axis](#up_axis). If the obtained coordinates will be used to set the transforms for anything relative to the entity (such as camera on the plane or a laser beam from the plane), switch the up axis type to [geodetic normal](#UP_AXIS_GEODETIC_NORMAL).

### Return value

New world transformation.
## Math:: dmat4 toWorldPreserveRotation ( const Math:: dmat4 & world_transform , const Math:: dvec3 & geodetic_coords , GeodeticPivot::UP_AXIS up_axis = Enum.GeodeticPivot.UP_AXIS.GEOCENTRIC_NORMAL )


Returns new world transformation matrix preserving rotation relative to normal.


> **Notice:** If the obtained coordinates will be used to set the transforms for anything relative to the entity (such as camera on the plane or a laser beam from the plane), switch the up axis type to [geodetic normal](#UP_AXIS_GEODETIC_NORMAL).


### Arguments

- *const  Math::[dmat4](../../../api/library/math/class.dmat4_cpp.md) &* **world_transform** - World transformation.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_coords** - Geodetic coordinates.
- *[GeodeticPivot::UP_AXIS](../../../api/library/geodetics/class.geodeticpivot_cpp.md#UP_AXIS)* **up_axis** - Type of the [UP axis](#up_axis). If the obtained coordinates will be used to set the transforms for anything relative to the entity (such as camera on the plane or a laser beam from the plane), switch the up axis type to [geodetic normal](#UP_AXIS_GEODETIC_NORMAL).

### Return value

New world transformation.
## static int type ( )

Returns the type of the object.
### Return value

[GeodeticPivot](../../../api/library/nodes/class.node_cpp.md#GEODETIC_PIVOT) type identifier.
