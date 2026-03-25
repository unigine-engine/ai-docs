# Setting Up LODs


Using [Levels of Details](../../../../principles/world_management/index.md#lods) (LODs) is the main way to optimize your project. The point is to switch the high detailed mesh to a mesh with lower number of details when the mesh is far from camera. For that, you need to take your detailed model and create several versions of it, each with lower polygon count.


In UNIGINE, a model with LODs can be represented as a single Mesh object with a number of [surfaces](../../../../principles/world_structure/index.md#surfaces) representing LODs. LODs settings allow you to specify the distance when a surface should be switched to another.


LODs can be configured in one of the following ways:


- [Automatically](#automatic) when importing the model into UNIGINE.
- [Manually](#manual) by means of a 3D editor and UnigineEditor.


### See Also


- The [Levels of Details](../../../../principles/world_management/index.md#lods) section of the article on World Management
- The [Surfaces](../../../../editor2/assets_optimize/content_profiler/surface_profiler.md) tab of the [Content Profiler](../../../../editor2/assets_optimize/content_profiler/index.md) tool to monitor surface LODs by toggling Min/Max Visibility and Min/Max Fade filters


## Automatic LODs Setting


Automatic LODs setting implies that LODs for the model are assigned and configured on its importing into UNIGINE.


> **Notice:** Automatic LODs setting can be found in the [![](../../youtube_link.png)Content Optimization](https://youtu.be/Iqsr3fEvnis?t=109) video tutorial and the [dedicated quick guide](../../../../videotutorials/how_to/how_to_basics/configure_lods.md).


When importing the model, you can choose one of the following options:


- **Automatically generate** LODs by UNIGINE. In this case, you only need your high-poly model - the Engine will do the rest.
- Use the **name postfixes** to specify LODs. In this case, you should previously prepare different meshes for different LODs of your model in a third-party software.


### Generating LODs Automatically


UNIGINE enables you to automatically generate LODs for your high-poly model right when importing it, saving you a lot of time cause now you don't have to prepare levels of detail manually in some third-party software. The feature is based on the *[meshoptimizer](https://github.com/zeux/meshoptimizer)* library.


To automatically generate LODs on importing the model into UNIGINE, simply drag it to the *[Asset Browser](../../../../editor2/assets_workflow/index.md#asset_browser)* and perform the following:


1. In the import settings window, choose *[Auto-Generated](../../../../editor2/fbx/index.md#lods_autogen)* in the **Use LODs** drop-down list. ![](auto_generate.png)
2. Set the required number of LODs. For example, we will generate 3 LODs.
3. Specify the *[Target Polycount (%)](../../../../editor2/fbx/index.md#fbx_lod_autogen_target_polycount)* value for each LOD. It defines the degree of geometry simplification for each LOD. ![](target_polycount.png)

  - For **LOD 0**, leave the default value of 100 percent.
  - For **LOD 1**, set the 60 percent of the original number of polygons.
  - For **LOD 2**, set the 30 percent of the original number of polygons.
4. Specify the minimum and maximum *[visibility](../../../../editor2/fbx/index.md#lod_autogen_visibility)* distances for each LOD. Maximum visibility distance of each LOD should be equal to the minimum visibility distance of the next LOD. Maximum visibility distance of the last LOD should be equal to inf. ![](auto_visibility_distance.png) ![](../../../../principles/world_management/lods_fade.png)

  - For **LOD 0**, leave the default *Min* distance and set the *Max* distance at 5 units. It means that no matter how close the camera comes to the mesh, the surfaces will still be visible.
  - For **LOD 1**, set the *Min* and *Max* distances at 5 and 30 units. It means that when the camera is 5 units away from the mesh, the first LOD surfaces won't be visible and the second LOD surfaces will be shown over the distance of 30 units.
  - For **LOD 2**, set the *Min* distance at 30 units and leave the default *Max* distance. After 30 units, the second LOD surfaces won't be visible and the third LOD surfaces will be shown.
5. Specify the minimum and maximum *[fade](../../../../editor2/fbx/index.md#lod_autogen_visibility)* distances for each LOD: ![](auto_fade_distance.png)

  - For **LOD 0**, leave the default *Min* distance and set the *Max* distance to 10 units. It will prolong the distance over which the LOD surfaces are still visible and provide smooth fading.
  - For **LOD 1**, set the *Min* distance to 10 units. After 5 up to 15 units, the second LOD surfaces will smoothly fade in. The *Max* distance set to 20 units. After 30 up to 50 units, the second LOD surfaces will smoothly fade out.
  - For **LOD 2**, set the *Min* distance to 20 units and leave the default *Max* distance. The third LOD surfaces will start to smoothly fade in from 30 to 50 units.
6. Leave the 0 value for the *[Normals Preserve](../../../../editor2/fbx/index.md#fbx_lod_autogen_normals_preserve)* option to ignore normals while simplifyign the mesh topology.
7. Leave the default 60 value for the *[Recalculate Normals by Angle](../../../../editor2/fbx/index.md#fbx_lod_autogen_recalc_normals)* option.


The Engine will generate and configure all LODs automatically using the specified settings.


### Combining LODs By Postfixes


If you prepare LODs in a third-party software, you can automatically assign and configure LODs of the model based on name postfixes.


#### Step 1. Export a Model From a Third-Party Software


As an example, we will use the `tubes_constructor_chrome_1120.fbx` model from the Oil Refinery demo (available in UNIGINE SDK Browser). This FBX consists of several meshes, each of which represents an element of the tubes constructor.


Perform the following in a 3D editor:


1. Create several meshes for different LODs of your model: a detailed mesh for the closest LOD and a number of less detailed meshes for farther LODs. > **Notice:** When naming the meshes, add a postfix to specify the LOD each mesh represents. For example: *_lod_0* for the 1st LOD, *_lod_1* for the 2nd LOD, etc. For example, for each mesh representing an element of the tubes constructor (10 meshes), there are 3 meshes representing LODs: ![](lods_naming.png)
2. [Export the meshes](../../../../editor2/assets_workflow/assets_create_import.md#export) as an `.fbx` file.


#### Step 2. Import Model to UNIGINE


To import the model into UNIGINE, drag and drop the previously exported FBX file to the *[Asset Browser](../../../../editor2/assets_workflow/index.md#asset_browser)* and perform the following to automatically create LODs based on the name postfixes:


1. Choose *[Combine By Postfixes](../../../../editor2/fbx/index.md#fbx_use_lods)* in the **Use LODs** drop-down list.
2. Specify the maximum number of LODs stored in the FBX container (in our case, 3).
3. For each LOD, define a postfix that will be used to group objects in an FBX file into a corresponding LOD. > **Notice:** The postfix must be the same as the one used when [creating objects in a 3D editor](#postfixes). For the tubes constructor model, the following postfixes should be specified: ![](combine_by_postfix.png) Names of generated surfaces will be as follows: *material_name + LOD_postfix*.
4. Specify the minimum and maximum visibility distances for each LOD. Maximum visibility distance of each LOD should be equal to the minimum visibility distance of the next LOD. Maximum visibility distance of the last LOD should be equal to inf. ![](combined_visibility.png) ![](../../../../principles/world_management/lods_fade.png)

  - For ***_lod_0***, leave the default *Min* distance and set the *Max* distance at 5 units. It means that no matter how close the camera comes to the mesh, the surfaces will still be visible.
  - For ***_lod_1***, set the *Min* and *Max* distances at 5 and 30 units. It means that when the camera is 5 units away from the mesh, the first LOD surfaces won't be visible and the second LOD surfaces will be shown over the distance of 30 units.
  - For ***_lod_2***, set the *Min* distance at 30 units and leave the default *Max* distance. After 30 units, the second LOD surfaces won't be visible and the third LOD surfaces will be shown.
5. Specify the minimum and maximum fade distances for each LOD: ![](combined_fade.png)

  - For ***_lod_0***, leave the default *Min* distance and set the *Max* distance to 10 units. It will prolong the distance over which the LOD surfaces are still visible and provide smooth fading.
  - For ***_lod_1***, set the *Min* distance to 10 units. After 5 up to 15 units, the second LOD surfaces will smoothly fade in. The *Max* distance set to 20 units. After 30 up to 50 units, the second LOD surfaces will smoothly fade out.
  - For ***_lod_2***, set the *Min* distance to 20 units and leave the default *Max* distance. The third LOD surfaces will start to smoothly fade in from 30 to 50 units.


In the result, the FBX container with 10 meshes will be imported. Each mesh will have 3 surfaces representing LODs.


![](auto_imported_meshes.png)

*Meshes of the Imported FBX*


> **Notice:** When working with large scenes, you cannot know for sure how many LODs some model will have. So, it is recommended to specify more LODs in the importer: in this case, you won't have to set up LODs manually, if the model contains more LODs than the previously imported one. For example, if you set up 10 LODs in the importer, you can import models with up to 10 LODs.


#### Step 3. Add Model to the World


Add an exported model into the world as [described here](../../../../editor2/fbx/index.md#add_fbx). All LODs will be already created and set up according to the specified import values:


![](auto_imported.png)

*Imported Tubes Constructor with LODs*


![](auto_imported_tubes.png)

*FBX Added to the World*


If required, adjust the LODs surfaces in the *Node* tab of the *Parameters* window:


- Configure the *[Min and Max Parent](../../../../principles/world_management/index.md#parents)* settings. In this tutorial, we use the default values of 1.


Try to move the camera forward/backward to check how LODs are switched:


![](lods_switching.gif)

*LODs Switching*


## Manual LODs Setting


Manual LODs setting implies that LODs for the model are created in a third-party 3D editor and LODs parameters are adjusted when the model is already imported and added to the scene.


> **Notice:** Manual LODs setting is also shown in the *[![](../../youtube_link.png)Content Optimization](https://youtu.be/Iqsr3fEvnis?t=38)* video tutorial.


### Step 1. Export LODs


To export the mesh with LODs, do the following:


1. In your 3D editor, create a detailed model and a number of models with a low number of polygons. For example, you can just copy the existing detailed model and reduce the number of polygons. > **Notice:** You should create a separate LOD for each part of the model to which a unique material is assigned. As an example, we will use the model of an oscilloscope from Superposition benchmark (available via *UNIGINE SDK Browser*). This model already contains 3 LODs. ![](1_lods_3dsmax.jpg) | **10109 polygons** | **5004 polygons** | **2583 polygons** | |---|---|---| | [![](lod_0_sm.png)](lod_0.png) | [![](lod_1_sm.png)](lod_1.png) | [![](lod_2_sm.png)](lod_2.png) | | *LOD 0* | *LOD 1* | *LOD 2* |
2. Generate LODs according to a pipeline used by your 3D editor. For example, in 3ds Max, you should group meshes representing LODs and then create LODs via the *Level of Detail* utility.
3. Export the model with LODs as an `*.fbx` file.


### Step 2. Import Model to UNIGINE


To [import the model](../../../../videotutorials/essentials/importing_3d_models.md) into UNIGINE:


1. Click *Import* in the *[Asset Browser](../../../../editor2/assets_workflow/index.md#asset_browser)* and choose the exported FBX file.
2. In the *[Import FBX](../../../../editor2/fbx/index.md)* window, enable the *[Merge Static Meshes](../../../../editor2/fbx/index.md#fbx_merge_static_meshes)* option. Otherwise, LODs will be imported as separate meshes, not surfaces.
3. Import the model.


If you select the imported FBX, its content will be previewed in the *Hierarchy* section of the *Parameters* window.


![](2_surfaces.png)


### Step 3. Add a Model to the World


Add an exported model into the world as [described here](../../../../editor2/fbx/index.md#add_fbx). By default, all surfaces (LODs) are visible at the same time:


![](all_lods.png)

*Oscilloscope Model*


The surfaces of the exported model that represent LODs can be found in the *Node* tab of the *[Parameters](../../../../editor2/node_parameters/index.md)* window:


![](3_surfaces.png)


### Step 4. Set Up LODs


This section explains how to set up LODs of the mesh to smoothly switch a high detailed LOD to a low detailed when the camera begins to move away from the mesh. LOD surfaces have 3 parameters:


- [Parents](../../../../principles/world_management/index.md#parents)
- [Visibility distances](../../../../principles/world_management/index.md#visible)
- [Fade distance](../../../../principles/world_management/index.md#fading)


> **Notice:** The chapter contains the example values of the parameters. You can specify your own ones, if necessary.


#### Visibility and Fade Distances


For each LOD surface, you should specify a visibility distance and a fade distance. The following image illustrates these distances and how they work.


![](../../../../principles/world_management/lods_fade.png)


For setting up the LOD surfaces, do the following:


1. Open the [*World Hierarchy*](../../../../editor2/interface/index.md#world_hierarchy) window, and choose the added node.
2. In the *Surfaces* group of the *[Node](../../../../editor2/node_parameters/index.md)* tab (the *Parameters* window), choose **the first LOD surface**: ![](3_select_lods.png) ![](visibility_lod_0.png) > **Notice:** You can disable other LOD surfaces to see the result of the current LOD surface settings.

  - Set its *[Maximum Visibility](../../../../principles/world_management/index.md#max_visible)* distance to 5. It means that when the camera is 5 units away from mesh, the first LOD surfaces won't be visible.
  - Leave the *[Minimum Visibility](../../../../principles/world_management/index.md#min_visible)* distance at -inf. It means that no matter how close the camera comes to the mesh, the surfaces will still be visible.
  - Set the *[Maximum Fade](../../../../principles/world_management/index.md#max_fade)* distance to 10 units. It will extend the distance over which the LOD surfaces are still visible and provide smooth fading.
3. Choose the **second LOD** surfaces and: ![](visibility_lod_1.png)

  - Set the *[Minimum Visibility](../../../../principles/world_management/index.md#min_visible)* distance of the second LOD surfaces to start exactly where the *[Maximum Visible](../../../../principles/world_management/index.md#max_visible)* distance of the first LOD surfaces ends: at 5 units. It means that when the first LOD surfaces begin to fade out, the second LOD surfaces will be shown.
  - Set the *[Maximum Visibility](../../../../principles/world_management/index.md#max_visible)* distance at **30** units. After 30 units, the second LOD surfaces begin to fade out and the third LOD surfaces will be shown.
  - Set the *[Minimum Fade](../../../../principles/world_management/index.md#min_fade)* distance to 10 units. After 5 up to 15 units, the second LOD surfaces will smoothly fade in.
  - Set the *[Maximum Fade](../../../../principles/world_management/index.md#max_fade)* distance to 20 units. After 30 up to 50 units, the second LOD surfaces will smoothly fade out.
4. Choose the **third LOD** surfaces and: ![](visibility_lod_2.png)

  - Set the *[Minimum Visibility](../../../../principles/world_management/index.md#min_visible)* distance to 30 units. It means that when the second LOD surfaces begin to disappear, the third LOD surfaces will be shown.
  - Set the *[Maximum Visibility](../../../../principles/world_management/index.md#max_visible)* distance at 300 units. After 300 units the third LOD surfaces totally disappear.
  - Set the *[Minimum Fade](../../../../principles/world_management/index.md#min_fade)* distance to 20 units. The third LOD surfaces will start to smoothly fade in from 30 to 50 units.
  - Set the *[Maximum Fade](../../../../principles/world_management/index.md#max_fade)* distance to 50 units. After 300 units, the mesh will begin to smoothly fade out. > **Notice:** If you want to leave the last LOD surface always visible, set the Maximum Visibility distance to inf.


You should specify the same settings for each surface of the same LOD (if any). Different surfaces from one level of details should have the same settings to appear and disappear simultaneously.


#### Minimum and Maximum Parents


Another important parameters of the LODs are *[Min Parent and Max Parent](../../../../principles/world_management/index.md#parents)*.


These parameters enable you to specify to which surface or node up in the hierarchy the minimum and maximum visibility distances will be measured. Use the default values of 1. In this case, all surfaces of the mesh will be switched simultaneously, because their distances will be measured not to surfaces themselves, but to the bounding box of the whole mesh.


Read [here](../../../../principles/world_management/index.md#reference_object) about these parameters.
