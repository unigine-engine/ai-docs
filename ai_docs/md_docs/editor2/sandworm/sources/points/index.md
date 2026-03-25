# Point Object Parameters


Houses, landmarks, and other such objects are placed at specific points of the terrain. The object is placed at the position specified by the point and oriented the same way as when saved to a `*.node` file.


![](../../workflow/points/example.jpg)


An example of setting points is given [here](../../../../editor2/sandworm/workflow/points/index.md).


The object location and details are retrieved from vector data sources (`*.shp` and `*.geojson` assets).


Filter settings are described [here](../../../../editor2/sandworm/sources/index.md#filters).


## Parameters


![](point_parameters.png)


| Node | The path to the [primary object](../../../../editor2/sandworm/workflow/points/index.md#create_primary_object)'s `*.node` file. The process of creating an object is described [here](../../../../editor2/sandworm/workflow/points/index.md#create_primary_object). > **Notice:** Intersections should be enabled for any type of the primary object. |
|---|---|
| Collider | Flag indicating if collisions for the generated object are to be detected. > **Notice:** Available only for geometry type. |
| Drop To Ground | Flag indicating if the generated object will be aligned with the terrain surface. |
| Height Offset (m) | Distance from the terrain surface along the **Z**-axis, in meters. > **Notice:** If you see the generated object partially, You can try to increase this value to lift it above the terrain surface. |
| Bake To Cluster | If enabled, bakes generated point objects to *[Mesh Cluster](../../../../objects/objects/mesh_cluster/index.md)*. If disabled, generated objects are added to the world hierarchy as *[NodeReference](../../../../objects/nodes/reference/index.md)* objects. |
| Forward Axis | Axis which determines the orientation of the primary object: X, -X, Y, -Y. |
