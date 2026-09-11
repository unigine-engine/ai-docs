# DoorTranslatable Component

**Inherits from:** Component


DoorTranslatable implements a sliding door that moves between minimum and maximum positions in response to signal input. Implements the ISignalSlot interface to receive float, int, and string signals.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Min Translate | *vec3* | Minimum translation position. |
| Max Translate | *vec3* | Maximum translation position. |


## DoorTranslatable Class

---

## void ReceiveFloat ( )

Receives a float signal and interpolates the door position between min and max.
### Arguments

## void ReceiveInt ( )

Receives an integer signal.
### Arguments

## void ReceiveString ( )

Receives a string signal.
### Arguments
