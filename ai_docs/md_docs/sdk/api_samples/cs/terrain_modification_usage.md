# Terrain Modification & Usage

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/csharp-component-samples](https://github.com/unigine-engine/csharp-component-samples)**.


## Polygon-Based Tools for Procedural Modifications

This sample demonstrates procedural generation of polygon objects from world points, enabling runtime landscape editing and object placement.


It dynamically creates polygonal geometry and applies it in multiple contexts:


- **ObjectMeshStatic** - creates *ObjectMeshStatic* and places it at the center of the *WorldBoundBox* formed by the points.
- **DecalMesh** - creates *DecalMesh* and places it at the center of the *WorldBoundBox* formed by the points.
- **DecalOrtho** - renders mesh into a texture applied to the albedo slot of *DecalOrtho* material.
- **Terrain mask** - renders mesh into Layer Map mask to control clutter placement (cubes) on landscape.
- **Level terrain** - levels terrain height to the lowest point value within the polygon area.
- **Lower terrain** - lowers terrain by 20 units within the polygon area.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/terrain_modification_usage/polygon_based_procedural_modifications*
