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

## void setPath ( string path )

Sets a new path to the `*.lmap` file containing landscape map data.
### Arguments

- *string* **path** - The path to the *.lmap file containing landscape map data

## const char * getPath () const

Returns the current path to the `*.lmap` file containing landscape map data.
### Return value

Current path to the *.lmap file containing landscape map data
## void setCollision ( int collision )

Sets a new value indicating if collision detection is enabled for the landscape layer map.
### Arguments

- *int* **collision** - The value indicating if collision detection is enabled for the landscape layer map

## int isCollision () const

Returns the current value indicating if collision detection is enabled for the landscape layer map.
### Return value

Current value indicating if collision detection is enabled for the landscape layer map
## void setIntersection ( int intersection )

Sets a new value indicating if intersection detection is enabled for the landscape layer map.
### Arguments

- *int* **intersection** - The value indicating if intersection detection is enabled for the landscape layer map

## int isIntersection () const

Returns the current value indicating if intersection detection is enabled for the landscape layer map.
### Return value

Current value indicating if intersection detection is enabled for the landscape layer map
## void setIntersectionBicubicFilter ( int filter )

Sets a new value indicating if bicubic filtering is enabled for height texture (collision and intersection detection and fetch requests) and normals texture (intersection detection and fetch requests).
### Arguments

- *int* **filter** - The value indicating if bicubic filtering is enabled for height texture (collision and intersection detection and fetch requests) and normals texture (intersection detection and fetch requests)

## int isIntersectionBicubicFilter () const

Returns the current value indicating if bicubic filtering is enabled for height texture (collision and intersection detection and fetch requests) and normals texture (intersection detection and fetch requests).
### Return value

Current value indicating if bicubic filtering is enabled for height texture (collision and intersection detection and fetch requests) and normals texture (intersection detection and fetch requests)
## void setCulling ( int culling )

Sets a new value indicating if heights data of the layer map is to be used for culling precalculation. In order to define which parts of the terrain are to be rendered a culling test is required. This test is performed on the basis of a precalculated low-detail height map, combining heights data of all landscape layer maps having a significant impact on the result. Precalculation is performed on the CPU side, so processing a large number of landscape layer maps may reduce performance. Moreover, some layer maps may be used as decals (i.e. their impact on the resulting height map is insignificant). For such cases you can simply disable this option to avoid unnecessary calculations.
### Arguments

- *int* **culling** - The value indicating if heights data of the layer map is to be used for culling precalculation

## int isCulling () const

Returns the current value indicating if heights data of the layer map is to be used for culling precalculation. In order to define which parts of the terrain are to be rendered a culling test is required. This test is performed on the basis of a precalculated low-detail height map, combining heights data of all landscape layer maps having a significant impact on the result. Precalculation is performed on the CPU side, so processing a large number of landscape layer maps may reduce performance. Moreover, some layer maps may be used as decals (i.e. their impact on the resulting height map is insignificant). For such cases you can simply disable this option to avoid unnecessary calculations.
### Return value

Current value indicating if heights data of the layer map is to be used for culling precalculation
## void setOrder ( int order )

Sets a new rendering order for the landscape layer map. A map with a higher order value shall be rendered above the ones with lower ones.
### Arguments

- *int* **order** - The rendering order for the landscape layer map

## int getOrder () const

Returns the current rendering order for the landscape layer map. A map with a higher order value shall be rendered above the ones with lower ones.
### Return value

Current rendering order for the landscape layer map
## void setSize ( Vec2 size )

Sets a new two-component vector **(X, Y)** defining the size of the landscape layer map along X and Y axes, in units.
### Arguments

- *Vec2* **size** - The two-component vector

## Vec2 getSize () const

Returns the current two-component vector **(X, Y)** defining the size of the landscape layer map along X and Y axes, in units.
### Return value

Current two-component vector
## void setHeightScale ( float scale )

Sets a new scale factor used for heights data. Height values of the landscape layer map are multiplied by this value during terrain rendering.
### Arguments

- *float* **scale** - The scale factor used for heights data

## float getHeightScale () const

Returns the current scale factor used for heights data. Height values of the landscape layer map are multiplied by this value during terrain rendering.
### Return value

Current scale factor used for heights data
## Vec2 getTexelSize () const

Returns the current two-component vector **(X, Y)** defining the size of the texel of the landscape layer map textures along X and Y axes.
### Return value

