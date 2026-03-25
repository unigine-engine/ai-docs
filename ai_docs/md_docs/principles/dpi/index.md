# DPI Scaling


This article is targeted at developers, UI designers, and technical artists who need to ensure that their applications look right on high-DPI monitors, maintaining precise scene content and GUI scaling, correct input handling, and optimal performance across various resolutions.


**Understanding DPI scaling is important when:**


- developing applications that run on multiple displays with different resolutions and scaling
- ensuring that GUI elements, viewport content and text remain sharp and correctly positioned
- avoiding issues related to window size and position coordinates.


## DPI Overview


### Pixel Scaling Problem and Its Solution


High-DPI (4K, Retina, HiDPI) devices have become a part of our lives and are no longer a novelty. Yet higher DPI quite often leads to a poorer experience. Why is that? Let's look at the main concept closely to answer this question.


Historically, applications relied on fixed pixel sizes as the sole metric for display quality - an approach that worked when most monitors shared similar pixel densities (normally 96 pixels per inch). This system remained effective until pixel counts became disconnected from physical screen size. While every display has a fixed number of physical pixels (like 1920x1080 or 3840x2160), their dimensions vary significantly: a laptop screen might pack four times more pixels into half the physical space of a desktop monitor.


This discrepancy introduces a major problem: pixel count no longer defines the size of content on screen:


- A 1920x1080 resolution on a 24-inch monitor looks normal.
- A 3840x2160 (4K) resolution on that same screen quadruples the pixel count, making UI elements rendered at fixed pixel sizes appear much smaller.


**This entailed the following problems:**


- **Tiny UI Elements** - Interfaces became illegible (e.g., a 32x32 pixel button on a 4K screen appeared microscopic).
- **Distorted fonts and textures** - Forced OS scaling (e.g., Windows at 125%) with no support at the application level resulted in blurred graphics.
- **Inconsistent Sizing** - A 10-pixel line on a 300 DPI monitor looked 3x thinner than on a 96 DPI display, breaking design intent.
- **Incorrect layout and mouse coordinates**, affecting both visual aspect and the application behavior.


This is where **DPI** comes into play.


**DPI (dots per inch)** is a measure of pixel density on a display. DPI was introduced to standardize rendering across varying screen densities, ensuring a consistent appearance regardless of resolution or physical screen size.


### A Smarter Approach: Logical Units


The new approach has brought about a new universal measurement unit - **Device-Independent Pixel (DIP)**, also known as Logical Pixel, Virtual Pixel or Resolution-Independent Unit. We'll call them "**logical units**" to avoid any confusion with *physical pixels* in this article.


DPI scaling appeared as a critical feature to address the challenges posed by evolving display technologies. It isn't just about "making things bigger" - it's about separating design from hardware. Logical units let you focus on physical usability (how big a button feels) rather than pixel-counting.


## DPI Fundamentals and Scale Factor


### DPI and System Scaling


The standard DPI for most systems is 96 DPI, which means 96 pixels are rendered **per inch**. Higher DPI values indicate that **more pixels are packed into the same physical space**. For example, 120 DPI (125% scaling) or 144 DPI (150% scaling), increase the perceived size of GUI elements while maintaining visual clarity.


**System scaling (or DPI scaling)** is the process of adjusting GUI elements, text, textures, etc. to appear at a consistent size regardless of the display resolution. When a user sets their system scaling (commonly configured under *Display Settings -> Scale* in modern OSes) to 125%, 150%, or 175%, the OS effectively increases the window size.


![](system_scaling.png)


Then, a DPI change **aware** application responds by applying a corresponding scale factor (the OS-provided multiplier, e.g. 1.5 for 150%) to all internal components.


**For example:**


- **100% (96 DPI)**: 1 logical unit = 1 physical pixel (no scaling, displayed elements remain at their **original pixel size**)
- **150% (144 DPI)**: 1 logical unit = 1.5 physical pixels (displayed elements are enlarged by 1.5x)
- **200% (192 DPI)**: 1 logical unit = 2 physical pixels (displayed elements are enlarged by 2x).


