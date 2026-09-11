# Unigine::Plugins::CesiumConfig Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


This class is the programmatic view of the [Cesium plugin configuration file](../../../../code/plugins/cesium/config.md): the access token location, the streamed data sources (assets), the terrain insets, the level of detail, the masks of the streamed tiles, the tile cache, and the diagnostics. The settings are stored in the `cesium_config.json` file located in the `data/` directory of the project.


The configuration is obtained via the *[Cesium](../../../../api/library/plugins/cesium/class.cesium_usc.md)* class. Edits take effect when the plugin's configuration is applied. The tilesets are rebuilt, dropping and re-streaming every loaded tile, only when a setting they read has changed: edits they do not read, such as the inset list or the log level, are applied instantly. Call **[save()()](../../../...md#save_bool)** first to make the changes persistent, or omit it for a change that should die with the application.


An invalid or unusable combination of settings never stops the plugin from loading: the globe stays idle and the reason is reported to the log.


## CesiumConfig Class

### Members

## int isIonAccessTokenFromEnvironment () const

Returns the current Returns a value indicating if the ion access token came from the *CESIUM_ION_TOKEN* environment variable. The variable is checked before the token file: while it is set, the file is not read, and a token saved through the API goes to the file but loses to the variable on the next run.
### Return value

Current the ion access token was taken from the environment
## int getNumAssets () const

Returns the current number of entries in the assets list of the configuration (the data sources to stream, in order).
### Return value

Current number of assets in the configuration
## int getNumInsets () const

Returns the current number of entries in the insets list of the configuration (the high-detail terrain patches to be swapped in when the camera comes close enough). Disabled entries are counted too.
### Return value

Current number of terrain insets in the configuration
---

## string getConfigPath ( )

Returns the path of the plugin configuration file. By default it is the `cesium_config.json` file located in the `data/` directory of the project.
### Return value

Path to the configuration file.
## void setConfigPath ( string path )

Sets the path of the plugin configuration file.
### Arguments

- *string* **path** - Path to the configuration file.

## string getIonAccessToken ( )

Returns the *Cesium ion* access token. Every *Cesium ion* asset requires a token that is entitled to it.
### Return value

*Cesium ion* access token.
## void setIonAccessToken ( string token )

