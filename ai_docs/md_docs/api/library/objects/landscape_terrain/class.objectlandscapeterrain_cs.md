# Unigine.ObjectLandscapeTerrain Class (CS)

**Inherits from:** Object


This class is used to create and manage [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) object and its detail masks.


### See also


- C++ sample


## ObjectLandscapeTerrain Class

### Properties

## float IntersectionPrecision

The precision for intersection detection as a fraction of maximum precision in the [0; 1] range. The default value is 0.5f. Maximum precision is determined by the Engine on the basis of the data of your Landscape Terrain.
## 🔒︎ int NumDetailMasks

The total number of detail masks of the landscape terrain.
## bool ActiveTerrain

The value indicating if the landscape terrain is active.
## 🔒︎ long LastStreamingFrame

The number of the frame when the last commit to the *Virtual Texture* was performed. This method enables you to check if the *Landscape Terrain* data is loaded completely at the moment (the *Virtual Texture* is created and the last commit to it is already applied).
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

### Members

---

## ObjectLandscapeTerrain ( )

The ObjectLandscapeTerrain constructor.
## TerrainDetailMask GetDetailMask ( int num )

Returns the detail mask by its index. The number of detail masks is fixed and is equal to 20.
### Arguments

- *int* **num** - Detail mask index in the **[0; 19]** range.

### Return value

Detail mask having the specified index.
## TerrainDetailMask GetDetailMaskSortRender ( int num )

Returns the detail mask by its rendering order. The number of detail masks is fixed and is equal to 20, masks rendering order is back to front.
### Arguments

- *int* **num** - Detail mask rendering order, in the **[0; 19]** range.

### Return value

Detail mask having the specified rendering order.
## TerrainDetailMask FindDetailMask ( string name )

Returns a detail mask by its name. The search is performed among the immediate children only.
### Arguments

- *string* **name** - Detail mask name.

### Return value

Detail mask having the specified name (if it exists); otherwise, nullptr.
## void GetDetailMasks ( TerrainDetailMask [] masks )

Builds the list of all detail masks of the landscape terrain and puts them to the specified buffer. The number of detail masks is fixed and is equal to 20.
### Arguments

- *[TerrainDetailMask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cs.md)[]* **masks** - Buffer to which the list of detail masks it to be put.

## void GetDetailMasksSortRender ( TerrainDetailMask [] masks )

Builds the list of all detail masks of the landscape terrain according to their rendering order (back to front) and puts them to the specified buffer. The number of detail masks is fixed and is equal to 20.
### Arguments

- *[TerrainDetailMask](../../../../api/library/objects/landscape_terrain/class.terraindetailmask_cs.md)[]* **masks** - Buffer to which the list of detail masks it to be put.

## static int type ( )

Returns the type of the node.
### Return value

[ObjectLandscapeTerrain](../../../../api/library/nodes/class.node_cs.md#OBJECT_LANDSCAPE_TERRAIN) type identifier.
## ulong GetVideoMemoryUsage ( )

## ulong GetDetailVideoMemoryUsage ( )

## int GetNumReloadTiles ( )

## int GetNumReloadBounds ( )

## bool IsReloading ( )

## bool IsReloading ( WorldBoundBox bb )

### Arguments

- *[WorldBoundBox](../../../../api/library/math/cs/bounds/worldboundbox_cs.md)* **bb**
