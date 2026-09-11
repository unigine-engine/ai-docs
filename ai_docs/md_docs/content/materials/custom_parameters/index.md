# Custom Parameters for Surfaces and Materials


**Custom parameters** are named values of your own. You attach them to individual surfaces of your scene, and read them back while the frame is rendered. Each surface carries a separate set of values, so two surfaces of the same object can describe entirely different properties, even when they share a material.


The renderer knows nothing about such a value, but effects can be built on it: a class number for a segmentation pass, a flag for outlining a picked object, a temperature a thermal view reacts to. What the values mean is up to the project. The engine only delivers them to the pixel where the surface was drawn.


Materials can carry custom parameters of their own too, in a separate set shared by everything using them. That is where a property of the substance belongs - the backscatter coefficient of sheet metal, the emissivity of asphalt - so that it is filled in once and answers for every surface made of it. [Choosing Where a Value Belongs](#choosing) compares the two.


[Use Cases](#usecases) describes the tasks this solves, and [Quick Start](../../../content/materials/custom_parameters/quick_start.md) takes one of them from an empty project to a working image.


## See also


The rest of this section:


- *[Quick Start](../../../content/materials/custom_parameters/quick_start.md)* - a surface parameter and a material one, from an empty project to a working image
- *[Surface ID, Material ID and Buffers](../../../content/materials/custom_parameters/ids_and_buffers.md)* - how the IDs are assigned, where they are written, and how to look at them
- *[Declaring Parameters and Setting Values](../../../content/materials/custom_parameters/declaring_and_setting_cpp.md)* - the layout, and every place a value can be written
- *[Reading Parameters](../../../content/materials/custom_parameters/reading_parameters.md)* - in a shader and in a material graph


The shader-side reference:


- *[UUSL Surface and Material Parameters](../../../code/uusl/custom_parameters.md)* - the generated structures, the defines behind them, and every function that reads a block


Related articles:


- *[Custom Materials](../../../content/materials/custom.md)*
- *[Material Editor](../../../content/materials/graph/index.md)*
- *[UUSL: GBuffer](../../../code/uusl/gbuffer.md)*
- *[Using Visual Debugging](../../../editor2/rendering_debug/index.md)*
- *[GlobalConfig](../../../api/library/engine/class.globalconfig_cpp.md)* class


Samples using custom parameters:


- *[Simulation](../../../sdk/api_samples/sim_cpp/simulation.md)* - C++ SIM samples
- *[Simulation](../../../sdk/api_samples/sim_cs/simulation.md)* - C# SIM samples


## Use Cases


### Segmentation and Ground-Truth Views


[![](classification.jpg)](classification.jpg)


A perception dataset needs more than the picture: every frame has to come with maps saying what each pixel is - the substance, the category, the individual object.


Custom parameters make those maps part of the scene. The same frame is rendered again with a value in place of the color, so a map matches the geometry exactly, nothing is outlined by hand, and no second set of assets is needed. One scene can serve several labelings: a run that keeps cars and trucks apart writes different numbers than a run where both are simply vehicles, and neither the geometry nor the materials change.


| View | What it colors by | Where the value comes from |
|---|---|---|
| **Material** | What a surface is made of - glass, metal, asphalt, foliage, sky | The Material ID every surface already carries, so nothing has to be created for it |
| **Class** | What kind of thing it is - car, building, pedestrian, road | A class_id surface parameter: a category belongs to the object, not to the substance it is made of |
| **Instance** | Which particular thing it is, so that two cars of the same model can be told apart | An instance_id surface parameter, assigned as the scene is populated |


Transparency is covered too: with [multilayered Surface ID](../../../content/materials/custom_parameters/ids_and_buffers.md#modes) one pixel labels both the windscreen and the driver behind it, instead of only the surface on top.


### One Material for a Whole CAD Model


An imported CAD assembly often has thousands of surfaces with the same material on all of them, and the engineer still has to see where one part ends and the next begins.


Custom parameters give every part a look of its own without anything being authored per part: the material stays one, the parts still batch into one draw call, and no asset is duplicated. The color can be arbitrary, just to tell the parts apart. It can also mean something, such as an assembly group or a maintenance status, if the project writes its own number into a declared parameter.


The same values serve as a source of variety where one asset is repeated to build a large structure: a slightly shifted hue, roughness or set of texture coordinates turns one part repeated into many similar parts, at no cost in materials or textures.


### Per-Instance Appearance


Scenes are built from repeated geometry: a parking lot filled with one car model, a crowd made from three characters, an orchard placed as a *[Mesh Cluster](../../../objects/objects/mesh_cluster/index.md)*. The geometry is meant to repeat, the look is not.


Every surface, and every instance of a *Mesh Cluster*, has values of its own, so a tint, a livery or a variation index becomes a number instead of a new asset. The instances keep sharing the mesh and the material and are still drawn together, so variety costs no extra memory and no extra draw calls. It can also change while the application runs: repaint a car, mark a tree as burnt, and nothing is reloaded.


### Radar, Thermal and Lidar Views


[![](thermal.jpg)](thermal.jpg)


A sensor reacts to what a camera does not: a radar to backscatter, a thermal imager to temperature, a lidar to reflectance at its own wavelength. A PBR material holds none of that.


Custom parameters let a project keep such attributes in the scene itself: a backscatter coefficient on the **material**, so that a whole scene is described by the handful of materials it is built from, and the velocity of a target or the temperature of a pipe on the **surface**. The values can be rewritten while the application runs, so the sensor image follows the simulation, and one "steel" material serves a cold pipe and a hot one without the material library being forked to hold sensor data.


With [multilayered Surface ID](../../../content/materials/custom_parameters/ids_and_buffers.md#modes), transparent geometry and water get Surface ID Buffers of their own, so one pixel holds a value in each buffer instead of only the one from the surface on top. A sensor can read a single buffer and ignore glass and water. It can also read several buffers and add the results: a lidar beam partly reflects off a windscreen and partly off the driver behind it, and both returns are available only when both buffers are read. Without the setting, the pixel holds the windscreen alone.


### Picking, Selection and Highlighting


Picking, selection and highlighting all begin with the same question: what is the user pointing at? The answer is available for any pixel of the frame, down to one surface of one instance, including a surface seen through a windscreen or through water.


Highlighting then costs one integer: mark the selected surfaces, and a post-effect outlines them. No material is swapped and no asset is duplicated, so a thousand parts light up as cheaply as one, and the selection can change every frame.


### Wetness, Wear and Other Changing Values


Some values keep changing while the application runs: wetness after rain, snow, dirt, scorching, wear, the maintenance status of a component in a digital twin.


As a custom parameter, one number serves the picture and the logic at once. The shader shades the surface with it, and the application reads the same number back, so nothing has to be kept in sync by hand and no material is duplicated per state. A wet surface and a dry one are the same asset with different values, and the change shows on the object itself rather than only in a picture drawn over it.


## How It Works


To work with the feature, you need to know three concepts:


| Concept | What it is |
|---|---|
| Custom parameter | A value you declare once for the whole project: a name, a type (float, int or uint) and a default. It is declared in one of two independent layouts, the surface one or the material one. Every surface, or every material, then has a field for it |
| Surface ID | The number the engine gives every surface it renders, valid for that one frame and that one view. You never assign it: it is what the renderer uses to find the values that belong to the surface drawn at a given pixel, which makes it a lookup key and never an identity to store - see [Surface ID and Material ID](../../../content/materials/custom_parameters/ids_and_buffers.md#ids) |
| Material ID | The same for materials, so a shader can also reach the values shared by every surface that material is assigned to. Unlike a Surface ID it is **not** frame-local: a material keeps its ID for as long as it stays loaded |


On a single house it looks like this. The metal roof has a **Surface ID** of its own and a **Material ID** of its own; the plastered walls have theirs. Two values were declared for surfaces and filled in on the roof, and two more were declared for materials and filled in on the metal that roof is made of.


![A house whose roof and walls are made of different materials, the surface and material parameter blocks of the roof, and the four views built from them](custom_parameters_views.svg)


Each of the values feeds a different view of the same frame:


| View | From | What it shows |
|---|---|---|
| **Surface parameters** |  |  |
| Classification | class_id | Every part painted with the color of the class it belongs to. Roof and walls are both building and share a color although their materials differ, while the same metal used for a car body would have to answer vehicle |
| Highlight | selected | The roof outlined as long as the integer holds anything but 0. It marks this one roof at this one moment, not the metal it is made of |
| **Material parameters** |  |  |
| Radar | radar_gamma_db | A sensor view drawn from the backscatter coefficient of the substance. The roof answers with a bright echo and the plaster of the walls stays dark, because they are made of different things. Every other surface made of that same metal answers alike, with nothing filled in on it |
| Emission | emission_boost | Everything made of that metal glowing at once |


The rule behind this split is in [Choosing Where a Value Belongs](#choosing).


The working order is always the same:


1. [Declare the parameters](../../../content/materials/custom_parameters/declaring_and_setting_cpp.md#declare) - once for the whole project.
2. [Fill in the values](../../../content/materials/custom_parameters/declaring_and_setting_cpp.md#values) - per surface, per instance, per decal or per material.
3. [Read them where you need them](../../../content/materials/custom_parameters/reading_parameters.md) - in a [material graph](../../../content/materials/graph/index.md) or in a custom shader, whether that is the material drawing the surface or a post-effect running over the finished frame.


## Choosing Where a Value Belongs


A custom value can be stored on a surface or on a material. The choice depends on how many surfaces one change to it should affect, and the short rule is: what a surface is **made of** goes on the material, what it **is** and what it is **doing right now** goes on the surface.


A value that describes the substance itself belongs on the material: the roughness of a glass, the emission boost of a lamp shade, the backscatter coefficient of sheet metal. It is then set in one place, and one change retunes every surface made of that material, instead of the same number being repeated per surface and kept in sync by hand. Surface parameters are for what varies **between** the surfaces that share a material: which class this one belongs to, which instance it is, how hot or how corroded it is at this moment.


The two are not an either-or. A sensor view usually needs both at once: the coefficient of the substance from the material, corrected by the state of this particular object from the surface. A single lookup delivers both, because the surface block carries the Material ID of the surface it belongs to. [Reading Parameters](../../../content/materials/custom_parameters/reading_parameters.md) shows that pair of reads.


| Changing the value should affect... | Stored in | Set with |
|---|---|---|
| every surface that uses the material | [Material parameters](../../../content/materials/custom_parameters/declaring_and_setting_cpp.md#values_material) | Material::setCustomParameter*() |
| one surface of one object, and nothing else that shares its material | [Surface parameters](../../../content/materials/custom_parameters/declaring_and_setting_cpp.md#values_surface) | setSurfaceRenderCustomParameter*() |
| one instance of a *[Mesh Cluster](../../../objects/objects/mesh_cluster/index.md)* | [Surface parameters](../../../content/materials/custom_parameters/declaring_and_setting_cpp.md#values_instance) | setInstanceCustomParameter*() |
| one decal | [Surface parameters](../../../content/materials/custom_parameters/declaring_and_setting_cpp.md#values_decal) | Decal::setSurfaceRenderCustomParameter*() |


> **Notice:** Surface and material parameters are two independent declarations, not one store seen from two sides. A name declared in one is unknown to the other.


## Limitations


| Limitation | Details |
|---|---|
| One global layout | Parameters are declared once for the whole project, not per material or per object type. Every surface carries the full block |
| Three types only | float, int and uint. There are no vector or texture parameters |
| A Surface ID is not an identity | It cannot be stored, compared between frames or used to key anything of your own. Use **unigine_node_id** / **unigine_surface** / **unigine_instance**, or a declared parameter - see [Surface ID and Material ID](../../../content/materials/custom_parameters/ids_and_buffers.md#ids) |
| A Material ID is not reproducible across runs | It does not change while the material is loaded, so within a session it can be relied on - but the numbers follow the order materials are loaded, so they shift between runs and whenever a material is added to the project. Labels that have to match across runs need a declared parameter, as [Surface ID and Material ID](../../../content/materials/custom_parameters/ids_and_buffers.md#ids) explains |
| No API lookup from an ID back to its owner | Neither a Surface ID nor a Material ID can be turned back into the node or material it belongs to. For a surface the reverse lookup exists shader-side only, through the node and surface fields of the block, and a [ray cast](../../../content/materials/custom_parameters/declaring_and_setting_cpp.md#values_surface) answers the same question directly in the application; for a material the application keeps [a map of its own](../../../content/materials/custom_parameters/ids_and_buffers.md#ids) |
| No per-instance values in a *[Mesh Clutter](../../../objects/objects/mesh_clutter/index.md)* | Every instance of a clutter surface is drawn with the same Surface ID, so instances share one set of values and cannot be told apart. A scattered forest that has to vary tree by tree needs a *[Mesh Cluster](../../../objects/objects/mesh_cluster/index.md)*, whose instances are addressable, or a source of variety other than the parameter block |
