# Elevation and Imagery


Elevation and Imagery are required to create a landscape with some basic coloring:


- **Elevation / Height** — to generate terrain geometry
- **Imagery / Color** — to generate textures for the terrain surface


![](settings.png)


You can add a [georeferenced image](../../../../editor2/sandworm/sources/index.md#georeferenced_image) or a [TMS](../../../../editor2/sandworm/sources/index.md#tms) as a data source.


You can also define the data source [boundaries](../../../../editor2/sandworm/sources/index.md#boundaries) to specify the scope of the required data.


An example of adding a data source is given [here](../../../../editor2/sandworm/workflow/landscape/index.md).


## Preview


The *Preview* button generates the data preview in the *Map* window after setting and resetting the data sources.


> **Notice:** The preview generation process may take much time for heavy source files, therefore you can [cancel it](../../../../editor2/sandworm/interface/index.md#cancel_preview), and [generate later](../../../../editor2/sandworm/interface/index.md#context_menu), if required.


## Creating a Layer


The *Create Elevation Layer* (*Create Imagery Layer*) button adds the created layer to your *Sandworm* project.


## Updating a Layer


You can modify the layer boundaries and Zoom level (for TMS sources) after the layer was created.


To save changes to TMS sources, click the *Update Elevation Layer* (*Update Imagery Layer*) button.


Changes to the boundaries of georeferenced images are saved automatically.
