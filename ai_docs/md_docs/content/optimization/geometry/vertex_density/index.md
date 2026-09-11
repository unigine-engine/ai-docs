# Optimizing Vertex Density


![](vertex_density.png)


A model with an excessive vertex count doesn't necessarily produce better visual quality, and it certainly doesn't help performance - beyond a certain point, extra vertices only increase rendering cost without delivering a visible improvement. Yet every vertex in a scene adds computational cost. **Excessive vertex density** (whether from over-tessellated models, inefficient *[LODs](../../../../principles/world_management/index.md#lods)* that barely reduce complexity, or hidden geometry) increases GPU load, memory usage, and **slows down frame rendering**.


## Tool Overview


**Vertex Density visualizer** helps diagnose these issues quickly. It is ideal for **optimizing LODs, high-poly meshes created in digital sculpting tools, and geometry imported from external tools** to maintain a balanced topology. It displays a heatmap of vertex concentration directly in the viewport, making it easy to spot areas where geometry can be simplified or reorganized for better performance and efficiency.


> **Notice:** Vertex Density visualizer tool is only available for ***Development* and *Debug* builds** of the Engine: not compiled for *Release* builds.


To open the **Vertex Density**visualizer choose *Rendering Debug -> Vertex Density* on the *[Rendering Debug](../../../../editor2/rendering_debug/index.md)* *Panel* of UnigineEditor.


![](render_debug_tool.png)


The *Vertex Density* visualizer window will open:


![](vertex_density_dt_tool.png)


| **Visualizer Mode** | Defines how vertex density information is displayed in the viewport. Available modes: - **Discrete Threshold** - Highlights only the areas where the vertex density exceeds the specified *[Vertex Density Threshold](#threshold)* value within the defined *[Searching Area](#search_area)*. - **Gradient** - Displays a color gradient representing vertex density from black (0) up to the specified *[Vertex Density Threshold](#threshold)* within the defined *[Searching Area](#search_area)*. Areas exceeding the threshold appear white. |
|---|---|
| **Front Side Only** | Enables depth testing so that only visible (not occluded) vertices in the current viewport are visualized. |
| **Visualizer Opacity** | Controls the opacity of the vertex density overlay. |
| **Searching Area in pixels** | Specifies the screen grid cell size used for vertex density sampling, in pixels (8 by default). Vertex density value is calculated and displayed for each cell of the screen area. |
| **Vertex Density Threshold** | Defines the maximum acceptable vertex density within a single grid cell (100 by default). |


## Using the Tool


Instead of guessing which models are too dense, you can now see exactly where the geometry is overspending vertices and how severely. The tool divides the rendered image into a grid and measures vertex density within each cell. Each cell is color-coded according to how many vertices fall inside its area:


- **Black areas** indicate low vertex density.
- **White** (or **red** in *Discrete Threshold* mode) cells highlight dense regions that exceed the *[Vertex Density Threshold](#threshold)* you define.


![](vertex_density_dt.png) ![](vertex_density_gr.png)


By adjusting parameters such as *[Searching Area](#search_area)* and *[Vertex Density Threshold](#threshold)*, you can analyze your scene at different scales. The *Front Side Only* option enables depth testing, so the visualizer considers only visible geometry.


A few white or red cells localized on small, detailed parts of a model such as facial features or curved shapes may be acceptable, but if large portions of a mesh glows in white, or distant LODs show the same density as close-up geometry, that's a clear sign of wasted detail.


At this point, the visualizer gives you a roadmap of where to optimize.


**Typical issues** include:


- **Inefficient LODs** that do not meaningfully reduce vertex count.
- **Overly complex meshes** for background or occluded areas.
- **Unnecessarily high tessellation** on flat surfaces.
- **Duplicate or internal faces** that will never be visible.


## Recommended Workflow


1. Enable the *Vertex Density* visualizer tool via the *Rendering Debug Panel*.
2. Start with a small grid size (for example, 4x4 pixels) to reveal fine detail. Larger cell sizes, such as 8 or 16 pixels, are useful for scanning broad surfaces or distant geometry.
3. Focus first on the geometry that's actually visible in camera. Use *Front Side Only* mode for this.
4. Use *Discrete Threshold* mode to highlight problem areas that exceed your density limit. You'll instantly see where vertex clustering is heaviest. Then switch to *Gradient* mode to get a smoother visualization of how density changes across a surface.
5. When a region looks suspicious, enable wireframe rendering under *Helpers -> Wireframe Mode*:

  - *Front Geometry Occluded* shows visible geometry with depth testing.
  - *Front Always On Top* and *Front and Back Always On Top* reveal all faces, including hidden or back-facing surfaces.


### Optimization Options


Simplify meshes where density is excessive, starting with these techniques:


- **Simplify LODs.** Ensure each LOD reduces vertex count significantly. A 5-10x reduction from LOD0 to LOD3 is typical for large objects.
- **Retopologize or decimate high-density regions**, especially flat areas where extra vertices add no visual value.
- **Remove internal geometry.** Faces inside closed meshes, hidden cavity surfaces, and unused structural detail.
- **Bake high-frequency detail** into normal or height maps instead of keeping it in geometry.
- **Merge small static meshes** that always render together, reducing draw calls and vertex processing overhead.
- **Adjust vertex attributes.** Remove unused UV sets, tangents, or vertex colors. Use compact formats (e.g., half precision) when possible.
- **Use impostors or billboards** for distant repeating geometry like trees or props.


## See Also


- *[Vertex Density visualizer API Reference](../../../../api/library/rendering/class.render_cpp.md#setShowVertexDensityBlend_float_void)*
- *[Vertex Density visualizer console commands](../../../../code/console/index.md#vertex_density_debug)*
- Quick video guide: *[How To Analyze Scene Content Using Vertex Density Visualizer](../../../../videotutorials/how_to/how_to_rendering/vertex_visualizer.md)*.
