# What's in the Scene (CPP)


The VR Template comes with a demo scene where you can grab, hold, throw, and use various objects. Start the application and you'll find a table with several primitive shapes, a laser pointer, and a button on its surface.


What each object can do is defined by the properties attached to it. For example, geometric primitives have the [ObjMovable](../../../api/modules/vr/components/objects/class.objmovable.md) property (grab, hold, throw), while the laser pointer also has [ObjLaserPointer](../../../api/templates/template_vr/objects/class.objlaserpointer.md) (emits a beam when activated).


## What's in the Scene


Here is what you can interact with in the demo scene:


### Movable Objects


Pick up any of the geometric primitives on the table -hold them, toss them around, watch them bounce off walls. When you let go, the object keeps the momentum of your hand. If the *Can Attach to Head* option is enabled, you can also toss the object near your headset and it will stick -useful for things like hats or visors.


![](movable_objects.png)


Built with: [ObjMovable](../../../api/modules/vr/components/objects/class.objmovable.md)


### Switches


Grab the button on the table to toggle it -it animates between two positions with a click.


![](switches.png)


Built with: [ObjSwitch](../../../api/modules/vr/components/objects/class.objswitch.md)


### Handles


Grab a lever or a valve and move it -handles constrain your motion to a specific axis or range, so they feel like real mechanical controls.


![](handles.png)


Built with: [ObjHandle](../../../api/modules/vr/components/objects/class.objhandle.md)


### Laser Pointer


Pick up the laser pointer and activate it -it casts a ray and shows the name of whatever you are pointing at.


![](laser_pointer.png)


Built with: [ObjMovable](../../../api/modules/vr/components/objects/class.objmovable.md), [ObjLaserPointer](../../../api/templates/template_vr/objects/class.objlaserpointer.md)


### Gun


Grab the gun and pull the trigger to fire. It shoots a ray from the muzzle with sound and visual effects, knocking physics objects on impact.


![](gun.png)


Built with: [ObjGun](../../../api/templates/template_vr/objects/class.objgun.md)


### Cables, Plugs & Sockets


Pick up a cable end and bring it close to a socket -it snaps in automatically. In the demo, connecting both ends of a cable to the generator powers on a lamp and opens a door.


![](cables.png)


Built with: [VRObjectPhysicalCable](../../../api/modules/vr/components/objects/class.vrobjectphysicalcable.md), [VRPluggable](../../../api/modules/vr/components/objects/class.vrpluggable.md), [VRSocketObject](../../../api/modules/vr/components/objects/class.vrsocketobject.md)


### Inventory


Open the inventory and throw an object toward the grid -it snaps into a free cell. Grab it back to take it out.


![](inventory.png)


Built with: [VRInventory](../../../api/modules/vr/components/objects/class.vrinventory.md), [VRInventoryItem](../../../api/modules/vr/components/objects/class.vrinventoryitem.md)


### Platforms


Step onto a moving platform -it carries you along, automatically compensating for its velocity so you stay stable.


Built with: [ObjectPlatform](../../../api/modules/vr/components/objects/class.objectplatform.md)


For a complete list of all classes and components, see the [Classes & Components Reference](../../../vr_development/vr_template/vr_template_classes_and_components/index_cpp.md).
