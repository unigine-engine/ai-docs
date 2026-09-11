# Unigine.LightWorld Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Light


This class is used to create [world light sources](../../../objects/lights/world/index.md). This type of light source imitates sunlight and uses [parallel-split shadow mapping](../../../principles/render/lights_shadows/shadows/pssm.md).


### Example


The following code illustrates how to create a world light source and set its parameters (intensity scattering, etc.).


```cpp
// creating a world light source and setting its color to white (1.0f, 1.0f, 1.0f, 1.0f)
LightWorld thesun = new LightWorld(vec4(1.0f, 1.0f, 1.0f, 1.0f));

// setting the name of the world light
thesun.setName("Sun");

// setting disable angle of the world light
thesun.setDisableAngle(90.0f);

// setting light intensity
thesun.setIntensity(1.0f);

// setting scattering type to sun scattering
thesun.setScattering(LIGHT_WORLD_SCATTERING_SUN);

```


### Setting Position


A world light is an infinitely distant light source, so its physical position is not important, only the direction matters, as it defines orientation of shadows. You can change the light's direction via the [*setRotation()*](../../../api/library/nodes/class.node_usc.md#setRotation_quat_int_void) method.


Let's illustrate that by setting the correct position of the Sun for a certain geographic location (latitude, longitude), date and time. To calculate elevation and azimuth values let's use the following *sunPosition()* function:


<details>
<summary>sunPosition() function | Close</summary>

**sunPosition() function:**


```cpp
/// function calculating azimuth and elevation for the specified date, time (GMT) and geo-coordinates (https://stackoverflow.com/questions/8708048/position-of-the-sun-given-time-of-day-latitude-and-longitude)
void sunPosition(double & elevation, double & azimuth, double lat, double lon, int year=2019, int month=12, int day=31, double hour=23, int min=59,int sec=59) {
    double pi = 3.141592650f;
    double twopi = 2 * pi;
    double deg2rad = pi / 180.0f;

    // get a day of the year, e.g. Feb 1 = 32, Mar 1 = 61 on leap years
    int month_days[13] = ( 0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30 );
    for (int i=0; i<month; i++)
        day += month_days[i];
    int leapdays = (year % 4) == 0 && ((year % 400) == 0 || (year % 100) != 0) && day >= 60 && !(month==2 && day==60);
	if (leapdays > 0) day++;

    // Get Julian date - 2400000
    hour += min / 60.0f + sec / 3600.0f; // hour plus fraction
    double delta = year - 1949.0f;
    double leap = int(delta / 4.0f); // former leapyears
    double jd = 32916.5f + delta * 365 + leap + day + hour / 24.0f;

    // calculating input for the Astronomer's almanach as the difference between
    // the Julian date and JD 2451545.0 (noon, 1 January 2000)
    double time = jd - 51545.0f;

    // calculating mean longitude and mean anomaly
	double mnlong = 280.460f + 0.9856474f * time;
    mnlong = mnlong % 360;
    if (mnlong < 0) mnlong += 360;
    double mnanom = 357.528f + 0.9856003f * time;
    mnanom = mnanom %360;
    if (mnanom < 0) mnanom += 360;
    mnanom *= deg2rad;

    // calculating ecliptic longitude and obliquity of ecliptic
    double eclong = mnlong + 1.915f * sin(mnanom) + 0.020f * sin(2 * mnanom);
    eclong = eclong % 360;
    if (eclong < 0) eclong+= 360;
    double oblqec = 23.439f - 0.0000004f * time;
    eclong *= deg2rad;
    oblqec *= deg2rad;

    // calculating celestial coordinates: right ascension and declination
    double num = cos(oblqec) * sin(eclong);
    double den = cos(eclong);
    double ra = atan(num / den);
    if (den < 0) ra += pi;
    if (den >= 0 && num < 0) ra += twopi;
    double dec = asin(sin(oblqec) * sin(eclong));

    // calculating local coordinates Greenwich mean sidereal time
    double gmst = 6.697375f + 0.0657098242f * time + hour;
    gmst = gmst % 24;
    if (gmst < 0) gmst+= 24.0f;

    // calculating local mean sidereal time
    double lmst = gmst + lon / 15.0f;
    lmst = lmst %24;
    if (lmst < 0) lmst += 24.0f;
    lmst = lmst * 15.0f * deg2rad;

    // calculating hour angle
    double ha = lmst - ra;
    if (ha < -pi) ha += twopi;
    if (ha > pi) ha -= twopi;

    // converting latitude to radians
    lat = lat * deg2rad;

    // calculating azimuth and elevation
    elevation = asin(sin(dec) * sin(lat) + cos(dec) * cos(lat) * cos(ha));
    azimuth = asin(-cos(dec) * sin(ha) / cos(elevation));

    // for logic and names, see Spencer, J.W. 1989. Solar Energy. 42(4):353
    int cosAzPos = (0 <= sin(dec) - sin(elevation) * sin(lat));
    int sinAzNeg = (sin(azimuth) < 0);
    if (cosAzPos && sinAzNeg) azimuth +=twopi;
    if (!cosAzPos) azimuth=  pi - azimuth;

    // return elevation and azimuth
    elevation = elevation / deg2rad;
    azimuth = azimuth / deg2rad;
}

```

