# Working with Landscape Terrain via Code (CPP)


This article describes how to create and modify the *[Landscape Terrain](../../../objects/objects/terrain/landscape_terrain/index.md)* object via code. But before we get down to coding, let's start with a bit of theory.


The surface of *Landscape Terrain* (*[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md)* class) is represented by a single or multiple rectangular layers called Landscape Layer Maps (*[LandscapeLayerMap](../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md)* class). By creating and arranging layer maps you define the look and functionality of the terrain.


To see a terrain, **at least one *Landscape Layer Map* is required**. Data of each Landscape Layer Map (*heights, albedo*, and *masks*) is stored in an `.lmap` file. To create such a file the *[LandscapeMapFileCreator](../../../api/library/objects/landscape_terrain/class.landscapemapfilecreator_cpp.md)* class is used. If you want to load, modify, and apply settings stored in this file later, use the *[LandscapeMapFileSettings](../../../api/library/objects/landscape_terrain/class.landscapemapfilesettings_cpp.md)* class.


*Landscape Terrain* rendering and modification is managed via the *[Landscape](../../../api/library/objects/landscape_terrain/class.landscape_cpp.md)* class.


There is a set of API classes used to manage the *Landscape Terrain* object:


- *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md)* � managing general *Landscape Terrain* object parameters.
- *[TerrainDetail](../../../api/library/objects/landscape_terrain/class.terraindetail_cpp.md)* � managing terrain details that define its appearance. Details are organized into a hierarchy, each of them can have an unlimited number of children. Details are attached to detail masks and are drawn in accordance with their rendering order (the one with the highest order shall be rendered above all others).
- *[TerrainDetailMask](../../../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md)* � managing terrain detail masks. Each detail mask can have an unlimited number of details.
- *[LandscapeFetch](../../../api/library/objects/landscape_terrain/class.landscapefetch_cpp.md)* � getting terrain data at a certain point (e.g. a height request) or check for an intersection with a traced line.
- *[LandscapeImages](../../../api/library/objects/landscape_terrain/class.landscapeimages_cpp.md)* � to edit landscape terrain via API.
- *[LandscapeTextures](../../../api/library/objects/landscape_terrain/class.landscapetextures_cpp.md)* � to edit landscape terrain via API.


### See Also


- **[C++ Sample set](../../../sdk/api_samples/cpp/terrain_modification_usage.md)** demonstrating various Landscape Terrain features and use cases


## Creating a Terrain


To create a Landscape Terrain based on arbitrary height and albedo maps, the following **workflow** is used:


