# PropellerAnimation Component

**Inherits from:** Drone::Component


PropellerAnimation handles visual representation of spinning propellers. It supports three rendering modes: dynamic (speed-based material parameters), static (rotating mesh nodes), and shutter (camera rolling shutter simulation). The component transitions between modes based on propeller RPM.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Dynamic Group |  |  |  |
| Dynamic Node | *Node* | � | Object with dynamic propeller material. |
| Dynamic FL Surface Name | *String* | fl | Front-left surface name. |
| Dynamic FR Surface Name | *String* | fr | Front-right surface name. |
| Dynamic Speed Material Param | *String* | normal_speed | Material parameter for speed. |
| Dynamic Transparent Material Param | *String* | transparent | Material parameter for transparency. |
| Static Group |  |  |  |
| Static FL/FR/BL/BR | *Node* | � | Static propeller nodes for each position. |
| Static Speed Multiplier | *Float* | 500 | Rotation speed multiplier. |
| Static Transparent Material Param | *String* | transparent | Transparency parameter name. |
| Shutter Group |  |  |  |
| Shutter Node | *Node* | � | Object for rolling shutter effect. |
| Shutter Surface Name FL/FR | *String* | fl, fr | Surface names for shutter effect. |
| Shutter Speed Material Param | *String* | normal_speed | Material speed parameter. |
| Shutter Transparent Material Param | *String* | transparent | Transparency parameter. |


### See Also


- **[Propeller](../../../../../api/templates/template_aviation_uav/drone/components/class.propeller.md)**
- **[Drone](../../../../../api/templates/template_aviation_uav/drone/class.drone.md)**


## PropellerAnimation Class

---

## void setShutterEnabled ( )

Enables or disables the rolling shutter simulation effect.
### Arguments

## isShutterEnabled ( )

Returns whether the rolling shutter effect is enabled.
### Return value

True if shutter enabled.
