# Elevation and Imagery


Elevation and Imagery are required to create a landscape with some basic coloring:


- **Elevation / Height** � to generate terrain geometry
- **Imagery / Color** � to generate textures for the terrain surface


![](settings.png)


You can add a [georeferenced image](../../../../editor2/sandworm/sources/index.md#georeferenced_image) or a [TMS](../../../../editor2/sandworm/sources/index.md#tms) as a data source. See the [list of supported formats](../../../../editor2/sandworm/index.md#data_formats).


You can also define the data source [boundaries](../../../../editor2/sandworm/sources/index.md#boundaries) to specify the scope of the required data.


An example of adding a data source is given [here](../../../../editor2/sandworm/workflow/landscape/index.md).


## NoData Value for Elevation Sources


An elevation source may carry no NoData value in its metadata at all, or carry one that does not match the value its empty pixels actually hold. The *NoData Value* field sets the pixel value to be interpreted as NoData for this source, overriding the one declared in the source metadata. Tick the checkbox next to the field to enable it: while the checkbox is clear, the field is disabled and the value from the metadata is used. What is then done with the pixels found this way is defined by the [NoData](../../../../editor2/sandworm/generation/nodata/index.md) generation settings.


![](nodata_setting.png)


For example, a DEM stored as 16-bit integers may declare -9999 in its metadata while its empty areas over the sea actually hold -32768. Nothing is recognized as NoData then, and the sea is generated as a pit dropping to -32768. Setting the field to -32768 fixes it.


The value is matched exactly, with a tolerance of 1e-6 � there is no "everything below a threshold" mode. Suppose the empty areas of a source hold a mix of values: -9999 over the sea and -32768 between the flight lines. With the field set to -9999, only the first ones are treated as NoData, while the -32768 pixels stay in the terrain as valid heights, even though they lie far below the value specified. Only one value per source can be caught this way. The field itself takes values from -1e9 to 1e9 with 4 decimal places.


The field is available both for georeferenced images and for *TMS* elevation sources. A *TMS* source carries no metadata at all, so for it this field is the only way to declare a NoData value; a change made for an existing *TMS* layer is applied by the *[Update Elevation Layer](#update_layer)* button.


> **Warning:** Pixels are matched by value across the whole source, not by location. Choose a value that never occurs in the data as a valid height: -32768 or -31750 are safe for elevation in meters, while 0 would remove every pixel at sea level from the terrain along with the empty ones.


## Creating a Layer


The *Create Elevation Layer(s)* (*Create Imagery Layer(s)*) button adds the created layer to your *Sandworm* project. A single *TMS* source always yields one layer, so for it the button is named *Create Elevation Layer* (*Create Imagery Layer*).


## Updating a Layer


You can modify the layer boundaries and, for TMS sources, the *Zoom Level* and the *[NoData Value](#nodata)* after the layer was created.


To save changes to TMS sources, click the *Update Elevation Layer* (*Update Imagery Layer*) button.


Changes to the boundaries of georeferenced images are saved automatically.