Current two-component vector
## int isInit () const

Returns the current value indicating if the landscape layer map is initialized.
### Return value

Current the landscape layer map is initialized
## ivec2 getResolution () const

Returns the current two-component vector (X, Y) representing landscape map resolution along X and Y axes, in pixels.
### Return value

Current two-component vector (X, Y) representing landscape map resolution along X and Y axes, in pixels
## void setFadeAttenuation ( vec2 attenuation )

Sets a new two-component vector **(X, Y)** defining the fade attenuation of the landscape layer map along X and Y axes.
### Arguments

- *vec2* **attenuation** - The two-component vector

## vec2 getFadeAttenuation () const

Returns the current two-component vector **(X, Y)** defining the fade attenuation of the landscape layer map along X and Y axes.
### Return value

Current two-component vector
## int isCompressed () const

Returns the current value indicating if the landscape layer map is compressed.
### Return value

Current the landscape layer map is compressed
## vec2 getAlbedoFadeAttenuation () const

Returns the current two-component vector (X, Y) defining the fade attenuation of the albedo data along the X and Y axes.
### Return value

Current fade attenuation of the albedo data along the X and Y axes, as a two-component vector (X, Y)
## vec2 getHeightFadeAttenuation () const

Returns the current two-component vector (X, Y) defining the fade attenuation of the height data along the X and Y axes.
### Return value

Current fade attenuation of the height data along the X and Y axes, as a two-component vector (X, Y)
## int getAlbedoBlending () const

Returns the current blending mode for the albedo data. One of the *[LANDSCAPE_BLENDING_MODE()](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#BLENDING_MODE)* values
### Return value

Current blending mode for the albedo data
## int getHeightBlending () const

Returns the current blending mode for the height data. One of the *[LANDSCAPE_BLENDING_MODE()](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#BLENDING_MODE)* values
### Return value

Current blending mode for the height data
## int isEnabledOpacityAlbedo () const

Returns the current value indicating if albedo data with an additional opacity mask applied is enabled for the landscape layer map.
### Return value

Current albedo data with an additional opacity mask applied is enabled for the landscape layer map
## int isEnabledOpacityHeight () const

Returns the current value indicating if heightmap with an additional opacity mask applied is enabled for the landscape layer map.
### Return value

Current heightmap with an additional opacity mask applied is enabled for the landscape layer map
## int isEnabledAlbedo () const

Returns the current value indicating if albedo data is enabled for the landscape layer map.
### Return value

Current albedo data is enabled for the landscape layer map
## int isEnabledHeight () const

Returns the current value indicating if heightmap data is enabled for the landscape layer map.
### Return value

Current heightmap data is enabled for the landscape layer map
---

## static LandscapeLayerMap ( )

The LandscapeLayerMap constructor.
## UGUID getGUID ( )

Returns the [GUID](../../../../api/library/filesystem/class.uguid_usc.md) of the LandscapeLayerMap node.
### Return value

[GUID](../../../../api/library/filesystem/class.uguid_usc.md) of the LandscapeLayerMap node.
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
## int isEnabledMask ( int mask )

Returns the value specifying if the specified mask is enabled for the landscape layer map.
### Arguments

- *int* **mask** - Mask index.

### Return value

**1** if the specified mask is enabled for the landscape layer map; otherwise, **0**.
## int isEnabledOpacityMask ( int mask )

Returns the value specifying if the specified mask with an additional opacity mask applied is enabled for the landscape layer map.
### Arguments

- *int* **mask** - Mask index.

### Return value

**1** if heightmap with an opacity mask is enabled for the landscape layer map; otherwise, **0**.
## int getMaskBlending ( int mask )

Returns the blending mode set for the mask data.
### Arguments

- *int* **mask** - Mask index.

### Return value

The blending mode, one of the *[LANDSCAPE_BLENDING_MODE()](../../../../api/library/objects/landscape_terrain/class.landscape_usc.md#BLENDING_MODE)* values.
## vec2 getMaskFadeAttenuation ( int mask )

Returns the current fade attenuation for the data of the specified detail mask. This parameter defines the distance of the transparency attenuation starting from the edge of the map.
### Arguments

- *int* **mask** - Mask index.

### Return value

The two-component vector **(X, Y)** defining the fade attenuation of the detail mask data along X and Y axes.
