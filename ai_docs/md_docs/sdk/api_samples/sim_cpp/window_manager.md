# Window Manager

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


## Complex Layout

This sample demonstrates a complex layout similar to a typical layout used in UnigineEditor with multiple stackable windows.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/window_manager/complex_layout*
## Group Types

This sample demonstrates all available window group types (vertical and horizontal arrangements, and a group of tabs).


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/window_manager/group_types*
## Main Windows

This sample demonstrates an application with multiple main windows. *[Console](../../../code/console/index.md)* and *[Profiler](../../../tools/profiling/profiler/index.md)* are displayed in the currently active window.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/window_manager/main_windows*
## Screenshot Advanced

This sample showcases how to capture high-resolution screenshots from focused windows, individual cameras, the main player camera, or grouped windows in real time, with optional GUI overlays.


At runtime, several additional windows are created, each with its own dedicated camera for multi-view rendering. All windows are stackable. To create a group, arrange the windows by dragging them close to each other - a green alignment grid will appear to assist with layout. Once grouped, screenshots can be captured from the group view.


Captured images are saved with timestamped filenames to a user-defined directory. By default, this is the folder displayed in the *Parameters* section.


Use Cases:


- Capturing viewport content (GUI and non-GUI screenshots)
- Testing multi-camera setups


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/window_manager/screenshot_advanced*
## Window Behaviour

This sample demonstrates a collection of windows designed to visualize the behavior-related methods of the *[EngineWindow](../../../api/library/gui/class.enginewindow_cpp.md)* class.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/window_manager/window_behaviour*
## Window Cameras

This sample demonstrates how to use different cameras for each window (main camera along with front, top, and right view cameras).


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/window_manager/window_cameras*
## Window Events

This sample demonstrates how to subscribe to window events via *[WindowManager](../../../api/library/gui/class.windowmanager_cpp.md)* and filter out only the ones you need. It creates a separate system viewport with a sprite element and subscribes to window events to track position and size changes. The event handler filters specific window actions like resizing and moving, automatically repositioning UI elements to maintain proper layout.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/window_manager/window_events*
## Window Intersection

This sample demonstrates how to detect intersections with various components of separate, parent, and nested windows.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/window_manager/window_intersection*
## Window Modal

Demonstration of the concept of modal windows: if a window has modal children, it cannot be closed. Any other interaction with a parent window is possible.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/window_manager/window_modal*
## Window Order

This sample demonstrates the window order and relevant features.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/window_manager/window_order*
## Window Position

This sample demonstrates visualization of the window and client position for various types of windows, changing their position to the mouse cursor or specific screen coordinates.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/window_manager/window_position*
## Window Sandbox

This sample demonstrates an interface with all available window settings for quick visualization of the result. You can create as many windows as you need, change their style or manage otherwise, create and manage window groups, and see the window status info.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/window_manager/window_sandbox*
## Window Size

This sample demonstrates visualization of the window and client size for various types of windows, setting the minimum and maximum sizes.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/window_manager/window_size*
## Window Visual

This sample demonstrates visualization of all available window parameters such as *ID* and *Gui, index, title*, possibility to add an icon, etc.


**SDK Path:***<SAMPLES_PROJECT_PATH>/source/window_manager/window_visual*
