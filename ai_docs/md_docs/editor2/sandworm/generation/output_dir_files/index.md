# Output Directories and Files


![](settings.png)


## Export World


*Export World* is a world to which the terrain will be generated. If a world is open when creating a *Sandworm* project, it is automatically added as *Export World*.


## Generation Path


*Sandworm* stores the paths to all data sources as well as all generation parameters as an `asset`. So, after setting up all output parameters, save the *Sandworm* project by choosing *File -> Save* or *File -> Save As* and specifying the name and path for your asset.


The *Sandworm* project can be stored only inside the `/data` folder.


## Cache Path


Cache folder stores the data for *[Export Area](../../../../editor2/sandworm/generation/export_area/index.md)*. If you don't set the export area, the cache is created for all sources that were added to the project. This data is reused if you decide to set the export area.


If *[Export Area](../../../../editor2/sandworm/generation/export_area/index.md)* is redefined, and it contains the parts of the previously defined export area, the cache is reused to speed up the generation process.


The ![](../../interface/trash_bin.png) button is used to clean the cache folder. We recommend clearing cache before you start the terrain generation.
