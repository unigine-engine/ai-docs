# Unigine::LightPlanarProbe Class (CS)

**Inherits from:** Light


This class is used to create and manage [Planar Reflection Probes](../../../objects/lights/planar/index.md) the implement planar reflections functionality (used to create mirrors etc.). The probe grabs the reflection, and requires a surface to project the reflection onto. There is a set of parameters enabling you to tweak the look of your reflections and optimize rendering load (by limiting visibility distance, [reflections rendering distance](#setReflectionDistance_float_void), etc.).


### Usage Example


In the example below a *Planar Reflection Probe* is created along with a plane primitive. The surface of the primitive serves for projecting the reflection grabbed by the probe (the reflection is projected only within the area of intersection of the probe and the surface). Some parameters of the material assigned to the reflecting surface are also tweaked in order to provide the desired effect and match [roughness](#setReflectionVisibilityRoughnessMin_float_void) range (which enables rendering of reflections depending on surface roughness).


Copy the source code below implemented as a C# component, save it to the `PlanarReflector.cs` file, create a new *Dummy Node* or choose any other node in the scene and assign the component to it.


```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;
#region Math Variables
#if UNIGINE_DOUBLE
using Vec3 = Unigine.dvec3;
using Mat4 = Unigine.dmat4;
#else
using Vec3 = Unigine.vec3;
using Mat4 = Unigine.mat4;
#endif
#endregion

public partial class PlanarReflector : Component
{
	private ObjectMeshDynamic plane;
	private LightPlanarProbe planar_probe;
	private void Init()
	{
		// write here code to be called on component initialization
		//creating a reflecting plane, onto which the reflection is to be projected by the probe
		plane = Primitives.CreatePlane(20, 20, 1);

		// Creating a planar reflection probe of the same size
		planar_probe = new LightPlanarProbe();
		planar_probe.ProjectionSize = new vec3(20, 20, 1);
		plane.Rotate(-90.0f, 0.0f, 0.0f);
		plane.Translate(0.0f, 5.0f, 5.0f);

		// putting the planar probe so that it covers the reflecting surface
		planar_probe.Transform = plane.Transform;

		// inheriting a new material from the one assigned
		// to the surface by default in order to tweak it
		// and set metalness and roughness values (metallic and polished)
		Material plane_mat = plane.GetMaterialInherit(0);
		plane_mat.SetParameterFloat("metalness", 1.0f);
		plane_mat.SetParameterFloat("roughness", 0.0f);

		// set the distance from the camera, up to which
		// the planar reflection will be visible
		planar_probe.VisibleDistance = 5.0f;
	}

	private void Update()
	{
		// write here code to be called before updating each render frame

	}
}

```


## LightPlanarProbe Class

### Enums

## REFLECTION_RESOLUTION

| Name | Description |
|---|---|
| **MODE_HEIGHT** = 0 | Reflection texture size equals to the viewport height resolution. |
| **MODE_HALF_HEIGHT** = 1 | Reflection texture size equals to half of the viewport height resolution. |
| **MODE_QUART_HEIGHT** = 2 | Reflection texture size equals to the quarter of the viewport height resolution. |
| **MODE_128** = 3 | Reflection texture size equals to 128x128 pixels. |
| **MODE_256** = 4 | Reflection texture size equals to 256x256 pixels. |
| **MODE_512** = 5 | Reflection texture size equals to 512x512 pixels. |
| **MODE_1024** = 6 | Reflection texture size equals to 1024x1024 pixels. |
| **MODE_2048** = 7 | Reflection texture size equals to 2048x2048 pixels. |
| **MODE_4096** = 8 | Reflection texture size equals to 4096x4096 pixels. |

### Properties

## vec3 ProjectionSize

The size of the Light Planar Probe. Defines the box-shaped influence volume around the probe, in units, in which reflective surfaces (having the appropriate roughness values) shall use the results captured by the probe.
## vec3 AttenuationDistance

The attenuation distance that specifies how far the projection can reach any surfaces from the Probe position. It also specifies the attenuation area around the Probe at which the projection starts to fade out at the specified rate.
## int RoughnessSamples

The number of samples used to adjust quality of the blurring effect for the reflection on rough surfaces.
## LightPlanarProbe.REFLECTION_RESOLUTION ReflectionResolution

The resolution of the reflection texture for the projection.
## bool TwoSided

The value indicating if the reflection is two-sided.
## bool StereoPerEyeEnabled

The value indicating if rendering of the reflection for each eye separately is enabled.
## float DistanceScale

The distance multiplier for the reflection visibility distance. Distance Scale is applied to the distance measured from the reflection camera to the node (surface) bound.
## float ReflectionDistance

The rendering distance of the reflected projection that specifies how far the reflection is rendered from the camera.
## int ReflectionViewportMask

The [reflection mask](../../../principles/bit_masking/index.md#reflection_mask) that controls rendering of the Planar Reflection Probe reflections into the reflection camera viewport.
## 🔒︎ int VisibilitySkipFlags

The mask that specifies what objects to ingore for the reflection projection.
## float ZNear

The distance to the near clipping plane defining a frustum to be used for grabbing reflections.
## float ZFar

The distance to the far clipping plane defining a frustum to be used for grabbing reflections.
## float ReflectionVisibilityRoughnessMin

The surface roughness value, starting from which the reflection starts to fade out gradually.
## float ReflectionVisibilityRoughnessMax

The surface roughness value, starting from which the reflection completely disappears.
## bool VisibilitySky

The value indicating if rendering of the sky is enabled or disabled for the reflection.
## float Parallax

The degree of reflection distortion. Distortion depends on an angle between the probe plane and the surface onto which the probe projects reflection. Increasing the value amplifies visual distortion as a result of increasing this angle.
## float NoiseIntensity

The intensity of jitter for roughness samples that creates a noise effect on the reflection.
## float ReflectionOffset

The reflection Z axis offset relative to the probe coordinate system.
### Members

---

## LightPlanarProbe ( )

Constructor. Creates a new planar probe.
## static int type ( )

Returns the object node type.
