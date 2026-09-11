# River Object Parameters


> **Warning:** This feature is under active development and is not yet stable.


*Sandworm* allows generating rivers based on the spline or polygon data. The object is generated as a *[Decal Mesh](../../../../objects/decals/mesh/index.md)* uses the default *water_decal*.


![](generated_river.jpg)


## Parameters


![River object parameters](river_parameters.jpg)


| Line River Width | Width of the River object generated based on the vector type data. |
|---|---|
| Min / Max Visibility | Minimum and maximum visibility distance values, in units, for the generated river *Decal Mesh* object. |
| Min / Max Fade | Distance in units within which the generated river *Decal Mesh* object gradually fades in/out. |
| Split Lines Length (km) | Rivers are projected onto the terrain with *[Decal Mesh](../../../../objects/decals/mesh/index.md)* objects. A single decal spanning a long river would be too large, so the river is cut into a grid with this cell size, and every cell becomes a decal of its own. |
| Adjust Terrain Masks | Cut the **masks data** of the terrain out along the rivers, over the width given by *[Area Width](#area_width)* � to keep grass from growing on water, for example. Every mask layer in the project is affected, not only the one used for vegetation. - Enabling this significantly increases generation time. - Only those mask LODs are adjusted whose density satisfies **Density < Area Width x 6**. |
| Area Width | Width of the band along the river line affected by mask adjustment. |
