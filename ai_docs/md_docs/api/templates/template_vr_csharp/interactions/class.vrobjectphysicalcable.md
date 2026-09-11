# VRObjectPhysicalCable Component

**Inherits from:** Component


VRObjectPhysicalCable creates a physics-based cable between two endpoints. The cable is constructed from spherical physics bodies connected by joints, with a procedural mesh rendered on top. Each end can have a **[VRPluggable](../../../../api/templates/template_vr_csharp/interactions/class.vrpluggable.md)** plug attached.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Cable Start | *Node* | Start point node of the cable. |
| Cable End | *Node* | End point node of the cable. |
| Material | *Material* | Material applied to the cable mesh. |
| Num Segments | *Int* | Number of physics segments in the cable. |
| Collision Mask | *Mask* | Collision mask for cable segments. |
| Socket ID | *Int* | Socket ID assigned to plugs at cable ends. |
| Socket ID For Cable Segments | *Int* | Socket ID for cable segment bodies. |
| Cable Radius | *Float* | Visual radius of the cable mesh. |
| Slices | *Int* | Number of circular slices in the cable mesh cross-section. |
| Subdivisions | *Int* | Number of length subdivisions per segment in the cable mesh. |
| Are Ends Fixed | *Bool* | Whether cable endpoints are fixed in place. |
| Max Impulse | *Float* | Maximum impulse for cable joints. |
| Sphere Mass | *Float* | Mass of each cable segment sphere. |
| Sphere Radius | *Float* | Collision radius of each cable segment sphere. |
| Segment Length | *Float* | Length of each cable segment. |


### See Also


- **[VRPluggable](../../../../api/templates/template_vr_csharp/interactions/class.vrpluggable.md)**
- **[VRSocketObject](../../../../api/templates/template_vr_csharp/interactions/class.vrsocketobject.md)**


## VRObjectPhysicalCable Class
