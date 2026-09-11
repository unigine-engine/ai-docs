# RadioModule Component

**Inherits from:** Drone::Component


RadioModule simulates radio communication and GNSS (GPS) reception. It calculates signal strength based on distance from the home location and simulates satellite visibility using raycasts. Signal quality affects control responsiveness.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| FakeRadio Group |  |  |  |
| Max Distance | *Float* | 200 | Maximum control range. |
| Max Height | *Float* | 200 | Maximum altitude for signal. |
| Distance To Noise | *Curve2d* | � | Signal degradation curve over distance. |
| FakeGNSS Group |  |  |  |
| Skip Frame | *Int* | 10 | Frames between satellite checks. |
| Min Length | *Float* | 0.5 | Minimum raycast length. |
| Max Length | *Float* | 100 | Maximum raycast length. |
| Intersection Mask | *Mask* | 255 | Collision mask for satellite visibility. |
| Debug Group |  |  |  |
| Debug | *Toggle* | false | Enable debug visualization. |


### See Also


- **[Drone](../../../../../api/templates/template_aviation_uav/drone/class.drone.md)**
- **[TelemetryUI](../../../../../api/templates/template_aviation_uav/ui/class.telemetryui.md)**


## RadioModule Class

---

## getDistance ( )

Returns the distance from the home location.
### Return value

Distance from home.
## getSignal ( )

Returns the radio signal strength.
### Return value

Signal strength 0-1.
## getNoise ( )

Returns the total signal noise level.
### Return value

Total noise level.
## void addExtraNoise ( )

Adds extra noise to the signal (for interference simulation).
### Arguments

## getNumSatelites ( )

Returns the number of visible GNSS satellites.
### Return value

Number of visible satellites.
## getGNSSNoise ( )

Returns the GNSS position noise based on satellite visibility.
### Return value

Position noise vector.
## getGNSSQuality ( )

Returns the GNSS signal quality.
### Return value

GNSS quality 0-1.