Applications are offered to choose a **[DPI awareness level](#awareness_levels)** to tell the OS how they want to scale both the viewport content and GUI elements based on their specific requirements.


### Physical Pixels and Logical Units


Although applications now use **logical units** to ensure they look the same on different screens and can automatically adjust to new display parameters when necessary, even when the number of physical pixels changes, **rendering and mouse coordinates remain pixel-based**. This duality forces developers to account for both coordinate systems, ensuring accurate calculations.


### Setting Coordinates and Size in Logical Units


In UNIGINE:


- Positions of **[window components](../../api/library/gui/class.enginewindow_cpp.md#intro)** and the mouse cursor are defined in **physical pixels** relative to the top-left corner of the main screen, serving as a fixed reference point for all the other elements to prevent inconsistency across different displays.
- Window and client area sizes are set in **logical units**, **[minimum](../../api/library/gui/class.enginewindow_cpp.md#setMinSize_ivec2_void)** and **[maximum](../../api/library/gui/class.enginewindow_cpp.md#setMaxSize_ivec2_void)** sizes are also set in logical units (see the corresponding **[API methods](#dpi_api)**).
- Positions of Widgets within a window or a separate GUI are set in **logical units** and calculated relative to the top-left corner of the window/GUI object.
- When necessary, positions and sizes of Widgets in **physical pixels** can be **calculated** by multiplying the size in units by the **[current DPI scale](#current_scale)**.
- When necessary, convert the size and position coordinates from units to pixels and visa versa using the **[corresponding methods](#unit_conversion)**.


For a practical example of how to convert pixels to logical units, see the code snippet in the **[Best Practices](#best_practices_conversion)** section below.


## DPI in UNIGINE


UNIGINE provides built-in support to help you work efficiently in high-DPI environments, including **command-line arguments** to control **[automatic DPI Scaling mode](#auto_dpi)** and choose the desired **[DPI awareness level](#awareness_levels)** for your application **at startup**, as well as a set of **[API methods](#dpi_api)** to control DPI-related functionality at runtime.


### DPI Awareness Levels and Auto DPI Scaling in UNIGINE


UNIGINE supports several **DPI awareness levels** - the instructions that allow applications explicitly tell Windows how they wish to handle DPI scaling (by default, the OS considers desktop applications DPI unaware unless otherwise specified, and bitmap-stretches their windows):


- **Level -1 (User-Defined DPI Awareness)**: The developer has full manual control over DPI scaling, handling event processing and scaling logic (via a **[CustomSystemProxy](../../api/library/engine/class.customsystemproxy_cpp.md)** implementation).
- **Level 0 (DPI Unaware)**: The application **ignores system DPI** settings and remains at 96 DPI (100% scaling), all content is bitmap-stretched by the OS..
- **Level 1 (System Aware)**: The application detects DPI of the main monitor at startup. > **Warning:** If moved to another monitor with a different DPI, scaling issues may occur.
- **Level 2 (Per Monitor DPI Aware)**: The application dynamically adjusts to different DPI settings when moved between monitors. This is the most flexible mode for high-DPI setups. > **Notice:** By default, UNIGINE initializes with this DPI awareness level on supported platforms.


> **Warning:** On Linux, only **Level 0 (DPI Unaware)** and **Level 1 (System Aware)** are available.


Additionally, **Auto DPI Scaling** handles scaling of GUI objects (buttons, loading screens, console, profiler, etc.) automatically based on the system's DPI, minimizing the need for manual tuning.


Toggle **Auto DPI Scaling** via the command line argument **at startup**:


- `-auto_dpi_scaling 1` : Enables automatic scaling to the window content. This is the simplest approach for applications that don't need fine-tuned manual control.
- `-auto_dpi_scaling 0` : Disables automatic content scaling. UI elements remain at a fixed size, requiring manual handling of scaling adjustments.


> **Notice:** - **Auto DPI scaling** and **DPI awareness levels** can only be set at the Engine initialization, **runtime changes are not supported**. Adjust DPI-related settings via the command line argument or SDK Browser **at startup**, or by manually editing the **[boot configuration file](../../code/configuration_file_cpp.md#boot)**. Use dpi_awareness and auto_dpi_scaling **[console](../../code/console/index.md)** commands to check the current status.
> - DPI scaling is fully applied to both viewport content and GUI elements only with the DPI awareness level set to **Level 1 (System Aware)** or **Level 2 (Per Monitor DPI Aware)** for viewport content, and **Auto DPI Scaling** flag enabled for GUI.


### Related Classes and Methods Supporting DPI Scaling


You can manage DPI-related behavior and the pixel-logical unit conversions using API.


#### Current DPI Level


To retrieve and set the DPI Mode, use:


- **WindowEventDpi Class:**

  - *[setDpi()](../../api/library/gui/class.windoweventdpi_cpp.md#setDpi_int_void)* - Sets the DPI level.
  - *[getDpi()](../../api/library/gui/class.windoweventdpi_cpp.md#getDpi_int)* - Returns the current DPI level.
- **EngineWindow Class:**

  - *[getDpi()](../../api/library/gui/class.enginewindow_cpp.md#getDpi_int)* - Returns the current DPI level for the window.
- **WindowManager Class:**

  - *[getDpiAwareness()](../../api/library/gui/class.windowmanager_cpp.md#getDpiAwareness_int)* - Returns the DPI awareness level, the value indicating the DPI level that was attempted to apply at launch.
  - *[getCurrentDpiAwareness()](../../api/library/gui/class.windowmanager_cpp.md#getCurrentDpiAwareness_int)* - Returns the current actual DPI awareness level that the system actually applied.
- **Displays Class**

  - *[getDefaultSystemDPI()](../../api/library/gui/class.displays_cpp.md#getDefaultSystemDPI_int)* - Returns the default system dots/pixels-per-inch value.
  - *[getDPI()](../../api/library/gui/class.displays_cpp.md#getDPI_int_int)* - Returns the display DPI by its index.


#### Current Scale Factor


To retrieve and set the scale factor, use:


- **Gui Class:**

  - *[getDpiScale()](../../api/library/gui/class.gui_cpp.md#getDpiScale_float)* - Returns the current DPI scale applied to the GUI.
  - *[setDpiScale()](../../api/library/gui/class.gui_cpp.md#setDpiScale_float_void)* - Sets the DPI scale to be applied to the GUI.
- **EngineWindow Class:**

  - *[getDpiScale()](../../api/library/gui/class.enginewindow_cpp.md#getDpiScale_float)* - Returns the current DPI scale applied to the elements inside the window.
- **Widget Class:**

  - *[getDpiScale()](../../api/library/gui/class.widget_cpp.md#getDpiScale_float)* - Returns the current DPI scale applied to the widget.
- **WindowManager Class:**

  - *[isAutoDpiScaling()](../../api/library/gui/class.windowmanager_cpp.md#isAutoDpiScaling_int)* - Returns the value specifying if automatic DPI scaling is applied to the window.


#### Conversion Between Pixels and Units


Conversion between physical pixels and logical units is implemented by means of:


- **Gui Class:**

  - *[toRenderSize()](../../api/library/gui/class.gui_cpp.md#toRenderSize_int_int)* - Transforms the unit value to the pixel value.
  - *[toUnitSize()](../../api/library/gui/class.gui_cpp.md#toUnitSize_int_int)* - Transforms the pixel value to the unit value.
- **Widget Class:**

  - *[toRenderSize()](../../api/library/gui/class.widget_cpp.md#toRenderSize_int_int)* - Transforms the unit value to the pixel value.
  - *[toUnitSize()](../../api/library/gui/class.widget_cpp.md#toUnitSize_int_int)* - Transforms the pixel value to the unit value.
- **EngineWindow Class:**

  - *[toRenderSize()](../../api/library/gui/class.enginewindow_cpp.md#toRenderSize_int_int)* - Transforms the unit value to the pixel value.
  - *[toUnitSize()](../../api/library/gui/class.enginewindow_cpp.md#toUnitSize_int_int)* - Transforms the pixel value to the unit value.
  - *[globalToLocalUnitPosition()](../../api/library/gui/class.enginewindow_cpp.md#globalToLocalUnitPosition_ivec2_ivec2)* - Transforms the global screen coordinates in pixels into units relative to the window client area.
  - *[localUnitToGlobalPosition()](../../api/library/gui/class.enginewindow_cpp.md#localUnitToGlobalPosition_ivec2_ivec2)* - Transforms the position in units relative to the window client area into the global screen coordinates in pixels.


## Adapting Projects to DPI Environment


### Typical Issues


When an application doesn't properly account for DPI scaling, things can quickly go wrong. Here are some of the most common issues developers may encounter:


#### Misaligned Window Coordinates


If your application isn't **[DPI-aware](#awareness_levels)**, the operating system may apply automatic scaling, but that doesn't always mean everything lines up correctly. One common problem is misaligned window borders, where the application **thinks** it's at one position, but the system **renders** it somewhere else without proper coordinate conversion. This can cause, for example, **window scrolling being triggered too early or too late**. For instance, instead of scrolling when you reach the edge, it may only start when the cursor is somewhere in the middle of the window.


**Example**. System scaling: 175%.


When working with raw mouse coordinates (e.g. *[Input::getMousePosition()](../../api/library/controls/class.input_cpp.md#getMousePosition_ivec2)*) it's important to remember that these coordinates are usually in global screen coordinates (pixels), whereas most other UI sizes are in logical units by default (e.g. **[window size](#coordinates_size)**).


**WRONG**


```cpp
ivec2 mouse_pos = Input::getMousePosition(); // pixels
ivec2 client_pos = window->getClientPosition(); // pixels

${#HL}$ivec2 client_size = window->getClientSize(); // units - WRONG ${HL#}$

if (client_pos.x > mouse_pos.x && mouse_pos.x > (client_pos.x + client_size.x))
{
    if (client_pos.y > mouse_pos.y && mouse_pos.y > (client_pos.y + client_size.y))
    {
        // intersection
    }
}

```


![](scrolling_trigger.gif)

*Widgets are offset, and rightward scrolling is triggered too early. Although the visual output is distorted, application logic (selection) still functions correctly.*


**FIXED**


```cpp
ivec2 mouse_pos = Input::getMousePosition(); // pixels
ivec2 client_pos = window->getClientPosition(); // pixels

${#HL}$ivec2 client_size = window->getClientRenderSize(); // pixels - CORRECT ${HL#}$

if (client_pos.x > mouse_pos.x && mouse_pos.x > (client_pos.x + client_size.x))
{
    if (client_pos.y > mouse_pos.y && mouse_pos.y > (client_pos.y + client_size.y))
    {
        // intersection
    }
}

```


![](scrolling_trigger_fixed.gif)

*Fixed input offset by converting UI sizes to match pixel-based mouse coordinates, restoring correct interaction and scroll behavior.*


**FIXED**


```cpp
ivec2 mouse_pos = Input::getMousePosition(); // pixels
ivec2 client_pos = window->getClientPosition(); // pixels

${#HL}$ivec2 client_size = window->toRenderSize(window->getClientSize()); // pixels - CORRECT ${HL#}$

if (client_pos.x > mouse_pos.x && mouse_pos.x > (client_pos.x + client_size.x))
{
    if (client_pos.y > mouse_pos.y && mouse_pos.y > (client_pos.y + client_size.y))
    {
        // intersection
    }
}

```


![](scrolling_trigger_fixed.gif)

*Fixed input offset by converting UI sizes to match pixel-based mouse coordinates, restoring correct interaction and scroll behavior.*


#### Widget Position and Input Offset


Similarly, GUI elements might not scale correctly, becoming more difficult to interact with. The most typical cases are:


- Widgets positioning offset from where they should be
- Click areas not matching up with visible GUI elements.


That also happens because your application thinks its top-left corner is at (100,100) pixels, but after scaling, it's actually at (150,150) pixels.


**Example**. System scaling: 125%.


When doing size and position calculations it's important to do them in one unit system (pixels or logical units) and then convert the results to the target, unit system, if necessary. Intermixing of pixels and logical units in calculations might likely lead to incorrect behavior and appearance at DPI scales > 100%, as can be seen here with the offset primitive shapes in *[WidgetCanvas](../../api/library/gui/class.widgetcanvas_cpp.md)*.


**WRONG**


```cpp
WidgetCanvasPtr canvas = WidgetCanvas::create();

WindowManager::getMainWindow()->addChild(canvas, Gui::ALIGN_OVERLAP);

${#HL}$ivec2 window_size = WindowManager::getMainWindow()->getClientRenderSize(); // pixels - WRONG ${HL#}$

vec2 text_position = vec2(window_size) * .5f; // units

int text = canvas->addText();
canvas->setTextSize(text, 40);
canvas->setTextText(text, "Text");
canvas->setTextPosition(text, text_position); // text position is expected to be in units

```


![](widget_offset.gif)

*Widgets are offset from their expected positions and do not accurately reflect the scene layout.*


**FIXED**


```cpp
WidgetCanvasPtr canvas = WidgetCanvas::create();

WindowManager::getMainWindow()->addChild(canvas, Gui::ALIGN_OVERLAP);

${#HL}$ivec2 window_size = WindowManager::getMainWindow()->getClientSize(); // units - CORRECT ${HL#}$

vec2 text_position = vec2(window_size) * .5f; // units

int text = canvas->addText();
canvas->setTextSize(text, 40);
canvas->setTextText(text, "Text");
canvas->setTextPosition(text, text_position); // text position is expected to be in units

```


![](widget_offset_fixed.gif)

*Widget offsets fixed by using consistent unit types.*


#### Blurry Text and Visual Artifacts


Text elements and visual components can become blurry, and objects may also degrade in quality due to incorrect DPI scaling:


- Fonts and textures that are sharp at 100% scaling look overly smoothed at 125% or 150%.
- GUI elements like icons and images look pixelated or stretched.
- An object's edges might appear jagged, etc.


All of the above happens because the operating system scales elements automatically, effectively stretching the image rather than properly re-rendering it at the correct resolution.


**Example**. Same GUI at 200% scaling.


**WRONG**


![](auto_dpi_scaling_0.png)

*Auto DPI Scalingdisabled. The font and the background texture become blurry and visually degraded with the parameter toggled off.*


**FIXED**


![](auto_dpi_scaling_1.png)

*Auto DPI Scalingenabled. Both the font and the background texture look sharp.*


### Setting Up Proper DPI Scaling


Transitioning an application to support proper DPI scaling can be complicated, especially when dealing with legacy code that was built with fixed pixel-based layouts. Here are several approaches to making the transition smoother while minimizing breakage:


1. If you want to keep the old behaviour completely, use DPI Awareness **[Level 0 (DPI Unaware)](#level_0)** and disabled GUI **[Auto DPI Scaling](#auto_dpi)**. To do this, use the following launch arguments:

  - `-dpi_awareness 0 -auto_dpi_scaling 0`
2. If you want to enable window viewport scaling but not apply it to widgets yet, use DPI Awareness **[Level 1 (System Aware)](#level_1)** or DPI Awareness **[Level 2 (Per Monitor DPI Aware)](#level_2)** and disabled **[Auto DPI Scaling](#auto_dpi)**. To do this, use the following launch arguments: The window will allow you to get the current value of DPI, but the widget scale will remain at 100%. <details> <summary>AppSystemLogic.cpp | Close</summary> ```cpp ivec2 pixels_window_size(1920, 1080); // pixels window->setSize(pixels_window_size); // wrong, pixels -> units window->setSize(window->toUnitSize(pixels_window_size)); // correct, units -> units // window window->setSize(ivec2()); // units window->getSize(); // units window->getRenderSize(); // pixels window->setClientSize(ivec2()); // units window->getClientSize(); // units window->getClientRenderSize(); // pixels window->setMinSize(ivec2()); // units window->getMinSize(); // units window->getMinRenderSize(); // pixels window->setMaxSize(ivec2()); // units window->getMaxSize(); // units window->getMaxRenderSize(); // pixels window->setMinAndMaxSize(ivec2(), ivec2()); // units window->toRenderSize(ivec2()); // units to pixels window->toUnitSize(ivec2()); // pixels to units window->globalToLocalUnitPosition(ivec2()); // pixels to units window->localUnitToGlobalPosition(ivec2()); // units to pixels ``` </details> Since there is access to the current window DPI, you can manually calculate the current scale. It can be applied to individual widgets and to individual widget parameters. For example, you can change the size of the widget and its font size.

  - `-dpi_awareness 1 -auto_dpi_scaling 0`
  - `-dpi_awareness 2 -auto_dpi_scaling 0`
3. If you want to enable window viewport scaling and apply it to widgets, use DPI Awareness **[Level 1 (System Aware)](#level_1)** or DPI Awareness **[Level 2 (Per Monitor DPI Aware)](#level_2)** and turn on **[Auto DPI Scaling](#auto_dpi)**. To do this, use the following launch arguments: After this, the values in units and pixels may be different. Now you need to remember about these two different measurements, and choose one for calculations. Most of the methods work with units, and the sizes in pixels are only in getters. <details> <summary>AppSystemLogic.cpp | Close</summary> ```cpp ivec2 pixels_position(256, 128); // pixels widget->setPosition(pixels_position.x, pixels_position.y); // wrong, pixels -> units ivec2 units_position = widget->toUnitSize(pixels_position); widget->setPosition(units_position.x, units_position.y); // correct, units -> units // widget widget->setPosition(0, 0); // units widget->setPositionX(0); // units widget->setPositionY(0); // units widget->setWidth(0); // units widget->getWidth(); // units widget->getRenderWidth(); // pixels widget->setHeight(0); // units widget->getHeight(); // units widget->getRenderHeight(); // pixels widget->toRenderSize(ivec2()); // units to pixels widget->toUnitSize(ivec2()); // pixels to units ``` </details>

  - `-dpi_awareness 1 -auto_dpi_scaling 1`
  - `-dpi_awareness 2 -auto_dpi_scaling 1`


### Best Practices


#### Use Logical Units in UI Development


One of the most important principles in DPI-aware development is to **avoid using fixed pixel values** whenever it's possible. Instead, **use logical units** that scale dynamically based on the DPI setting - logical units ensure consistent UI appearance across different DPIs and resolutions.


#### Coordinates Conversion Working with Different Classes


DPI scaling affects the viewport content, GUI and widgets, as their layout and sizes are defined in logical units. However, you should remember that window positions and mouse inputs rely on pixels. This means you need to **work with both pixels and logical units**, converting between them to ensure correct behavior. Ignoring this can result in an inconsistent application appearance.


Use UNIGINE's **[built-in methods](#unit_conversion)** to convert between pixels and logical units:


<details>
<summary>AppSystemLogic.cpp | Close</summary>

```cpp
EngineWindowViewportPtr window = WindowManager::getMainWindow();
WidgetPtr widget = WidgetLabel::create("Label");
window->addChild(widget, Gui::ALIGN_OVERLAP);

// You can use the Widget::, Gui::, EngineWindow:: toUnitSize and toRenderSize methods
// to convert between logical units and pixels.

ivec2 pixel_size = ivec2(640, 480);
ivec2 unit_size = window->toUnitSize(pixel_size);
window->setSize(unit_size);

// toRenderSize is usually redundant, since you can often
// use getRender* methods to get the pixel sizes directly

int pixel_width = 0;
int unit_width = widget->getWidth();

pixel_width = widget->toRenderSize(unit_width);
pixel_width = widget->getRenderWidth();

// You can use EngineWindow's globalToLocalUnitPosition and localUnitToGlobalPosition
// methods to convert between global screen coordinates (pixels) and local window
// coordinates (units)

ivec2 global_mouse = Input::getMousePosition(); // in global coordinates
ivec2 local_mouse = window->globalToLocalUnitPosition(global_mouse); // convert to local window units

widget->setPosition(local_mouse.x, local_mouse.y); // set position in window-local units (assuming this widget is a direct child of the window)

ivec2 local_position = ivec2(widget->getPositionX(), widget->getPositionY()); // units
ivec2 global_position = window->localUnitToGlobalPosition(local_position); // pixels

```

</details>


#### Avoid Manual Scaling - Use Built-in Functions


Manually adjusting every element for DPI scaling can be time-consuming and error-prone as it increases the likelihood of overlooking certain components. Instead, use UNIGINE's DPI functions *[toRenderSize()](#unit_conversion)* and *[toUnitSize()](#unit_conversion)* - which apply the DPI scale factor internally, allowing for seamless conversion between UI units and physical pixels - to handle most layout adjustments automatically.


However, if you need direct access to the coefficient (for example, to apply custom logic or perform manual scaling with **[Auto DPI Scaling](#auto_dpi)** disabled), you can retrieve the scale factor the following way:


```cpp
float dpi_scale = Math::itof(window->getDpi()) / Displays::getDefaultSystemDPI();

widget->setWidth(Math::ftoi(256 * dpi_scale));
widget->setHeight(Math::ftoi(128 * dpi_scale));
widget->setFontSize(Math::ftoi(60 * dpi_scale));

```


> **Notice:** When **[Auto DPI Scaling](#auto_dpi)** is disabled, *[getDpiScale()](#current_scale)* will always return 1, making it unsuitable for manual scaling calculations. In this case, use *[Displays::getDefaultSystemDPI()](../../api/library/gui/class.displays_cpp.md#getDefaultSystemDPI_int)* to retrieve the actual system DPI value and calculate the scale factor yourself.


## Frequently Asked Questions (FAQ)


1. **How can I check the current scale factor?** To determine the current DPI scale factor in UNIGINE, use the following API methods:

  - *[EngineWindow::getDpiScale()](../../api/library/gui/class.enginewindow_cpp.md#getDpiScale_float)* - Returns the current DPI scale applied to the elements inside the window. For example, a value of 1.5 indicates 150% scaling, meaning one logical unit equals 1.5 physical pixels.This method is also available in **[Gui](../../api/library/gui/class.gui_cpp.md)**, and **[Widget](../../api/library/gui/class.widget_cpp.md)** classes.
  - *[EngineWindow::getDPI()](../../api/library/gui/class.enginewindow_cpp.md#getDpi_int)* - Returns the current DPI level for the window.
  - *[WindowManager::isAutoDpiScaling()](../../api/library/gui/class.windowmanager_cpp.md#isAutoDpiScaling_int)* - Indicates whether Auto DPI Scaling is enabled (returns true) or disabled (false).
  - *[WindowManager::getDpiAwareness()](../../api/library/gui/class.windowmanager_cpp.md#getDpiAwareness_int)* - Returns the DPI awareness level that was configured at startup.
  - *[WindowManager::getCurrentDpiAwareness()](../../api/library/gui/class.windowmanager_cpp.md#getCurrentDpiAwareness_int)* - Returns the actual DPI awareness level applied by the operating system.
2. **Why is my scene or GUI unexpectedly scaled (larger/smaller), misaligned, or triggering scroll in the wrong areas?** If your application's interface appears improperly scaled or misbehaves visually, consider the following common causes:

  - **Incorrect DPI awareness level**: If the application is **[DPI unaware](#awareness_levels)**, the OS may bitmap-scale it, resulting in blurriness or incorrect proportions. **Solution**: Enable **[Level 1 (System Aware)](#level_1)** or **[Level 2 (Per Monitor DPI Aware)](#level_2)** DPI awareness levels.
  - **[Auto DPI Scaling](#auto_dpi) is disabled**: With `auto_dpi_scaling` set to 0, widgets won't automatically scale with the system DPI. **Solution**: Enable **Auto DPI Scaling** (`auto_dpi_scaling 1`) unless you plan to scale manually.
  - **Wrong unit conversion:** Using physical pixel values instead of logical units can make widgets appear too small on high-DPI screens and cause input misalignment (e.g., mouse clicks landing or scrolling trigger in the wrong place). **Solution**: Use UNIGINE's **[built-in methods](#unit_conversion)** to convert between pixels and logical units.
3. **How can I debug DPI-related issues?** If you're experiencing DPI-related problems, follow these steps:

  - **Check the current DPI settings**: Use UNIGINE's built-in methods (*[EngineWindow::getDPI()](../../api/library/gui/class.enginewindow_cpp.md#getDpi_int), [EngineWindow::getDpiScale()](../../api/library/gui/class.enginewindow_cpp.md#getDpiScale_float), [WindowManager::getDpiAwareness()](../../api/library/gui/class.windowmanager_cpp.md#getDpiAwareness_int), [WindowManager::getCurrentDpiAwareness()](../../api/library/gui/class.windowmanager_cpp.md#getCurrentDpiAwareness_int)* and *[WindowManager::isAutoDpiScaling()](../../api/library/gui/class.windowmanager_cpp.md#isAutoDpiScaling_int)*) to verify the scaling setups, adjust the **[DPI awareness level](#awareness_levels)** and **[Auto DPI Scaling](#auto_dpi)** if necessary.
  - **Test on multiple monitors**: Move your application across displays with different DPI settings to see if it adapts correctly.
  - **Enable debug overlay**: Compare logical and physical coordinates, inspect mouse positions to spot misalignment. The following example demonstrates how to create a debug overlay to detect coordinates misalignment: <details> <summary>AppSystemLogic.h | Close</summary> ```cpp #ifndef __APP_SYSTEM_LOGIC_H__ #define __APP_SYSTEM_LOGIC_H__ #include "UnigineLogic.h" #include "UnigineWidgets.h" class AppSystemLogic : public Unigine::SystemLogic { public: int init() override; int update() override; private: Unigine::WidgetLabelPtr info_label; Unigine::WidgetLabelPtr mouse_info_label; Unigine::WidgetButtonPtr button; Unigine::WidgetCanvasPtr info_canvas; int polygon_client_window{-1}; int polygon_button{-1}; int polygon_mouse{-1}; int text_button{-1}; Unigine::Math::vec4 polygon_button_color{0.5f, 1.0f, 0.5f, 0.3f}; Unigine::EventConnections connections; }; #endif // __APP_SYSTEM_LOGIC_H__ ``` </details> <details> <summary>AppSystemLogic.cpp | Close</summary> ```cpp #include "AppSystemLogic.h" using namespace Unigine; using namespace Unigine::Math; int AppSystemLogic::init() { info_canvas = WidgetCanvas::create(); polygon_client_window = info_canvas->addPolygon(); polygon_button = info_canvas->addPolygon(); text_button = info_canvas->addText(); polygon_mouse = info_canvas->addPolygon(); info_canvas->setTextText(text_button, "Button"); info_canvas->setTextSize(text_button, 60); WindowManager::getMainWindow()->addChild(info_canvas, Gui::ALIGN_LEFT | Gui::ALIGN_OVERLAP | Gui::ALIGN_BACKGROUND); info_label = WidgetLabel::create(); info_label->setFontSize(16); info_label->setFontOutline(1); WindowManager::getMainWindow()->addChild(info_label, Gui::ALIGN_LEFT | Gui::ALIGN_OVERLAP); mouse_info_label = WidgetLabel::create(); mouse_info_label->setFontSize(16); mouse_info_label->setFontOutline(1); WindowManager::getMainWindow()->addChild(mouse_info_label, Gui::ALIGN_OVERLAP); button = WidgetButton::create("Button"); button->setFontSize(60); button->setFontOutline(1); WindowManager::getMainWindow()->addChild(button, Gui::ALIGN_CENTER); button->getEventPressed().connect(connections, [this]() { polygon_button_color = vec4(0.0f, 1.0f, 0.0f, 0.3f); }); button->getEventReleased().connect(connections, [this]() { polygon_button_color = vec4(0.5f, 1.0f, 0.5f, 0.3f); }); Input::setMouseHandle(Input::MOUSE_HANDLE_USER); return 1; } int AppSystemLogic::update() { String info; auto print_dpi_awareness = [&info](const char *title, WindowManager::DPI_AWARENESS awareness) { info += String::format("\t%s: ", title); switch (awareness) { case WindowManager::DPI_AWARENESS_CUSTOM:            info += "Custom";            break; case WindowManager::DPI_AWARENESS_UNAWARE:           info += "Unaware";           break; case WindowManager::DPI_AWARENESS_SYSTEM_AWARE:      info += "System Aware";      break; case WindowManager::DPI_AWARENESS_PER_MONITOR_AWARE: info += "Per Monitor Aware"; break; } info += "\n"; }; auto print_int = [&info](const char *title, int value) { info += String::format("\t%s: %d\n", title, value); }; auto print_float = [&info](const char *title, float value) { info += String::format("\t%s: %f\n", title, value); }; auto print_ivec2 = [&info](const char *title, const ivec2 &value, const char *measure) { info += String::format("\t%s: %d x %d %s\n", title, value.x, value.y, measure); }; auto print_units_and_pixels = [&info](const char *title, const ivec2 &units, const ivec2 &pixels) { info += String::format("\t%s: %d x %d units, %d x %d pixels\n", title, units.x, units.y, pixels.x, pixels.y); }; // window manager info += "Window Manager:\n"; info += String::format("\tAuto Dpi Scaling: %s\n", WindowManager::isAutoDpiScaling() ? "true" : "false"); print_dpi_awareness("Dpi Awareness", WindowManager::getDpiAwareness()); print_dpi_awareness("Current Dpi Awareness", WindowManager::getCurrentDpiAwareness()); info += "\n"; // window info += "Window:\n"; EngineWindowPtr window = WindowManager::getMainWindow(); print_int("Display Index", window->getDisplayIndex()); print_int("Dpi", window->getDpi()); print_float("Dpi Scale", window->getDpiScale()); print_units_and_pixels("Size", window->getSize(), window->getRenderSize()); print_units_and_pixels("Client Size", window->getClientSize(), window->getClientRenderSize()); print_ivec2("Position", window->getPosition(), "pixels"); print_ivec2("Client Position", window->getClientPosition(), "pixels"); info += "\n"; // gui info += "Gui:\n"; GuiPtr gui = window->getSelfGui(); print_float("Dpi Scale", gui->getDpiScale()); ivec2 unit_gui_size = gui->getSize(); ivec2 pixel_gui_size(gui->toRenderSize(unit_gui_size.x), gui->toRenderSize(unit_gui_size.y)); print_units_and_pixels("Size", unit_gui_size, pixel_gui_size); print_ivec2("Position", gui->getPosition(), "pixels"); ivec2 unit_gui_mouse_position(gui->getMouseX(), gui->getMouseY()); ivec2 pixel_gui_mouse_position(gui->toRenderSize(unit_gui_mouse_position.x), gui->toRenderSize(unit_gui_mouse_position.y)); print_units_and_pixels("Mouse Position", unit_gui_mouse_position, pixel_gui_mouse_position); info += "\n"; // button info += "Button:\n"; print_float("Dpi Scale", button->getDpiScale()); ivec2 unit_button_size(button->getWidth(), button->getHeight()); ivec2 pixel_button_size(button->toRenderSize(unit_button_size)); print_units_and_pixels("Size", unit_button_size, pixel_button_size); ivec2 unit_button_position(button->getPositionX(), button->getPositionY()); ivec2 pixel_button_position(button->toRenderSize(unit_button_position)); print_units_and_pixels("Position", unit_button_position, pixel_button_position); info += "\n"; info_label->setText(info); // mouse info String mouse_info = "\n"; ivec2 global_mouse_position = Input::getMousePosition(); ivec2 unit_local_mouse_position = window->globalToLocalUnitPosition(global_mouse_position); ivec2 pixel_local_mouse_position = global_mouse_position - window->getClientPosition(); mouse_info += String::format("Global Position: %d x %d pixels\n", global_mouse_position.x, global_mouse_position.y); mouse_info += String::format("Client Local Position: %d x %d units, %d x %d pixels\n", unit_local_mouse_position.x, unit_local_mouse_position.y, pixel_local_mouse_position.x, pixel_local_mouse_position.y); mouse_info_label->setText(mouse_info); mouse_info_label->setPositionX(unit_local_mouse_position.x); mouse_info_label->setPositionY(unit_local_mouse_position.y); // canvas info_canvas->setPosition(0, 0); info_canvas->setWidth(unit_gui_size.x); info_canvas->setHeight(unit_gui_size.y); const float line_size = 3.0f; const float dpi_scale = window->getDpiScale(); auto update_polygon = [this, dpi_scale](int id, const vec2 p0, const vec2 p1, const vec2 p2, const vec2 p3, const vec4 &color) { info_canvas->clearPolygonPoints(id); info_canvas->clearPolygonIndices(id); info_canvas->addPolygonPoint(id, vec3(p0.x, p0.y, 0.0f) / dpi_scale); info_canvas->addPolygonPoint(id, vec3(p1.x, p1.y, 0.0f) / dpi_scale); info_canvas->addPolygonPoint(id, vec3(p2.x, p2.y, 0.0f) / dpi_scale); info_canvas->addPolygonPoint(id, vec3(p3.x, p3.y, 0.0f) / dpi_scale); info_canvas->setPolygonColor(id, color); }; // client window update_polygon(polygon_client_window, vec2(0.0f, 0.0f), vec2(0.0f, itof(unit_gui_size.y)), vec2(itof(unit_gui_size.x), itof(unit_gui_size.y)), vec2(itof(unit_gui_size.x), 0.0f), vec4(0.0f, 0.0f, 1.0f, 0.3f) ); // button update_polygon(polygon_button, vec2(itof(unit_button_position.x), itof(unit_button_position.y)), vec2(itof(unit_button_position.x), itof(unit_button_position.y + unit_button_size.y)), vec2(itof(unit_button_position.x + unit_button_size.x), itof(unit_button_position.y + unit_button_size.y)), vec2(itof(unit_button_position.x + unit_button_size.x), itof(unit_button_position.y)), polygon_button_color ); info_canvas->setTextColor(text_button, vec4(0.0f, 1.0f, 0.0f, 0.5f)); info_canvas->setTextSize(text_button, ftoi(60 / dpi_scale)); info_canvas->setTextPosition(text_button, (vec2(unit_button_position) + vec2(34.0f, -10.0f)) / dpi_scale); // mouse update_polygon(polygon_mouse, vec2(unit_local_mouse_position) + vec2(-5.0f, -5.0f), vec2(unit_local_mouse_position) + vec2(-5.0f, +5.0f), vec2(unit_local_mouse_position) + vec2(+5.0f, +5.0f), vec2(unit_local_mouse_position) + vec2(+5.0f, -5.0f), vec4(1.0f, 0.0f, 0.0f, 1.0f) ); return 1; } ``` </details> ![](debug_overlay.png) *Coordinate misalignment caused by mixing pixel and logical units without proper DPI scaling.*
4. **How can I make old code work without rewriting everything?** If your project contains legacy code that wasn't originally designed for high-DPI scaling, you can adapt it **[incrementally](#set_dpi_scaling)** without a full rewrite:

  1. **Start safe**: Begin with DPI Awareness **[Level 0](#level_0)** and **[Auto DPI Scaling](#auto_dpi)** disabled to preserve existing behavior and avoid layout disruptions.
  2. **Update progressively**: As you modernize parts of your project, switch to DPI Awareness **[Level 1 (System Aware)](#level_1)** or **[Level 2 (Per Monitor Aware)](#level_2)**, while keeping **[Auto DPI Scaling](#auto_dpi)** disabled. This allows you to scale viewport content without affecting the GUI yet.
  3. **Try enabling [Auto DPI Scaling](#auto_dpi)**: Once your application handles viewport scaling correctly, the optimal next step is to enable **Auto DPI Scaling**. This allows UNIGINE to automatically adjust GUI elements based on system DPI, reducing the need for manual scaling. If this works well for your project, **skip step 4** and let the Engine take care of scaling tasks ensuring consistent visual appearance of your application across different DPI configurations.
  4. **Prioritize critical GUI elements**: If enabling **[Auto DPI Scaling](#auto_dpi)** across the entire project isn't possible, you can keep it disabled and selectively apply **[manual DPI scaling](#best_practices_manual)** to essential widgets. This means calculating their sizes using the DPI scale factor to ensure consistent appearance. For some projects, this partial adaptation may be sufficient. > **Notice:** If you later decide to switch to **Auto DPI Scaling**, be sure to remove any manual scaling logic to avoid conflicts or double scaling.


## Conclusion


**Why Embrace DPI Scaling?**


Screens aren't what they used to be and DPI scaling makes your application appear and function intended, no matter the device. Transitioning to proper DPI scaling brings real, tangible benefits:


- Consistency across devices: Whether your app runs on a 1080p laptop or a 4K external monitor, UI elements look and behave predictably.
- Crisp visuals: Text and UI elements stay sharp and readable. No more blurry fonts or squished widgets.
- Fewer bugs and layout issues: Proper scaling helps avoid visual glitches, misaligned elements, and confusing input behavior.


**You Don't Have to Do It All at Once**


One of the key advantages of moving to DPI-aware development in UNIGINE is that it can be **[gradual](#legacy_transition)** and you don't have to refactor your entire app overnight.