</details>


Thus, we can simply set the position of the Sun as follows:


```cpp
int init() {
	/* ... */

	// geo-coordinates of a point (latitude and longitude)
	double lat = 56.49771;
	double lon = 84.97437;

	// elevation and azimuth to store calculated values
	double elevation, azimuth;

	// getting the default world light source named "sun"
	LightWorld sun = node_cast(engine.world.getNodeByName("sun"));
	if (sun!=NULL) {
		// calculating azimuth and elevation
		// for the specified date,
		// GMT time and geo-coordinates
		sunPosition(elevation,azimuth, lat, lon,
					2019, 2, 5, 				// February 5, 2019
					4, 0, 0);					// 04:00:00 (GMT)

		// setting real Sun position for the calculated azimuth and elevation values
		sun.setRotation( quat(90,270,270) * quat(azimuth,0,0) * quat(0,90,0) * quat(elevation,0,0) * quat(90,0,0) );
	}

	return 1;
}

```


## LightWorld Class

### Members

## void setMode ( int mode )

Sets a new rendering mode for the light source. This option determines whether the light is to be rendered as a dynamic or static one.
### Arguments

- *int* **mode** - The light mode, one of the [LIGHT_MODE_*](../../../api/library/lights/class.light_usc.md#MODE_DYNAMIC) variables.

## int getMode () const

Returns the current rendering mode for the light source. This option determines whether the light is to be rendered as a dynamic or static one.
### Return value

Current light mode, one of the [LIGHT_MODE_*](../../../api/library/lights/class.light_usc.md#MODE_DYNAMIC) variables.
## void setShadowZFar ( float zfar )

Sets a new distance to the far clipping plane used for generation of static shadow cascades. Static cascades are generated relative to the world light's position.
> **Notice:** This parameter is available only when the [shadow cascade mode](#setShadowCascadeBorder_int_float_void) of the world light is set to [*static*](#SHADOW_CASCADE_MODE_STATIC).


### Arguments

- *float* **zfar** - The distance to the far clipping plane to be used, in units.

## float getShadowZFar () const

Returns the current distance to the far clipping plane used for generation of static shadow cascades. Static cascades are generated relative to the world light's position.
> **Notice:** This parameter is available only when the [shadow cascade mode](#setShadowCascadeBorder_int_float_void) of the world light is set to [*static*](#SHADOW_CASCADE_MODE_STATIC).


### Return value

Current distance to the far clipping plane to be used, in units.
## void setShadowWidth ( float width )

Sets a new view width of the orthographic projection used for generation of static shadow cascades. Static cascades are generated relative to the world light's position.
> **Notice:** This parameter is available only when the [shadow cascade mode](#setShadowCascadeBorder_int_float_void) of the world light is set to [*static*](#SHADOW_CASCADE_MODE_STATIC).


### Arguments

- *float* **width** - The view width of the orthographic projection used for shadow cascade generation, in units.

## float getShadowWidth () const

Returns the current view width of the orthographic projection used for generation of static shadow cascades. Static cascades are generated relative to the world light's position.
> **Notice:** This parameter is available only when the [shadow cascade mode](#setShadowCascadeBorder_int_float_void) of the world light is set to [*static*](#SHADOW_CASCADE_MODE_STATIC).


### Return value

Current view width of the orthographic projection used for shadow cascade generation, in units.
## void setShadowHeight ( float height )

Sets a new view height of the orthographic projection used for generation of static shadow cascades. Static cascades are generated relative to the world light's position.
> **Notice:** This parameter is available only when the [shadow cascade mode](#setShadowCascadeBorder_int_float_void) of the world light is set to [*static*](#SHADOW_CASCADE_MODE_STATIC).


### Arguments

- *float* **height** - The view height of the orthographic projection used for shadow cascade generation, in units.

## float getShadowHeight () const

Returns the current view height of the orthographic projection used for generation of static shadow cascades. Static cascades are generated relative to the world light's position.
> **Notice:** This parameter is available only when the [shadow cascade mode](#setShadowCascadeBorder_int_float_void) of the world light is set to [*static*](#SHADOW_CASCADE_MODE_STATIC).


### Return value

Current view height of the orthographic projection used for shadow cascade generation, in units.
## void setNumShadowCascades ( int cascades )

Sets a new number of shadow cascades with different shadow maps. All shadow maps have the same resolution, but are applied to different cascades. Thus, close-range shadows are of higher quality and distant ones of lower.
### Arguments

- *int* **cascades** - The number of shadow cascades. Accepted values are from 1 to 4. The default is 4.

## int getNumShadowCascades () const

Returns the current number of shadow cascades with different shadow maps. All shadow maps have the same resolution, but are applied to different cascades. Thus, close-range shadows are of higher quality and distant ones of lower.
### Return value

Current number of shadow cascades. Accepted values are from 1 to 4. The default is 4.
## void setShadowCascadeMode ( int mode )

Sets a new shadow cascade generation mode for the world light source.
### Arguments

- *int* **mode** - The shadow cascade mode, one of the [LIGHT_SHADOW_CASCADE_MODE_*](#SHADOW_CASCADE_MODE_DYNAMIC) variables.

## int getShadowCascadeMode () const

Returns the current shadow cascade generation mode for the world light source.
### Return value

Current shadow cascade mode, one of the [LIGHT_SHADOW_CASCADE_MODE_*](#SHADOW_CASCADE_MODE_DYNAMIC) variables.
## vec2 getRenderShadowDepthRange () const

Returns the current shadow depth range for the light source.
### Return value

Current shadow depth range for the light source as a two-component vector (min, max).
## void setDisableAngle ( float angle )

Sets a new angle at which the light source is disabled (shadows and the diffuse component is disabled). However, the light source still affects scattering.
### Arguments

- *float* **angle** - The angle at which the light source is disabled.

## float getDisableAngle () const

Returns the current angle at which the light source is disabled (shadows and the diffuse component is disabled). However, the light source still affects scattering.
### Return value

Current angle at which the light source is disabled.
## void setScattering ( int scattering )

Sets a new lighting type set for the world light.
### Arguments

- *int* **scattering** - The lighting type set for the world light, one of the [LIGHT_WORLD_SCATTERING_*](#SCATTERING_MOON) variables.

## int getScattering () const

Returns the current lighting type set for the world light.
### Return value

Current lighting type set for the world light, one of the [LIGHT_WORLD_SCATTERING_*](#SCATTERING_MOON) variables.
## void setOneCascadePerFrame ( bool frame )

Sets a new value indicating if the One Cascade Per Frame mode is enabled. This mode distributes the update of shadow cascades across multiple rendering frames: shadows cast by static geometry are rendered into only one cascade per frame.
> **Notice:** Shadows cast by transparent surfaces cannot be baked. To make such shadows visible when any light-baking mode is enabled, configure the transparent surfaces: toggle the [dynamic lighting mode](../../../api/library/objects/class.object_usc.md#SURFACE_LIGHTING_MODE_DYNAMIC) for them.


### Arguments

- *bool* **frame** - Set **true** to enable the One Cascade Per Frame mode; **false** - to disable it.

## bool isOneCascadePerFrame () const

Returns the current value indicating if the One Cascade Per Frame mode is enabled. This mode distributes the update of shadow cascades across multiple rendering frames: shadows cast by static geometry are rendered into only one cascade per frame.
> **Notice:** Shadows cast by transparent surfaces cannot be baked. To make such shadows visible when any light-baking mode is enabled, configure the transparent surfaces: toggle the [dynamic lighting mode](../../../api/library/objects/class.object_usc.md#SURFACE_LIGHTING_MODE_DYNAMIC) for them.


### Return value

**true** if the One Cascade Per Frame mode is enabled ; otherwise **false**.
## void setShadowCascadeOriginMode ( int mode )

Sets a new mode defining what position is used as the origin of the shadow cascades, one of the *SHADOW_CASCADE_ORIGIN_MODE_** values: following the camera (default) or anchored at a manually set world point.
### Arguments

- *int* **mode** - The origin mode of the shadow cascades

## int getShadowCascadeOriginMode () const

Returns the current mode defining what position is used as the origin of the shadow cascades, one of the *SHADOW_CASCADE_ORIGIN_MODE_** values: following the camera (default) or anchored at a manually set world point.
### Return value

Current origin mode of the shadow cascades
## void setShadowCascadeOriginPosition ( Vec3 position )

Sets a new world-space anchor point for the shadow cascades, used when the cascade origin mode is set to manual. Ignored in the automatic mode.
### Arguments

- *Vec3* **position** - The world-space anchor point of the shadow cascades

## Vec3 getShadowCascadeOriginPosition () const

Returns the current world-space anchor point for the shadow cascades, used when the cascade origin mode is set to manual. Ignored in the automatic mode.
### Return value

Current world-space anchor point of the shadow cascades
## void setShadowCascadePlacementMode ( int mode )

Sets a new mode defining how the shadow cascades of the light are sized and placed, one of the *SHADOW_CASCADE_PLACEMENT_MODE_** values. The default is the uniform mode.
### Arguments

- *int* **mode** - The placement mode of the shadow cascades

## int getShadowCascadePlacementMode () const

Returns the current mode defining how the shadow cascades of the light are sized and placed, one of the *SHADOW_CASCADE_PLACEMENT_MODE_** values. The default is the uniform mode.
### Return value

Current placement mode of the shadow cascades
## void setShadowFilterFar ( float far )

Sets a new intensity of shadow filtering (blurring) for the far shadow cascades of the light, complementing the base shadow filter that acts on the near cascades. The higher the value, the less noticeable the stair-step effect at the edges of distant shadows. The effective filter width is interpolated per cascade between the near and far values. The default value is 1.
### Arguments

- *float* **far** - The intensity of shadow filtering for the far cascades

## float getShadowFilterFar () const

Returns the current intensity of shadow filtering (blurring) for the far shadow cascades of the light, complementing the base shadow filter that acts on the near cascades. The higher the value, the less noticeable the stair-step effect at the edges of distant shadows. The effective filter width is interpolated per cascade between the near and far values. The default value is 1.
### Return value

Current intensity of shadow filtering for the far cascades
---

## static LightWorld ( vec4 color )

Constructor. Creates a new world light source with a given color.
### Arguments

- *vec4* **color** - Color of the new light source.

## void setShadowCascadeBorder ( int num , float r )

Sets the multiplier for the distance to the border of the specified shadow cascade at which the corresponding shadows are rendered.
### Arguments

- *int* **num** - Number of the cascade in range [0;[num_cascades](#getNumShadowCascades_int)-1].
- *float* **r** - Distance multiplier to be set, in range [0; 1].

## float getShadowCascadeBorder ( int num )

Returns the multiplier for the distance to the border of the specified shadow cascade at which the corresponding shadows are rendered.
### Arguments

- *int* **num** - Number of the cascade in range [0;[num_cascades](#getNumShadowCascades_int)-1].

### Return value

Current distance multiplier, in range [0;1].
## static int type ( )

Returns the type of the node.
### Return value

[Light](../../../api/library/lights/class.light_usc.md) type identifier.
## Mat4 getRenderShadowCascadeModelview ( int num )

Returns the model-view matrix for the specified shadow cascade.
### Arguments

- *int* **num** - Shadow cascade number in the [0;[num_cascades](#getNumShadowCascades_int)-1] range.

### Return value

Shadow cascade model-view matrix.
## mat4 getRenderShadowCascadeProjection ( int num )

Returns the shadow cascade projection matrix for the specified cascade number.
### Arguments

- *int* **num** - Shadow cascade number in the [0;[num_cascades](#getNumShadowCascades_int)-1] range.

### Return value

Shadow cascade projection matrix.
## void updateRenderShadowCascadeMatrices ( Vec3 camera_position , float zfar )

Updates projection matrices for the shadow cascades of the light source in accordance with the specified camera position and distance to the far clipping plane.
### Arguments

- *Vec3* **camera_position** - Position of the camera in world coordinates.
- *float* **zfar** - Distance to the far z-clipping plane, in units.
