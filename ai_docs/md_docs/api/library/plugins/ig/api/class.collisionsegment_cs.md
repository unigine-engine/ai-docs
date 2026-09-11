# Unigine::Plugins::IG::CollisionSegment Class (CS)


This class is used to manage collision segments that are assigned to [entities](../../../../../api/library/plugins/ig/api/class.entity_cs.md) and used for collision detection.


> **Notice:** IG plugin must be loaded.


A collision detection segment is a line segment along which collision testing is performed by the IG. When a collision detection segment intersects a polygon, the IG registers a collision by sending the corresponding notification.


> **Notice:** Collision detection testing is performed by the IG every frame.


The segment is defined by specifying the locations of its endpoints with respect to the associated entity�s body coordinate system. Figure below illustrates five segments defined for an aircraft.


![](collision_segments.jpg)


Collision detection volumes are tested segment-to-polygon. An entity will not perform collision detection segment testing against its own geometry.


If an entity is destroyed, all collision detection segments defined for that entity will also be destroyed.


## CollisionSegment Class

### Properties

## int MaterialMask

The Gets the material mask for the collision segment. This parameter specifies the environmental and cultural features to be included in or excluded from consideration for collision testing.
## 🔒︎ int ID

The ID of the collision segment.
## vec3 EndPoint

The coordinates of the end point of the collision segment.
## vec3 StartPoint

The coordinates of the start point of the collision segment.
## bool Enabled

The a value indicating if the collision segment is enabled.
## 🔒︎ Entity Entity

The [entity](../../../../../api/library/plugins/ig/api/class.entity_cs.md) to which the collision segment is assigned.
### Members

---

## IntPtr AddOnCollisionDetectedCallback ( OnCollisionDetectedDelegate func )

Adds a callback function to be called when a collision with the collision segment is detected. This function can be used to define specific actions to be performed when a collision with the segment is detected. The signature of the callback function must be as follows:
```csharp
void(CollisionSegment segment , Object object, WorldIntersection wi)
```


You can set a callback function as follows:


```csharp
AddOnCollisionDetectedCallback((seg, obj, wi) => collision_callback_function_name(seg, obj, wi));
```


**Example:** Setting a collision detected callback for a collision segment of an entity


```csharp
class SomeClass
{
	/*...*/

	/// callback function to be called when a collision with the collision segment is detected
	private void on_position(CollisionSegment segment , Object object, WorldIntersection wi)
	{
		// insert your code handling collision event here
	}

	private void RegisterCallback()
	{
		// adding "my_callback" to be called when a collision with the segment is detected
		ig_manager.GetEntity(entity_id).GetCollisionSegment(segment_id).AddOnCollisionDetectedCallback((seg, obj, wi) => collision_callback_function_name(seg, obj, wi));
	}

	/*...*/
}

```


### Arguments

- *OnCollisionDetectedDelegate* **func** - Callback function with the following signature: void OnCollisionDetectedDelegate(*CollisionSegment* **segment**, *Object* **object**, *WorldIntersection* **wi**)

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
