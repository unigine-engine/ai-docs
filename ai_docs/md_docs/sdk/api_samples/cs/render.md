# Rendering

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/csharp-component-samples](https://github.com/unigine-engine/csharp-component-samples)**.


## Camera To Texture

This sample shows how to capture the output of a camera in real time and project it onto a material's albedo texture using *[Viewport.RenderTexture2D()](../../../api/library/rendering/class.viewport_cpp.md#renderTexture2D_Camera_Texture_void)*.


A renderable 2D texture is created and set as the albedo texture of the material assigned to the plane. Each frame, the active camera's view is rendered into this texture, updating the appearance of the object it's applied to. Texture sampling settings like linear filtering and anisotropy are configured to ensure visual quality. The UV transform is also adjusted to correct for platform-dependent flipping.


This method can be used for features such as security monitors, live camera feeds, dynamic mirrors, portals, or mini-maps in your worlds.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/rendering/camera_to_texture*
## FFP Triangle Fan Rendering

This sample demonstrates how to render a simple 2D shape using the *[Fixed Function Pipeline (Ffp)](../../../api/library/rendering/class.ffp_cpp.md)* in UNIGINE via the C# API. A colorful figure composed of 16 vertices is drawn directly on screen using orthographic projection.


The rendering logic is called every frame by hooking into the Engine's render loop. Ffp mode is enabled for drawing and then disabled, keeping this rendering isolated from the rest of the frame.


This approach is useful for quick visualization overlays, Editor tools, or debugging tasks where shader-based rendering isn't required.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/rendering/ffp_triangle_fan_rendering*
## Gui To Texture

This sample demonstrates how to render GUI elements into a texture using *[Gui.Render()](../../../api/library/gui/class.gui_cpp.md#render_void)*. Instead of drawing directly to the screen, the GUI is redirected to a custom framebuffer, which isolates its rendering pipeline and allows the resulting texture to be applied to materials.


You can use this sample to display dynamic GUI elements on in-game monitors, control panels, or other similar surfaces.


The **GuiToTexture** component supports two update modes:


- In manual mode, the texture is updated only when explicitly calling *RenderToTexture()* method. This is used in the **WidgetClock** component, where the GUI (a digital clock) is re-rendered once per second, only when the displayed time changes.
- Automatic mode is enabled by default and updates the GUI texture every frame. This is demonstrated in the **WidgetNoSignal** component, where a *"No Signal"* label moves across the screen like a screensaver. Because the position of the widget changes every frame, the texture must be continuously updated to reflect those changes.


The render flow involves saving and clearing the current render state, binding a texture, configuring the viewport, rendering the GUI widgets, and restoring the render state. Mipmaps are also generated to ensure proper filtering at different scales and distances.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/rendering/gui_to_texture*
## Mesh To Mask Texture

This sample demonstrates how to render a mesh into a texture using a custom material, producing an image to be used as a mask. The mesh is rendered from a dedicated camera view directly into a texture, which is then assigned to the albedo slot of a preview material.


Use the manipulator to move the camera view and observe how different viewing angles affect the generated texture mask.


The sample compares two rendering approaches:


- **Renderer.RenderMesh** - standard camera-based rendering **(recommended for most use cases)**. The Engine automatically prepares matrices, render states, and shaders, so you only need to provide the mesh, material, transform, and camera.
- **MeshRender.Render** - low-level, **fully manual** projection and modelview setup. This method provides finer control over the rendering pipeline but requires explicit setup of projection and view matrices, RenderState configuration, and manual shader parameter management.


Both methods produce identical visual results, allowing you to choose whichever approach best fits your workflow.


This technique is useful for dynamic decals, procedural effects, or any feature requiring real-time texture generation from 3D geometry.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/rendering/mesh_to_mask_texture*
## Procedural 3D Volume Texture Generation

This sample shows how to procedurally generate *3D* image data and use it as a density texture for a volume-based material in real time. The result is visualized using a volume box that updates dynamically every frame based on custom field simulation.


The sample initializes a *3D* image with a predefined resolution and fills it with voxel data derived from a set of moving fields. Each field represents an abstract spherical influence zone that contributes to the voxel density based on distance. Field dynamics are updated every frame to simulate motion.


The raw image data is accessed directly via a pixel pointer and modified per frame, with density values mapped to *RGBA* channels. The resulting image is then uploaded to a material as a *3D* texture used in a volumetric shading model.


The sample demonstrates how to work with the *[Image](../../../api/library/common/class.image_cpp.md)* class and update *GPU* resources efficiently at runtime. This approach can be used for generating volumetric effects such as clouds, fog, or procedurally driven visual phenomena.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/rendering/procedural_3d_volume_texture_generation*
## Screenshot

Simple demonstration of how to make a screenshot by grabbing the final image from the rendering sequence.
**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/rendering/screenshot*

## Visualizer

This sample demonstrates the full range of features provided by the *[Visualizer](../../../api/library/engine/class.visualizer_cpp.md)* class.


The sample illustrates how to use *Visualizer* for debugging node positions, physics vectors, bounding volumes, and custom geometry in both world space and screen space. Use controls to explore the area.


*VisualizerUsage.cs* renders a wide range of primitives including points, lines, boxes, frustums, spheres, capsules, and object bounds using *Visualizer* methods.


*2D* visualizer features can be toggled on and off via the corresponding checkboxes.


Enable or disable depth testing, toggle specific primitives, and inspect how different rendering options behave in real time.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/rendering/visualizer*
## Weapon Clipping

In first-person games, weapon models can clip through walls or geometry when the camera gets too close. This sample solves the problem by rendering the weapon separately into a texture and overlaying it on top of the main camera view.


This approach keeps the weapon always visible, even when the camera is close to walls, without interfering with the main rendering pipeline.


The setup uses two cameras with identical transforms to keep their views aligned. *[Viewport masks](../../../principles/bit_masking/index.md#viewport)* for cameras are set via UnigineEditor: the main camera renders everything except the weapon, while the secondary (weapon) camera renders only the weapon. The weapon view is captured into a texture using *[Viewport.RenderTexture2D()](../../../api/library/rendering/class.viewport_cpp.md#renderTexture2D_Camera_Texture_void)*.


Each frame, this texture is overlaid onto the screen using *[Render.RenderScreenMaterial()](../../../api/library/rendering/class.render_cpp.md#renderScreenMaterial_cstr_void)*, compositing the weapon on top of the environment. The component handles screen resizing, maintains isolated render states, and offers optional settings like skipping shadows in the weapon rendering pass.


**SDK Path:***<SAMPLES_PROJECT_PATH>/data/csharp_component_samples/rendering/weapon_clipping*
