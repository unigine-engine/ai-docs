# WidgetPictureInPicture Component

**Inherits from:** ComponentBase


WidgetPictureInPicture creates a picture-in-picture viewport overlay that renders a separate camera view. This is useful for displaying sensor feeds, rear-view mirrors, or auxiliary camera views in a small overlay window.


The widget renders to an off-screen texture using its own viewport, then displays the result as a sprite overlay. You can assign any camera to the widget and control visibility dynamically.


### Component Parameters


| Name | Type | Description |
|---|---|---|
| Position | *WidgetPosition struct* | Screen position and alignment settings for the overlay. |
| Size | *IVec2* | Pixel dimensions of the picture-in-picture viewport (*default: 320x240*). |


### See Also


- **[WidgetPictureInPictureConfigurator](../../../api/modules/sensors/class.widgetpictureinpictureconfigurator.md)**


## WidgetPictureInPicture Class

---

## isHidden ( )

Returns whether the overlay is hidden.
### Return value

True if hidden.
## void setHidden ( )

Sets whether the overlay is hidden.
### Arguments

## void setCamera ( )

Sets the camera used for rendering the picture-in-picture view.
### Arguments

## getCamera ( )

Returns the camera used for rendering.
### Return value

Current camera.
## getViewport ( )

Returns the viewport used for off-screen rendering.
### Return value

Internal viewport.
## getVBox ( )

Returns the container widget that holds the sprite overlay.
### Return value

Container widget.
