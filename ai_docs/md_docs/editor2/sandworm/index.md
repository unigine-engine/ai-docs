# Sandworm


The **Sandworm** tool is used to generate georeferenced terrain of any form using the provided data sources. This tool helps to quickly re-create portions of the real world by projecting them onto a flat *[Landscape Terrain](../../objects/objects/terrain/landscape_terrain/index.md)* or *[Terrain Global](../../objects/objects/terrain/terrain_global/index.md)* that supports [Curved](../../objects/geodetics/geodeticpivot/index.md) mode and natively works with geo-coordinates. The maximum terrain size depends on the available memory and data density, but typically, it's enough to create a big city or country landscape.


> **Notice:** *Sandworm* generates terrain based on geodata only. To generate a terrain using non-georeferenced data, use the *[Landscape Terrain](../../objects/objects/terrain/landscape_terrain/index.md)* object directly.


The list of *Sandworm* features currently includes the following:


- Support for multiple georeferenced sources: raster (elevation, imagery, and masks) and vector (roads, buildings, etc.)
- Advanced data filtering options: via attributes (vector sources), via indexed, color, and channel masks (raster sources)
- Support for online *TMS (Mapbox, OSM)* and offline data sources
- Mask-based generation of vegetation
- Generation of additional details (sand, rocks, etc.) based on landcover data for more realistic landscape surfaces
- Procedural generation of objects (roads, powerlines, buildings, landmarks, etc.)
- Advanced control and fine-tuning of placement parameters
- Support for most of the widely used Coordinate Reference Systems *(CRS)* for input as well as output projections
- Ability to combine sources with different projection types within a single project
- Export to *Landscape Terrain* and *Terrain Global*
- Coherent and user-friendly interface


*Sandworm* generates a terrain using the elevation (height) and imagery (albedo) data provided. You can use the following types of data sources:


- **Offline** � locally stored tilesets: **raster** (elevation, imagery, and masks) and **vector** data sources from your local storage device
- **Online** � Tile Map Services *(TMS)*: you can connect to both open services (such as *[OpenStreetMap](https://www.openstreetmap.org/)* or various state/municipal databases) and private tile servers created and supported by users.


Georeferenced imagery and elevation data are processed using *GDAL* � Geospatial Data Abstraction Library. It supports various raster formats with different map projections for input data. It is also possible to combine different projection types and data sources to generate a terrain.


*Sandworm* uses *GDAL* for data processing, therefore, the supported formats are those marked **Built-in by default** in the **Build Requirements** column of the following lists:


- [Raster data formats](https://gdal.org/en/stable/drivers/raster/index.html)
- [Vector data formats](https://gdal.org/en/stable/drivers/vector/index.html)


As assets, *Sandworm* takes vector data in `*.shp`, `*.geojson`, and `*.sxf`; raster data comes in any format the Editor imports as a texture � `*.tif`, `*.tiff`, `*.png`, `*.jpg`, `*.dds`, `*.exr`, `*.hdr`, and others.


Any other format from the lists above is added as an *[External File](../../editor2/sandworm/sources/index.md#data_sources)* instead: such a file is read from its location on the disk and is not imported into the project, so the path to it has to be updated if you share the project.


These data sources usually contain a lot of information that can be filtered out.


For example, by using filters you can:


- Generate grass or trees for areas marked with specific colors of the landcover texture.
- Generate only highways ignoring small roads using a *road type* Attribute in a vector data file.
- Generate buildings of a particular type only (e.g., apartments, garages, single- or multi-story buildings, depending on the data stored in the vector data source).


*Sandworm* supports multiple data layers aligned by geo or raster coordinates: you can easily create high-resolution insets by adding a highly detailed landscape area over a less detailed one. This can be useful for flight simulators, where a high level of detail is required only for areas around airports. The quality of generated terrain is determined by the density of the data sources used.


[![](inset_sm.jpg)](inset.jpg)

*Highly detailed inset over a low-detail area*


### See Also


- Series of [video tutorials on the terrain generation](../../videotutorials/essentials/sandworm.md) using Sandworm
- Article on *[Landscape Terrain](../../objects/objects/terrain/landscape_terrain/index.md)*
- Documentation on the *[GDAL](http://www.gdal.org/)* library
- [Wikipedia article on Equirectangular projection](https://en.wikipedia.org/wiki/Equirectangular_projection)
