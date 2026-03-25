# CigiSensorControl Class (CPP)

**Header:** #include <plugins/Unigine/CIGIConnector/UnigineCIGIConnector.h>

**Inherits from:** CigiHostPacket


## CigiSensorControl Class

### Members

---

## int getViewID ( ) const

Returns the view ID specified in the packet.
### Return value

View ID.
## int getSensorID ( ) const

Returns the sensor ID specified in the packet.
### Return value

Sensor ID.
## int getSensorEnabled ( ) const

Returns the value of the **Sensor On/Off** parameter specified in the packet.
### Return value

**Sensor On/Off** parameter value: 1 if the sensor is on; otherwise, 0.
## int getPolarity ( ) const

Returns the value of the **Polarity** parameter specified in the packet. Determines whether the sensor shows white hot or black hot.
### Return value

**Polarity** parameter value. The following values are supported:
- 0 - White hot
- 1 - Red hot


## int getDropoutEnabled ( ) const

Returns the value of the **Line-by-Line Dropout Enable** parameter specified in the packet. This effect is meant to simulate the horizontal stripes caused by a transient loss of video information.
### Return value

**Line-by-Line Dropout Enable** parameter value: 1 if line-by-line dropout is enabled; otherwise, 0.
## int getAutomaticGain ( ) const

Returns the value of the **Automatic Gain** parameter specified in the packet.
### Return value

**Automatic Gain** parameter value: 1 if the sensor automatically adjusts the gain value to optimize the brightness and contrast of the sensor display; otherwise, 0.
## int getTrackColor ( ) const

Returns the value of the **Track White/Black** parameter specified in the packet.
### Return value

**Track White/Black** parameter value: 1 - if the sensor tracks black; 0 - if the sensor tracks white.
## int getTrackMode ( ) const

Returns the value of the **Track Mode** parameter specified in the packet. Determines which track mode the sensor will use.
### Return value

**Track Mode** parameter value. The following values are supported:
- 0 - Off
- 1 - Force Correlate. Tracking behavior shall be similar to that found in a Maverick missile.
- 2 - Scene. Tracking behavior shall be similar to that found in a FLIR (Forward Looking Infrared).
- 3 - Target. Contrast tracking shall be used to lock to a specific target area.
- 4 - Ship. Contrast tracking shall be used, with adjustment of the tracking point so that the weapon strikes close to the water line.
- 5-7 - Defined by IG


## int getResponse ( ) const

Returns the value of the **Response Type** parameter specified in the packet.
### Return value

**Response Type** parameter value: 1 - Extended (gate and target position), the IG will return a [Sensor Extended Response packet](../../../../../api/library/plugins/ig/cigi/class.icigisensorextresponse_cpp.md); 0 - Normal (gate position), the IG will return a [Sensor Response packet](../../../../../api/library/plugins/ig/cigi/class.icigisensorresponse_cpp.md).
> **Notice:** The IG shall return one of the two sensor response packets every frame as long as the following two criteria are met:
> 1. Sensor On/Off is set to On (1).
> 2. Track Mode is not set to Off (0).


## float getGain ( ) const

Returns the value of the **Gain** parameter specified in the packet. Determines the contrast of the sensor display.
### Return value

**Gain** parameter value in the [0.0; 1.0] range.
## float getLevel ( ) const

Returns the value of the **Level** parameter specified in the packet. Determines the brightness of the sensor display.
### Return value

**Level** parameter value in the [0.0; 1.0] range.
## float getCoupling ( ) const

Returns the value of the **AC Coupling** parameter specified in the packet. Determines the AC coupling decay constant for the sensor display.
### Return value

**AC Coupling** parameter value.
## float getNoise ( ) const

Returns the value of the **Noise** parameter specified in the packet. Determines the amount of detector noise for the sensor.
### Return value

**Noise** parameter value in the [0.0; 1.0] range.
