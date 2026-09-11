# LandingGearPart Component

**Inherits from:** ComponentBase


LandingGearPart represents a single animated element of a landing gear system - either a gear strut or a cover door. The component defines how this part rotates during gear extension/retraction.


Each part can be configured as a gear strut (the main landing gear leg) or a cover door (doors that open before the gear extends and optionally close after).


The animation is controlled by specifying rotation axis and on/off angles. The parent **[LandingGears](../../../api/modules/ig_aviation/class.landinggears.md)** component orchestrates the animation sequence of all parts.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Part Settings Group |  |  |
| Part | *Node* | The node to animate. |
| Is Cover | *Toggle* | Whether this part is a cover door. |
| Cover Clossable | *Toggle* | Whether the cover closes after gear is extended. |
| Visibility Group |  |  |
| Change Enable | *Toggle* | Toggle node visibility during animation. |
| Change Enable Invert | *Toggle* | Invert the enable state logic. |
| Rotation Group |  |  |
| Rotate | *Toggle* | Whether to animate rotation. |
| Axis | *Vec3* | Rotation axis. |
| On Angle | *Float* | Angle when gear is deployed (*default: 0*). |
| Off Angle | *Float* | Angle when gear is retracted (*default: 90*). |


### See Also


- **[LandingGears](../../../api/modules/ig_aviation/class.landinggears.md)**


## LandingGearPart Class

---

## void setAngle ( )

Sets the current rotation angle of the part.
### Arguments

## isCover ( )

Returns whether this part is a cover door.
### Return value

True if this part is a cover door.
## isCoverClossable ( )

Returns whether the cover door closes after the gear is fully extended.
### Return value

True if the cover closes after gear deployment.
