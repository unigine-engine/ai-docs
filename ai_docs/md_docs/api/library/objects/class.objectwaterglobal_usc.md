# ObjectWaterGlobal Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


Interface for **[Global Water](../../../objects/objects/water/water_object.md)** object handling. This water object represents infinitely spread water with auto-tessellation (the wireframe of the water object is not scaled — regardless of the camera position it stays the same) and the underwater mode. This type is suitable to represent boundless ocean while not overloading the GPU.


However, it cannot have a body assigned, and thus does not provide proper physical interaction with scene objects. If you need to simulate the physics of buoyancy, you should use **[Physical Water](../../../objects/effects/physicals/physical_water/index.md)**. Also it is limited to a single water level. It means that the filling level of water always remains the same. So, if you need to create, for example, mountain lakes or water flows with height difference, you should use a **[Water Mesh](../../../objects/objects/water/water_mesh.md)**.


There are three options for creating waves:


- **Layer mode** — you create layers on which waves will be randomly generated in a given range of wave parameters. All the layers are added together. > **Notice:** Wave layers are usually created through the UnigineEditor, but you can also create and edit them via code.
- **Manual mode** — you create your own individual waves and have full control over them. This mode can only be set via code, you cannot do this in the UnigineEditor. > **Notice:** In **Manual mode**, be careful with the *Steepness* parameter, the waves will be everted if this value is set high.
- **Beauforts mode** — waves are generated based on the presets reproducing the state of the sea according to the Beaufort wind force scale (0 - Calm, 12 - Hurricane). In this mode, the parameters that define the main wave geometry will not be available for editing via code.


For all modes, wave frequency is calculated based on the wavelength using the formula:

 sqrt (*Gravity* * 2 * PI / *Wavelength*)
 where *Gravity* = 9.81 m/s2.
When you enable **Manual mode**, the list of the generated waves is cleared and you can set up your own waves.


When you save the world, the layers will be saved, but the user-defined waves will not, since they are created via code.


The maximum total number of waves is **256**. For better performance, we recommend using about **100**.


The following *WorldScript* file shows how to create waves in **Manual mode**.


<details>
<summary>WorldScript | Close</summary>

`WorldScript`


```cpp
#include <core/unigine.h>
// This file is in UnigineScript language.
// World script, it takes effect only when the world is loaded.

ObjectWaterGlobal water = NULL;

int init() {
	// Write here code to be called on world initialization: initialize resources for your world scene during the world start.

		// Changing preset to custom (4) and adjusting tesselation parameters
		engine.render.setWaterGeometryPreset(4);
		engine.render.setWaterGeometryPolygonSize(0.01f);
		engine.render.setWaterGeometryProgression(1.0f);
		engine.render.setWaterGeometrySubpixelReduction(6.0f);

		water = node_cast(engine.world.getNodeByType(Node::OBJECT_WATER_GLOBAL));
		if (!water)
		{
			water = ObjectWaterGlobal();
		}

		// You can set each wave only in Manual mode
		water.setWavesMode(ObjectWaterGlobal.WAVES_MODE.MANUAL);

		// Adding waves.
		// addWave(wave length, amplitude, steepness, direction angle[0.0; 360.0], phase offset[0.0; 2*PI])

		water.addWave(8.0f, 0.05f, 2.0f, 270.0f, 0.0f);
		water.addWave(8.0f, 0.015f, 1.0f, 150.0f, 1.0f);
		water.addWave(8.0f, 0.02f, 6.0f, 75.0f, 0.0f);
		water.addWave(16.0f, 0.05f, 2.0f, 270.0f, 3.0f);
		water.addWave(16.0f, 0.05f, 7.0f, 45.0f, 0.5f);
		water.addWave(32.0f, 0.1f, 2.0f, 120.0f, 2.0f);
		water.addWave(64.0f, 0.2f, 1.0f, -90.0f, 0.1f);

		// Changing amplitude and length for the second wave
		water.setWaveAmplitude(1, 0.03f);
		water.setWaveLength(1, 10.0f);

	return 1;
}

```

</details>


### Getting Water Level and Surface Normal


To ensure proper placement and orientation of objects relatively to the water surface you need to obtain water level (height) and normal orientation at a certain point. You can do this using the following methods:


