# RenderToTextureHelper Class


RenderToTextureHelper is a utility class that handles the technical details of rendering 2D GUI content onto 3D surfaces. All analog avionics indicators (**[Airspeed](../../../api/modules/avionics/class.airspeed.md)**, **[Altimeter](../../../api/modules/avionics/class.altimeter.md)**, **[Attitude](../../../api/modules/avionics/class.attitude.md)**, **[Compass](../../../api/modules/avionics/class.compass.md)**, **[Variometer](../../../api/modules/avionics/class.variometer.md)**) use this helper internally to display their gauges on mesh surfaces in the cockpit.


The class manages render target setup (creates an off-screen texture of the specified size), GUI instance (provides a dedicated Gui for widget rendering without affecting the main window), and material binding (automatically finds the specified surface and texture slot on the target mesh and binds the rendered texture).


While you typically don't use this class directly (the indicator components handle it internally), understanding it helps when creating custom instruments that need to render widgets to textures, debugging texture rendering issues in cockpit instruments, or extending the avionics system with new display types.


### See Also


- **[Airspeed](../../../api/modules/avionics/class.airspeed.md)**
- **[Altimeter](../../../api/modules/avionics/class.altimeter.md)**
- **[Attitude](../../../api/modules/avionics/class.attitude.md)**
- **[Compass](../../../api/modules/avionics/class.compass.md)**
- **[Variometer](../../../api/modules/avionics/class.variometer.md)**


## RenderToTextureHelper Class

---

## void init ( )

Initializes the render-to-texture helper using settings from an AnalogAvionicsRenderSettings structure.
### Arguments

## void init ( )

Initializes the render-to-texture helper with explicit parameters.
### Arguments

## void shutdown ( )

Shuts down the render-to-texture helper and releases resources.
## void render ( )

Renders the GUI contents to the texture.
## getGui ( )

Returns the GUI instance used for widget rendering.
### Return value

The GUI pointer used for rendering.
## getSize ( )

Returns the viewport size.
### Return value

The viewport size.
