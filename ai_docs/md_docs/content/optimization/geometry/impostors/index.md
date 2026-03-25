# Using Impostors


When the scene contains a lot of objects that should be visible at large distances, the application performance suffers. To reduce the number of such objects, *impostors* are used. They allow speeding up geometry rendering while saving visual fidelity: each impostor repeats transformation and appearance of the original object.


UNIGINE provides the *[Impostors Creator](../../../../editor2/tools/impostors_creator/index.md)* tool that allows generating impostors for a **single object** or for **objects baked into a *[Mesh Clutter](../../../../objects/objects/mesh_clutter/index.md)***.


For example, you can replace the distant trees with impostors to optimize forest rendering:


[![](impostors_sm.png)](impostors.png)

*Forest Optimized by Using Impostor Trees*


> **Notice:** Generating impostors is shown in the [Content Optimization](../../../../videotutorials/essentials/content_optimization.md) video tutorial, it is available both for a [single object](https://youtu.be/Iqsr3fEvnis?t=161) and for [objects baked into a *Mesh Cluster*](https://youtu.be/Iqsr3fEvnis?t=416).


## 1. Grabbing Impostors


> **Notice:** Grabbing of impostors is not supported for objects with transparent materials. E.g. if you have an object using a material with *Alpha Blend* preset enabled, the impostor generated for it will not be displayed.


To grab impostor with the *Impostors Creator* tool, perform the following:


1. In the Menu Bar, choose *Tools -> Impostors Creator*. The *Impostors Creator* tool will open. ![](creator_open.png)
2. In the *World Hierarchy* window, choose *a single mesh* or *a clutter*, for which an impostor should be created. > **Notice:** Impostors can be generated only for *[Mesh Clutter](../../../../objects/objects/mesh_clutter/index.md)* objects, *[World Clutter](../../../../objects/worlds/world_clutter/index.md)* isn't supported.
3. In the *Impostors Creator* window, specify the required [textures](../../../../editor2/tools/impostors_creator/index.md#textures) and [settings](../../../../editor2/tools/impostors_creator/index.md#texture_settings). We recommend selecting the *[**Octahedral**](../../../../editor2/tools/impostors_creator/index.md#impostor_type)* impostor type as a more advanced approach to creating impostors. > **Notice:** If you are going to generate the impostors for vegetation, you should specify **For Vegetation** option for textures (where available).
4. Click *Create* and specify a name for textures in the file dialog window that opens.


The generated impostor(s) will be added as a child node to the original mesh/clutter:


- For objects baked into the clutter, the [Mesh Clutter](../../../../objects/objects/mesh_clutter/index.md) object with the *[<node_name>_impostor_material](../../../../editor2/tools/impostors_creator/impostor_material.md)* will be added. All required settings will be copied from the original *Mesh Clutter* automatically. ![](clutter_impostor.png) | ![](clutter_impostors_0.png) | ![](clutter_impostors.png) | |---|---| | *Real Clutter Objects and Its Impostors in Scene* | *Objects and Impostors Wireframes* |
- For a single object, the *[Mesh Static](../../../../objects/objects/mesh/index.md)* object with the material inherited from *[<node_name>_impostor_material](../../../../editor2/tools/impostors_creator/impostor_material.md)* will be added. ![](mesh_impostor.png) | ![](single_object_impostor_0.png) | ![](single_object_impostor.png) | |---|---| | *Real Object (left) and Its Impostor (right) in Scene* | *Object and Impostor Wireframes* |


## 2. Setting Up Impostor Material


All textures specified in the *Impostors Creator* are generated in the `data` folder and applied in the material automatically. The impostor material may require additional set up:


- If you grab only the ***[Albedo](../../../../editor2/tools/impostors_creator/index.md#albedo)*** and ***[Normal](../../../../editor2/tools/impostors_creator/index.md#normal)*** textures, you will have to manually set up the other shading parameters of the impostor material (*Specular, Translucence*, etc.), so that the impostor visually match the original object. However, if the original object has several surfaces with different shading, the impostors may significantly differ (so it is better to grab all textures in this case).
- For vegetation impostors, the **Specular** parameter should be set to 0 to avoid unnecessary specks on trees.
- If you simply want to improve visual representation of impostors, you can adjust shading parameters (for example, increase *Translucence* for trees impostors and so on).
