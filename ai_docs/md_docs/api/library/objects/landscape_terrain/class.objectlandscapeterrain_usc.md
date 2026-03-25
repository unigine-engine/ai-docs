# Unigine.ObjectLandscapeTerrain Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


This class is used to create and manage [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) object and its detail masks.


### See also


- C++ sample


## ObjectLandscapeTerrain Class

### Members

---

## ObjectLandscapeTerrain ( )

The ObjectLandscapeTerrain constructor.
## void setActiveTerrain ( int enabled )

Sets a value indicating if the landscape terrain is active.
### Arguments

- *int* **enabled** - **1** to set the landscape terrain as active, **0** - to set it as inactive.

## int isActiveTerrain ( )

Returns a value indicating if the landscape terrain is active.
### Return value

**1** if the landscape terrain is active; otherwise, **0**.
## void setIntersectionPrecision ( float begin )

Sets a new precision value to be used for intersection detection.
### Arguments

- *float* **begin** - Precision for intersection detection as a fraction of maximum precision in the [0; 1] range. The default value is 0.5f. Maximum precision is determined by the Engine on the basis of the data of your Landscape Terrain.

## float getIntersectionPrecision ( )

Returns the current precision value used for intersection detection.
### Return value

Precision for intersection detection as a fraction of maximum precision in the [0; 1] range. The default value is 0.5f. Maximum precision is determined by the Engine on the basis of the data of your Landscape Terrain.
## int getNumDetailMasks ( )

Returns the total number of detail masks of the landscape terrain.
### Return value

Total number of detail masks of the landscape terrain.
## TerrainDetailMask getDetailMask ( int num )

Returns the detail mask by its index. The number of detail masks is fixed and is equal to 20.
### Arguments

- *int* **num** - Detail mask index in the **[0; 19]** range.

### Return value

Detail mask having the specified index.
## TerrainDetailMask getDetailMaskSortRender ( int num )

Returns the detail mask by its rendering order. The number of detail masks is fixed and is equal to 20, masks rendering order is back to front.
### Arguments

- *int* **num** - Detail mask rendering order, in the **[0; 19]** range.

### Return value

Detail mask having the specified rendering order.
## TerrainDetailMask findDetailMask ( string name )

Returns a child detail's number by its name. The search is performed among the immediate children only.
### Arguments

- *string* **name** - Detail mask name.

### Return value

Detail mask having the specified name (if it exists); otherwise, nullptr.
## void getDetailMasks ( )

Builds the list of all detail masks of the landscape terrain and puts them to the specified buffer. The number of detail masks is fixed and is equal to 20.
### Arguments

## void getDetailMasksSortRender ( )

Builds the list of all detail masks of the landscape terrain according to their rendering order (back to front) and puts them to the specified buffer. The number of detail masks is fixed and is equal to 20.
### Arguments

## long getLastStreamingFrame ( )

Returns the number of the frame when the last commit to the *Virtual Texture* was performed. This method enables you to check if the *Landscape Terrain* data is loaded completely at the moment (the *Virtual Texture* is created and the last commit to it is already applied).
```cpp
#include "AppWorldLogic.h"
#include <UnigineWorld.h>
#include <UnigineGame.h>

using namespace Unigine;
ObjectLandscapeTerrainPtr terrain;

int AppWorldLogic::init()
{
	terrain = checked_ptr_cast<ObjectLandscapeTerrain>(World::getNodeByName("ObjectLandscapeTerrain"));

	return 1;
}

int AppWorldLogic::update()
{
	if (!terrain.isValid())
		return 1;
	int64_t last_commit_frame = terrain->getLastStreamingFrame();
	if (last_commit_frame == -1)
	{
		Log::message("The Virtual Texture is not created yet\n");
		return 1;
		// not ready
	}
	if ((Game::getFrame() - last_commit_frame) > 45)
	{
		Log::message("Virtual Texture update is completed (all commits are applied)\n");
		// ...
	}
	else
	{
		Log::message("Virtual Texture update is pending (commit_frame = %d)\n", last_commit_frame);
		// ...
	}
	return 1;
}


```


### Return value

Number of the last streaming frame.
## static int type ( )

Returns the type of the node.
### Return value

[ObjectLandscapeTerrain](../../../../api/library/nodes/class.node_usc.md#OBJECT_LANDSCAPE_TERRAIN) type identifier.
## int getVideoMemoryUsage ( )

## int getDetailVideoMemoryUsage ( )

## int getNumReloadTiles ( )

## int getNumReloadBounds ( )

## int isReloading ( )

## int isReloading ( WorldBoundBox bb )

### Arguments

- *WorldBoundBox* **bb**
