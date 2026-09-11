# Unigine.Landscape Class (CS)

> **Notice:** This class is a singleton.


This class is used to manage landscape terrain rendering and modification.


Terrain modification is performed in asynchronous mode on GPU side by calling a corresponding method, that commences a drawing operation. When calling such a method you should specify the GUID of an `.lmap` file [landscape layer map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md) to be modified, the coordinates of the upper-left corner and the resolution of the segment of data to be modified, you should also define which data layers are to be affected (heights, albedo, masks) via a set of [flags](#FLAGS_FILE_DATA_HEIGHT). The operation itself is to be implemented inside a callback handler.


### GPU-Based Terrain Modification


The workflow is as follows:


1. Implement your GPU-based terrain modification logic in a function.
2. Set this handler function when subscribing for the *Texture Draw* event (when GPU-based terrain modification operation is performed) via *[EventTextureDraw](#EventTextureDraw)*.
3. Commence a GPU drawing operation by calling the [*AsyncTextureDraw()*](#asyncTextureDraw_UGUID_ivec2_ivec2_int_void) method. Here you should specify the GUID of an `.lmap` file [landscape layer map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md) to be modified, the coordinates of the upper-left corner and the resolution of the segment of data to be modified, you should also define which data layers are to be affected (heights, albedo, masks) via a set of [flags](#FLAGS_FILE_DATA_HEIGHT). > **Notice:** In case your modification requires additional data beyond the specified area as well as the data of other landscape layer maps (e.g. a copy brush) you can enable force loading of required data, in this case you should use [this overload of the *AsyncTextureDraw()* method](#asyncTextureDraw_UGUID_ivec2_ivec2_int_VECWorldBoundBox_void).


```csharp
// GPU-based modification
void my_texture_draw(UGUID guid, int id, LandscapeTextures buffer, ivec2 coord, int data_mask)
{
	// getting the desired brush material (built - in "cirle_soft" Editor's brush) and inheriting a child material from it
	UGUID file_guid = FileSystem.GetGUID(FileSystem.ResolvePartialVirtualPath("circle_soft.brush"));
	if (!file_guid.IsValid())
	{
		Log.Warning("LandscapePainter Init(): can not find \"circle_soft.brush\" material\n");
		return;
	}

	brush_material = Materials.FindMaterialByFileGUID(file_guid).Inherit();

	// setting necessary textures (e.g., albedo and heights)
	brush_material.SetTexture("terrain_albedo", buffer.Albedo);
	brush_material.SetTexture("terrain_height", buffer.Height);

	// setting up brush material parameters (size, color, etc. and specifying masks to be affected by the brush)
	brush_material.SetParameterFloat("size", 10.0f);
	brush_material.SetParameterFloat("height", 1.0f);
	brush_material.SetParameterFloat4("color", vec4.GREEN);
	brush_material.SetParameterInt("data_mask", data_mask);

	// running material's "brush" expression
	brush_material.RunExpression("brush", buffer.Resolution.x, buffer.Resolution.y);

	// resetting material textures
	brush_material.SetTexture("terrain_albedo", null);
	brush_material.SetTexture("terrain_height", null);

}

// ...

private void Init()
{
	// getting an existing landscape terrain object
	ObjectLandscapeTerrain terrain = Landscape.GetActiveTerrain();

	// getting the first layermap that we're going to modify
	lmap = terrain.GetChild(0) as LandscapeLayerMap;

	// adding a handler function to be executed on a Texture Draw operation
	Landscape.EventTextureDraw.Connect(texture_draw_connections, my_texture_draw);

	// generating a new ID for the draw operation
	int id = Landscape.GenerateOperationID();
	// user's code (bounding to ID)

	// commencing a Texture Draw operation for the selected landscape map at (1, 1) with the size of [32 x 32]
	Landscape.AsyncTextureDraw(id, lmap.GetGUID(), new ivec2(1, 1),
					new ivec2(32, 32), (int)(Landscape.FLAGS_DATA.HEIGHT | Landscape.FLAGS_DATA.ALBEDO));

	return;
}

// ...

private void Shutdown()
{
	// removing all subscriptions for the TextureDraw event
	texture_draw_connections.DisconnectAll();
}


```


And the process:


1. After commencing of a terrain modification operation with all necessary parameters specified, the Engine copies a fragment of terrain data from the specified [landscape layer map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md) file at the specified coordinates to a buffer ([*LandscapeTextures*](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cs.md)) of the specified resolution.
2. Upon completion of the copying process a handler function which you used to subscribe for the *[TextureDraw](#EventTextureDraw)* event is executed. This function modifies the buffer.
3. After this selected data layers of the modified buffer are pasted back to the [landscape layer map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md) file.


##### Usage Example: Brush Editor


Below is a C# component implementing brush-based *Landscape Terrain* modification.


<details>
<summary>LandscapeBrush.cs | Close</summary>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class LandscapeBrush : Component
{
	public float brush_size = 10.0f;
	public float brush_height = 1.0f;
	private Material brush_material;
	private LandscapeLayerMap lmap;
	private Player player;
	private LandscapeFetch landscape_fetch;
	private EventConnections texture_draw_connections = new EventConnections();
	// GPU-based modification
	void my_texture_draw(UGUID guid, int id, LandscapeTextures buffer, ivec2 coord, int data_mask)
	{
		// setting necessary textures (e.g., albedo and heights)
		brush_material.SetTexture("terrain_albedo", buffer.Albedo);
		brush_material.SetTexture("terrain_height", buffer.Height);

		// setting up brush material parameters (size, color, etc. and specifying masks to be affected by the brush)
		brush_material.SetParameterFloat("size", brush_size);
		brush_material.SetParameterFloat("height", brush_height);
		brush_material.SetParameterFloat4("color", vec4.GREEN);
		brush_material.SetParameterInt("data_mask", data_mask);

		// running material's "brush" expression
		brush_material.RunExpression("brush", buffer.Resolution.x, buffer.Resolution.y);

		// resetting material textures
		brush_material.SetTexture("terrain_albedo", null);
		brush_material.SetTexture("terrain_height", null);
	}
	private void Init()
	{
		// write here code to be called on component initialization
		// getting the desired brush material (built - in "cirle_soft" Editor's brush) and inheriting a child material from it
		UGUID file_guid = FileSystem.GetGUID(FileSystem.ResolvePartialVirtualPath("circle_soft.brush"));
		if (!file_guid.IsValid())
		{
			Log.Warning("LandscapePainter Init(): can not find \"circle_soft.brush\" material\n");
			return;
		}

		brush_material = Materials.FindMaterialByFileGUID(file_guid).Inherit();

		// getting an existing landscape terrain object
		ObjectLandscapeTerrain terrain = Landscape.GetActiveTerrain();

		// getting the first layermap that we're going to modify
		lmap = terrain.GetChild(0) as LandscapeLayerMap;

		// adding a handler function to be executed on a Texture Draw operation
		Landscape.EventTextureDraw.Connect(texture_draw_connections, my_texture_draw);

		// setting the mouse handling mode to USER to display the cursor on the screen
		ControlsApp.MouseHandle = Input.MOUSE_HANDLE.USER;

		player = Game.Player;
	}

	private void Update()
	{
		// write here code to be called before updating each render frame
		// if right mouse button is clicked
		if (Input.IsMouseButtonDown(Input.MOUSE_BUTTON.RIGHT))
		{
			landscape_fetch = new LandscapeFetch();
			// getting direction from the current mouse position
			ivec2 mouse = Input.MousePosition;
			vec3 dir = player.GetDirectionFromMainWindow(mouse.x, mouse.y);
			// fetching the coordinates of the point of intersection
			bool fetched = landscape_fetch.IntersectionForce(player.Position,
			new vec3(player.Position + dir * 10000.0));

			if (fetched)
			{
				// getting the local position of the brush relative to the layer map
				vec3 brush_local_position = new vec3(lmap.IWorldTransform * landscape_fetch.Position);

				// calculating the bound of the layer map area to be affected by the brush
				float half_size = brush_size / 2.0f;
				vec3[] brush_local_corners = new vec3[] {
					brush_local_position + new vec3(-half_size, -half_size, 0.0),
					brush_local_position + new vec3(half_size, -half_size, 0.0),
					brush_local_position + new vec3(-half_size,  half_size, 0.0),
					brush_local_position + new vec3(half_size,  half_size, 0.0)
				};
				vec2 brush_local_bbox_min = new vec2(
					MathLib.Min(MathLib.Min(brush_local_corners[0].x, brush_local_corners[1].x), MathLib.Min(brush_local_corners[2].x, brush_local_corners[3].x)),
					MathLib.Min(MathLib.Min(brush_local_corners[0].y, brush_local_corners[1].y), MathLib.Min(brush_local_corners[2].y, brush_local_corners[3].y))
				);
				vec2 brush_local_bbox_max = new vec2(
					MathLib.Max(MathLib.Max(brush_local_corners[0].x, brush_local_corners[1].x), MathLib.Max(brush_local_corners[2].x, brush_local_corners[3].x)),
					MathLib.Max(MathLib.Max(brush_local_corners[0].y, brush_local_corners[1].y), MathLib.Max(brush_local_corners[2].y, brush_local_corners[3].y))
				);

				// calculating the number of pixels per unit length
				vec2 pixels_per_unit = new vec2(lmap.Resolution / lmap.Size);

				// calculating the coordinates and the size of the region or the landscape layer texture to be modified
				ivec2 drawing_region_coord = new ivec2 (pixels_per_unit * brush_local_bbox_min);
				ivec2 drawing_region_size = new ivec2 (pixels_per_unit * (brush_local_bbox_max - brush_local_bbox_min) );

				// user's code (bounding to ID)
				int id = Landscape.GenerateOperationID();

				// commencing a Texture Draw operation for the selected landscape map for the region with the specified coords and size
				// affecting Height and Albedo data
				Landscape.AsyncTextureDraw(id, lmap.GetGUID(), drawing_region_coord,
					drawing_region_size, (int)(Landscape.FLAGS_DATA.HEIGHT | Landscape.FLAGS_DATA.ALBEDO));
			}

		}
	}
	private void Shutdown()
	{
		// removing all subscriptions for the TextureDraw event
		texture_draw_connections.DisconnectAll();
	}

}

```

</details>


### See also


- C++ sample
- C++ sample
- C++ sample


## Landscape Class

### Enums

## TYPE_DATA

| Name | Description |
|---|---|
| **HEIGHT** = 0 | Heights data type. |
| **ALBEDO** = 1 | Albedo data type. |
| **MASK_0** = 2 | Mask0 data type. |
| **MASK_1** = 3 | Mask1 data type. |
| **MASK_2** = 4 | Mask2 data type. |
| **MASK_3** = 5 | Mask3 data type. |
| **MASK_4** = 6 | Mask4 data type. |
| **MASK_5** = 7 | Mask5 data type. |
| **MASK_6** = 8 | Mask6 data type. |
| **MASK_7** = 9 | Mask7 data type. |
| **MASK_8** = 10 | Mask8 data type. |
| **MASK_9** = 11 | Mask9 data type. |
| **MASK_10** = 12 | Mask10 data type. |
| **MASK_11** = 13 | Mask11 data type. |
| **MASK_12** = 14 | Mask12 data type. |
| **MASK_13** = 15 | Mask13 data type. |
| **MASK_14** = 16 | Mask14 data type. |
| **MASK_15** = 17 | Mask15 data type. |
| **MASK_16** = 18 | Mask16 data type. |
| **MASK_17** = 19 | Mask17 data type. |
| **MASK_18** = 20 | Mask18 data type. |
| **MASK_19** = 21 | Mask19 data type. |

## FLAGS_DATA

| Name | Description |
|---|---|
| **HEIGHT** = 1 << 0 | Heights data flag. |
| **ALBEDO** = 1 << 1 | Albedo data flag. |
| **MASK_0** = 1 << 2 | Mask0 data flag. |
| **MASK_1** = 1 << 3 | Mask1 data flag. |
| **MASK_2** = 1 << 4 | Mask2 data flag. |
| **MASK_3** = 1 << 5 | Mask3 data flag. |
| **MASK_4** = 1 << 6 | Mask4 data flag. |
| **MASK_5** = 1 << 7 | Mask5 data flag. |
| **MASK_6** = 1 << 8 | Mask6 data flag. |
| **MASK_7** = 1 << 9 | Mask7 data flag. |
| **MASK_8** = 1 << 10 | Mask8 data flag. |
| **MASK_9** = 1 << 11 | Mask9 data flag. |
| **MASK_10** = 1 << 12 | Mask10 data flag. |
| **MASK_11** = 1 << 13 | Mask11 data flag. |
| **MASK_12** = 1 << 14 | Mask12 data flag. |
| **MASK_13** = 1 << 15 | Mask13 data flag. |
| **MASK_14** = 1 << 16 | Mask14 data flag. |
| **MASK_15** = 1 << 17 | Mask15 data flag. |
| **MASK_16** = 1 << 18 | Mask16 data flag. |
| **MASK_17** = 1 << 19 | Mask17 data flag. |
| **MASK_18** = 1 << 20 | Mask18 data flag. |
| **MASK_19** = 1 << 21 | Mask19 data flag. |

## TYPE_FILE_DATA

File data types.
| Name | Description |
|---|---|
| **HEIGHT** = 0 | Landscape map file heights data. |
| **ALBEDO** = 1 | Landscape map file albedo data. |
| **MASK_0** = 2 | Landscape map file detail mask data (masks with indices 0, 1, 2, 3). |
| **MASK_1** = 3 | Landscape map file detail mask data (masks with indices 4, 5, 6, 7). |
| **MASK_2** = 4 | Landscape map file detail mask data (masks 8, 9, 10, 11). |
| **MASK_3** = 5 | Landscape map file detail mask data (masks with indices 12, 13, 14, 15). |
| **MASK_4** = 6 | Landscape map file detail mask data (masks with indices 16, 17, 18, 19). |
| **OPACITY_HEIGHT** = 7 | Landscape map file height opacity data. |
| **OPACITY_MASK_0** = 8 | Landscape map file detail mask opacity data (masks with indices 0, 1, 2, 3). |
| **OPACITY_MASK_1** = 9 | Landscape map file detail mask opacity data (masks with indices 4, 5, 6, 7). |
| **OPACITY_MASK_2** = 10 | Landscape map file detail mask opacity data (masks with indices 8, 9, 10, 11). |
| **OPACITY_MASK_3** = 11 | Landscape map file detail mask opacity data (masks with indices 12, 13, 14, 15). |
| **OPACITY_MASK_4** = 12 | Landscape map file detail mask opacity data (masks with indices 16, 17, 18, 19). |

## FLAGS_FILE_DATA

File data layer flags.
| Name | Description |
|---|---|
| **HEIGHT** = 1 << 0 | Landscape map file height data. |
| **ALBEDO** = 1 << 1 | Landscape map file albedo data. |
| **MASK_0** = 1 << 2 | Landscape map file first masks data block (masks with indices 0,1,2,3). |
| **MASK_1** = 1 << 3 | Landscape map file second masks data block (masks with indices 4,5,6,7). |
| **MASK_2** = 1 << 4 | Landscape map file third masks data block (masks with indices 8,9,10,11). |
| **MASK_3** = 1 << 5 | Landscape map file fourth masks data block (masks with indices 12,13,14,15). |
| **MASK_4** = 1 << 6 | Landscape map file fifth masks data block (masks with indices 16,17,18,19). |
| **OPACITY_HEIGHT** = 1 << 7 | Landscape map file height opacity data. |
| **OPACITY_MASK_0** = 1 << 8 | Landscape map file first masks opacity data block (for masks with indices 0,1,2,3). |
| **OPACITY_MASK_1** = 1 << 9 | Landscape map file second masks opacity data block (for masks with indices 4,5,6,7). |
| **OPACITY_MASK_2** = 1 << 10 | Landscape map file third masks opacity data block (for masks with indices 8,9,10,11). |
| **OPACITY_MASK_3** = 1 << 11 | Landscape map file fourth masks opacity data block (for masks with indices 12,13,14,15). |
| **OPACITY_MASK_4** = 1 << 12 | Landscape map file fifth masks opacity data block (for masks with indices 16,17,18,19). |

## COMPRESSOR_TYPE

Compression method used for the layer map.
| Name | Description |
|---|---|
| **NONE** = 0 | No compression is used. |
| **JACKALLESS** = 1 | **Our Method** compression is used. It is optimized for compressing 2D and 3D textures and provides better results than **LZ4** and **Zlib** without deteriorating the quality. |
| **LZ4** = 2 | **LZ4** compression is used (temporary option, planned to be removed in the upcoming releases). |
| **ZLIB** = 3 | **Zlib** compression (can provide up to 2 times higher compression ratio, but takes up to 20 times longer). |

## BLENDING_MODE

Blending mode used for the layer map.
| Name | Description |
|---|---|
| **ALPHA_BLEND** = 0 | Alpha blending mode - the colors of the layer map and the underlying one are blended. |
| **ADDITIVE** = 1 | Additive blending mode - data of the layer map is added atop of the data of underlying maps. |
| **OVERLAY** = 2 | Overlay blending mode - data of the layer map replaces the data of underlying maps. |
| **MULTIPLICATIVE** = 3 | Multiplicative blending mode - albedo colors of the underlying map are multiplied by the colors of the layer map. |

### Properties

## 🔒︎ bool IsFilesClosed

The value indicating if `.lmap` files for all [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md) are closed. Call this method before making any changes (modification, deletion, renaming) to `.lmap` files of the landscape terrain object to ensure that these files are not currently used by the Engine to avoid conflicts. If not, you can use the [*filesClose()*](#filesClose_void) method co close them.
## 🔒︎ Event< UGUID , int, string, string> EventSaveFile

The Event triggered when applying changes made to a landscape layer map file and saving old and new states to temporary files. The signature of the event handler must be as follows:
```csharp
void savefile_handler(UGUID guid,  int operation_id,  string path_new_state,  string path_old_state)

```

 You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(UGUID **guid**, int **operation_id**, string **path_new_state**, string **path_old_state**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the SaveFile event handler
void savefile_event_handler(UGUID guid,  int operation_id,  string path_new_state,  string path_old_state)
{
	Log.Message("\Handling SaveFile event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections savefile_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Landscape.EventSaveFile.Connect(savefile_event_connections, savefile_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Landscape.EventSaveFile.Connect(savefile_event_connections, (UGUID guid,  int operation_id,  string path_new_state,  string path_old_state) => {
		Log.Message("Handling SaveFile event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
savefile_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the SaveFile event with a handler function
Landscape.EventSaveFile.Connect(savefile_event_handler);

// remove subscription to the SaveFile event later by the handler function
Landscape.EventSaveFile.Disconnect(savefile_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection savefile_event_connection;

// subscribe to the SaveFile event with a lambda handler function and keeping the connection
savefile_event_connection = Landscape.EventSaveFile.Connect((UGUID guid,  int operation_id,  string path_new_state,  string path_old_state) => {
		Log.Message("Handling SaveFile event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
savefile_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
savefile_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
savefile_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring SaveFile events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Landscape.EventSaveFile.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Landscape.EventSaveFile.Enabled = true;

```

</details>

## 🔒︎ Event< UGUID , int, string> EventApplyDiff

The Event triggered when applying a diff to the landscape layer map file. The signature of the event handler must be as follows:
```csharp
void applydiff_handler(UGUID guid,  int operation_id,  string lmap_file_path)

```

 You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(UGUID **guid**, int **operation_id**, string **lmap_file_path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the ApplyDiff event handler
void applydiff_event_handler(UGUID guid,  int operation_id,  string lmap_file_path)
{
	Log.Message("\Handling ApplyDiff event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections applydiff_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Landscape.EventApplyDiff.Connect(applydiff_event_connections, applydiff_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Landscape.EventApplyDiff.Connect(applydiff_event_connections, (UGUID guid,  int operation_id,  string lmap_file_path) => {
		Log.Message("Handling ApplyDiff event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
applydiff_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the ApplyDiff event with a handler function
Landscape.EventApplyDiff.Connect(applydiff_event_handler);

// remove subscription to the ApplyDiff event later by the handler function
Landscape.EventApplyDiff.Disconnect(applydiff_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection applydiff_event_connection;

// subscribe to the ApplyDiff event with a lambda handler function and keeping the connection
applydiff_event_connection = Landscape.EventApplyDiff.Connect((UGUID guid,  int operation_id,  string lmap_file_path) => {
		Log.Message("Handling ApplyDiff event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
applydiff_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
applydiff_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
applydiff_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring ApplyDiff events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Landscape.EventApplyDiff.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Landscape.EventApplyDiff.Enabled = true;

```

</details>

## 🔒︎ Event< UGUID , int, LandscapeTextures , ivec2, int> EventTextureDraw

The Event triggered when a Texture Draw (GPU-based terrain modification) operation is performed. The signature of the event handler must be as follows:
```csharp
void texturedraw_handler(UGUID guid,  int operation_id,  LandscapeTextures buffer,  ivec2 coords,  int data_mask)

```

 You can subscribe to events via *Connect()* �and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cs.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cs.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cs.md) article.

 The event handler signature is as follows: *myhandler(UGUID **guid**, int **operation_id**, LandscapeTextures **buffer**, ivec2 **coords**, int **data_mask**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the TextureDraw event handler
void texturedraw_event_handler(UGUID guid,  int operation_id,  LandscapeTextures buffer,  ivec2 coords,  int data_mask)
{
	Log.Message("\Handling TextureDraw event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections texturedraw_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
Landscape.EventTextureDraw.Connect(texturedraw_event_connections, texturedraw_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Landscape.EventTextureDraw.Connect(texturedraw_event_connections, (UGUID guid,  int operation_id,  LandscapeTextures buffer,  ivec2 coords,  int data_mask) => {
		Log.Message("Handling TextureDraw event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
texturedraw_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the TextureDraw event with a handler function
Landscape.EventTextureDraw.Connect(texturedraw_event_handler);

// remove subscription to the TextureDraw event later by the handler function
Landscape.EventTextureDraw.Disconnect(texturedraw_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection texturedraw_event_connection;

// subscribe to the TextureDraw event with a lambda handler function and keeping the connection
texturedraw_event_connection = Landscape.EventTextureDraw.Connect((UGUID guid,  int operation_id,  LandscapeTextures buffer,  ivec2 coords,  int data_mask) => {
		Log.Message("Handling TextureDraw event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
texturedraw_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
texturedraw_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
texturedraw_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring TextureDraw events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Landscape.EventTextureDraw.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
Landscape.EventTextureDraw.Enabled = true;

```

</details>

### Members

---

## bool TerrainLoad ( WorldBoundBox bb )

Loads terrain data (tiles) for all landscape layer maps within the specified bounding box to cache.
### Arguments

- *[WorldBoundBox](../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb** - Bounding box, defining landscape layer maps for which the data is to be loaded.

### Return value

true if terrain data was successfully loaded for all landscape layer maps within the specified bounding box; otherwise, false.
## bool Render ( LandscapeTextures buffers , mat4 transform , Scalar texel_size )

Renders the area of the specified landscape layer maps defined by the specified transform and texel size, to the specified [buffers](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cs.md).
### Arguments

- *[LandscapeTextures](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cs.md)* **buffers** - Target [texture buffers](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cs.md) to which the specified landscape layer maps are to be rendered.
- *mat4* **transform** - Transformation of the landscape terrain area to be rendered (Z-coordinate is ignored).
- *Scalar* **texel_size** - Texel size to be used. Defines the size of the area depending on the *buffers* resolution.

### Return value

true if the data of the landscape terrain area (all landscape layer maps) defined by the specified transformation and texel size, was successfully rendered to the specified buffers; otherwise, false.
## bool Render ( LandscapeTextures buffers , mat4 transform , Scalar texel_size , int padding )

Renders the area of the specified landscape layer maps defined by the specified transform and texel size, to the specified [buffers](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cs.md). Use the *padding* parameter to set inner padding size for the area (when necessary).
### Arguments

- *[LandscapeTextures](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cs.md)* **buffers** - Target [texture buffers](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cs.md) to which the specified landscape layer maps are to be rendered.
- *mat4* **transform** - Transformation of the landscape terrain area to be rendered (Z-coordinate is ignored).
- *Scalar* **texel_size** - Texel size to be used. Defines the size of the area depending on the *buffers* resolution.
- *int* **padding** - Inner padding size for the area to be rendered (if necessary).

### Return value

true if the data of the landscape terrain area (all landscape layer maps) defined by the specified transformation and texel size, was successfully rendered to the specified buffers; otherwise, false.
## bool Render ( LandscapeLayerMap [] maps , LandscapeTextures buffers , mat4 transform , Scalar texel_size )

Renders the area of the specified landscape layer maps defined by the specified transform and texel size, to the specified [buffers](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cs.md).
### Arguments

- *[LandscapeLayerMap](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md)[]* **maps** - List of the landscape layer maps to be rendered.
- *[LandscapeTextures](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cs.md)* **buffers** - Target [texture buffers](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cs.md) to which the specified landscape layer maps are to be rendered.
- *mat4* **transform** - Transformation of the landscape terrain area to be rendered (Z-coordinate is ignored).
- *Scalar* **texel_size** - Texel size to be used. Defines the size of the area depending on the *buffers* resolution.

### Return value

true if the data of the landscape terrain area (specified landscape layer maps) defined by the specified transformation and texel size, was successfully rendered to the specified buffers; otherwise, false.
## bool Render ( LandscapeLayerMap [] maps , LandscapeTextures buffers , mat4 transform , Scalar texel_size , int padding )

Renders the area of the specified landscape layer maps defined by the specified transform and texel size, to the specified [buffers](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cs.md). Use the *padding* parameter to set inner padding size for the area (when necessary).
### Arguments

- *[LandscapeLayerMap](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md)[]* **maps** - List of the landscape layer maps to be rendered.
- *[LandscapeTextures](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cs.md)* **buffers** - Target [texture buffers](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cs.md) to which the specified landscape layer maps are to be rendered.
- *mat4* **transform** - Transformation of the landscape terrain area to be rendered (Z-coordinate is ignored).
- *Scalar* **texel_size** - Texel size to be used. Defines the size of the area depending on the *buffers* resolution.
- *int* **padding** - Inner padding size for the area to be rendered.

### Return value

true if the data of the landscape terrain area (specified landscape layer maps) defined by the specified transformation and texel size, was successfully rendered to the specified buffers; otherwise, false.
## void AsyncTextureDraw ( int operation_id , UGUID file_guid , ivec2 coord , ivec2 resolution , int flags_file_data , WorldBoundBox [] bounds_preload_lmaps )

Commences an asynchronous GPU-based drawing operation with forced pre-loading of terrain data within the specified bounding box (all landscape layer maps). The drawing operation represents modification of the texture buffer of the specified size taken at specified coordinates and combining data layers defined by the specified flags. The operation itself is to be implemented in the [TextureDraw](#getEventTextureDraw_Event) event handler. This method can be used for implementing GPU-based terrain modification (e.g. brushes) that requires additional data beyond the area specified by *coords* and *resolution* parameters as well as the data of other [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md) (e.g. a copy brush).
### Arguments

- *int* **operation_id** - Draw [operation ID](#generateOperationID_int).
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the landscape layer map file to be modified.
- *ivec2* **coord** - Coordinates of the upper left corner of the landscape layer map data segment to be modified along the X and Y axes.
- *ivec2* **resolution** - Resolution of the landscape layer map data segment to be modified along the X and Y axes, the value within range [0, 4096] along each axis.
- *int* **flags_file_data** - Data layer mask. A combination of [FLAGS_FILE_DATA_*](#FLAGS_FILE_DATA_HEIGHT) flags indicating data layers to be affected (heights, albedo, certain masks).
- *[WorldBoundBox](../../../../api/library/math/cs/bounds/worldboundbox_cs.md)[]* **bounds_preload_lmaps** - [Bounding box](../../../../api/library/math/bounds/class.worldboundbox_cs.md) (world) specifying the area containing terrain tiles (all landscape layer maps) to be loaded to memory prior to making modifications.

## void AsyncTextureDraw ( int operation_id , UGUID file_guid , ivec2 coord , ivec2 resolution , int flags_file_data )

Commences an asynchronous GPU-based drawing operation. The drawing operation represents modification of the texture buffer of the specified size taken at specified coordinates and combining data layers defined by the specified flags. The operation itself is to be implemented in the [TextureDraw](#getEventTextureDraw_Event) event handler. This method can be used for implementing GPU-based terrain modification (e.g. brushes).
### Arguments

- *int* **operation_id** - Draw [operation ID](#generateOperationID_int).
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the landscape layer map file to be modified.
- *ivec2* **coord** - Coordinates of the upper left corner of the landscape layer map data segment to be modified along the X and Y axes.
- *ivec2* **resolution** - Resolution of the landscape layer map data segment to be modified along the X and Y axes, the value within range [0, 4096] along each axis.
- *int* **flags_file_data** - Data layer mask. A combination of [FLAGS_FILE_DATA_*](#FLAGS_FILE_DATA_HEIGHT) flags indicating data layers to be affected (heights, albedo, certain masks).

## void AsyncTextureDraw ( int operation_id , UGUID file_guid , ivec2 coord , ivec2 resolution )

Commences an asynchronous GPU-based drawing operation. The drawing operation represents modification of the texture buffer of the specified size taken at specified coordinates and combining all data layers. The operation itself is to be implemented in the [TextureDraw](#getEventTextureDraw_Event) event handler. This method can be used for implementing GPU-based terrain modification (e.g. brushes).
### Arguments

- *int* **operation_id** - Draw [operation ID](#generateOperationID_int).
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the landscape layer map file to be modified.
- *ivec2* **coord** - Coordinates of the upper left corner of the landscape layer map data segment to be modified along the X and Y axes.
- *ivec2* **resolution** - Resolution of the landscape layer map data segment to be modified along the X and Y axes, the value within range [0, 4096] along each axis.

## void AsyncTextureDraw ( UGUID file_guid , ivec2 coord , ivec2 resolution , int flags_file_data , WorldBoundBox [] bounds_preload_lmaps )

Commences an asynchronous GPU-based drawing operation with forced pre-loading of terrain data within the specified bounding box (all landscape layer maps). The drawing operation represents modification of the texture buffer of the specified size taken at specified coordinates and combining data layers defined by the specified flags. The operation itself is to be implemented in the [TextureDraw](#getEventTextureDraw_Event) event handler. This method can be used for implementing GPU-based terrain modification (e.g. brushes) that requires additional data beyond the area specified by *coords* and *resolution* parameters as well as the data of other [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md) (e.g. a copy brush).
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the landscape layer map file to be modified.
- *ivec2* **coord** - Coordinates of the upper left corner of the landscape layer map data segment to be modified along the X and Y axes.
- *ivec2* **resolution** - Resolution of the landscape layer map data segment to be modified along the X and Y axes, the value within range [0, 4096] along each axis.
- *int* **flags_file_data** - Data layer mask. A combination of [FLAGS_FILE_DATA_*](#FLAGS_FILE_DATA_HEIGHT) flags indicating data layers to be affected (heights, albedo, certain masks).
- *[WorldBoundBox](../../../../api/library/math/cs/bounds/worldboundbox_cs.md)[]* **bounds_preload_lmaps** - [Bounding box](../../../../api/library/math/bounds/class.worldboundbox_cs.md) (world) specifying the area containing terrain tiles (all landscape layer maps) to be loaded to memory prior to making modifications.

## void AsyncTextureDraw ( UGUID file_guid , ivec2 coord , ivec2 resolution , int flags_file_data )

Commences an asynchronous GPU-based drawing operation. The drawing operation represents modification of the texture buffer of the specified size taken at specified coordinates and combining data layers defined by the specified flags. The operation itself is to be implemented in the [TextureDraw](#getEventTextureDraw_Event) event handler. This method can be used for implementing GPU-based terrain modification (e.g. brushes).
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the landscape layer map file to be modified.
- *ivec2* **coord** - Coordinates of the upper left corner of the landscape layer map data segment to be modified along the X and Y axes.
- *ivec2* **resolution** - Resolution of the landscape layer map data segment to be modified along the X and Y axes, the value within range [0, 4096] along each axis.
- *int* **flags_file_data** - Data layer mask. A combination of [FLAGS_FILE_DATA_*](#FLAGS_FILE_DATA_HEIGHT) flags indicating data layers to be affected (heights, albedo, certain masks).

## void AsyncTextureDraw ( UGUID file_guid , ivec2 coord , ivec2 resolution )

Commences an asynchronous GPU-based drawing operation. The drawing operation represents modification of the texture buffer of the specified size taken at specified coordinates and combining all data layers. The operation itself is to be implemented in the [TextureDraw](#getEventTextureDraw_Event) event handler. This method can be used for implementing GPU-based terrain modification (e.g. brushes).
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the landscape layer map file to be modified.
- *ivec2* **coord** - Coordinates of the upper left corner of the landscape layer map data segment to be modified along the X and Y axes.
- *ivec2* **resolution** - Resolution of the landscape layer map data segment to be modified along the X and Y axes, the value within range [0, 4096] along each axis.

## void AsyncTextureDraw ( int operation_id , UGUID file_guid , ivec2 coord , ivec2 resolution , int flags_file_data , WorldBoundBox [] bounds_preload_lmaps , WorldBoundBox [] bounds_preload_vtextures )

Commences an asynchronous GPU-based drawing operation with forced pre-loading of terrain data within the specified bounding boxes, including both landscape layer maps and virtual textures. The drawing operation represents a modification of the texture buffer of the specified size taken at specified coordinates and combining data layers defined by the specified flags. Preloaded [virtual texture data](../../../../objects/objects/terrain/landscape_terrain/index.md#virtual_texture) includes surface color (albedo), surface details (normal), and geometry height information (height) used for terrain tessellation. The operation is linked to the provided operation ID and is to be implemented in the [TextureDraw](#getEventTextureDraw_Event) event handler. This method can be used for implementing GPU-based terrain modifications (e.g. brushes) that require comprehensive access to both [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md) and detailed [virtual texture data](../../../../objects/objects/terrain/landscape_terrain/index.md#virtual_texture) beyond the target area.
### Arguments

- *int* **operation_id** - Draw [operation ID](#generateOperationID_int).
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the landscape layer map file to be modified.
- *ivec2* **coord** - Coordinates of the upper left corner of the landscape layer map data segment to be modified along the X and Y axes.
- *ivec2* **resolution** - Resolution of the landscape layer map data segment to be modified along the X and Y axes, the value within range [0, 4096] along each axis.
- *int* **flags_file_data** - Data layer mask. A combination of [FLAGS_FILE_DATA_*](#FLAGS_FILE_DATA_HEIGHT) flags indicating data layers to be affected (heights, albedo, certain masks).
- *[WorldBoundBox](../../../../api/library/math/cs/bounds/worldboundbox_cs.md)[]* **bounds_preload_lmaps** - [Bounding box](../../../../api/library/math/bounds/class.worldboundbox_cs.md) (world) specifying the area containing terrain tiles (all landscape layer maps) to be loaded to memory prior to making modifications.
- *[WorldBoundBox](../../../../api/library/math/cs/bounds/worldboundbox_cs.md)[]* **bounds_preload_vtextures** - [Bounding box](../../../../api/library/math/bounds/class.worldboundbox_cs.md) (world) specifying the area containing terrain tiles (virtual textures, including surface color, normals, and height data) to be loaded to memory prior to making modifications.

## void AsyncTextureDraw ( UGUID file_guid , ivec2 coord , ivec2 resolution , int flags_file_data , WorldBoundBox [] bounds_preload_lmaps , WorldBoundBox [] bounds_preload_vtextures )

Commences an asynchronous GPU-based drawing operation with forced pre-loading of terrain data within the specified bounding boxes, including both landscape layer maps and virtual textures. The drawing operation represents a modification of the texture buffer of the specified size taken at specified coordinates and combining data layers defined by the specified flags. Preloaded [virtual texture data](../../../../objects/objects/terrain/landscape_terrain/index.md#virtual_texture) includes surface color (albedo), surface details (normal), and geometry height information (height) used for terrain tessellation. The operation is to be implemented in the [TextureDraw](#getEventTextureDraw_Event) event handler. This method can be used for implementing GPU-based terrain modifications (e.g. brushes) that require comprehensive access to both [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md) and detailed [virtual texture data](../../../../objects/objects/terrain/landscape_terrain/index.md#virtual_texture) beyond the target area.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the landscape layer map file to be modified.
- *ivec2* **coord** - Coordinates of the upper left corner of the landscape layer map data segment to be modified along the X and Y axes.
- *ivec2* **resolution** - Resolution of the landscape layer map data segment to be modified along the X and Y axes, the value within range [0, 4096] along each axis.
- *int* **flags_file_data** - Data layer mask. A combination of [FLAGS_FILE_DATA_*](#FLAGS_FILE_DATA_HEIGHT) flags indicating data layers to be affected (heights, albedo, certain masks).
- *[WorldBoundBox](../../../../api/library/math/cs/bounds/worldboundbox_cs.md)[]* **bounds_preload_lmaps** - [Bounding box](../../../../api/library/math/bounds/class.worldboundbox_cs.md) (world) specifying the area containing terrain tiles (all landscape layer maps) to be loaded to memory prior to making modifications.
- *[WorldBoundBox](../../../../api/library/math/cs/bounds/worldboundbox_cs.md)[]* **bounds_preload_vtextures** - [Bounding box](../../../../api/library/math/bounds/class.worldboundbox_cs.md) (world) specifying the area containing terrain tiles (virtual textures, including surface color, normals, and height data) to be loaded to memory prior to making modifications.

## void AsyncApplyDiff ( int operation_id , UGUID file_guid , string path )

Applies the state of the landscape layer map stored in the specified file to the landscape layer map file with the specified GUID.
### Arguments

- *int* **operation_id** - [Operation ID](#generateOperationID_int).
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the landscape layer map file to which a state stored at the specified path is to be applied.
- *string* **path** - Path to a file where the current landscape map modification state is stored.

## void AsyncApplyDiff ( UGUID file_guid , string path )

Applies the state of the landscape layer map stored in the specified file to the landscape layer map file with the specified GUID.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the landscape layer map file to which a state stored at the specified path is to be applied.
- *string* **path** - Path to a file where the current landscape map modification state is stored.

## void AsyncSaveFile ( int operation_id , UGUID file_guid )

Saves the landscape layer map file with the specified GUID.
### Arguments

- *int* **operation_id** - [Operation ID](#generateOperationID_int).
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the landscape layer map file.

## void AsyncSaveFile ( UGUID file_guid )

Saves the landscape layer map file with the specified GUID.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the landscape layer map file.

## void AsyncSaveFile ( int operation_id , UGUID file_guid , string path_new_diff , string path_old_diff )

Saves the specified landscape layer map file applying all changes along with saving old and new states (diff) to temporary files. These temporary files can be used to perform undo/redo operations via the [*applyDiff()*](#asyncApplyDiff_UGUID_cstr_void) method.
### Arguments

- *int* **operation_id** - [Operation ID](#generateOperationID_int).
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the landscape layer map file.
- *string* **path_new_diff** - Path to a file to store the new landscape layer map state.
- *string* **path_old_diff** - Path to a file to store the old landscape layer map state.

## void AsyncSaveFile ( UGUID file_guid , string path_new_diff , string path_old_diff )

Saves the specified landscape layer map file applying all changes along with saving old and new states (diff) to temporary files. These temporary files can be used to perform undo/redo operations via the [*applyDiff()*](#asyncApplyDiff_UGUID_cstr_void) method.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the landscape layer map file.
- *string* **path_new_diff** - Path to a file to store the new landscape layer map state.
- *string* **path_old_diff** - Path to a file to store the old landscape layer map state.

## void FilesClose ( UGUID [] reload_files )

Closes `.lmap` files for all [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md) and reloads the ones with specified GUIDs. This method should be called before making any changes (modification, deletion, renaming) to `.lmap` files of the landscape terrain object to avoid conflicts, as these files are streamed continuosly by the Engine. Thus, by calling this method you inform the Engine that it should stop streaming terrain data. The list informs the Engine which files are no longer valid and should be reloaded or removed. As you're done with modification you should call the [*filesOpen()*](#filesOpen_void) method to resume streaming operations.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)[]* **reload_files** - List of [GUIDs](../../../../api/library/filesystem/class.uguid_cs.md) of `.lmap` files to be reloaded. This list should contain `.lmap` files, that were deleted or having their data changed (albedo, heights, masks). If there are no such files, you can simply call the [*filesClose()*](#filesClose_void) method.

## void FilesClose ( )

 Closes `.lmap` files for all [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md).This method should be called before making any changes (modification, deletion, renaming) to `.lmap` files of the landscape terrain object to avoid conflicts, as these files are streamed continuosly by the Engine. Thus, by calling this method you inform the Engine that it should stop streaming terrain data. As you're done with modification you should call the [*filesOpen()*](#filesOpen_void) method to resume streaming operations.
## void FilesOpen ( )

 Opens `.lmap` files for all [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cs.md).This method should be called after making any changes (modification, deletion, renaming) to `.lmap` files of the landscape terrain object. Prior to making such modifications the [*filesClose()*](#filesClose_void) method should be called.
## ObjectLandscapeTerrain GetActiveTerrain ( )

Returns the current active [Landscape Terrain](../../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cs.md) object.
> **Notice:** If a scene contains multiple Landscape Terrain objects, only one of them can be active (rendered).


### Return value

[Landscape Terrain](../../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cs.md) object that is currently active.
## int GenerateOperationID ( )

Generates a new ID for the operation. This ID is used to manage operations.
```cpp
int id = Landscape::generateOperationID();
// user's code (bounding to ID)
Landscape::asyncTextureDraw(id, file_guid, coord, resolution, flags_file_data);

```


### Return value

New operation ID.
## void AsyncResetModifications ( int operation_id , UGUID file_guid )

Asynchronously resets all unsaved modifications that were made to the landscape layer map identified by file GUID.
### Arguments

- *int* **operation_id** - Draw [operation ID](#generateOperationID_int).
- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the landscape layer map file to be restored.

## void AsyncResetModifications ( UGUID file_guid )

Asynchronously resets all unsaved modifications that were made to the landscape layer map identified by file GUID.
### Arguments

- *[UGUID](../../../../api/library/filesystem/class.uguid_cs.md)* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the landscape layer map file to be restored.
