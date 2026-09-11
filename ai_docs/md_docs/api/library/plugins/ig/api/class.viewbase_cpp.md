# Unigine::Plugins::IG::ViewBase Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


This class represents the *IG View* base interface. It contains common methods for View and ViewGroup interfaces.


> **Notice:** IG plugin must be loaded.


## ViewBase Class

### Enums

## VIEW_TYPE

| Name | Description |
|---|---|
| **VIEW_TYPE_VIEW** = 0 |  |
| **VIEW_TYPE_VIEWGROUP** = 1 |  |

### Members

---

## void setParentEntity ( Entity * entity )

Attaches the View(Group) as a child to the specified parent [entity](../../../../../api/library/plugins/ig/api/class.entity_cpp.md).
### Arguments

- *[Entity](../../../../../api/library/plugins/ig/api/class.entity_cpp.md) ** **entity** - Parent entity.

## long long getParentEntityID ( ) const

Returns the ID of the parent entity for the View(Group).
### Return value

Parent entity ID.
## void setGeoPosition ( const Math::dvec3& position )

Sets the View(Group) position, in geo-coordinates (lat, lon, alt).
### Arguments

- *const  Math::dvec3&* **position** - View(Group) position to set, in geo-coordinates (lat, lon, alt).

## Math:: dvec3 getGeoPosition ( ) const

Returns the current View(Group) position, in geo-coordinates (lat, lon, alt).
### Return value

View(Group) position, in geo-coordinates (lat, lon, alt).
## void setPosition ( const Math::dvec3& position )

Sets the View(Group) position.
### Arguments

- *const  Math::dvec3&* **position** - View(Group) position coordinates to set.

## Math:: dvec3 getPosition ( ) const

Returns the current View(Group) position.
### Return value

View(Group) position coordinates.
## void setWorldPosition ( const Math::dvec3& pos )

Sets the View(Group) position, in world coordinates.
### Arguments

- *const  Math::dvec3&* **pos** - View(Group) position to set, in world coordinates.

## Math:: dvec3 getWorldPosition ( ) const

Returns the current View(Group) position, in world coordinates.
### Return value

View(Group) position, in world coordinates.
## void setRotationEuler ( const Math:: vec3 & euler )

Sets the View(Group) rotation.
### Arguments

- *const  Math::[vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **euler** - View(Group) rotation euler angles to set.

## Math:: vec3 getRotationEuler ( ) const

Returns the current View(Group) rotation.
### Return value

View(Group) rotation euler angles.
## void setWorldRotationEuler ( const Math::vec3& euler )

Sets the View(Group) rotation, in world coordinates.
### Arguments

- *const  Math::vec3&* **euler** - View(Group) rotation euler angles to set.

## Math:: vec3 getWorldRotationEuler ( ) const

Returns the current View(Group) rotation, in world coordinates.
### Return value

View(Group) rotation euler angles.
## Ptr < Node > getNode ( ) const

Returns the node assigned to the View(Group).
### Return value

Node assigned to the View(Group).
## Ptr < PlayerDummy > getPlayer ( ) const

Returns the PlayerDummy assigned to the View(Group).
### Return value

PlayerDummy assigned to the View(Group).
## void copyTransformFromPlayer ( const Ptr < Player > & player )

Copies the modelview matrix and sets it for the View(Group).
### Arguments

- *const [Ptr](../../../../../api/library/common/class.ptr_cpp.md)<[Player](../../../../../api/library/players/class.player_cpp.md)> &* **player** - Source player to copy the transform from.

## Component * getComponent ( int id )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.component_cpp.md) of the component by its ID.
### Arguments

- *int* **id** - ID of the component.

### Return value

Component interface if it exists, or nullptr otherwise.
## ViewBase::VIEW_TYPE getType ( ) const

Returns the type identifier indicating whether it is a *View* or a *ViewGroup*.
### Return value

View type identifier.
