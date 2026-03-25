# Unigine.LandscapeLayerMap Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Node


This class is used to manage landscape [layer maps](../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md) of the [Landscape Terrain object](../../../../objects/objects/terrain/landscape_terrain/index.md). Landscape layer map data (height, albedo, masks, settings) is stored in a `.lmap` file (see the [LandscapeMapFileCreator](../../../../api/library/objects/landscape_terrain/class.landscapemapfilecreator_usc.md) and [LandscapeMapFileSettings](../../../../api/library/objects/landscape_terrain/class.landscapemapfilesettings_usc.md) classes). A landscape map has a single resolution and density, and cannot have insets. Insets are created by adding a high-resolution landscape layer map above the low-resolution one.


![](../../../../objects/objects/terrain/landscape_terrain/landscape_layers.png)


Several maps can be blended with each other. Blending parameters for the landscape layer map are controlled via the corresponding methods of the [*LandscapeMapFilesettings*](../../../../api/library/objects/landscape_terrain/class.landscapemapfilesettings_usc.md) class.


### Maximum and Minimum Terrain Height


This example demonstrates how to obtain minimum and maximum height values for the whole [Landscape Terrain](../../../../objects/objects/terrain/landscape_terrain/index.md) (all layer maps) along with the enclosing bounding box. For this puprose we should find all *LandscapeLayerMap* objects in the World, extend a bounding box to enclose all of them, and use the [*getExtremumHeight()*](#getExtremumHeight_float_Vec2) method to get minimum and maximum height values.


```cpp
WorldBoundBox b;
float min = 99999, max = -9999;
Vector<NodePtr> v;
World::getNodes(v);
for (auto & it : v)
{
	if (it->getType() == Node::LANDSCAPE_LAYER_MAP)
	{
		b.expand(it->getWorldBoundBox());
		auto ext = checked_ptr_cast<LandscapeLayerMap>(it)->getExtremumHeight();
		if (ext.x < min)
			min = ext.x;
		if (ext.y > max)
			max = ext.y;
	}
}
vec3 minp = vec3(b.getMin());
vec3 maxp = vec3(b.getMax());
minp.z = min;
maxp.z = max;
BoundBox bb = BoundBox(minp, maxp);
Visualizer::renderBoundBox(bb, Mat4_identity, vec4_red);

```


## LandscapeLayerMap Class

### Members

---

## static LandscapeLayerMap ( )

The LandscapeLayerMap constructor.
## void setPath ( string path )

Sets a new path to the `*.lmap` file containing landscape map data.
### Arguments

- *string* **path** - New path to the `*.lmap` file with landscape map data.

## string getPath ( )

Returns the current path to the `*.lmap` file containing landscape map data.
### Return value

Path to the `*.lmap` file containing landscape map data.
## UGUID getGUID ( )

Returns the [GUID](../../../../api/library/filesystem/class.uguid_usc.md) of the LandscapeLayerMap node.
### Return value

[GUID](../../../../api/library/filesystem/class.uguid_usc.md) of the LandscapeLayerMap node.
## void setIntersection ( int intersection )

Sets a value indicating if intersection detection is enabled for the landscape layer map.
### Arguments

- *int* **intersection** - **1** to enable intersection detection for the landscape layer map, **0** - to disable it.

## int isIntersection ( )

Returns a value indicating if intersection detection is enabled for the landscape layer map.
### Return value

**1** if intersection detection for the landscape layer map is enabled; otherwise, **0**.
## void setIntersectionBicubicFilter ( int filter )

Sets a value indicating if bicubic filtering is enabled for height texture (collision and intersection detection and fetch requests) and normals texture (intersection detection and fetch requests).
### Arguments

- *int* **filter** - **1** to enable bicubic filtering is enabled for height texture (collision and intersection detection and fetch requests) and normals texture (intersection detection and fetch requests), **0** - to disable it.

## int isIntersectionBicubicFilter ( )

Returns a value indicating if bicubic filtering is enabled for height texture (collision and intersection detection and fetch requests) and normals texture (intersection detection and fetch requests).
### Return value

**1** if bicubic filtering is enabled for height texture (collision and intersection detection and fetch requests) and normals texture (intersection detection and fetch requests); otherwise, **0**.
## void setCollision ( int collision )

Sets a value indicating if collision detection is enabled for the landscape layer map.
### Arguments

- *int* **collision** - **1** to enable collision detection for the landscape layer map, **0** - to disable it.

## int isCollision ( )

Returns a value indicating if collision detection is enabled for the landscape layer map.
### Return value

**1** if collision detection for the landscape layer map is enabled; otherwise, **0**.
## void setCulling ( int culling )

Sets a value indicating if heights data of the layer map is to be used for culling precalculation. In order to define which parts of the terrain are to be rendered a culling test is required. This test is performed on the basis of a precalculated low-detail height map, combining heights data of all landscape layer maps having a significant impact on the result.  Precalculation is performed on the CPU side, so processing a large number of landscape layer maps may reduce performance.  Moreover, some layer maps may be used as decals (i.e. their impact on the resulting height map is insignificant).  For such cases you can simply disable this option to avoid unnecessary calculations.
> **Notice:** Disabling this option for a single


### Arguments

- *int* **culling** - **1** to use the layer map for culling, **0** - to ignore it.

## int isCulling ( )

Returns a value indicating if heights data of the layer map is to be used for culling precalculation. In order to define which parts of the terrain are to be rendered a culling test is required. This test is performed on the basis of a precalculated low-detail height map, combining heights data of all landscape layer maps having a significant impact on the result. Precalculation is performed on the CPU side, so processing a large number of landscape layer maps may reduce performance. Moreover, some layer maps may be used as decals (i.e. their impact on the resulting height map is insignificant). For such cases you can simply disable this option to avoid unnecessary calculations.
### Return value

**1** if heights data of the layer map is to be used for culling precalculation; otherwise, **0**.
## void setOrder ( int order )

Returns a new rendering order for the landscape layer map. A map with a higher order value shall be rendered above the ones with lower ones.
### Arguments

- *int* **order** - New rendering order to be set for the landscape layer map.

## int getOrder ( )

Sets the current rendering order for the landscape layer map. A map with a higher order value shall be rendered above the ones with lower ones.
### Return value

Current rendering order of the landscape layer map.
## void setSize ( Vec2 size )

Sets a new size for the landscape layer map.
### Arguments

- *Vec2* **size** - The two-component vector **(X, Y)** defining the size of the landscape layer map along X and Y axes, in units.

## Vec2 getSize ( )

Returns the current size of the landscape layer map.
### Return value

The two-component vector **(X, Y)** defining the size of the landscape layer map along X and Y axes, in units.
## void setHeightScale ( float scale )

Sets a new scale factor to be used for heights data. Height values of landscape layer map are multiplied by this value during terrain rendering.
### Arguments

- *float* **scale** - The scale factor used for heights data.

## float getHeightScale ( )

Returns the current scale factor used for heights data. Height values of landscape layer map are multiplied by this value during terrain rendering.
### Return value

The scale factor used for heights data.
## Vec2 getTexelSize ( )

Returns the current texel size for the landscape layer map textures.
### Return value

The two-component vector **(X, Y)** defining the size of the texel of the landscape layer map textures along X and Y axes.
## int isInit ( )

Returns a value indicating if the landscape layer map is initialized.
### Return value

**1** if the landscape layer map is initialized; otherwise, **0**.
## getExtremumHeight ( float precision = 1.0f )

Returns the minimum and maximum height of the landscape layer map as a two-component vector.
### Arguments

- *float* **precision** - Precision value in the **[0.0f, 1.0f]** range. The default value is 1.0f (maximum).

### Return value

The two-component vector **(X, Y)** defining the minimum (**X**) and maximum (**Y**) height of the landscape layer map.
## static int type ( )

Returns the type of the node.
### Return value

[LandscapeLayerMap](../../../../api/library/nodes/class.node_usc.md#LANDSCAPE_LAYER_MAP) type identifier.
## ivec2 getResolution ( )

Returns the current landscape map resolution.
### Return value

The two-component vector (X, Y) representing landscape map resolution along X and Y axes, in pixels.
## void setFadeAttenuation ( vec2 attenuation )

Sets a new fade attenuation of landscape layer map. This parameter defines the distance of the map transparency attenuation, starting from the edge of the map.
### Arguments

- *vec2* **attenuation** - The two-component vector **(X, Y)** defining the fade attenuation of the landscape layer map along X and Y axes.

## vec2 getFadeAttenuation ( )

Returns the current fade attenuation for the landscape layer map. This parameter defines the distance of the map transparency attenuation, starting from the edge of the map.
### Return value

The two-component vector **(X, Y)** defining the fade attenuation of the landscape layer map along X and Y axes.
## int isEnabledHeight ( )

Returns the value specifying if heightmap data is enabled for the landscape layer map.
### Return value

**1** if heightmap data is enabled for the landscape layer map; otherwise, **0**.
## int isEnabledAlbedo ( )

Returns the value specifying if albedo data is enabled for the landscape layer map.
### Return value

**1** if albedo data is enabled for the landscape layer map; otherwise, **0**.
## int isEnabledMask ( int mask )

Returns the value specifying if the specified mask is enabled for the landscape layer map.
### Arguments

- *int* **mask** - Mask index.

### Return value

**1** if the specified mask is enabled for the landscape layer map; otherwise, **0**.
## int isEnabledOpacityHeight ( )

Returns the value specifying if heightmap with an additional opacity mask applied is enabled for the landscape layer map.
### Return value

**1** if heightmap with an opacity mask is enabled for the landscape layer map; otherwise, **0**.
## int isEnabledOpacityAlbedo ( )

Returns the value specifying if albedo data with an additional opacity mask applied is enabled for the landscape layer map.
### Return value

**1** if heightmap with an opacity mask is enabled for the landscape layer map; otherwise, **0**.
## int isEnabledOpacityMask ( int mask )

Returns the value specifying if the specified mask with an additional opacity mask applied is enabled for the landscape layer map.
### Arguments

- *int* **mask** - Mask index.

### Return value

**1** if heightmap with an opacity mask is enabled for the landscape layer map; otherwise, **0**.
## int getHeightBlending ( )

Returns the blending mode set for the height data.
### Return value

The blending mode, one of the *[LANDSCAPE_BLENDING_MODE()](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#BLENDING_MODE)* values.
## int getAlbedoBlending ( )

Returns the blending mode set for the albedo data.
### Return value

The blending mode, one of the *[LANDSCAPE_BLENDING_MODE()](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#BLENDING_MODE)* values.
## int getMaskBlending ( int mask )

Returns the blending mode set for the mask data.
### Arguments

- *int* **mask** - Mask index.

### Return value

The blending mode, one of the *[LANDSCAPE_BLENDING_MODE()](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#BLENDING_MODE)* values.
## vec2 getHeightFadeAttenuation ( )

Returns the current fade attenuation for height data of the landscape map. This parameter defines the distance of the transparency attenuation starting from the edge of the map.
### Return value

The two-component vector **(X, Y)** defining the fade attenuation of the height data along X and Y axes.
## vec2 getAlbedoFadeAttenuation ( )

Returns the current fade attenuation for albedo data of the landscape map. This parameter defines the distance of the transparency attenuation starting from the edge of the map.
### Return value

The two-component vector **(X, Y)** defining the fade attenuation of the albedo data along X and Y axes.
## vec2 getMaskFadeAttenuation ( int mask )

Returns the current fade attenuation for the data of the specified detail mask. This parameter defines the distance of the transparency attenuation starting from the edge of the map.
### Arguments

- *int* **mask** - Mask index.

### Return value

The two-component vector **(X, Y)** defining the fade attenuation of the detail mask data along X and Y axes.
## int isCompressed ( )

Returns the value indicating if the landscape layer map is compressed.
### Return value

**1** if the landscape layer map is compressed; otherwise, **0**.
