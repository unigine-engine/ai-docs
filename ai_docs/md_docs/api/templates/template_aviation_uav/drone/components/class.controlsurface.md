# ControlSurface Component

**Inherits from:** Drone::Component


ControlSurface represents an aerodynamic control surface (aileron, elevator, rudder, flap). It animates the surface rotation based on deflection input with configurable limits and smoothing.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Name | *String* | aileron.left | Surface identifier (e.g., "aileron.left"). |
| Max Deflection Angle | *Float* | 13.0 | Maximum positive deflection in degrees. |
| Min Deflection Angle | *Float* | -13.0 | Maximum negative deflection in degrees. |
| Rotation Axis | *Vec3* | (0, 1, 0) | Local axis of rotation. |
| Lerp Factor | *Float* | 0.2 | Smoothing factor for deflection. |


### See Also


- **[FixedWing](../../../../../api/templates/template_aviation_uav/drone/flightmodel/class.fixedwing.md)**
- **[Drone](../../../../../api/templates/template_aviation_uav/drone/class.drone.md)**


## ControlSurface Class

---

## getNameHash ( )

Returns the hash of the surface name for fast lookup.
### Return value

Name hash.
## void setDeflection ( )

Sets the target deflection (normalized -1 to 1).
### Arguments

## getDeflection ( )

Returns the current deflection value.
### Return value

Current deflection.