- *[fetchHeight()](#fetchHeight_Vec3_float)*
- *[fetchNormal()](#fetchNormal_Vec3_vec3)*


By default the quality (precision) of calculating heights and normals is set to optimize performance, but in case of higher Beaufort levels (resulting in significant wave steepness and height differences on the water surface), calculation results may differ from visual representation (e.g. calculated water level may be greater the actual value). This may, for example, result in setting incorrect position and orientation for a ship relative to the water surface. To avoid such cases you can increase the quality of calculations for height/normal fetch requests via the following parameters are available via API:


- **Steepness Quality** *[setFetchSteepnessQuality()](../../...md#setFetchSteepnessQuality_int_void)* - wave steepness calculation accuracy used when calculating water level (height) and normal orientation at a certain point. This parameter is used to improve calculation results in case of high wave steepness (higher Beaufort levels). Low quality is usually sufficient for calm water (*high* quality provides good results for Beauforts 6-7, while *ultra* is recommended for Beauforts 8-10).
- **Amplitude Threshold** *[setFetchAmplitudeThreshold()](../../...md#setFetchAmplitudeThreshold_float_void)* - this is the minimum amplitude threshold for waves to be taken into account in height and normal calculations (waves having smaller amplitudes will be ignored).


> **Notice:** Using higher quality has an impact on performance, so we recommended to increase it only when necessary (when Beaufort levels are high) and set it back to the default level, when the water surface gets relatively calm.


So in case of higher Beaufort levels you can adjust the quality of intersections calculation using the following lines:


```cpp
water_global_object.setFetchSteepnessQuality(3);
water_global_object.setFetchAmplitudeThreshold(0.01f);

```


### Finding Intersection Points


Intersections are used for many purposes, for example, you can find an intersection point of a projectile with the water surface to spawn some splashes. By default the quality (precision) of calculating intersection points is set to optimize performance, but in case of higher Beaufort levels (resulting in significant wave steepness and height differences on the water surface), calculation results may differ from visual representation (e.g. intersection point is detected at some distance from the water surface). This may, for example, result in spawning particle systems representing splashes at a wrong position. To avoid such cases you can increase the quality of calculations for intersection detection via the following parameters are available via API:


- **Precision** *[setIntersectionPrecision()](../../...md#setIntersectionPrecision_float_void)* - represents a permissible error between the calculated and real water intersection point.
- **Steepness Quality** *[setIntersectionSteepnessQuality()](../../...md#setIntersectionSteepnessQuality_int_void)* - wave steepness calculation accuracy used in intersection calculations. This parameter is used to improve calculation of intersections in case of high wave steepness (higher Beaufort levels). Low quality is usually sufficient for calm water (*high* quality provides good results for Beauforts 6-7, while *ultra* is recommended for Beauforts 8-10).
- **Amplitude Threshold** *[setIntersectionAmplitudeThreshold()](../../...md#setIntersectionAmplitudeThreshold_float_void)* - this is the minimum amplitude threshold for waves to be taken into account in intersection calculations (waves having smaller amplitudes will be ignored).


> **Notice:** Using higher quality has an impact on performance, so we recommended to increase it only when necessary (when Beaufort levels are high) and set it back to the default level, when the water surface gets relatively calm.


So in case of higher Beaufort levels you can adjust the quality of intersections calculation using the following lines:


```cpp
water_global_object.setIntersectionSteepnessQuality(3);
water_global_object.setIntersectionAmplitudeThreshold(0.01f);

```


### Usage Example


This example demonstrates the influence of the **[Steepness Quality](#setFetchSteepnessQuality_int_void), [Amplitude Threshold](#setFetchAmplitudeThreshold_float_void)**, and **[Precision](#setIntersectionPrecision_float_void)** parameters on the accuracy of fetch and intersection requests for the *Global Water* object at various Beaufort levels.


### See Also


- C++ samples:

  -
  -
  -
  -
  -
- C# samples:

  -
  -
  -


## ObjectWaterGlobal Class

### Members

---

## static ObjectWaterGlobal ( )

Constructor. Creates a new global water object.
## int getPhysicsFieldMask ( )

Returns the FieldHeight physics mask of the assigned material on the Global Water.
### Return value

The FieldHeight physics mask.
## int getVisualFieldMask ( )

Returns the FieldHeight visual mask of the assigned material on the Global Water.
### Return value

The FieldHeight visual mask.
## float getMeanLevel ( )

Returns the average Z coordinate of the water object.
### Return value

The Z coordinate value.
## void setAnimationTime ( float time )


Sets water animation time value for water synchronization. It is used for effects, such as normals, caustics, and foam.


### Arguments

- *float* **time** - Water animation time value.

## float getAnimationTime ( )

Returns water animation time value for water synchronization.
### Return value

Water animation time value.
## void setLayerName ( int layer , string value )

Sets a new name for the wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number
- *string* **value** - Name of the layer.

## string getLayerName ( int layer )

Returns the name of the wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number

### Return value

Name of the layer
## void setLayerWeight ( int layer , float value )

Sets a weight for a given wave layer. This value determines how much the given layer affects the final wave form. It can be used for smooth transitions between the states of water. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number
- *float* **value** - Layer weight

## float getLayerWeight ( int layer )

Returns the current weight of the wave layer. This value determines how much the given layer affects the final wave form. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number

### Return value

Weight of the layer.
## void setLayerDirectionAngleVariance ( int layer , float value )

Sets a variance value of the wave direction angle for a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number
- *float* **value** - Variance value.

## float getLayerDirectionAngleVariance ( int layer )

Returns the current variance value of the wave direction angle for a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number

### Return value

Variance value.
## void setLayerSteepnessScale ( int layer , float value )

Sets a [steepness scale](../../../objects/objects/water/water_object.md#steepness_scale) value for a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number
- *float* **value** - Steepness scale value.

## float getLayerSteepnessScale ( int layer )

Returns the current [steepness scale](../../../objects/objects/water/water_object.md#steepness_scale) value for a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number

### Return value

Steepness scale value.
## void setLayerAmplitudeRange ( int layer , vec2 value )

Sets a range of wave amplitudes for a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number.
- *vec2* **value** - Amplitude range.

## vec2 getLayerAmplitudeRange ( int layer )

Returns the current range of wave amplitudes of a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number.

### Return value

Amplitude range.
## void setLayerLengthRange ( int layer , vec2 value )

Sets a range of wave lengths for a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number
- *vec2* **value** - Length range.

## vec2 getLayerLengthRange ( int layer )

Returns the current range of wave lengths of a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number

### Return value

Length range.
## void setLayerNumWaves ( int layer , int num )

Sets the number of waves for a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number
- *int* **num** - Number of waves.

## int getLayerNumWaves ( int layer )

Returns the number of waves on a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number

### Return value

Number of waves.
## int isLayerEnabled ( int layer )

Returns a value indicating if a given wave layer is enabled. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number

### Return value

**1** if the layer is enabled; otherwise, **0**.
## void setLayerEnabled ( int layer , int enabled )

Enables or disables a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number
- *int* **enabled** - **1** to enable the layer, **0** to disable it.

## void swapLayer ( int num_0 , int num_1 )

Swaps two specified wave layers. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **num_0** - Layer1 number.
- *int* **num_1** - Layer2 number.

## int getNumLayers ( )

Returns the current number of wave layers. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Return value

Number of wave layers.
## void removeLayer ( int layer )

Removes a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number

## int addLayer ( )

Appends a new wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Return value

Number of the new added layer.
## void setWavePhaseOffset ( int index , float value )

Sets the phase offset parameter for a given wave. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.
- *float* **value** - Phase offset parameter value in radians in range [0; 2pi].

## float getWavePhaseOffset ( int index )

Returns the value of the Phase Offset parameter of a wave. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.

### Return value

Phase offset parameter value in radians in range [0; 2pi].
## void setWaveDirectionAngle ( int index , float value )

Sets direction (angle of spreading) for a given wave:
- If 0 is specified, the wave spreads along the Y axis and is parallel to the X axis.
- If a positive value is specified, the wave direction is slanted counterclockwise relative to its initial spread.
- If a negative value is specified, the wave is rotated clockwise.


Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).


### Arguments

- *int* **index** - Wave number.
- *float* **value** - Angle, in degrees. Both positive and negative values are acceptable.

## float getWaveDirectionAngle ( int index )

Returns direction (angle of spreading) of a given wave. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.

### Return value

Angle, in degrees.
## void setWaveSteepness ( int index , float value )

Sets the steepness value for a given wave. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.
- *float* **value** - Steepness value.

## float getWaveSteepness ( int index )

Returns the current steepness value of the given wave. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.

### Return value

Steepness value.
## void setWaveAmplitude ( int index , float value )

Sets the distance between the highest and the lowest peaks for a given wave. It sets the wave form along with the [setWaveLength()](#setWaveLength_int_float_void) function. The higher the value is, the higher the waves are. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.
- *float* **value** - Amplitude, in units.

## float getWaveAmplitude ( int index )

Returns the distance between the highest and the lowest peaks for the given wave. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.

### Return value

Amplitude, in units.
## void setWaveLength ( int index , float value )

Sets the distance between successive crests for a given wave. The higher the length value is, the broader the waves are. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.
- *float* **value** - Length, in units.

## float getWaveLength ( int index )

Returns the distance between successive crests of the given wave. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.

### Return value

Length, in units.
## int getNumWaves ( )

Returns the current number of simulated waves. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Return value

Number of waves.
## void removeWave ( int index )

Removes the wave having a specified number. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.

## int addWave ( float length , float amplitude , float steepness , float direction_angle , float phase )

Adds a wave if the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Arguments

- *float* **length** - Wave length.
- *float* **amplitude** - Wave amplitude.
- *float* **steepness** - Wave steepness.
- *float* **direction_angle** - Angle of the wave direction in degrees. At 0 angle the wave will be directed along the X-axis.
- *float* **phase** - Phase offset of the wave in radians (0 to 2pi).

### Return value

Number of the added wave.
## float getWindAffect ( )

Returns the current value determining how much the wind direction affects the waves.
### Return value

Wind influence value in range [0;1].
## void setWindAffect ( float affect )

Sets how much the wind direction affects the waves.
### Arguments

- *float* **affect** - Wind influence in range [0;1]. If you set it to 1, all waves will be directed along the wind direction.

## float getWindDirectionAngle ( )

Returns the angle that determines the wind direction.
### Return value

Angle, in degrees.
## void setWindDirectionAngle ( float angle )

Sets the angle that determines the wind direction.
### Arguments

- *float* **angle** - Wind direction angle, in degrees.

## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_usc.md) type identifier.
## void setActiveWater ( int water )

Sets a value indicating if the global water object is active. If there are more than one global water nodes in the scene, only the active one will be rendered.
### Arguments

- *int* **water** - **1** to set the global water object as active, **0** - to set it as inactive.

## int isActiveWater ( )

Returns a value indicating if the global water object is active.
### Return value

**1** if the global water object is active, **0** - if it is inactive.
## float fetchHeight ( Vec3 position )

Returns a height offset of the specified point relative to the current water level calculated at this point. E.g. in case the specified point is (0, 0, -3) and the current water level calculated for this point is equal to 5, the function shall return 8.


![](fetch.png)


> **Notice:** In case of higher Beaufort levels (resulting in significant wave steepness and height differences on the water surface), calculation results may differ from visual representation (e.g. calculated water level may be greater the actual value). To avoid it and increase precision, [adjust calculation quality](#fetch).

### Arguments

- *Vec3* **position** - Point position coordinates.

### Return value

Height offset of the specified point relative to the current water level calculated at this point, in meters.
## vec3 fetchNormal ( Vec3 position )

Returns a normal vector to the water surface at the specified point (to orient objects along the waves normals).
> **Notice:** In case of higher Beaufort levels (resulting in significant wave steepness and height differences on the water surface), calculation results may differ from visual representation (e.g. calculated water level may be greater the actual value). To avoid it and increase precision, [adjust calculation quality](#fetch).

### Arguments

- *Vec3* **position** - Point position coordinates.

### Return value

Normal vector.
## void setFetchAmplitudeThreshold ( float threshold )

Sets the threshold for amplitude values that will not participate in [height and normal calculations](#fetch). The more you cut off, the less accurate the height value you get, but the faster are the calculations.
### Arguments

- *float* **threshold** - Amplitude threshold. The default value is 0.1f.

## float getFetchAmplitudeThreshold ( )

Returns the current threshold for amplitude values that will not participate in [height and normal calculations](#fetch).
### Return value

Amplitude threshold.
## void setFetchSteepnessQuality ( int quality )

Sets the wave steepness calculation quality used in [height and normal calculations](#fetch). Low quality is usually sufficient for calm water and large floating objects. If the waves are big, or you want to simulate small floating objects, you may need to increase the quality. Higher quality gives a more precise result but affects performance.
### Arguments

- *int* **quality** - Quality value.

## int getFetchSteepnessQuality ( )

Returns the wave steepness calculation quality used in [height and normal calculations](#fetch).
### Return value

Number of iterations (0 to 4). The default number is 0.
## float getIntersectionAmplitudeThreshold ( )

Returns the current threshold of amplitude values that will not participate in [intersection calculations](#intersections).
### Return value

Amplitude threshold.
## void setIntersectionAmplitudeThreshold ( float threshold )

Sets the threshold for amplitude values that will not participate in [intersection calculations](#intersections). The default value is 0.1f.
### Arguments

- *float* **threshold** - Amplitude threshold.

## void setIntersectionPrecision ( float precision )

Sets an intersection precision which represents an error between the real value of the water intersection point and the calculated value. The default value is 0.25.
### Arguments

- *float* **precision** - Precision for intersection detection.

## float getIntersectionPrecision ( )

Returns current intersection precision which represents an error between the real value of the water intersection point and the calculated value.
### Return value

Precision for intersection detection.
## void setIntersectionSteepnessQuality ( int quality )

Sets the wave steepness calculation quality used in [intersection calculations](#intersections). Low quality is usually sufficient for calm water and large floating objects. If the waves are big, or you want to simulate small floating objects, you may need to increase the quality. Higher quality gives a more precise result but affects performance.
### Arguments

- *int* **quality** - Number of iterations (0 to 4). The default number is 0.

## int getIntersectionSteepnessQuality ( )

Returns the wave steepness calculation quality used in [intersection calculations](#intersections). Low quality is usually sufficient for calm water and large floating objects. If the waves are big, or you want to simulate small floating objects, you may need to increase the quality. Higher quality gives a more precise result but affects performance.
### Return value

Steepness quality.
## void setSoftInteraction ( float intersection )

Sets soft intersection of water with the shoreline and surfaces of objects.
### Arguments

- *float* **intersection** - Soft intersection value.

## float getSoftInteraction ( )

Returns the current soft intersection of water with the shoreline and surfaces of objects.
### Return value

Soft intersection value.
## void takeSyncData ( Stream stream )

Writes wave synchronization data to the specified stream.
### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream to which wave synchronization data is to be written.

## void applySyncData ( Stream stream )

Reads wave synchronization data from the specified stream and applies it to the wave system.
### Arguments

- *[Stream](../../../api/library/common/class.stream_usc.md)* **stream** - Stream with wave synchronization data to be applied.

## void setWavesMode ( int mode )

Sets the [wave generation mode](../../../objects/objects/water/water_object.md#creating_waves).
### Arguments

- *int* **mode** - A desired wave mode.

## int getWavesMode ( )

Returns the current [wave generation mode](../../../objects/objects/water/water_object.md#creating_waves).
### Return value

Wave mode.
## void setBeaufort ( float beaufort )

Sets the Beaufort wind force scale value.
### Arguments

- *float* **beaufort** - Beaufort value from 0 (Calm) to 12 (Hurricane). Available when the *Beauforts* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).

## float getBeaufort ( )

Returns the current Beaufort wind force scale value. Available when the *Beauforts* mode [is set](../../../api/library/objects/class.objectwaterglobal_usc.md#setWavesMode_int_void).
### Return value

Beaufort value.
## void setGeometryNormalIntensity ( float intensity )

Sets the intensity of normals of the waves.
### Arguments

- *float* **intensity** - Intensity value.

## float getGeometryNormalIntensity ( )

Returns the current intensity of normals of the waves.
### Return value

Intensity value.
## void setTextureNormalBlur ( float blur )

Sets the blurring ratio for the procedurally generated normals. This parameter enables you to reduce pixelation of the normal map, and make it less pronounced. It is recommended to use small values for correction, when necessary. This affects the normals generated for [Field Height](../../../objects/effects/fields/field_height/index.md) and [Field Shoreline](../../../objects/effects/fields/field_shoreline/index.md).
### Arguments

- *float* **blur** - Normal blur value.

## float getTextureNormalBlur ( )

Returns the current blurring ratio for the procedurally generated normals. This parameter enables you to reduce pixelation of the normal map, and make it less pronounced. It is recommended to use small values for correction, when necessary. This affects the normals generated for [Field Height](../../../objects/effects/fields/field_height/index.md) and [Field Shoreline](../../../objects/effects/fields/field_shoreline/index.md).
### Return value

Normal blur value.
## void setTextureNormalIntensity ( float intensity )

Sets the intensity of procedurally generated normals. This affects the normals generated for [Field Height](../../../objects/effects/fields/field_height/index.md) and [Field Shoreline](../../../objects/effects/fields/field_shoreline/index.md).
### Arguments

- *float* **intensity** - Intensity value.

## float getTextureNormalIntensity ( )

Returns the current intensity of procedurally generated normals. This affects the normals generated for [Field Height](../../../objects/effects/fields/field_height/index.md) and [Field Shoreline](../../../objects/effects/fields/field_shoreline/index.md).
### Return value

Intensity value.
## void setDetailTexturePath ( string path )

Sets a path to the location of a [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
### Arguments

- *string* **path** - Detail texture path.

## string getDetailTexturePath ( )

Returns the current path to the location of a [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
### Return value

Detail texture path.
## void setDetail0UVSize ( vec2 size )

Sets the size of the first sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
### Arguments

- *vec2* **size** - Size value.

## vec2 getDetail0UVSize ( )

Returns the current size of the first sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
### Return value

Size value.
## void setDetail0UVSpeed ( vec2 speed )

Sets the speed of the first sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
### Arguments

- *vec2* **speed** - Speed value.

## vec2 getDetail0UVSpeed ( )

Returns the current speed of the first sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
### Return value

Speed value.
## void setDetail0Intensity ( float intensity )

Sets the intensity of the first sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
### Arguments

- *float* **intensity** - Intensity value.

## float getDetail0Intensity ( )

Returns the current intensity of the first sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
### Return value

Intensity value.
## void setDetail1UVSize ( vec2 size )

Sets the size of the second sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
### Arguments

- *vec2* **size** - Size value.

## vec2 getDetail1UVSize ( )

Returns the current size of the second sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
### Return value

Size value.
## void setDetail1UVSpeed ( vec2 speed )

Sets the speed of the second sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
### Arguments

- *vec2* **speed** - Speed of the detail texture.

## vec2 getDetail1UVSpeed ( )

Returns the current speed of the second sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
### Return value

Speed value.
## void setDetail1Intensity ( float intensity )

Sets the intensity of the second sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
### Arguments

- *float* **intensity** - Intensity value.

## float getDetail1Intensity ( )

Returns the current intensity of the first sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
### Return value

Intensity value.
## void setDistantWavesTexturePath ( string path )

Sets the path to the [normal map](../../../objects/objects/water/water_object.md#distant_waves_normal_map) of the [distant waves](../../../objects/objects/water/water_object.md#distant_waves).
### Arguments

- *string* **path** - Path to the [normal map](../../../objects/objects/water/water_object.md#distant_waves_normal_map).

## string getDistantWavesTexturePath ( )

Returns the current path to the [normal map](../../../objects/objects/water/water_object.md#distant_waves_normal_map) of the [distant waves](../../../objects/objects/water/water_object.md#distant_waves).
### Return value

Path to the [normal map](../../../objects/objects/water/water_object.md#distant_waves_normal_map).
## void setDistantWavesUVTransform ( vec4 transform )

Specifies the UV transform for the [distant waves](../../../objects/objects/water/water_object.md#distant_waves) normal map.
### Arguments

- *vec4* **transform** - The first two values (x, y) represent the scale texture coordinates along the X and Y axes. The third and forth (z, w) specify the speed of movement animation.

## vec4 getDistantWavesUVTransform ( )

Returns the current UV transform for the [distant waves](../../../objects/objects/water/water_object.md#distant_waves) normal map.
### Return value

The first two values (x, y) represent the scale texture coordinates along the X and Y axes. The third and forth (z, w) specify the speed of movement animation.
## void setDistantWavesIntensity ( float scale )

Sets the intensity for [distant waves](../../../objects/objects/water/water_object.md#distant_waves).
> **Notice:** Unavailable for modes with Beaufort levels blending.

### Arguments

- *float* **scale** - Intensity value.

## float getDistantWavesIntensity ( )

Returns the current intensity value for [distant waves](../../../objects/objects/water/water_object.md#distant_waves).
> **Notice:** Unavailable for modes with Beaufort levels blending.

### Return value

Intensity value.
## void setDistantWavesBlendDistanceStart ( float start )

Sets the fade-in start distance for [distant waves](../../../objects/objects/water/water_object.md#distant_waves).
### Arguments

- *float* **start** - Fade-in start distance.

## float getDistantWavesBlendDistanceStart ( )

Returns the current fade-in start distance for [distant waves](../../../objects/objects/water/water_object.md#distant_waves).
### Return value

Fade-in start distance.
## void setDistantWavesBlendDistanceEnd ( float end )

Sets the fade-in end distance for [distant waves](../../../objects/objects/water/water_object.md#distant_waves).
### Arguments

- *float* **end** - Fade-in end distance.

## float getDistantWavesBlendDistanceEnd ( )

Returns the current fade-in end distance for [distant waves](../../../objects/objects/water/water_object.md#distant_waves).
### Return value

Fade end distance.
## void setDistantWavesBlendMax ( float value )

Sets the value representing the maximum amount of [distant waves](../../../objects/objects/water/water_object.md#distant_waves) in the crossfade zone where the main geometry waves fade out and distant waves fade in.
### Arguments

- *float* **value** - A value representing the maximum amount of distant waves. Range: [0; 1], the default value is 0.

## float getDistantWavesBlendMax ( )

Returns the current value representing the maximum amount of [distant waves](../../../objects/objects/water/water_object.md#distant_waves) in the crossfade zone where the main geometry waves fade out and distant waves fade in.
### Return value

A value representing the maximum amount of distant waves.
## void setDistantWavesBlendMin ( float value )

Sets the value representing the minimum amount of [distant waves](../../../objects/objects/water/water_object.md#distant_waves) in the crossfade zone where the main geometry waves fade out and distant waves fade in.
### Arguments

- *float* **value** - A value representing the minimum amount of distant waves. Range: [0; 1], the default value is 0.

## float getDistantWavesBlendMin ( )

Returns the current value representing the minimum amount of [distant waves](../../../objects/objects/water/water_object.md#distant_waves) in the crossfade zone where the main geometry waves fade out and distant waves fade in.
### Return value

A value representing the minimum amount of distant waves.
## void setFoamTexturePath ( string path )

Sets the path to the [foam texture](../../../objects/objects/water/water_object.md#texture).
### Arguments

- *string* **path** - Path to the foam texture.

## string getFoamTexturePath ( )

Returns the current path to the [foam texture](../../../objects/objects/water/water_object.md#texture).
### Return value

Path to the foam texture.
## void setFoam0UVScale ( float scale )

Sets the UV scale for the first sample of the foam texture.
### Arguments

- *float* **scale** - Scale value.

## float getFoam0UVScale ( )

Returns the current UV scale for the first sample of the foam texture.
### Return value

Scale value.
## void setFoam0UVSpeed ( float speed )

Sets the speed for the first sample of the foam texture.
### Arguments

- *float* **speed** - Speed value.

## float getFoam0UVSpeed ( )

Returns the current speed for the first sample of the foam texture.
### Return value

Speed value.
## void setFoam1UVScale ( float scale )

Sets the UV scale for the second sample of the foam texture.
### Arguments

- *float* **scale** - Scale value.

## float getFoam1UVScale ( )

Returns the current UV scale for the second sample of the foam texture.
### Return value

Scale value.
## void setFoam1UVSpeed ( float speed )

Sets the speed for the second sample of the foam texture.
### Arguments

- *float* **speed** - Speed value.

## float getFoam1UVSpeed ( )

Returns the current speed for the second sample of the foam texture.
### Return value

Speed value.
## void setFoamPeakContrast ( float contrast )

Sets the foam contrast on the wave peaks.
### Arguments

- *float* **contrast** - Contrast value.

## float getFoamPeakContrast ( )

Returns the current foam contrast on the wave peaks.
### Return value

Contrast value.
## void setFoamPeakIntensity ( float intensity )

Sets the foam intensity on the wave peaks.
### Arguments

- *float* **intensity** - Intensity value.

## float getFoamPeakIntensity ( )

Returns the current foam intensity on the wave peaks.
### Return value

Intensity value.
## void setFoamWhitecapContrast ( float contrast )

Sets the foam contrast on the white caps.
### Arguments

- *float* **contrast** - Contrast value.

## float getFoamWhitecapContrast ( )

Returns the current foam contrast on the white caps.
### Return value

Contrast value.
## void setFoamWhitecapIntensity ( float intensity )

Sets the foam intensity on the white caps.
### Arguments

- *float* **intensity** - Intensity value.

## float getFoamWhitecapIntensity ( )

Returns the current foam intensity on the white caps.
### Return value

Intensity value.
## void setFoamWindContrast ( float contrast )

Sets the contrast for the foam generated based on the wind direction.
### Arguments

- *float* **contrast** - Contrast value.

## float getFoamWindContrast ( )

Returns the current contrast for the foam generated based on the wind direction.
### Return value

Contrast value.
## void setFoamWindIntensity ( float intensity )

Sets the intensity for the foam generated based on the wind direction.
### Arguments

- *float* **intensity** - Intensity value.

## float getFoamWindIntensity ( )

Returns the current intensity for the foam generated based on the wind direction.
### Return value

Intensity value.
## void setFieldHeightFoamContrast ( float contrast )

Sets the contrast of the foam generated from the [FieldHeight](../../../objects/effects/fields/field_height/index.md) objects placed in Global Water.
### Arguments

- *float* **contrast** - Contrast value.

## float getFieldHeightFoamContrast ( )

Returns the current contrast of the foam generated from the [FieldHeight](../../../objects/effects/fields/field_height/index.md) objects placed in Global Water.
### Return value

Contrast value.
## void setFieldHeightFoamIntensity ( float intensity )

Sets the intensity of the foam generated from the [FieldHeight](../../../objects/effects/fields/field_height/index.md) objects placed in Global Water.
### Arguments

- *float* **intensity** - Intensity value.

## float getFieldHeightFoamIntensity ( )

Returns the current intensity of the foam generated from the [FieldHeight](../../../objects/effects/fields/field_height/index.md) objects placed in Global Water.
### Return value

Intensity value.
## void setFoamContactIntensity ( float intensity )

Sets the foam intensity near shores or different objects in water.
### Arguments

- *float* **intensity** - Intensity value.

## float getFoamContactIntensity ( )

Returns the current foam intensity near shores or different objects in water.
### Return value

Intensity value.
## void setFoamTextureAffect ( float affect )

Sets the visibility of the foam texture. It can be used to create additional effects, e.g., foam bubbles.
### Arguments

- *float* **affect** - Texture affect value.

## float getFoamTextureAffect ( )

Sets the visibility of the foam texture.
### Return value

Texture affect value.
## void setSubsurfaceColor ( vec4 color )

Sets the [water subsurface scattering (SSS) color](../../../objects/objects/water/water_object.md#color).
### Arguments

- *vec4* **color** - Color value.

## vec4 getSubsurfaceColor ( )

Returns the current [water subsurface scattering (SSS) color](../../../objects/objects/water/water_object.md#color).
### Return value

Color value.
## void setSubsurfaceAmbientIntensity ( float intensity )

Sets the [intensity of subsurface scattering](../../../objects/objects/water/water_object.md#ambient_intensity) for ambient lighting.
### Arguments

- *float* **intensity** - Intensity value. The lower the value, the faster the light rays dissipate in water.

## float getSubsurfaceAmbientIntensity ( )

Returns the current [intensity of subsurface scattering](../../../objects/objects/water/water_object.md#ambient_intensity) for ambient lighting.
### Return value

Intensity value.
## void setSubsurfaceWaveIntensity ( float intensity )

Sets the intensity of [light rays passing through waves](../../../objects/objects/water/water_object.md#intensity_through_waves).
### Arguments

- *float* **intensity** - Intensity value. The lower the value, the faster the light rays dissipate in water.

## float getSubsurfaceWaveIntensity ( )

Returns the current intensity of [light rays passing through waves](../../../objects/objects/water/water_object.md#intensity_through_waves).
### Return value

Intensity value.
## void setSubsurfaceWaveFoamIntensity ( float intensity )

Sets the intensity of [subsurface scattering near the foam areas](../../../objects/objects/water/water_object.md#intensity_around_foam).
### Arguments

- *float* **intensity** - Intensity value.

## float getSubsurfaceWaveFoamIntensity ( )

Returns the current intensity of subsurface scattering near the foam areas.
### Return value

Intensity value.
## void setSubsurfaceDecalsIntensity ( float intensity )

Sets the intensity of subsurface scattering of diffuse lighting for decals.
### Arguments

- *float* **intensity** - New subsurface scattering intensity value to be set.

## float getSubsurfaceDecalsIntensity ( )

Returns the current intensity of subsurface scattering of diffuse lighting for decals.
### Return value

Current subsurface scattering intensity value.
## void setDepthLUTTexturePath ( string path )

Sets the path to the [LUT texture](../../../objects/objects/water/water_object.md#depth_lut) that shows the color of the bottom.
### Arguments

- *string* **path** - Path to the texture.

## string getDepthLUTTexturePath ( )

Returns the current path to the [LUT texture](../../../objects/objects/water/water_object.md#depth_lut) that shows the color of the bottom.
### Return value

Path to the texture.
## void setUnderwaterFogColor ( vec4 color )

Sets the [underwater fog color](../../../objects/objects/water/water_object.md#fog_color). The Sun and Environment lighting affect this parameter to create the final underwater fog color.
### Arguments

- *vec4* **color** - Color value.

## vec4 getUnderwaterFogColor ( )

Returns the current [underwater fog color](../../../objects/objects/water/water_object.md#fog_color).
### Return value

Color value.
## void setUnderwaterFogTransparency ( float transparency )

Sets the [transparency of the underwater fog](../../../objects/objects/water/water_object.md#fog_transparency).
### Arguments

- *float* **transparency** - Transparency value. The higher the value, the more transparent the underwater fog is.

## float getUnderwaterFogTransparency ( )

Returns the current [transparency of the underwater fog](../../../objects/objects/water/water_object.md#fog_transparency).
### Return value

Transparency value.
## void setUnderwaterFogDepth ( float depth )

Sets the [distance from the water surface](../../../objects/objects/water/water_object.md#fog_lighting_depth) up to which the light affects the underwater color.
### Arguments

- *float* **depth** - Depth value, in units.

## float getUnderwaterFogDepth ( )

Returns the current [distance from the water surface](../../../objects/objects/water/water_object.md#fog_lighting_depth) up to which the light affects the underwater color.
### Return value

Depth value, in units.
## void setUnderwaterFogOffset ( float offset )

Sets the height offset for lighting.
### Arguments

- *float* **offset** - Offset value.

## float getUnderwaterFogOffset ( )

Returns the current height offset for lighting.
### Return value

Offset value.
## void setUnderwaterFogEnvironmentInfluence ( float influence )

Sets the degree of impact of the environment lighting on the final underwater color.
### Arguments

- *float* **influence** - Influence value.

## float getUnderwaterFogEnvironmentInfluence ( )

Returns the current degree of impact of the environment lighting on the final underwater color.
### Return value

Influence value.
## void setUnderwaterFogSunInfluence ( float influence )

Sets the degree of impact of the sun lighting on the final underwater color.
### Arguments

- *float* **influence** - Influence value.

## float getUnderwaterFogSunInfluence ( )

Returns the current degree of impact of the sun lighting on the final underwater color.
### Return value

Influence value.
## void setUnderwaterShaftIntensity ( float intensity )

Sets the intensity of the underwater sun shafts.
### Arguments

- *float* **intensity** - Intensity value.

## float getUnderwaterShaftIntensity ( )

Returns the current intensity of the underwater sun shafts.
### Return value

Intensity value.
## void setWaterlineSize ( float size )

Sets the [size of the borderline](../../../objects/objects/water/water_object.md#waterline_size) between the overwater and underwater environments.
### Arguments

- *float* **size** - Waterline size.

## float getWaterlineSize ( )

Returns the current [size of the borderline](../../../objects/objects/water/water_object.md#waterline_size) between the overwater and underwater environments.
### Return value

Waterline size.
## void setUnderwaterDofDistance ( float distance )

Sets the focal distance for the [underwater DOF effect](../../../objects/objects/water/water_object.md#underwater_dof).
### Arguments

- *float* **distance** - Focal distance.

## float getUnderwaterDofDistance ( )

Returns the current focal distance for the [underwater DOF effect](../../../objects/objects/water/water_object.md#underwater_dof).
### Return value

Focal distance.
## void setPlanarReflectionDistance ( float distance )

Sets the distance from the reflection viewport camera to the reflected object. This distance sums up to the distance from the camera to the reflective surface plus the distance from object to reflective surface.
### Arguments

- *float* **distance** - Distance, in units.

## float getPlanarReflectionDistance ( )

Returns the current distance from the reflection viewport camera to the reflected object. This distance sums up to the distance from the camera to the reflective surface plus the distance from object to reflective surface.
### Return value

Distance, in units.
## void setPlanarReflectionPivotOffset ( vec3 offset )

Sets the position of the reflection pivot point.
### Arguments

- *vec3* **offset** - Pivot point offset.

## vec3 getPlanarReflectionPivotOffset ( )

Returns the current position of the reflection pivot point.
### Return value

Pivot point offset.
## void setReflectionRoughness ( float roughness )

Sets the environment [reflection roughness](../../../objects/objects/water/water_object.md#roughness) of the water surface. This parameter helps to tweak reflections on the water surface relative to the environment.
### Arguments

- *float* **roughness** - Roughness value.

## float getReflectionRoughness ( )

Returns the current environment [reflection roughness](../../../objects/objects/water/water_object.md#roughness) of the water surface. This parameter helps to tweak reflections on the water surface relative to the environment.
### Return value

Roughness value.
## void setReflectionOcclusion ( float occlusion )

Sets the [occlusion factor for environment reflections](../../../objects/objects/water/water_object.md#occlusion) on parts of the water surface with negative normals. Using this parameter enables simulation of reflection of waves on the water surface removing too bright areas on waves close to the horizon.
### Arguments

- *float* **occlusion** - Occlusion value. Minimum value is 0 - no occlusion. By the higher values, occlusion is performed for reflections on parts of the water surface with negative normals that have a certain slope. The higher the value, the less intensive reflections are on the surface parts with negative normals.

## float getReflectionOcclusion ( )

Returns the current [occlusion factor for environment reflections](../../../objects/objects/water/water_object.md#occlusion) on parts of the water surface with negative normals. Using this parameter enables simulation of reflection of waves on the water surface removing too bright areas on waves close to the horizon.
### Return value

Occlusion value.
## void setReflectionOcclusionSlope ( float slope )

Sets the slope of negative normals of the water surface, at which occlusion is performed for wave reflections.
### Arguments

- *float* **slope** - Slope value.

## float getReflectionOcclusionSlope ( )

Returns the current slope of negative normals of the water surface, at which occlusion is performed for wave reflections.
### Return value

Slope value.
## void setCausticsTexturePath ( string path )

Sets the path to the [3D Caustic texture](../../../objects/objects/water/water_object.md#caustics_texture) which determines the [pattern of light rays](../../../objects/objects/water/water_object.md#enable_caustics) refracted by the water surface. The texture is 1-channeled: *R* value defines the caustics pattern.
### Arguments

- *string* **path** - Path to the texture.

## string getCausticsTexturePath ( )

Returns the current path to the [3D Caustic texture](../../../objects/objects/water/water_object.md#caustics_texture) which determines the [pattern of light rays](../../../objects/objects/water/water_object.md#enable_caustics) refracted by the water surface.
### Return value

Path to the texture.
## void setCausticUVTransform ( vec4 transform )

Sets the [UV Transform](../../../objects/objects/water/water_object.md#caustics_uv_transform) coordinates for the caustic texture.
### Arguments

- *vec4* **transform** - Transform coordinates.

## vec4 getCausticUVTransform ( )

Returns the current [UV Transform](../../../objects/objects/water/water_object.md#caustics_uv_transform) coordinates for the caustic texture.
### Return value

Transform coordinates.
## void setCausticDistanceFade ( float fade )

Sets the [distance from the water surface](../../../objects/objects/water/water_object.md#caustics_distance_fade) downwards, at which light shapes fade.
### Arguments

- *float* **fade** - Distance, in units.

## float getCausticDistanceFade ( )

Returns the current [distance from the water surface](../../../objects/objects/water/water_object.md#caustics_distance_fade) downwards, at which light shapes fade.
### Return value

Distance, in units.
## void setCausticAnimationSpeed ( float speed )

Sets the movement speed of the light patterns.
### Arguments

- *float* **speed** - Speed value.

## float getCausticAnimationSpeed ( )

Returns the current movement speed of the light patterns.
### Return value

Speed value.
## void setCausticBrightness ( float brightness )

Sets the brightness of the light shapes.
### Arguments

- *float* **brightness** - Brightness value.

## float getCausticBrightness ( )

Returns the current brightness of the light shapes.
### Return value

Brightness value.
## void setFieldShorelineLUTTexturePath ( string path )

Sets the path to the LUT texture used for shoreline wetness effect.
### Arguments

- *string* **path** - Path to the texture.

## string getFieldShorelineLUTTexturePath ( )

Returns the current path to the LUT texture used for shoreline wetness effect.
### Return value

Path to the texture.
## void setFieldShorelineWaveSpeed ( float speed )

Sets the speed of tidal waves.
### Arguments

- *float* **speed** - Wave speed value.

## float getFieldShorelineWaveSpeed ( )

Returns the current speed of tidal waves.
### Return value

Wave speed value.
## void setFieldShorelineWaveTiling ( float tiling )

Sets the frequency of tidal waves.
### Arguments

- *float* **tiling** - Tiling value.

## float getFieldShorelineWaveTiling ( )

Returns the current frequency of tidal waves.
### Return value

Tiling value.
## void setFieldShorelineWaveHeight ( float height )

Sets the height of oncoming tidal waves.
### Arguments

- *float* **height** - Height value.

## float getFieldShorelineWaveHeight ( )

Returns the current height of oncoming tidal waves.
### Return value

Height value.
## void setFieldShorelineWaveFalloff ( float falloff )

Sets the visibility gradient of waves coming from sea to the shore.
### Arguments

- *float* **falloff** - Falloff value.

## float getFieldShorelineWaveFalloff ( )

Returns the current visibility gradient of waves coming from sea to the shore.
### Return value

Falloff value.
## void setFieldShorelineWaveExponent ( float exponent )

Sets the nonlinearity of tidal waves frequency and movement speed depending on their distance from the shoreline.
### Arguments

- *float* **exponent** - Exponent value.

## float getFieldShorelineWaveExponent ( )

Returns the current nonlinearity of tidal waves frequency and movement speed.
### Return value

Exponent value.
## void setFieldShorelineWaveFrontExponent ( float exponent )

Sets the semi-transparency of the foam at an angle to the wind direction. Allows making the foam visible only on the windward side.
### Arguments

- *float* **exponent** - Exponent value.

## float getFieldShorelineWaveFrontExponent ( )

Returns the current semi-transparency of the foam at an angle to the wind direction. Allows making the foam visible only on the windward side.
### Return value

Exponent value.
## void setFieldShorelineFoamStretching ( float stretching )

Sets the width of the Shoreline LUT texture that creates a tidal wave.
### Arguments

- *float* **stretching** - Stretching value.

## float getFieldShorelineFoamStretching ( )

Returns the current width of the Shoreline LUT texture that creates a tidal wave.
### Return value

Stretching value.
## void setFieldShorelineFoamIntensity ( float intensity )

Sets the degree of foam intensity along the shoreline.
### Arguments

- *float* **intensity** - Intensity value.

## float getFieldShorelineFoamIntensity ( )

Returns the current degree of foam intensity along the shoreline.
### Return value

Intensity value.
## void setFieldShorelineFoamExponent ( float exponent )

Sets the visibility of the foam texture pattern.
### Arguments

- *float* **exponent** - Exponent value.

## float getFieldShorelineFoamExponent ( )

Returns the current visibility of the foam texture pattern.
### Return value

Exponent value.
## void setFieldShorelineMaskTiling ( float tiling )

Sets a size of the foam procedural pattern used to reduce the foam tiling effect when seen from above.
### Arguments

- *float* **tiling** - Tiling value.

## float getFieldShorelineMaskTiling ( )

Returns the current size of the foam procedural pattern used to reduce the foam tiling effect.
### Return value

Tiling value.
## void setFieldShorelineBeaufortFalloff ( float falloff )

Sets the Beaufort falloff value that provides height control of main geometry waves near the shoreline.
### Arguments

- *float* **falloff** - Falloff value.

## float getFieldShorelineBeaufortFalloff ( )

Returns the current Beaufort falloff value that provides height control of main geometry waves near the shoreline.
### Return value

Falloff value.
## void setShorelineWetnessIntensity ( float intensity )

Sets the intensity of the wetness effect along the shoreline.
### Arguments

- *float* **intensity** - Wetness intensity value.

## float getShorelineWetnessIntensity ( )

Returns the current intensity of the wetness effect along the shoreline.
### Return value

Wetness intensity value.
## void setShorelineWetnessDistance ( float distance )

Sets the spread of the wetness area along the shoreline.
### Arguments

- *float* **distance** - Wetness distance value, in units.

## float getShorelineWetnessDistance ( )

Returns the current spread of the wetness area along the shoreline.
### Return value

Wetness distance value, in units.
## void setShorelineWetnessOffset ( float offset )

Sets the offset of the wetness area from the water.
### Arguments

- *float* **offset** - Wetness offset value, in units.

## float getShorelineWetnessOffset ( )

Returns the current offset of the wetness area from the water.
### Return value

Wetness offset value, in units.
## void setAuxiliaryColor ( vec4 color )

Sets the color that goes into the auxiliary buffer. *Alpha* is the blend factor.
### Arguments

- *vec4* **color** - Auxiliary color.

## vec4 getAuxiliaryColor ( )

Returns the current color that goes into the auxiliary buffer.
### Return value

Auxiliary color.
## void setRefractionScale ( float scale )

Sets the scale of the [water refraction](../../../objects/objects/water/water_object.md#refraction_scale).
### Arguments

- *float* **scale** - Refraction scale value.

## float getRefractionScale ( )

Returns the current scale of the [water refraction](../../../objects/objects/water/water_object.md#refraction_scale).
### Return value

Refraction scale value.
## void setDecalsDistortion ( float distortion )

Distortion of [decals](../../../objects/decals/index.md) projected onto water.
### Arguments

- *float* **distortion** - Distortion value.

## float getDecalsDistortion ( )

Returns the current distortion of [decals](../../../objects/decals/index.md) projected onto water.
### Return value

Distortion value.
## void setDecalsSoftInteraction ( float interaction )

Sets a new soft intersection of water with decals.
### Arguments

- *float* **interaction** - Soft intersection value.

## float getDecalsSoftInteraction ( )

Returns the current soft intersection of water with decals.
### Return value

Soft intersection value.
## void setFieldHeightSteepness ( float steepness )

Sets the sharpness of the crests for the waves generated from the [FieldHeight](../../../objects/effects/fields/field_height/index.md) objects placed in Global Water.
### Arguments

- *float* **steepness** - Steepness value.

## float getFieldHeightSteepness ( )

Returns the current sharpness of the crests for the waves generated from the [FieldHeight](../../../objects/effects/fields/field_height/index.md) objects placed in Global Water.
### Return value

Steepness value.
## void setUnderwaterDOF ( int underwaterdof )

Enables/disables the [underwater DOF](../../../objects/objects/water/water_object.md#underwater_dof) effect.
### Arguments

- *int* **underwaterdof** - **1** to enable underwater DOF effect, **0** to disable it.

## int isUnderwaterDOF ( )

Returns a value indicating if the [underwater DOF](../../../objects/objects/water/water_object.md#underwater_dof) effect is enabled.
### Return value

**1** if underwater DOF effect is enabled, otherwise, **0**.
## void setPlanarReflection ( int reflection )

Enables/disables the use of planar reflections on the water surface instead of SSR. It is better to use this option for undisturbed water (0-2 Beaufort). Enabling the option activates [Planar Reflection MapSize](../../../api/library/objects/class.objectwaterglobal_usc.md#setPlanarReflectionMapSizeType_int_void) and Planar Reflection parameters.
### Arguments

- *int* **reflection** - **1** to enable planar reflections, **0** to disable them.

## int isPlanarReflection ( )

Returns a value indicating if the planar reflections option is enabled.
### Return value

**1** if planar reflections option is enabled, otherwise, **0**.
## void setPlanarReflectionMapSizeType ( int type )

Sets the size of the planar reflection map. The higher the value, the better the quality is.
### Arguments

- *int* **type** - Size of the planar reflection map.

## int getPlanarReflectionMapSizeType ( )

Returns the current size of the planar reflection map.
### Return value

Size of the planar reflection map.
## void setPlanarReflectionViewportMask ( int mask )

Sets the viewport [mask](../../../principles/bit_masking/index.md#viewport) of the reflection camera. A surface has its reflection rendered, if its viewport mask and its material's viewport mask match this mask.
### Arguments

- *int* **mask** - Viewport mask.

## int getPlanarReflectionViewportMask ( )

Returns the current viewport [mask](../../../principles/bit_masking/index.md#viewport) of the reflection camera. A surface has its reflection rendered, if its viewport mask and its material's viewport mask match this mask.
### Return value

Viewport mask.
## void setCaustics ( int caustics )

Enables/disables the effect of [light rays refraction](../../../objects/objects/water/water_object.md#enable_caustics) by the water surface.
### Arguments

- *int* **caustics** - **1** to enable the caustics, **0** to disable them.

## int isCaustics ( )

Returns a value indicating if the [caustics effect](../../../objects/objects/water/water_object.md#enable_caustics) is enabled.
### Return value

**1** if the caustics effect is enabled, otherwise, **0**.
## void setCausticsDistortion ( int distortion )

Enables/disables the [caustics distortion](../../../objects/objects/water/water_object.md#caustics_distortion) option. This effect removes pixelation and makes caustics look smoother. When smoothing is not required, you can disable this option to gain performance.
### Arguments

- *int* **distortion** - **1** to enable caustics distortion, **0** to disable it.

## int isCausticsDistortion ( )

Returns a value indicating if the [caustics distortion](../../../objects/objects/water/water_object.md#caustics_distortion) effect is enabled.
### Return value

**1** if caustics distortion is enabled, otherwise, **0**.
## void setFieldShorelineEnabled ( int enabled )

Enables/disables the effect of the [FieldShoreline](../../../objects/effects/fields/field_shoreline/index.md) object on the Global Water object. Enabling this option makes available the group of Field Shoreline states.
### Arguments

- *int* **enabled** - **1** to enable FieldShoreline, **0** to disable it.

## int isFieldShorelineEnabled ( )

Checks if the assigned material on the Global Water object has enabled [FieldShoreline](../../../objects/effects/fields/field_shoreline/index.md) interaction option.
### Return value

**1** if the FieldShoreline interaction option is enabled, otherwise, **0**.
## void setFieldShorelineHighPrecision ( int precision )

Enables/disables [improved interpolation](../../../objects/objects/water/water_object.md#high_precision) between the adjacent pixels of the shoreline texture to reduce stepping artifacts. This can be noticed when looking at the waterline separating overwater and underwater. This option should be used only when [geometry](../../../api/library/objects/class.objectwaterglobal_usc.md#setFieldShorelineGeometry_int_void) and/or [normal](../../../api/library/objects/class.objectwaterglobal_usc.md#setFieldShorelineNormal_int_void) states are enabled.
### Arguments

- *int* **precision** - **1** to enable high precision, **0** to disable it.

## int isFieldShorelineHighPrecision ( )

Returns a value indicating if the [high precision](../../../objects/objects/water/water_object.md#high_precision) of the shoreline is enabled. If enabled, this option improves interpolation between the adjacent pixels of the shoreline texture to reduce stepping artifacts.
### Return value

**1** if high precision is enabled, otherwise, **0**.
## void setFieldShorelineNormal ( int normal )

Enables/disables calculation of normals for geometry of shoreline waves. This option significantly reduces performance and can be used in cases, when really large waves are required. Enabling just the [geometry](../../../api/library/objects/class.objectwaterglobal_usc.md#setFieldShorelineGeometry_int_void) state to simulate distortion of the water surface by a shoreline wave is enough in most cases.
### Arguments

- *int* **normal** - **1** to enable, **0** to disable.

## int isFieldShorelineNormal ( )

Returns a value indicating if calculation of normals for geometry of shoreline waves is enabled.
### Return value

**1** if enabled, otherwise, **0**.
## void setFieldShorelineGeometry ( int geometry )

Enables/disables [rendering of wave geometry](../../../objects/objects/water/water_object.md#fieldshoreline_geometry) for shoreline waves. If disabled, the water surface remains flat. Disabling this option in cases where wave geometry is hardly noticeable (e.g. a flight simulator) gives a performance gain.
### Arguments

- *int* **geometry** - **1** to enable, **0** to disable.

## int isFieldShorelineGeometry ( )

Returns a value indicating if [rendering of wave geometry](../../../objects/objects/water/water_object.md#fieldshoreline_geometry) for shoreline waves is enabled.
### Return value

**1** if enabled, otherwise, **0**.
## void setFieldShorelineFoam ( int foam )

Enables/disables [rendering of foam](../../../objects/objects/water/water_object.md#fieldshoreline_foam) for shoreline zones.
### Arguments

- *int* **foam** - **1** to enable, **0** to disable.

## int isFieldShorelineFoam ( )

Returns a value indicating if [rendering of foam](../../../objects/objects/water/water_object.md#fieldshoreline_foam) for shoreline zones is enabled.
### Return value

**1** if enabled, otherwise, **0**.
## void setAuxiliary ( int auxiliary )

Enables/disables the [auxiliary rendering pass](../../../objects/objects/water/water_object.md#auxiliary) for the material. Can be used for custom post-effects, such as thermal vision, night vision, etc. Enabling the option activates the [Auxiliary Color](../../../api/library/objects/class.objectwaterglobal_usc.md#setAuxiliaryColor_vec4_void) parameter.
### Arguments

- *int* **auxiliary** - **1** to enable, **0** to disable.

## int isAuxiliary ( )

Returns a value indicating if the auxiliary rendering pass for the material is enabled.
### Return value

**1** if enabled, otherwise, **0**.
## void setFieldHeightEnabled ( int enabled )

Enables/disables the effect of [FieldHeight](../../../objects/effects/fields/field_height/index.md) object on the Global Water object.
### Arguments

- *int* **enabled** - **1** to enable, **0** to disable.

## int isFieldHeightEnabled ( )

Checks if the assigned material on the Global Water object has enabled [FieldHeight](../../../objects/effects/fields/field_height/index.md) interaction option.
### Return value

**1** if the FieldHeight interaction option is enabled, otherwise, **0**.
## void setFieldSpacerEnabled ( int enabled )

Enables/disables the effect of [FieldSpacer](../../../objects/effects/fields/field_spacer/index.md) object on the Global Water object.
### Arguments

- *int* **enabled** - **1** to enable, **0** to disable.

## int isFieldSpacerEnabled ( )

Returns a value indicating if the effect of [FieldSpacer](../../../objects/effects/fields/field_spacer/index.md) object on the Global Water object is enabled.
### Return value

**1** if enabled, otherwise, **0**.
## void setWavesSpeedScale ( float scale )

Sets a scale value that affects the speed of all the waves. The resulting wave speed is calculated as ***sqrt(gravity * 2 * pi / wave_length) * waves_speed_scale***, where *gravity* = 9.81 m/s2.
### Arguments

- *float* **scale** - Scale value.

## float getWavesSpeedScale ( )

Returns the current scale value that affects the speed of all the waves.
### Return value

Scale value.
