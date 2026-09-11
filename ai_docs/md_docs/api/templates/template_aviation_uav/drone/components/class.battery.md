# Battery Component

**Inherits from:** Drone::Component


Battery simulates drone battery discharge over time. It tracks the current charge level and depletes at a configurable rate while the drone is active.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Level | *Float* | 1.0 | Initial battery level 0-1. |
| Rate | *Float* | 0.002 | Discharge rate per frame. |


### See Also


- **[Drone](../../../../../api/templates/template_aviation_uav/drone/class.drone.md)**


## Battery Class

---

## getLevel ( )

Returns the current battery charge level.
### Return value

Current battery level 0-1.
## void setLevel ( )

Sets the battery charge level.
### Arguments

## getRate ( )

Returns the battery discharge rate.
### Return value

Discharge rate.
## void setRate ( )

Sets the battery discharge rate.
### Arguments

## void reset ( )

Resets battery to initial parameters.
