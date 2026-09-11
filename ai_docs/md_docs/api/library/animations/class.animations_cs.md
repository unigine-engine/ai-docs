# Unigine::Animations Class (CS)


This class gives access to what the animation system knows about itself: which parameters of the engine can be animated at all, what kind of [channel](../../../api/library/animations/timeline/class.animationchannel_cs.md) each of them needs, and how a parameter is shown and edited. A tool that builds a [sequence](../../../api/library/animations/timeline/class.animationsequence_cs.md) from code asks these questions before it creates a channel.


The same singleton also drives the animation scripts: it rebuilds them, reports whether the build succeeded and tells when a custom library has been built.


Every parameter the engine allows to animate has an identifier of its own, and those identifiers make up a registry generated from the engine classes. It holds thousands of entries and is not meant to be typed out by hand: look an identifier up by name with *[GetParameterByName()](../../...md#getParameterByName_cstr_int)* or *[GetParameterByReflectionName()](../../...md#getParameterByReflectionName_cstr_cstr_int)*, and ask this class about everything else it carries, from the channel type it needs to the title it is shown under.


## Animations Class

### Properties

## 🔒︎ size_t MemoryUsage

The amount of memory taken by the animation system, in bytes.
## 🔒︎ bool AnimScriptsLoaded

The value indicating if the animation scripts are loaded.
## 🔒︎ bool AnimScriptsRebuilding

The value indicating if the animation scripts are being rebuilt right now.
## 🔒︎ bool AnimScriptsSuccessBuild

The value indicating if the last build of the animation scripts succeeded.
## bool AnimScriptsPreviewBuild

The value indicating if the animation scripts are built in the preview mode.
## 🔒︎ int NumAnimScriptTypes

The number of animation script types the engine knows.
## 🔒︎ Event<string, string, string> EventCustomLibBuild

The event triggered when a custom animation library has been built. You can subscribe to events via *Connect()* and unsubscribe via *Disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cs.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cs.md)* classes for convenience.
> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cs.md) article.

