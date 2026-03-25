# Detecting Unique Assets


When your project contains multiple worlds, you may need to identify which assets are used exclusively in a specific world and not shared with others.


The *Show Assets Used Only In This World* option is designed to simplify this process. It displays a list of assets used exclusively in the selected world (meaning that the assets are not used in any of the worlds included in dependency search).


To generate the list of unique assets, right-click the world file in the Asset Browser and choose *Show Assets Used Only In This World*.


![](context_menu_unique_assets.png)


This will open the following window:


![](unique_assets_window.png)


The window contains the following sections:


| Worlds Included in Dependency Search | Worlds to be used for comparison. Enable the *Use* checkbox for the worlds to be included. |
|---|---|
| Assets Used Only In This World | All the assets (materials, textures, FBX files, meshes, properties, etc.) that are used exclusively in the world you right-clicked to open this window (the name of this world is displayed on the tab). These assets are not used in any of the worlds selected in the *Worlds Included in Dependency Search* section. |
