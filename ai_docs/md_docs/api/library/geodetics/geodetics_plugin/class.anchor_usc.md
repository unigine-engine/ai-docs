# Unigine::Plugins::Geodetics::Anchor Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


The Anchor binds the engine's world space to the geocentric (ECEF) coordinate system. It stores the pair of transformations between world and geocentric coordinates and lets you re-anchor the world at any geodetic position. Re-anchoring keeps world coordinates small near the current area of interest, preserving floating-point precision in large georeferenced scenes.


To re-anchor the world, set the anchor position via the **[getGeoPosition()()](../../../...md#getGeoPosition_dvec3)** property: the plugin builds an East-North-Up tangent frame on the WGS84 ellipsoid at the specified geodetic position, and this frame becomes the new world frame. The transformations that were in effect before the last re-anchoring remain available via the **[getOldGeocentricToWorld()()](../../../...md#getOldGeocentricToWorld_dmat4)** and **[getOldWorldToGeocentric()()](../../../...md#getOldWorldToGeocentric_dmat4)** properties, so the data you keep in world coordinates can be converted to the new frame. Calling **[reset()()](../../../...md#reset_void)** drops the anchor, making world space coincide with the geocentric coordinate system.


The anchor is a part of the *[Geodetics](../../../../code/plugins/geodetics/index.md)* plugin and is obtained via the *[Converter](../../../../api/library/geodetics/geodetics_plugin/class.converter_usc.md)* class.


## Anchor Class

### Members

## getMode () const

Returns the current anchoring mode defining how the current world frame was established. *[ANCHOR_MODE_GEOPOSITION](#ANCHOR_MODE_GEOPOSITION)* means the world is anchored at a geodetic position, *[ANCHOR_MODE_GEOCENTRIC](#ANCHOR_MODE_GEOCENTRIC)* means no anchor position is set and world space coincides with the geocentric coordinate system.
### Return value

Current anchoring mode
## void setGeoPosition ( )

Sets a new geodetic position (latitude and longitude in degrees, altitude in meters) the world is anchored at. Setting this property re-anchors the world: an East-North-Up tangent frame is built on the WGS84 ellipsoid at the specified position and becomes the new world frame, while the previous transformations remain available via the **[getOldGeocentricToWorld()()](../../../...md#getOldGeocentricToWorld_dmat4)** and **[getOldWorldToGeocentric()()](../../../...md#getOldWorldToGeocentric_dmat4)** properties.
### Arguments

- **position** - The geodetic position the world is anchored at

## getGeoPosition () const

Returns the current geodetic position (latitude and longitude in degrees, altitude in meters) the world is anchored at. Setting this property re-anchors the world: an East-North-Up tangent frame is built on the WGS84 ellipsoid at the specified position and becomes the new world frame, while the previous transformations remain available via the **[getOldGeocentricToWorld()()](../../../...md#getOldGeocentricToWorld_dmat4)** and **[getOldWorldToGeocentric()()](../../../...md#getOldWorldToGeocentric_dmat4)** properties.
### Return value

Current geodetic position the world is anchored at
## getGeocentricToWorld () const

Returns the current transformation matrix converting geocentric (ECEF) coordinates to world coordinates for the current anchor frame.
### Return value

Current geocentric-to-world transformation matrix
## getWorldToGeocentric () const

Returns the current transformation matrix converting world coordinates to geocentric (ECEF) coordinates for the current anchor frame.
### Return value

Current world-to-geocentric transformation matrix
## getOldGeocentricToWorld () const

Returns the current geocentric-to-world transformation matrix that was in effect before the last re-anchoring. Together with the current matrices it can be used to convert the data you keep in world coordinates to the new anchor frame.
### Return value

Current previous geocentric-to-world transformation matrix
## getOldWorldToGeocentric () const

Returns the current world-to-geocentric transformation matrix that was in effect before the last re-anchoring. Together with the current matrices it can be used to convert the data you keep in world coordinates to the new anchor frame.
### Return value

Current previous world-to-geocentric transformation matrix
## Event getEventChanged () const

Returns the current event triggered each time the anchor frame is applied: when a new position is set via **[getGeoPosition()()](../../../...md#getGeoPosition_dvec3)**, when the anchor is dropped via **[reset()()](../../../...md#reset_void)**, and when the anchor is moved by an external driver, such as the [Cesium](../../../../code/plugins/cesium/index.md) plugin. By the time the callback runs, the new frame is already in effect: the current transformations are available via **[getGeocentricToWorld()()](../../../...md#getGeocentricToWorld_dmat4)** and **[getWorldToGeocentric()()](../../../...md#getWorldToGeocentric_dmat4)**, and the previous ones via **[getOldGeocentricToWorld()()](../../../...md#getOldGeocentricToWorld_dmat4)** and **[getOldWorldToGeocentric()()](../../../...md#getOldWorldToGeocentric_dmat4)**.
### Return value

Current event triggered when the anchor frame changes
---