Sets the *Cesium ion* access token. A token set through the API is persisted on save (see **[save()()](../../../...md#save_bool)**) to the token file at the resolved path, never into the configuration file itself. It is written even while the *CESIUM_ION_TOKEN* environment variable supplies the token, but on the next run the variable wins (see **[isIonAccessTokenFromEnvironment()()](../../../...md#isIonAccessTokenFromEnvironment_int)**).
### Arguments

- *string* **token** - *Cesium ion* access token.

## string getIonAccessTokenPathOverride ( )

Returns the override path to the file that holds the *Cesium ion* access token. Normally it is empty and the token file lives at the machine-default location: the token is a per-machine credential rather than a project setting, and it is deliberately kept out of the configuration file, so that the configuration remains safe to share and to store in a version control system. The path actually in use is returned by **[getResolvedIonAccessTokenPath()()](../../../...md#getResolvedIonAccessTokenPath_cstr)**.
### Return value

Override path to the token file, or an empty string when the default location is used.
## void setIonAccessTokenPathOverride ( string path )

Sets the override path to the file that holds the *Cesium ion* access token.
### Arguments

- *string* **path** - Override path to the token file; an empty string means the default location.

## string getResolvedIonAccessTokenPath ( )

Returns the path of the token file that is actually in use: the override path when one is set, the machine-default location otherwise. It always names a file, and it is where a token set through the API is saved.
### Return value

Path of the token file in use.
## string getDefaultIonAccessTokenPath ( )

Returns the default location of the token file: a `UnigineCesium/cesium_token` file in the per-user application data directory of the machine. Use it to arrange a token before any configuration exists.
### Return value

Default, machine-specific path of the token file.
## string getAssetName ( int index )

Returns the name of the asset with the given index, displayed in the user interface and the log.
### Arguments

- *int* **index** - Index of the asset.

### Return value

Name of the asset.
## void setAssetName ( int index , string name )

Sets the name of the asset with the given index, displayed in the user interface and the log.
### Arguments

- *int* **index** - Index of the asset.
- *string* **name** - Name of the asset.

## int getAssetType ( int index )

Returns the type of the asset with the given index, defining what the asset is used for: terrain, imagery, or 3D tiles.
### Arguments

- *int* **index** - Index of the asset.

### Return value

Type of the asset, one of the *ASSET_TYPE_** values.
## void setAssetType ( int index , int type )

Sets the type of the asset with the given index, defining what the asset is used for: terrain, imagery, or 3D tiles.
### Arguments

- *int* **index** - Index of the asset.
- *int* **type** - Type of the asset, one of the *ASSET_TYPE_** values.

## int getAssetSource ( int index )

Returns the source of the asset with the given index, defining where the tiles come from.
### Arguments

- *int* **index** - Index of the asset.

### Return value

Source of the asset, one of the *ASSET_SOURCE_** values.
## void setAssetSource ( int index , int source )

Sets the source of the asset with the given index, defining where the tiles come from.
### Arguments

- *int* **index** - Index of the asset.
- *int* **source** - Source of the asset, one of the *ASSET_SOURCE_** values.

## int getAssetIonId ( int index )

Returns the *Cesium ion* asset ID of the asset with the given index. Meaningful only for the *Cesium ion* source.
### Arguments

- *int* **index** - Index of the asset.

### Return value

*Cesium ion* asset ID.
## void setAssetIonId ( int index , int id )

Sets the *Cesium ion* asset ID of the asset with the given index. Meaningful only for the *Cesium ion* source.
### Arguments

- *int* **index** - Index of the asset.
- *int* **id** - *Cesium ion* asset ID (for example, 1 for *Cesium World Terrain* or 2 for *Bing Maps Aerial* imagery).

## bool isAssetEnabled ( int index )

Returns a value indicating if the asset with the given index is used for streaming (subject to the asset combination rules).
### Arguments

- *int* **index** - Index of the asset.

### Return value

true if the asset is used; otherwise, false.
## void setAssetEnabled ( int index , bool enabled )

Sets a value indicating if the asset with the given index is used for streaming.
### Arguments

- *int* **index** - Index of the asset.
- *bool* **enabled** - true to use the asset for streaming; false to disable it.

## int addAsset ( )

Appends an empty asset entry to the configuration and returns its index.
### Return value

Index of the new asset entry.
## void removeAsset ( int index )

Removes the asset entry with the given index from the configuration.
### Arguments

- *int* **index** - Index of the asset to remove.

## void clearAssets ( )

Removes all asset entries from the configuration.
## string getInsetName ( int index )

Returns the name of the terrain inset with the given index, displayed in the user interface and the log.
### Arguments

- *int* **index** - Index of the inset.

### Return value

Name of the inset.
## void setInsetName ( int index , string name )

Sets the name of the terrain inset with the given index, displayed in the user interface and the log.
### Arguments

- *int* **index** - Index of the inset.
- *string* **name** - Name of the inset.

## string getInsetPath ( int index )

Returns the path to the world file of the terrain inset with the given index. The path is resolved relative to the data directory of the project.
### Arguments

- *int* **index** - Index of the inset.

### Return value

Path to the inset world file.
## void setInsetPath ( int index , string path )

Sets the path to the world file of the terrain inset with the given index.
### Arguments

- *int* **index** - Index of the inset.
- *string* **path** - Path to the inset world file, relative to the data directory of the project.

## bool isInsetEnabled ( int index )

Returns a value indicating if the terrain inset with the given index is enabled. A disabled entry keeps its slot but is not used: its terrain is not loaded and it never activates. Changes to the insets take effect when the configuration is applied.
### Arguments

- *int* **index** - Index of the inset.

### Return value

true if the inset is enabled; otherwise, false.
## void setInsetEnabled ( int index , bool enabled )

Sets a value indicating if the terrain inset with the given index is enabled. Changes to the insets take effect when the configuration is applied.
### Arguments

- *int* **index** - Index of the inset.
- *bool* **enabled** - true to enable the inset; false to skip it.

## double getInsetActivationDistance ( int index )

Returns the activation distance of the terrain inset with the given index: how close the camera must come to the inset origin for the inset to be activated.
### Arguments

- *int* **index** - Index of the inset.

### Return value

Activation distance of the inset, in meters.
## void setInsetActivationDistance ( int index , double meters )

Sets the activation distance of the terrain inset with the given index: how close the camera must come to the inset origin for the inset to be activated. It is specified per inset, because a large area is swapped in from further away than a small one.
### Arguments

- *int* **index** - Index of the inset.
- *double* **meters** - Activation distance, in meters. Choose a value noticeably larger than the radius of the inset itself.

## int addInset ( )

Appends an empty terrain inset entry to the configuration and returns its index. Changes to the insets take effect when the configuration is applied.
### Return value

Index of the new inset entry.
## void removeInset ( int index )

Removes the terrain inset entry with the given index from the configuration. Changes to the insets take effect when the configuration is applied.
### Arguments

- *int* **index** - Index of the inset to remove.

## void clearInsets ( )

Removes all terrain inset entries from the configuration. Changes to the insets take effect when the configuration is applied.
## double getMaxScreenSpaceError ( )

Returns the level-of-detail target for the tiles in view, in pixels. Lower values give finer tiles at the cost of more streaming, memory, and bandwidth; higher values give coarser and cheaper tiles.
### Return value

Level-of-detail target for the tiles in view, in pixels.
## void setMaxScreenSpaceError ( double value )

Sets the level-of-detail target for the tiles in view, in pixels. Lower values give finer tiles at the cost of more streaming, memory, and bandwidth; higher values give coarser and cheaper tiles.
### Arguments

- *double* **value** - Level-of-detail target, in pixels.

## double getCulledScreenSpaceError ( )

Returns the level-of-detail target for the tiles that are kept but not seen: those outside the frustum when frustum culling is off, and those hidden by fog when fog culling is off. It is meant to be coarser than the main target, so that such tiles are held at a cheap level of detail.
### Return value

Level-of-detail target for the culled tiles, in pixels.
## void setCulledScreenSpaceError ( double value )

Sets the level-of-detail target for the tiles that are kept but not seen: those outside the frustum when frustum culling is off, and those hidden by fog when fog culling is off. It is meant to be coarser than the main target, so that such tiles are held at a cheap level of detail.
### Arguments

- *double* **value** - Level-of-detail target for the culled tiles, in pixels.

## bool isFrustumCullingEnabled ( )

Returns a value indicating if the tiles outside the camera frustum are dropped instead of being kept at the culled level of detail. Culling saves memory and bandwidth; keeping the tiles means a turn of the camera finds coarse tiles already there instead of an empty area being streamed in.
### Return value

true if the tiles outside the camera frustum are dropped; otherwise, false.
## void setFrustumCullingEnabled ( bool enabled )

Sets a value indicating if the tiles outside the camera frustum are dropped instead of being kept at the culled level of detail.
### Arguments

- *bool* **enabled** - true to drop the tiles outside the camera frustum; false to keep them at the culled level of detail.

## bool isFogCullingEnabled ( )

Returns a value indicating if the tiles far enough away to be hidden by fog are dropped instead of being kept at the culled level of detail.
### Return value

true if the tiles hidden by fog are dropped; otherwise, false.
## void setFogCullingEnabled ( bool enabled )

Sets a value indicating if the tiles far enough away to be hidden by fog are dropped instead of being kept at the culled level of detail.
### Arguments

- *bool* **enabled** - true to drop the tiles hidden by fog; false to keep them at the culled level of detail.

## bool isTerrainWaterMaskEnabled ( )

Returns a value indicating if the water mask supplied inside quantized-mesh terrain tiles is used, so that oceans and lakes are shaded as water on the streamed terrain. Has no effect without an enabled terrain asset; it is unrelated to the global water object, which is disabled in globe mode.
### Return value

true if the water mask of the terrain tiles is used; otherwise, false.
## void setTerrainWaterMaskEnabled ( bool enabled )

Sets a value indicating if the water mask supplied inside quantized-mesh terrain tiles is used, so that oceans and lakes are shaded as water on the streamed terrain.
### Arguments

- *bool* **enabled** - true to use the water mask supplied inside terrain tiles; false to ignore it.

## int getTileViewportMask ( )

Returns the viewport mask assigned to the nodes the streamed tiles are rendered as, defining which viewports the tiles are rendered into.
### Return value

Viewport mask assigned to the tile nodes.
## void setTileViewportMask ( int mask )

Sets the viewport mask assigned to the nodes the streamed tiles are rendered as, defining which viewports the tiles are rendered into. The mask is applied to every tile.
### Arguments

- *int* **mask** - Viewport mask; 0 switches the tiles out of rendering entirely.

## int getTileShadowMask ( )

Returns the shadow mask assigned to the nodes the streamed tiles are rendered as, defining whether the tiles cast shadows from a light source.
### Return value

Shadow mask assigned to the tile nodes.
## void setTileShadowMask ( int mask )

Sets the shadow mask assigned to the nodes the streamed tiles are rendered as, defining whether the tiles cast shadows from a light source. The mask is applied to every tile.
### Arguments

- *int* **mask** - Shadow mask; 0 disables shadow casting for the tiles.

## int getTileIntersectionMask ( )

Returns the intersection mask assigned to the nodes the streamed tiles are rendered as, used by ray casts against the world (height-above-terrain requests among them).
### Return value

Intersection mask assigned to the tile nodes.
## void setTileIntersectionMask ( int mask )

Sets the intersection mask assigned to the nodes the streamed tiles are rendered as, used by ray casts against the world (height-above-terrain requests among them). The mask is applied to every tile.
### Arguments

- *int* **mask** - Intersection mask; 0 excludes the tiles from intersection tests.

## int getTileCollisionMask ( )

Returns the collision mask assigned to the nodes the streamed tiles are rendered as, used by the collision detection of the engine. Off by default: a globe streamed at run time is not a stable surface to build physics on, and the ground a simulation lands on is normally a terrain inset.
### Return value

Collision mask assigned to the tile nodes.
## void setTileCollisionMask ( int mask )

Sets the collision mask assigned to the nodes the streamed tiles are rendered as, used by the collision detection of the engine. The mask is applied to every tile.
### Arguments

- *int* **mask** - Collision mask; 0 excludes the tiles from collision detection.

## int getTilePhysicsIntersectionMask ( )

Returns the physics intersection mask assigned to the nodes the streamed tiles are rendered as. Off by default: a globe streamed at run time is not a stable surface to build physics on.
### Return value

Physics intersection mask assigned to the tile nodes.
## void setTilePhysicsIntersectionMask ( int mask )

Sets the physics intersection mask assigned to the nodes the streamed tiles are rendered as. The mask is applied to every tile.
### Arguments

- *int* **mask** - Physics intersection mask; 0 excludes the tiles from physics intersections.

## int getMaxMemoryUsageMb ( )

Returns the upper limit, in megabytes, for the tiles kept in memory.
### Return value

Upper limit for the tiles kept in memory, in megabytes.
## void setMaxMemoryUsageMb ( int value )

Sets the upper limit, in megabytes, for the tiles kept in memory.
### Arguments

- *int* **value** - Upper limit for the tiles kept in memory, in megabytes.

## double getTileCacheUnloadTimeLimitMs ( )

Returns the per-frame time budget for unloading tiles, in milliseconds. Raising it frees memory faster at the cost of frame time.
### Return value

Per-frame time budget for unloading tiles, in milliseconds.
## void setTileCacheUnloadTimeLimitMs ( double value )

Sets the per-frame time budget for unloading tiles, in milliseconds. Raising it frees memory faster at the cost of frame time.
### Arguments

- *double* **value** - Per-frame time budget for unloading tiles, in milliseconds.

## int getLogLevel ( )

Returns the verbosity level of the plugin diagnostics. The default level is info.
### Return value

Verbosity level of the plugin diagnostics, one of the *LOG_LEVEL_** values.
## void setLogLevel ( int level )

Sets the verbosity level of the plugin diagnostics.
### Arguments

- *int* **level** - Verbosity level, one of the *LOG_LEVEL_** values.

## bool load ( )

Reads the configuration from the configuration file. Loading does not apply the streaming changes by itself: call the plugin's *applyConfig()* for that.
### Return value

true if the configuration is read successfully; otherwise, false.
## bool save ( )

Persists the current state of the configuration to the configuration file. Call it before applying the changes to make them persistent; omit it for a change that should die with the application.
### Return value

true if the configuration is saved successfully; otherwise, false.
