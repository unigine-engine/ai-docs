# Unigine::Plugins::IG::NEDConverter Class (CS)


This utility class is used to perform conversions between different coordinate systems for the IG (e.g. ENU <-> NED, Euler rotation <-> quaternion, etc.).


> **Notice:** IG plugin must be loaded.


## NEDConverter Class

### Enums

## TARGET_COORDINATE_SYSTEM

| Name | Description |
|---|---|
| **NED** = 0 | NED (North-East-Down) coordinate system. X - front, Y - right, Z - down, default in Unigine. Rotation order: Z -> Y -> X (Yaw-Pitch-Roll) |
| **ENU** = 1 | ENU (East-North-Up) coordinate system. X - right, Y - front, Z - up, default in Unigine. Rotation order: Z -> X -> Y (Yaw-Roll-Pitch) |

### Properties

## NEDConverter.TARGET_COORDINATE_SYSTEM TargetCoordinateSystem

The target coordinate system.
### Members

---

## dvec3 ENUtoNED ( dvec3 enu_pos )

Converts the coordinates of a point specified in the ENU (East-North-Up) system to NED (North-East-Down).
### Arguments

- *dvec3* **enu_pos** - Coordinates of a point in the ENU (East-North-Up) system.

### Return value

Coordinates of the point in the NED (North-East-Down) system.
## dvec3 NEDtoENU ( dvec3 ned_pos )

Converts the coordinates of a point specified in the NED (North-East-Down) system to ENU (East-North-Up).
### Arguments

- *dvec3* **ned_pos** - Coordinates of a point in the NED (North-East-Down) system.

### Return value

Coordinates of the point in the ENU (East-North-Up) system.
## dvec3 TARGETtoENU ( dvec3 ig_pos )

Converts the coordinates of a point specified in the target coordinate system (see *[TargetCoordinateSystem](../../../../...md#setTargetCoordinateSystem_int_void)*) to ENU (East-North-Up).
### Arguments

- *dvec3* **ig_pos** - Coordinates of the point in the target coordinate system.

### Return value

Vector representing rotation (*roll, pitch, yaw*) in ENU (East-North-Up) coordinates.
## dvec3 ENUtoTARGET ( dvec3 enu_pos )

Converts the coordinates of a point specified in ENU (East-North-Up) system to the target coordinate system (see *[TargetCoordinateSystem](../../../../...md#setTargetCoordinateSystem_int_void)*).
### Arguments

- *dvec3* **enu_pos** - Vector representing rotation (*roll, pitch, yaw*) in ENU (East-North-Up) coordinates.

### Return value

Coordinates of the point in the target coordinate system.
## vec3 ENUtoNED ( vec3 enu_pos )

Converts the coordinates of a point specified in the ENU (East-North-Up) system to NED (North-East-Down).
### Arguments

- *vec3* **enu_pos** - Coordinates of a point in the ENU (East-North-Up) system.

### Return value

Coordinates of the point in the NED (North-East-Down) system.
## vec3 NEDtoENU ( vec3 ned_pos )

Converts the coordinates of a point specified in the NED (North-East-Down) system to ENU (East-North-Up).
### Arguments

- *vec3* **ned_pos** - Coordinates of the point in the NED (North-East-Down) system.

### Return value

Coordinates of a point in the ENU (East-North-Up) system.
## vec3 TARGETtoENU ( vec3 ig_pos )

Converts the coordinates of a point specified in the target coordinate system (see *[TargetCoordinateSystem](../../../../...md#setTargetCoordinateSystem_int_void)*) to ENU (East-North-Up).
### Arguments

- *vec3* **ig_pos** - Coordinates of the point in the target coordinate system.

### Return value

Coordinates of a point in the ENU (East-North-Up) system.
## vec3 ENUtoTARGET ( vec3 enu_pos )

Converts the coordinates of a point specified in ENU (East-North-Up) system to the target coordinate system (see *[TargetCoordinateSystem](../../../../...md#setTargetCoordinateSystem_int_void)*).
### Arguments

- *vec3* **enu_pos** - Coordinates of a point in the ENU (East-North-Up) system.

### Return value

Coordinates of the point in the target coordinate system.
## quat EulerENUToRotation ( vec3 euler )


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

- *vec3* **euler** - Vector representing rotation (*roll, pitch, yaw*) in ENU (East-North-Up) coordinates.

### Return value

Rotation quaternion.
## quat EulerNEDToRotation ( vec3 euler )


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

- *vec3* **euler** - Vector representing Euler rotation (*roll, pitch, yaw*) in NED (North-East-Down) coordinates.

### Return value

Rotation quaternion.
## quat EulerTARGETToRotation ( vec3 euler )

Converts the specified Euler rotation vector in the target coordinate system (see *[TargetCoordinateSystem](../../../../...md#setTargetCoordinateSystem_int_void)*) to a rotation quaternion.
### Arguments

- *vec3* **euler** - Vector representing Euler rotation (*roll, pitch, yaw*) in the target coordinate system.

### Return value

Rotation quaternion.
## vec3 RotationToEulerENU ( quat rotation )


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

- *quat* **rotation** - Rotation quaternion.

## vec3 RotationToEulerNED ( quat rotation )


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

- *quat* **rotation** - Rotation quaternion.

### Return value

Vector representing Euler rotation (*roll, pitch, yaw*) in NED (North-East-Down) coordinates.
## vec3 RotationToEulerTARGET ( quat rotation )

Converts the specified rotation quaternion to Euler rotation vector in the target coordinate system (see *[TargetCoordinateSystem](../../../../...md#setTargetCoordinateSystem_int_void)*).
### Arguments

- *quat* **rotation** - Rotation quaternion.

### Return value

Vector representing Euler rotation (*roll, pitch, yaw*) in the target coordinate system.
