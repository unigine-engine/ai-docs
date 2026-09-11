# CigiSegmentNotify Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>


## CigiSegmentNotify Class

### Members

---

## void setEntityID ( int id )

Sets ID of the entity to which the collision detection segment belongs.
### Arguments

- *int* **id** - ID of the entity to which the collision detection segment belongs.

## void setSegmentID ( int id )

Sets the ID of the collision detection segment along which the collision occurred. This parameter, along with [Entity ID](#setEntityID_int_void), allows the Host to match this response with the corresponding request.
### Arguments

- *int* **id** - ID of the collision detection segment along which the collision occurred.

## void setContactEntityID ( int id )

Sets the entity with which the collision occurred. If [Collision Type](#setCollisionType_int_void) is set to Non-entity (0), this parameter is ignored.
### Arguments

- *int* **id** - ID of contacted entity.

## void setCollisionType ( int type )

This parameter indicates whether the collision occurred with another entity or with a non-entity object such as the terrain.
### Arguments

- *int* **type** - Type of collision. Available values:

  - 0 � for collisions with a non-entity object.
  - 1 � for collisions with other entities.

## void setMaterialCode ( unsigned int code )

Sets the material code of the surface at the point of collision.
### Arguments

- *unsigned int* **code** - Material code of the surface at the point of collision.

## void setDistance ( float d )

Sets the distance along the collision test vector from the source endpoint (the [first point](../../../../../api/library/plugins/ig/cigi/class.icigisegmentdef_cpp.md#getPoint1_vec3) of the collision segment) to the point of intersection.
### Arguments

- *float* **d** - Length along the segment from the source endpoint, in meters.