1. Create a *[LandscapeMapFileCreator](../../../api/library/objects/landscape_terrain/class.landscapemapfilecreator_cpp.md)* instance, set necessary parameters (grid size, resolution, etc.) and generate a new `.lmap` file based on specified albedo and height images (tiles) via the *[Run()](../../../api/library/objects/landscape_terrain/class.landscapemapfilecreator_cpp.md#run_int_int_int)* method. Here you can subscribe for events at different stages of creation.
2. Create a *[LandscapeMapFileSettings](../../../api/library/objects/landscape_terrain/class.landscapemapfilesettings_cpp.md)* instance, load target `.lmap` file for settings, set necessary parameters (opacity and blending for height and albedo data) and apply them.
3. Create a new *[ObjectLandscapeTerrain](../../../api/library/objects/landscape_terrain/class.objectlandscapeterrain_cpp.md)* object.
4. Create a *[LandscapeLayerMap](../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md)* based on the previously created `.lmap` file.


### Preparing a Project


Before we get to code, perform the following:


1. Open *SDK Browser* and [create a new C# (.NET) or C++ project](../../../sdk/projects/index_cpp.md#creation) depending on the programming language selected.
2. Open your project in UnigineEditor via the **Open Editor** button in *SDK Browser*.
3. Save the following images to your computer: | Albedo Map | Height Map | |---|---| | ![Albedo Map](albedo.png) | ![Height Map](height.png) |
4. Drag the `height.png` file directly to the *[Asset Browser](../../../editor2/assets_workflow/index.md#asset_browser)* window to add it to your project. In the Import Dialog for your height map, set *Image Format* to R32F and click **Yes**.
5. Drag the `albedo.png` file directly to the *[Asset Browser](../../../editor2/assets_workflow/index.md#asset_browser)* window too. In the Import Dialog for your height map, set *Texture Preset* to **Albedo (RGB � color, A � opacity)** and click **Yes**.


### Code


Copy the source code below and paste it to the corresponding source files of your project.


In the `AppWorldLogic.h` file, define all parameters required for terrain creation, as well as the terrain itself with a layer map.


<details>
<summary>AppWorldLogic.h | Close</summary>

`AppWorldLogic.h`


```cpp
#ifndef __APP_WORLD_LOGIC_H__
#define __APP_WORLD_LOGIC_H__

#include <UnigineLogic.h>
#include <UnigineStreams.h>
#include <UnigineObjects.h>
#include <UnigineImage.h>

class AppWorldLogic : public Unigine::WorldLogic
{
	// Layer map parameters
	// position, rotation and scaling factor along the Z axis
	Unigine::Math::Vec3 lmapPosition = Unigine::Math::Vec3_zero;
	float lmapRotation = 0.0f;
	float lmapHeightScale = 1.0f;

	// size of the layer map (in units)
	Unigine::Math::Vec2 lmapSize = Unigine::Math::Vec2(20.0f, 20.0f);

	// landscape layer map grid size (number of cells along X and Y axes)
	int lmapGridSizeX = 2;
	int lmapGridSizeY = 2;

	// resolution of a single tile of the layer map
	// (tile images to be used must have the same resolution)
	int lmapTileResolutionX = 512;
	int lmapTileResolutionY = 512;

	// layer map name
	Unigine::String lmapName = "map";

	// set of images for a single tile
	struct TileImages
	{
		Unigine::String albedoImagePath;
		Unigine::String heightImagePath;
	};

	// vector for the tileset data
	Unigine::Vector<TileImages> tiles;

	// pointers to the terrain and landscape map (at least one is required)
	Unigine::ObjectLandscapeTerrainPtr terrain;
	Unigine::LandscapeLayerMapPtr lmap;

public:
	AppWorldLogic();
	virtual ~AppWorldLogic();

	int init() override;

	int update() override;
	int postUpdate() override;
	int updatePhysics() override;

	int shutdown() override;

	void makeTileset();
	void applySettings();
	void createTerrain();
	Unigine::EventConnections connections;
	// event handlers for different stages of landscape layer map creation
	void OnCreatorCreate(const Unigine::LandscapeMapFileCreatorPtr &creator, const Unigine::LandscapeImagesPtr &images, int x, int y);
	void OnCreatorBegin(const Unigine::LandscapeMapFileCreatorPtr &creator);
	void OnCreatorProgress(const Unigine::LandscapeMapFileCreatorPtr &creator);
	void OnCreatorEnd(const Unigine::LandscapeMapFileCreatorPtr &creator);
};

#endif // __APP_WORLD_LOGIC_H__

```

</details>


Insert the following code implementing terrain creation into the `AppWorldLogic.cpp` file.


> **Notice:** Unchanged methods of the *AppWorldLogic* class are not listed here, so leave them as they are.


<details>
<summary>AppWorldLogic.cpp | Close</summary>

`AppWorldLogic.cpp`


```cpp
#include "AppWorldLogic.h"
#include <UnigineConsole.h>
#include <UnigineFileSystem.h>
#include <UnigineInput.h>
#include <UnigineGame.h>
#include <UnigineWorld.h>
using namespace Unigine;
using namespace Math;

// function to be fired on creating a tile
void AppWorldLogic::OnCreatorCreate(const LandscapeMapFileCreatorPtr &creator, const LandscapeImagesPtr &images, int x, int y)
{
	// get number of the current tile
	int tileNumber = x * lmapGridSizeY + y;
	Log::message("Create tile %d\n", tileNumber);

	// set albedo for current tile
	if (FileSystem::isFileExist(tiles[tileNumber].albedoImagePath))
	{
		ImagePtr albedoImage = Image::create(tiles[tileNumber].albedoImagePath);
		if (albedoImage && (albedoImage->getWidth() == lmapTileResolutionX) && (albedoImage->getHeight() == lmapTileResolutionY))
		{
			ImagePtr albedo = images->getAlbedo();
			albedo->create2D(albedoImage->getWidth(), albedoImage->getHeight(), albedoImage->getFormat(), albedoImage->getNumMipmaps());
			albedo->copy(albedoImage, 0, 0, 0, 0, albedoImage->getWidth(), albedoImage->getHeight());
		}
		else
			Log::error("The albedo image cannot be loaded, or its resolution does not match the resolution of tile.\n");
	}
	else
		Log::error("Albedo file does not exist.\n");

	// set height for current tile
	if (FileSystem::isFileExist(tiles[tileNumber].heightImagePath))
	{
		ImagePtr heightImage = Image::create(tiles[tileNumber].heightImagePath);
		if (heightImage && (heightImage->getWidth() == lmapTileResolutionX) && (heightImage->getHeight() == lmapTileResolutionY))
		{
			ImagePtr height = images->getHeight();
			height->create2D(heightImage->getWidth(), heightImage->getHeight(), heightImage->getFormat(), heightImage->getNumMipmaps());
			height->copy(heightImage, 0, 0, 0, 0, heightImage->getWidth(), height->getHeight());
		}
		else
			Log::error("The height image cannot be loaded, or its resolution does not match the resolution of tile.\n");
	}
	else
		Log::error("Height file does not exist.\n");
}

// function to be executed on beginning the landscape map file generation process
void AppWorldLogic::OnCreatorBegin(const LandscapeMapFileCreatorPtr &creator)
{
	Log::message("--------------------\n");
	Log::message("--- %s creation started ---\n", creator->getPath());
	Log::message("lmap creator begin\n");
}

// function to be used for visualizing landscape map file generation progress
void AppWorldLogic::OnCreatorProgress(const LandscapeMapFileCreatorPtr &creator)
{
	Log::message("lmap creator progress: %d\n", creator->getProgress());
}

// function to be executed on beginning the landscape map generation process
void AppWorldLogic::OnCreatorEnd(const LandscapeMapFileCreatorPtr &creator)
{
	Log::message("lmap creator end\n");
	Log::message("--- %s created ---\n", creator->getPath());
	Log::message("--------------------\n");

	// after creating .lmap file apply settings
	applySettings();

	// and create terrain
	createTerrain();
}

// function applying .lmap file settings
void AppWorldLogic::applySettings()
{
	// load target .lmap file for settings
	LandscapeMapFileSettingsPtr settings = LandscapeMapFileSettings::create();
	settings->load(FileSystem::getGUID(String::format("%s.lmap", lmapName.get())));

	// set parameters and apply them
	if (settings->isLoaded())
	{
		// set alpha blend for height and albedo
		settings->setHeightBlending(Landscape::BLENDING_MODE::ALPHA_BLEND);
		settings->setAlbedoBlending(Landscape::BLENDING_MODE::ALPHA_BLEND);

		settings->setEnabledHeight(true);
		settings->setEnabledAlbedo(true);

		// disable opacity for height and albedo
		settings->setEnabledOpacityAlbedo(false);
		settings->setEnabledOpacityHeight(false);

		settings->apply();
	}
}
// function creating the Landscape Terrain object using the generated .lmap file
void AppWorldLogic::createTerrain()
{
	// create new terrain
	terrain = ObjectLandscapeTerrain::create();
	terrain->setActiveTerrain(true);
	terrain->setCollision(true, 0);

	// create layer map based on created .lmap file
	lmap = LandscapeLayerMap::create();
	lmap->setParent(Landscape::getActiveTerrain());
	lmap->setPath(String::format("%s.lmap", lmapName.get()));
	lmap->setName(lmapName.get());
	lmap->setSize(lmapSize);
	lmap->setHeightScale(lmapHeightScale);
	lmap->setWorldPosition(lmapPosition);
	lmap->setWorldRotation(quat(vec3_up, lmapRotation));
}

// function creating the Landscape Terrain object using the generated .lmap file
void AppWorldLogic::makeTileset()
{
	// filling
	TileImages timg;
	timg.albedoImagePath = "albedo.png";
	timg.heightImagePath = "height.png";
	int n_tiles = lmapGridSizeX * lmapGridSizeY;
	while (tiles.size() < n_tiles)
		tiles.append(timg);
}
AppWorldLogic::AppWorldLogic()
{
}

AppWorldLogic::~AppWorldLogic()
{
}

int AppWorldLogic::init()
{
	// set the camera
	Game::getPlayer()->setPosition(Vec3(0.0f, lmapSize.y, 8.0f));
	Game::getPlayer()->worldLookAt(Vec3(lmapSize.x / 2, lmapSize.y / 2, 0.0f));

	// disable nodes created in the template world by default
	NodePtr content_root = World::getNodeByName("content");
	if (content_root)
		content_root->setEnabled(false);
	//enable displaying console messages
	Console::run("console_onscreen 1");

	// collect the tileset
	makeTileset();

	// create .lmap file based on tiles with albedo and height images
	LandscapeMapFileCreatorPtr lmapCreator = LandscapeMapFileCreator::create();
	lmapCreator->setGrid(ivec2(lmapGridSizeX, lmapGridSizeY));
	lmapCreator->setResolution(ivec2(lmapTileResolutionX * lmapGridSizeX, lmapTileResolutionY * lmapGridSizeY));

	lmapCreator->setPath(String::format("%s.lmap", lmapName.get()));

	// subscribe for different stages of *.lmap file creation
	lmapCreator->getEventCreate().connect(connections, this, &AppWorldLogic::OnCreatorCreate);
	lmapCreator->getEventBegin().connect(connections, this, &AppWorldLogic::OnCreatorBegin);
	lmapCreator->getEventProgress().connect(connections, this, &AppWorldLogic::OnCreatorProgress);
	lmapCreator->getEventEnd().connect(connections, this, &AppWorldLogic::OnCreatorEnd);

	// start the creation process
	lmapCreator->run();
	return 1;
}

////////////////////////////////////////////////////////////////////////////////
// start of the main loop
////////////////////////////////////////////////////////////////////////////////
// - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
// 												(3)
// - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
int AppWorldLogic::update()
{
	return 1;
}
int AppWorldLogic::postUpdate()
{
	// The engine calls this function after updating each render frame: correct behavior after the state of the node has been updated.
	return 1;
}

int AppWorldLogic::updatePhysics()
{
	// Write here code to be called before updating each physics frame: control physics in your application and put non-rendering calculations.
	// The engine calls updatePhysics() with the fixed rate (60 times per second by default) regardless of the FPS value.
	// WARNING: do not create, delete or change transformations of nodes here, because rendering is already in progress.
	return 1;
}

////////////////////////////////////////////////////////////////////////////////
// end of the main loop
////////////////////////////////////////////////////////////////////////////////

int AppWorldLogic::shutdown()
{
	return 1;
}

```

</details>


## Modifying Terrain By Adding New Layer Maps


Spawn new *Landscape Layer Maps (LandscapeLayerMap)* to modify terrain surface, these layer maps can represent vehicle tracks, chunks of trenches, or pits. This way is similar to using Decals: **each layer is a separate node, so you can control each modification separately.** Moreover, using *Landscape Layer Map* implies no data density limits, enabling you to achieve realistic results with high-quality insets.


![](../../../objects/objects/terrain/landscape_terrain/runtime_trace_low.gif)


### Adding Assets


Let's create a new layer map for a crater, to do so, perform the following actions:


1. Save the following images to be used for the crater to your computer: | Crater Albedo Map | Crater Height Map | |---|---| | ![Crater Albedo Map](crater_albedo.png) | ![Crater Height Map](crater_height.png) |
2. Switch to UnigineEditor and Drag the `crater_height.png` file directly to the *[Asset Browser](../../../editor2/assets_workflow/index.md#asset_browser)* window to add it to your project (just like you did before for the terrain's *Height* map). In the Import Dialog for your height map, set *Image Format* to **R32F** and click **Yes**.
3. Drag the `crater_albedo.png` file directly to the *[Asset Browser](../../../editor2/assets_workflow/index.md#asset_browser)* window (just like you did before for the terrain's *Albedo* map). In the Import Dialog for your albedo map set *Texture Preset* to **Albedo (RGB � color, A � opacity)** and click **Yes**.
4. Select *Create -> Create Landscape Layer Map* in the *[Asset Browser](../../../editor2/assets_workflow/index.md#asset_browser)*. ![](create_lmap.png)
5. Enter a name for the layer map: `crater`.
6. Select your new `crater.lmap` asset and adjust its settings as shown below (assign our images, select blending mode and adjust heights range for the crater). ![](adjust_lmap.png)
7. Click **Reimport** and process to the **Code** section below.


### Code


So, we have a layer map file representing a crater (`crater.lmap`). To add a crater to the landscape surface at the desired location we simply create a new *LandscapeLayerMap* using our file and set its size and transformation.


Let's implement a method spawning a crater at a specified location (***AddCrater()***):


```cpp
// method spawning a new crater at the specified location
LandscapeLayerMapPtr AddCrater(float x, float y) {
	// create a new layer map
	LandscapeLayerMapPtr crater_lmap = LandscapeLayerMap::create();

	// add the layer map as a child to the active terrain
	crater_lmap->setParent(Landscape::getActiveTerrain());

	// set a path to the crater.lmap file representing a crater
	crater_lmap->setPath(String::format("crater.lmap"));
	crater_lmap->setName("crater");

	// set the size of the crater layer to 5x5 units
	crater_lmap->setSize(Vec2(5.0f, 5.0f));

	// set the height scale multiplier
	crater_lmap->setHeightScale(0.5f);

	// set the position and rotation of the new layer
	crater_lmap->setWorldPosition(Vec3(x, y, 0.0f));
	crater_lmap->setWorldRotation(quat(vec3_up, 35.0f));

	// set the order of the new layer to place is above the first one (basic)
	crater_lmap->setOrder(2);

	return crater_lmap;
}


```


> **Notice:** Although layer maps are relatively light and fast, genereating too many of them may drop performance.


This approach is **non-destructive** (i.e., it does not irreversibly change initial terrain data). To see the underlaying layer again in its initial state simply disable an overlaying layer map:


```cpp
crater_lmap->setEnabled(false);


```


For example, after disabling a layer map representing a crater, you'll have the surface looking just the way it was before the explosion.


To illustrate that let's add the *AddCrater()* method described above to our `AppWorldLogic.cpp` file, declare a vector to store all spawned craters, and add handlers for *Enter* key (spawn a new crater) and *Backspace* key (show/hide all craters) in the *AppWorldLogic::update()* method:


```cpp
// declare a vector to store craters
Unigine::Vector<Unigine::LandscapeLayerMapPtr> craters;

int AppWorldLogic::update()
{
	if (Input::isKeyDown(Input::KEY_BACKSPACE))// spawning a new crater at a random point
		craters.append(AddCrater(Game::getRandomFloat(0.0f, lmapSize.x), Game::getRandomFloat(0.0f, lmapSize.y)));
	else if (Input::isKeyDown(Input::KEY_ENTER))// hiding all craters to show initial landscape state
		for (Vector<LandscapeLayerMapPtr>::Iterator it = craters.begin(); it != craters.end(); ++it)
			it->get()->setEnabled(!it->get()->isEnabled());
	return 1;
}

int AppWorldLogic::shutdown()
{
	// delete all spawned craters
	for (Vector<LandscapeLayerMapPtr>::Iterator it = craters.begin(); it != craters.end(); ++it)
		(*it).deleteLater();
	return 1;
}


```


## GPU-Based Terrain Modification


Terrain modification is performed in asynchronous mode on GPU side by calling the *[asyncTextureDraw](../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#asyncTextureDraw_int_UGUID_ivec2_ivec2_int_VECWorldBoundBox_void)* method of the *Landscape* class, that commences a drawing operation. The operation itself is to be implemented inside an event handler.


The workflow here is as follows:


1. Implement your GPU-based terrain modification logic in a function.
2. Set this handler function when subscribing for the *Texture Draw* event (when GPU-based terrain modification operation is performed) via *[getEventTextureDraw()](../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#getEventTextureDraw_Event)*.
3. Commence a GPU drawing operation by calling the *[asyncTextureDraw()](../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#asyncTextureDraw_UGUID_ivec2_ivec2_int_void)* method. Here you should specify the GUID of an `.lmap` file of the [landscape layer map](../../../api/library/objects/landscape_terrain/class.landscapelayermap_cpp.md) to be modified, the coordinates of the top-left corner and the resolution of the segment of data to be modified, you should also define which data layers are to be affected (*heights, albedo, masks*) via a set of [flags](../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#FLAGS_FILE_DATA_HEIGHT). > **Notice:** If your modification requires additional data beyond the specified area as well as data of other landscape layer maps (e.g. a copy brush), you can enable force loading of required data. In this case you should use [this overload of the *asyncTextureDraw()* method](../../../api/library/objects/landscape_terrain/class.landscape_cpp.md#asyncTextureDraw_UGUID_ivec2_ivec2_int_VECWorldBoundBox_void).


### Adding Assets


Let us modify the *Heights* and *Albedo* data of the terrain, so we need two custom maps for that. Save the following images to your computer and drag them to the *[Asset Browser](../../../editor2/assets_workflow/index.md#asset_browser)* window to add them to your project (just like you did before for the terrain's *Albedo* and *Height* maps):


| Custom Albedo Map | Custom Height Map |
|---|---|
| ![Custom Albedo Map](custom_albedo.png) | ![Custom Height Map](custom_height.png) |


Don't forget to set *Image Format* to **R32F** for your height map and set *Texture Preset* to **Albedo (RGB � color, A � opacity)** for your albedo map and reimport them with new settings.


### Code


Insert the following code into the `AppWorldLogic.cpp` file.


> **Notice:** Unchanged methods of the *AppWorldLogic* class are not listed here, so leave them as they are.


```cpp
// - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
// 												(1)
// - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
// images to be used for terrain modification
Unigine::ImagePtr custom_albedo_image1;
Unigine::ImagePtr custom_height_image1;

// function to be executed on commencing a texture draw operation
void my_texture_draw(const UGUID &guid, int id, const LandscapeTexturesPtr &buffer, const ivec2 &coord, int data_mask)
{
	// preparing images for terrain modification
	// Note: image preparation block can be moved outside the event handler, not to repeat these operations every time,
	// e.g. you can move this block to a place before calling the asyncTextureDraw() method
	{
		// create a new image to load a custom albedo map to
		custom_albedo_image1 = Image::create("custom_albedo.png");

		// set the format required for the albedo map - RGBA8
		custom_albedo_image1->convertToFormat(Image::FORMAT_RGBA8);

		// create a new image to load a custom height map to
		custom_height_image1 = Image::create("custom_height.png");

		// set the format required for the heightmap - R32F
		custom_height_image1->convertToFormat(Image::FORMAT_R32F);
	}
	// resize albedo and height images to fit the area to be modified
	custom_albedo_image1->resize(buffer->getResolution().x, buffer->getResolution().y);
	custom_height_image1->resize(buffer->getResolution().x, buffer->getResolution().y);

	// setting our custom image to the albedo buffer
	buffer->getAlbedo()->setImage(custom_albedo_image1);

	// setting our custom image to the height buffer
	buffer->getHeight()->setImage(custom_height_image1);
}

// - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
// 												(2)
// - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

int AppWorldLogic::init()
{
	// add a function to be executed on a Texture Draw operation
	Landscape::getEventTextureDraw().connect(connections, my_texture_draw);
	return 1;
}

// - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
// 												(3)
// - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -

int AppWorldLogic::update()
{
	if (Input::isKeyPressed(Input::KEY_SPACE)) {
		// get the first layermap that we're going to modify
		LandscapeLayerMapPtr lmap = checked_ptr_cast <LandscapeLayerMap> (terrain->getChild(0));

		// generate new ID for the draw operation
		int id = Landscape::generateOperationID();

		// user's code (bounding to ID)
		// commence a Texture Draw operation for the selected landscape map at (10, 10) with the size of [512 x 512]
		Landscape::asyncTextureDraw(id, lmap->getGUID(), ivec2(10, 10), ivec2(512, 512), (int)(Landscape::FLAGS_FILE_DATA_HEIGHT | Landscape::FLAGS_FILE_DATA_ALBEDO));
	}
	return 1;
}

int AppWorldLogic::shutdown()
{
	// remove all event subscriptions on shutdown
	connections.disconnectAll();
	return 1;
}


```


## Resulting Demonstration Code


Copy the source code below and paste it to the corresponding source files of your project.


<details>
<summary>AppWorldLogic.h | Close</summary>

`AppWorldLogic.h`


```cpp
#ifndef __APP_WORLD_LOGIC_H__
#define __APP_WORLD_LOGIC_H__

#include <UnigineLogic.h>
#include <UnigineStreams.h>
#include <UnigineObjects.h>
#include <UnigineImage.h>

class AppWorldLogic : public Unigine::WorldLogic
{
	// Layer map parameters
	// position, rotation and scaling factor along the Z axis
	Unigine::Math::Vec3 lmapPosition = Unigine::Math::Vec3_zero;
	float lmapRotation = 0.0f;
	float lmapHeightScale = 1.0f;

	// size of the layer map (in units)
	Unigine::Math::Vec2 lmapSize = Unigine::Math::Vec2(20.0f, 20.0f);

	// landscape layer map grid size (number of cells along X and Y axes)
	int lmapGridSizeX = 2;
	int lmapGridSizeY = 2;

	// resolution of a single tile of the layer map
	// (tile images to be used must have the same resolution)
	int lmapTileResolutionX = 512;
	int lmapTileResolutionY = 512;

	// layer map name
	Unigine::String lmapName = "map";

	// set of images for a single tile
	struct TileImages
	{
		Unigine::String albedoImagePath;
		Unigine::String heightImagePath;
	};

	// vector for the tileset data
	Unigine::Vector<TileImages> tiles;

	// pointers to the terrain and landscape map (at least one is required)
	Unigine::ObjectLandscapeTerrainPtr terrain;
	Unigine::LandscapeLayerMapPtr lmap;

public:
	AppWorldLogic();
	virtual ~AppWorldLogic();

	int init() override;

	int update() override;
	int postUpdate() override;
	int updatePhysics() override;

	int shutdown() override;

	void makeTileset();
	void applySettings();
	void createTerrain();
	Unigine::EventConnections connections;
	// event handlers for different stages of landscape layer map creation
	void OnCreatorCreate(const Unigine::LandscapeMapFileCreatorPtr &creator, const Unigine::LandscapeImagesPtr &images, int x, int y);
	void OnCreatorBegin(const Unigine::LandscapeMapFileCreatorPtr &creator);
	void OnCreatorProgress(const Unigine::LandscapeMapFileCreatorPtr &creator);
	void OnCreatorEnd(const Unigine::LandscapeMapFileCreatorPtr &creator);
};

#endif // __APP_WORLD_LOGIC_H__

```

</details>


<details>
<summary>AppWorldLogic.cpp | Close</summary>

`AppWorldLogic.cpp`


```cpp
#include "AppWorldLogic.h"
#include <UnigineConsole.h>
#include <UnigineFileSystem.h>
#include <UnigineInput.h>
#include <UnigineGame.h>
#include <UnigineWorld.h>
using namespace Unigine;
using namespace Math;

// images to be used for terrain modification
Unigine::ImagePtr custom_albedo_image1;
Unigine::ImagePtr custom_height_image1;

// function to be executed on commencing a texture draw operation
void my_texture_draw(const UGUID &guid, int id, const LandscapeTexturesPtr &buffer, const ivec2 &coord, int data_mask)
{
	// resize albedo and height images to fit the area to be modified
	custom_albedo_image1->resize(buffer->getResolution().x, buffer->getResolution().y);
	custom_height_image1->resize(buffer->getResolution().x, buffer->getResolution().y);

	// setting our custom image to the albedo buffer
	buffer->getAlbedo()->setImage(custom_albedo_image1);

	// setting our custom image to the height buffer
	buffer->getHeight()->setImage(custom_height_image1);
}
// declare a vector to store craters
Unigine::Vector<Unigine::LandscapeLayerMapPtr> craters;
// method spawning a new crater at the specified location
LandscapeLayerMapPtr AddCrater(float x, float y) {
	// create a new layer map
	LandscapeLayerMapPtr crater_lmap = LandscapeLayerMap::create();

	// add the layer map as a child to the active terrain
	crater_lmap->setParent(Landscape::getActiveTerrain());

	// set a path to the crater.lmap file representing a crater
	crater_lmap->setPath(String::format("crater.lmap"));
	crater_lmap->setName("crater");

	// set the size of the crater layer to 5x5 units
	crater_lmap->setSize(Vec2(5.0f, 5.0f));

	// set the height scale multiplier
	crater_lmap->setHeightScale(0.5f);

	// set the position and rotation of the new layer
	crater_lmap->setWorldPosition(Vec3(x, y, 0.0f));
	crater_lmap->setWorldRotation(quat(vec3_up, 35.0f));

	// set the order of the new layer to place is above the first one (basic)
	crater_lmap->setOrder(2);

	return crater_lmap;
}

// function to be fired on creating a tile
void AppWorldLogic::OnCreatorCreate(const LandscapeMapFileCreatorPtr &creator, const LandscapeImagesPtr &images, int x, int y)
{
	// get number of the current tile
	int tileNumber = x * lmapGridSizeY + y;
	Log::message("Create tile %d\n", tileNumber);

	// set albedo for current tile
	if (FileSystem::isFileExist(tiles[tileNumber].albedoImagePath))
	{
		ImagePtr albedoImage = Image::create(tiles[tileNumber].albedoImagePath);
		if (albedoImage && (albedoImage->getWidth() == lmapTileResolutionX) && (albedoImage->getHeight() == lmapTileResolutionY))
		{
			ImagePtr albedo = images->getAlbedo();
			albedo->create2D(albedoImage->getWidth(), albedoImage->getHeight(), albedoImage->getFormat(), albedoImage->getNumMipmaps());
			albedo->copy(albedoImage, 0, 0, 0, 0, albedoImage->getWidth(), albedoImage->getHeight());
		}
		else
			Log::error("The albedo image cannot be loaded, or its resolution does not match the resolution of tile.\n");
	}
	else
		Log::error("Albedo file does not exist.\n");

	// set height for current tile
	if (FileSystem::isFileExist(tiles[tileNumber].heightImagePath))
	{
		ImagePtr heightImage = Image::create(tiles[tileNumber].heightImagePath);
		if (heightImage && (heightImage->getWidth() == lmapTileResolutionX) && (heightImage->getHeight() == lmapTileResolutionY))
		{
			ImagePtr height = images->getHeight();
			height->create2D(heightImage->getWidth(), heightImage->getHeight(), heightImage->getFormat(), heightImage->getNumMipmaps());
			height->copy(heightImage, 0, 0, 0, 0, heightImage->getWidth(), height->getHeight());
		}
		else
			Log::error("The height image cannot be loaded, or its resolution does not match the resolution of tile.\n");
	}
	else
		Log::error("Height file does not exist.\n");
}

// function to be executed on beginning the landscape map file generation process
void AppWorldLogic::OnCreatorBegin(const LandscapeMapFileCreatorPtr &creator)
{
	Log::message("--------------------\n");
	Log::message("--- %s creation started ---\n", creator->getPath());
	Log::message("lmap creator begin\n");
}

// function to be used for visualizing landscape map file generation progress
void AppWorldLogic::OnCreatorProgress(const LandscapeMapFileCreatorPtr &creator)
{
	Log::message("lmap creator progress: %d\n", creator->getProgress());
}

// function to be executed on beginning the landscape map generation process
void AppWorldLogic::OnCreatorEnd(const LandscapeMapFileCreatorPtr &creator)
{
	Log::message("lmap creator end\n");
	Log::message("--- %s created ---\n", creator->getPath());
	Log::message("--------------------\n");

	// after creating .lmap file apply settings
	applySettings();

	// and create terrain
	createTerrain();
}

// function applying .lmap file settings
void AppWorldLogic::applySettings()
{
	// load target .lmap file for settings
	LandscapeMapFileSettingsPtr settings = LandscapeMapFileSettings::create();
	settings->load(FileSystem::getGUID(String::format("%s.lmap", lmapName.get())));

	// set parameters and apply them
	if (settings->isLoaded())
	{
		// set alpha blend for height and albedo
		settings->setHeightBlending(Landscape::BLENDING_MODE::ALPHA_BLEND);
		settings->setAlbedoBlending(Landscape::BLENDING_MODE::ALPHA_BLEND);

		settings->setEnabledHeight(true);
		settings->setEnabledAlbedo(true);

		// disable opacity for height and albedo
		settings->setEnabledOpacityAlbedo(false);
		settings->setEnabledOpacityHeight(false);

		settings->apply();
	}
}
// function creating the Landscape Terrain object using the generated .lmap file
void AppWorldLogic::createTerrain()
{
	// create new terrain
	terrain = ObjectLandscapeTerrain::create();
	terrain->setActiveTerrain(true);
	terrain->setCollision(true, 0);

	// create layer map based on created .lmap file
	lmap = LandscapeLayerMap::create();
	lmap->setParent(Landscape::getActiveTerrain());
	lmap->setPath(String::format("%s.lmap", lmapName.get()));
	lmap->setName(lmapName.get());
	lmap->setSize(lmapSize);
	lmap->setHeightScale(lmapHeightScale);
	lmap->setWorldPosition(lmapPosition);
	lmap->setWorldRotation(quat(vec3_up, lmapRotation));
}

// function creating the Landscape Terrain object using the generated .lmap file
void AppWorldLogic::makeTileset()
{
	// filling
	TileImages timg;
	timg.albedoImagePath = "albedo.png";
	timg.heightImagePath = "height.png";
	int n_tiles = lmapGridSizeX * lmapGridSizeY;
	while (tiles.size() < n_tiles)
		tiles.append(timg);
}
AppWorldLogic::AppWorldLogic()
{
}

AppWorldLogic::~AppWorldLogic()
{
}

int AppWorldLogic::init()
{
	// set the camera
	Game::getPlayer()->setPosition(Vec3(0.0f, lmapSize.y, 8.0f));
	Game::getPlayer()->worldLookAt(Vec3(lmapSize.x / 2, lmapSize.y / 2, 0.0f));

	// disable nodes created in the template world by default
	NodePtr content_root = World::getNodeByName("content");
	if (content_root)
		content_root->setEnabled(false);
	//enable displaying console messages
	Console::run("console_onscreen 1");

	// collect the tileset
	makeTileset();

	// create .lmap file based on tiles with albedo and height images
	LandscapeMapFileCreatorPtr lmapCreator = LandscapeMapFileCreator::create();
	lmapCreator->setGrid(ivec2(lmapGridSizeX, lmapGridSizeY));
	lmapCreator->setResolution(ivec2(lmapTileResolutionX * lmapGridSizeX, lmapTileResolutionY * lmapGridSizeY));

	lmapCreator->setPath(String::format("%s.lmap", lmapName.get()));

	// subscribe for different stages of *.lmap file creation
	lmapCreator->getEventCreate().connect(connections, this, &AppWorldLogic::OnCreatorCreate);
	lmapCreator->getEventBegin().connect(connections, this, &AppWorldLogic::OnCreatorBegin);
	lmapCreator->getEventProgress().connect(connections, this, &AppWorldLogic::OnCreatorProgress);
	lmapCreator->getEventEnd().connect(connections, this, &AppWorldLogic::OnCreatorEnd);

	// start the creation process
	lmapCreator->run();
	// preparing images for terrain modification
	// create a new image to load a custom albedo map to
	custom_albedo_image1 = Image::create("custom_albedo.png");

	// set the format required for the albedo map - RGBA8
	custom_albedo_image1->convertToFormat(Image::FORMAT_RGBA8);

	// create a new image to load a custom height map to
	custom_height_image1 = Image::create("custom_height.png");

	// set the format required for the heightmap - R32F
	custom_height_image1->convertToFormat(Image::FORMAT_R32F);
	// add a function to be executed on a Texture Draw operation
	Landscape::getEventTextureDraw().connect(connections, my_texture_draw);
	return 1;
}

////////////////////////////////////////////////////////////////////////////////
// start of the main loop
////////////////////////////////////////////////////////////////////////////////
int AppWorldLogic::update()
{
	if (Input::isKeyDown(Input::KEY_BACKSPACE))// spawning a new crater at a random point
		craters.append(AddCrater(Game::getRandomFloat(0.0f, lmapSize.x), Game::getRandomFloat(0.0f, lmapSize.y)));
	else if (Input::isKeyDown(Input::KEY_ENTER))// hiding all craters to show initial landscape state
		for (Vector<LandscapeLayerMapPtr>::Iterator it = craters.begin(); it != craters.end(); ++it)
			it->get()->setEnabled(!it->get()->isEnabled());
	if (Input::isKeyPressed(Input::KEY_SPACE)) {
		// get the first layermap that we're going to modify
		LandscapeLayerMapPtr lmap = checked_ptr_cast <LandscapeLayerMap> (terrain->getChild(0));

		// generate new ID for the draw operation
		int id = Landscape::generateOperationID();

		// user's code (bounding to ID)
		// commence a Texture Draw operation for the selected landscape map at (10, 10) with the size of [512 x 512]
		Landscape::asyncTextureDraw(id, lmap->getGUID(), ivec2(10, 10), ivec2(512, 512), (int)(Landscape::FLAGS_FILE_DATA_HEIGHT | Landscape::FLAGS_FILE_DATA_ALBEDO));
	}
	return 1;
}
int AppWorldLogic::postUpdate()
{
	// The engine calls this function after updating each render frame: correct behavior after the state of the node has been updated.
	return 1;
}

int AppWorldLogic::updatePhysics()
{
	// Write here code to be called before updating each physics frame: control physics in your application and put non-rendering calculations.
	// The engine calls updatePhysics() with the fixed rate (60 times per second by default) regardless of the FPS value.
	// WARNING: do not create, delete or change transformations of nodes here, because rendering is already in progress.
	return 1;
}

////////////////////////////////////////////////////////////////////////////////
// end of the main loop
////////////////////////////////////////////////////////////////////////////////

int AppWorldLogic::shutdown()
{
	// delete all spawned craters
	for (Vector<LandscapeLayerMapPtr>::Iterator it = craters.begin(); it != craters.end(); ++it)
		(*it).deleteLater();
	// remove all event subscriptions on shutdown
	connections.disconnectAll();
	return 1;
}

```

</details>
