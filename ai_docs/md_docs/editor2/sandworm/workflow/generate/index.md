# Generating the Terrain and Objects


As soon as you have [added imagery and/or elevation](../../../../editor2/sandworm/workflow/landscape/index.md), you are ready to generate a terrain.


The *Generation Settings* panel is behind the *Parameters* panel and is accessible by switching the tabs.


![](settings.png)


The items required to be set in order to start the terrain generation process, are highlighted red and displayed as clickable links at the bottom.


## Export Area


By default, all imported data are used to generate a terrain. It might take some time depending on the scope of your data.


You can set boundaries for the export area to limit the generated terrain area.


## Export World


*Export World* is a world where your terrain will be generated. If you have a world open in *UNIGINE Editor*, it would be set as the export world automatically. Otherwise, you'll need to (create and) select the world manually.


## Generating a Terrain


As soon as you configured all settings, click the *Generate Object Landscape Terrain* (*Generate Object Terrain Global*) button below and wait until the generation process is finished. A generated terrain is available in the selected world.


> **Notice:** You can also generate only the selected [type of data](../../../../editor2/sandworm/generation/data_types/index.md).


Switch to *Sandworm Camera* generated with a terrain to immediately observe the created terrain.


![](sw_camera.jpg)


If the generation process takes too much time, you can cancel it by closing the generation window and reconfigure the settings.


![](cancel_generation.png)


## Generating Once Again


Generate the terrain once again if you changed or added the data. You can also regenerate only the selected [type of data](../../../../editor2/sandworm/generation/data_types/index.md).


If you changed anything in the generated assets manually (directly in *UNIGINE Editor*) and then regenerate them, all manual changes will be lost.


## What Else


- [Frequently asked questions](../../../../editor2/sandworm/faq/index.md) on *Sandworm*
- Detailed information on all [generation settings](../../../../editor2/sandworm/generation/index.md)
