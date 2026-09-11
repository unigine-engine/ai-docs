# CigiVolumeNotify Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>


## CigiVolumeNotify Class

### Members

---

## void setEntityID ( int id )

Sets the ID of the entity to which the collision detection volume belongs.
### Arguments

- *int* **id** - ID of the entity to which the collision detection volume belongs.

## void setVolumeID ( int id )

Sets the ID of the collision detection volume within which the collision occurred. This parameter, along with [Entity ID](#setEntityID_int_void), allows the Host to match this response with the corresponding request.
### Arguments

- *int* **id** - ID of the collision detection volume within which the collision occurred.

## void setContactEntityID ( int id )

Sets the entity with which the collision occurred. If [Collision Type](#setCollisionType_int_void) is set to Non-entity (0), this parameter is ignored.
### Arguments

- *int* **id** - ID of contacted entity.

## void setContactVolumeID ( int id )

Sets the ID of the collision detection volume with which the collision occurred.
### Arguments

- *int* **id** - ID of the collision detection volume with which the collision occurred.

## void setCollisionType ( int type )

This parameter indicates whether the collision occurred with another entity or with a non-entity object such as the terrain.
### Arguments

- *int* **type** - Type of collision. Available values:

  - 0 � for collisions with a non-entity object.
  - 1 � for collisions with other entities.
