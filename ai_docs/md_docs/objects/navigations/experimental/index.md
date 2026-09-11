# Experimental Navigation


The experimental navigation system searches paths over a walkable surface built from the geometry of the scene. Three node types take part in it:


- **[Navigation Mesh (Experimental)](../../../objects/navigations/experimental/navigation_mesh/index.md)** builds the walkable surface out of the geometry inside its volume, and every path query is made against it.
- **[Navigation Mesh Invoker (Experimental)](../../../objects/navigations/experimental/invoker/index.md)** loads the navigation mesh around itself as it moves, so that a world too large to fit in memory keeps only the part that is in use.
- **[Navigation Mesh Area Volume (Experimental)](../../../objects/navigations/experimental/area_volume/index.md)** marks a special zone on the walkable surface, such as mud to be avoided or a road to be preferred, or cuts a hole in it.


> **Notice:** The [Navigation Areas](../../../objects/navigations/navigation/index.md) are a separate system: they have their own nodes, their own masks and their own API, and neither system knows about the walkable surface of the other. The [Obstacles](../../../objects/navigations/obstacle/index.md) are shared and work in both.
