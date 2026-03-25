# Rendering

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


## Gaussian Splatting Visualization

![](gaussian.gif)

This sample illustrates how to render 3D Gaussian splatting scenes in UNIGINE using the *[GaussianSplatting](../../../code/plugins/gaussian/index.md)* plugin.


The sample 3DGS Scene contains a node used as 3DGS scene's origin (*Node Dummy*) with the **gaussian** property assigned onto it. This property is a part of the *GaussianSplatting* plugin, and it is used to specify the path to the required 3DGS `*.ply` file.


The property also contains parameters available for adjustment, such as spherical harmonics degree and render order for the 3DGS scenes.


In addition, you can adjust the parameters of the **gaussian_render** material to tune the look of Gaussian splats.


> **Notice:** To render Gaussian splats both at runtime and in the Editor, the *UnigineGaussianSplatting* engine plugin must be loaded successfully, with no errors shown in the console.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/gaussian_splatting_visualization*
