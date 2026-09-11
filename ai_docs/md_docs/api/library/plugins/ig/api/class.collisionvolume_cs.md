# Unigine::Plugins::IG::CollisionVolume Class (CS)


This class is used to manage collision volumes that are assigned to [entities](../../../../../api/library/plugins/ig/api/class.entity_cs.md) and used for collision detection.


> **Notice:** IG plugin must be loaded.


A collision detection volume is a sphere or a cuboid through which collision testing is performed by the IG. When a collision detection volume passes through another collision volume, the IG registers a collision by sending the corresponding notification.


> **Notice:** Collision detection testing is performed by the IG every frame.


A volume is defined by specifying its location, size, and orientation with respect to the associated entity�s body coordinate system. A sphere�s size is specified as a radius; a cuboid�s size is specified by its width, height, and depth.


Unlike collision detection segments, which are tested segment-to-polygon, collision detection volumes are tested volume-to-volume. Volumes associated with the same entity are not tested against each other.


## CollisionVolume Class

### Properties

## quat Rotation

The rotation of the cuboid-shaped collision volume. You can convert the obtained rotation quaternion to NED euler rotation (*roll, pitch, yaw*) via the *[NEDConverter.RotationToEulerNED()](../../../../../api/library/plugins/ig/api/class.nedconverter_cs.md#rotationToEulerNED_quat_vec3)* method.
## vec3 Position

The coordinates of the center of the collision volume, in the coordinate system of the [entity](#getEntity_Entity).
## string Name

The name of the collision volume.
## bool Enabled

The a value indicating if the collision volume is enabled.
## 🔒︎ Entity Entity

The [entity](../../../../../api/library/plugins/ig/api/class.entity_cs.md) to which the collision volume is assigned.
## 🔒︎ int ID

The ID of the collision volume.
### Members

---

## void SetSize ( vec3 size )

Sets the size of the cuboid-shaped collision volume.
### Arguments

- *vec3* **size** - Vector defining the size of the cuboid-shaped collision volume (*depth, width, height*). Each component is specified in meters.

## void SetRadius ( float radius )

Sets the radius of the spherical collision volume.
### Arguments

- *float* **radius** - Radius of the spherical collision volume, in meters.

## IntPtr AddOnCollisionDetectedCallback ( OnCollisionDetectedDelegate func )

Adds a callback function to be called when a collision with the collision volume is detected. This function can be used to define specific actions to be performed when a collision with the volume is detected. The signature of the callback function must be as follows:
```csharp
void(CollisionVolume v , ShapeContact contact, LongLong contacted_entity, int contacted_segment)
```


You can set a callback function as follows:


```csharp
AddOnCollisionDetectedCallback((vol, cnt, entity, seg) => collision_callback_function_name(vol, cnt, entity, seg));
```


**Example:** Setting a collision detected callback for a collision volume of an entity


```csharp
class SomeClass
{
	/*...*/

	/// callback function to be called when a collision with the collision volume is detected
	private void on_position(CollisionVolume v , ShapeContact contact, LongLong contacted_entity, int contacted_segment)
	{
		// insert your code handling collision event here
	}

	private void RegisterCallback()
	{
		// adding "my_callback" to be called when a collision with the volume is detected
		ig_manager.GetEntity(entity_id).GetCollisionVolume(volume_id).AddOnCollisionDetectedCallback((vol, cnt, entity, seg) => collision_callback_function_name(vol, cnt, entity, seg));
	}

	/*...*/
}

```


### Arguments

- *OnCollisionDetectedDelegate* **func** - Callback function with the following signature: void OnCollisionDetectedDelegate(*CollisionVolume* **v**, *ShapeContact* **contact**, *LongLong* **contacted_entity**, *int* **contacted_segment**)

### Return value

ID of the last added collision detected callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnCollisionDetectedCallback_void_ptr_bool) this callback when necessary.
## bool RemoveOnCollisionDetectedCallback ( IntPtr id )

Removes the specified callback from the list of collision detected callbacks.
### Arguments

- *IntPtr* **id** - Collision detected callback ID obtained when [adding](#addOnCollisionDetectedCallback_CallbackBase_ptr_void) it.

### Return value

True if the collision detected callback with the given ID was removed successfully; otherwise false.
## void ClearOnCollisionDetectedCallbacks ( )

Clears all [added](#addOnCollisionDetectedCallback_CallbackBase_ptr_void) collision detected callbacks.
