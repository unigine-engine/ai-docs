# NoData


Raster sources commonly mark pixels that carry no measurement � sea beyond a surveyed area, gaps between flight lines � with a dedicated **NoData** value. This section tells *Sandworm* what to do with such pixels.


All of this applies only to the pixels *Sandworm* recognizes as NoData. Where the value that counts as NoData comes from depends on the source:


- A **georeferenced image** � from the source metadata. The [*NoData Value*](../../../../editor2/sandworm/sources/elevation_imagery/index.md#nodata) field of the source overrides the declared value.
- A **TMS** elevation source � from the [*NoData Value*](../../../../editor2/sandworm/sources/elevation_imagery/index.md#nodata) field only, as a TMS source carries no metadata.


> **Notice:** If no value is declared at all, no pixel is ever treated as NoData: *Replace NoData* has nothing to act upon, and the empty areas are generated as if they held valid measurements.


Where these pixels are makes a difference, as the two cases are handled by different settings:


- Gaps **inside** the covered area (the ones between flight lines, for example) are processed pixel by pixel. *Replace NoData* decides whether such a pixel gets a value or stays transparent, letting the layer beneath show through.
- Areas that **no source covers at all**, such as the sea beyond the surveyed area, are processed by *Fill NoData Areas*, which fills the whole tiles left without elevation data.


## Parameters


![](nodata.png)


| Replace NoData | Replace the NoData pixels found in the data sources with the value specified below. When disabled, NoData pixels are zeroed and stay transparent, so that the layer beneath shows through. Applies to every raster source alike � elevation, imagery, and masks. |
|---|---|
| NoData Value | The value the NoData pixels are replaced with. Available in two cases, with a different effect in each: - If *[Replace NoData](#replace_nodata)* is enabled � the value is written into the NoData pixels found in the sources, making them opaque. Applied to any raster source. - If *Fill NoData Areas* is set to **[NoData Value](#fill_nodata)** � the value also fills the areas that no source covers at all. Applied to elevation data only. Do not confuse it with the *NoData Value* field of an [elevation source](../../../../editor2/sandworm/sources/elevation_imagery/index.md#nodata), which sets the value that marks the pixels as NoData for a specific elevation layer. |
| Fill NoData Areas | What to do with the areas of the elevation that the sources left uncovered: - **Off** � leave them transparent, so that the layer beneath shows through. - **Height Min Value** � fill them with the minimum height value, so that the layer maps blend consistently. The areas themselves stay transparent: the height is written only to give the neighboring maps a meaningful value to blend with. Use it only if you see visual artifacts such as sharp peaks rising from the water: it slows the generation of tiles down and increases their size. - **NoData Value** � treat everything outside the source data and the *Boundaries* of the layer as NoData and replace it with the value set in the *[NoData Value](#nodata_value)* generation setting (not the per-source *NoData Value* field). Applies to the elevation data of every landscape map. Use it to get a defined background level over the whole generated area � it makes the generated maps opaque over their entire area, increasing their size. > **Notice:** The parameter is available when *[Terrain Type](../../../../editor2/sandworm/interface/index.md#terrain_type)* is *[Object Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md)*. |
