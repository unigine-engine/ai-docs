# Fixed-Wing Template - Water Traffic Simulation


Water traffic populates the maritime part of the scene with vessels that follow closed routes and ride the waves of the *[Global Water](../../../objects/objects/water/water_object.md)* object. Together with *[background vehicle traffic](../../../sdk/templates/fixedwing/traffic.md)*, it makes the environment look inhabited from the air.


![](../modules/water_traffic/img/intro.png)


Each vessel is driven along an authored path and rides the wave surface sampled beneath it. This gives you full control over where the shipping lanes run, at a low cost, with the CPU budget reserved for the core aspects of the simulation.


**Key Features:**


- **Authored, repeatable routes**: every vessel follows a path you lay out in the Editor.
- **Low performance cost**: movement reduces to spline evaluation and three wave-height samples per vessel per frame, with no physics solver involved.
- **Synchronization support**: vessels are **IG** entities, so their state is replicated across the *[Syncker](../../../code/plugins/syncker/index.md)* network together with the rest of the entity traffic.


Movement is implemented via the `EntitySplineMovement` component, with each route in the scene representing an independent vessel.


The routes and vessel models shipped with the template demonstrate the capabilities of the framework and serve as a starting point for your own scene: you lay out the shipping lanes your scenario requires and plug in your own vessel models. To adapt water traffic to your own project, see *[configuring water traffic for your project](../../../sdk/templates/fixedwing/custom.md#custom_water_traffic)*.


## Route Structure


All routes are grouped under a single *NodeDummy* named `ship_paths`. Each route inside it (`path`, `path_1`, ...) is a container node carrying the component, and its direct children are the route points. No separate *[WorldSpline](../../../objects/worlds/world_spline_graph/index.md)* node is involved: the path is built at runtime from the world positions of the children as a Catmull-Rom spline, so authoring a lane comes down to placing the waypoints where the vessel should pass.


![](../modules/water_traffic/img/hierarchy.png)


The route is closed automatically - the end point is connected back to the first one, so the vessel travels in a loop indefinitely.


> **Notice:** The spline is built at initialization from the world positions of the *waypoints*.


## Vessel Entities


The vessel models are not part of the scene hierarchy - they are **IG** entities, created at runtime from the types declared in the *[<entity_types>](../../../ig/config.md#config_entities)* section of the `ig_config.xml` file, the same way the aircraft itself is.


The component identifies its vessel by two parameters:


- *[Entity Type](#entity_type)* selects the declared model
- *[Entity Id](#entity_id)* identifies the individual instance


A single type can back any number of instances, so the same model can sail several routes at once. And because the vessels are regular IG entities, their movement replicates across the *[Syncker](../../../code/plugins/syncker/index.md)* network on its own.


## Framework Logic


Every frame the component performs two steps for each vessel: it *[advances](#logic_movement)* the vessel along its route, and then *[settles](#logic_water)* it onto the wave surface.


### Movement Along the Route


The vessel advances along the spline over time, at a rate set by the *[Speed](#speed)* parameter. The route is traversed as a whole rather than segment by segment, so the vessel keeps moving at the same pace regardless of how densely the waypoints are placed.


Heading is not stored in the route: every frame the vessel is aimed at the spline position just ahead of its current one, so the hull follows the curve continuously instead of turning at the waypoints. The resulting position and orientation are passed to the entity as geodetic coordinates and Euler angles.


### Putting the Vessel on Water


The route defines only where the vessel goes, not how it sits on the water. Once the vessel has been placed on its route, the wave surface is measured around that position, and the hull is fitted to it: the route keeps the vessel on its lane, while the waves affect only its height, roll and pitch. Three sampling points are placed around the vessel, spaced 120 degrees apart, forming a triangle centered on it. The wave height is fetched at each point, and the triangle they form becomes the surface the vessel is aligned to: its average height gives the vertical position, and its tilt gives roll and pitch.


The points are placed at the radius of the *[bounding sphere](../../../api/library/math/bounds/class.boundsphere_cpp.md)* enclosing the vessel and its child nodes, scaled by *[Radius Factor](#radius_factor)*. The smaller the radius, the more the vessel responds to short waves, while a larger one averages them out, leaving only the broader swell.


The remaining parameters adjust the result: *[Z Offset](#z_offset)* shifts the vessel vertically to account for its draft, and *[Inertion](#inertion)* smooths both height and rotation over time, so the vessel eases onto the wave instead of snapping to it.


The *Global Water* object is searched for once at initialization, by iterating over all nodes of the world.


> **Notice:** Water traffic requires a *Global Water* object in the scene, as wave heights are fetched from it every frame.


## EntitySplineMovement Component


The `EntitySplineMovement` component property is assigned to the *NodeDummy* container of a route and exposes the following parameters:


![](../modules/water_traffic/img/component.png)


| Entity Type | The template type defining which model IG loads. Must be declared in the `<entity_types>` section of the *[ig_config.xml](../../../ig/config.md)* file. Reused by multiple instances. |
|---|---|
| Entity Id | The entity instance. Each route must have its own unique ID. |
| Speed | The speed at which the vessel advances along the route, in meters per second. |
| Inertion | The rate at which the vessel adjusts to the wave. |
| Z Offset | Vertical offset that defines the draft of the vessel. In the template, `supply_ship` uses -6, while boats use 0. |
| Radius Factor | Multiplier applied to the bounding sphere radius of the vessel, including its child nodes, to define the distance at which the wave height is measured. |
