# Rendering

> **Notice:** The complete sample source code is available on GitHub:
> **[github.com/unigine-engine/cpp-api-samples](https://github.com/unigine-engine/cpp-api-samples)**.


## CAD-Like View

This sample demonstrates how to build a CAD-style layout by combining four synchronized views of the same scene: top, side, front, and perspective. Each view uses its own camera with a separate projection matrix - orthographic for technical views and perspective for the main one. Each view is rendered off-screen and displayed through a *[WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cpp.md)*.

The views are arranged in a 2x2 grid using GUI widgets. When the window is resized, texture resolutions are automatically updated to match the new layout and keep the viewports sharp.


Viewcubes are centered on the main object to maintain consistency across all views. They help indicate camera orientation and are updated based on the window size and viewport positions.


This setup is ideal for tools that require accurate inspection of a scene from multiple directions, such as modeling, level design, or CAD-style applications.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/cad_like_view*
## Camera To Texture

This sample shows how to capture the output of a camera in real time and project it onto a material's albedo texture using *[Viewport::renderTexture2D()](../../../api/library/rendering/class.viewport_cpp.md#renderTexture2D_Camera_Texture_void)*.


A renderable 2D texture is created and set as the albedo texture of the material assigned to the plane. Each frame, the active camera's view is rendered into this texture, updating the appearance of the object it's applied to. Texture sampling settings like linear filtering and anisotropy are configured to ensure visual quality. The UV transform is also adjusted to correct for platform-dependent flipping.


This method can be used for features such as security monitors, live camera feeds, dynamic mirrors, portals, or mini-maps in your worlds.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/camera_to_texture*
## Compute Shader

This sample demonstrates a GPU-based particle system implemented with compute shaders. It initializes a dynamic particle renderer, updates particle positions and velocities each frame using a ping-pong texture mechanism, and uses UV-mapped static meshes to influence particle behavior.


These mesh-to-particle transformations are well-suited for real-time visual effects, such as fluid or smoke simulations or interactive art installations.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/compute_shader*
## Compute Shader Image

This sample demonstrates how to create a texture at runtime and update it entirely on the GPU using compute shaders with read-write (unordered) access. The 2D texture is dynamically created and assigned to a material's albedo slot.


Each frame, the compute shader updates the texture by using simulation parameters frame time (ifps) and dispatching GPU threads in 32x32 groups. Then the shader modifies the texture content using unordered access, with all calculations and writes handled fully on the GPU. The CPU is only responsible for initial setup and parameter updates.


The compute shader is used to perform custom operations on textures, allowing for real-time image manipulation or procedural content generation.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/compute_shader_image*
## FFP Depth-Tested Line Rendering

This sample demonstrates how to render custom visual elements (lines) using the *FFP* with depth testing enabled.


The elements are drawn during the visualizer stage and properly sorted with respect to scene geometry using the depth buffer.


The sample sets up a render callback via *[Render::getEventEndVisualizer()](../../../api/library/rendering/class.render_cpp.md#getEventEndVisualizer_Event)*, which is used to draw a simple line segment in camera space. Drawing is performed using *FFP*, with blending and depth-testing configured manually via *[RenderState](../../../api/library/rendering/class.renderstate_cpp.md)* class.


The scene features a red line intersecting the object. The projection matrix is modified to account for reverse depth and range remapping, ensuring correct visual sorting. The line vertices are transformed into camera space using the current modelview matrix, and rendered in screen space.


This sample can be used for fast rendering of various additional or debug elements (such as semi-transparent objects, frames, *3D* grids and coordinate systems, path traces, motion trails, line-of-sight visualization etc.) while ensuring consistency with the scene content.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/ffp_depth_tested_line_rendering*
## FFP Triangle Fan Rendering

This sample demonstrates how to render a simple 2D shape using the *[Fixed Function Pipeline (Ffp)](../../../api/library/rendering/class.ffp_cpp.md)* in UNIGINE via the C++ API. A colorful figure composed of 16 vertices is drawn directly on screen using orthographic projection.


The rendering logic is called every frame by hooking into the Engine's render loop. Ffp mode is enabled for drawing and then disabled, keeping this rendering isolated from the rest of the frame.


This approach is useful for quick visualization overlays, Editor tools, or debugging tasks where shader-based rendering isn't required.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/ffp_triangle_fan_rendering*
## Gbuffer Read

This sample demonstrates how to access *G-buffer* textures at different stages of the rendering process by configuring a custom *[Viewport](../../../api/library/rendering/class.viewport_cpp.md)* and intercepting its output at the [*G-buffer* rendering stage.](../../../principles/render/sequence/index.md#gbuffer)


A temporary viewport is used to render a selected node with a simplified pipeline to stop rendering after the *G-buffer* is filled. When the rendering reaches this stage, a callback is triggered to fetch *G-buffer* textures such as depth, albedo, normals, metalness, and roughness. These textures are then copied to user-defined render targets and displayed on screen planes using custom materials.


This setup is useful for debugging, material analysis, or developing post-processing effects that require direct access to the intermediate data in the rendering pipeline.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/gbuffer_read*
## Gbuffer Write

This sample demonstrates how to modify *G-buffer* textures at different stages of the rendering process by injecting a custom material at the end of the *G-buffer* pass.


An event handler is registered using *[getEventEndOpacityGBuffer()](../../../api/library/rendering/class.render_cpp.md#getEventEndOpacityGBuffer_Event)*, which is triggered once all *G-buffer* textures (albedo, normal, etc.) are populated. In this callback, a custom post-material is applied to modify the contents of these textures using dynamic parameters such as influence, plasticity, and color. Temporary render targets are used to perform intermediate writes, and the modified textures are then swapped back into the pipeline.


This technique allows real-time manipulation of *G-buffer* data during the rendering process, enabling custom surface effects or advanced material pre-processing.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/gbuffer_write*
## Gui To Texture

This sample demonstrates how to render GUI elements into a texture using *[Gui::render()](../../../api/library/gui/class.gui_cpp.md#render_void)*. Instead of drawing directly to the screen, the GUI is redirected to a custom framebuffer, which isolates its rendering pipeline and allows the resulting texture to be applied to materials.


The **GuiToTexture** component supports two update modes:


- In **Manual** mode, the texture is updated only when explicitly calling *renderToTexture()*. This is used in the **WidgetClock** example, where the GUI (a digital clock) is re-rendered once per second, only when the displayed time changes.
- **Automatic** mode is enabled by default and updates the GUI texture every frame. This is demonstrated in the **WidgetNoSignal** example, where a *"No Signal"* label moves across the screen like a screensaver. Because the position of the widget changes every frame, the texture must be continuously updated to reflect those changes.


The render flow involves saving and clearing the current render state, binding a texture, configuring the viewport, rendering the GUI widgets, and restoring the render state. Mipmaps are also generated to ensure proper filtering at different scales and distances.


You can use this sample to display dynamic GUI elements on in-game monitors, control panels, or other similar surfaces.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/gui_to_texture*
## Mesh To Mask Texture

This sample demonstrates how to render a mesh into a texture using a custom material, producing an image to be used as a mask. The mesh is rendered from a dedicated camera view directly into a texture, which is then assigned to the albedo slot of a preview material.


Use the manipulator to move the camera view and observe how different viewing angles affect the generated texture mask.


The sample compares two rendering approaches:


- **Renderer.RenderMesh** - standard camera-based rendering **(recommended for most use cases)**. The Engine automatically prepares matrices, render states, and shaders, so you only need to provide the mesh, material, transform, and camera.
- **MeshRender.Render** - low-level, **fully manual** projection and modelview setup. This method provides finer control over the rendering pipeline but requires explicit setup of projection and view matrices, RenderState configuration, and manual shader parameter management.


Both methods produce identical visual results, allowing you to choose whichever approach best fits your workflow.


This technique is useful for dynamic decals, procedural effects, or any feature requiring real-time texture generation from 3D geometry.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/mesh_to_mask_texture*
## Node To Texture

This sample demonstrates how to render a specific node and its children into a texture using *[Viewport::renderNodeTexture2D()](../../../api/library/rendering/class.viewport_cpp.md#renderNodeTexture2D_Camera_Node_Texture_int_int_int_void)*. Instead of rendering the whole scene, a custom viewport captures only the target node as seen from a camera, and outputs the result into a 2D texture.


The texture is then assigned as the material's albedo texture. To create clean output, the viewport is configured to skip transparent objects, velocity buffers, post-effects, and debugging visualizers. Lighting is inherited from the world, and the environment is overridden to a black cubemap to prevent background influence.


This sample can be useful for rendering character previews, dynamic item thumbnails, or isolated object views directly onto surfaces.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/node_to_texture*
## Procedural 3D Volume Texture Generation

This sample shows how to procedurally generate *3D* image data and use it as a density texture for a volume-based material in real time. The result is visualized using a volume box that updates dynamically every frame based on custom field simulation.


The sample initializes a *3D* image with a predefined resolution and fills it with voxel data derived from a set of moving fields. Each field represents an abstract spherical influence zone that contributes to the voxel density based on distance. Field dynamics are updated every frame to simulate motion.


The raw image data is accessed directly via a pixel pointer and modified per frame, with density values mapped to *RGBA* channels. The resulting image is then uploaded to a material as a *3D* texture used in a volumetric shading model.


The sample demonstrates how to work with the *[Image](../../../api/library/common/class.image_cpp.md)* class and update *GPU* resources efficiently at runtime. This approach can be used for generating volumetric effects such as clouds, fog, or procedurally driven visual phenomena.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/procedural_3d_volume_texture_generation*
## Render Target

This sample demonstrates how to draw directly into a texture using the *[RenderTarget](../../../api/library/rendering/class.rendertarget_cpp.md)* class. The system initializes multiple textures, including a background layer and a dynamic result texture, which then is assigned to the object's material. The *[RenderTarget](../../../api/library/rendering/class.rendertarget_cpp.md)* is used to redirect rendering output from the main framebuffer to a texture, allowing full control over how sprites are composited. Each draw operation includes a UV-based transform to place and scale the sprite, and uses a custom material with direct access to the involved textures. After each draw, the result is blended with the background and mipmaps are generated for correct appearance at various distances. Sprites appear both on mouse clicks and automatically at random positions on the wall surface.


Render states are saved and restored around each operation to isolate the off-screen rendering flow from the rest of the pipeline.


This technique is suitable for creating effects like decal placement, user-driven painting, hit markers, or procedural texture overlays in real time.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/render_target*
## Screenshot

Simple demonstration of how to make a screenshot by grabbing the final image from the rendering sequence.
**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/screenshot*

## Split-Screen Texture

This sample demonstrates how to capture views from two different cameras into separate textures and implement a split-screen layout using the C++ API.


Each camera renders its output to a texture using *[Viewport::renderTexture2D()](../../../api/library/rendering/class.viewport_cpp.md#renderTexture2D_Camera_Texture_void)*. These textures are displayed in a vertical split-screen layout using *[WidgetSprite](../../../api/library/gui/class.widgetsprite_cpp.md)* elements, and at the same time are applied to surfaces by assigning them to the albedo slot of static mesh materials. The layout adjusts dynamically to screen size changes.


This setup can be used for multiplayer screen sharing, camera comparisons, CCTV-like monitors, or in-game monitors rendered from multiple viewpoints.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/split_screen_texture*
## Structured Buffer

This sample demonstrates how to compress a texture into **DXT1** format using compute shaders and structured buffers.


At initialization, a compute material is loaded, and a source texture is prepared. A *DXT1Block* structure is used to hold the compressed data, with its size based on the texture's dimensions (in 4x4 blocks). A structured buffer is created on the GPU to store the output.


The compute shader runs in two stages: a warm-up to trigger shader compilation and the actual compression pass. The number of compute groups is calculated dynamically from the texture size and thread group size to achieve efficient parallel execution.


When compression is complete, the GPU buffer is transferred to CPU memory asynchronously. A new image with the compressed data is created in **DXT1** format and saved to a `*.dds` file.


Open the Console (`) to view compression performance metrics and the saved file path location.


This method offloads all heavy processing to the GPU, minimizes CPU overhead, and takes advantage of structured memory access for optimal performance.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/structured_buffer*
## Textures

This sample demonstrates how to create and update procedural textures on static meshes in real time using the C++ API.


Each mesh is assigned a custom-generated image, which is updated every frame using a time-based color pattern. The pixel data is written manually into an *[Image](../../../api/library/common/class.image_cpp.md)* class instance, and the result is applied to the albedo texture slot of the mesh's material using *[Material::setTextureImage()](../../../api/library/rendering/class.material_cpp.md#setTextureImage_int_Image_int)*.


This method allows generating dynamic patterns, noise, or other procedural visuals without using compute shaders or external image files.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/textures*
## Visualizer

This sample demonstrates the full range of features provided by the *[Visualizer](../../../api/library/engine/class.visualizer_cpp.md)* class.


The sample illustrates how to use *Visualizer* for debugging node positions, physics vectors, bounding volumes, and custom geometry in both world space and screen space. Use controls to explore the area.


*VisualizerUsage.cpp* renders a wide range of primitives including points, lines, boxes, frustums, spheres, capsules, and object bounds using *Visualizer* methods.


*2D* visualizer features can be toggled on and off via the corresponding checkboxes.


Enable or disable depth testing, toggle specific primitives, and inspect how different rendering options behave in real time.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/visualizer*
## Weapon Clipping

In first-person games, weapon models can clip through walls or geometry when the camera gets too close. This sample solves the problem by rendering the weapon separately into a texture and compositing it over the main scene.


Two cameras with identical transforms are used to ensure alignment. Their [Viewport masks](../../../principles/bit_masking/index.md#viewport) are set via UNIGINE Editor in the following way: one renders the environment without the weapon, and the other renders only the weapon. The weapon view is drawn into a texture using *[Viewport::renderTexture2D()](../../../api/library/rendering/class.viewport_cpp.md#renderTexture2D_Camera_Texture_void)*, and then overlaid onto the screen with *[Render::renderScreenMaterial()](../../../api/library/rendering/class.render_cpp.md#renderScreenMaterial_cstr_void)*. The system handles window resizing, render-state isolation, and allows optional settings like skipping shadows in the weapon rendering pass.


This approach keeps the weapon always visible, even when the camera is close to walls, without interfering with the main rendering pipeline.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/rendering/weapon_clipping*
