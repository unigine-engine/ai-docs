# ObjectWaterGlobal Class (CS)

**Inherits from:** Object


Interface for **[Global Water](../../../objects/objects/water/water_object.md)** object handling. This water object represents infinitely spread water with auto-tessellation (the wireframe of the water object is not scaled � regardless of the camera position it stays the same) and the underwater mode. This type is suitable to represent boundless ocean while not overloading the GPU.


However, it cannot have a body assigned, and thus does not provide proper physical interaction with scene objects. If you need to simulate the physics of buoyancy, you should use **[Physical Water](../../../objects/effects/physicals/physical_water/index.md)**. Also it is limited to a single water level. It means that the filling level of water always remains the same. So, if you need to create, for example, mountain lakes or water flows with height difference, you should use a **[Water Mesh](../../../objects/objects/water/water_mesh.md)**.


There are three options for creating waves:


- **Layer mode** � you create layers on which waves will be randomly generated in a given range of wave parameters. All the layers are added together. > **Notice:** Wave layers are usually created through the UnigineEditor, but you can also create and edit them via code.
- **Manual mode** � you create your own individual waves and have full control over them. This mode can only be set via code, you cannot do this in the UnigineEditor. > **Notice:** In **Manual mode**, be careful with the *Steepness* parameter, the waves will be everted if this value is set high.
- **Beauforts mode** � waves are generated based on the presets reproducing the state of the sea according to the Beaufort wind force scale (0 - Calm, 12 - Hurricane). In this mode, the parameters that define the main wave geometry will not be available for editing via code.


For all modes, wave frequency is calculated based on the wavelength using the formula:

 sqrt (*Gravity* * 2 * PI / *Wavelength*)
 where *Gravity* = 9.81 m/s2.
When you enable **Manual mode**, the list of the generated waves is cleared and you can set up your own waves.


When you save the world, the layers will be saved, but the user-defined waves will not, since they are created via code.


The maximum total number of waves is **256**. For better performance, we recommend using about **100**.


Here is how you can modify the *AppWorldLogic.cs* file to create waves in **Manual mode**:


<details>
<summary>AppWorldLogic.cs | Close</summary>

`AppWorldLogic.cs`


```csharp
ObjectWaterGlobal water = null;

/* ... */

private void Init()
{
	// Write here code to be called on world initialization: initialize resources for your world scene during the world start.

	// Changing preset to custom (4) and adjusting tesselation parameters
	Render.WaterGeometryPreset = 4;
	Render.WaterGeometryPolygonSize = 0.01f;
	Render.WaterGeometryProgression = 1.0f;
	Render.WaterGeometrySubpixelReduction = 6.0f;

	water = (ObjectWaterGlobal)World.GetNodeByType((int)Node.TYPE.OBJECT_WATER_GLOBAL);
	if (water == null)
	{
		water = new ObjectWaterGlobal();
	}

	// You can set each wave only in Manual mode
	water.WavesMode = ObjectWaterGlobal.WAVES_MODE.MANUAL;

	// add each wave.
	// addWave(wave length, amplitude, steepness, direction angle[0.0; 360.0], phase offset[0.0; 2*PI])

	water.AddWave(8.0f, 0.05f, 2.0f, 270.0f, 0.0f);
	water.AddWave(8.0f, 0.015f, 1.0f, 150.0f, 1.0f);
	water.AddWave(8.0f, 0.02f, 6.0f, 75.0f, 0.0f);
	water.AddWave(16.0f, 0.05f, 2.0f, 270.0f, 3.0f);
	water.AddWave(16.0f, 0.05f, 7.0f, 45.0f, 0.5f);
	water.AddWave(32.0f, 0.1f, 2.0f, 120.0f, 2.0f);
	water.AddWave(64.0f, 0.2f, 1.0f, -90.0f, 0.1f);

	// Changing amplitude and length for the second wave
	water.SetWaveAmplitude(1, 0.03f);
	water.SetWaveLength(1, 10.0f);

}

/* ... */


```

</details>


### Getting Water Level and Surface Normal


To ensure proper placement and orientation of objects relatively to the water surface you need to obtain water level (height) and normal orientation at a certain point. You can do this using the following methods:


