# Unigine::Plugins::IG::NEDConverter Class (CPP)

**Header:** #include <plugins/Unigine/IG/UnigineIG.h>


This utility class is used to perform conversions between different coordinate systems for the IG (e.g. ENU <-> NED, Euler rotation <-> quaternion, etc.).


> **Notice:** IG plugin must be loaded.


## NEDConverter Class

### Enums

## TARGET_COORDINATE_SYSTEM

| Name | Description |
|---|---|
| **TARGET_COORDINATE_SYSTEM_NED** = 0 | NED (North-East-Down) coordinate system. X - front, Y - right, Z - down, default in Unigine. Rotation order: Z -> Y -> X (Yaw-Pitch-Roll) |
| **TARGET_COORDINATE_SYSTEM_ENU** = 1 | ENU (East-North-Up) coordinate system. X - right, Y - front, Z - up, default in Unigine. Rotation order: Z -> X -> Y (Yaw-Roll-Pitch) |

### Members

## void setTargetCoordinateSystem ( NEDConverter::TARGET_COORDINATE_SYSTEM system )

Sets a new target coordinate system.
### Arguments

- *NEDConverter::TARGET_COORDINATE_SYSTEM* **system** - The target coordinate system.

## NEDConverter::TARGET_COORDINATE_SYSTEM getTargetCoordinateSystem () const

Returns the current target coordinate system.
### Return value

Current target coordinate system.
---

## Math:: dvec3 ENUtoNED ( const Math:: dvec3 & enu_pos ) const

Converts the coordinates of a point specified in the ENU (East-North-Up) system to NED (North-East-Down).
### Arguments

- *const  Math::[dvec3](../../../../../api/library/math/class.dvec3_cpp.md) &* **enu_pos** - Coordinates of a point in the ENU (East-North-Up) system.

### Return value

Coordinates of the point in the NED (North-East-Down) system.
## Math:: dvec3 NEDtoENU ( const Math:: dvec3 & ned_pos ) const

Converts the coordinates of a point specified in the NED (North-East-Down) system to ENU (East-North-Up).
### Arguments

- *const  Math::[dvec3](../../../../../api/library/math/class.dvec3_cpp.md) &* **ned_pos** - Coordinates of a point in the NED (North-East-Down) system.

### Return value

Coordinates of the point in the ENU (East-North-Up) system.
## Math:: dvec3 TARGETtoENU ( const Math:: dvec3 & ig_pos ) const

