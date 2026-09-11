# Unigine.LandscapeLayerMap Class (CS)

**Inherits from:** Node


This class is used to manage landscape [layer maps](../../../../objects/objects/terrain/landscape_terrain/landscape_layer_map.md) of the [Landscape Terrain object](../../../../objects/objects/terrain/landscape_terrain/index.md). Landscape layer map data (height, albedo, masks, settings) is stored in a `.lmap` file (see the [LandscapeMapFileCreator](../../../../api/library/objects/landscape_terrain/class.landscapemapfilecreator_cs.md) and [LandscapeMapFileSettings](../../../../api/library/objects/landscape_terrain/class.landscapemapfilesettings_cs.md) classes). A landscape map has a single resolution and density, and cannot have insets. Insets are created by adding a high-resolution landscape layer map above the low-resolution one.


![](../../../../objects/objects/terrain/landscape_terrain/landscape_layers.png)


Several maps can be blended with each other. Blending parameters for the landscape layer map are controlled via the corresponding methods of the [*LandscapeMapFilesettings*](../../../../api/library/objects/landscape_terrain/class.landscapemapfilesettings_cs.md) class.


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

### Properties

## string Path

The path to the `*.lmap` file containing landscape map data.
## bool Collision

The value indicating if collision detection is enabled for the landscape layer map.
## bool Intersection

The value indicating if intersection detection is enabled for the landscape layer map.
## bool IntersectionBicubicFilter

The value indicating if bicubic filtering is enabled for height texture (collision and intersection detection and fetch requests) and normals texture (intersection detection and fetch requests).
## bool Culling

The value indicating if heights data of the layer map is to be used for culling precalculation. In order to define which parts of the terrain are to be rendered a culling test is required. This test is performed on the basis of a precalculated low-detail height map, combining heights data of all landscape layer maps having a significant impact on the result. Precalculation is performed on the CPU side, so processing a large number of landscape layer maps may reduce performance. Moreover, some layer maps may be used as decals (i.e. their impact on the resulting height map is insignificant). For such cases you can simply disable this option to avoid unnecessary calculations.
## int Order

The rendering order for the landscape layer map. A map with a higher order value shall be rendered above the ones with lower ones.
## vec2 Size

The two-component vector **(X, Y)** defining the size of the landscape layer map along X and Y axes, in units.
## float HeightScale

The scale factor used for heights data. Height values of the landscape layer map are multiplied by this value during terrain rendering.
## 🔒︎ vec2 TexelSize

The two-component vector **(X, Y)** defining the size of the texel of the landscape layer map textures along X and Y axes.
## 🔒︎ bool IsInit

The value indicating if the landscape layer map is initialized.
## 🔒︎ ivec2 Resolution

The two-component vector (X, Y) representing landscape map resolution along X and Y axes, in pixels.
## vec2 FadeAttenuation

The two-component vector **(X, Y)** defining the fade attenuation of the landscape layer map along X and Y axes.
## 🔒︎ bool IsCompressed

The value indicating if the landscape layer map is compressed.
## 🔒︎ vec2 AlbedoFadeAttenuation

The two-component vector (X, Y) defining the fade attenuation of the albedo data along the X and Y axes.
## 🔒︎ vec2 HeightFadeAttenuation

The two-component vector (X, Y) defining the fade attenuation of the height data along the X and Y axes.
## 🔒︎ Landscape.BLENDING_MODE AlbedoBlending

The blending mode for the albedo data. One of the *[Landscape.BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#BLENDING_MODE)* values
## 🔒︎ Landscape.BLENDING_MODE HeightBlending

The blending mode for the height data. One of the *[Landscape.BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#BLENDING_MODE)* values
## 🔒︎ bool IsEnabledOpacityAlbedo

The value indicating if albedo data with an additional opacity mask applied is enabled for the landscape layer map.
## 🔒︎ bool IsEnabledOpacityHeight

The value indicating if heightmap with an additional opacity mask applied is enabled for the landscape layer map.
## 🔒︎ bool IsEnabledAlbedo

The value indicating if albedo data is enabled for the landscape layer map.
## 🔒︎ bool IsEnabledHeight

The value indicating if heightmap data is enabled for the landscape layer map.
### Members

---

## LandscapeLayerMap ( )

The LandscapeLayerMap constructor.
## UGUID GetGUID ( )

Returns the [GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the LandscapeLayerMap node.
### Return value

[GUID](../../../../api/library/filesystem/class.uguid_cs.md) of the LandscapeLayerMap node.
## vec2 GetExtremumHeight ( float precision = 1.0f )

Returns the minimum and maximum height of the landscape layer map as a two-component vector.
### Arguments

- *float* **precision** - Precision value in the **[0.0f, 1.0f]** range. The default value is 1.0f (maximum).

### Return value

The two-component vector **(X, Y)** defining the minimum (**X**) and maximum (**Y**) height of the landscape layer map.
## static int type ( )

Returns the type of the node.
### Return value

[LandscapeLayerMap](../../../../api/library/nodes/class.node_cs.md#LANDSCAPE_LAYER_MAP) type identifier.
## bool IsEnabledMask ( int mask )

Returns the value specifying if the specified mask is enabled for the landscape layer map.
### Arguments

- *int* **mask** - Mask index.

### Return value

true if the specified mask is enabled for the landscape layer map; otherwise, false.
## bool IsEnabledOpacityMask ( int mask )

Returns the value specifying if the specified mask with an additional opacity mask applied is enabled for the landscape layer map.
### Arguments

- *int* **mask** - Mask index.

### Return value

true if heightmap with an opacity mask is enabled for the landscape layer map; otherwise, false.
## Landscape.BLENDING_MODE GetMaskBlending ( int mask )

Returns the blending mode set for the mask data.
### Arguments

- *int* **mask** - Mask index.

### Return value

The blending mode, one of the *[Landscape.BLENDING_MODE](../../../../api/library/objects/landscape_terrain/class.landscape_cs.md#BLENDING_MODE)* values.
## vec2 GetMaskFadeAttenuation ( int mask )

Returns the current fade attenuation for the data of the specified detail mask. This parameter defines the distance of the transparency attenuation starting from the edge of the map.
### Arguments

- *int* **mask** - Mask index.

### Return value

The two-component vector **(X, Y)** defining the fade attenuation of the detail mask data along X and Y axes.
