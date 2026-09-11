# DynamicWidgetBackgroundRenderer Class


DynamicWidgetBackgroundRenderer renders dynamic backgrounds for VR widgets, including progress bars and highlight effects. It generates textures that can be applied to UI elements for visual feedback.


The renderer supports customizable colors for background, progress bar, highlight, and border, as well as configurable border thickness.


### See Also


- **[Tooltip](../../../../../../api/modules/vr/components/objects/tooltip/class.tooltip.md)**
- **[MenuBaseUI](../../../../../../api/modules/vr/components/objects/class.menubaseui.md)**


## DynamicWidgetBackgroundRenderer Class

---

## void setCurrentValue ( )

Sets the current value for progress bar rendering.
### Arguments

## void setMaxValue ( )

Sets the maximum value for progress bar calculation.
### Arguments

## void setHighlighted ( )

Sets whether the widget should be rendered as highlighted.
### Arguments

## void setBorderThickness ( )

Sets the border thickness for the widget background.
### Arguments

## void setTextureSize ( )

Sets the size of the output texture.
### Arguments

## getTexture ( )

Returns the rendered background texture.
### Return value

Rendered texture.
## void setBackgroundColor ( )

Sets the background color of the widget.
### Arguments

## void setProgressBarColor ( )

Sets the color of the progress bar.
### Arguments

## void setHighlightColor ( )

Sets the color used when the widget is highlighted.
### Arguments

## void setBorderColor ( )

Sets the border color of the widget.
### Arguments

## void renderToTexture ( )

Renders the widget background to the internal texture.
