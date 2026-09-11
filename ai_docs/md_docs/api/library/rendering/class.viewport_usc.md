# Unigine.Viewport Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The **Viewport** class is used to render a scene with the specified settings.


The main use cases of the Viewport class are as follows:


1. Render a scene to the [texture](../../../api/library/rendering/class.texture_usc.md) interface (data stays in the GPU memory), using the following methods: ```cpp // initialization Viewport viewport = new Viewport(); Texture texture = new Texture(); texture.create2D(512, 512, TEXTURE_FORMAT_RGBA8);// create 512 x 512 render target CameraPtr camera = new Camera(); // set modelview & projection matrices to camera instance // rendering an image from the camera to the texture viewport.renderTexture2D(camera, texture); ```

  - *[renderTexture2D(camera,texture)](#renderTexture2D_Camera_Texture_void)*
  - *[renderTexture2D(camera,texture,width,height,hdr)](#renderTexture2D_Camera_Texture_int_int_int_void)*
  - *[renderTextureCube(camera,texture,local_space)](#renderTextureCube_Camera_Texture_int_void)*
  - *[renderTextureCube(camera,texture,size,hdr,local_space)](#renderTextureCube_Camera_Texture_int_int_int_void)*
2. Render a node to a [texture](../../../api/library/rendering/class.texture_usc.md) (data stays in the GPU memory).

  - To render a node (or nodes) to a [Texture](../../../api/library/rendering/class.texture_usc.md) interface, use the following methods:

    - *[renderNodeTexture2D(camera,node,texture)](#renderNodeTexture2D_Camera_Node_Texture_void)*
    - *[renderNodeTexture2D(camera,node,texture,width,height,hdr)](#renderNodeTexture2D_Camera_Node_Texture_int_int_int_void)*
    - *[renderNodesTexture2D(camera,nodes,texture)](#renderNodesTexture2D_Camera_VECNode_Texture_void)*
    - *[renderNodesTexture2D(camera,nodes,texture,width,height,hdr)](#renderNodesTexture2D_Camera_VECNode_Texture_int_int_int_void)*


> **Notice:** To set any viewport as a main, use the [setViewport()](../../../api/library/rendering/class.render_usc.md#setViewport_Viewport_void)  method of the *Render* class.
>
>
> **A single viewport should be used with a single camera**, otherwise it may cause visual artefacts. To avoid artefacts, when using several cameras with a single viewport, all post effects must be disabled using the [setSkipFlags()](#setSkipFlags_int_void)  method with the *[VIEWPORT_SKIP_POSTEFFECTS()](../../...md#SKIP_POSTEFFECTS)* flag.


<details>
<summary>Example: Single Viewport & Several Cameras | Close</summary>

```cpp
void setupMultipleCamerasWithSingleViewport()
{
    // Create a shared viewport for multiple cameras
    Viewport shared_viewport = new Viewport();

    // CRITICAL: Disable post-effects to avoid visual artifacts
    // when using multiple cameras with a single viewport
    shared_viewport.setSkipFlags(VIEWPORT_SKIP_POSTEFFECTS);

    shared_viewport.setNodeLightUsage(VIEWPORT_USAGE_WORLD_LIGHT);

    // Create multiple cameras
    Camera camera1 = new Camera();
    Camera camera2 = new Camera();

    // Position cameras differently
    camera1.setPosition(vec3(0.0f, 0.0f, 5.0f));
    camera2.setPosition(vec3(10.0f, 0.0f, 5.0f));

    // Create textures for each camera's output
    Texture texture1 = new Texture();
    Texture texture2 = new Texture();

    texture1.create2D(1920, 1080, TEXTURE_FORMAT_RGBA8,
        TEXTURE_FORMAT_USAGE_RENDER);
    texture2.create2D(1920, 1080, TEXTURE_FORMAT_RGBA8,
        TEXTURE_FORMAT_USAGE_RENDER);

    // Render from different cameras using the same viewport
    // Post-effects are disabled, so no artifacts will occur
    shared_viewport.renderTexture2D(camera1, texture1);
    shared_viewport.renderTexture2D(camera2, texture2);
}

```

</details>


### See also


- C++ samples:

  -
  -
  -
  -
- C# Component sample
- C++/C# usage example: [Creating Mirrors Using Viewports (Rendering to Texture) or a Standard Material](../../../code/usage/mirrors_viewports_materials/index.md)


## Viewport Class

### Members

## void setNodeLightUsage ( int usage )

Sets a new type of lighting of the render node.
### Arguments

- *int* **usage** - The lighting type. Can be one of the following:

  - 0 - *[VIEWPORT_USAGE_WORLD_LIGHT()](../../...md#USAGE_WORLD_LIGHT)* (use lighting from the [LightWorld](../../../api/library/lights/class.lightworld_usc.md) set in the current loaded world).
  - 1 - *[VIEWPORT_USAGE_AUX_LIGHT()](../../...md#USAGE_AUX_LIGHT)* (use lighting from the auxiliary virtual scene containing one LightWorld with 45 degrees slope angles along all axes, scattering is not used).
  - 2 - *[VIEWPORT_USAGE_NODE_LIGHT()](../../...md#USAGE_NODE_LIGHT)* (use the node lighting).

## int getNodeLightUsage () const

Returns the current type of lighting of the render node.
### Return value

Current
lighting type. Can be one of the following:


- 0 - *[VIEWPORT_USAGE_WORLD_LIGHT()](../../...md#USAGE_WORLD_LIGHT)* (use lighting from the [LightWorld](../../../api/library/lights/class.lightworld_usc.md) set in the current loaded world).
- 1 - *[VIEWPORT_USAGE_AUX_LIGHT()](../../...md#USAGE_AUX_LIGHT)* (use lighting from the auxiliary virtual scene containing one LightWorld with 45 degrees slope angles along all axes, scattering is not used).
- 2 - *[VIEWPORT_USAGE_NODE_LIGHT()](../../...md#USAGE_NODE_LIGHT)* (use the node lighting).


## void setStereoOffset ( float offset )

Sets a new virtual camera offset (an offset after the perspective projection).
### Arguments

- *float* **offset** - The virtual camera offset in units.

## float getStereoOffset () const

Returns the current virtual camera offset (an offset after the perspective projection).
### Return value

Current virtual camera offset in units.
## void setStereoRadius ( float radius )

Sets a new radius for stereo � the half of the separation distance between the cameras (i.e. between eyes).
### Arguments

- *float* **radius** - The stereo radius in units. If a negative value is provided, 0 will be used instead.

## float getStereoRadius () const

Returns the current radius for stereo � the half of the separation distance between the cameras (i.e. between eyes).
### Return value

Current stereo radius in units. If a negative value is provided, 0 will be used instead.
## void setStereoDistance ( float distance )

Sets a new focal distance for stereo rendering (distance in the world space to the point where two views line up, i.e. to the zero parallax plane).
### Arguments

- *float* **distance** - The focal distance in units.

## float getStereoDistance () const

Returns the current focal distance for stereo rendering (distance in the world space to the point where two views line up, i.e. to the zero parallax plane).
### Return value

Current focal distance in units.
## isStereo () const

Returns the current value indicating if the stereo rendering is enabled for the current viewport (one of the [stereo modes](../../../api/library/rendering/class.render_usc.md#VIEWPORT_MODE_STEREO_ANAGLYPH) is set).
### Return value

Current stereo rendering for the current viewport (one of the [stereo modes](../../../api/library/rendering/class.render_usc.md#VIEWPORT_MODE_STEREO_ANAGLYPH))
## isPanorama () const

Returns the current value indicating if the panoramic rendering is enabled.
### Return value

Current panoramic rendering
## void setRenderMode ( int mode )

Sets a new render mode. The mode determines the set of buffers to be rendered.
### Arguments

- *int* **mode** - The render mode, one of the following:

  - *[VIEWPORT_RENDER_DEPTH()](../../...md#RENDER_DEPTH)*
  - *[VIEWPORT_RENDER_DEPTH_GBUFFER()](../../...md#RENDER_DEPTH_GBUFFER)*
  - *[VIEWPORT_RENDER_DEPTH_GBUFFER_FINAL()](../../...md#RENDER_DEPTH_GBUFFER_FINAL)*

## int getRenderMode () const

Returns the current render mode. The mode determines the set of buffers to be rendered.
### Return value

Current
render mode, one of the following:


- *[VIEWPORT_RENDER_DEPTH()](../../...md#RENDER_DEPTH)*
- *[VIEWPORT_RENDER_DEPTH_GBUFFER()](../../...md#RENDER_DEPTH_GBUFFER)*
- *[VIEWPORT_RENDER_DEPTH_GBUFFER_FINAL()](../../...md#RENDER_DEPTH_GBUFFER_FINAL)*


## void setMode ( )

Sets a new rendering mode for the current viewport.
### Arguments

- **mode** - The rendering mode set for the current viewport. It can be one of the [stereo](../../../api/library/rendering/class.render_usc.md#VIEWPORT_MODE_STEREO_ANAGLYPH) or [panoramic](../../../api/library/rendering/class.render_usc.md#VIEWPORT_MODE_PANORAMA_CURVED_180) modes or the [default](../../../api/library/rendering/class.render_usc.md#VIEWPORT_MODE_DEFAULT) mode.

## getMode () const

Returns the current rendering mode for the current viewport.
### Return value

Current rendering mode set for the current viewport. It can be one of the [stereo](../../../api/library/rendering/class.render_usc.md#VIEWPORT_MODE_STEREO_ANAGLYPH) or [panoramic](../../../api/library/rendering/class.render_usc.md#VIEWPORT_MODE_PANORAMA_CURVED_180) modes or the [default](../../../api/library/rendering/class.render_usc.md#VIEWPORT_MODE_DEFAULT) mode.
## void setSkipFlags ( int flags )

Sets a new [skip flag](#SKIP_SHADOWS) set for the current viewport.
### Arguments

- *int* **flags** - The [skip flag](#SKIP_SHADOWS) set for the current viewport.

## int getSkipFlags () const

Returns the current [skip flag](#SKIP_SHADOWS) set for the current viewport.
### Return value

Current [skip flag](#SKIP_SHADOWS) set for the current viewport.
## void setFirstFrame ( int frame )

Sets a new value indicating if the first frame is enabled over the current frame.
### Arguments

- *int* **frame** - The value indicating if the first frame is enabled over the current frame: 1 for the first frame flag; otherwise, 0.

## int getFirstFrame () const

Returns the current value indicating if the first frame is enabled over the current frame.
### Return value

Current value indicating if the first frame is enabled over the current frame: 1 for the first frame flag; otherwise, 0.
## void setAspectCorrection ( bool correction )

Sets a new value indicating if the aspect correction enabled for current viewport.
### Arguments

- *bool* **correction** - Set **true** to enable the aspect correction; **false** - to disable it.

## bool isAspectCorrection () const

Returns the current value indicating if the aspect correction enabled for current viewport.
### Return value

**true** if the aspect correction is enabled ; otherwise **false**.
## int getID () const

Returns the current Viewport ID.
### Return value

Current Viewport ID.
## void setPanoramaFisheyeFov ( float fov )

Sets a new field of view angle used for the panorama rendering mode.
### Arguments

- *float* **fov** - The field of view angle used for the panorama rendering mode, in degrees.

## float getPanoramaFisheyeFov () const

Returns the current field of view angle used for the panorama rendering mode.
### Return value

Current field of view angle used for the panorama rendering mode, in degrees.
## void setEnvironmentTexture ( )

Sets a new cubemap defining the environment color.
### Arguments

- **texture** - The cubemap defining the environment color.

## getEnvironmentTexture () const

Returns the current cubemap defining the environment color.
### Return value

Current cubemap defining the environment color.
## void setUseTAAOffset ( bool taaoffset )

Sets a new  value indicating if skipping render mode check is enabled for using TAA.
Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to *[VIEWPORT_RENDER_DEPTH()](../../...md#RENDER_DEPTH)*.

### Arguments

- *bool* **taaoffset** - Set **true** to enable skipping render mode check when using TAA; **false** - to disable it.

## bool isUseTAAOffset () const

Returns the current  value indicating if skipping render mode check is enabled for using TAA.
Can be used to ensure proper TAA calculation when rendering mode for the *Viewport* is set to *[VIEWPORT_RENDER_DEPTH()](../../...md#RENDER_DEPTH)*.

### Return value

**true** if skipping render mode check when using TAA is enabled ; otherwise **false**.
## void setLifetime ( int lifetime )

Sets a new value indicating how many frames temporary viewport resources are available after the viewport stops rendering.
### Arguments

- *int* **lifetime** - The number of frames during which temporary viewport resources are available after the viewport stops rendering

## int getLifetime () const

Returns the current value indicating how many frames temporary viewport resources are available after the viewport stops rendering.
### Return value

Current number of frames during which temporary viewport resources are available after the viewport stops rendering
## getEventBegin () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginEnvironment () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndEnvironment () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginShadows () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginWorldShadow () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndWorldShadow () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginProjShadow () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndProjShadow () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginOmniShadow () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndOmniShadow () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndShadows () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginScreen () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginMixedRealityBlendMaskColor () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndMixedRealityBlendMaskColor () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginOpacityGBuffer () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventBeginAuxiliarySurfaces () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventEndAuxiliarySurfaces () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndOpacityGBuffer () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginOpacityDecals () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndOpacityDecals () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventBeginAuxiliaryDecals () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventEndAuxiliaryDecals () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginCurvature () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndCurvature () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginCurvatureComposite () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndCurvatureComposite () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginSSRTGI () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndSSRTGI () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginOpacityLights () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndOpacityLights () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginOpacityVoxelProbes () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndOpacityVoxelProbes () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginOpacityEnvironmentProbes () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndOpacityEnvironmentProbes () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginOpacityPlanarProbes () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndOpacityPlanarProbes () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginRefractionBuffer () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndRefractionBuffer () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginTransparentBlurBuffer () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndTransparentBlurBuffer () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginSSSS () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndSSSS () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginSSR () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndSSR () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginSSAO () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndSSAO () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginSSGI () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndSSGI () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginSky () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndSky () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginCompositeDeferred () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndCompositeDeferred () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginTransparent () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginClouds () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndClouds () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginWater () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginWaterGBuffer () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndWaterGBuffer () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginWaterDecals () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndWaterDecals () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginWaterLights () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndWaterLights () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginWaterVoxelProbes () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndWaterVoxelProbes () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginWaterEnvironmentProbes () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndWaterEnvironmentProbes () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginWaterPlanarProbes () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndWaterPlanarProbes () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndWater () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndTransparent () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginSrgbCorrection () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndSrgbCorrection () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginAdaptationColorAverage () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndAdaptationColorAverage () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginAdaptationColor () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndAdaptationColor () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginTAA () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndTAA () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginCameraEffects () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndCameraEffects () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginPostMaterials () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndPostMaterials () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginDebugMaterials () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndDebugMaterials () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventBeginVisualizer () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndVisualizer () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndScreen () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEnd () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## getEventEndVRQuadComposeEyeSwapchains () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## void setPanoramaFisheyeKannalaBrandtCoefficients ( vec4 coefficients )

Sets a new four radial distortion coefficients (k1, k2, k3, k4) of the Kannala-Brandt fisheye camera model used by the corresponding panorama mode. They define the polynomial mapping the angle between the incoming ray and the optical axis to the normalized image radius. The default value (1, 0, 0, 0) corresponds to the pure equidistant projection. This mode reproduces the image geometry of a real calibrated fisheye camera, with the coefficients taken from the camera calibration data.
### Arguments

- *vec4* **coefficients** - The radial distortion coefficients of the Kannala-Brandt model

## vec4 getPanoramaFisheyeKannalaBrandtCoefficients () const

Returns the current four radial distortion coefficients (k1, k2, k3, k4) of the Kannala-Brandt fisheye camera model used by the corresponding panorama mode. They define the polynomial mapping the angle between the incoming ray and the optical axis to the normalized image radius. The default value (1, 0, 0, 0) corresponds to the pure equidistant projection. This mode reproduces the image geometry of a real calibrated fisheye camera, with the coefficients taken from the camera calibration data.
### Return value

Current radial distortion coefficients of the Kannala-Brandt model
## void setPanoramaFisheyeKannalaBrandtFocalLength ( vec2 length )

Sets a new focal length intrinsics (fx, fy) of the calibrated fisheye camera, in pixels, used by the Kannala-Brandt panorama mode to convert pixel coordinates to normalized camera coordinates.
### Arguments

- *vec2* **length** - The focal length intrinsics of the calibrated fisheye camera

## vec2 getPanoramaFisheyeKannalaBrandtFocalLength () const

Returns the current focal length intrinsics (fx, fy) of the calibrated fisheye camera, in pixels, used by the Kannala-Brandt panorama mode to convert pixel coordinates to normalized camera coordinates.
### Return value

Current focal length intrinsics of the calibrated fisheye camera
## void setPanoramaFisheyeKannalaBrandtImageCircleRadius ( float radius )

Sets a new radius of the valid image circle of the fisheye lens in normalized radial coordinates, used by the Kannala-Brandt panorama mode: pixels outside this radius are masked out, reproducing the image circle of the real lens.
### Arguments

- *float* **radius** - The radius of the valid image circle of the fisheye lens

## float getPanoramaFisheyeKannalaBrandtImageCircleRadius () const

Returns the current radius of the valid image circle of the fisheye lens in normalized radial coordinates, used by the Kannala-Brandt panorama mode: pixels outside this radius are masked out, reproducing the image circle of the real lens.
### Return value

Current radius of the valid image circle of the fisheye lens
## void setPanoramaFisheyeKannalaBrandtImageDimensions ( vec2 dimensions )

Sets a new dimensions (width, height), in pixels, of the calibrated camera image the Kannala-Brandt intrinsics refer to. The viewport coordinates are mapped to this pixel space before the intrinsics are applied.
### Arguments

- *vec2* **dimensions** - The image dimensions the fisheye intrinsics refer to

## vec2 getPanoramaFisheyeKannalaBrandtImageDimensions () const

Returns the current dimensions (width, height), in pixels, of the calibrated camera image the Kannala-Brandt intrinsics refer to. The viewport coordinates are mapped to this pixel space before the intrinsics are applied.
### Return value

Current image dimensions the fisheye intrinsics refer to
## void setPanoramaFisheyeKannalaBrandtPrincipalPoint ( vec2 point )

Sets a new principal point intrinsics (cx, cy) of the calibrated fisheye camera, in pixels: the image position of the optical axis used by the Kannala-Brandt panorama mode.
### Arguments

- *vec2* **point** - The principal point intrinsics of the calibrated fisheye camera

## vec2 getPanoramaFisheyeKannalaBrandtPrincipalPoint () const

Returns the current principal point intrinsics (cx, cy) of the calibrated fisheye camera, in pixels: the image position of the optical axis used by the Kannala-Brandt panorama mode.
### Return value

Current principal point intrinsics of the calibrated fisheye camera
## void setPanoramaFisheyeKannalaBrandtSkew ( float skew )

Sets a new skew (axis non-orthogonality) coefficient of the calibration matrix used by the Kannala-Brandt panorama mode. The value of 0 (default) corresponds to orthogonal pixel axes.
### Arguments

- *float* **skew** - The skew intrinsic of the calibrated fisheye camera

## float getPanoramaFisheyeKannalaBrandtSkew () const

Returns the current skew (axis non-orthogonality) coefficient of the calibration matrix used by the Kannala-Brandt panorama mode. The value of 0 (default) corresponds to orthogonal pixel axes.
### Return value

Current skew intrinsic of the calibrated fisheye camera
## void setPanoramaFisheyeKannalaBrandtTangentialDistortion ( vec2 distortion )

Sets a new tangential (decentering) distortion coefficients (p1, p2) of the calibrated fisheye camera used by the Kannala-Brandt panorama mode. The value (0, 0) means no tangential distortion.
### Arguments

- *vec2* **distortion** - The tangential distortion coefficients of the calibrated fisheye camera

## vec2 getPanoramaFisheyeKannalaBrandtTangentialDistortion () const

Returns the current tangential (decentering) distortion coefficients (p1, p2) of the calibrated fisheye camera used by the Kannala-Brandt panorama mode. The value (0, 0) means no tangential distortion.
### Return value

Current tangential distortion coefficients of the calibrated fisheye camera
## void setPanoramaForceDisableScreenSpaceEffects ( int effects )

Sets a new value indicating if screen-space and screen-dependent camera effects (such as SSR, SSAO, SSGI, motion blur, DOF, bloom, lens flares, local tonemapper) are forcibly disabled while the viewport renders a panorama. These effects are computed per panorama face and would produce visible seams between the faces. Enabled by default; when disabled, the effects stay as configured at the cost of per-face artifacts.
### Arguments

- *int* **effects** - The forced disabling of screen-space effects in panorama modes

## int isPanoramaForceDisableScreenSpaceEffects () const

Returns the current value indicating if screen-space and screen-dependent camera effects (such as SSR, SSAO, SSGI, motion blur, DOF, bloom, lens flares, local tonemapper) are forcibly disabled while the viewport renders a panorama. These effects are computed per panorama face and would produce visible seams between the faces. Enabled by default; when disabled, the effects stay as configured at the cost of per-face artifacts.
### Return value

Current forced disabling of screen-space effects in panorama modes
## void setPanoramaFisheyeKannalaBrandtChromaticAberration ( float aberration )

Sets a new chromatic aberration intensity of the fisheye lens, used by the Kannala-Brandt panorama mode: the red channel is sampled at the radial distance scaled by (1 - value), the blue channel at (1 + value), reproducing lateral chromatic aberration of a real lens. 0 means no chromatic aberration.
### Arguments

- *float* **aberration** - The chromatic aberration intensity of the fisheye lens

## float getPanoramaFisheyeKannalaBrandtChromaticAberration () const

Returns the current chromatic aberration intensity of the fisheye lens, used by the Kannala-Brandt panorama mode: the red channel is sampled at the radial distance scaled by (1 - value), the blue channel at (1 + value), reproducing lateral chromatic aberration of a real lens. 0 means no chromatic aberration.
### Return value

Current chromatic aberration intensity of the fisheye lens
## void setPanoramaFisheyeKannalaBrandtVignettingCoefficient5 ( float coefficient5 )

Sets a new fifth coefficient of the fisheye vignetting polynomial, used by the Kannala-Brandt panorama mode: the coefficient at the 10th power of the normalized radial distance, kept separate because the coefficients vector holds only four components.
### Arguments

- *float* **coefficient5** - The fifth coefficient of the fisheye vignetting polynomial

## float getPanoramaFisheyeKannalaBrandtVignettingCoefficient5 () const

Returns the current fifth coefficient of the fisheye vignetting polynomial, used by the Kannala-Brandt panorama mode: the coefficient at the 10th power of the normalized radial distance, kept separate because the coefficients vector holds only four components.
### Return value

Current fifth coefficient of the fisheye vignetting polynomial
## void setPanoramaFisheyeKannalaBrandtVignettingCoefficients ( vec4 coefficients )

Sets a new first four coefficients of the fisheye vignetting polynomial, used by the Kannala-Brandt panorama mode: the vignetting intensity is an even-order polynomial of the radial distance normalized by the image circle radius, with these values as the coefficients at the 2nd, 4th, 6th, and 8th powers.
### Arguments

- *vec4* **coefficients** - The first four coefficients of the fisheye vignetting polynomial

## vec4 getPanoramaFisheyeKannalaBrandtVignettingCoefficients () const

Returns the current first four coefficients of the fisheye vignetting polynomial, used by the Kannala-Brandt panorama mode: the vignetting intensity is an even-order polynomial of the radial distance normalized by the image circle radius, with these values as the coefficients at the 2nd, 4th, 6th, and 8th powers.
### Return value

Current first four coefficients of the fisheye vignetting polynomial
---

## static Viewport ( )


Creates a new viewport with default settings.


> **Notice:** We don't recommend creating a viewport every frame, as such approach is unoptimal and exhaust GPU resources. Create viewports in  instead, to have them cached for further use.


## void appendSkipFlags ( int flags )

Appends specified [skip flags](#SKIP_SHADOWS) to the list of currently used ones.
### Arguments

- *int* **flags** - [Skip flags](#SKIP_SHADOWS) to append.

## int checkSkipFlags ( int flags )

Returns a value indicating if the specified [skip flags](#SKIP_SHADOWS) are set for the current viewport.
### Arguments

- *int* **flags** - [Skip flags](#SKIP_SHADOWS) to check.

### Return value

1 if the skip flags are set; otherwise, 0.
## void removeSkipFlags ( int flags )

Removes specified [skip flags](#SKIP_SHADOWS) from the list of currently used ones.
### Arguments

- *int* **flags** - [Skip flags](#SKIP_SHADOWS) to remove.

## void render ( Camera camera )


Renders an image from the specified camera.


To render an image from the camera to the [RenderTarget](../../../api/library/rendering/class.rendertarget_usc.md) interface, do the following:


```cpp
camera = new Camera();

rendertarget->enable();
	viewport->render(camera);
rendertarget->disable();

```


### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera** - Camera an image from which should be rendered.

## void render ( Camera camera , int width , int height )

Renders an image of the specified size from the specified camera to the current rendering target.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera** - Camera, an image from which should be rendered.
- *int* **width** - Image width, in pixels.
- *int* **height** - Image height, in pixels.

## void renderEngine ( Camera camera )

Renders an Engine viewport for the specified camera to the current rendering target. This method renders a splash screen and provides an image in accordance with panoramic and stereo rendering settings.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera** - Camera, an image from which should be rendered.

## void renderTexture2D ( Camera camera , Texture texture )

Renders an image from the camera to the specified 2D texture.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera** - Camera, an image from which should be rendered.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Target 2D [texture](../../../api/library/rendering/class.texture_usc.md) to save the result to.

## void renderTexture2D ( Camera camera , Texture texture , int width , int height , int hdr = 0 )

Renders an image of the specified size from the camera to a 2D texture.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera** - Camera, an image from which should be rendered.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Target 2D [texture](../../../api/library/rendering/class.texture_usc.md) to save the result to.
- *int* **width** - Texture width, in pixels.
- *int* **height** - Texture height, in pixels.
- *int* **hdr** - HDR flag. > **Notice:** This parameter determines the format of the 2D texture: > > > - **1** - texture format will be set to [**RGBA16F**](../../../api/library/rendering/class.texture_usc.md#FORMAT_RGBA16F) > - **0** - texture format will be set to [**RGBA8**](../../../api/library/rendering/class.texture_usc.md#FORMAT_RGBA8)

## void renderTextureCube ( Camera camera , Texture texture , int local_space = false )

Renders the image from the camera to the cubemap texture.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera** - Camera, an image from which should be rendered.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Target Cube [texture](../../../api/library/rendering/class.texture_usc.md) to save the result to.
- *int* **local_space** - A flag indicating if the camera angle should be used for the cube map rendering.

## void renderTextureCube ( Camera camera , Texture texture , int size , int hdr = 0 , int local_space = 0 )

Renders the image from the camera to the cube map of the specified size.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera** - Camera, an image from which should be rendered.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Target cube map to save the result to.
- *int* **size** - Cube map edge size.
- *int* **hdr** - HDR flag. > **Notice:** This parameter determines the format of the 2D texture: > > > - **1** - texture format will be set to [**RGBA16F**](../../../api/library/rendering/class.texture_usc.md#FORMAT_RGBA16F) > - **0** - texture format will be set to [**RGBA8**](../../../api/library/rendering/class.texture_usc.md#FORMAT_RGBA8)
- *int* **local_space** - A flag indicating if the camera angle should be used for the cube map rendering.

## void renderNode ( Camera camera , Node node )

Renders the given node with all children to the current rendering target.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera** - Camera, an image from which should be rendered.
- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - Node to be rendered.

## void renderNode ( Camera camera , Node node , int width , int height )

Renders the given node with all children to the current rendering target.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera** - Camera, an image from which should be rendered.
- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - Node to be rendered.
- *int* **width** - Image width, in pixels.
- *int* **height** - Image height, in pixels.

## void renderNodeTexture2D ( Camera camera , Node node , Texture texture , int width , int height , int hdr )

Renders the given node with all children to the 2D texture of the specified size.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera** - Camera, an image from which should be rendered.
- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - Node to be rendered.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Target 2D [texture](../../../api/library/rendering/class.texture_usc.md) to save the result to.
- *int* **width** - Texture width, in pixels.
- *int* **height** - Texture height, in pixels.
- *int* **hdr** - HDR flag. > **Notice:** This parameter determines the format of the 2D texture: > > > - **1** - texture format will be set to [**RGBA16F**](../../../api/library/rendering/class.texture_usc.md#FORMAT_RGBA16F) > - **0** - texture format will be set to [**RGBA8**](../../../api/library/rendering/class.texture_usc.md#FORMAT_RGBA8)

## void renderNodeTexture2D ( Camera camera , Node node , Texture texture )

Renders the given node with all children to the specified 2D texture.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera** - Camera, an image from which should be rendered.
- *[Node](../../../api/library/nodes/class.node_usc.md)* **node** - Node to be rendered.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture** - Target 2D [texture](../../../api/library/rendering/class.texture_usc.md) to save the result to.

## void renderStereo ( Camera camera_left , Camera camera_right , string stereo_material )

Renders a stereo image in the current viewport.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera_left** - Camera that renders an image for the left eye.
- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera_right** - Camera that renders an image for the right eye.
- *string* **stereo_material** - List of names of stereo materials to be used.

## void renderStereoPeripheral ( Camera camera_left , Camera camera_right , Camera camera_focus_left , Camera camera_focus_right , Texture texture_left , Texture texture_right , Texture texture_focus_left , Texture texture_focus_right , string stereo_material )

Renders a stereo image for HMDs having context (peripheral) and focus displays. This method saves performance on shadows and reflections along with other optimizations reducing rendering load, such as reduced resolutions for textures.
### Arguments

- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera_left** - Camera that renders an image for the left context (low-res) display.
- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera_right** - Camera that renders an image for the right context (low-res) display.
- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera_focus_left** - Camera that renders an image for the left focus (high-res) display.
- *[Camera](../../../api/library/rendering/class.camera_usc.md)* **camera_focus_right** - Camera that renders an image for the right focus (high-res) display.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture_left** - Texture to save the image rendered for the left context (low-res) display.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture_right** - Texture to save the image rendered for the right context (low-res) display.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture_focus_left** - Texture to save the image rendered for the left focus (high-res) display.
- *[Texture](../../../api/library/rendering/class.texture_usc.md)* **texture_focus_right** - Texture to save the image rendered for the right focus (high-res) display.
- *string* **stereo_material** - List of names of stereo materials to be used.

## void setStereoHiddenAreaMesh ( Mesh hidden_area_mesh_left , Mesh hidden_area_mesh_right )


Sets custom meshes to be used for culling pixels, that are not visible in VR.


> **Notice:** Requires [render_stereo_hidden_area](../../../code/console/index.md#render_stereo_hidden_area) = 2


### Arguments

- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **hidden_area_mesh_left** - [Mesh](../../../api/library/rendering/class.mesh_usc.md) representing hidden area for the left eye.
- *[Mesh](../../../api/library/rendering/class.mesh_usc.md)* **hidden_area_mesh_right** - [Mesh](../../../api/library/rendering/class.mesh_usc.md) representing hidden area for the right eye.

## void clearStereoHiddenAreaMesh ( )

Clears meshes that represent hidden areas for both, left and right eye. Hidden areas are used for culling pixels, that are not visible in VR
## void setEnvironmentTexturePath ( string name )

Sets the path to the [cubemap defining the environment color](../../../editor2/settings/render_settings/environment/index.md#env_texture) for the viewport. This texture is used for imitating landscape reflections and lighting in accordance with the ground mask.
### Arguments

- *string* **name** - Path to the cubemap defining the environment color.

## string getEnvironmentTexturePath ( )

Returns the path to the [cubemap defining the environment color](../../../editor2/settings/render_settings/environment/index.md#env_texture) set for the viewport. This texture is used for imitating landscape reflections and lighting in accordance with the ground mask.
### Return value

Path to the cubemap defining the environment color.
## void resetEnvironmentTexture ( )

Resets the current environment texture to the default one.
## void renderVREngine ( )

Renders the VR viewport if VR is enabled, taking into account the [vr mirror mode](../../../api/library/vr/class.vr_usc.md#MirrorMode) set.
## void lockResources ( )

Locks resources (such as temporal old textures) in the current viewport so they won't be reused or released.
## void unlockResources ( )

Unlocks resources (such as temporal old textures) in the current viewport so they can be reused and released by the engine.
## int isLockedResources ( )

Returns a value indicating if resources (such as temporal old textures) in the current viewport are locked and won't be reused or released.
### Return value

**1** if the resources are locked; otherwise, **0**.
