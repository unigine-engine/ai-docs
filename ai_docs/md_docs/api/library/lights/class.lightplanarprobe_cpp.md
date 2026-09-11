# Unigine::LightPlanarProbe Class (CPP)

**Header:** #include <UnigineLights.h>

**Inherits from:** Light


This class is used to create and manage [Planar Reflection Probes](../../../objects/lights/planar/index.md) the implement planar reflections functionality (used to create mirrors etc.). The probe grabs the reflection, and requires a surface to project the reflection onto. There is a set of parameters enabling you to tweak the look of your reflections and optimize rendering load (by limiting visibility distance, [reflections rendering distance](#setReflectionDistance_float_void), etc.).


### Usage Example


In the example below a *Planar Reflection Probe* is created along with a plane primitive. The surface of the primitive serves for projecting the reflection grabbed by the probe (the reflection is projected only within the area of intersection of the probe and the surface). Some parameters of the material assigned to the reflecting surface are also tweaked in order to provide the desired effect and match [roughness](#setReflectionVisibilityRoughnessMin_float_void) range (which enables rendering of reflections depending on surface roughness).


[Create](../../../principles/component_system/component_system_cpp/index.md#workflow) a new class named **PlanarReflector** and copy **.h** and **.cpp** files into respective files of a class. Then [assign](../../../principles/component_system/component_system_cpp/index.md#workflow) a property generated for your component to any desired node of the *Object* type, to see its albedo texture replaced by a new created image.


<details>
<summary>PlanarReflector.h | Close</summary>

```cpp
#pragma once
#include <UnigineComponentSystem.h>
#include <UnigineObjects.h>
#include <UnigineLights.h>

class PlanarReflector :
	public Unigine::ComponentBase
{
public:
	COMPONENT_DEFINE(PlanarReflector, Unigine::ComponentBase);
	COMPONENT_INIT(init);

private:
	// declaring a reflecting plane and a planar reflection probe
	Unigine::ObjectMeshDynamicPtr plane;
	Unigine::LightPlanarProbePtr planar_probe;
	void init();
};

```

</details>


<details>
<summary>PlanarReflector.cpp | Close</summary>

```cpp
#include "PlanarReflector.h"
#include <UniginePrimitives.h>
#include <UnigineObjects.h>
#include <UnigineLights.h>
REGISTER_COMPONENT(PlanarReflector);

using namespace Unigine;

void PlanarReflector::init()
{
	// creating a reflecting plane, onto which the reflection is to be projected by the probe
	plane = Primitives::createPlane(20, 20, 1);

	// creating a planar reflection probe of the same size
	planar_probe = LightPlanarProbe::create();
	planar_probe->setProjectionSize(Math::vec3(20, 20, 1));
	plane->rotate(-90.0f, 0.0f, 0.0f);
	plane->translate(0.0f, 5.0f, -5.0f);

	// putting the planar probe so that it covers the reflecting surface
	planar_probe->setTransform(plane->getTransform());

	// inheriting a new material from the one assigned
	// to the surface by default in order to tweak it
	// and set metalness and roughness values (metallic and polished)
	MaterialPtr plane_mat = plane->getMaterialInherit(0);
	plane_mat->setParameterFloat("metalness", 1.0f);
	plane_mat->setParameterFloat("roughness", 0.0f);

	// set the distance from the camera, up to which
	// the planar reflection will be visible
	planar_probe->setVisibleDistance(5.0f);
}

```

</details>


## LightPlanarProbe Class

### Enums

## REFLECTION_RESOLUTION

| Name | Description |
|---|---|
| **REFLECTION_RESOLUTION_MODE_HEIGHT** = 0 | Reflection texture size equals to the viewport height resolution. |
| **REFLECTION_RESOLUTION_MODE_HALF_HEIGHT** = 1 | Reflection texture size equals to half of the viewport height resolution. |
| **REFLECTION_RESOLUTION_MODE_QUART_HEIGHT** = 2 | Reflection texture size equals to the quarter of the viewport height resolution. |
| **REFLECTION_RESOLUTION_MODE_128** = 3 | Reflection texture size equals to 128x128 pixels. |
| **REFLECTION_RESOLUTION_MODE_256** = 4 | Reflection texture size equals to 256x256 pixels. |
| **REFLECTION_RESOLUTION_MODE_512** = 5 | Reflection texture size equals to 512x512 pixels. |
| **REFLECTION_RESOLUTION_MODE_1024** = 6 | Reflection texture size equals to 1024x1024 pixels. |
| **REFLECTION_RESOLUTION_MODE_2048** = 7 | Reflection texture size equals to 2048x2048 pixels. |
| **REFLECTION_RESOLUTION_MODE_4096** = 8 | Reflection texture size equals to 4096x4096 pixels. |

### Members

## void setProjectionSize ( const Math:: vec3 & size )

Sets a new size of the Light Planar Probe. Defines the box-shaped influence volume around the probe, in units, in which reflective surfaces (having the appropriate roughness values) shall use the results captured by the probe.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **size** - The size along X, Y and Z axes. The default value is (2.0f, 2.0f, 0.1f).

## Math:: vec3 getProjectionSize () const

Returns the current size of the Light Planar Probe. Defines the box-shaped influence volume around the probe, in units, in which reflective surfaces (having the appropriate roughness values) shall use the results captured by the probe.
### Return value

Current size along X, Y and Z axes. The default value is (2.0f, 2.0f, 0.1f).
## void setAttenuationDistance ( const Math:: vec3 & distance )

Sets a new attenuation distance that specifies how far the projection can reach any surfaces from the Probe position. It also specifies the attenuation area around the Probe at which the projection starts to fade out at the specified rate.
### Arguments

- *const  Math::[vec3](../../../api/library/math/class.vec3_cpp.md)&* **distance** - The attenuation distance. The default value is (0.1f, 0.1f, 0.1f).

## Math:: vec3 getAttenuationDistance () const

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
## void setReflectionResolution ( LightPlanarProbe::REFLECTION_RESOLUTION resolution )

Sets a new resolution of the reflection texture for the projection.
### Arguments

- *[LightPlanarProbe::REFLECTION_RESOLUTION](../../../api/library/lights/class.lightplanarprobe_cpp.md#REFLECTION_RESOLUTION)* **resolution** - The reflection resolution. The default value is REFLECTION_RESOLUTION_MODE_HEIGHT.

## LightPlanarProbe::REFLECTION_RESOLUTION getReflectionResolution () const

Returns the current resolution of the reflection texture for the projection.
### Return value

Current reflection resolution. The default value is REFLECTION_RESOLUTION_MODE_HEIGHT.
## void setTwoSided ( bool sided )

Sets a new value indicating if the reflection is two-sided.
### Arguments

- *bool* **sided** - Set **true** to enable two-sided reflection; **false** - to disable it.

## bool isTwoSided () const

Returns the current value indicating if the reflection is two-sided.
### Return value

**true** if two-sided reflection is enabled ; otherwise **false**.
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
## void setVisibilitySky ( bool sky )

Sets a new value indicating if rendering of the sky is enabled or disabled for the reflection.
### Arguments

- *bool* **sky** - Set **true** to enable rendering of the sky for the reflection; **false** - to disable it.

## bool isVisibilitySky () const

Returns the current value indicating if rendering of the sky is enabled or disabled for the reflection.
### Return value

**true** if rendering of the sky for the reflection is enabled ; otherwise **false**.
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