- *[fetchHeight()](#fetchHeight_Vec3_float)*
- *[fetchNormal()](#fetchNormal_Vec3_vec3)*


By default the quality (precision) of calculating heights and normals is set to optimize performance, but in case of higher Beaufort levels (resulting in significant wave steepness and height differences on the water surface), calculation results may differ from visual representation (e.g. calculated water level may be greater the actual value). This may, for example, result in setting incorrect position and orientation for a ship relative to the water surface. To avoid such cases you can increase the quality of calculations for height/normal fetch requests via the following parameters are available via API:


- **Steepness Quality** *[FetchSteepnessQuality](../../...md#setFetchSteepnessQuality_int_void)* - wave steepness calculation accuracy used when calculating water level (height) and normal orientation at a certain point. This parameter is used to improve calculation results in case of high wave steepness (higher Beaufort levels). Low quality is usually sufficient for calm water (*high* quality provides good results for Beauforts 6-7, while *ultra* is recommended for Beauforts 8-10).
- **Amplitude Threshold** *[FetchAmplitudeThreshold](../../...md#setFetchAmplitudeThreshold_float_void)* - this is the minimum amplitude threshold for waves to be taken into account in height and normal calculations (waves having smaller amplitudes will be ignored).


> **Notice:** Using higher quality has an impact on performance, so we recommended to increase it only when necessary (when Beaufort levels are high) and set it back to the default level, when the water surface gets relatively calm.


So in case of higher Beaufort levels you can adjust the quality of intersections calculation using the following lines:


```csharp
water.FetchSteepnessQuality = ObjectWaterGlobal.STEEPNESS_QUALITY.ULTRA;
water.FetchAmplitudeThreshold = 0.01f;


```


### Finding Intersection Points


Intersections are used for many purposes, for example, you can find an intersection point of a projectile with the water surface to spawn some splashes. By default the quality (precision) of calculating intersection points is set to optimize performance, but in case of higher Beaufort levels (resulting in significant wave steepness and height differences on the water surface), calculation results may differ from visual representation (e.g. intersection point is detected at some distance from the water surface). This may, for example, result in spawning particle systems representing splashes at a wrong position. To avoid such cases you can increase the quality of calculations for intersection detection via the following parameters are available via API:


- **Precision** *[IntersectionPrecision](../../...md#setIntersectionPrecision_float_void)* - represents a permissible error between the calculated and real water intersection point.
- **Steepness Quality** *[IntersectionSteepnessQuality](../../...md#setIntersectionSteepnessQuality_int_void)* - wave steepness calculation accuracy used in intersection calculations. This parameter is used to improve calculation of intersections in case of high wave steepness (higher Beaufort levels). Low quality is usually sufficient for calm water (*high* quality provides good results for Beauforts 6-7, while *ultra* is recommended for Beauforts 8-10).
- **Amplitude Threshold** *[IntersectionAmplitudeThreshold](../../...md#setIntersectionAmplitudeThreshold_float_void)* - this is the minimum amplitude threshold for waves to be taken into account in intersection calculations (waves having smaller amplitudes will be ignored).


> **Notice:** Using higher quality has an impact on performance, so we recommended to increase it only when necessary (when Beaufort levels are high) and set it back to the default level, when the water surface gets relatively calm.


So in case of higher Beaufort levels you can adjust the quality of intersections calculation using the following lines:


```csharp
water.FetchSteepnessQuality = ObjectWaterGlobal.STEEPNESS_QUALITY.ULTRA;
water.FetchAmplitudeThreshold = 0.01f;


```


### Usage Example


This example demonstrates the influence of the **[Steepness Quality](#setFetchSteepnessQuality_int_void), [Amplitude Threshold](#setFetchAmplitudeThreshold_float_void)**, and **[Precision](#setIntersectionPrecision_float_void)** parameters on the accuracy of fetch and intersection requests for the *Global Water* object at various Beaufort levels.


[Create a new C# component](../../../code/usage/using_component_system/index.md#create_class) named **WaterFetchIntersection** and copy the code below to the corresponding file:


<details>
<summary>WaterFetchIntersection.cs | Close</summary>

`WaterFetchIntersection.cs`


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class WaterFetchIntersection : Component
{
	// Object Water Global node to perform requests for
	public Node water_node;

	// Fetch request mode flag (false - means Intersection request)
	private bool fetch = true;

	// size and number of points
	private int num_intersection = 100;
	private float intersect_point_size = 0.2f;

	//UI elements
	WidgetSlider slider_num_requests;
	WidgetSlider slider_beaufort;
	WidgetSlider slider_fetch_amplitude;
	WidgetSlider slider_fetch_stepness;
	WidgetSlider slider_intersection_amplitude;
	WidgetSlider slider_intersection_stepness;
	WidgetSlider slider_precision;

	// pointer to the Global Water object
	private ObjectWaterGlobal water;

	private WidgetWindow window;
	// UI construction for parameters
	// function creating a parameter and adding the corresponding UI element
	private WidgetSlider create_param(Widget parent, String name, float default_value, float min_value, float max_value, Func<float,int> f, bool floating)
	{
		WidgetLabel label = new WidgetLabel(name);
		label.Width = 100;
		parent.AddChild(label, Gui.ALIGN_LEFT);

		WidgetSlider slider = new WidgetSlider();
		slider.MinValue = MathLib.ToInt(min_value * (floating ? 1000 : 1));
		slider.MaxValue = MathLib.ToInt(max_value * (floating ? 1000 : 1));
		slider.Value = MathLib.ToInt(default_value * (floating ? 1000 : 1));

		slider.Width = 200;
		slider.ButtonWidth = 20;
		slider.ButtonHeight = 20;
		parent.AddChild(slider, Gui.ALIGN_LEFT);

		label = new WidgetLabel(default_value.ToString());
		label.Width = 20;
		parent.AddChild(label);

		slider.EventChanged.Connect(() =>
		{
			float v = slider.Value / (floating ? 1000.0f : 1.0f);
			label.Text = v.ToString();
			f(v);
		});

		return slider;
	}
	private void Init_GUI()
	{
		window = new WidgetWindow("Fetch and Intersection Water Parameters");
		Gui.GetCurrent().AddChild(window, Gui.ALIGN_OVERLAP);

		WidgetGroupBox group_box = new WidgetGroupBox("Parameters", 8, 8);
		window.AddChild(group_box, Gui.ALIGN_LEFT);

		WidgetHBox hbox = new WidgetHBox();
		group_box.AddChild(hbox, Gui.ALIGN_LEFT);
		WidgetLabel label = new WidgetLabel("Request Type");
		label.Width = 180;
		hbox.AddChild(label, Gui.ALIGN_LEFT);

		WidgetButton fetch_b = new WidgetButton("Fetch");
		hbox.AddChild(fetch_b, Gui.ALIGN_LEFT);
		fetch_b.Toggleable = true;
		fetch_b.Toggled = fetch;
		WidgetButton intersection_b = new WidgetButton("Intersection");
		hbox.AddChild(intersection_b, Gui.ALIGN_LEFT);
		intersection_b.Toggleable = true;
		intersection_b.Toggled = !fetch;

		fetch_b.EventChanged.Connect(()=>
		{
			fetch = fetch_b.Toggled;
			intersection_b.Toggled = !fetch;
		}
		);
		intersection_b.EventChanged.Connect(()=>
		{
			fetch = !intersection_b.Toggled;
			fetch_b.Toggled = fetch;
		}
		);
		WidgetGridBox grid = new WidgetGridBox(3);
		group_box.AddChild(grid);

		// number of fetch/intersection requests slider
		slider_num_requests = create_param(grid, "Request Count", num_intersection, 100, 10000, (v) => { num_intersection = MathLib.ToInt(v); return 1;}, false);

		// Beaufort level slider
		slider_beaufort = create_param(grid, "Beaufort", 0, 0, 13, (v) => { water.Beaufort = v; return 1;}, true);

		for (int i = 0; i < 3; i++)
		{
			WidgetSpacer s = new WidgetSpacer();
			grid.AddChild(s);
			s.Orientation = 1;
		}

		// sliders controlling quality parameters for fetch requests
		slider_fetch_amplitude = create_param(grid, "Fetch Amplitude Threshold", water.FetchAmplitudeThreshold, 0.001f, 0.5f, (v) => { water.FetchAmplitudeThreshold = v; return 1;}, true);
		slider_fetch_stepness = create_param(grid, "Fetch Steepness Quality", (float) water.FetchSteepnessQuality, 0, 4, (v) => { water.FetchSteepnessQuality = (ObjectWaterGlobal.STEEPNESS_QUALITY) MathLib.RoundToInt(v); return 1;}, false);

		for (int i = 0; i < 3; i++)
		{
			WidgetSpacer s = new WidgetSpacer();
			grid.AddChild(s);
			s.Orientation = 1;
		}

		// sliders controlling quality and precision parameters for intersection requests
		slider_intersection_amplitude = create_param(grid, "Intersection Amplitude Threshold", water.IntersectionAmplitudeThreshold, 0.001f, 0.5f, (v) => { water.IntersectionAmplitudeThreshold = v; return 1;}, true);
		slider_intersection_stepness = create_param(grid, "Intersection Steepness Quality", (float) water.IntersectionSteepnessQuality, 0, 4, (v) => { water.IntersectionSteepnessQuality = (ObjectWaterGlobal.STEEPNESS_QUALITY) MathLib.RoundToInt(v); return 1;}, false);
		slider_precision = create_param(grid, "Intersection Precision", water.IntersectionPrecision, 0.01f, 2.0f, (v) => { water.IntersectionPrecision = v; return 1;}, true);
	}

	private void Shutdown_GUI()
	{
		window.DeleteLater();
	}

	private void Init()
	{
		// write here code to be called on component initialization
		water = water_node as ObjectWaterGlobal;
		Visualizer.Enabled = true;
		Init_GUI();
	}

	private void Update()
	{
		// calculating the number of fetch/intersection points along X and Y axes
		int count = MathLib.ToInt(MathLib.Sqrt(num_intersection));

		// creating an object to store intersection data
		ObjectIntersectionNormal oin = new ObjectIntersectionNormal();

		// looping over all points to perform fetch/intersection requests with the current settings
		for (int i = 0; i < count; i++)
		{
			for (int j = 0; j < count; j++)
			{
				vec3 pos = new vec3(i, j, 0);
				if (fetch)
				{
					// getting Global Water height data  and the point and displaying it
					float v = water.FetchHeight(pos);
					pos.z += v;
					Visualizer.RenderPoint3D(pos, intersect_point_size, vec4.BLUE);

					// getting and displaying normals at fetch points
					vec3 n = water.FetchNormal(pos);
					Visualizer.RenderVector(pos, pos + new vec3(n), vec4.WHITE);
				}
				else
				{
					// getting and displaying normals at intersection points
					if (water.GetIntersection(pos + vec3.UP * 100, pos - vec3.UP * 100, oin, 0))
					{
						Visualizer.RenderPoint3D(oin.Point, intersect_point_size, vec4.GREEN);
						Visualizer.RenderVector(oin.Point, oin.Point + new vec3(oin.Normal), vec4.WHITE);
					}

				}
			}
		}
	}

	private void Shutdown()
	{
		Shutdown_GUI();
	}
}

```

</details>


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

### Enums

## WAVES_MODE

| Name | Description |
|---|---|
| **MANUAL** = 0 | Manual mode of wave generation. |
| **LAYERS** = 1 | Layer mode of wave generation. |
| **BEAUFORTS** = 2 | Beaufort scale mode of wave generation. |

## STEEPNESS_QUALITY

Steepness calculation accuracy used when calculating intersections, as well as fetching water level (height) and normal orientation at a certain point. This parameter is used to improve calculation results in case of high wave steepness (higher Beaufort levels). Low quality is usually sufficient for calm water (*high* quality provides good results for Beauforts 6-7, while *ultra* is recommended for Beauforts 8-10, if you're still not satisfied with the result you can use *extreme*).
| Name | Description |
|---|---|
| **LOW** = 0 | Default. Low quality of wave steepness calculation. |
| **MEDIUM** = 1 | Medium quality of wave steepness calculation. |
| **HIGH** = 2 | High quality of wave steepness calculation. |
| **ULTRA** = 3 | Ultra quality of wave steepness calculation. |
| **EXTREME** = 4 | Extreme quality of wave steepness calculation. Significantly affects performance. |

## PLANAR_REFLECTION_SIZE

| Name | Description |
|---|---|
| **RESOLUTION_128** = 0 | Reflection image with 128x128 resolution. |
| **RESOLUTION_256** = 1 | Reflection image with 256x256 resolution. |
| **RESOLUTION_512** = 2 | Reflection image with 512x512 resolution. |
| **RESOLUTION_1024** = 3 | Reflection image with 1024x1024 resolution. |
| **RESOLUTION_2048** = 4 | Reflection image with 2048x2048 resolution. |
| **RESOLUTION_4096** = 5 | Reflection image with 4096x4096 resolution. |
| **RESOLUTION_HEIGHT_QUART** = 6 | Reflection image with the resolution *height/4* x *height/4*, where height is an application window height. |
| **RESOLUTION_HEIGHT_HALF** = 7 | Reflection image with the resolution *height/2* x *height/2*, where height is an application window height. |
| **RESOLUTION_HEIGHT** = 8 | Reflection image with the resolution *height* x *height*, where height is an application window height. |

### Properties

## bool FieldSpacerEnabled

The value indicating if the effect of [FieldSpacer](../../../objects/effects/fields/field_spacer/index.md) object on the Global Water object is enabled.
## float SoftInteraction

The soft intersection of water with the shoreline and surfaces of objects.
## float DecalsSoftInteraction

The soft intersection of water with decals.
## float DecalsDistortion

The distortion of [decals](../../../objects/decals/index.md) projected onto water.
## float RefractionScale

The scale of the [water refraction](../../../objects/objects/water/water_object.md#refraction_scale).
## vec4 AuxiliaryColor

The color that goes into the auxiliary buffer. *Alpha* is the blend factor.
## bool Auxiliary

The value indicating if the [auxiliary rendering pass](../../../objects/objects/water/water_object.md#auxiliary) for the material is enabled. Can be used for custom post-effects, such as thermal vision, night vision, etc. Enabling the option activates the [Auxiliary Color](../../../api/library/objects/class.objectwaterglobal_cs.md#setAuxiliaryColor_vec4_void) parameter.
## float ShorelineWetnessOffset

The offset of the wetness area from the water.
## float ShorelineWetnessDistance

The spread of the wetness area along the shoreline.
## float ShorelineWetnessIntensity

The intensity of the wetness effect along the shoreline.
## float FieldShorelineBeaufortFalloff

The Beaufort falloff value that provides height control of main geometry waves near the shoreline.
## float FieldShorelineMaskTiling

The size of the foam procedural pattern used to reduce the foam tiling effect.
## float FieldShorelineFoamExponent

The visibility of the foam texture pattern.
## float FieldShorelineFoamIntensity

The degree of foam intensity along the shoreline.
## float FieldShorelineFoamStretching

The width of the Shoreline LUT texture that creates a tidal wave.
## float FieldShorelineWaveFrontExponent

The semi-transparency of the foam at an angle to the wind direction. Allows making the foam visible only on the windward side.
## float FieldShorelineWaveExponent

The nonlinearity of tidal waves frequency and movement speed.
## float FieldShorelineWaveFalloff

The visibility gradient of waves coming from sea to the shore.
## float FieldShorelineWaveHeight

The height of oncoming tidal waves.
## float FieldShorelineWaveTiling

The frequency of tidal waves.
## float FieldShorelineWaveSpeed

The speed of tidal waves.
## string FieldShorelineLUTTexturePath

The path to the LUT texture used for shoreline wetness effect.
## bool FieldShorelineFoam

The value indicating if [rendering of foam](../../../objects/objects/water/water_object.md#fieldshoreline_foam) for shoreline zones is enabled.
## bool FieldShorelineGeometry

The value indicating if [rendering of wave geometry](../../../objects/objects/water/water_object.md#fieldshoreline_geometry) for shoreline waves is enabled. If disabled, the water surface remains flat. Disabling this option in cases where wave geometry is hardly noticeable (e.g. a flight simulator) gives a performance gain.
## bool FieldShorelineNormal

The value indicating if calculation of normals for [geometry](../../../api/library/objects/class.objectwaterglobal_cs.md#setFieldShorelineGeometry_int_void) of shoreline waves is enabled. This option significantly reduces performance and can be used in cases, when really large waves are required. Enabling just the geometry state to simulate distortion of the water surface by a shoreline wave is enough in most cases.
## bool FieldShorelineHighPrecision

The value indicating if the [high precision](../../../objects/objects/water/water_object.md#high_precision) of the shoreline is enabled. If enabled, this option improves interpolation between the adjacent pixels of the shoreline texture to reduce stepping artifacts. This can be noticed when looking at the waterline separating overwater and underwater. This option should be used only when [geometry](../../../api/library/objects/class.objectwaterglobal_cs.md#setFieldShorelineGeometry_int_void) and/or [normal](../../../api/library/objects/class.objectwaterglobal_cs.md#setFieldShorelineNormal_int_void) states are enabled.
## bool FieldShorelineEnabled

The value indicating if the assigned material on the Global Water object has enabled [FieldShoreline](../../../objects/effects/fields/field_shoreline/index.md) interaction option. Enabling this option makes available the group of Field Shoreline states.
## float FieldHeightSteepness

The sharpness of the crests for the waves generated from the [FieldHeight](../../../objects/effects/fields/field_height/index.md) objects placed in Global Water.
## float FieldHeightFoamIntensity

The intensity of the foam generated from the [FieldHeight](../../../objects/effects/fields/field_height/index.md) objects placed in Global Water.
## float FieldHeightFoamContrast

The contrast of the foam generated from the [FieldHeight](../../../objects/effects/fields/field_height/index.md) objects placed in Global Water.
## bool FieldHeightEnabled

The value indicating if the assigned material on the Global Water object has enabled [FieldHeight](../../../objects/effects/fields/field_height/index.md) interaction option.
## float CausticBrightness

The brightness of the light shapes.
## float CausticAnimationSpeed

The movement speed of the light patterns.
## float CausticDistanceFade

The [distance from the water surface](../../../objects/objects/water/water_object.md#caustics_distance_fade) downwards, at which light shapes fade.
## vec4 CausticUVTransform

The [UV Transform](../../../objects/objects/water/water_object.md#caustics_uv_transform) coordinates for the caustic texture.
## string CausticsTexturePath

The path to the [3D Caustic texture](../../../objects/objects/water/water_object.md#caustics_texture) which determines the [pattern of light rays](../../../objects/objects/water/water_object.md#enable_caustics) refracted by the water surface. The texture is 1-channeled: *R* value defines the caustics pattern.
## bool CausticsDistortion

The value indicating if the [caustics distortion](../../../objects/objects/water/water_object.md#caustics_distortion) effect is enabled. This effect removes pixelation and makes caustics look smoother. When smoothing is not required, you can disable this option to gain performance.
## bool Caustics

The value indicating if the [caustics effect](../../../objects/objects/water/water_object.md#enable_caustics) is enabled.
## float ReflectionOcclusionSlope

The slope of negative normals of the water surface, at which occlusion is performed for wave reflections.
## float ReflectionOcclusion

The [occlusion factor for environment reflections](../../../objects/objects/water/water_object.md#occlusion) on parts of the water surface with negative normals. The higher the value, the less intensive reflections are on the surface parts with negative normals. Using this parameter enables simulation of reflection of waves on the water surface removing too bright areas on waves close to the horizon.
## float ReflectionRoughness

The environment [reflection roughness](../../../objects/objects/water/water_object.md#roughness) of the water surface. The value is used for shading of the water surface: the higher the value, the more blurred environment reflections are; [planar reflections](../../../objects/objects/water/water_object.md#planar_reflection_toggle) are blurred and attenuated by this value as well. When waves are generated in the [Beauforts mode](../../../objects/objects/water/water_object.md#beauforts_mode), this parameter is driven by the Beaufort preset automatically and cannot be changed manually.
## int PlanarReflectionViewportMask

The viewport [mask](../../../principles/bit_masking/index.md#viewport) of the reflection camera. A surface has its reflection rendered, if its viewport mask and its material's viewport mask match this mask.
## vec3 PlanarReflectionPivotOffset

The position of the reflection pivot point.
## float PlanarReflectionDistance

The distance from the reflection viewport camera to the reflected object. This distance sums up to the distance from the camera to the reflective surface plus the distance from object to reflective surface.
## ObjectWaterGlobal.PLANAR_REFLECTION_SIZE PlanarReflectionMapSizeType

The size of the planar reflection map. The higher the value, the better the quality is.
## bool PlanarReflection

The value indicating if the planar reflections option is enabled. When enabled, planar reflections are used on the water surface instead of SSR. It is better to use this option for undisturbed water (0-2 Beaufort). Enabling the option activates [Planar Reflection MapSize](../../../api/library/objects/class.objectwaterglobal_cs.md#setPlanarReflectionMapSizeType_int_void) and Planar Reflection parameters.
## float UnderwaterDofDistance

The focal distance for the [underwater DOF effect](../../../objects/objects/water/water_object.md#underwater_dof).
## bool UnderwaterDOF

The value indicating if the [underwater DOF](../../../objects/objects/water/water_object.md#underwater_dof) effect enabled.
## float WaterlineSize

The [size of the borderline](../../../objects/objects/water/water_object.md#waterline_size) between the overwater and underwater environments.
## float UnderwaterShaftIntensity

The intensity of the underwater sun shafts.
## float UnderwaterFogSunInfluence

The degree of impact of the sun lighting on the final underwater color.
## float UnderwaterFogEnvironmentInfluence

The degree of impact of the environment lighting on the final underwater color.
## float UnderwaterFogOffset

The height offset for lighting.
## float UnderwaterFogDepth

The [distance from the water surface](../../../objects/objects/water/water_object.md#fog_lighting_depth) up to which the light affects the underwater color.
## float UnderwaterFogTransparency

The [transparency of the underwater fog](../../../objects/objects/water/water_object.md#fog_transparency). The higher the value, the more transparent the underwater fog is.
## vec4 UnderwaterFogColor

The [underwater fog color](../../../objects/objects/water/water_object.md#fog_color). The Sun and Environment lighting affect this parameter to create the final underwater fog color.
## string DepthLUTTexturePath

The path to the [LUT texture](../../../objects/objects/water/water_object.md#depth_lut) that shows the color of the bottom.
## float SubsurfaceDecalsIntensity

The intensity of subsurface scattering of diffuse lighting for decals.
## float SubsurfaceWaveFoamIntensity

The intensity of [subsurface scattering near the foam areas](../../../objects/objects/water/water_object.md#intensity_around_foam).
## float SubsurfaceWaveIntensity

The intensity of [light rays passing through waves](../../../objects/objects/water/water_object.md#intensity_through_waves). The lower the value, the faster the light rays dissipate in water.
## float SubsurfaceAmbientIntensity

The [intensity of subsurface scattering](../../../objects/objects/water/water_object.md#ambient_intensity) for ambient lighting. The lower the value, the faster the light rays dissipate in water.
## vec4 SubsurfaceColor

The [water subsurface scattering (SSS) color](../../../objects/objects/water/water_object.md#color).
## float FoamTextureAffect

The visibility of the foam texture. It can be used to create additional effects, e.g., foam bubbles.
## float FoamContactIntensity

The foam intensity near shores or different objects in water.
## float FoamWindIntensity

The intensity for the foam generated based on the wind direction.
## float FoamWindContrast

The contrast for the foam generated based on the wind direction.
## float FoamWhitecapIntensity

The foam intensity on the white caps.
## float FoamWhitecapContrast

The foam contrast on the white caps.
## float FoamPeakIntensity

The foam intensity on the wave peaks.
## float FoamPeakContrast

The foam contrast on the wave peaks.
## float Foam1UVSpeed

The speed for the second sample of the foam texture.
## float Foam1UVScale

The UV scale for the second sample of the foam texture.
## float Foam0UVSpeed

The speed for the first sample of the foam texture.
## float Foam0UVScale

The UV scale for the first sample of the foam texture.
## string FoamTexturePath

The path to the [foam texture](../../../objects/objects/water/water_object.md#texture).
## float DistantWavesBlendMax

The value representing the maximum amount of [distant waves](../../../objects/objects/water/water_object.md#distant_waves) in the crossfade zone where the main geometry waves fade out and distant waves fade in.
## float DistantWavesBlendMin

The value representing the minimum amount of [distant waves](../../../objects/objects/water/water_object.md#distant_waves) in the crossfade zone where the main geometry waves fade out and distant waves fade in.
## float DistantWavesBlendDistanceEnd

The fade-in end distance for [distant waves](../../../objects/objects/water/water_object.md#distant_waves).
## float DistantWavesBlendDistanceStart

The fade-in start distance for [distant waves](../../../objects/objects/water/water_object.md#distant_waves).
## float DistantWavesIntensity

The intensity for [distant waves](../../../objects/objects/water/water_object.md#distant_waves).
> **Notice:** Unavailable for modes with Beaufort levels blending.

## vec4 DistantWavesUVTransform

The UV transform for the [distant waves](../../../objects/objects/water/water_object.md#distant_waves) normal map. The first two values (x, y) represent the scale texture coordinates along the X and Y axes. The third and forth (z, w) specify the speed of movement animation.
## string DistantWavesTexturePath

The path to the [normal map](../../../objects/objects/water/water_object.md#distant_waves_normal_map) of the distant waves.
## float Detail1Intensity

The intensity of the first sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
## vec2 Detail1UVSpeed

The speed of the second sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
## vec2 Detail1UVSize

The size of the second sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
## float Detail0Intensity

The intensity of the first sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
## vec2 Detail0UVSpeed

The speed of the first sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
## vec2 Detail0UVSize

The size of the first sample of the [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
## string DetailTexturePath

The path to the location of a [normal detail texture](../../../objects/objects/water/water_object.md#detail_normal_map).
## float TextureNormalIntensity

The intensity of procedurally generated normals. This affects the normals generated for [Field Height](../../../objects/effects/fields/field_height/index.md) and [Field Shoreline](../../../objects/effects/fields/field_shoreline/index.md).
## float TextureNormalBlur

The blurring ratio for the procedurally generated normals. This parameter enables you to reduce pixelation of the normal map, and make it less pronounced. It is recommended to use small values for correction, when necessary. This affects the normals generated for [Field Height](../../../objects/effects/fields/field_height/index.md) and [Field Shoreline](../../../objects/effects/fields/field_shoreline/index.md).
## float GeometryNormalIntensity

The intensity of normals of the waves.
## float Beaufort

The Beaufort wind force scale value, from 0 (Calm) to 12 (Hurricane). Available when the *Beauforts* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
## 🔒︎ int NumLayers

The number of wave layers. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
## 🔒︎ int NumWaves

The number of simulated waves. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
## ObjectWaterGlobal.WAVES_MODE WavesMode

The [wave generation mode](../../../objects/objects/water/water_object.md#creating_waves).
## 🔒︎ int VisualFieldMask

The FieldHeight visual mask of the assigned material on the Global Water.
## 🔒︎ int PhysicsFieldMask

The FieldHeight physics mask of the assigned material on the Global Water.
## ObjectWaterGlobal.STEEPNESS_QUALITY IntersectionSteepnessQuality

The wave steepness calculation quality used in [intersection calculations](#intersections).
## float IntersectionAmplitudeThreshold

The threshold of amplitude values that will not participate in [intersection calculations](#intersections).
## float IntersectionPrecision

The intersection precision which represents an error between the real value of the water intersection point and the calculated value. The default value is 0.25.
## ObjectWaterGlobal.STEEPNESS_QUALITY FetchSteepnessQuality

The wave steepness calculation quality used in [height and normal calculations](#fetch). Low quality is usually sufficient for calm water and large floating objects. If the waves are big, or you want to simulate small floating objects, you may need to increase the quality. Higher quality gives a more precise result but affects performance. The default is [STEEPNESS_QUALITY_LOW](../../../api/library/objects/class.objectwaterglobal_cs.md#STEEPNESS_QUALITY_LOW).
## float FetchAmplitudeThreshold

The threshold for amplitude values that will not participate in [height and normal calculations](#fetch). The more you cut off, the less accurate the height value you get, but the faster are the calculations. The default value is 0.1f.
## float WavesSpeedScale

The scale value that affects the speed of all the waves. The resulting wave speed is calculated as ***sqrt(gravity * 2 * pi / wave_length) * waves_speed_scale***, where *gravity* = 9.81 m/s2.
## float WindAffect

The value determining how much the wind direction affects the waves, in range [0;1]. If you set it to 1, all waves will be directed along the wind direction.
## float WindDirectionAngle

The angle that determines the wind direction.
## 🔒︎ float MeanLevel

The average Z coordinate of the water object.
## float AnimationTime

The water animation time value for water synchronization. It is used for effects, such as normals, caustics, and foam.
## bool ActiveWater

The value indicating if the global water object is active. If there are more than one global water nodes in the scene, only the active one will be rendered.
## 🔒︎ uint BackfaceMaterialID

The runtime material ID of the internal backface material of the water. The engine inherits a hidden material from the assigned water material to represent the back (underwater) side of the water surface with its own material mask and feature bits; pixels showing the water backface reference this ID. If the backface material does not exist, *[MATERIAL_ID_NONE](../../../api/library/rendering/class.material_cs.md#MATERIAL_ID_NONE)* is returned.
### Members

---

## ObjectWaterGlobal ( )

Constructor. Creates a new global water object.
## void SetLayerName ( int layer , string value )

Sets a new name for the wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number
- *string* **value** - Name of the layer.

## string GetLayerName ( int layer )

Returns the name of the wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number

### Return value

Name of the layer
## void SetLayerWeight ( int layer , float value )

Sets a weight for a given wave layer. This value determines how much the given layer affects the final wave form. It can be used for smooth transitions between the states of water. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number
- *float* **value** - Layer weight

## float GetLayerWeight ( int layer )

Returns the current weight of the wave layer. This value determines how much the given layer affects the final wave form. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number

### Return value

Weight of the layer.
## void SetLayerDirectionAngleVariance ( int layer , float value )

Sets a variance value of the wave direction angle for a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number
- *float* **value** - Variance value.

## float GetLayerDirectionAngleVariance ( int layer )

Returns the current variance value of the wave direction angle for a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number

### Return value

Variance value.
## void SetLayerSteepnessScale ( int layer , float value )

Sets a [steepness scale](../../../objects/objects/water/water_object.md#steepness_scale) value for a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number
- *float* **value** - Steepness scale value.

## float GetLayerSteepnessScale ( int layer )

Returns the current [steepness scale](../../../objects/objects/water/water_object.md#steepness_scale) value for a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number

### Return value

Steepness scale value.
## void SetLayerAmplitudeRange ( int layer , vec2 value )

Sets a range of wave amplitudes for a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number.
- *vec2* **value** - Amplitude range.

## vec2 GetLayerAmplitudeRange ( int layer )

Returns the current range of wave amplitudes of a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number.

### Return value

Amplitude range.
## void SetLayerLengthRange ( int layer , vec2 value )

Sets a range of wave lengths for a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number
- *vec2* **value** - Length range.

## vec2 GetLayerLengthRange ( int layer )

Returns the current range of wave lengths of a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number

### Return value

Length range.
## void SetLayerNumWaves ( int layer , int num )

Sets the number of waves for a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number
- *int* **num** - Number of waves.

## int GetLayerNumWaves ( int layer )

Returns the number of waves on a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number

### Return value

Number of waves.
## bool IsLayerEnabled ( int layer )

Returns a value indicating if a given wave layer is enabled. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number

### Return value

true if the layer is enabled; otherwise, false.
## void SetLayerEnabled ( int layer , bool enabled )

Enables or disables a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number
- *bool* **enabled** - true to enable the layer, false to disable it.

## void SwapLayer ( int num_0 , int num_1 )

Swaps two specified wave layers. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **num_0** - Layer1 number.
- *int* **num_1** - Layer2 number.

## void RemoveLayer ( int layer )

Removes a given wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **layer** - Layer number

## int AddLayer ( )

Appends a new wave layer. Available when the *Layers* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Return value

Number of the new added layer.
## void SetWavePhaseOffset ( int index , float value )

Sets the phase offset parameter for a given wave. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.
- *float* **value** - Phase offset parameter value in radians in range [0; 2pi].

## float GetWavePhaseOffset ( int index )

Returns the value of the Phase Offset parameter of a wave. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.

### Return value

Phase offset parameter value in radians in range [0; 2pi].
## void SetWaveDirectionAngle ( int index , float value )

Sets direction (angle of spreading) for a given wave:
- If 0 is specified, the wave spreads along the Y axis and is parallel to the X axis.
- If a positive value is specified, the wave direction is slanted counterclockwise relative to its initial spread.
- If a negative value is specified, the wave is rotated clockwise.


Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).


### Arguments

- *int* **index** - Wave number.
- *float* **value** - Angle, in degrees. Both positive and negative values are acceptable.

## float GetWaveDirectionAngle ( int index )

Returns direction (angle of spreading) of a given wave. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.

### Return value

Angle, in degrees.
## void SetWaveSteepness ( int index , float value )

Sets the steepness value for a given wave. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.
- *float* **value** - Steepness value.

## float GetWaveSteepness ( int index )

Returns the current steepness value of the given wave. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.

### Return value

Steepness value.
## void SetWaveAmplitude ( int index , float value )

Sets the distance between the highest and the lowest peaks for a given wave. It sets the wave form along with the [setWaveLength()](#setWaveLength_int_float_void) function. The higher the value is, the higher the waves are. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.
- *float* **value** - Amplitude, in units.

## float GetWaveAmplitude ( int index )

Returns the distance between the highest and the lowest peaks for the given wave. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.

### Return value

Amplitude, in units.
## void SetWaveLength ( int index , float value )

Sets the distance between successive crests for a given wave. The higher the length value is, the broader the waves are. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.
- *float* **value** - Length, in units.

## float GetWaveLength ( int index )

Returns the distance between successive crests of the given wave. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.

### Return value

Length, in units.
## void RemoveWave ( int index )

Removes the wave having a specified number. Available when the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *int* **index** - Wave number.

## int AddWave ( float length , float amplitude , float steepness , float direction_angle , float phase )

Adds a wave if the *Manual* mode [is set](../../../api/library/objects/class.objectwaterglobal_cs.md#setWavesMode_int_void).
### Arguments

- *float* **length** - Wave length.
- *float* **amplitude** - Wave amplitude.
- *float* **steepness** - Wave steepness.
- *float* **direction_angle** - Angle of the wave direction in degrees. At 0 angle the wave will be directed along the X-axis.
- *float* **phase** - Phase offset of the wave in radians (0 to 2pi).

### Return value

Number of the added wave.
## static int type ( )

Returns the type of the node.
### Return value

[Object](../../../api/library/objects/class.object_cs.md) type identifier.
## float FetchHeight ( vec3 position )

Returns a height offset of the specified point relative to the current water level calculated at this point. E.g. in case the specified point is (0, 0, -3) and the current water level calculated for this point is equal to 5, the function shall return 8.


![](fetch.png)


> **Notice:** In case of higher Beaufort levels (resulting in significant wave steepness and height differences on the water surface), calculation results may differ from visual representation (e.g. calculated water level may be greater the actual value). To avoid it and increase precision, [adjust calculation quality](#fetch).

### Arguments

- *vec3* **position** - Point position coordinates.

### Return value

Height offset of the specified point relative to the current water level calculated at this point, in meters.
## vec3 FetchNormal ( vec3 position )

Returns a normal vector to the water surface at the specified point (to orient objects along the waves normals).
> **Notice:** In case of higher Beaufort levels (resulting in significant wave steepness and height differences on the water surface), calculation results may differ from visual representation (e.g. calculated water level may be greater the actual value). To avoid it and increase precision, [adjust calculation quality](#fetch).

### Arguments

- *vec3* **position** - Point position coordinates.

### Return value

Normal vector.
## void TakeSyncData ( Stream stream )

Writes wave synchronization data to the specified stream.
### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream to which wave synchronization data is to be written.

## void ApplySyncData ( Stream stream )

Reads wave synchronization data from the specified stream and applies it to the wave system.
### Arguments

- *[Stream](../../../api/library/common/class.stream_cs.md)* **stream** - Stream with wave synchronization data to be applied.
