# Geodetic Pivot


> **Notice:** In UNIGINE SDK editions other than *Engineering* and *Sim*, the geodetic pivot object is equivalent to *[NodeDummy](../../../api/library/nodes/class.nodedummy_cpp.md)*.


A **Geodetic Pivot** object is an abstract object that contains an ellipsoid with a pivot point. By using *Geodetic Pivot* you can place objects on the scene on the corresponding places in the real world.


*Geodetic Pivot* helps to place world objects on their real world positions (latitude, longitude and altitude) by curving a plane with objects on it. Pivot converts real geodetic data to Cartesian and simultaneously "curves" objects to simulate the contorted Earth's surface.


*Geodetic Pivot* works with:


- [ObjectTerrainGlobal](../../../objects/objects/terrain/terrain_global/index.md)
- [ObjectWaterGlobal](../../../objects/objects/water/water_object.md)
- [ObjectCloudLayer](../../../objects/objects/cloud_layer/index.md)
- [ObjectSky](../../../objects/objects/sky/index.md)
- [ObjectMeshStatic](../../../objects/objects/mesh/index.md)
- [ObjectGrass](../../../objects/objects/grass/index.md)
- [ObjectMeshClutter](../../../objects/objects/mesh_clutter/index.md)
- [WorldClutter](../../../objects/worlds/world_clutter/index.md)
- [Mesh Decals](../../../objects/decals/mesh/index.md)


[![](index.jpg)](index.jpg)

*CurvedObjectMeshStaticwithWorldClutter*


### See Also


- The *[GeodeticPivot](../../../api/library/geodetics/class.geodeticpivot_cpp.md)* class to manage scenes with geodetic data via API
- The `render_show_geodetic_pivot` console command to show *Geodetic Pivots* in the scene
- A Wikipedia article on *[Ellipsoid](https://en.wikipedia.org/wiki/Ellipsoid)*
- A Wikipedia article on *[Geodesics on an ellipsoid](https://en.wikipedia.org/wiki/Geodesics_on_an_ellipsoid)*


## Adding a Geodetic Pivot


To add a *Geodetic Pivot* to the scene via UnigineEditor do the following:


1. [Run](../../../sdk/projects/index_cpp.md#run) the project with UnigineEditor.
2. On the Menu bar, click *Create -> Geodetics -> Pivot*. ![](create.png)
3. Place the *Geodetic Pivot* somewhere in the world.


## Setting Up a Geodetic Pivot


After adding the *Geodetic Pivot* on the scene, set up the parameters located in the *Geodetic Pivot* section (*[Parameters](../../../editor2/node_parameters/index.md)* window -> *Node* tab).


![](settings.png)


- **Location settings**. The geodetic location on the Earth of the pivot point. It is specified by 3 components:

  - **Latitude** is the north�south position in degrees of a point on the Earth's surface. For example, Abu Dhabi city latitude is 24.4667. 0 value means equator, 90 value means the North Pole, -90 means the South Pole.
  - **Longitude** is the east-west position in degrees of a point on the Earth's surface. For example, Abu Dhabi city longitude is 54.3667. 0 value means a prime meridian (Greenwich). This field supports two ranges: from -180 to 180 and from 0 to 360.
  - **Altitude** is the height above sea level of a location. For example, Abu Dhabi city altitude is 27 meters.
  - **Flat** geopositioning mode of the *Geodetic Pivot*. This mode should be used, when it is necessary only to set node positions via geo coordinates (latitude, longitude, altitude) without curving the terrain, clouds, etc.
- **Ellipsoid settings**.

  - **Reference** is a mathematically defined ellipsoid that approximates the surface of the planet. We offer popular geocentric reference ellipsoids: *WGS84, GRS80, Airy 1830*, etc.


## Working with Geodetic Pivot


After adding and setting up the *Geodetic Pivot*, you can simply add objects to "curve" them:


1. Choose the necessary nodes (*Static Mesh, Grass, Clutter*, etc.) in the *Nodes* window and set them as children of the *Geodetic Pivot*. ![](children.png)
2. Specify the necessary [settings](#settings) of the *Geodetic Pivot*.
3. The update will be performed automatically.


As you add a node as a child to the *Geodetic Pivot*, its geo position coordinates (latitude, longitude, and altitude) are displayed in the *[Geo](../../../editor2/node_parameters/geo/index.md)* section of the *Node* tab:


![](additional_node_parameters.png)


| Geo (Lat, Lon, Alt) | Specifies the geo position coordinates for the node (latitude, longitude, and altitude). |
|---|---|
| By default only the following objects are curved by the *Geodetic Pivot*: - Global Terrain (*ObjectTerrainGlobal*) - Global Water (*ObjectWaterGlobal*) - Cloud Layers (*ObjectCloudLayer*) As for *[Static Meshes](../../../objects/objects/mesh/index.md), [Mesh Decals](../../../objects/decals/mesh/index.md), and [Billboards](../../../objects/objects/billboards/index.md)*, sometimes you might just want to set their positions in real world coordinates an leave their geometry as is, but in some cases they should be curved (e.g., large static meshes, or roads represented as mesh decals). For this purpose you should use the following button: |  |
| Make Curved | Curves the geometry of the object according to the specified settings. A curved clone of the initial node is created, the initial node (using a non-curved mesh) is simply disabled, so you can use it when you need to return geometry back to normal (uncurved) state. |


> **Notice:** The button described above is available only for *[Static Mesh](../../../objects/objects/mesh/index.md), [Mesh Decal](../../../objects/decals/mesh/index.md)*, and *[Billboards](../../../objects/objects/billboards/index.md)* objects, when they are added as children to the *Geodetic Pivot*.
