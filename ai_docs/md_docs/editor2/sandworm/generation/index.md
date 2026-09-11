# Generation Settings


The source data added using *Sandworm* can be exported to a world in either of the two [Terrain Types](../../../editor2/sandworm/interface/index.md#terrain_type), both having a practical limit of up to 10,000 x 10,000 km:


- *[Object Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md)* � a more efficient advanced type of terrain, useful for very detailed terrains, doesn't support geo-coordinates for now, supports collaborative editing, supports runtime modification, faster intersection testing, binoculars-friendly.
- *[Object Terrain Global](../../../objects/objects/terrain/terrain_global/index.md)* � useful for large-scale multi-inset terrains, supports [curved](../../../objects/geodetics/geodeticpivot/index.md) mode, natively works with geo-coordinates, can be generated from raw GIS data.


As these two objects are different in their nature, you need to define the following output settings depending on the selected type of the terrain:


## Articles in This Section

- [Export Area](../../../editor2/sandworm/generation/export_area/index.md)

- [Data Types](../../../editor2/sandworm/generation/data_types/index.md)

- [Projection](../../../editor2/sandworm/generation/projection/index.md)

- [Quality](../../../editor2/sandworm/generation/quality/index.md)

- [NoData](../../../editor2/sandworm/generation/nodata/index.md)

- [Distributed Generation and Headless Mode](../../../editor2/sandworm/generation/distributed_computing/index.md)

- [Output Directories and Files](../../../editor2/sandworm/generation/output_dir_files/index.md)
