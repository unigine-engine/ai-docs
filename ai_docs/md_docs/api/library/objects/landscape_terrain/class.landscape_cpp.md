# Unigine.Landscape Class (CPP)

**Header:** #include <UnigineObjects.h>

> **Notice:** This class is a singleton.


This class is used to manage landscape terrain rendering and modification.


Terrain modification is performed in asynchronous mode on GPU side by calling a corresponding method, that commences a drawing operation. When calling such a method you should specify the GUID of an `.lmap` file [landscape layer map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md) to be modified, the coordinates of the upper-left corner and the resolution of the segment of data to be modified, you should also define which data layers are to be affected (heights, albedo, masks) via a set of [flags](#FLAGS_FILE_DATA_HEIGHT). The operation itself is to be implemented inside a callback handler.


### GPU-Based Terrain Modification


The workflow is as follows:


1. Implement your GPU-based terrain modification logic in a function.
2. Set this handler function when subscribing for the *Texture Draw* event (when GPU-based terrain modification operation is performed) via *[getEventTextureDraw()](#getEventTextureDraw_Event)*.
3. Commence a GPU drawing operation by calling the [*asyncTextureDraw()*](#asyncTextureDraw_UGUID_ivec2_ivec2_int_void) method. Here you should specify the GUID of an `.lmap` file [landscape layer map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md) to be modified, the coordinates of the upper-left corner and the resolution of the segment of data to be modified, you should also define which data layers are to be affected (heights, albedo, masks) via a set of [flags](#FLAGS_FILE_DATA_HEIGHT). > **Notice:** In case your modification requires additional data beyond the specified area as well as the data of other landscape layer maps (e.g. a copy brush) you can enable force loading of required data, in this case you should use [this overload of the *asyncTextureDraw()* method](#asyncTextureDraw_UGUID_ivec2_ivec2_int_VECWorldBoundBox_void).


```cpp
// GPU-based modification
void my_texture_draw(const UGUID &guid, int id, const LandscapeTexturesPtr &buffer, const Math::ivec2 &coord, int data_mask)
{
	// getting the desired brush material (built - in "cirle_soft" Editor's brush)
	// and inheriting a child material from it
	auto file_guid = FileSystem::getGUID(FileSystem::resolvePartialVirtualPath("circle_soft.brush"));
	if (!file_guid.isValid())
	{
		Log::warning("LandscapePainter::init(): can not find \"circle_soft.brush\" material\n");
		return;
	}

	MaterialPtr brush_material = Materials::findMaterialByFileGUID(file_guid)->inherit();

	// setting necessary textures (e.g., albedo and heights)
	brush_material->setTexture("terrain_albedo", buffer->getAlbedo());
	brush_material->setTexture("terrain_height", buffer->getHeight());

	// setting up brush material parameters (size, color, etc. and specifying masks to be affected by the brush)
	brush_material->setParameterFloat("size", 100.0f);
	brush_material->setParameterFloat("height", 10.0f);
	brush_material->setParameterFloat4("color", vec4_green);
	brush_material->setParameterInt("data_mask", data_mask);

	// running material's "brush" expression
	brush_material->runExpression("brush", buffer->getResolution().x, buffer->getResolution().y);

	// resetting material textures
	brush_material->setTexture("terrain_albedo", nullptr);
	brush_material->setTexture("terrain_height", nullptr);

}

// ...

int AppWorldLogic::init()
{
	// getting an existing landscape terrain object
	ObjectLandscapeTerrainPtr terrain = Landscape::getActiveTerrain();

	// getting the first layermap that we're going to modify
	LandscapeLayerMapPtr lmap = checked_ptr_cast<LandscapeLayerMap> (terrain->getChild(0));

	// subscribing for a Texture Draw operation
	Landscape::getEventTextureDraw().connect(connections, my_texture_draw);

	// generating a new ID for the draw operation
	int id = Landscape::generateOperationID();

	// user's code (bounding to ID)

	// commencing a Texture Draw operation for the selected landscape map at (1, 1) with the size of [32 x 32]
	Landscape::asyncTextureDraw(id, lmap->getGUID(), ivec2(1, 1), ivec2(32, 32), Landscape::FLAGS_DATA_HEIGHT | Landscape::FLAGS_DATA_ALBEDO);

	return 1;
}

// ...

 int AppWorldLogic::shutdown()
{
	// removing all subscriptions
	connections.disconnectAll();

	return 1;
}


```


And the process:


1. After commencing of a terrain modification operation with all necessary parameters specified, the Engine copies a fragment of terrain data from the specified [landscape layer map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md) file at the specified coordinates to a buffer ([*LandscapeTextures*](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cpp.md)) of the specified resolution.
2. Upon completion of the copying process a handler function which you used to subscribe for the *[TextureDraw](#getEventTextureDraw_Event)* event is executed. This function modifies the buffer.
3. After this selected data layers of the modified buffer are pasted back to the [landscape layer map](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md) file.


##### Usage Example: Brush Editor


Below is a C++ component implementing brush-based *Landscape Terrain* modification.


<details>
<summary>LandscapeBrush.h | Close</summary>

```cpp
#pragma once

#include <UnigineComponentSystem.h>
#include <UniginePlayers.h>
class LandscapeBrush :
	public Unigine::ComponentBase
{
public:
	COMPONENT_DEFINE(LandscapeBrush, Unigine::ComponentBase);
	COMPONENT_INIT(init);
	COMPONENT_UPDATE(update);
	COMPONENT_SHUTDOWN(shutdown);

	PROP_PARAM(Float, brush_size, 10.0f, "Brush Size");
	PROP_PARAM(Float, brush_height, 1.0f, "Brush Height");

private:
	void init();
	void update();
	void shutdown();
	void my_texture_draw(const Unigine::UGUID &guid, int id, const Unigine::LandscapeTexturesPtr &buffer, const Unigine::Math::ivec2 &coord, int data_mask);
	Unigine::LandscapeLayerMapPtr lmap;
	Unigine::PlayerPtr player;
	Unigine::LandscapeFetchPtr landscape_fetch;
	Unigine::MaterialPtr brush_material;
	Unigine::EventConnections connections;

```

</details>


<details>
<summary>LandscapeBrush.cpp | Close</summary>

```cpp
#include "LandscapeBrush.h"
#include <UnigineGame.h>
REGISTER_COMPONENT(LandscapeBrush);

using namespace Unigine;
using namespace Math;

// GPU-based modification
void LandscapeBrush::my_texture_draw(const UGUID &guid, int id, const LandscapeTexturesPtr &buffer, const Math::ivec2 &coord, int data_mask)
{
	// setting necessary textures (e.g., albedo and heights)
	brush_material->setTexture("terrain_albedo", buffer->getAlbedo());
	brush_material->setTexture("terrain_height", buffer->getHeight());

	// setting up brush material parameters (size, color, etc. and specifying masks to be affected by the brush)
	brush_material->setParameterFloat("size", brush_size);
	brush_material->setParameterFloat("height", brush_height);
	brush_material->setParameterFloat4("color", Math::vec4_green);
	brush_material->setParameterInt("data_mask", data_mask);

	// running material's "brush" expression
	brush_material->runExpression("brush", buffer->getResolution().x, buffer->getResolution().y);

	// resetting material textures
	brush_material->setTexture("terrain_albedo", nullptr);
	brush_material->setTexture("terrain_height", nullptr);
}

void LandscapeBrush::init()
{
	// getting the desired brush material (built - in "cirle_soft" Editor's brush) and inheriting a child material from it
	auto guid = FileSystem::getGUID(FileSystem::resolvePartialVirtualPath("circle_soft.brush"));
	if (!guid.isValid())
	{
		Log::warning("LandscapePainter::init(): can not find \"circle_soft.brush\" material\n");
		return;
	}

	brush_material = Materials::findMaterialByFileGUID(guid)->inherit();

	// getting an existing landscape terrain object
	ObjectLandscapeTerrainPtr terrain = Landscape::getActiveTerrain();

	// getting the first layermap that we're going to modify
	lmap = checked_ptr_cast<LandscapeLayerMap>(terrain->getChild(0));

	// subscribing for the Texture Draw operation
	Landscape::getEventTextureDraw().connect(connections, this, &LandscapeBrush::my_texture_draw);

	// setting the mouse handling mode to USER to display the cursor on the screen
	ControlsApp::setMouseHandle(Input::MOUSE_HANDLE_USER);

	// Getting the current player
	player = Game::getPlayer();

	return;
}

void LandscapeBrush::update()
{
	// Write here code to be called before updating each render frame: specify all graphics-related functions you want to be called every frame while your application executes.
	// if right mouse button is clicked
	if (Input::isMouseButtonDown(Input::MOUSE_BUTTON_RIGHT))
	{
		landscape_fetch = LandscapeFetch::create();

		// getting direction from the current mouse position
		Math::ivec2 mouse = Input::getMousePosition();
		Math::Vec3 dir = Math::Vec3(player->getDirectionFromMainWindow(mouse.x, mouse.y));
		// fetching the coordinates of the point of intersection
		bool fetched = landscape_fetch->intersectionForce(player->getPosition(),
			player->getPosition() + Vec3(dir) * 10000.0);

		if (fetched)
		{
			// getting the local position of the brush relative to the layer map
			Vec3 brush_local_position = lmap->getIWorldTransform() * landscape_fetch->getPosition();

			// calculating the bound of the layer map area to be affected by the brush
			float half_size = brush_size / 2.0f;
			Vec3 brush_local_corners[4] = {
				brush_local_position + Vec3(-half_size, -half_size, 0.0),
				brush_local_position + Vec3(half_size, -half_size, 0.0),
				brush_local_position + Vec3(-half_size,  half_size, 0.0),
				brush_local_position + Vec3(half_size,  half_size, 0.0)
			};
			auto brush_local_bbox_min = Vec2{
				min(min(brush_local_corners[0].x, brush_local_corners[1].x), min(brush_local_corners[2].x, brush_local_corners[3].x)),
				min(min(brush_local_corners[0].y, brush_local_corners[1].y), min(brush_local_corners[2].y, brush_local_corners[3].y))
			};
			auto brush_local_bbox_max = Vec2{
				max(max(brush_local_corners[0].x, brush_local_corners[1].x), max(brush_local_corners[2].x, brush_local_corners[3].x)),
				max(max(brush_local_corners[0].y, brush_local_corners[1].y), max(brush_local_corners[2].y, brush_local_corners[3].y))
			};

			// calculating the number of pixels per unit length
			auto pixels_per_unit = Vec2{ lmap->getResolution() } / Vec2{ lmap->getSize() };

			// calculating the coordinates and the size of the region or the landscape layer texture to be modified
			auto drawing_region_coord = ivec2{ pixels_per_unit * brush_local_bbox_min };
			auto drawing_region_size = ivec2{ pixels_per_unit * (brush_local_bbox_max - brush_local_bbox_min) };

			// user's code (bounding to ID)
			auto id = Landscape::generateOperationID();

			// commencing a Texture Draw operation for the selected landscape map for the region with the specified coords and size
			// affecting Height and Albedo data
			Landscape::asyncTextureDraw(id, lmap->getGUID(), drawing_region_coord,
				drawing_region_size, Landscape::FLAGS_DATA_HEIGHT | Landscape::FLAGS_DATA_ALBEDO);
		}

	}
	return;
}

void LandscapeBrush::shutdown()
{
	// removing all subscriptions
	connections.disconnectAll();

	return;
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
| **TYPE_DATA_HEIGHT** = 0 | Heights data type. |
| **TYPE_DATA_ALBEDO** = 1 | Albedo data type. |
| **TYPE_DATA_MASK_0** = 2 | Mask0 data type. |
| **TYPE_DATA_MASK_1** = 3 | Mask1 data type. |
| **TYPE_DATA_MASK_2** = 4 | Mask2 data type. |
| **TYPE_DATA_MASK_3** = 5 | Mask3 data type. |
| **TYPE_DATA_MASK_4** = 6 | Mask4 data type. |
| **TYPE_DATA_MASK_5** = 7 | Mask5 data type. |
| **TYPE_DATA_MASK_6** = 8 | Mask6 data type. |
| **TYPE_DATA_MASK_7** = 9 | Mask7 data type. |
| **TYPE_DATA_MASK_8** = 10 | Mask8 data type. |
| **TYPE_DATA_MASK_9** = 11 | Mask9 data type. |
| **TYPE_DATA_MASK_10** = 12 | Mask10 data type. |
| **TYPE_DATA_MASK_11** = 13 | Mask11 data type. |
| **TYPE_DATA_MASK_12** = 14 | Mask12 data type. |
| **TYPE_DATA_MASK_13** = 15 | Mask13 data type. |
| **TYPE_DATA_MASK_14** = 16 | Mask14 data type. |
| **TYPE_DATA_MASK_15** = 17 | Mask15 data type. |
| **TYPE_DATA_MASK_16** = 18 | Mask16 data type. |
| **TYPE_DATA_MASK_17** = 19 | Mask17 data type. |
| **TYPE_DATA_MASK_18** = 20 | Mask18 data type. |
| **TYPE_DATA_MASK_19** = 21 | Mask19 data type. |

## FLAGS_DATA

| Name | Description |
|---|---|
| **FLAGS_DATA_HEIGHT** = 1 << 0 | Heights data flag. |
| **FLAGS_DATA_ALBEDO** = 1 << 1 | Albedo data flag. |
| **FLAGS_DATA_MASK_0** = 1 << 2 | Mask0 data flag. |
| **FLAGS_DATA_MASK_1** = 1 << 3 | Mask1 data flag. |
| **FLAGS_DATA_MASK_2** = 1 << 4 | Mask2 data flag. |
| **FLAGS_DATA_MASK_3** = 1 << 5 | Mask3 data flag. |
| **FLAGS_DATA_MASK_4** = 1 << 6 | Mask4 data flag. |
| **FLAGS_DATA_MASK_5** = 1 << 7 | Mask5 data flag. |
| **FLAGS_DATA_MASK_6** = 1 << 8 | Mask6 data flag. |
| **FLAGS_DATA_MASK_7** = 1 << 9 | Mask7 data flag. |
| **FLAGS_DATA_MASK_8** = 1 << 10 | Mask8 data flag. |
| **FLAGS_DATA_MASK_9** = 1 << 11 | Mask9 data flag. |
| **FLAGS_DATA_MASK_10** = 1 << 12 | Mask10 data flag. |
| **FLAGS_DATA_MASK_11** = 1 << 13 | Mask11 data flag. |
| **FLAGS_DATA_MASK_12** = 1 << 14 | Mask12 data flag. |
| **FLAGS_DATA_MASK_13** = 1 << 15 | Mask13 data flag. |
| **FLAGS_DATA_MASK_14** = 1 << 16 | Mask14 data flag. |
| **FLAGS_DATA_MASK_15** = 1 << 17 | Mask15 data flag. |
| **FLAGS_DATA_MASK_16** = 1 << 18 | Mask16 data flag. |
| **FLAGS_DATA_MASK_17** = 1 << 19 | Mask17 data flag. |
| **FLAGS_DATA_MASK_18** = 1 << 20 | Mask18 data flag. |
| **FLAGS_DATA_MASK_19** = 1 << 21 | Mask19 data flag. |

## TYPE_FILE_DATA

File data types.
| Name | Description |
|---|---|
| **TYPE_FILE_DATA_HEIGHT** = 0 | Landscape map file heights data. |
| **TYPE_FILE_DATA_ALBEDO** = 1 | Landscape map file albedo data. |
| **TYPE_FILE_DATA_MASK_0** = 2 | Landscape map file detail mask data (masks with indices 0, 1, 2, 3). |
| **TYPE_FILE_DATA_MASK_1** = 3 | Landscape map file detail mask data (masks with indices 4, 5, 6, 7). |
| **TYPE_FILE_DATA_MASK_2** = 4 | Landscape map file detail mask data (masks 8, 9, 10, 11). |
| **TYPE_FILE_DATA_MASK_3** = 5 | Landscape map file detail mask data (masks with indices 12, 13, 14, 15). |
| **TYPE_FILE_DATA_MASK_4** = 6 | Landscape map file detail mask data (masks with indices 16, 17, 18, 19). |
| **TYPE_FILE_DATA_OPACITY_HEIGHT** = 7 | Landscape map file height opacity data. |
| **TYPE_FILE_DATA_OPACITY_MASK_0** = 8 | Landscape map file detail mask opacity data (masks with indices 0, 1, 2, 3). |
| **TYPE_FILE_DATA_OPACITY_MASK_1** = 9 | Landscape map file detail mask opacity data (masks with indices 4, 5, 6, 7). |
| **TYPE_FILE_DATA_OPACITY_MASK_2** = 10 | Landscape map file detail mask opacity data (masks with indices 8, 9, 10, 11). |
| **TYPE_FILE_DATA_OPACITY_MASK_3** = 11 | Landscape map file detail mask opacity data (masks with indices 12, 13, 14, 15). |
| **TYPE_FILE_DATA_OPACITY_MASK_4** = 12 | Landscape map file detail mask opacity data (masks with indices 16, 17, 18, 19). |

## FLAGS_FILE_DATA

File data layer flags.
| Name | Description |
|---|---|
| **FLAGS_FILE_DATA_HEIGHT** = 1 << 0 | Landscape map file height data. |
| **FLAGS_FILE_DATA_ALBEDO** = 1 << 1 | Landscape map file albedo data. |
| **FLAGS_FILE_DATA_MASK_0** = 1 << 2 | Landscape map file first masks data block (masks with indices 0,1,2,3). |
| **FLAGS_FILE_DATA_MASK_1** = 1 << 3 | Landscape map file second masks data block (masks with indices 4,5,6,7). |
| **FLAGS_FILE_DATA_MASK_2** = 1 << 4 | Landscape map file third masks data block (masks with indices 8,9,10,11). |
| **FLAGS_FILE_DATA_MASK_3** = 1 << 5 | Landscape map file fourth masks data block (masks with indices 12,13,14,15). |
| **FLAGS_FILE_DATA_MASK_4** = 1 << 6 | Landscape map file fifth masks data block (masks with indices 16,17,18,19). |
| **FLAGS_FILE_DATA_OPACITY_HEIGHT** = 1 << 7 | Landscape map file height opacity data. |
| **FLAGS_FILE_DATA_OPACITY_MASK_0** = 1 << 8 | Landscape map file first masks opacity data block (for masks with indices 0,1,2,3). |
| **FLAGS_FILE_DATA_OPACITY_MASK_1** = 1 << 9 | Landscape map file second masks opacity data block (for masks with indices 4,5,6,7). |
| **FLAGS_FILE_DATA_OPACITY_MASK_2** = 1 << 10 | Landscape map file third masks opacity data block (for masks with indices 8,9,10,11). |
| **FLAGS_FILE_DATA_OPACITY_MASK_3** = 1 << 11 | Landscape map file fourth masks opacity data block (for masks with indices 12,13,14,15). |
| **FLAGS_FILE_DATA_OPACITY_MASK_4** = 1 << 12 | Landscape map file fifth masks opacity data block (for masks with indices 16,17,18,19). |

## COMPRESSOR_TYPE

Compression method used for the layer map.
| Name | Description |
|---|---|
| **COMPRESSOR_TYPE_NONE** = 0 | No compression is used. |
| **COMPRESSOR_TYPE_JACKALLESS** = 1 | **Our Method** compression is used. It is optimized for compressing 2D and 3D textures and provides better results than **LZ4** and **Zlib** without deteriorating the quality. |
| **COMPRESSOR_TYPE_LZ4** = 2 | **LZ4** compression is used (temporary option, planned to be removed in the upcoming releases). |
| **COMPRESSOR_TYPE_ZLIB** = 3 | **Zlib** compression (can provide up to 2 times higher compression ratio, but takes up to 20 times longer). |

## BLENDING_MODE

Blending mode used for the layer map.
| Name | Description |
|---|---|
| **ALPHA_BLEND** = 0 | Alpha blending mode - the colors of the layer map and the underlying one are blended. |
| **ADDITIVE** = 1 | Additive blending mode - data of the layer map is added atop of the data of underlying maps. |
| **OVERLAY** = 2 | Overlay blending mode - data of the layer map replaces the data of underlying maps. |
| **MULTIPLICATIVE** = 3 | Multiplicative blending mode - albedo colors of the underlying map are multiplied by the colors of the layer map. |

### Members

## bool isFilesClosed () const

Returns the current value indicating if `.lmap` files for all [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md) are closed. Call this method before making any changes (modification, deletion, renaming) to `.lmap` files of the landscape terrain object to ensure that these files are not currently used by the Engine to avoid conflicts. If not, you can use the [*filesClose()*](#filesClose_void) method co close them.
### Return value

**true** if `.lmap` files for all landscape layer maps are closed is enabled ; otherwise **false**.
## static Event<const UGUID &, int, const char *, const char *> getEventSaveFile () const

Event triggered when applying changes made to a landscape layer map file and saving old and new states to temporary files. The signature of the event handler must be as follows:
```cpp
void savefile_event_handler(const UGUID & guid,  int operation_id,  const char * path_new_state,  const char * path_old_state)

```

 You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const UGUID & **guid**, int **operation_id**, const char * **path_new_state**, const char * **path_old_state**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the SaveFile event handler
void savefile_event_handler(const UGUID & guid,  int operation_id,  const char * path_new_state,  const char * path_old_state)
{
	Log::message("\Handling SaveFile event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections savefile_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Landscape::getEventSaveFile().connect(savefile_event_connections, savefile_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Landscape::getEventSaveFile().connect(savefile_event_connections, [](const UGUID & guid,  int operation_id,  const char * path_new_state,  const char * path_old_state) {
		Log::message("\Handling SaveFile event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
savefile_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection savefile_event_connection;

// subscribe to the SaveFile event with a handler function keeping the connection
Landscape::getEventSaveFile().connect(savefile_event_connection, savefile_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
savefile_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
savefile_event_connection.setEnabled(true);

// ...

// remove subscription to the SaveFile event via the connection
savefile_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A SaveFile event handler implemented as a class member
	void event_handler(const UGUID & guid,  int operation_id,  const char * path_new_state,  const char * path_old_state)
	{
		Log::message("\Handling SaveFile event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Landscape::getEventSaveFile().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId savefile_handler_id;

// subscribe to the SaveFile event with a lambda handler function and keeping connection ID
savefile_handler_id = Landscape::getEventSaveFile().connect(e_connections, [](const UGUID & guid,  int operation_id,  const char * path_new_state,  const char * path_old_state) {
		Log::message("\Handling SaveFile event (lambda).\n");
	}
);

// remove the subscription later using the ID
Landscape::getEventSaveFile().disconnect(savefile_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all SaveFile events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Landscape::getEventSaveFile().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Landscape::getEventSaveFile().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const UGUID &, int, const char *> getEventApplyDiff () const

Event triggered when applying a diff to the landscape layer map file. The signature of the event handler must be as follows:
```cpp
void applydiff_event_handler(const UGUID & guid,  int operation_id,  const char * lmap_file_path)

```

 You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const UGUID & **guid**, int **operation_id**, const char * **lmap_file_path**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the ApplyDiff event handler
void applydiff_event_handler(const UGUID & guid,  int operation_id,  const char * lmap_file_path)
{
	Log::message("\Handling ApplyDiff event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections applydiff_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Landscape::getEventApplyDiff().connect(applydiff_event_connections, applydiff_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Landscape::getEventApplyDiff().connect(applydiff_event_connections, [](const UGUID & guid,  int operation_id,  const char * lmap_file_path) {
		Log::message("\Handling ApplyDiff event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
applydiff_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection applydiff_event_connection;

// subscribe to the ApplyDiff event with a handler function keeping the connection
Landscape::getEventApplyDiff().connect(applydiff_event_connection, applydiff_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
applydiff_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
applydiff_event_connection.setEnabled(true);

// ...

// remove subscription to the ApplyDiff event via the connection
applydiff_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A ApplyDiff event handler implemented as a class member
	void event_handler(const UGUID & guid,  int operation_id,  const char * lmap_file_path)
	{
		Log::message("\Handling ApplyDiff event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Landscape::getEventApplyDiff().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId applydiff_handler_id;

// subscribe to the ApplyDiff event with a lambda handler function and keeping connection ID
applydiff_handler_id = Landscape::getEventApplyDiff().connect(e_connections, [](const UGUID & guid,  int operation_id,  const char * lmap_file_path) {
		Log::message("\Handling ApplyDiff event (lambda).\n");
	}
);

// remove the subscription later using the ID
Landscape::getEventApplyDiff().disconnect(applydiff_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all ApplyDiff events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Landscape::getEventApplyDiff().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Landscape::getEventApplyDiff().setEnabled(true);

```

</details>

### Return value

Event instance.
## static Event<const UGUID &, int, const Ptr < LandscapeTextures > &, const Math:: ivec2 &, int> getEventTextureDraw () const

Event triggered when a Texture Draw (GPU-based terrain modification) operation is performed. The signature of the event handler must be as follows:
```cpp
void texturedraw_event_handler(const UGUID & guid,  int operation_id,  const Ptr<LandscapeTextures> & buffer,  const Math::ivec2 & coords,  int data_mask)

```

 You can subscribe to events via *connect()* �and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../../api/library/common/events/class.eventconnection_cpp.md)* �and *[EventConnections](../../../../api/library/common/events/class.eventconnections_cpp.md)* �classes for convenience (see examples below).

> **Notice:** For more details see the [Event Handling](../../../../code/fundamentals/events/index_cpp.md) article.

 The event handler signature is as follows: *myhandler(const UGUID & **guid**, int **operation_id**, const Ptr<LandscapeTextures> & **buffer**, const Math::ivec2 & **coords**, int **data_mask**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the TextureDraw event handler
void texturedraw_event_handler(const UGUID & guid,  int operation_id,  const Ptr<LandscapeTextures> & buffer,  const Math::ivec2 & coords,  int data_mask)
{
	Log::message("\Handling TextureDraw event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections texturedraw_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
Landscape::getEventTextureDraw().connect(texturedraw_event_connections, texturedraw_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
Landscape::getEventTextureDraw().connect(texturedraw_event_connections, [](const UGUID & guid,  int operation_id,  const Ptr<LandscapeTextures> & buffer,  const Math::ivec2 & coords,  int data_mask) {
		Log::message("\Handling TextureDraw event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
texturedraw_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection texturedraw_event_connection;

// subscribe to the TextureDraw event with a handler function keeping the connection
Landscape::getEventTextureDraw().connect(texturedraw_event_connection, texturedraw_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
texturedraw_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
texturedraw_event_connection.setEnabled(true);

// ...

// remove subscription to the TextureDraw event via the connection
texturedraw_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A TextureDraw event handler implemented as a class member
	void event_handler(const UGUID & guid,  int operation_id,  const Ptr<LandscapeTextures> & buffer,  const Math::ivec2 & coords,  int data_mask)
	{
		Log::message("\Handling TextureDraw event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
Landscape::getEventTextureDraw().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId texturedraw_handler_id;

// subscribe to the TextureDraw event with a lambda handler function and keeping connection ID
texturedraw_handler_id = Landscape::getEventTextureDraw().connect(e_connections, [](const UGUID & guid,  int operation_id,  const Ptr<LandscapeTextures> & buffer,  const Math::ivec2 & coords,  int data_mask) {
		Log::message("\Handling TextureDraw event (lambda).\n");
	}
);

// remove the subscription later using the ID
Landscape::getEventTextureDraw().disconnect(texturedraw_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all TextureDraw events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
Landscape::getEventTextureDraw().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
Landscape::getEventTextureDraw().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## bool terrainLoad ( const Math:: WorldBoundBox & bb )

Loads terrain data (tiles) for all landscape layer maps within the specified bounding box to cache.
### Arguments

- *const  Math::[WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) &* **bb** - Bounding box, defining landscape layer maps for which the data is to be loaded.

### Return value

true if terrain data was successfully loaded for all landscape layer maps within the specified bounding box; otherwise, false.
## bool render ( const Ptr < LandscapeTextures > & buffers , const Math:: Mat4 & transform , Math::Scalar texel_size )

Renders the area of the specified landscape layer maps defined by the specified transform and texel size, to the specified [buffers](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cpp.md).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[LandscapeTextures](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cpp.md)> &* **buffers** - Target [texture buffers](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cpp.md) to which the specified landscape layer maps are to be rendered.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation of the landscape terrain area to be rendered (Z-coordinate is ignored).
- *Math::Scalar* **texel_size** - Texel size to be used. Defines the size of the area depending on the *buffers* resolution.

### Return value

true if the data of the landscape terrain area (all landscape layer maps) defined by the specified transformation and texel size, was successfully rendered to the specified buffers; otherwise, false.
## bool render ( const Ptr < LandscapeTextures > & buffers , const Math:: Mat4 & transform , Math::Scalar texel_size , int padding )

Renders the area of the specified landscape layer maps defined by the specified transform and texel size, to the specified [buffers](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cpp.md). Use the *padding* parameter to set inner padding size for the area (when necessary).
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[LandscapeTextures](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cpp.md)> &* **buffers** - Target [texture buffers](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cpp.md) to which the specified landscape layer maps are to be rendered.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation of the landscape terrain area to be rendered (Z-coordinate is ignored).
- *Math::Scalar* **texel_size** - Texel size to be used. Defines the size of the area depending on the *buffers* resolution.
- *int* **padding** - Inner padding size for the area to be rendered (if necessary).

### Return value

true if the data of the landscape terrain area (all landscape layer maps) defined by the specified transformation and texel size, was successfully rendered to the specified buffers; otherwise, false.
## bool render ( const Vector < Ptr < LandscapeLayerMap >> & maps , const Ptr < LandscapeTextures > & buffers , const Math:: Mat4 & transform , Math::Scalar texel_size )

Renders the area of the specified landscape layer maps defined by the specified transform and texel size, to the specified [buffers](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cpp.md).
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[LandscapeLayerMap](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md)>> &* **maps** - List of the landscape layer maps to be rendered.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[LandscapeTextures](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cpp.md)> &* **buffers** - Target [texture buffers](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cpp.md) to which the specified landscape layer maps are to be rendered.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation of the landscape terrain area to be rendered (Z-coordinate is ignored).
- *Math::Scalar* **texel_size** - Texel size to be used. Defines the size of the area depending on the *buffers* resolution.

### Return value

true if the data of the landscape terrain area (specified landscape layer maps) defined by the specified transformation and texel size, was successfully rendered to the specified buffers; otherwise, false.
## bool render ( const Vector < Ptr < LandscapeLayerMap >> & maps , const Ptr < LandscapeTextures > & buffers , const Math:: Mat4 & transform , Math::Scalar texel_size , int padding )

Renders the area of the specified landscape layer maps defined by the specified transform and texel size, to the specified [buffers](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cpp.md). Use the *padding* parameter to set inner padding size for the area (when necessary).
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[LandscapeLayerMap](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md)>> &* **maps** - List of the landscape layer maps to be rendered.
- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[LandscapeTextures](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cpp.md)> &* **buffers** - Target [texture buffers](../../../../api/library/objects/landscape_terrain/class.landscapetextures_cpp.md) to which the specified landscape layer maps are to be rendered.
- *const  Math::[Mat4](../../../../api/library/math/class.mat4_cpp.md) &* **transform** - Transformation of the landscape terrain area to be rendered (Z-coordinate is ignored).
- *Math::Scalar* **texel_size** - Texel size to be used. Defines the size of the area depending on the *buffers* resolution.
- *int* **padding** - Inner padding size for the area to be rendered.

### Return value

true if the data of the landscape terrain area (specified landscape layer maps) defined by the specified transformation and texel size, was successfully rendered to the specified buffers; otherwise, false.
## void asyncTextureDraw ( int operation_id , const UGUID & file_guid , const Math:: ivec2 & coord , const Math:: ivec2 & resolution , int flags_file_data , const Vector < Math:: WorldBoundBox > & bounds_preload_lmaps )

Commences an asynchronous GPU-based drawing operation with forced pre-loading of terrain data within the specified bounding box (all landscape layer maps). The drawing operation represents modification of the texture buffer of the specified size taken at specified coordinates and combining data layers defined by the specified flags. The operation itself is to be implemented in the [TextureDraw](#getEventTextureDraw_Event) event handler. This method can be used for implementing GPU-based terrain modification (e.g. brushes) that requires additional data beyond the area specified by *coords* and *resolution* parameters as well as the data of other [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md) (e.g. a copy brush).
### Arguments

- *int* **operation_id** - Draw [operation ID](#generateOperationID_int).
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the landscape layer map file to be modified.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **coord** - Coordinates of the upper left corner of the landscape layer map data segment to be modified along the X and Y axes.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **resolution** - Resolution of the landscape layer map data segment to be modified along the X and Y axes, the value within range [0, 4096] along each axis.
- *int* **flags_file_data** - Data layer mask. A combination of [FLAGS_FILE_DATA_*](#FLAGS_FILE_DATA_HEIGHT) flags indicating data layers to be affected (heights, albedo, certain masks).
- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Math::[WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md)> &* **bounds_preload_lmaps** - [Bounding box](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) (world) specifying the area containing terrain tiles (all landscape layer maps) to be loaded to memory prior to making modifications.

## void asyncTextureDraw ( int operation_id , const UGUID & file_guid , const Math:: ivec2 & coord , const Math:: ivec2 & resolution , int flags_file_data )

Commences an asynchronous GPU-based drawing operation. The drawing operation represents modification of the texture buffer of the specified size taken at specified coordinates and combining data layers defined by the specified flags. The operation itself is to be implemented in the [TextureDraw](#getEventTextureDraw_Event) event handler. This method can be used for implementing GPU-based terrain modification (e.g. brushes).
### Arguments

- *int* **operation_id** - Draw [operation ID](#generateOperationID_int).
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the landscape layer map file to be modified.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **coord** - Coordinates of the upper left corner of the landscape layer map data segment to be modified along the X and Y axes.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **resolution** - Resolution of the landscape layer map data segment to be modified along the X and Y axes, the value within range [0, 4096] along each axis.
- *int* **flags_file_data** - Data layer mask. A combination of [FLAGS_FILE_DATA_*](#FLAGS_FILE_DATA_HEIGHT) flags indicating data layers to be affected (heights, albedo, certain masks).

## void asyncTextureDraw ( int operation_id , const UGUID & file_guid , const Math:: ivec2 & coord , const Math:: ivec2 & resolution )

Commences an asynchronous GPU-based drawing operation. The drawing operation represents modification of the texture buffer of the specified size taken at specified coordinates and combining all data layers. The operation itself is to be implemented in the [TextureDraw](#getEventTextureDraw_Event) event handler. This method can be used for implementing GPU-based terrain modification (e.g. brushes).
### Arguments

- *int* **operation_id** - Draw [operation ID](#generateOperationID_int).
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the landscape layer map file to be modified.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **coord** - Coordinates of the upper left corner of the landscape layer map data segment to be modified along the X and Y axes.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **resolution** - Resolution of the landscape layer map data segment to be modified along the X and Y axes, the value within range [0, 4096] along each axis.

## void asyncTextureDraw ( const UGUID & file_guid , const Math:: ivec2 & coord , const Math:: ivec2 & resolution , int flags_file_data , const Vector < Math:: WorldBoundBox > & bounds_preload_lmaps )

Commences an asynchronous GPU-based drawing operation with forced pre-loading of terrain data within the specified bounding box (all landscape layer maps). The drawing operation represents modification of the texture buffer of the specified size taken at specified coordinates and combining data layers defined by the specified flags. The operation itself is to be implemented in the [TextureDraw](#getEventTextureDraw_Event) event handler. This method can be used for implementing GPU-based terrain modification (e.g. brushes) that requires additional data beyond the area specified by *coords* and *resolution* parameters as well as the data of other [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md) (e.g. a copy brush).
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the landscape layer map file to be modified.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **coord** - Coordinates of the upper left corner of the landscape layer map data segment to be modified along the X and Y axes.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **resolution** - Resolution of the landscape layer map data segment to be modified along the X and Y axes, the value within range [0, 4096] along each axis.
- *int* **flags_file_data** - Data layer mask. A combination of [FLAGS_FILE_DATA_*](#FLAGS_FILE_DATA_HEIGHT) flags indicating data layers to be affected (heights, albedo, certain masks).
- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Math::[WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md)> &* **bounds_preload_lmaps** - [Bounding box](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) (world) specifying the area containing terrain tiles (all landscape layer maps) to be loaded to memory prior to making modifications.

## void asyncTextureDraw ( const UGUID & file_guid , const Math:: ivec2 & coord , const Math:: ivec2 & resolution , int flags_file_data )

Commences an asynchronous GPU-based drawing operation. The drawing operation represents modification of the texture buffer of the specified size taken at specified coordinates and combining data layers defined by the specified flags. The operation itself is to be implemented in the [TextureDraw](#getEventTextureDraw_Event) event handler. This method can be used for implementing GPU-based terrain modification (e.g. brushes).
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the landscape layer map file to be modified.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **coord** - Coordinates of the upper left corner of the landscape layer map data segment to be modified along the X and Y axes.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **resolution** - Resolution of the landscape layer map data segment to be modified along the X and Y axes, the value within range [0, 4096] along each axis.
- *int* **flags_file_data** - Data layer mask. A combination of [FLAGS_FILE_DATA_*](#FLAGS_FILE_DATA_HEIGHT) flags indicating data layers to be affected (heights, albedo, certain masks).

## void asyncTextureDraw ( const UGUID & file_guid , const Math:: ivec2 & coord , const Math:: ivec2 & resolution )

Commences an asynchronous GPU-based drawing operation. The drawing operation represents modification of the texture buffer of the specified size taken at specified coordinates and combining all data layers. The operation itself is to be implemented in the [TextureDraw](#getEventTextureDraw_Event) event handler. This method can be used for implementing GPU-based terrain modification (e.g. brushes).
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the landscape layer map file to be modified.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **coord** - Coordinates of the upper left corner of the landscape layer map data segment to be modified along the X and Y axes.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **resolution** - Resolution of the landscape layer map data segment to be modified along the X and Y axes, the value within range [0, 4096] along each axis.

## void asyncTextureDraw ( int operation_id , const UGUID & file_guid , const Math:: ivec2 & coord , const Math:: ivec2 & resolution , int flags_file_data , const Vector < Math:: WorldBoundBox > & bounds_preload_lmaps , const Vector < Math:: WorldBoundBox > & bounds_preload_vtextures )

Commences an asynchronous GPU-based drawing operation with forced pre-loading of terrain data within the specified bounding boxes, including both landscape layer maps and virtual textures. The drawing operation represents a modification of the texture buffer of the specified size taken at specified coordinates and combining data layers defined by the specified flags. Preloaded [virtual texture data](../../../../objects/objects/terrain/landscape_terrain/index.md#virtual_texture) includes surface color (albedo), surface details (normal), and geometry height information (height) used for terrain tessellation. The operation is linked to the provided operation ID and is to be implemented in the [TextureDraw](#getEventTextureDraw_Event) event handler. This method can be used for implementing GPU-based terrain modifications (e.g. brushes) that require comprehensive access to both [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md) and detailed [virtual texture data](../../../../objects/objects/terrain/landscape_terrain/index.md#virtual_texture) beyond the target area.
### Arguments

- *int* **operation_id** - Draw [operation ID](#generateOperationID_int).
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the landscape layer map file to be modified.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **coord** - Coordinates of the upper left corner of the landscape layer map data segment to be modified along the X and Y axes.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **resolution** - Resolution of the landscape layer map data segment to be modified along the X and Y axes, the value within range [0, 4096] along each axis.
- *int* **flags_file_data** - Data layer mask. A combination of [FLAGS_FILE_DATA_*](#FLAGS_FILE_DATA_HEIGHT) flags indicating data layers to be affected (heights, albedo, certain masks).
- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Math::[WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md)> &* **bounds_preload_lmaps** - [Bounding box](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) (world) specifying the area containing terrain tiles (all landscape layer maps) to be loaded to memory prior to making modifications.
- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Math::[WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md)> &* **bounds_preload_vtextures** - [Bounding box](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) (world) specifying the area containing terrain tiles (virtual textures, including surface color, normals, and height data) to be loaded to memory prior to making modifications.

## void asyncTextureDraw ( const UGUID & file_guid , const Math:: ivec2 & coord , const Math:: ivec2 & resolution , int flags_file_data , const Vector < Math:: WorldBoundBox > & bounds_preload_lmaps , const Vector < Math:: WorldBoundBox > & bounds_preload_vtextures )

Commences an asynchronous GPU-based drawing operation with forced pre-loading of terrain data within the specified bounding boxes, including both landscape layer maps and virtual textures. The drawing operation represents a modification of the texture buffer of the specified size taken at specified coordinates and combining data layers defined by the specified flags. Preloaded [virtual texture data](../../../../objects/objects/terrain/landscape_terrain/index.md#virtual_texture) includes surface color (albedo), surface details (normal), and geometry height information (height) used for terrain tessellation. The operation is to be implemented in the [TextureDraw](#getEventTextureDraw_Event) event handler. This method can be used for implementing GPU-based terrain modifications (e.g. brushes) that require comprehensive access to both [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md) and detailed [virtual texture data](../../../../objects/objects/terrain/landscape_terrain/index.md#virtual_texture) beyond the target area.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the landscape layer map file to be modified.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **coord** - Coordinates of the upper left corner of the landscape layer map data segment to be modified along the X and Y axes.
- *const  Math::[ivec2](../../../../api/library/math/class.ivec2_cpp.md) &* **resolution** - Resolution of the landscape layer map data segment to be modified along the X and Y axes, the value within range [0, 4096] along each axis.
- *int* **flags_file_data** - Data layer mask. A combination of [FLAGS_FILE_DATA_*](#FLAGS_FILE_DATA_HEIGHT) flags indicating data layers to be affected (heights, albedo, certain masks).
- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Math::[WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md)> &* **bounds_preload_lmaps** - [Bounding box](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) (world) specifying the area containing terrain tiles (all landscape layer maps) to be loaded to memory prior to making modifications.
- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)< Math::[WorldBoundBox](../../../../api/library/math/bounds/class.worldboundbox_cpp.md)> &* **bounds_preload_vtextures** - [Bounding box](../../../../api/library/math/bounds/class.worldboundbox_cpp.md) (world) specifying the area containing terrain tiles (virtual textures, including surface color, normals, and height data) to be loaded to memory prior to making modifications.

## void asyncApplyDiff ( int operation_id , const UGUID & file_guid , const char * path )

Applies the state of the landscape layer map stored in the specified file to the landscape layer map file with the specified GUID.
### Arguments

- *int* **operation_id** - [Operation ID](#generateOperationID_int).
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the landscape layer map file to which a state stored at the specified path is to be applied.
- *const char ** **path** - Path to a file where the current landscape map modification state is stored.

## void asyncApplyDiff ( const UGUID & file_guid , const char * path )

Applies the state of the landscape layer map stored in the specified file to the landscape layer map file with the specified GUID.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the landscape layer map file to which a state stored at the specified path is to be applied.
- *const char ** **path** - Path to a file where the current landscape map modification state is stored.

## void asyncSaveFile ( int operation_id , const UGUID & file_guid )

Saves the landscape layer map file with the specified GUID.
### Arguments

- *int* **operation_id** - [Operation ID](#generateOperationID_int).
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the landscape layer map file.

## void asyncSaveFile ( const UGUID & file_guid )

Saves the landscape layer map file with the specified GUID.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the landscape layer map file.

## void asyncSaveFile ( int operation_id , const UGUID & file_guid , const char * path_new_diff , const char * path_old_diff )

Saves the specified landscape layer map file applying all changes along with saving old and new states (diff) to temporary files. These temporary files can be used to perform undo/redo operations via the [*applyDiff()*](#asyncApplyDiff_UGUID_cstr_void) method.
### Arguments

- *int* **operation_id** - [Operation ID](#generateOperationID_int).
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the landscape layer map file.
- *const char ** **path_new_diff** - Path to a file to store the new landscape layer map state.
- *const char ** **path_old_diff** - Path to a file to store the old landscape layer map state.

## void asyncSaveFile ( const UGUID & file_guid , const char * path_new_diff , const char * path_old_diff )

Saves the specified landscape layer map file applying all changes along with saving old and new states (diff) to temporary files. These temporary files can be used to perform undo/redo operations via the [*applyDiff()*](#asyncApplyDiff_UGUID_cstr_void) method.
```cpp
UGUID lmap_file_guid;	// .lmap file GUID
String cache_path;		// path to some cache directory

String new_filepath;	// path to store a new state
String old_filepath;	// path to store an old state

// method implementing the "apply" operation
void apply() override
{
	// generating necessary paths to save states (generate_filepath - some abstract method)
	new_filepath = generate_filepath(cache_path);
	old_filepath_ = generate_filepath(cache_path);

	// applying changes and saving current and previous states
	Landscape::asyncSaveFile(lmap_file_guid, new_filepath, old_filepath);
}

// method implementing the "undo" operation by applying the previous saved state
void undo() override
{
	if (!old_filepath.empty())
		Landscape::asyncApplyDiff(lmap_file_guid, old_filepath);
}

// method implementing the "redo" operation by applying the new saved state
void redo() override
{
	if (!new_filepath.empty())
		Landscape::asyncApplyDiff(lmap_file_guid, new_filepath);
}

```


### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the landscape layer map file.
- *const char ** **path_new_diff** - Path to a file to store the new landscape layer map state.
- *const char ** **path_old_diff** - Path to a file to store the old landscape layer map state.

## void filesClose ( const Vector < UGUID > & reload_files )

Closes `.lmap` files for all [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md) and reloads the ones with specified GUIDs. This method should be called before making any changes (modification, deletion, renaming) to `.lmap` files of the landscape terrain object to avoid conflicts, as these files are streamed continuosly by the Engine. Thus, by calling this method you inform the Engine that it should stop streaming terrain data. The list informs the Engine which files are no longer valid and should be reloaded or removed. As you're done with modification you should call the [*filesOpen()*](#filesOpen_void) method to resume streaming operations.
### Arguments

- *const [Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[UGUID](../../../../api/library/filesystem/class.uguid_cpp.md)> &* **reload_files** - List of [GUIDs](../../../../api/library/filesystem/class.uguid_cpp.md) of `.lmap` files to be reloaded. This list should contain `.lmap` files, that were deleted or having their data changed (albedo, heights, masks). If there are no such files, you can simply call the [*filesClose()*](#filesClose_void) method.

## void filesClose ( )

 Closes `.lmap` files for all [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md).This method should be called before making any changes (modification, deletion, renaming) to `.lmap` files of the landscape terrain object to avoid conflicts, as these files are streamed continuosly by the Engine. Thus, by calling this method you inform the Engine that it should stop streaming terrain data. As you're done with modification you should call the [*filesOpen()*](#filesOpen_void) method to resume streaming operations.
## void filesOpen ( )

 Opens `.lmap` files for all [landscape layer maps](../../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md).This method should be called after making any changes (modification, deletion, renaming) to `.lmap` files of the landscape terrain object. Prior to making such modifications the [*filesClose()*](#filesClose_void) method should be called.
## Ptr < ObjectLandscapeTerrain > getActiveTerrain ( )

Returns the current active [Landscape Terrain](../../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md) object.
> **Notice:** If a scene contains multiple Landscape Terrain objects, only one of them can be active (rendered).


### Return value

[Landscape Terrain](../../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md) object that is currently active.
## int generateOperationID ( )

Generates a new ID for the operation. This ID is used to manage operations.
```cpp
int id = Landscape::generateOperationID();
// user's code (bounding to ID)
Landscape::asyncTextureDraw(id, file_guid, coord, resolution, flags_file_data);

```


### Return value

New operation ID.
## void asyncResetModifications ( int operation_id , const UGUID & file_guid )

Asynchronously resets all unsaved modifications that were made to the landscape layer map identified by file GUID.
### Arguments

- *int* **operation_id** - Draw [operation ID](#generateOperationID_int).
- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the landscape layer map file to be restored.

## void asyncResetModifications ( const UGUID & file_guid )

Asynchronously resets all unsaved modifications that were made to the landscape layer map identified by file GUID.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - [GUID](../../../../api/library/filesystem/class.uguid_cpp.md) of the landscape layer map file to be restored.
