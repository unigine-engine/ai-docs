# Spline Object Parameters


Spline object settings allow placing the selected node at the position specified by the first point, while the second point determines the orientation of the object's forward direction vector (positive **Y**).


![](../../workflow/lines/example_fence.jpg)


An example of setting lines is given [here](../../../../editor2/sandworm/workflow/lines/index.md).


The object location and details are retrieved from vector data sources (`*.shp` and `*.geojson` assets).


Filter settings are described [here](../../../../editor2/sandworm/sources/index.md#filters).


## Parameters


![](spline_parameters.png)


| Node | The path to the primary object's `*.node` file that contains either [billboards](../../../../editor2/sandworm/workflow/lines/index.md#create_billboards) or [mesh](../../../../editor2/sandworm/workflow/lines/index.md#create_fence). Other parameters are available depending on the primary object type. > **Notice:** Intersections should be enabled for any type of the primary object. |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|
| Autosize | Autosizing for lengthy objects such as fences and pipes. If enabled, basic objects are stretched and placed with zero-spacing so that bounding boxes of the first and the last basic objects are aligned with start and end points of the line segment respectively. ![](vector_placement.jpg) Disabling this option makes the following parameters available: \| Step \| Distance between two adjacent basic objects, in units. \| \|---\|---\| \| Start offset \| Offset of the first basic object's pivot from the start point of the line segment, in units. \| \| End offset \| Offset of the last basic object's pivot from the end point of the line segment, in units. \| \| Fit to size \| Enables stretching/shrinking of basic objects so that they are placed along line segments without spaces between them. \| | Step | Distance between two adjacent basic objects, in units. | Start offset | Offset of the first basic object's pivot from the start point of the line segment, in units. | End offset | Offset of the last basic object's pivot from the end point of the line segment, in units. | Fit to size | Enables stretching/shrinking of basic objects so that they are placed along line segments without spaces between them. |
| Step | Distance between two adjacent basic objects, in units. |  |  |  |  |  |  |  |  |
| Start offset | Offset of the first basic object's pivot from the start point of the line segment, in units. |  |  |  |  |  |  |  |  |
| End offset | Offset of the last basic object's pivot from the end point of the line segment, in units. |  |  |  |  |  |  |  |  |
| Fit to size | Enables stretching/shrinking of basic objects so that they are placed along line segments without spaces between them. |  |  |  |  |  |  |  |  |
| Skew | If enabled, each mesh in the Mesh Cluster is aligned to the terrain relief. ![](skew_off.png) ![](skew_on.png) |  |  |  |  |  |  |  |  |
| Collider | Flag indicating if collisions for the generated object are to be detected. > **Notice:** Available only for geometry type. |  |  |  |  |  |  |  |  |
| Drop To Ground | Flag indicating if the generated object will be aligned with the terrain surface. |  |  |  |  |  |  |  |  |
| Height Offset (m) | Distance from the terrain surface along the **Z**-axis, in meters. > **Notice:** If you see the generated object partially, You can try to increase this value to lift it above the terrain surface. |  |  |  |  |  |  |  |  |
| Bake To Cluster | If enabled, bakes generated point objects to *[Mesh Cluster](../../../../objects/objects/mesh_cluster/index.md)*. If disabled, generated objects are added to the world hierarchy as *[NodeReference](../../../../objects/nodes/reference/index.md)* objects. |  |  |  |  |  |  |  |  |
| Split Length (km) | This parameter is required to control the number of objects (either Billboards or Mesh Clusters, depending on the primary object) to be generated due to area splitting: - *Low* values will increase the number of generated objects. - *High* values will reduce this number. Too many generated objects may reduce performance. |  |  |  |  |  |  |  |  |
| Max Visibility (km) | Maximum visibility distance at which the generated clusters are no longer fully visible: they can either disappear completely or start to fade out depending on the Max Fade distance. |  |  |  |  |  |  |  |  |
| Max Fade (km) | Distance in units within which cluster meshes gradually disappear. Meshes outside this range are completely invisible. |  |  |  |  |  |  |  |  |
| Forward Axis | Axis which determines the orientation of the primary object: X, -X, Y, -Y. |  |  |  |  |  |  |  |  |
