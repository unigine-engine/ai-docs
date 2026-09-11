# Unigine::Plugins::IG::ViewBase Class (CS)


This class represents the *IG View* base interface. It contains common methods for View and ViewGroup interfaces.


> **Notice:** IG plugin must be loaded.


## ViewBase Class

### Enums

## VIEW_TYPE

| Name | Description |
|---|---|
| **VIEW_TYPE_VIEW** = 0 |  |
| **VIEW_TYPE_VIEWGROUP** = 1 |  |

### Properties

## vec3 WorldRotationEuler

The View(Group) rotation, in world coordinates.
## vec3 RotationEuler

The View(Group) rotation.
## dvec3 WorldPosition

The View(Group) position, in world coordinates.
## dvec3 Position

The View(Group) position.
## dvec3 GeoPosition

The View(Group) position, in geo-coordinates (lat, lon, alt).
## 🔒︎ ViewBase.VIEW_TYPE Type

The type identifier indicating whether it is a *View* or a *ViewGroup*.
### Members

---

## void SetParentEntity ( Entity entity )

Attaches the View(Group) as a child to the specified parent [entity](../../../../../api/library/plugins/ig/api/class.entity_cs.md).
### Arguments

- *[Entity](../../../../../api/library/plugins/ig/api/class.entity_cs.md)* **entity** - Parent entity.

## long GetParentEntityID ( )

Returns the ID of the parent entity for the View(Group).
### Return value

Parent entity ID.
## Node GetNode ( )

Returns the node assigned to the View(Group).
### Return value

Node assigned to the View(Group).
## PlayerDummy GetPlayer ( )

Returns the PlayerDummy assigned to the View(Group).
### Return value

PlayerDummy assigned to the View(Group).
## void CopyTransformFromPlayer ( Player player )

Copies the modelview matrix and sets it for the View(Group).
### Arguments

- *[Player](../../../../../api/library/players/class.player_cs.md)* **player** - Source player to copy the transform from.

## Component GetComponent ( int id )

Returns the [interface](../../../../../api/library/plugins/ig/api/class.component_cs.md) of the component by its ID.
### Arguments

- *int* **id** - ID of the component.

### Return value

Component interface if it exists, or nullptr otherwise.
## ViewBase.VIEW_TYPE GetType ( )

Returns the type identifier indicating whether it is a *View* or a *ViewGroup*.
### Return value

View type identifier.
