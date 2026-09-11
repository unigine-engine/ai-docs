# Unigine::Plugins::IG::CollisionVolume Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


This class is used to manage collision volumes that are assigned to [entities](../../../../../api/library/plugins/ig/api/class.entity_cpp.md) and used for collision detection.


> **Notice:** IG plugin must be loaded.


A collision detection volume is a sphere or a cuboid through which collision testing is performed by the IG. When a collision detection volume passes through another collision volume, the IG registers a collision by sending the corresponding notification.


> **Notice:** Collision detection testing is performed by the IG every frame.


A volume is defined by specifying its location, size, and orientation with respect to the associated entity�s body coordinate system. A sphere�s size is specified as a radius; a cuboid�s size is specified by its width, height, and depth.


Unlike collision detection segments, which are tested segment-to-polygon, collision detection volumes are tested volume-to-volume. Volumes associated with the same entity are not tested against each other.


## CollisionVolume Class

### Members

---

## int getID ( ) const

Returns the ID of the collision volume.
### Return value

Collision volume ID.
## Entity * getEntity ( ) const

Returns the [entity](../../../../../api/library/plugins/ig/api/class.entity_cpp.md) to which the collision volume is assigned.
### Return value

Entity to which the collision volume is assigned.
## void setEnabled ( bool value )

Enables or disables the collision volume.
### Arguments

- *bool* **value** - true to enable the collision volume; false - to disable it.

## bool isEnabled ( ) const

Returns a value indicating if the collision volume is enabled.
### Return value

true if the collision volume is enabled; otherwise, false
## void setPosition ( const Math::vec3& value )

Sets the coordinates of the center of the collision volume.
### Arguments

- *const  Math::vec3&* **value** - Coordinates of the center of the collision volume, in the coordinate system of the [entity](#getEntity_Entity).

## Math:: vec3 getPosition ( ) const

Returns the current coordinates of the center of the collision volume.
### Return value

Current coordinates of the center of the collision volume, in the coordinate system of the [entity](#getEntity_Entity).
## void setRotation ( const Math::quat& value )

Sets the rotation of the cuboid-shaped collision volume. The rotation quaternion is obtained by converting NED euler rotation (*roll, pitch, yaw*) to a quaternion via the *[NEDConverter::eulerNEDToRotation()](../../../../../api/library/plugins/ig/api/class.nedconverter_cpp.md#eulerNEDToRotation_vec3_quat)* method.
### Arguments

- *const  Math::quat&* **value** - Quaternion defining rotation of the cuboid-shaped collision volume.

## Math:: quat getRotation ( ) const

Returns the current rotation of the cuboid-shaped collision volume. You can convert the obtained rotation quaternion to NED euler rotation (*roll, pitch, yaw*) via the *[NEDConverter::rotationToEulerNED()](../../../../../api/library/plugins/ig/api/class.nedconverter_cpp.md#rotationToEulerNED_quat_vec3)* method.
### Return value

Quaternion defining rotation of the cuboid-shaped collision volume.
## void setSize ( const Math::vec3& size )

Sets the size of the cuboid-shaped collision volume.
### Arguments

- *const  Math::vec3&* **size** - Vector defining the size of the cuboid-shaped collision volume (*depth, width, height*). Each component is specified in meters.

## void setRadius ( float radius )

Sets the radius of the spherical collision volume.
### Arguments

- *float* **radius** - Radius of the spherical collision volume, in meters.

## void * addOnCollisionDetectedCallback ( Unigine:: CallbackBase4 < CollisionVolume *, Ptr < ShapeContact >, long long, int > * func )

Adds a callback function to be called when a collision with the collision volume is detected. This function can be used to define specific actions to be performed when a collision with the volume is detected. The signature of the callback function must be as follows:
```cpp
void(CollisionVolume *v, ContactPtr cnt, long long contacted_entity, int contacted_segment);
```


You can set a callback function as follows:


```cpp
addOnCollisionDetectedCallback(MakeCallback(collision_callback_function_name));
```


**Example:** Setting a collision detected callback for a collision volume of an entity


```cpp
/// callback function to be called when a collision with the collision volume is detected
void my_callback(CollisionVolume *v, ShapeContactPtr cnt, long long contacted_entity, int contacted_segment)
{
	// your code
}

// ...
// somewhere in code
void SomeClass::init()
{
	// adding "my_callback" to be called when a collision with the volume is detected
	ig_manager->getEntity(entity_id)->getCollisionVolume(volume_id)->addOnCollisionDetectedCallback(Unigine::MakeCallback( my_callback );
}

```


### Arguments

- *Unigine::[CallbackBase4](../../../../../api/library/common/callbacks/class.callbackbase4_cpp.md)< [CollisionVolume](../../../../../api/library/plugins/ig/api/class.collisionvolume_cpp.md) *, [Ptr](../../../../../api/library/common/class.ptr_cpp.md)<[ShapeContact](../../../../../api/library/physics/class.shapecontact_cpp.md)>, long long, int > ** **func** - Callback function.

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
## void setName ( const char * value )

Sets a new name for the collision volume.
### Arguments

- *const char ** **value** - Collision volume name to be set.

## const char * getName ( ) const

Returns the name of the collision volume.
### Return value

Collision volume name.
