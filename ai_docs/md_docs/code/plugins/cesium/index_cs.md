# Cesium Plugin (CS)


Real-world planet data covers the whole Earth and is far too large to be loaded at once. The **Cesium** plugin is a [3D Tiles](https://github.com/CesiumGS/3d-tiles) client: it streams elevation, imagery and pre-textured geometry from [Cesium ion](https://cesium.com/platform/cesium-ion/) for wherever the camera is, and renders them on a globe inside UNIGINE.


Rendering a planet in a Cartesian scene is a precision problem, so the plugin maintains a moving local origin - an [anchor](../../../code/plugins/cesium/index_cs.md#anchor) - shared with *[Geodetics](../../../code/plugins/geodetics/index_cs.md)*, and can swap in [high-detail terrain insets](../../../code/plugins/cesium/insets.md) at chosen locations.


### See also


- *[Cesium Plugin Configuration](../../../code/plugins/cesium/config.md)*
- *[Cesium ion Assets](../../../code/plugins/cesium/assets.md)*
- *[Terrain Insets](../../../code/plugins/cesium/insets.md)*
- *[Cesium Editor Plugin](../../../code/plugins/cesium/editor_plugin.md)*
- *[Cesium](../../../sdk/demos/cesium_ig.md)* demo


## Launching Cesium Plugin


To use the *Cesium* plugin, specify the `extern_plugin` command line option on the application start-up:


```bash
main_x64 -extern_plugin "UnigineIG,UnigineCesium,UnigineCIGIConnector"
```


> **Warning:** In an IG application, *Cesium* must be loaded **before** *CIGIConnector*, otherwise the first start-up packets sent by the host can be lost.


A connector that is loaded on the command line opens its connection during its first frame, whether or not the application is ready for a host to start driving it. An application that decides between a host-driven and a standalone session at run time can leave *CIGIConnector* out of the list and load it when the session actually starts, which is what the [Cesium](../../../sdk/demos/cesium_ig.md) demo does - the load order above then takes care of itself.


The plugin always loads, even without an access token or a usable data source. In that case the globe stays idle, which is a normal state rather than an error: the plugin can be configured from the [editor panel](../../../code/plugins/cesium/editor_plugin.md) and brought up afterwards.


## How It Works


### Tile Streaming


The dataset is served as a tree of tiles: coarse at the root, each tile splitting into finer children down to street-level detail. The client estimates how large a tile would appear on screen, streams in only the tiles fine enough to matter for the current view, and drops them again as the camera moves away. The level of detail is controlled by the screen-space error target, [max_screen_space_error](../../../code/plugins/cesium/config.md#streaming): lower values mean finer tiles, more streaming and more memory.


### Earth-Centred Coordinates


Cesium positions data in Earth-centered, Earth-fixed (ECEF) coordinates: a single frame with its origin at the center of the Earth and axes locked to the planet, so every point on Earth has one exact position. This is the correct way to describe a globe, and unsuitable for rendering directly.


### The Precision Problem


A scene is rendered in local coordinates using floating-point numbers, which lose precision the further they get from the origin. In ECEF the origin is the center of the Earth, so every point on the surface lies about 6378 km away from it, and at that distance the error grows to meters - enough to make geometry visibly jitter.


In a conventional flat world the origin sits inside the scene, so the content stays close to it and the error remains negligible. A globe has no such low-error region: there is nothing near the origin to work with, because the origin is a point no camera or object ever occupies. This is why a moving local origin is required rather than merely useful.


> **Notice:** A double-precision build of the engine is required for a georeferenced globe.


### Floating Origin and the Anchor


The plugin keeps a local frame whose origin sits on the surface near the camera, converts ECEF data into that frame for rendering, and moves the origin as the camera travels. This is called **rebasing**, and the geodetic position of that local origin is the **anchor**.


The anchor is owned by *[Geodetics](../../../code/plugins/geodetics/index_cs.md)* and driven by *Cesium*. Everything that lives in the local frame - entities, cameras, weather - must recompute its position from geodetic coordinates whenever the anchor moves, by subscribing to the anchor-changed event - *[Geodetics.Anchor.EventChanged](../../../api/library/geodetics/geodetics_plugin/class.anchor_cs.md#EventChanged)*. In an IG application this is already handled: IG places its entities and cameras through the anchor, and Weather repositions the sky, sun and clouds on the same event.


> **Warning:** If a system placed in the local frame does not follow the anchor, its content drifts away from the terrain or jumps when the world rebases.


## Using the Plugin in Your Own Application


The plugin does not assume that it owns the camera or the anchor. A host application declares its role once, at start-up:


```csharp
using Unigine;
using Unigine.Plugins;

private void InitCesium()
{
    // Cesium drives the anchor, so the world scan must not stamp a static
    // georeference over it on world load.
    Geodetics.Converter.AutoWorldInit = false;

    // ...which leaves nobody to establish a frame, and the start world carries
    // no georeferenced terrain anyway. So declare the starting one here: the
    // orbital frame, world == geocentric, the whole planet in view.
    Geodetics.Converter.GetAnchor().Reset();

    // A Syncker slave follows the anchor written into Geodetics from the
    // master's synced value instead of deciding its own rebases.
    if (!IG.Manager.IsMaster)
        Cesium.AnchorAutoUpdate = false;
}

```


The camera to follow is supplied every frame - and only once it is the camera actually being rendered through:


```csharp
private void Update()
{
    IG.View view = IG.Manager.GetView(IG.Manager.CurrentView, false);

    // IG creates its views at session start but enables none until a session is
    // running, so hand the plugin nothing rather than a parked dummy camera
    Cesium.Player = view != null && view.Enabled ? view.GetPlayer() : null;

    // and nothing else to the player from here: the depth range belongs to the
    // view definition, not to this call site - see below
}

```


> **Notice:** Passing a camera that is not being rendered through is worse than passing none: with no anchor set yet, the world origin is the centre of the Earth, and the plugin streams tiles around that point for nobody to look at.


The depth range itself is declared through *[IG.View.SetDefinition()](../../../api/library/plugins/ig/api/class.view_cs.md#setDefinition_float_float_float_float_float_float_void)*, which keeps the aspect ratio and replicates to [Syncker](../../../code/plugins/syncker/index.md) slaves. A fixed pair of planes works, but the range can also follow the camera - the [Cesium](../../../sdk/demos/cesium_ig.md) demo derives the far plane from the distance to the horizon at the current altitude, with a floor of 4000 km and a margin above the geometric value, sets the near plane to a small fraction of it, and re-declares the view only when the window size or the depth range has actually moved, since the call goes over the network:


```csharp
double altitude = Math.Max(spectator.GetAltitude(), 0.0);
float zfar = (float)Math.Max(VIEW_FAR_FLOOR_M, VIEW_FAR_MARGIN
    * Math.Sqrt(2.0 * Geodetics.Converter.WGS84_MAJOR_AXIS * altitude + altitude * altitude));
float znear = Math.Max(1.0f, zfar / VIEW_NEAR_FAR_RATIO);

view.SetDefinition(znear, zfar, -right_deg, right_deg, top_deg, -top_deg);

```


The following rules follow from this:


| Rule | If it is not followed |
|---|---|
| Supply a player every frame via *[Player](../../../api/library/plugins/cesium/class.cesium_cs.md#Player)*. | The plugin has no camera, the anchor never moves, and nothing rebases. |
| Call *[AnchorAutoUpdate = false](../../../api/library/plugins/cesium/class.cesium_cs.md#AnchorAutoUpdate)* on a follower, such as a [Syncker](../../../code/plugins/syncker/index.md) slave. | The follower runs its own rebase logic and fights the anchor set externally. |
| Call *[AutoWorldInit = false](../../../api/library/geodetics/geodetics_plugin/class.converter_cs.md#AutoWorldInit)* on the *Geodetics* converter, and only when Cesium drives the anchor. | Loading a world overwrites the anchor with a static georeference. Conversely, an application without Cesium that disables it never georeferences its worlds at all. |
| Establish the starting frame yourself once the world scan has been switched off - *[Reset()](../../../api/library/geodetics/geodetics_plugin/class.anchor_cs.md#reset_void)* on the *Geodetics* anchor declares the orbital one. | Nothing defines a frame, since the scan is what normally does it, and a start world with no georeferenced terrain has nothing to define one from. The plugin then streams nothing at all. |
| Open the frustum up to planetary distances - in an IG application through the *[*IG.View*](../../../api/library/plugins/ig/api/class.view_cs.md)* definition rather than on the player. | The globe is clipped away when seen from orbit, so the far plane has to reach thousands of kilometres while the near plane stays at a metre or more for the depth buffer to remain usable at that range. Setting the two on the player every frame additionally throws IG's own frustum away, because *[Camera](../../../api/library/rendering/class.camera_cs.md)* rebuilds its projection at a 1:1 aspect. |


## Applying Changes and Reading State


The configuration is available at run time through *[Cesium.GetConfig()](../../../api/library/plugins/cesium/class.cesium_cs.md#getConfig_CesiumConfig)*. After editing it, call *[ApplyConfig()](../../../api/library/plugins/cesium/class.cesium_cs.md#applyConfig_bool)* for the change to take effect. Settings the tilesets read (access token, asset list, **streaming**, **tile_masks**, **cache**) rebuild them, so every loaded tile is dropped and the globe is streamed again; the rest (inset list and log level) are applied at once. Call *[Save()](../../../api/library/plugins/cesium/class.cesiumconfig_cs.md#save_bool)* on the configuration first to make the change persistent - omit it for a change that should die with the application.


```csharp
CesiumConfig config = Cesium.GetConfig();

// AddAsset() appends an empty entry and returns its index; AddInset() does the same
int index = config.AddAsset();
config.SetAssetName(index, "OSM Buildings");
config.SetAssetType(index, CesiumConfig.ASSET_TYPE.TILES_3D);
config.SetAssetSource(index, CesiumConfig.ASSET_SOURCE.CESIUM_ION);
config.SetAssetIonId(index, 96188);
config.SetAssetEnabled(index, true);

config.Save();                             // persist to the configuration file
bool streaming = Cesium.ApplyConfig();     // rebuild the tilesets

```


Streaming statistics are available as *[NumRenderTiles](../../../api/library/plugins/cesium/class.cesium_cs.md#NumRenderTiles)*, *[NumLoadedTiles](../../../api/library/plugins/cesium/class.cesium_cs.md#NumLoadedTiles)*, *[NumLoadingTiles](../../../api/library/plugins/cesium/class.cesium_cs.md#NumLoadingTiles)*, *[LoadProgress](../../../api/library/plugins/cesium/class.cesium_cs.md#LoadProgress)* and *[UsedMemoryMb](../../../api/library/plugins/cesium/class.cesium_cs.md#UsedMemoryMb)*. Three more report what the traversal did rather than what is on screen: *[NumVisitedTiles](../../../api/library/plugins/cesium/class.cesium_cs.md#NumVisitedTiles)*, *[NumCulledTiles](../../../api/library/plugins/cesium/class.cesium_cs.md#NumCulledTiles)* and *[MaxTileDepth](../../../api/library/plugins/cesium/class.cesium_cs.md#MaxTileDepth)*.


> **Notice:** *[IsStreaming](../../../api/library/plugins/cesium/class.cesium_cs.md#IsStreaming)* reports that the globe has what it needs and its tilesets are built. It does not report that tiles are arriving - that can only be judged from the tile counters, since the plugin is ready before a world exists and before the first tile has been requested.


The debug overlay - the tile bounding volumes and the inset bounds - is a separate case. It is not a part of the [configuration](../../../code/plugins/cesium/config.md) and is never saved: *[RenderTileBounds()](../../../api/library/plugins/cesium/class.cesium_cs.md#renderTileBounds_int_void)* requests it for one frame at a time, so the application calls it every frame while the bounds should stay on screen, and stops calling it to hide them. Drawing goes through the engine visualizer, which the application has to enable itself:


```csharp
private void Update()
{
    // with the engine visualizer enabled (show_visualizer 1)
    Cesium.RenderTileBounds();
}

```


## Insets at Run Time


The [terrain insets](../../../code/plugins/cesium/insets.md) listed in the configuration are registered when the plugin is initialized and re-registered whenever the configuration is applied, and are addressed by index: *[NumInsets](../../../api/library/plugins/cesium/class.cesium_cs.md#NumInsets)*, *[GetInsetNode()](../../../api/library/plugins/cesium/class.cesium_cs.md#getInsetNode_int_Node)*, *[GetInsetGeoPosition()](../../../api/library/plugins/cesium/class.cesium_cs.md#getInsetGeoPosition_int_dvec3_bool)* and *[GetInsetStatus()](../../../api/library/plugins/cesium/class.cesium_cs.md#getInsetStatus_int_int)*.


A registered inset is not necessarily a usable one: the world may be unreadable, or its terrain may not meet the [requirements](../../../code/plugins/cesium/insets.md). *[GetInsetStatus()](../../../api/library/plugins/cesium/class.cesium_cs.md#getInsetStatus_int_int)* answers which of the two it is, as one of the *[INSET_STATUS.*](../../../api/library/plugins/cesium/class.cesium_cs.md#INSET_STATUS_OK)* values.


The same check is available for a world or a node that has not been registered - *[CheckInsetWorld()](../../../api/library/plugins/cesium/class.cesium_cs.md#checkInsetWorld_cstr_int)* and *[CheckInsetNode()](../../../api/library/plugins/cesium/class.cesium_cs.md#checkInsetNode_Node_int)* - which is what the [editor panel](../../../code/plugins/cesium/editor_plugin.md) reports beside an inset in its list.


Activation follows the camera, and can also be driven by the application: *[FindNearbyInset()](../../../api/library/plugins/cesium/class.cesium_cs.md#findNearbyInset_dvec3_int)* returns the inset registered near a geodetic position, *[SetActiveInset()](../../../api/library/plugins/cesium/class.cesium_cs.md#setActiveInset_int_bool)* swaps one in by index, *[SetCustomActiveInset()](../../../api/library/plugins/cesium/class.cesium_cs.md#setCustomActiveInset_Node_bool)* does the same for a terrain node of your own, and *[ClearActiveInset()](../../../api/library/plugins/cesium/class.cesium_cs.md#clearActiveInset_void)* drops back to the streamed globe. *[HasActiveInset()](../../../api/library/plugins/cesium/class.cesium_cs.md#hasActiveInset_bool)*, *[IsInsetActive()](../../../api/library/plugins/cesium/class.cesium_cs.md#isInsetActive_int_bool)* and *[ActiveInsetIndex](../../../api/library/plugins/cesium/class.cesium_cs.md#ActiveInsetIndex)* report the current state.


> **Notice:** An inset can only be swapped in while this plugin drives the anchor. A follower - a [Syncker](../../../code/plugins/syncker/index.md) slave, or an application that sets the anchor itself - has to place the frame at the inset first, otherwise the activation is refused and the reason is logged.


Loading the inset worlds is the plugin's job by default. *[UseConfigInsets](../../../api/library/plugins/cesium/class.cesium_cs.md#UseConfigInsets)* switches that off, for an application that wants to decide itself which terrain is swapped in and when, through *[SetCustomActiveInset()](../../../api/library/plugins/cesium/class.cesium_cs.md#setCustomActiveInset_Node_bool)*. This is what the [editor plugin](../../../code/plugins/cesium/editor_plugin.md) does to preview the terrain of whatever world is open. A registered inset whose world was never loaded cannot be activated, and says so:


```text
Cesium(InsetController): inset '<name>' has no terrain (the config's insets are switched off, or its world could not be loaded).

```


## Limitations


| Limitation | Details |
|---|---|
| One ground surface | At most one enabled terrain asset is used. See [Cesium ion Assets](../../../code/plugins/cesium/assets.md). |
| One active inset | Only one [terrain inset](../../../code/plugins/cesium/insets.md) can be swapped in at a time. It is chosen by camera proximity, and can also be [set by the application](../../../code/plugins/cesium/index_cs.md#insets_api). |
| Cesium ion only | Custom data sources - a direct tileset URL or a local path - are not supported yet. |
| No water on the globe | Global water is disabled in globe mode. The [terrain water mask](../../../code/plugins/cesium/config.md#streaming) still shades water areas on the streamed terrain. |
| Haze disabled by default | Flat-world haze draws as a hard band across the horizon on a globe. It can be re-enabled in the [weather configuration](../../../ig/weather/config_cs.md). |
