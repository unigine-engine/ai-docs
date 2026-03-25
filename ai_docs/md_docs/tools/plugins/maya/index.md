# Plugins for Maya


> **Warning:** Maya plugin is deprecated and no longer supported. We can't guarantee the stable work of the plugin.


## Manual Installation


If Unigine plugins were not installed automatically, do the following:

1. Go to the UNIGINE SDK folder, `plugins/Maya/` directory and choose the plugin depending on the installed version of Maya.
2. Copy a binary file into the `plug-ins` folder, namely:

  - On Windows, copy the `*.mll` file into the `Maya*/bin/plug-ins` directory (`*` means installed version of Maya: 2013, 2014 or 2015).
  - On Linux, copy the `*.so` file into the `/usr/autodesk/maya*-x64/bin/plug-ins` directory (`*` means installed version of Maya: 2013, 2014 or 2015).
  - On Mac OS X, copy the `*.bundle` file into the `Applications/Autodesk/maya*/Maya.app/Contents/MacOS/plug-ins` directory (`*` means installed version of Maya: 2013, 2014 or 2015).
3. Copy the MEL script (`*.mel`) into the `others` directory, namely:

  - On Windows, copy into the `Maya*/scripts/others` (`*` means installed version of Maya: 2013, 2014 or 2015).
  - On Linux, copy into the `/usr/autodesk/maya*-x64/scripts/others`(`*` means installed version of Maya: 2013, 2014 or 2015).
  - On Mac OS X, copy into the `Applications/Autodesk/maya*/Maya.app/Contents/scripts/others`(`*` means installed version of Maya: 2013, 2014 or 2015).
4. Run Maya.
5. Choose *Window -> Settings/Preferences -> Plug-in manager* in the Maya main menu.
6. Set *Loaded* and *Auto load* flags for UnigineMesh plugins. ![](manual_install.png) *Loaded and Auto load flags checked for the UnigineMesh.mll*


## Export into Mesh


To export static geometry or an animated object into the `*.mesh` file:

1. Select a model you want to export into Unigine.
2. Select *File* -> *Export Selection...* in the main menu.
3. Choose ***UnigineMesh*** in the*Files of type* drop-down list.


By using the way described above, you can export animated (skinned) object baked together with its animation in one file (`*.mesh`).  To export only the bind pose of the model, specify the **0** values in both fields of the *Animation Range*.


![Export into mesh from Maya](maya_mesh_export.png)

*Static geometry export (into MESH format)*


> **Notice:** For skinned mesh:
> - The maximum number of bones per surface is equal to **128**.
> - Each vertex can have up to **4** bones assigned to it.


| Flip Y/Z Axes | This option flips the Y and Z axes and inverts **Y** axis. |
|---|---|
| Flip Tangent Space | Flips the sign of the binormal component of the tangent space. |
| Export Blend Shapes | Exports blend shapes (i.e. morph targets). |
| Export Skin Clusters | Exports skin clusters (i.e. skin controllers). You should check this option to export a skinned mesh. |
| Alignment | Sets a point that will be used as the origin of coordinates: - **World** — use the origin of world coordinates. - **Center** — use the center of the model's bounding sphere. - **Bottom** — use the bottom of the model's bounding sphere. - **Top** — use the top of the model's bounding sphere. |
| Scale | Scaling ratio. This value scales the size of a mesh. The default value of **1** means the mesh is exported without scaling. |
| Animation Range | Sets the range of animation. To export only the bind pose of the model without animation, specify the **0** values in both fields. To export animation, specify the first and the last animation frame number. |


To check whether the export is done successfully, choose *Window* -> *General Editors* -> *Script Editor* and check the following information:


![](script_editor.png)


> **Notice:** The exported surfaces and animations will be sorted alphabetically.


## Export Only Animation of Skinned Mesh


To export the animation of Unigine skinned mesh into the `*.anim` file:

1. Select a model whose animation you want to export into Unigine.
2. Select *File* -> *Export Selection...* in the main menu.
3. Choose `UnigineMesh` in the *Files of type* drop-down list.
4. Specify the name of the exported file with the `*.anim` extension. For example: `my_animation.anim`.
5. Click *Export Selection*.


> **Notice:** The exported animations will be sorted alphabetically.


## Import of Mesh and Skinned Mesh


To import a Unigine-native mesh or skinned mesh into Maya:

1. Select *File* -> *Import* in the main menu.
2. Choose **UnigineMesh** in the *Files of type* drop-down list.
3. Choose a file in `*.mesh` format.
4. Click *Import*.
