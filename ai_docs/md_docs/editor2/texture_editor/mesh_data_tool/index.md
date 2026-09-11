# Draw Mesh Data Tool


![](../draw_mesh_data.png) **Draw Mesh Data** tool allows drawing textures that store mesh data (positions, mesh normals).


## Settings


![](mesh_data.png)


| Draw Data Type | Type of the texture to draw: - Position allows painting a 32-bit position texture in the object space. - Normal allows painting mesh normals in the object space. |
|---|---|
| Normal Range | Specifies the range of values for mesh normals: - From zero to positive � components of the normal vectors can have only positive values. It is a remapped range. You can use it if you are going to edit the texture in a third-party image editor. - From negative to positive � components of the normal vectors can have negative and positive values. It is a native range. |
