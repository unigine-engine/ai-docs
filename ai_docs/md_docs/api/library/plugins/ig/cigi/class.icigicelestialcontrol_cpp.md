# CigiCelestialControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiCelestialControl Class

### Members

---

## int getHour ( ) const

Returns the value of the **Hour** parameter specified in the packet.
### Return value

**Hour** parameter value in the [0; 23] range.
## int getMinute ( ) const

Returns the value of the **Minute** parameter specified in the packet.
### Return value

**Minute** parameter value in the [0; 59] range.
## unsigned int getDate ( ) const

Returns the value of the **Date** parameter specified in the packet. Specifies the current date within the simulation.
### Return value

**Date** parameter value. The date shall be represented as a seven- or eight-digit decimal integer formatted as follows: **MMDDYYYY = (month � 1000000) + (day � 10000) + year**
## int getTimeValid ( ) const

Returns the value of the **Date/Time Valid** parameter specified in the packet.
### Return value

**Date/Time Valid** parameter value: 1 if the Hour, Minute, and Date parameters are valid; otherwise, 0.
## int getContinuous ( ) const

Returns the value of the **Ephemeris Model Enable** parameter specified in the packet.
### Return value

**Ephemeris Model Enable** parameter value. The following values are supported:
- 0 - Static time of day
- 1 - Continuous time of day


## int getSunEnabled ( ) const

Returns the value of the **Sun Enable** parameter specified in the packet.
### Return value

**Sun Enable** parameter value: 1 if the sun is enabled; otherwise, 0.
> **Notice:** The value of this parameter, along with the appropriate time-of-day and location on the globe specifies whether the sun is seen in the sky.


## int getMoonEnabled ( ) const

Returns the value of the **Moon Enable** parameter specified in the packet.
### Return value

**Moon Enable** parameter value: 1 if the moon is enabled; otherwise, 0.
> **Notice:** The value of this parameter, along with the appropriate time-of-day and location on the globe specifies whether the moon is seen in the sky.


## int getStarsEnabled ( ) const

Returns the value of the **Star Field Enable** parameter specified in the packet.
### Return value

**Star Field Enable** parameter value: 1 if the stars are enabled; otherwise, 0.
> **Notice:** The value of this parameter, along with the appropriate time-of-day and location on the globe specifies whether stars are seen in the sky.


## float getStarsIntensity ( ) const

Returns the value of the **Star Field Intensity** parameter specified in the packet.
### Return value

**Star Field Intensity** parameter value in the [0; 1] range.
