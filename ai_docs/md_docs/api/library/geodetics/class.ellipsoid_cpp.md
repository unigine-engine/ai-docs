# Unigine::Ellipsoid Class (CPP)

**Header:** #include <UnigineEllipsoid.h>


The *Ellipsoid* class handles the geodetic transformations:


- Specifies the Ellipsoid settings: semimajor axis, flattening coefficient
- Performs systems coordinates (ECF, ENU, NED, Geodetic) conversion
- Solves direct and inverse geodetic problems with different calculation mode (Great Circle and Vincenty algorithms)


This class is used to create an Ellipsoid instance to the *[GeodeticPivot](../../../api/library/geodetics/class.geodeticpivot_cpp.md)* class.


Here is a code snippet of the *Ellipsoid* class usage:


```cpp
#include "UnigineMathLib.h"
#include "UnigineGeodetics.h"
#include "UnigineEllipsoid.h"

using namespace Unigine;
using namespace Unigine::Math;

/* ... */

// define the geodetic origin
dvec3 tomsk_origin = dvec3(58.49771, 84.97437, 117.0);

// create a new GeodeticPivot object
GeodeticPivotPtr pivot = GeodeticPivot::create();

// create a new ellipsoid and specify its settings
EllipsoidPtr ellipsoid = pivot->getEllipsoid();
ellipsoid->setSemimajorAxis(80000.0f);
ellipsoid->setMode(Ellipsoid::MODE_FAST);

// set the ellipsoid to the pivot
pivot->setOrigin(tomsk_origin);
pivot->setEllipsoid(ellipsoid);

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

## static EllipsoidPtr create ( double semimajor_axis , double flattening )

Constructor. Creates a new Ellipsoid class instance with given flattening and semimajor axis.
### Arguments

- *double* **semimajor_axis** - Semimajor axis.
- *double* **flattening** - Flattening coefficient.

## static EllipsoidPtr create ( )

Constructor. Creates a new Ellipsoid class instance (WGS84 Ellipsoid).
## Math:: dvec3 getENUSurfacePoint ( const Math:: dvec3 & geodetic_origin , const Math:: dvec3 & tangent_point )

Returns surface point by using tangent point coordinates.

> **Notice:** The Up-axis (Z+) direction in ENU points upward along the ellipsoid normal, while in UNIGINE implementation of ENU it goes from the Earth's center.

### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **tangent_point** - Tangent point coordinates to converted (curved) to surface coordinates (offset related to point of junction).

### Return value

Surface point coordinates.
## Math:: dvec3 getENUTangentPoint ( const Math:: dvec3 & geodetic_origin , const Math:: dvec3 & surface_point )

Returns tangent point ENU coordinates based on the geographical coordinates.

> **Notice:** The Up-axis (Z+) direction in ENU points upward along the ellipsoid normal, while in UNIGINE implementation of ENU it goes from the Earth's center.

### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **surface_point** - Surface point coordinates to be converted (flatten) to tangent point (offset related to point of junction).

### Return value

Tangent point coordinates.
## Math:: quat getENUWorldRotation ( const Math:: dvec3 & geodetic_origin )

Returns the world rotation quaternion in ENU coordinates.

> **Notice:** The Up-axis (Z+) direction in ENU points upward along the ellipsoid normal, while in UNIGINE implementation of ENU it goes from the Earth's center.

### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).

### Return value

World rotation in ENU coordinates.
## Math:: dmat4 getENUWorldTransform ( const Math:: dvec3 & geodetic_origin )

Returns the world transformation matrix in ENU coordinates.

> **Notice:** The Up-axis (Z+) direction in ENU points upward along the ellipsoid normal, while in UNIGINE implementation of ENU it goes from the Earth's center.

### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).

### Return value

World transformation matrix in ENU coordinates.
## int isSupported ( )

Returns a value indicating if the geodetics feature is enabled.
### Return value

1 if the geodetics feature is enabled; otherwise, 0.
## Math:: dvec3 getNEDSurfacePoint ( const Math:: dvec3 & geodetic_origin , const Math:: dvec3 & tangent_point )

Returns surface point by using tangent point coordinates.

> **Notice:** The Down-axis direction in NED points downward along the ellipsoid normal, while in UNIGINE implementation of NED it goes through the Earth's center.

### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **tangent_point** - Tangent point coordinates to converted (curved) to surface coordinates (offset related to point of junction).

### Return value

Surface point coordinates.
## Math:: dvec3 getNEDTangentPoint ( const Math:: dvec3 & geodetic_origin , const Math:: dvec3 & surface_point )

Returns tangent point NED coordinates based on the geographical coordinates.

> **Notice:** The Down-axis direction in NED points downward along the ellipsoid normal, while in UNIGINE implementation of NED it goes through the Earth's center.

### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **surface_point** - Surface point coordinates to be converted (flatten) to tangent point (offset related to point of junction).

### Return value

Tangent point coordinates.
## Math:: quat getNEDWorldRotation ( const Math:: dvec3 & geodetic_origin )

Returns the world rotation quaternion in NED coordinates.

> **Notice:** The Down-axis direction in NED points downward along the ellipsoid normal, while in UNIGINE implementation of NED it goes through the Earth's center.

### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).

### Return value

World rotation in NED coordinates.
## Math:: dmat4 getNEDWorldTransform ( const Math:: dvec3 & geodetic_origin )

Returns the world transformation matrix in NED coordinates.

> **Notice:** The Down-axis direction in NED points downward along the ellipsoid normal, while in UNIGINE implementation of NED it goes through the Earth's center.

### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).

### Return value

World transformation matrix in NED coordinates.
## Math:: dvec3 solveGeodeticDirect ( const Math:: dvec3 & geodetic_start , double bearing , double distance )

Solves the direct geodetic problem: calculates end point coordinates on the ellipsoid by using given start point, distance between points, and bearing value.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_start** - Start point on the ellipsoid.
- *double* **bearing** - Bearing value.
- *double* **distance** - Distance between two points on the ellipsoid.

## void solveGeodeticInverse ( const Math:: dvec3 & geodetic_start , const Math:: dvec3 & geodetic_end , double & bearing , double & distance )

Solves the inverse geodetic problem: calculates distance and bearing values by using given start and end points on the ellipsoid.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_start** - Start point on the ellipsoid.
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_end** - End point on the ellipsoid.
- *double &* **bearing** - Variable to save the calculated bearing value.
- *double &* **distance** - Variable to save the calculated distance value.

## Math:: dvec3 toECF ( const Math:: dvec3 & geodetic_coords )

Converts geodetic coordinates to Cartesian (ECF).
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_coords** - Ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters)) to be converted to Cartesian.

### Return value

Cartesian coordinates.
## Math:: dvec3 toENU ( const Math:: dvec3 & geodetic_origin , const Math:: dvec3 & geodetic_coords )

Converts geodetic coordinates to ENU (East, North, Up).

> **Notice:** The Up-axis (Z+) direction in ENU points upward along the ellipsoid normal, while in UNIGINE implementation of ENU it goes from the Earth's center.

### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_coords** - Coordinates to be converted to ENU.

### Return value

ENU coordinates.
## Math:: dvec3 toGeodetic ( const Math:: dvec3 & ecf_coords , int need_alt = 1 )

Converts Cartesian (ECF) coordinates to Ellipsoid.
### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **ecf_coords** - Cartesian ECF coordinates to be converted.
- *int* **need_alt** - Flag indicating if altitude is to be calculated. 1 to calculate altitude, 0 - to skip altitude calculation.The default value is 1.

### Return value

Ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters)
## Math:: dvec3 toNED ( const Math:: dvec3 & geodetic_origin , const Math:: dvec3 & geodetic_coords )

Converts geodetics coordinates to NED (North, East, Down).

> **Notice:** The Down-axis direction in NED points downward along the ellipsoid normal, while in UNIGINE implementation of NED it goes through the Earth's center.

### Arguments

- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_origin** - The origin in ellipsoid coordinates (latitude (degrees), longitude (degrees) and altitude (meters).
- *const  Math::[dvec3](../../../api/library/math/class.dvec3_cpp.md) &* **geodetic_coords** - Coordinates to be converted to NED.

### Return value

NED coordinates.
