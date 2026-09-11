# Propeller Component

**Inherits from:** Drone::Component


Propeller represents a single drone propeller/motor. It tracks the propeller's RPM which is set by the flight model based on throttle input. Multiple propellers can be attached to a drone.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Name | *String* | � | Identifier for the propeller (e.g., "fl", "fr", "bl", "br"). |


### See Also


- **[Drone](../../../../../api/templates/template_aviation_uav/drone/class.drone.md)**
- **[PropellerAnimation](../../../../../api/templates/template_aviation_uav/drone/components/class.propelleranimation.md)**


## Propeller Class

---

## getNameHash ( )

Returns the hash of the propeller name for fast lookup.
### Return value

Name hash value.
## void setRPM ( )

Sets the propeller RPM.
### Arguments

## getRPM ( )

Returns the current propeller RPM.
### Return value

Current RPM.
