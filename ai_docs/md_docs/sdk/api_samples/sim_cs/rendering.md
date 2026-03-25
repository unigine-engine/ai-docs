# Rendering

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


## Airfield Ground Lighting

![](../../../samples/img/csharp_sim_samples_airfield_ground_lighting.jpg)

The sample demonstrates how to create performance-friendly *[Billboards](../../../objects/objects/billboards/index.md)*-based lights for airports and airfields instead of using real light sources.


For a detailed guide on the creation process, see the **[Lights Optimization](../../../content/optimization/lights/index.md#billboards)** article.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_sim_samples/rendering/airfield_ground_lighting*
## Cross Section Visualization

![](../../../samples/img/csharp_sim_samples_cross_section_visualization.jpg)

This content sample demonstrates rendering of cross sections using the *[Cross Section](../../../content/materials/library/mesh_base/index.md#option_cross_section)* option of the **mesh_base** material.


A cross-section of the object is created by the near clipping plane of the camera (player) viewing frustum that cuts this object. If the camera's near clipping plane is oblique, you can change its obliqueness and, therefore, change transformation of the cross-section. Enabling the *Cap Holes* checkbox fills the cross-section holes using the colors configured in the material parameters.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_sim_samples/rendering/cross_section_visualization*
