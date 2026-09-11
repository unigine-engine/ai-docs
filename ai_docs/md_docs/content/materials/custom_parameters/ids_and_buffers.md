# Surface ID, Material ID and Buffers


## How the Lookup Works


Let's look in detail at what happens when a Surface ID is sampled from a buffer. The mechanism itself is a chain of lookups, and it starts from a pixel.


Every pixel on the screen carries a number - the Surface ID of whatever surface was drawn there. It is stored in a **FORMAT_R32U** buffer - one 32-bit integer per pixel. Geometry is split into categories, and the buffers follow that split:


- one buffer per category - opaque geometry (the Surface ID plane of the G-buffer), transparent geometry, decals and water;
- and the Scene Buffer - the categories composited into one.


Not all four of those buffers exist at all times - which of them do is decided by the *[Multilayered](#modes)* setting.


The values of one surface sit in a slot of that frame's parameter buffer, and what the slot holds is the parameter block: the declared values plus the built-in fields.


The Surface ID is the key to everything else:


| Starting from | Look it up in | And you get |
|---|---|---|
| A pixel | A Surface ID Buffer | The Surface ID of the surface drawn at that pixel |
| A Surface ID | The surface parameter block of that ID | The custom values declared for that surface - and its Material ID |
| A Material ID | The material parameter block of that ID | The custom values of the material |


Two things follow from this:


- When a category has a buffer of its own, one pixel holds an answer per category rather than only the topmost one - which is what [Surface ID Buffers and the Multilayered Mode](#modes) is about;
- Inside a *[Mesh Cluster](../../../objects/objects/mesh_cluster/index.md)* every visible instance surface gets a slot of its own, so instances are distinguishable in the rendered output without any extra setup. A *[Mesh Clutter](../../../objects/objects/mesh_clutter/index.md)* is the opposite - all instances of one of its surfaces share a single ID, and therefore a single set of values.


## Surface ID and Material ID


IDs are managed by the engine, not authored. A Surface ID is also **frame-local**. Every frame the renderer goes through the surfaces it is about to draw for a given view and numbers them one by one, so the number is unique inside that frame and that view - and is not a name the surface keeps. Change what is visible, or draw the same scene from a second camera, and the same surface gets a different number.


Renumbering does not affect setting and reading values: they live on the node and its surface, and the renderer puts them into the slot it has just numbered. The number itself, however, must not be stored, compared between frames, or used to derive anything that has to look the same twice - a color keyed on it would flicker as the view changes, and two cameras looking at the same surface would disagree. What to use instead is in the block itself: the node, surface and instance numbers, which hold while the world is loaded, or a declared parameter of your own, which holds across runs as well.


A **Material ID** works differently. It is allocated when the material is registered and stays with it until it is unloaded. Because the number holds, an application can ask for it with *[*Material::getMaterialID()*](../../../api/library/rendering/class.material_cpp.md#MaterialID)* and keep it for as long as the material stays loaded. This is the one ID the API lets you request directly. For the same reason a segmentation view colored by material does not change from frame to frame. There is no getter in the other direction: no method takes an ID and returns the material. An application that needs such a lookup keeps a map of its own, built once rather than resolved every frame. The map has to be rebuilt whenever materials are loaded or unloaded, because a released number goes back to the pool and is given to another material.


Whether a material gets an ID depends on its type:


- Materials that draw geometry (mesh, decal or particles ones) get an ID as soon as they are registered, even if nothing in the scene uses them.
- Materials that draw no geometry (a post-effect one for instance) never get an ID, and *[*getMaterialID()*](../../../api/library/rendering/class.material_cpp.md#MaterialID)* returns *[*MATERIAL_ID_NONE*](../../../api/library/rendering/class.material_cpp.md#MATERIAL_ID)* for them.


> **Warning:** Do not use a Material ID as a label that has to survive a restart. IDs are assigned in the order materials load, so adding or removing a material in the project shifts them in the next run. Within one session they can be relied on, which is enough for a view rendered and used right away. For labels that must match across runs, declare an integer parameter of your own and write your category into it.


IDs are assigned starting from *[*Render::SURFACE_ID_RESERVED_NUM*](../../../api/library/rendering/class.render_cpp.md#SURFACE_ID)*, and everything below it is reserved: those values never belong to a real surface, so a 0 read out of the buffer means that nothing was written to that pixel, not that it belongs to surface number zero:


- *[*Render::SURFACE_ID_NONE*](../../../api/library/rendering/class.render_cpp.md#SURFACE_ID)* (0) - no surface, or no ID allocated
- *[*Render::SURFACE_ID_SKY*](../../../api/library/rendering/class.render_cpp.md#SURFACE_ID)* (1) - the sky


Material IDs have reserved values of their own, with the same meanings and their own names: *[*Material::MATERIAL_ID_NONE*](../../../api/library/rendering/class.material_cpp.md#MATERIAL_ID)*, *[*Material::MATERIAL_ID_SKY*](../../../api/library/rendering/class.material_cpp.md#MATERIAL_ID)* and *[*Material::MATERIAL_ID_RESERVED_NUM*](../../../api/library/rendering/class.material_cpp.md#MATERIAL_ID)*. The two sets are separate enums, so a constant from one should not be used with the other, even where the numbers currently coincide. Both sets are available from the API and from a shader alike.


In a shader an ID answers three questions:


- **isValid()** asks whether this is a real surface, rather than one of the reserved values;
- **isEmpty()** asks whether nothing was written at that pixel;
- **isSky()** asks whether the pixel is the sky.


A shader-side **MaterialID** has the same three. [In a Shader](../../../content/materials/custom_parameters/reading_parameters.md#shader_uusl) shows how a buffer is read, and *[UUSL Surface and Material Parameters](../../../code/uusl/custom_parameters.md#ref_buffers)* lists every getter with its arguments.


## Surface ID Buffers and the Multilayered Mode


Splitting the buffers by category is what lets one pixel be asked more than one question. By default there is one buffer for everything: each stage writes over what the previous one left, a pixel answers with the surface on top, and a windscreen, a wall decal or a water surface hides what is behind it.


A sensor that must not react to glass is the shortest example. With *Multilayered* on it reads the Opaque Buffer, which now holds only opaque IDs, and ignores the rest. If *Multilayered* is disabled, the only way to keep the glass out of it is to stop the glass from writing its Surface ID - which also takes away its [material mask](../../../principles/bit_masking/index.md#material_mask) and puts its feature bits out of reach (the engine's own depth of field and motion blur read those through the Surface ID), and can cost the material its G-buffer pass.


The buffers can also be read one after another, which is what an effect tracing a ray needs. The ray passes through the glass or the water, bounces off a decal, lands on the opaque surface behind it, and comes back the same way; at each of those points the effect reads the buffer of the matching category, so it knows which surface the ray met and what values that surface carries.


Every buffer is **FORMAT_R32U**: one 32-bit Surface ID per pixel.


Opaque geometry always writes its Surface ID into the G-buffer, which is available as a texture through *[*Renderer::getTextureGBufferSurfaceID()*](../../../api/library/rendering/class.renderer_cpp.md#TextureGBufferSurfaceID)*. Whether transparent geometry and water get buffers of their own is decided by one setting - **render_surface_id_multilayered**, also reachable as *[*Render::setSurfaceIDMultilayered()*](../../../api/library/rendering/class.render_cpp.md#SurfaceIDMultilayered)* / *[*Render::isSurfaceIDMultilayered()*](../../../api/library/rendering/class.render_cpp.md#SurfaceIDMultilayered)*:


- **Disabled** (by default) - transparent geometry and water write their IDs into the Scene Buffer on top of the opaque ones, so a pixel answers with whatever covered it last. Neither of the two gets a buffer of its own, so the shader getters **getTransparentSurfaceID()** and **getWaterSurfaceID()** yield **SURFACE_ID_NONE**, and **isTransparentSurfaceIDAvailable()** and **isWaterSurfaceIDAvailable()** return false
- **Enabled** - transparent geometry and water each get a buffer of their own whenever they have something to draw, and those checks return true, so a pixel can be asked separately what the transparent stage wrote there and what lies under it. The stages are composited into the Scene Buffer as well


> **Notice:** Decals stand outside this choice. A decal reads the Surface ID of the geometry underneath while it is being drawn and writes its own, so it cannot share a target with it: the Decal Buffer is allocated in either mode, and **isDecalSurfaceIDAvailable()** always returns true.


Allocation is per frame and per stage. A stage that has nothing to draw gets no target at all, and its getter then reads **SURFACE_ID_NONE** everywhere, the same answer an unconfigured stage gives. That happens when no transparent surface is in view, or when no decal has *Write Surface ID* enabled. Every target that does get allocated costs one full-screen texture in video memory: **FORMAT_R32U**, four bytes per pixel, about 8 MB at 1920x1080.


The setting has a checkbox of its own: *Settings -> Runtime -> World -> Render -> [Custom Parameters](../../../editor2/settings/render_settings/custom_parameters/index.md)*, *[Multilayered](../../../editor2/settings/render_settings/custom_parameters/index.md#multilayered)*, above the tabs with the parameter declarations. Pressing *Save* stores it with the project, though in a file of its own rather than together with the declarations - see [Where Declarations and Settings Are Saved](../../../content/materials/custom_parameters/declaring_and_setting_cpp.md#declare_storage).


> **Notice:** The Scene Buffer can be read whatever the *Multilayered* setting is, which is why **getSceneSurfaceID()** and **getSceneSurfaceParameters()** are the default choice. The per-stage buffers are needed only when one pixel has to be read layer by layer: the Transparent Buffer gives the windscreen, and the opaque one gives the driver behind it.


Writing the ID is a per-material state. Only some geometry needs it switched on, and where the ID is written depends on the mode:


| Geometry | Where the ID is written | What has to be enabled |
|---|---|---|
| Opaque geometry | Surface ID Buffer of the G-buffer | nothing - always written |
| Water | Water Buffer while *Multilayered* is on, Scene Buffer otherwise | nothing - always written |
| Alpha-blend geometry (*Transparent* set to *Alpha Blend*) and particles | Transparent Buffer while *Multilayered* is on, Scene Buffer otherwise | *Surface ID* (transparent_surface_id), off by default |
| Decals | Decal Buffer, in either mode | *Write Surface ID* (surface_id_write), off by default |


Where that toggle sits depends on what kind of material it is:


- a **mesh** material - the *Buffers* group of the material parameters, which holds exactly four switches: *Scene Depth*, *Opacity Depth*, *Velocity* and *Surface ID*. The group shows up only when *Transparent* is set to *Alpha Blend*, because that is the only case where there is a choice to make;
- a **particles** material - the same *Buffers* group, which also holds *Threshold*: a particle fragment is written into the buffer only while its alpha is above that value, 0.5 by default;
- a **decal** material: the *Options* group, as *Write Surface ID*. A decal built on a [material graph](../../../content/materials/graph/index.md): the switch above the groups labelled *Surface Id Write*;
- a **material graph** - the *Write Surface ID* checkbox in the graph settings, shown for transparent and decal graphs only, for the same reason. It is off in a newly created graph.

  ![](enable_surface_id_mesh.png)  ![](enable_surface_id_particles.png)  ![](enable_surface_id_decal.png)  ![](enable_surface_id_mgraph.png)
From code it is an ordinary material state, set by name:


```cpp
// alpha-blend mesh and particles materials
material->setState("transparent_surface_id", 1);

// decal materials
decal_material->setState("surface_id_write", 1);

```


Writing is off by default on purpose, and switching it on costs two different things:


- a write per covered fragment - one integer into the buffer, whatever the mode. On top of that a target may have to be allocated: a full-screen **R32U** texture, about 8 MB at 1920x1080. Decals get one as soon as any decal writes an ID; transparent geometry and water get one only while *Multilayered* is on, because in the default mode their IDs go into the Scene Buffer, which exists anyway;
- for an alpha-blend mesh or a particles material, the G-buffer pass itself. Such a material skips that pass entirely while none of its deferred buffers is written, and *Surface ID* is one of them - the others being *Opacity Depth*, *Velocity* and, for a mesh material, the graph-only *[Write Reactivity](../../../content/materials/graph/index.md#transparent_settings)*. *Scene Depth* is not in that count, so switching it on does not hold the pass open on its own.


The *Surface ID* state (**transparent_surface_id**) also governs the classic [material mask](../../../principles/bit_masking/index.md#material_mask) of transparent geometry.


> **Warning:** The state governs the *buffers*, not the parameter block. A surface that writes no ID is invisible to every reader that starts from a pixel: a post-effect, a segmentation pass, picking, and the engine's own depth of field and motion blur, which judge the pixel by the [feature bits](../../../content/materials/custom_parameters/reading_parameters.md#shader_uusl) of whatever the buffer does hold there. Its own material is not affected - the ID arrives with the draw call either way, so the *[Current Surface Parameters](../../../content/materials/graph/node_library/input/current_surface_parameters.md)* node still reads the surface's own values.


The buffers are exposed as textures:


- *[*Renderer::getTextureSurfaceIDScene()*](../../../api/library/rendering/class.renderer_cpp.md#TextureSurfaceIDScene)* - the composed scene
- *[*Renderer::getTextureSurfaceIDTransparent()*](../../../api/library/rendering/class.renderer_cpp.md#TextureSurfaceIDTransparent)* and *[*Renderer::getTextureSurfaceIDWater()*](../../../api/library/rendering/class.renderer_cpp.md#TextureSurfaceIDWater)* - the per-stage buffers. These API getters do not mirror their shader counterparts: while the setting is off they hand out the Scene Buffer, which is where those stages actually wrote, whereas the shader getters report **SURFACE_ID_NONE**. With the setting on but the stage empty there is no target either, and the getter returns NULL
- *[*Renderer::getTextureSurfaceIDDecal()*](../../../api/library/rendering/class.renderer_cpp.md#TextureSurfaceIDDecal)* - the Decal Buffer regardless of the *Multilayered* setting, and NULL in the same situation: a frame where no decal wrote an ID and no target was allocated


## Visual Debugging


The [Rendering Debug](../../../editor2/rendering_debug/index.md) panel visualizes the buffers directly, as *Surface ID* and *Material ID* modes: *Opaque*, *Decal*, *Transparent*, *Water* and *All* - the last one being the composed Scene Buffer, every category stacked into one. The *Transparent* and *Water* modes are greyed out while [multilayered Surface ID](#modes) is off, because there is no buffer behind them; the other three always work.


The panel draws the IDs themselves, not the values stored under them. To check a value, output it with a post-effect of your own: [Quick Start](../../../content/materials/custom_parameters/quick_start.md) builds such a material, and the same graph with its output simplified serves as a debug view.
