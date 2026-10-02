# MLAgents::CameraSensor Class

**Inherits from:** Sensor


CameraSensor renders the scene from the node it sits on and hands the pixels to the policy as a visual observation. The node's +Y axis is the view direction and +Z is up, the same convention as **[RaySensor](../../../api/modules/ml_agents/class.raysensor.md)** uses.


The block it produces is three-dimensional and made of bytes, which is what marks it as visual and makes the trainer put a convolutional network in front of it.


> **Notice:** A visual observation is the most expensive one available: it needs a larger network and a rendered frame per decision, so the training runs only as fast as the renderer - and it rules out the headless mode, since **isOperational()** returns false with no renderer to capture from. Use a camera only where the task cannot be expressed as numbers or raycasts.


### Component Parameters


| Name | Type | Default | Description |
|---|---|---|---|
| Width | *Int* | 64 | Observation width in pixels. The cost is dominated by the number of captures rather than by their resolution, but the trainer's convolutional network needs at least 36 |
| Height | *Int* | 64 | Observation height in pixels (at least 36) |
| Grayscale | *Toggle* | 0 | One luma channel instead of three. Thirds the observation while the render costs the same. Keep it off for any task where color carries the meaning |
| Field Of View | *Float* | 70.0 | Vertical field of view in degrees |
| Near Clipping | *Float* | 0.05 | Near clipping plane (m) |
| Far Clipping | *Float* | 100.0 | Far clipping plane (m). Keep it as tight as the task allows |
| Viewport Mask | *Mask* | viewport | What this camera can see. Give each training area its own bit and the agent stops seeing the neighboring copies |
| Debug Save Path | *String* |  | Save one capture to this `.png`. The fastest way to check the capture path, the framing and the exposure - use it before blaming the training |
| Debug Save At | *Int* | 120 | Which capture to save, counted from the world load. Deliberately not the first one: at that point the episode has not been rolled yet and the scene is still in its authored pose |


### See Also


- **[MLAgents::Sensor](../../../api/modules/ml_agents/class.sensor.md)**
- **[MLAgents::RaySensor](../../../api/modules/ml_agents/class.raysensor.md)**


## CameraSensor Class

---

## virtual getObservationSize ( )

Returns the size of the visual observation. There are three channels, or one when *Grayscale* is on.
### Return value

Number of bytes in one capture: *Width* * *Height* * channels.
## virtual void getObservationShape ( )

Returns the three-dimensional shape of the capture, which is what marks the observation as visual.
### Arguments

## virtual getDataType ( )

Returns the data type of the capture: one byte per channel.
### Return value

Always ObsDataType::UINT8.
## virtual void writeVisual ( )

Writes the pixels of the last capture.
### Arguments

## virtual void onEpisodeBegin ( )

Drops the flag saying the sensor holds a rendered frame, so the first decision of an episode never observes the last frame of the one before it.
## virtual isOperational ( )

Returns a value indicating if the sensor can capture at all. It returns false in the headless mode, and the sensor is then left out of the observation layout entirely.
### Return value

false when there is no renderer to capture from; otherwise, true.
## getPreview ( )

Returns the last captured frame as an image. Use it to show the agent's own view on a screen in the scene.
### Return value

Image holding the last capture.
## getTexture ( )

Returns the render target of the sensor camera.
### Return value

Texture the camera renders into.