Converts the coordinates of a point specified in the target coordinate system (see *[setTargetCoordinateSystem()](../../../../...md#setTargetCoordinateSystem_int_void)*) to ENU (East-North-Up).
### Arguments

- *const  Math::[dvec3](../../../../../api/library/math/class.dvec3_cpp.md) &* **ig_pos** - Coordinates of the point in the target coordinate system.

### Return value

Vector representing rotation (*roll, pitch, yaw*) in ENU (East-North-Up) coordinates.
## Math:: dvec3 ENUtoTARGET ( const Math:: dvec3 & enu_pos ) const

Converts the coordinates of a point specified in ENU (East-North-Up) system to the target coordinate system (see *[setTargetCoordinateSystem()](../../../../...md#setTargetCoordinateSystem_int_void)*).
### Arguments

- *const  Math::[dvec3](../../../../../api/library/math/class.dvec3_cpp.md) &* **enu_pos** - Vector representing rotation (*roll, pitch, yaw*) in ENU (East-North-Up) coordinates.

### Return value

Coordinates of the point in the target coordinate system.
## Math:: vec3 ENUtoNED ( const Math:: vec3 & enu_pos ) const

Converts the coordinates of a point specified in the ENU (East-North-Up) system to NED (North-East-Down).
### Arguments

- *const  Math::[vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **enu_pos** - Coordinates of a point in the ENU (East-North-Up) system.

### Return value

Coordinates of the point in the NED (North-East-Down) system.
## Math:: vec3 NEDtoENU ( const Math:: vec3 & ned_pos ) const

Converts the coordinates of a point specified in the NED (North-East-Down) system to ENU (East-North-Up).
### Arguments

- *const  Math::[vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **ned_pos** - Coordinates of the point in the NED (North-East-Down) system.

### Return value

Coordinates of a point in the ENU (East-North-Up) system.
## Math:: vec3 TARGETtoENU ( const Math:: vec3 & ig_pos ) const

Converts the coordinates of a point specified in the target coordinate system (see *[setTargetCoordinateSystem()](../../../../...md#setTargetCoordinateSystem_int_void)*) to ENU (East-North-Up).
### Arguments

- *const  Math::[vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **ig_pos** - Coordinates of the point in the target coordinate system.

### Return value

Coordinates of a point in the ENU (East-North-Up) system.
## Math:: vec3 ENUtoTARGET ( const Math:: vec3 & enu_pos ) const

Converts the coordinates of a point specified in ENU (East-North-Up) system to the target coordinate system (see *[setTargetCoordinateSystem()](../../../../...md#setTargetCoordinateSystem_int_void)*).
### Arguments

- *const  Math::[vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **enu_pos** - Coordinates of a point in the ENU (East-North-Up) system.

### Return value

Coordinates of the point in the target coordinate system.
## Math:: quat eulerENUToRotation ( const Math:: vec3 & euler ) const


Converts the specified Euler rotation vector in ENU (East-North-Up) coordinates to a rotation quaternion.


> **Notice:** Unigine uses ENU orientation!
>
>
> Axis order: Yaw -> Pitch -> Roll (ENU: Z -> X -> Y, NED: Z -> Y -> X)
>
>
> - `final_rotation =zero_rotation* entity_local_rotation`
> - `entity_local_rotation = final_rotation * inverse(zero_rotation)`


### Arguments

- *const  Math::[vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **euler** - Vector representing rotation (*roll, pitch, yaw*) in ENU (East-North-Up) coordinates.

### Return value

Rotation quaternion.
## Math:: quat eulerNEDToRotation ( const Math:: vec3 & euler ) const


Converts the specified Euler rotation vector in NED (North-East-Down) coordinates to a rotation quaternion.


> **Notice:** Unigine uses ENU orientation!
>
>
> Axis order: Yaw -> Pitch -> Roll (ENU: Z -> X -> Y, NED: Z -> Y -> X)
>
>
> - `final_rotation =zero_rotation* entity_local_rotation`
> - `entity_local_rotation = final_rotation * inverse(zero_rotation)`


### Arguments

- *const  Math::[vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **euler** - Vector representing Euler rotation (*roll, pitch, yaw*) in NED (North-East-Down) coordinates.

### Return value

Rotation quaternion.
## Math:: quat eulerTARGETToRotation ( const Math:: vec3 & euler ) const

Converts the specified Euler rotation vector in the target coordinate system (see *[setTargetCoordinateSystem()](../../../../...md#setTargetCoordinateSystem_int_void)*) to a rotation quaternion.
### Arguments

- *const  Math::[vec3](../../../../../api/library/math/class.vec3_cpp.md) &* **euler** - Vector representing Euler rotation (*roll, pitch, yaw*) in the target coordinate system.

### Return value

Rotation quaternion.
## Math:: vec3 rotationToEulerENU ( const Math:: quat & rotation ) const


Converts the specified rotation quaternion to Euler rotation vector in ENU (East-North-Up) coordinates.


> **Notice:** Unigine uses ENU orientation!
>
>
> Axis order: Yaw -> Pitch -> Roll (ENU: Z -> X -> Y, NED: Z -> Y -> X)
>
>
> - `final_rotation =zero_rotation* entity_local_rotation`
> - `entity_local_rotation = final_rotation * inverse(zero_rotation)`


### Arguments

- *const  Math::[quat](../../../../../api/library/math/class.quat_cpp.md) &* **rotation** - Rotation quaternion.

## Math:: vec3 rotationToEulerNED ( const Math:: quat & rotation ) const


Converts the specified rotation quaternion to Euler rotation vector in NED (North-East-Down) coordinates.


> **Notice:** Unigine uses ENU orientation!
>
>
> Axis order: Yaw -> Pitch -> Roll (ENU: Z -> X -> Y, NED: Z -> Y -> X)
>
>
> - `final_rotation =zero_rotation* entity_local_rotation`
> - `entity_local_rotation = final_rotation * inverse(zero_rotation)`


### Arguments

- *const  Math::[quat](../../../../../api/library/math/class.quat_cpp.md) &* **rotation** - Rotation quaternion.

### Return value

Vector representing Euler rotation (*roll, pitch, yaw*) in NED (North-East-Down) coordinates.
## Math:: vec3 rotationToEulerTARGET ( const Math:: quat & rotation ) const

Converts the specified rotation quaternion to Euler rotation vector in the target coordinate system (see *[setTargetCoordinateSystem()](../../../../...md#setTargetCoordinateSystem_int_void)*).
### Arguments

- *const  Math::[quat](../../../../../api/library/math/class.quat_cpp.md) &* **rotation** - Rotation quaternion.

### Return value

Vector representing Euler rotation (*roll, pitch, yaw*) in the target coordinate system.
