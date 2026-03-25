# Unigine.VRMarkerObject Class (CS)


The class is used for managing a Varjo object marker. Varjo markers are typically used in mixed reality applications, but can be also used without video pass-through rendering in virtual reality applications to align virtual objects in the scene with physical objects in the real world.


Object markers are used to track static or dynamic objects in the user environment. You can use the object markers in both XR and VR applications. Each marker has a unique ID, and you shouldn't use the same marker more than once in any given environment. For added precision, an application can use multiple markers to track a single object. You can, for example, track a monitor by placing a marker in each corner.


To obtain a marker object and retrieve information from it, use the *[GetMarkerObject()](../../../api/library/vr/class.vrmixedreality_cs.md#getMarkerObject_short_VRMarkerObject)* or *[GetMarkerObjectByID()](../../../api/library/vr/class.vrmixedreality_cs.md#getMarkerObjectByID_short_VRMarkerObject)* methods of the **[VRMixedReality](../../../api/library/vr/class.vrmixedreality_cs.md)** class.


## VRMarkerObject Class

### Properties

## 🔒︎ int ID

The unique ID of the marker object.
## 🔒︎ mat4 Transform

The marker pose transformation.
## 🔒︎ mat4 WorldTransform

The marker pose transformation in global space.
## 🔒︎ vec3 Size

The size of the marker.
## 🔒︎ vec3 Velocity

The linear velocity.
## 🔒︎ vec3 AngularVelocity

The angular velocity.
## 🔒︎ vec3 Acceleration

The acceleration.
## 🔒︎ long RawTimestamp

The timestamp of the pose. This represents the time the pose has been extrapolated to.
## 🔒︎ double Confidence

The tracker confidence.
## 🔒︎ int PoseFlags

The bit field value describing pose.
## bool Dynamic

The value indicating if the marker is tracked as dynamic (the marker pose is predicted).
## float Lifetime

The lifetime of the marker.
### Members

---

## void RenderVisualizer ( )

Renders visualizer for the marker object.
