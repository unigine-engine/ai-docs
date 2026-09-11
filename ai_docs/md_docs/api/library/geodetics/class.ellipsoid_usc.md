# Unigine::Ellipsoid Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The *Ellipsoid* class handles the geodetic transformations:


- Specifies the Ellipsoid settings: semimajor axis, flattening coefficient
- Performs systems coordinates (ECF, ENU, NED, Geodetic) conversion
- Solves direct and inverse geodetic problems with different calculation mode (Great Circle and Vincenty algorithms)


This class is used to create an Ellipsoid instance to the *[GeodeticPivot](../../../api/library/geodetics/class.geodeticpivot_usc.md)* class.


Here is a code snippet of the *Ellipsoid* class usage:


```cpp
// define the geodetic origin
dvec3 tomsk_origin = dvec3(58.49771,84.97437,117.0);

// create a new GeodeticPivot object
GeodeticPivot pivot = new GeodeticPivot();

// create a new ellipsoid and specify its settings
Ellipsoid ellipsoid = pivot.getEllipsoid();
ellipsoid.setSemimajorAxis(80000.0f);
ellipsoid.setMode(ELLIPSOID_MODE_FAST);

// set the ellipsoid to the pivot
pivot.setOrigin(tomsk_origin);
pivot.setEllipsoid(ellipsoid);

```


## Ellipsoid Class

### Members

## double getSemiminorEccentricitySqr () const

Returns the current squared eccentricity calculated along the semiminor axis.
### Return value

Current squared eccentricity calculated along the semiminor axis
## double getSemimajorEccentricitySqr () const

Returns the current squared eccentricity calculated along the semimajor axis.
### Return value

Current squared eccentricity calculated along the semimajor axis
## double getMeanRadius () const

Returns the current mean radius of the ellipsoid.
### Return value

Current mean radius of the ellipsoid
## double getSemiminorAxis () const

Returns the current semiminor axis of the ellipsoid, in units.
### Return value

Current semiminor axis of the ellipsoid, in units
## void setMode ( int mode )

Sets a new calculation mode int value: 1 if the mode is [MODE_ACCURATE](#MODE_ACCURATE), 0 if the mode is [MODE_FAST](#MODE_FAST).
### Arguments

- *int* **mode** - The calculation mode

## int getMode () const

Returns the current calculation mode int value: 1 if the mode is [MODE_ACCURATE](#MODE_ACCURATE), 0 if the mode is [MODE_FAST](#MODE_FAST).
### Return value

Current calculation mode
## void setFlattening ( double flattening )

Sets a new flattening coefficient of the ellipsoid. If the value is 0, the ellipsoid has a sphere shape, for 1 the ellipsoid has a circle (completely flat) shape.
### Arguments

- *double* **flattening** - The flattening coefficient of the ellipsoid

## double getFlattening () const

Returns the current flattening coefficient of the ellipsoid. If the value is 0, the ellipsoid has a sphere shape, for 1 the ellipsoid has a circle (completely flat) shape.
### Return value

Current flattening coefficient of the ellipsoid
## void setSemimajorAxis ( double axis )

Sets a new semimajor axis length of the ellipsoid, in units.
### Arguments

- *double* **axis** - The semimajor axis length of the ellipsoid, in units

## double getSemimajorAxis () const

Returns the current semimajor axis length of the ellipsoid, in units.
### Return value

Current semimajor axis length of the ellipsoid, in units
---

## static Ellipsoid ( double semimajor_axis , double flattening )

Constructor. Creates a new Ellipsoid class instance with given flattening and semimajor axis.
### Arguments

- *double* **semimajor_axis** - Semimajor axis.
- *double* **flattening** - Flattening coefficient.

## static Ellipsoid ( )

Constructor. Creates a new Ellipsoid class instance (WGS84 Ellipsoid).
## dvec3 getENUSurfacePoint ( dvec3 geodetic_origin , dvec3 tangent_point )

Returns surface point by using tangent point coordinates.

> **Notice:** The Up-axis (Z+) direction in ENU points upward along the ellipsoid normal, while in UNIGINE implementation of ENU it goes from the Earth's center.

### Arguments

- *dvec3* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).
- *dvec3* **tangent_point** - Tangent point coordinates to converted (curved) to surface coordinates (offset related to point of junction).

### Return value

Surface point coordinates.
## dvec3 getENUTangentPoint ( dvec3 geodetic_origin , dvec3 surface_point )

Returns tangent point ENU coordinates based on the geographical coordinates.

> **Notice:** The Up-axis (Z+) direction in ENU points upward along the ellipsoid normal, while in UNIGINE implementation of ENU it goes from the Earth's center.

### Arguments

- *dvec3* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).
- *dvec3* **surface_point** - Surface point coordinates to be converted (flatten) to tangent point (offset related to point of junction).

### Return value

Tangent point coordinates.
## quat getENUWorldRotation ( dvec3 geodetic_origin )

Returns the world rotation quaternion in ENU coordinates.

