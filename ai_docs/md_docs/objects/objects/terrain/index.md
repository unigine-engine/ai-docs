# Terrain


Unigine provides realistic terrain which can be designed and created manually or procedurally generated on the basis of geospatial data.


In Unigine, terrain is implemented as 2 types of objects:


- [![](terrain.png)](../../../objects/objects/terrain/landscape_terrain/index.md) � *[**Landscape Terrain**](../../../objects/objects/terrain/landscape_terrain/index.md)* that allows reconstructing practically any arbitrary landscape with diverse features: *Landscape Terrain* is recommended for ground operations (especially with scopes/binoculars required or where runtime modification is a must) or projects where extreme level of details is required (including helicopter simulation).

  - Virtually infinite terrain surface
  - Extreme details up to 1 mm per pixel
  - Adaptive hardware tessellation with displacement mapping
  - Dynamic modification at run time - craters, funnels, trenches
  - Simple and clear API
  - Up to 1024 detail materials
  - Layers system with flexible blending rules
  - Binoculars/scopes support (x20 / down to 1-degree FOV)
  - Optimized rendering and physics performance
  - Support for simultaneous editing by a team of 3D artists
  - Decal-based holes
- [![](terrain.png)](../../../objects/objects/terrain/terrain_global/index.md) � **[Global Terrain](../../../objects/objects/terrain/terrain_global/index.md)** is a virtually limitless terrain representing a certain fragment of Earth's surface generated on the basis of ordinary raster images and/or GIS data. It is recommended for large-scale flight simulation purposes (especially fixed wing) on georeferenced scenarios. Appearance of the global terrain object is determined by the accuracy and availability of source data. Features:

  - Limitless terrain which can cover the whole Earth's surface.
  - Plain or hilly relief based on imported height maps.
  - Realistic surface coverings (grass, rocks, dirt) created by means of [Terrain Global Details](../../../objects/objects/terrain/terrain_global/details/index.md).
  - Landcover masks used for Details and [Vegetation](../../../editor2/sandworm/workflow/vegetation/index.md).
  - [Decal-based](../../../objects/objects/terrain/terrain_global/index.md#decal_holes) holes.
  - Physical interaction with scene objects.
