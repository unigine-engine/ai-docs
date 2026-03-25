# Analyzing Quad Overdraw


![](quad_overdraw.png)


Imagine painting a detailed landscape, only to completely cover it with a dense fog layer. All that time spent on invisible details was wasted. This exact scenario happens constantly in 3D rendering when the same screen pixels are drawn multiple times - a phenomenon known as **Quad Overdraw**.


Modern GPUs process pixels in 2x2 blocks called **quads**, which leads to two main efficiency problems:


- **True Overdraw** - multiple transparent surfaces (like glass, particles, or foliage) overlap, forcing the GPU to shade and blend the same pixel repeatedly.
- **Overshading** - small or thin triangles occupy only part of a quad. The GPU still shades all four pixels, only to discard those that fall outside the triangle - like paying for a table for four while dining alone.


Additional overdraw also comes from materials that use multiple passes (lighting, emission, ambient, auxiliary, etc.), since each pass shades the same pixels again. Altogether, this **results in wasted GPU cycles, lower frame rates, and higher hardware requirements to achieve the same visual quality**.


## Tool Overview


To detect such hotspots in UnigineEditor, enable the **Quad Overdraw debug visualizer**. It highlights areas with excessive shading and helps identify which assets, materials, or scene elements need optimization. According to the selected visualizer mode the tool displays different results for each situation, depending on material type, number of its passes, additional Depth Pre-Pass rendering optimization and other settings.


> **Notice:** *Quad Overdraw* visualizer tool is only available for **Development and Debug builds** of the Engine: not compiled for *Release* builds.


To open the **Quad Overdraw**visualizer choose *Rendering Debug -> Quad Overdraw* on the  *Panel* of UnigineEditor.


![](render_debug_tool.png)


The *Quad Overdraw* visualizer window will open:


![](quad_overdraw_tool.png)


| **Passes** | Defines which rendering passes are included in the overdraw calculation. Available modes: - **All Passes with Depth Pre Pass** - displays the total number of overdraws, including all passes such as Auxiliary, Emission, Ambient, Light, and others if they are rendered. This mode also counts overdraw from depth pre-passes, whether enabled globally (via *[render_depth_pre_pass](../../../../code/console/index.md#render_depth_pre_pass)* console command) or forced on specific materials (*[Depth Pre Pass](../../../../principles/render/sequence/index.md#depth_pre_pass)* material option). - **Single Geometry Pass with Depth Pre-Pass** - displays the number of overdraws for the primary rendering pass of the content after applying the depth pre-pass. Separate passes (such as auxiliary or lighting) are not counted in this mode; it accounts only for the first draw call of the given object. - **Single Geometry Pass without Depth Pre-Pass** - displays the number of content overdraws without using depth pre-pass (before any early depth rejection is applied). |
|---|---|
| **Visualizer Mode** | *Quad Overdraw* visualizer display mode. Available modes: - **Discrete Threshold** - Highlights only the areas where the overdraw exceeds the specified threshold. ![](quad_overdraw_modes_dt.gif) - **Gradient** - Displays a color gradient representing overdraw intensity from black (0) to white (*[Quad Overdraw Threshold](#quad_overdraw_threshold)*). ![](quad_overdraw_modes.gif) |
| **Quad Overdraw Wireframe** | Enables rendering of *Quad Overdraw* wireframe overlay for all objects in the viewport according to the selected visualizer options. |
| **Show Landscape Terrain** | Toggles displaying of *Quad Overdraw* for the *[Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md)* object as well. |
| **Show Water Global** | Toggles displaying of *Quad Overdraw* for the *[Water Global](../../../../objects/objects/water/water_object.md)* object as well. |
| **Visualizer Opacity** | Quad Overdraw visualizer overlay opacity. |
| **Quad Overdraw Threshold** | Overdraw threshold used to highlight areas exceeding this value. |
| **Quad Overdraw** | Heatmap color scale showing Quad Overdraw intensity up to the *[Quad Overdraw Threshold](#quad_overdraw_threshold)*. |


## Recommended Workflow


1. **Enable the *Quad Overdraw* visualizer** tool via the *Rendering Debug Panel*.
2. **Start with the Big Picture** - use the *All Passes with Depth Pre Pass* visualizer mode to locate hotspots. Bright white (or red in *Discrete Threshold* mode) areas indicate the maximum number of redraws (depending on the set *Quad Overdraw Threshold* value). These areas are your primary optimization targets.
3. **Isolate the Core Issue** - switch between *Single Geometry Pass with/without Depth Pre Pass* modes. A significant reduction in overdraw across your scene when Depth Pre-Pass is enabled suggests that many opaque objects can benefit from early depth rejection. If the difference is small, the extra cost of a pre-pass may not be worth it, instead - focus on simplifying geometry, reducing transparency overlap, or forcing pre-pass only on specific complex materials.
4. **Classify the Culprits** - use the visualizer's filters and overlays to identify specific problem sources:

  - **Wireframe** overlay reveals dense geometry.
  - **Landscape Terrain/Water Global** toggles isolate system-specific overdraw.
  - **Discrete Threshold** mode only focuses on areas exceeding acceptable limits.


## Common Patterns and Solutions


- **Transparent Objects** (Particles, Glass, UI) are the most common offenders. Try to minimize overlap by baking multiple layers into a single texture, reducing particle count or using distance-based fading. If visual quality allows, switch to cheaper blending modes (for example, additive instead of alpha blend), or opaque materials. In large scenes, use *[LODs](../../../../content/optimization/geometry/lods/index.md)* or *[impostor](../../../../editor2/tools/impostors_creator/index.md)* transitions for distant transparency layers.
- **Complex Geometry** often contributes to overshading even when fully opaque. Very small triangles cause GPUs to process more pixels per quad than needed. Simplify meshes, merge small parts, and tune LODs so that distant or minor details use lower complexity or impostor models.
- **Multi-Pass Materials** multiply shading cost. Review whether *[auxiliary](../../../../principles/render/sequence/index.md#auxiliary)* or *[emission](../../../../principles/render/sequence/index.md#emission)* passes are really needed and combine them into a single shader where possible, or bake effects into textures.
- **For alpha-tested materials** (like foliage), minimize overlapping transparent areas. Rendering many overlapping alpha-tested surfaces is inefficient, since transparent pixels are still shaded and then discarded by the alpha test. Whenever possible, increase the opaque coverage of the texture or trim geometry. Fading out opacity beyond a certain distance can also be effective.
- **Enable *[Occlusion Culling](../../../../content/optimization/geometry/culling/index.md)*** (use occluders or hardware occlusion queries) if your scene contains many occluded objects. It prevents invisible nodes from being drawn at all, significantly reducing GPU workload before shading even begins.
- **When depth pre-pass is used**, balance its benefits against the extra cost of an additional geometry pass. Enable it globally (*[render_depth_pre_pass](../../../../code/console/index.md#render_depth_pre_pass)*) if the majority of the scene consists of opaque objects with high overdraw potential, or selectively per material (the *[Depth Pre Pass](../../../../principles/render/sequence/index.md#depth_pre_pass)* material option) for complex or expensive shaders.


Remember: The goal isn't eliminating overdraw entirely, but reducing it to levels your target hardware can handle efficiently. The *Quad Overdraw* visualizer tool provides the data - your judgment determines the right balance between visual quality and performance.


## See Also


*[Quad Overdraw visualizer API Reference](../../../../api/library/rendering/class.render_cpp.md#setShowQuadOverdrawBlend_float_void)*


*[Quad Overdraw visualizer console commands](../../../../code/console/index.md#overdraw_debug)*
