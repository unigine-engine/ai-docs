# Dummy Body


**Dummy body** is a static body, that does not move and has no physical properties. It is used as a prop to attach other bodies with [joints](../../../../principles/physics/joints/index.md) to.


- If a *Dummy body* is assigned to a *[Dummy Object](../../../../objects/objects/dummy/index.md)*, it is completely invisible.
- If a *Dummy body* has a [shape](../../../../principles/physics/shapes/index.md), it can collide with other physical objects. They will bounce off or slide along it in accordance with their parameters, but a *Dummy body* will always stay in place.


On the picture below you can see a dummy object with a *Dummy body* and without any collision shape. It pins the physical [cloth](../../../../principles/physics/bodies/cloth/index.md) so it can hang without any rack. At the same time, it does not collide with balls that roll through it.


![Dummy body](dummy_body_sm.jpg)

*An invisibleDummy body(with assigned shape) used to pin a cloth body to*


### See also


- *[BodyDummy](../../../../api/library/physics/class.bodydummy_cpp.md)* class
- Overview of the *[Dummy body](https://youtu.be/w_GJrE-6HtI?t=678s)* in the video tutorial on physics


## Assigning a Dummy Body


To assign a *Dummy body* to an object via [UnigineEditor](../../../../editor2/index.md) perform the following steps:


1. Open the *[World Hierarchy](../../../../editor2/interface/index.md#world_hierarchy)* window.
2. Select an object to assign a *Dummy body* to.
3. Go to the ***Physics*** tab in the *[Parameters](../../../../editor2/interface/index.md#parameters)* window and assign a physical [body](../../../../principles/physics/bodies/index.md) to the selected object by selecting *Body -> **Dummy***. ![Adding a body](../add_body.jpg)
4. Set body's name and change other parameters if necessary.
