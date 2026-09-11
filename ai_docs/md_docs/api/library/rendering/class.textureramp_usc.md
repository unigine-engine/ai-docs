# Unigine.TextureRamp Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.


Interface for handling ramp textures. This class lets the user store 2d curves in a form of a texture (convert vectors to raster data).


Ramp textures can be used for color variation in the [particles_base](../../../content/materials/library/particles_base/index.md) material of Particle Systems or in other custom materials.


![](texturecurve_editor.png)


You can set up to 4 channels for the ramp texture.


## TextureRamp Class

### Members

## Texture getTexture () const

Returns the current new texture and updates hashes for curves, if required. Returns a pointer to the texture or null if the texture was not created.
### Return value

Current new texture.
## void setNumChannels ( int channels )

Sets a new number of channels for the texture.
### Arguments

- *int* **channels** - The number of texture channels.

## int getNumChannels () const

Returns the current number of channels for the texture.
### Return value

Current number of texture channels.
## void setResolution ( int resolution )

Sets a new width resolution for the texture.
### Arguments

- *int* **resolution** - The texture width resolution.

## int getResolution () const

Returns the current width resolution for the texture.
### Return value

Current texture width resolution.
## void setFlags ( int flags )

Sets a new texture flags.
### Arguments

- *int* **flags** - The texture flags.

## int getFlags () const

Returns the current texture flags.
### Return value

Current texture flags.
## isDefaultAll () const

Returns the current value indicating if the values of all curve channels are the default ones which were previously set via *[setDefaultCurve()()](../../...md#setDefaultCurve_int_Curve2d_void)*.
### Return value

Current the values of all curve channels are the default ones which were previously set via *[setDefaultCurve()()](../../...md#setDefaultCurve_int_Curve2d_void)*
## getEventChanged () const

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

## static TextureRamp ( int num_channels , int resolution , int flags )

Sets resolution, number of channels and texture flags for this TextureRamp instance. The pointer to the ramp texture is set to null and curves are marked for an update.
### Arguments

- *int* **num_channels** - Number of texture channels.
- *int* **resolution** - Width resolution of the ramp texture.
- *int* **flags** - Texture flags.

## TextureRamp ( )

## void releaseTexture ( )

Deletes the texture and its pointer.
## void copy ( TextureRamp src_texture_ramp )

Copies the data of a source ramp texture to the texture.
### Arguments

- *[TextureRamp](../../../api/library/rendering/class.textureramp_usc.md)* **src_texture_ramp** - Source ramp texture.

## TextureRamp clone ( )

Duplicates the ramp texture and returns a pointer to the copy.
## Curve2d getCurve ( int channel )

Returns a pointer to the [Curve2d](../../../api/library/common/class.curve2d_usc.md) for the specified channel.
### Arguments

- *int* **channel** - Required channel.

### Return value

Pointer to a Curve2d object.
## void setDefaultCurve ( Curve2d default_curve )

Resets a curve to a default one.
### Arguments

- *[Curve2d](../../../api/library/common/class.curve2d_usc.md)* **default_curve** - A curve to be used as the default one.

## void setDefaultCurve ( int channel , const Curve2d default_curve )

Resets a curve for the given channel to a default one.
### Arguments

- *int* **channel** - R, G, B, or A channel set by the corresponding value from 0 to 3.
- *const [Curve2d](../../../api/library/common/class.curve2d_usc.md)* **default_curve** - A curve to be used as the default one.

## int isDefault ( int channel )

Returns a value indicating if the value of the given curve channel is the default one which was previously set via [setDefaultCurve](#setDefaultCurve_int_Curve2d_void).
### Arguments

- *int* **channel** - R, G, B, or A channel set by the corresponding value from 0 to 3.

### Return value

**1** if the curve value is the default one set via [setDefaultCurve](#setDefaultCurve_int_Curve2d_void), otherwise **0**.
## void save ( Xml xml )

Saves the ramp texture data to the given [Xml](../../../api/library/common/class.xml_usc.md) node.
### Arguments

- *[Xml](../../../api/library/common/class.xml_usc.md)* **xml** - Target Xml node.

## void load ( const Xml xml )

Loads the ramp texture data from the given [Xml](../../../api/library/common/class.xml_usc.md) node.
### Arguments

- *const [Xml](../../../api/library/common/class.xml_usc.md)* **xml** - Source Xml node containing ramp texture data.

## void saveState ( const Stream stream )


Saves the state of the ramp texture into a binary stream.


**Example** using *saveState()* and *[restoreState()](#restoreState_Stream_void)* methods:


```cpp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
ramp.saveState(blob_state);

// change state
//...//

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
ramp.restoreState(blob_state);

```


### Arguments

- *const [Stream](../../../api/library/common/class.stream_usc.md)* **stream** - The stream to save the ramp texture state data.

## void restoreState ( const Stream stream )


Restores the state of the ramp texture from the binary stream.


**Example** using *[saveState()](#saveState_Stream_void)* and *restoreState()* methods:


```cpp
// initialize a node and set its state
//...//

// save state
Blob blob_state = new Blob();
ramp.saveState(blob_state);

// change state
//...//

// restore state
blob_state.seekSet(0); // returning the carriage to the start of the blob
ramp.restoreState(blob_state);

```


### Arguments

- *const [Stream](../../../api/library/common/class.stream_usc.md)* **stream** - The stream that stores the ramp texture state data.
