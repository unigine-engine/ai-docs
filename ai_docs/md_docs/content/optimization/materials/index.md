# Materials Optimization


Materials optimization can give you more flexibility in balancing the quality of the rendered scene with the performance of the application.


You can use different texture resolutions or create different implementations inside a graph-based material for different quality levels and use the corresponding one when necessary.


The quality level of materials is set globally via the **[Materials Quality](../../../editor2/settings/render_settings/materials_quality/index.md)** section of the *Settings* window. You can choose between the *Low, Medium*, and *High* levels.


![](materials_quality_settings.png)


## Creating Materials for Different Quality Levels


The Material Nodes library provides the **[Material Quality Switcher](../../../content/materials/graph/node_library/misc/material_quality_switch.md)** node that allows switching between different implementations of the same material depending on the current quality level. You can use this node for materials optimization as follows:


1. Create three implementations of the material, one for each quality level.
2. Add the **Material Quality Switcher** node to the material graph.
3. Connect each material implementation to the corresponding port - *Low, Medium*, and *High*.


As a result, different versions of the material will be generated automatically. Each version will be used for the corresponding quality level selected globally.
