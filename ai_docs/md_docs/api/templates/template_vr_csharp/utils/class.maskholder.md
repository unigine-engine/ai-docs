# MaskHolder Component

**Inherits from:** Component


MaskHolder stores collision and intersection mask settings used by the VR player, teleportation, physics, and gun systems. These masks are configured in the editor and consumed by other components at runtime.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Ray Intersection Mask | *Mask* | Mask for general ray intersection queries. |
| Teleport Allowed Mask | *Mask* | Mask for surfaces that allow teleportation. |
| Player Physics Intersection Mask | *Mask* | Mask for player physics intersection queries. |
| Player Physics Collision Mask | *Mask* | Mask for player physics collision. |
| Player Exclusion Mask | *Mask* | Mask for excluding objects from player collision. |
| Player Check Move Mask | *Mask* | Mask for movement validation checks. |
| Player Stair Detection Mask | *Mask* | Mask for stair detection. |
| Gun Intersection Mask | *Mask* | Mask for gun raycast intersection. |
