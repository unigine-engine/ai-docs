# Refraction Raymarched Node


![](../img/refraction_raymarched.png)

### Description

Provides simulation of refractive material features using screen-space ray marching. Can be used for materials like glass, water, ice, or other transparent and translucent surfaces. You can find usage examples for this node in the [Glass](../../../../../content/materials/graph/samples/glass/index.md) material graph sample (see [Blended Refractive Material for Thick Glass](../../../../../content/materials/graph/samples/glass/index.md#blend_refraction_thick) and [Blended Refractive Material for Thin Glass](../../../../../content/materials/graph/samples/glass/index.md#blend_refraction_thin))


#### Ports

| Name | Description |  |
|---|---|---|
| ![](../img/types/float.png) | **Step Size** | Defines the texture sampling step; controls the precision of ray marching (smaller values result in higher accuracy). |
| ![](../img/types/float.png) | **Translucence Roughness** | Adjusts light scattering inside the material (0 = clear, higher = blurrier). |
| ![](../img/types/float.png) | **Last Step Size** | Sampling step used in the final phase of ray marching, helping to improve precision near intersections with scene geometry. |
| ![](../img/types/float.png) | **IOR** | Defines how much light bends when passing through the material (Index of Refraction). |
| ![](../img/types/float3.png) | **Normal Tangent Space** | Tangent-space surface normals used to distort the refraction effect across the material. |
| ![](../img/types/float3.png) | **Position View Space** | Position of the fragment in *View* space (relative to the camera). Used as the ray origin for screen-space refraction. |
| ![](../img/types/float3.png) | **Emission** | Outputs the refracted scene color. This result should be connected to the Emission input of the Material node to display the distorted background as seen through the refractive surface. |
| ![](../img/types/float.png) | **Ray Distance** | Distance traveled by the refracted ray from its origin to the point of intersection. |
| ![](../img/types/float2.png) | **Intersection Screen UV** | Screen-space UV coordinates at the intersection point between the refracted ray and the background. |
| ![](../img/types/float2.png) | **Refraction Screen UV Offset** | Offset applied to screen-space UVs due to refraction. Can be used to create distortion effects. |
