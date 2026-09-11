# Unigine::Plugins::IG::CollisionSegment Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


This class is used to manage collision segments that are assigned to [entities](../../../../../api/library/plugins/ig/api/class.entity_cpp.md) and used for collision detection.


> **Notice:** IG plugin must be loaded.


A collision detection segment is a line segment along which collision testing is performed by the IG. When a collision detection segment intersects a polygon, the IG registers a collision by sending the corresponding notification.


> **Notice:** Collision detection testing is performed by the IG every frame.


The segment is defined by specifying the locations of its endpoints with respect to the associated entity�s body coordinate system. Figure below illustrates five segments defined for an aircraft.


![](collision_segments.jpg)


Collision detection volumes are tested segment-to-polygon. An entity will not perform collision detection segment testing against its own geometry.


If an entity is destroyed, all collision detection segments defined for that entity will also be destroyed.


## CollisionSegment Class

### Members

---

## int getID ( ) const

Returns the ID of the collision segment.
### Return value

Collision segment ID.
## Entity * getEntity ( ) const

Returns the [entity](../../../../../api/library/plugins/ig/api/class.entity_cpp.md) to which the collision segment is assigned.
### Return value

Entity to which the collision segment is assigned.
## bool isEnabled ( ) const

Returns a value indicating if the collision segment is enabled.
### Return value

true if the collision segment is enabled; otherwise, false
## void setEnabled ( bool value )

Enables or disables the collision segment.
### Arguments

- *bool* **value** - true to enable the collision segment; false - to disable it.

## void setStartPoint ( const Math::vec3& point )

Sets the coordinates of the start point of the collision segment.
### Arguments

- *const  Math::vec3&* **point** - Coordinates of the start point of the collision segment, in the coordinate system of the [entity](#getEntity_Entity).

## const Math::vec3& getStartPoint ( ) const

Returns the current coordinates of the start point of the collision segment.
### Return value

Coordinates of the start point of the collision segment, in the coordinate system of the [entity](#getEntity_Entity).
## void setEndPoint ( Math:: vec3 point )

Sets the coordinates of the end point of the collision segment.
### Arguments

- *Math::[vec3](../../../../../api/library/math/class.vec3_cpp.md)* **point** - Coordinates of the end point of the collision segment, in the coordinate system of the [entity](#getEntity_Entity).

## Math:: vec3 getEndPoint ( ) const

Returns the current coordinates of the end point of the collision segment.
### Return value

Coordinates of the end point of the collision segment, in the coordinate system of the [entity](#getEntity_Entity).
## void setMaterialMask ( int mask )

Sets the material mask for the collision segment. This parameter specifies the environmental and cultural features to be included in or excluded from consideration for collision testing.
### Arguments

- *int* **mask** - Integer representing a bit mask, each bit of which represents a range of material code values. Setting that bit to 1 will cause the IG to register hits with materials within the corresponding range.

## int getMaterialMask ( ) const

Gets the material mask for the collision segment. This parameter specifies the environmental and cultural features to be included in or excluded from consideration for collision testing.
### Return value

Integer representing a bit mask, each bit of which represents a range of material code values. Setting that bit to 1 will cause the IG to register hits with materials within the corresponding range.
## void * addOnCollisionDetectedCallback ( Unigine:: CallbackBase3 < CollisionSegment *, Ptr < Object >, Ptr < WorldIntersection >> * func )

Adds a callback function to be called when a collision with the collision segment is detected. This function can be used to define specific actions to be performed when a collision with the segment is detected. The signature of the callback function must be as follows:
```cpp
void(CollisionSegment *segment , ObjectPtr object, WorldIntersectionPtr wi);
```


You can set a callback function as follows:


```cpp
addOnCollisionDetectedCallback(MakeCallback(collision_callback_function_name));
```


**Example:** Setting a collision detected callback for a collision segment of an entity


```cpp
/// callback function to be called when a collision with the collision segment is detected
void my_callback(CollisionSegment *segment , ObjectPtr object, WorldIntersectionPtr wi)
{
	// insert your code handling collision event here
}

// ...
// somewhere in code
void SomeClass::init()
{
	// adding "my_callback" to be called when a collision with the segment is detected
	ig_manager->getEntity(entity_id)->getCollisionSegment(segment_id)->addOnCollisionDetectedCallback(Unigine::MakeCallback( my_callback ));
}

```


### Arguments

- *Unigine::[CallbackBase3](../../../../../api/library/common/callbacks/class.callbackbase3_cpp.md)< [CollisionSegment](../../../../../api/library/plugins/ig/api/class.collisionsegment_cpp.md) *, [Ptr](../../../../../api/library/common/class.ptr_cpp.md)<[Object](../../../../../api/library/objects/class.object_cpp.md)>, [Ptr](../../../../../api/library/common/class.ptr_cpp.md)<[WorldIntersection](../../../../../api/library/worlds/class.worldintersection_cpp.md)>> ** **func** - Callback function.

### Return value

ID of the last added collision detected callback, if the callback was added successfully; otherwise, **nullptr**. This ID can be used to [remove](#removeOnCollisionDetectedCallback_void_ptr_bool) this callback when necessary.
## bool removeOnCollisionDetectedCallback ( void * id )

Removes the specified callback from the list of collision detected callbacks.
### Arguments

- *void ** **id** - Collision detected callback ID obtained when [adding](#addOnCollisionDetectedCallback_CallbackBase_ptr_void) it.

### Return value

True if the collision detected callback with the given ID was removed successfully; otherwise false.
## void clearOnCollisionDetectedCallbacks ( )

Clears all [added](#addOnCollisionDetectedCallback_CallbackBase_ptr_void) collision detected callbacks.