The event handler signature is as follows: *myhandler(string **name**, string **path**, string **message**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```csharp
// implement the CustomLibBuild event handler
void customlibbuild_event_handler(string name, string path, string message)
{
	Log.Message("\Handling CustomLibBuild event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an EventConnections instance
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections customlibbuild_event_connections = new EventConnections();

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher.EventCustomLibBuild.Connect(customlibbuild_event_connections, customlibbuild_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher.EventCustomLibBuild.Connect(customlibbuild_event_connections, (string name, string path, string message) => {
		Log.Message("Handling CustomLibBuild event lambda\n");
		}
	);

// later all of these linked subscriptions can be removed with a single line
customlibbuild_event_connections.DisconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via the handler function directly
//////////////////////////////////////////////////////////////////////////////

// subscribe to the CustomLibBuild event with a handler function
publisher.EventCustomLibBuild.Connect(customlibbuild_event_handler);

// remove subscription to the CustomLibBuild event later by the handler function
publisher.EventCustomLibBuild.Disconnect(customlibbuild_event_handler);

//////////////////////////////////////////////////////////////////////////////
//   3. Subscribe to an event and unsubscribe later via an EventConnection instance
//////////////////////////////////////////////////////////////////////////////

// define a connection to be used to unsubscribe later
EventConnection customlibbuild_event_connection;

// subscribe to the CustomLibBuild event with a lambda handler function and keeping the connection
customlibbuild_event_connection = publisher.EventCustomLibBuild.Connect((string name, string path, string message) => {
		Log.Message("Handling CustomLibBuild event lambda\n");
	}
);

// ...

// you can temporarily disable a particular event connection
customlibbuild_event_connection.Enabled = false;

// ... perform certain actions

// and enable it back when necessary
customlibbuild_event_connection.Enabled = true;

// ...

// remove the subscription later using the saved connection
customlibbuild_event_connection.Disconnect();

//////////////////////////////////////////////////////////////////////////////
//   4. Ignoring CustomLibBuild events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher.EventCustomLibBuild.Enabled = false;

// ... actions to be performed

// and enable it back when necessary
publisher.EventCustomLibBuild.Enabled = true;

```

</details>

### Members

---

## void RestoreEachFrame ( )

Restores the original values of every player that is set to give them back each frame. The engine calls it on its own, once per frame.
## void SetComponentWritesCollecting ( bool enabled )

Starts or stops collecting the writes made to component fields, which is how the editor learns what a running component changes.
### Arguments

- *bool* **enabled** - true to start collecting, false to stop.

## void FetchComponentWrites ( Blob blob )

Takes the writes collected so far and puts them into the specified blob.
### Arguments

- *[Blob](../../../api/library/common/class.blob_cs.md)* **blob** - Blob to put the collected writes into.

## void SetSequencerMusicMuted ( bool muted )

Mutes the music channels of every sequence that is playing.
### Arguments

- *bool* **muted** - true to mute the music, false to let it play.

## int GetClasses ( string[] OUT_out_classes )

Collects the names of every class the animation system knows and puts them to the **out_classes** buffer.
### Arguments

- *string[]* **OUT_out_classes** - Output buffer for the class names. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of class names put to the buffer.
## int GetBaseClasses ( string[] OUT_out_classes )

Collects the names of the base classes of the animation system and puts them to the **out_classes** buffer.
### Arguments

- *string[]* **OUT_out_classes** - Output buffer for the class names. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of class names put to the buffer.
## int GetSingletonClasses ( string[] OUT_out_classes )

Collects the names of the singleton classes that can be animated and puts them to the **out_classes** buffer.
### Arguments

- *string[]* **OUT_out_classes** - Output buffer for the class names. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of class names put to the buffer.
## string GetParentClass ( string class_name )

Returns the class the specified one inherits from.
### Arguments

- *string* **class_name** - Name of the class.

### Return value

Name of the parent class.
## int GetDerivedClasses ( string class_name , string[] OUT_out_classes )

Collects the classes that inherit from the specified one.
### Arguments

- *string* **class_name** - Name of the class.
- *string[]* **OUT_out_classes** - Output buffer for the class names. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of class names put to the buffer.
## int GetClassParameters ( string class_name , int[] OUT_out_parameters )

Collects the parameters the specified class exposes to animation.
### Arguments

- *string* **class_name** - Name of the class.
- *int[]* **OUT_out_parameters** - Output buffer for the parameters. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of parameters put to the buffer.
## string GetParameterClass ( AnimParams.PARAM param )

Returns the class the specified parameter belongs to.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.

### Return value

Name of the class the parameter belongs to.
## AnimationBind.TYPE GetParameterBindType ( AnimParams.PARAM param )

Returns the kind of binding a channel needs to animate the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.

### Return value

Kind of binding the parameter needs.
## bool IsParameterTarget ( AnimParams.PARAM param , Node node )

Returns a value indicating if the specified node is a target the parameter can be written into, that is, if the node is of the class the parameter belongs to. It answers whether a target may be accepted before a channel is pointed at it.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.
- *[Node](../../../api/library/nodes/class.node_cs.md)* **node** - Node to be checked as the target.

### Return value

true if the specified parameter can be animated on the specified node; otherwise, false.
## string GetParameterName ( AnimParams.PARAM param )

Returns the name of the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.

### Return value

Name of the parameter.
## AnimationChannel.TYPE GetParameterChannelType ( AnimParams.PARAM param )

Returns the type of channel that animates the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.

### Return value

Type of the channel that animates the parameter.
## AnimParams.WIDGET GetParameterWidget ( AnimParams.PARAM param )

Returns the widget the specified parameter is edited with in the interface.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.

### Return value

Widget the parameter is edited with.
## string GetParameterItems ( AnimParams.PARAM param )

Returns the items of the specified parameter, which is what an enumeration offers to choose from.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.

### Return value

Items of the parameter, when it is an enumeration.
## string GetParameterNodeType ( AnimParams.PARAM param )

Returns the node type the specified parameter accepts.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.

### Return value

Node type the parameter accepts.
## AnimParams.ACCESS GetParameterAccess ( AnimParams.PARAM param )

Returns the way the specified parameter is reached on its object.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.

### Return value

Way the parameter is reached.
## AnimParams.VEC_COMPONENT GetParameterVecComponent ( AnimParams.PARAM param )

Returns the component of a vector the specified parameter stands for.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.

### Return value

Component of the vector the parameter stands for.
## string GetParameterLogicalName ( AnimParams.PARAM param )

Returns the logical name of the specified parameter, which groups the components of one value together.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.

### Return value

Logical name of the parameter.
## string GetParameterKeyName ( AnimParams.PARAM param )

Returns the key name the specified parameter is stored under.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.

### Return value

Key name of the parameter.
## string GetParameterTitle ( AnimParams.PARAM param )

Returns the title the specified parameter is shown under in the interface.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.

### Return value

Title of the parameter.
## string GetParameterMinValue ( AnimParams.PARAM param )

Returns the lower bound of the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.

### Return value

Lower bound of the parameter.
## string GetParameterMaxValue ( AnimParams.PARAM param )

Returns the upper bound of the specified parameter.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.

### Return value

Upper bound of the parameter.
## string GetParameterAssetExtension ( AnimParams.PARAM param )

Returns the extension of the assets the specified parameter accepts.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.

### Return value

Extension of the assets the parameter accepts.
## string GetParameterSlotKindName ( AnimParams.PARAM param )

Returns the name of the kind of slot the specified parameter is indexed by, such as a surface or a bone.
### Arguments

- *AnimParams.PARAM* **param** - Parameter to be asked about.

### Return value

Name of the slot kind of the parameter.
## AnimParams.PARAM GetParameterByName ( string param_name )

Returns the parameter that goes by the specified name.
### Arguments

- *string* **param_name** - Name of the parameter.

### Return value

Parameter that goes by the specified name.
## AnimParams.PARAM GetParameterByReflectionName ( string class_name , string prop_name )

Returns the parameter a class member is animated through, addressed the way the reflection names it.
### Arguments

- *string* **class_name** - Name of the class.
- *string* **prop_name** - Name of the property as the reflection reports it.

### Return value

Parameter that answers to the specified names.
## bool ReadParameterValueFloat ( Node target , AnimParams.PARAM param , int param_index , int component , string param_name , out float out_value )

Reads the current value of an animatable parameter straight from a node, which is what recording a key from the scene is built on.
### Arguments

- *[Node](../../../api/library/nodes/class.node_cs.md)* **target** - Node to read the value from.
- *AnimParams.PARAM* **param** - Parameter to be asked about.
- *int* **param_index** - Slot of the parameter, or -1 when it has none.
- *int* **component** - Component of the value to be read.
- *string* **param_name** - Name that addresses the parameter when a number is not enough.
- *out float* **out_value** - Output buffer for the value.

### Return value

true if the value was read; otherwise, false.
## bool ReadChannelParameterValueFloat ( AnimationChannel channel , int component , out float out_value )

Reads the current value of the parameter the specified channel animates.
### Arguments

- *[AnimationChannel](../../../api/library/animations/timeline/class.animationchannel_cs.md)* **channel** - Channel to be asked about.
- *int* **component** - Component of the value to be read.
- *out float* **out_value** - Output buffer for the value.

### Return value

true if the value was read; otherwise, false.
## string ReadChannelParameterValueString ( AnimationChannel channel )

Reads the current value of the parameter the specified channel animates.
### Arguments

- *[AnimationChannel](../../../api/library/animations/timeline/class.animationchannel_cs.md)* **channel** - Channel to be asked about.

### Return value

Current value of the parameter.
## UGUID ReadChannelParameterValueUGUID ( AnimationChannel channel )

Reads the current value of the parameter the specified channel animates.
### Arguments

- *[AnimationChannel](../../../api/library/animations/timeline/class.animationchannel_cs.md)* **channel** - Channel to be asked about.

### Return value

Current value of the parameter.
## Node ReadChannelParameterValueNode ( AnimationChannel channel )

Reads the current value of the parameter the specified channel animates.
### Arguments

- *[AnimationChannel](../../../api/library/animations/timeline/class.animationchannel_cs.md)* **channel** - Channel to be asked about.

### Return value

Current value of the parameter.
## int GetChannelSlotCount ( AnimationChannel channel )

Returns how many slots the parameter of the specified channel offers, such as the surfaces of an object or the bones of a skeleton.
### Arguments

- *[AnimationChannel](../../../api/library/animations/timeline/class.animationchannel_cs.md)* **channel** - Channel to be asked about.

### Return value

Number of slots the parameter of the channel offers.
## int GetChannelSlotNames ( AnimationChannel channel , string[] OUT_out_names )

Collects the names of the slots the parameter of the specified channel offers.
### Arguments

- *[AnimationChannel](../../../api/library/animations/timeline/class.animationchannel_cs.md)* **channel** - Channel to be asked about.
- *string[]* **OUT_out_names** - Output buffer for the slot names. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of slot names put to the buffer.
## int GetChannelSlotIndex ( AnimationChannel channel , string name )

Looks a slot of the channel parameter up by name and returns the number it takes on the object the channel is currently bound to. It is the counterpart of [getChannelSlotNames()](#getChannelSlotNames_AnimationChannel_VECString_int) for a channel that addresses its slot by name, see [SlotAccess](../../../api/library/animations/timeline/class.animationchannel_cs.md#SlotAccess).
### Arguments

- *[AnimationChannel](../../../api/library/animations/timeline/class.animationchannel_cs.md)* **channel** - Channel to be asked about.
- *string* **name** - Name of the slot to be looked up.

### Return value

Number of the slot, or -1 if the parameter offers no slots or the object the channel is bound to has none under that name.
## bool IsChannelParameterReadable ( AnimationChannel channel )

Returns a value indicating if the current value of the channel parameter can be read from the scene. It cannot when the object the channel is bound to is not there to be resolved, or when the channel addresses a slot that object does not have.
### Arguments

- *[AnimationChannel](../../../api/library/animations/timeline/class.animationchannel_cs.md)* **channel** - Channel to be checked.

### Return value

true if the current value of the channel parameter can be read; otherwise, false.
## int GetChannelSupportedProperties ( AnimationChannel.TYPE channel_type , int[] OUT_out_kinds )

Collects the playback properties a channel of the specified type offers, such as the pitch and the fades of a sound.
### Arguments

- *[AnimationChannel.TYPE](../../../api/library/animations/timeline/class.animationchannel_cs.md#TYPE)* **channel_type** - Type of the channel.
- *int[]* **OUT_out_kinds** - Output buffer for the playback property kinds. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of kinds put to the buffer.
## string GetChannelPropertyName ( AnimationChannel.PROPERTY kind )

Returns the name of the specified playback property.
### Arguments

- *[AnimationChannel.PROPERTY](../../../api/library/animations/timeline/class.animationchannel_cs.md#PROPERTY)* **kind** - Kind of the playback property.

### Return value

Name of the playback property.
## float GetChannelPropertyDefaultValue ( AnimationChannel.PROPERTY kind )

Returns the value the specified playback property holds until it is animated.
### Arguments

- *[AnimationChannel.PROPERTY](../../../api/library/animations/timeline/class.animationchannel_cs.md#PROPERTY)* **kind** - Kind of the playback property.

### Return value

Default value of the playback property.
## float GetChannelPropertyMinValue ( AnimationChannel.PROPERTY kind )

Returns the lower bound of the specified playback property.
### Arguments

- *[AnimationChannel.PROPERTY](../../../api/library/animations/timeline/class.animationchannel_cs.md#PROPERTY)* **kind** - Kind of the playback property.

### Return value

Lower bound of the playback property.
## float GetChannelPropertyMaxValue ( AnimationChannel.PROPERTY kind )

Returns the upper bound of the specified playback property.
### Arguments

- *[AnimationChannel.PROPERTY](../../../api/library/animations/timeline/class.animationchannel_cs.md#PROPERTY)* **kind** - Kind of the playback property.

### Return value

Upper bound of the playback property.
## bool AnimToBonesChannel ( string anim_path , AnimationChannelBones out_channel , float duration )

Bakes a skeletal animation file into a bones channel, so that its pose can be edited key by key in the Sequencer.
### Arguments

- *string* **anim_path** - Path to the animation file.
- *[AnimationChannelBones](../../../api/library/animations/timeline/class.animationchannelbones_cs.md)* **out_channel** - Channel to receive the baked keys.
- *float* **duration** - Length the animation is baked over, in seconds.

### Return value

true if the animation was baked; otherwise, false.
## String ConvertLegacyTrackToSequence ( string track_path , string seq_path = "" , bool overwrite = false )

Converts a track authored in the legacy Tracker into a sequence. A track that plays other tracks inside itself is converted whole: every nested track becomes a sequence file of its own and the parent receives a sub-sequence channel whose clips point at them, so overwriting rebuilds the entire tree rather than the file that was named. Everything the conversion could not carry over is reported to the console, one line per parameter. The whole picture is in the [Converting Legacy Tracks](../../../editor2/tools/sequencer/track_import/index.md) article.
### Arguments

- *string* **track_path** - Path to the legacy `*.track` file to be converted.
- *string* **seq_path** - Path the `*.seq` file is to be written to. Left empty, the sequence is written beside the track under the same name. The default value is an empty string.
- *bool* **overwrite** - true to convert the track again and replace a `*.seq` that is already there, false to keep the existing file and write nothing. The default value is false.

### Return value

Path of the sequence file, or an empty string if nothing was written.
## void RebuildAnimScripts ( )

Rebuilds the animation scripts of the project.
## void WaitAnimScriptsRebuilding ( )

Blocks until the rebuild of the animation scripts is over.
## string GetAnimScriptTypeName ( int type_index )

Returns the name of an animation script type by its number.
### Arguments

- *int* **type_index** - Number of the animation script type.

### Return value

Name of the animation script type.
