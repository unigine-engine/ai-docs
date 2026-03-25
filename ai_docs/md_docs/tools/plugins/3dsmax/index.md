# Plugins for 3ds Max


## Manual Installation


> **Warning:** 3sd Max plugin is deprecated and no longer supported. We can't guarantee the stable work of the plugin.


If Unigine plugins were not installed automatically, do the following:

1. Go to the UNIGINE SDK folder, `plugins/Max/` directory and choose the plugin depending on the installed version of 3ds Max.
2. Copy the `UnigineMesh.dle` and `UniginePath.dle` files into the 3ds Max `plugins` folder: for example, `3ds Max 2013/plugins`.
3. Restart 3ds Max to get plugins ready to work.


## How to Use the Plugin


You should enable the Unigine mesh exporter on the *Utilities* panel:

1. Go to *Utilities* panel (click the ![](utilities_tab.png) tab on the right-hand column) and click *More...*. ![](utilities_open.png)
2. Choose *UnigineMesh Utility* in the list that appears and click *OK*. ![](UnigineMesh_utility.png) The *UnigineMesh* panel appears in the right-hand column: ![](UnigineMesh_panel.png)


To export 3ds Max models, use the following options:

- ***Export As...*** enables to choose the file to which the model should be exported.
- ***Export*** saves the model into the same file (as previously specified in the*Export As...* option).


