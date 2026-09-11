# Unigine.LoadingScreen Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


A singleton that controls the settings of the [loading screen](../../../code/gui/screens/index.md#loading). Demonstration of it gives UNIGINE the time to load all world nodes and resources. You can also show your own loading screen when needed.


A loading screen displays a [texture](../../../code/gui/skin/index.md#splash) that is usually divided into two parts stacked vertically � the initial and final pictures � which are gradually blended from the beginning up to the end of loading to show the progress. Blending is performed based on the alpha channel of the outro (lower) part of the texture so pseudo-animation can be created using the alpha channel: regions of the lower half with small alpha values will be shown first, regions with larger alpha values will be shown last.


### See Also


- Quick Video Guide: [How To Customize Loading Screens](../../../videotutorials/how_to/how_to_cs/loading_screen.md)
- UnigineScript samples:

  -
  -
  -


## LoadingScreen Class

### Members

## const char * getMessage () const

Returns the current text message representing the current loading stage.
### Return value

Current text message representing the current loading stage.
## int getProgress () const

Returns the current progress state.
### Return value

Current progress state in the **[0, 100]** range.
## void setMessageShadersCompilation ( string compilation )

Sets a new message displayed on shaders compilation. The text [aliases](#setText_cstr_void) are also supported.
### Arguments

- *string* **compilation** - The message displayed on shaders compilation.

## const char * getMessageShadersCompilation () const

Returns the current message displayed on shaders compilation. The text [aliases](#setText_cstr_void) are also supported.
### Return value

Current message displayed on shaders compilation.
## void setMessageLoadingWorld ( string world )

Sets a new message displayed on world loading. The text [aliases](#setText_cstr_void) are also supported.
### Arguments

- *string* **world** - The message displayed on world loading.

## const char * getMessageLoadingWorld () const

Returns the current message displayed on world loading. The text [aliases](#setText_cstr_void) are also supported.
### Return value

Current message displayed on world loading.
## void setFontPath ( string path )

Sets a new path to the font used to render the text.
### Arguments

- *string* **path** - The path to the font used to render the text (True Type Font).

## const char * getFontPath () const

Returns the current path to the font used to render the text.
### Return value

Current path to the font used to render the text (True Type Font).
## void setText ( string text )

Sets a new text of the loading screen.
### Arguments

- *string* **text** - The text of the loading screen. Can be either a plain or [rich text](../../../code/gui/ui/index.md#rich_text). A number of aliases is available:

  - UNIGINE_COPYRIGHT � the UNIGINE copyright text.
  - UNIGINE_VERSION � the current UNIGINE version.
  - LOADING_PROGRESS � the loading progress going from 0 to 100.
  - LOADING_WORLD � the world being loaded (if any).

## const char * getText () const

Returns the current text of the loading screen.
### Return value

Current
text of the loading screen. Can be either a plain or [rich text](../../../code/gui/ui/index.md#rich_text). A number of aliases is available:


- UNIGINE_COPYRIGHT � the UNIGINE copyright text.
- UNIGINE_VERSION � the current UNIGINE version.
- LOADING_PROGRESS � the loading progress going from 0 to 100.
- LOADING_WORLD � the world being loaded (if any).


## void setBackgroundColor ( vec4 color )

Sets a new background color of the loading screen.
### Arguments

- *vec4* **color** - The background color of the loading screen.

## vec4 getBackgroundColor () const

Returns the current background color of the loading screen.
### Return value

Current background color of the loading screen.
## void setTransform ( vec4 transform )

Sets a new transformation of the loading screen texture.
### Arguments

- *vec4* **transform** - The Transformation of the loading screen texture:

  1. Texture size multiplier.
  2. Window size multiplier.
  3. Horizontal position in the [0.0f, 1.0f] range.
  4. Vertical position in the [0.0f, 1.0f] range.

## vec4 getTransform () const

Returns the current transformation of the loading screen texture.
### Return value

Current Transformation of the loading screen texture:
1. Texture size multiplier.
2. Window size multiplier.
3. Horizontal position in the [0.0f, 1.0f] range.
4. Vertical position in the [0.0f, 1.0f] range.


## void setTexturePath ( string path )

Sets a new path to the texture for the loading screen.
### Arguments

- *string* **path** - The path to a file with the custom loading screen texture. If the value equals to NULL (0), no texture is used.

## const char * getTexturePath () const

Returns the current path to the texture for the loading screen.
### Return value

Current path to a file with the custom loading screen texture. If the value equals to NULL (0), no texture is used.
## void setThreshold ( int threshold )

Sets a new amount of blur in the alpha channel when interpolating between states of the loading screen.
> **Notice:** By default, the Threshold value is set to 16.


### Arguments

- *int* **threshold** - The amount of blur in the **[0, 255]** range.

## int getThreshold () const

Returns the current amount of blur in the alpha channel when interpolating between states of the loading screen.
> **Notice:** By default, the Threshold value is set to 16.


### Return value

Current amount of blur in the **[0, 255]** range.
## void setEnabled ( int enabled )

Sets a new value indicating if manual rendering of a loading screen is allowed.
> **Notice:** Enabling manual rendering is possible only together with the corresponding **render** functions (*[render()](#render_void)*). It cannot be used to enable or disable rendering of the loading screen during the initialization stage of the engine.


### Arguments

- *int* **enabled** - The rendering of the loading screen

## int isEnabled () const

Returns the current value indicating if manual rendering of a loading screen is allowed.
> **Notice:** Enabling manual rendering is possible only together with the corresponding **render** functions (*[render()](#render_void)*). It cannot be used to enable or disable rendering of the loading screen during the initialization stage of the engine.


### Return value

Current rendering of the loading screen
## static getEventRenderEnd () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
## static getEventRenderBegin () const

The event handler signature is as follows: *myhandler()*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp

```

</details>

### Return value

Event instance.
---

## void engine.loading_screen. setImage ( Image image )

Sets an [image](../../../code/gui/skin/index.md#splash) for a custom loading screen.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image** - Image to be used as a custom loading screen.

## void engine.loading_screen. getImage ( Image image )

Returns the current [image](../../../code/gui/skin/index.md#splash) for a custom loading screen.
### Arguments

- *[Image](../../../api/library/common/class.image_usc.md)* **image**

## void engine.loading_screen. renderInterface ( )

Renders a static loading screen. Such a screen does not display any progress.
## void engine.loading_screen. render ( )

Renders the loading screen in the current progress state and with the current stage message.
## void engine.loading_screen. render ( int progress )

Renders a custom loading screen in a given progress state. Use this function in a loop to create a gradual change between the initial (upper opaque part) and the final states (bottom transparent part) of the loading screen texture.
### Arguments

- *int* **progress** - Progress of alpha blending between 2 screens stored in the texture. The value in range **[0;100]** sets an alpha channel threshold, according to which pixels from the *initial* (opaque) or *final* (transparent) screen in the texture are rendered. By the value of **0**, the initial screen is loaded. By the value of **100**, the final screen is loaded.

## void engine.loading_screen. render ( int progress , string message )

Renders a custom loading screen in a given progress state and prints a given message. Use this function in a loop to create a gradual change between the initial (upper opaque part) and the final states (bottom transparent part) of the loading screen texture, while printing a custom loading stage.
### Arguments

- *int* **progress** - Progress of alpha blending between 2 loading screens stored in the texture. The value in range **[0;100]** sets an alpha channel threshold, according to which pixels from the *initial* (opaque) or *final* (transparent) loading screen in the texture are rendered. By the value of **0**, the initial screen is loaded. By the value of **100**, the final screen is loaded.
- *string* **message** - message to print representing the loading stage.

## void engine.loading_screen. renderForce ( )

Renders the loading screen regardless of whether the manual rendering is allowed or not.
## void engine.loading_screen. renderForce ( string message )

Renders the loading screen regardless of whether the manual rendering is allowed or not and prints a given message.
### Arguments

- *string* **message** - message to print that represents the loading stage.
