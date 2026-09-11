# LandingGears Component

**Inherits from:** NetworkComponentBase


LandingGears orchestrates the animation of an aircraft's landing gear system, including gear struts and cover doors. It handles the proper sequencing: covers open first, then gears extend, and optionally covers close again.


The component finds all **[LandingGearPart](../../../api/modules/ig_aviation/class.landinggearpart.md)** components in child nodes and animates them through a state machine with the following states: CLOSED (gear fully retracted, covers closed), COVER_1 (covers opening), GEARS (gear struts extending/retracting), COVER_2 (covers closing, if configured), and OPEN (gear fully extended).


The gear position can be controlled either automatically (setting the gear parameter to 0 or 1) or manually using a continuous 0-1 value for precise animation control.


The component supports network synchronization for distributed simulation environments.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Control Group |  |  |
| Gear | *Int* | Target gear state: -1 for undefined, 0 for retracted, 1 for extended. |
| Manual Gear | *Float* | Manual gear position (0-1) for continuous control (*default: 1.0*). |
| Continuous | *Toggle* | Enable continuous manual control mode instead of automatic state machine (*default: false*). |
| Timing Group |  |  |
| Time Covers | *Float* | Duration for cover door animation in seconds (*default: 0.5*). |
| Time Gears | *Float* | Duration for gear strut animation in seconds (*default: 2.0*). |


### See Also


- **[LandingGearPart](../../../api/modules/ig_aviation/class.landinggearpart.md)**