For other export options, see [below](#mesh_export).


## Export Static Geometry or Animated Object into Mesh


To export static geometry or an animated object into the `*.mesh` file:

1. Select models to be exported.
2. Do one of the following:

  - On the *UnigineMesh* panel:

    1. Set up the export options.
    2. Click the *Export as..* or *Export* (to export the whole scene).
    3. On the window that opens, choose the `*.mesh` format, specify a name and click the *Save*.
  - In the *File* menu option:

    1. Choose the *Export* -> *Export selected* or *Export* (to export the whole scene).
    2. On the window that opens, choose the `*.mesh` format, specify a name and click the *Save*.
    3. Set up the export options and click *OK*.


The window with export information opens if the export is done successfully:


![](export_info.png)


> **Notice:** The exported surfaces and animations will be sorted alphabetically.


By using the way described above, you can export animated (skinned) object baked together with its animation in one file (`*.mesh`).


It is also possible to export only the bind pose of the model (and after that, use it in the engine with separately exported animations, see details [below](#sanim_export)).  To export only the bind pose, specify the **0** for the *From Frame* and *To Frame* options when setting up the export options:


![](zero_frames.png)

*From Frame = 0; To Frame = 0*


> **Notice:** For skinned mesh:
> - The maximum number of bones per surface is equal to **128**. If the number exceeds this limit, small child bones will be simply ignored by export.
> - Each vertex can have up to **4** bones assigned to it.


### Mesh Export Options


![Export into a mesh from 3ds Max](export_options_1.png)

*Export of the static geometry or animated object (into MESH format)*


| Flip Y/Z Axes | This option flips the Y and Z axes and inverts the Y axis. You can export a mesh with a proper orientation even if *World Up Vector* is set to the Y axis. |
|---|---|
| Flip Tangent Space | Flips the sign of the binormal component of the tangent space. |
| Split By Materials | If Multi-materials are used, polygons with the same sub-material assigned are exported as a separate surface. - Sub-materials are considered the same if they have the same name. - Exported surfaces will be named after names of sub-materials (*<objectName>_<materialName>_<submaterialName>*). |
| Export Morphing | Exports the morph controller. |
| Export Skinning | Exports the skin controller. |
| Alignment | Sets a point that will be used as the origin of coordinates: - **World** — use the origin of world coordinates. - **Pivot** — use the pivot coordinates. > **Notice:** When exporting relative to the pivot, the value of the Scale option is ignored. It is reset to the default **100**  %. - **Center** — use the center of the model's bounding sphere. - **Bottom** — use the bottom of the model's bounding sphere. - **Top** — use the top of the model's bounding sphere. |
| Scale | A scaling ratio. This value scales the size of a mesh (static or skinned). |
| Channel 1 | UVW channel that should be copied into the 1st UV channel of the exported file. Enter **0** to fill the channel with zeros. |
| Channel 2 | UVW channel that should be copied into the 2nd UV channel of the exported file. Enter **0** to fill the channel with zeros. |
| From Frame | Start animation time. You can specify the **-1** to use the start time of the current viewport configuration. |
| To Frame | End animation time. You can specify the **-1** to use the end time of the current viewport configuration. |


## Export Only Animation of Skinned Mesh


You can export only animation (bones transformations) of a skinned mesh to a separate file. This way, you can have only one mesh and choose what animations to set for it.


To export only animation into `*.anim` file:

1. Select a skinned mesh which animation is going to be exported.
2. On the *UnigineMesh* panel set up the export options.
3. Click the *Export as..* or *Export* (to export the whole scene).
4. On the window that opens, choose the `*.anim` format, specify a name and click the *Save*.


The window with export information opens if the export is done successfully:


![](export_info.png)


> **Notice:** The exported animations will be sorted alphabetically.


## Export Path Transformation


You can export a spline (a line or other shape) along which object movement is constrained (via *Animation* -> *Constraints* -> *Path Constraint* in 3ds Max)  to a `*.path` file (a [native Unigine path](../../../api/library/common/class.path_cpp.md)).

> **Notice:** A path will be exported only if both the `UnigineMesh.dle` and `UniginePath.dle` files are located in the 3ds Max `plugins` folder.


To export a spline to the `*.path` file:

1. Select an object which movement is restricted along a spline.
2. On the main menu, select ![](file.png) *-> Export -> Export Selected*. > **Notice:** You can export only one path at a time.
3. On the window that opens, choose the `*.PATH` format, specify a name and click *Save*.
4. Set up the [export options](#path_export_options) and click *OK*.


The window with export information opens if the export is done successfully:


![](export_path.png)


You can create, for example, a frame-based succession of transformations from the exported path (an instance of the [*WorldTransformPath*](../../../api/library/worlds/class.worldtransformpath_cpp.md) class).


### Path Export Options


![](path_options.png)


| Flip Y/Z Axes | Flips the Y and Z axes and inverts the Y axis. You can export a path with a proper orientation even if *World Up Vector* is set to the Y axis. |
|---|---|
| Scale | A scaling ratio. This value scales the size of a path. |
| From Frame | Start animation time. You can specify the **-1** to use the start time of the current viewport configuration. |
| To Frame | End animation time. You can specify the **-1** to use the end time of the current viewport configuration. |


## Import of Unigine Mesh or Skinned Mesh


To import the native Unigine mesh of skinned mesh (`*.mesh` file) into 3ds Max:

1. On the main menu, select *File* -> *Import*.
2. Choose a `*.mesh` file and click the *Open*.
3. Specify the import options and click *OK*.


> **Notice:** The old formats `*.mesh` and `*.smesh` can also be imported.


### Mesh Import Options


![](import_options.png)


| Flip Y/Z Axes | Flips the Y and Z axes and inverts the Y axis. You can export a mesh with a proper orientation even if *World Up Vector* is set to the Y axis. |
|---|---|
| Import Morphing | Imports the morph controller. |
| Import Skinning | Imports the skin controller. |
| Scale | A scaling ratio. This value scales the size of a mesh (static or skinned). |


## Import of Unigine Skinned Mesh Animation


To import the animation of Unigine skinned mesh (`*.anim` file ) into 3ds Max:

1. On the main menu, select *File* -> *Import*.
2. Choose an `*.anim` file and click the *Open*.
3. Specify the import options and click *OK*.


> **Notice:** The `*.sanim` format can also be imported.
