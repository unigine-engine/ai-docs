# Occlusion Culling


This section contains settings related to [occlusion culling](../../../../content/optimization/geometry/culling/index.md).


![Occlusion culling settings](occlusion.png)

*Occlusion Culling Settings*


| Occlusion Query | The value indicating if additional hardware occlusion query test before sending data to GPU is enabled. This test is performed for all objects with the *[Culled by occlusion query](../../../../editor2/node_parameters/transformation_common/index.md#query)* flag set. **enabled** by default. `Console access:render_occlusion_queries` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_occlusion_queries)) |
|---|---|
| Frames | The number of frames for additional hardware occlusion query test performed before sending data to GPU. Make sure that the additional hardware occlusion query test*[OcclusionQueries](#render_occlusion_queries)* is enabled. Range of values: **[0, 1024]**. The default value is : **5**. `Console access:render_occlusion_queries_num_frames` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_occlusion_queries_num_frames)) |


### Occluders


| Occluders | The value indicating if rendering of occluders is enabled. **enabled** by default. `Console access:render_occluders` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_occluders)) |
|---|---|
| Resolution | The resolution of the texture, to which occluders*[Occluders](#render_occluders)* are rendered. From **1x1** to **1024x1024** Default: **128x64** `Console access:render_occluders_resolution` ([API control](../../../../api/library/rendering/class.render_cpp.md#render_occluders_resolution)) |
