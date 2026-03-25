# Unigine.VRMarkerObject Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The class is used for managing a Varjo object marker. Varjo markers are typically used in mixed reality applications, but can be also used without video pass-through rendering in virtual reality applications to align virtual objects in the scene with physical objects in the real world.


Object markers are used to track static or dynamic objects in the user environment. You can use the object markers in both XR and VR applications. Each marker has a unique ID, and you shouldn't use the same marker more than once in any given environment. For added precision, an application can use multiple markers to track a single object. You can, for example, track a monitor by placing a marker in each corner.


To obtain a marker object and retrieve information from it, use the *[getMarkerObject()()](../../../api/library/vr/class.vrmixedreality_usc.md#getMarkerObject_short_VRMarkerObject)* or *[getMarkerObjectByID()()](../../../api/library/vr/class.vrmixedreality_usc.md#getMarkerObjectByID_short_VRMarkerObject)* methods of the **[VRMixedReality](../../../api/library/vr/class.vrmixedreality_usc.md)** class.


## VRMarkerObject Class

### Members

## int getID () const

Returns the current unique ID of the marker object.
### Return value

Current marker object ID.
## mat4 getTransform () const

Returns the current marker pose transformation.
### Return value

Current pose transformation.
## Mat4 getWorldTransform () const

Returns the current marker pose transformation in global space.
### Return value

Current pose transformation in global space.
## Vec3 getSize () const

Returns the current size of the marker.
### Return value

Current size in meters.
## Vec3 getVelocity () const

Returns the current linear velocity.
### Return value

Current linear velocity, in meters per second.
## Vec3 getAngularVelocity () const

Returns the current angular velocity.
### Return value

Current angular velocity, in radians per second.
## Vec3 getAcceleration () const

Returns the current acceleration.
### Return value

Current acceleration, in m/s2.
## long getRawTimestamp () const

Returns the current timestamp of the pose. This represents the time the pose has been extrapolated to.
### Return value

Current timestamp of the pose, in nanoseconds.
## double getConfidence () const

Returns the current tracker confidence.
### Return value

Current tracker confidence in range [0.0, 1.0].
## int getPoseFlags () const

Returns the current bit field value describing pose.
### Return value

Current bit field value describing pose. One of the [*MARKER_POSE_FLAGS_**](#MARKER_POSE_FLAGS_TRACING_OK)
## void setDynamic ( int dynamic )

Sets a new value indicating if the marker is tracked as dynamic (the marker pose is predicted).
### Arguments

- *int* **dynamic** - The the marker is tracked as dynamic

## int isDynamic () const

Returns the current value indicating if the marker is tracked as dynamic (the marker pose is predicted).
### Return value

Current the marker is tracked as dynamic
## void setLifetime ( float lifetime )

Sets a new lifetime of the marker.
### Arguments

- *float* **lifetime** - The marker lifetime.

## float getLifetime () const

Returns the current lifetime of the marker.
### Return value

Current marker lifetime.
---

## void renderVisualizer ( )

Renders visualizer for the marker object.
