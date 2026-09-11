# Occluder


**Occluder** is an object that is used to cull surfaces of objects whose bounds are not visible behind it.


> **Notice:** - *[Mesh Clutter](../../../objects/objects/mesh_clutter/index.md)* cannot be culled by an *Occluder*.
> - *Occluder* culls objects conservatively (it hides only the objects that are definitely hidden by the occluder).
> - Precision of occluders depends on their [resolution](../../../code/console/index.md#render_occluders_resolution). If the *Occluder*'s resolution is insufficient, the culled object may become visible.
> - Objects are culled based on their bounds, more precisely [simplified screen projections](../../../objects/worlds/world_occluders/occluder_object/index.md) based on their bound boxes. These projections are **affected by the camera FOV and viewing angle**.


*Occluders* can be highly effective in case of complex environments where there are many objects that occlude each other and are costly to render (they have a lot of polygons and/or heavy shaders).


However, effective culling is possible only if objects are not too large. If objects are big and have several surfaces, it is likely that an additional performance load of an *Occluder* will not pay off.


> **Warning:** - Occluders are only **effective for ground-based viewer scenarios** where the camera always remains somewhere near the ground level and does not rise above the objects intended to be culled using occluders.
> - If a scene contains **a lot of flat objects or the camera views the scene from above** (as in flight simulators), it's better to **avoid using *Occluder* nodes**, or disable them.


*Occluder* is **rendered by the CPU** and stored in a separate buffer (there are **no per-pixel depth tests or GPU occlusion queries for them**). Only the *Occluder* nodes currently displayed in the viewport are rendered to the buffer.


To display the buffer, you can check the corresponding option in Editor settings (*Settings -> Render -> Occlusion Culling*), or do it via the `render_show_occluder` console command:


```bash
render_show_occluder 1
```


The buffer will open in the upper left corner:


![](occluder_buffer.png)

*SimplifiedOccluderthat is stored in the buffer*


> **Notice:** The buffer is rendered in a low [resolution](../../../editor2/settings/render_settings/occlusion_culling/index.md#occluders).


### Types of Occluder


There are two types of *Occluders*:


- ![](occluder.png)**� [Occluder](../../../objects/worlds/world_occluders/occluder_object/index.md)** � a simple cuboid shaped *Occluder*
- ![](occluder.png)**� [Occluder Mesh](../../../objects/worlds/world_occluders/occluder_mesh/index.md)** � *Occluder* based on an arbitrary `.mesh` file