> **Notice:** The Up-axis (Z+) direction in ENU points upward along the ellipsoid normal, while in UNIGINE implementation of ENU it goes from the Earth's center.

### Arguments

- *dvec3* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).

### Return value

World rotation in ENU coordinates.
## dmat4 getENUWorldTransform ( dvec3 geodetic_origin )

Returns the world transformation matrix in ENU coordinates.

> **Notice:** The Up-axis (Z+) direction in ENU points upward along the ellipsoid normal, while in UNIGINE implementation of ENU it goes from the Earth's center.

### Arguments

- *dvec3* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).

### Return value

World transformation matrix in ENU coordinates.
## dvec3 getNEDSurfacePoint ( dvec3 geodetic_origin , dvec3 tangent_point )

Returns surface point by using tangent point coordinates.

> **Notice:** The Down-axis direction in NED points downward along the ellipsoid normal, while in UNIGINE implementation of NED it goes through the Earth's center.

### Arguments

- *dvec3* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).
- *dvec3* **tangent_point** - Tangent point coordinates to converted (curved) to surface coordinates (offset related to point of junction).

### Return value

Surface point coordinates.
## dvec3 getNEDTangentPoint ( dvec3 geodetic_origin , dvec3 surface_point )

Returns tangent point NED coordinates based on the geographical coordinates.

> **Notice:** The Down-axis direction in NED points downward along the ellipsoid normal, while in UNIGINE implementation of NED it goes through the Earth's center.

### Arguments

- *dvec3* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).
- *dvec3* **surface_point** - Surface point coordinates to be converted (flatten) to tangent point (offset related to point of junction).

### Return value

Tangent point coordinates.
## quat getNEDWorldRotation ( dvec3 geodetic_origin )

Returns the world rotation quaternion in NED coordinates.

> **Notice:** The Down-axis direction in NED points downward along the ellipsoid normal, while in UNIGINE implementation of NED it goes through the Earth's center.

### Arguments

- *dvec3* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).

### Return value

World rotation in NED coordinates.
## dmat4 getNEDWorldTransform ( dvec3 geodetic_origin )

Returns the world transformation matrix in NED coordinates.

> **Notice:** The Down-axis direction in NED points downward along the ellipsoid normal, while in UNIGINE implementation of NED it goes through the Earth's center.

### Arguments

- *dvec3* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).

### Return value

World transformation matrix in NED coordinates.
## dvec3 solveGeodeticDirect ( dvec3 geodetic_start , double bearing , double distance )

Solves the direct geodetic problem: calculates end point coordinates on the ellipsoid by using given start point, distance between points, and bearing value.
### Arguments

- *dvec3* **geodetic_start** - Start point on the ellipsoid.
- *double* **bearing** - Bearing value.
- *double* **distance** - Distance between two points on the ellipsoid.

## void solveGeodeticInverse ( dvec3 geodetic_start , dvec3 geodetic_end , double & bearing , double & distance )

Solves the inverse geodetic problem: calculates distance and bearing values by using given start and end points on the ellipsoid.
### Arguments

- *dvec3* **geodetic_start** - Start point on the ellipsoid.
- *dvec3* **geodetic_end** - End point on the ellipsoid.
- *double &* **bearing** - Variable to save the calculated bearing value.
- *double &* **distance** - Variable to save the calculated distance value.

## dvec3 toECF ( dvec3 geodetic_coords )

Converts geodetic coordinates to Cartesian (ECF).
### Arguments

- *dvec3* **geodetic_coords** - Ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters)) to be converted to Cartesian.

### Return value

Cartesian coordinates.
## dvec3 toENU ( dvec3 geodetic_origin , dvec3 geodetic_coords )

Converts geodetic coordinates to ENU (East, North, Up).

> **Notice:** The Up-axis (Z+) direction in ENU points upward along the ellipsoid normal, while in UNIGINE implementation of ENU it goes from the Earth's center.

### Arguments

- *dvec3* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).
- *dvec3* **geodetic_coords** - Coordinates to be converted to ENU.

### Return value

ENU coordinates.
## dvec3 toGeodetic ( dvec3 ecf_coords , int need_alt = 1 )

Converts Cartesian (ECF) coordinates to Ellipsoid.
### Arguments

- *dvec3* **ecf_coords** - Cartesian ECF coordinates to be converted.
- *int* **need_alt** - Flag indicating if altitude is to be calculated. 1 to calculate altitude, 0 - to skip altitude calculation.The default value is 1.

### Return value

Ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters)
## dvec3 toNED ( dvec3 geodetic_origin , dvec3 geodetic_coords )

Converts geodetics coordinates to NED (North, East, Down).

> **Notice:** The Down-axis direction in NED points downward along the ellipsoid normal, while in UNIGINE implementation of NED it goes through the Earth's center.

### Arguments

- *dvec3* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).
- *dvec3* **geodetic_coords** - Coordinates to be converted to NED.

### Return value

NED coordinates.
