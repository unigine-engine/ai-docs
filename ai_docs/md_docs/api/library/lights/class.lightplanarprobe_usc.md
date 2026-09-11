# Unigine::LightPlanarProbe Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Light


This class is used to create and manage [Planar Reflection Probes](../../../objects/lights/planar/index.md) the implement planar reflections functionality (used to create mirrors etc.). The probe grabs the reflection, and requires a surface to project the reflection onto. There is a set of parameters enabling you to tweak the look of your reflections and optimize rendering load (by limiting visibility distance, [reflections rendering distance](#setReflectionDistance_float_void), etc.).


## LightPlanarProbe Class

### Members

## void setProjectionSize ( vec3 size )

Sets a new size of the Light Planar Probe. Defines the box-shaped influence volume around the probe, in units, in which reflective surfaces (having the appropriate roughness values) shall use the results captured by the probe.
### Arguments

- *vec3* **size** - The size along X, Y and Z axes. The default value is (2.0f, 2.0f, 0.1f).

## vec3 getProjectionSize () const

Returns the current size of the Light Planar Probe. Defines the box-shaped influence volume around the probe, in units, in which reflective surfaces (having the appropriate roughness values) shall use the results captured by the probe.
### Return value

Current size along X, Y and Z axes. The default value is (2.0f, 2.0f, 0.1f).
## void setAttenuationDistance ( vec3 distance )

Sets a new attenuation distance that specifies how far the projection can reach any surfaces from the Probe position. It also specifies the attenuation area around the Probe at which the projection starts to fade out at the specified rate.
### Arguments

- *vec3* **distance** - The attenuation distance. The default value is (0.1f, 0.1f, 0.1f).

## vec3 getAttenuationDistance () const

Returns the current attenuation distance that specifies how far the projection can reach any surfaces from the Probe position. It also specifies the attenuation area around the Probe at which the projection starts to fade out at the specified rate.
### Return value

Current attenuation distance. The default value is (0.1f, 0.1f, 0.1f).
## void setRoughnessSamples ( int samples )

Sets a new number of samples used to adjust quality of the blurring effect for the reflection on rough surfaces.
### Arguments

- *int* **samples** - The number of blurring samples. The default value is 0.

## int getRoughnessSamples () const

Returns the current number of samples used to adjust quality of the blurring effect for the reflection on rough surfaces.
### Return value

Current number of blurring samples. The default value is 0.
## void setReflectionResolution ( int resolution )

Sets a new resolution of the reflection texture for the projection.
### Arguments

- *int* **resolution** - The reflection resolution. The default value is REFLECTION_RESOLUTION_MODE_HEIGHT.

## int getReflectionResolution () const

Returns the current resolution of the reflection texture for the projection.
### Return value

Current reflection resolution. The default value is REFLECTION_RESOLUTION_MODE_HEIGHT.
## void setTwoSided ( int sided )

Sets a new value indicating if the reflection is two-sided.
### Arguments

- *int* **sided** - The two-sided reflection

## int isTwoSided () const

Returns the current value indicating if the reflection is two-sided.
### Return value

Current two-sided reflection
## void setStereoPerEyeEnabled ( bool enabled )

Sets a new value indicating if rendering of the reflection for each eye separately is enabled.
### Arguments

- *bool* **enabled** - Set **true** to enable rendering of the reflection for each eye separately; **false** - to disable it.

## bool isStereoPerEyeEnabled () const

Returns the current value indicating if rendering of the reflection for each eye separately is enabled.
### Return value

**true** if rendering of the reflection for each eye separately is enabled ; otherwise **false**.
## void setDistanceScale ( float scale )

Sets a new distance multiplier for the reflection visibility distance. Distance Scale is applied to the distance measured from the reflection camera to the node (surface) bound.
### Arguments

- *float* **scale** - The distance scale multiplier for the reflection. The default value is 0.5f.

## float getDistanceScale () const

Returns the current distance multiplier for the reflection visibility distance. Distance Scale is applied to the distance measured from the reflection camera to the node (surface) bound.
### Return value

Current distance scale multiplier for the reflection. The default value is 0.5f.
## void setReflectionDistance ( float distance )

Sets a new rendering distance of the reflected projection that specifies how far the reflection is rendered from the camera.
### Arguments

- *float* **distance** - The reflection render distance in units. The default value is 100.0f.

## float getReflectionDistance () const

Returns the current rendering distance of the reflected projection that specifies how far the reflection is rendered from the camera.
### Return value

Current reflection render distance in units. The default value is 100.0f.
## void setReflectionViewportMask ( int mask )

Sets a new [reflection mask](../../../principles/bit_masking/index.md#reflection_mask) that controls rendering of the Planar Reflection Probe reflections into the reflection camera viewport.
### Arguments

- *int* **mask** - The reflection viewport mask (integer, each bit of which is used to represent a mask).

## int getReflectionViewportMask () const

Returns the current [reflection mask](../../../principles/bit_masking/index.md#reflection_mask) that controls rendering of the Planar Reflection Probe reflections into the reflection camera viewport.
### Return value

Current reflection viewport mask (integer, each bit of which is used to represent a mask).
## int getVisibilitySkipFlags () const

Returns the current mask that specifies what objects to ingore for the reflection projection.
### Return value

Current visibility bit mask (integer, each bit of which is used to represent a mask)
## void setZNear ( float znear )

Sets a new distance to the near clipping plane defining a frustum to be used for grabbing reflections.
### Arguments

- *float* **znear** - The distance to the near clipping plane. The default value is 0.01f.

## float getZNear () const

Returns the current distance to the near clipping plane defining a frustum to be used for grabbing reflections.
### Return value

Current distance to the near clipping plane. The default value is 0.01f.
## void setZFar ( float zfar )

Sets a new distance to the far clipping plane defining a frustum to be used for grabbing reflections.
### Arguments

- *float* **zfar** - The distance to the far clipping plane. The default value is 100.0f.

## float getZFar () const

Returns the current distance to the far clipping plane defining a frustum to be used for grabbing reflections.
### Return value

Current distance to the far clipping plane. The default value is 100.0f.
## void setReflectionVisibilityRoughnessMin ( float min )

Sets a new surface roughness value, starting from which the reflection starts to fade out gradually.
### Arguments

- *float* **min** - The minimum visibility roughness value. The default value is 0.0f.

## float getReflectionVisibilityRoughnessMin () const

Returns the current surface roughness value, starting from which the reflection starts to fade out gradually.
### Return value

Current minimum visibility roughness value. The default value is 0.0f.
## void setReflectionVisibilityRoughnessMax ( float max )

Sets a new surface roughness value, starting from which the reflection completely disappears.
### Arguments

- *float* **max** - The maximum visibility roughness value. The default value is 0.25f.

## float getReflectionVisibilityRoughnessMax () const

Returns the current surface roughness value, starting from which the reflection completely disappears.
### Return value

Current maximum visibility roughness value. The default value is 0.25f.
## void setVisibilitySky ( int sky )

Sets a new value indicating if rendering of the sky is enabled or disabled for the reflection.
### Arguments

- *int* **sky** - The rendering of the sky for the reflection

## int isVisibilitySky () const

Returns the current value indicating if rendering of the sky is enabled or disabled for the reflection.
### Return value

Current rendering of the sky for the reflection
## void setParallax ( float parallax )

Sets a new degree of reflection distortion. Distortion depends on an angle between the probe plane and the surface onto which the probe projects reflection. Increasing the value amplifies visual distortion as a result of increasing this angle.
### Arguments

- *float* **parallax** - The degree of reflection distortion within the range of [0;1].

## float getParallax () const

Returns the current degree of reflection distortion. Distortion depends on an angle between the probe plane and the surface onto which the probe projects reflection. Increasing the value amplifies visual distortion as a result of increasing this angle.
### Return value

Current degree of reflection distortion within the range of [0;1].
## void setNoiseIntensity ( float intensity )

Sets a new intensity of jitter for roughness samples that creates a noise effect on the reflection.
### Arguments

- *float* **intensity** - The intensity of reflection noisiness. The default value is 0.5f.

## float getNoiseIntensity () const

Returns the current intensity of jitter for roughness samples that creates a noise effect on the reflection.
### Return value

Current intensity of reflection noisiness. The default value is 0.5f.
## void setReflectionOffset ( float offset )

Sets a new reflection Z axis offset relative to the probe coordinate system.
### Arguments

- *float* **offset** - The reflection offset along Z axis in units. The default value is 0.01f.

## float getReflectionOffset () const

Returns the current reflection Z axis offset relative to the probe coordinate system.
### Return value

Current reflection offset along Z axis in units. The default value is 0.01f.
---

## LightPlanarProbe ( )

Constructor. Creates a new planar probe.
## static int type ( )

Returns the object node type.
