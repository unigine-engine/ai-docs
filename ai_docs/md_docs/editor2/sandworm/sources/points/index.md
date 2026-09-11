# Point Object Parameters


Houses, landmarks, and other such objects are placed at specific points of the terrain. A point object is placed at the position given by the source feature; its orientation comes either from the `*.node` file it was saved with or from the source data.


![](../../workflow/points/example.jpg)


An example of setting points is given [here](../../../../editor2/sandworm/workflow/points/index.md).


What a generated object gets depends on the geometry type of the feature it is created from:


- **Point** � the position only. The object keeps the orientation it had when it was saved to the `*.node` file.
- **LineString** � the position and the orientation. An object is placed at a coordinate and turned so that its [Forward Axis](#forward_axis) is aimed at the coordinate that follows it. Only the direction between the two matters, the distance between them does not.


In a `*.geojson` source a feature that sets the position only looks as follows:


```text
"geometry": {
	"type": "Point",
	"coordinates": [37.617635, 55.755814]
}

```


And the same feature with the orientation defined:


```text
"geometry": {
	"type": "LineString",
	"coordinates": [
		[37.617635, 55.755814],
		[37.617635, 55.755903831]
	]
}

```


In this example the second coordinate has the same longitude and a greater latitude, so the generated object is turned to face north.


> **Notice:** A **LineString** is not limited to two coordinates. If the string contains N coordinates, it produces N-1 objects: every coordinate except the last one gets an object aimed at the coordinate that follows it, while the last one only supplies the direction for the object before it. A polyline therefore places a chain of objects, each facing the next.


The object location and details are retrieved from vector data sources (`*.shp` and `*.geojson` assets).


Filter settings are described [here](../../../../editor2/sandworm/sources/index.md#filters).


## Parameters


![](point_parameters.png)


| Node | The path to the [primary object](../../../../editor2/sandworm/workflow/points/index.md#create_primary_object)'s `*.node` file. The process of creating an object is described [here](../../../../editor2/sandworm/workflow/points/index.md#create_primary_object). > **Notice:** Intersections should be enabled for any type of the primary object. |
|---|---|
| Collider | Flag indicating if collisions for the generated object are to be detected. > **Notice:** Available only for geometry type. |
| Drop To Ground | Flag indicating if the generated object will be aligned with the terrain surface. |
| Height Offset (m) | Distance from the terrain surface along the **Z**-axis, in meters. > **Notice:** If the generated object is only partly visible, try increasing this value to lift it above the terrain surface. |
| Bake To Cluster | If enabled, bakes generated point objects to *[Mesh Cluster](../../../../objects/objects/mesh_cluster/index.md)*. If disabled, generated objects are added to the world hierarchy as *[Node Reference](../../../../objects/nodes/reference/index.md)* objects. The parameter is not available for a *[Billboards](../../../../objects/objects/billboards/index.md)* node. |
| Forward AXIS | Axis which determines the orientation of the primary object: X, -X, Y, -Y. |
