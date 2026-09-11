# Unigine.ObjectLandscapeTerrain Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


This class is used to create and manage [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) object and its detail masks.


### See also


- C++ sample


## ObjectLandscapeTerrain Class

### Members

## void setIntersectionPrecision ( float precision )

Sets a new precision for intersection detection as a fraction of maximum precision in the [0; 1] range. The default value is 0.5f. Maximum precision is determined by the Engine on the basis of the data of your Landscape Terrain.
### Arguments

- *float* **precision** - The precision for intersection detection as a fraction of maximum precision in the [0; 1] range

## float getIntersectionPrecision () const

Returns the current precision for intersection detection as a fraction of maximum precision in the [0; 1] range. The default value is 0.5f. Maximum precision is determined by the Engine on the basis of the data of your Landscape Terrain.
### Return value

Current precision for intersection detection as a fraction of maximum precision in the [0; 1] range
## int getNumDetailMasks () const

Returns the current total number of detail masks of the landscape terrain.
### Return value

Current total number of detail masks of the landscape terrain
## void setActiveTerrain ( int terrain )

Sets a new value indicating if the landscape terrain is active.
### Arguments

- *int* **terrain** - The value indicating if the landscape terrain is active

## int isActiveTerrain () const

Returns the current value indicating if the landscape terrain is active.
### Return value

Current value indicating if the landscape terrain is active
## long getLastStreamingFrame () const

Returns the current number of the frame when the last commit to the *Virtual Texture* was performed. This method enables you to check if the *Landscape Terrain* data is loaded completely at the moment (the *Virtual Texture* is created and the last commit to it is already applied).
```csharp
ObjectLandscapeTerrain terrain;

void Init()
{
	terrain = World.GetNodeByName("ObjectLandscapeTerrain") as ObjectLandscapeTerrain;
}

void Update()
{
	if (!terrain)
		return;
	long last_commit_frame = terrain.LastStreamingFrame;
	if (last_commit_frame == -1)
	{
		Log.Message("The Virtual Texture is not created yet\n");
		return;
		// not ready
	}
	if ((Game.Frame - last_commit_frame) > 45)
	{
		Log.Message("Virtual Texture update is completed (all commits are applied)\n");
		// ...
	}
	else
	{
		Log.Message("Virtual Texture update is pending (commit_frame = %d)\n", last_commit_frame);
		// ...
	}

}


```

### Return value

Current number of the frame when the last commit to the Virtual Texture was performed
---

## ObjectLandscapeTerrain ( )

The ObjectLandscapeTerrain constructor.
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

Returns a detail mask by its name. The search is performed among the immediate children only.
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
