# Exporting 3D Models From Maxon Cinema 4D


This article describes how to export your 3D Model From *Maxon Cinema 4D* so that it would have proper scaling, position, and orientation when imported to UnigineEditor.


## See Also


> **Warning:** The tutorial is created using **SDK version 2.11**. The general workflow demonstrated in the tutorial is applicable for versions **up to 2.21**. However, specific details such as UI may differ across various versions.


## Pre-Export Arrangement


Before the export, do the following:


- Select *Edit -> Preferences...* and check that **Centimeters** are set as Unit Display. ![](cinema4d_unit_display.png) In the *Project Settings*, check that **Centimeters** are set as working units. ![](cinema4d_units.png) In the Viewport options (*Options -> Configure*), *Background* tab, set the grid cell size of 1 meter for convenience. ![](cinema4d_grid.png)
- Orient the model towards the negative direction of the Z axis. ![](cinema4d_axis.png)
- Set the actual model size.
- Freeze all transformations to avoid placement issues. ![](cinema4d_transform.png)
- Check that materials are ready for export.


## Export Settings


As soon as your model is ready for export, click *File -> Export... -> FBX*.


In the Export Settings window, enable *Normals* and *Triangulate Geometry*.


![](cinema4d_export_settings.png)
