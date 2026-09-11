# Unigine::Animations Class (CPP)

**Header:** #include <UnigineAnimation.h>


This class gives access to what the animation system knows about itself: which parameters of the engine can be animated at all, what kind of [channel](../../../api/library/animations/timeline/class.animationchannel_cpp.md) each of them needs, and how a parameter is shown and edited. A tool that builds a [sequence](../../../api/library/animations/timeline/class.animationsequence_cpp.md) from code asks these questions before it creates a channel.


The same singleton also drives the animation scripts: it rebuilds them, reports whether the build succeeded and tells when a custom library has been built.


Every parameter the engine allows to animate has an identifier of its own, and those identifiers make up a registry generated from the engine classes. It holds thousands of entries and is not meant to be typed out by hand: look an identifier up by name with *[getParameterByName()](../../...md#getParameterByName_cstr_int)* or *[getParameterByReflectionName()](../../...md#getParameterByReflectionName_cstr_cstr_int)*, and ask this class about everything else it carries, from the channel type it needs to the title it is shown under.


## Animations Class

### Members

## size_t getMemoryUsage () const

Returns the current amount of memory taken by the animation system, in bytes.
### Return value

Current memory taken by the animation system, in bytes
## bool isAnimScriptsLoaded () const

Returns the current value indicating if the animation scripts are loaded.
### Return value

**true** if the animation scripts are loaded; otherwise **false**.
## bool isAnimScriptsRebuilding () const

Returns the current value indicating if the animation scripts are being rebuilt right now.
### Return value

**true** if the animation scripts are being rebuilt; otherwise **false**.
## bool isAnimScriptsSuccessBuild () const

Returns the current value indicating if the last build of the animation scripts succeeded.
### Return value

**true** if the last build of the animation scripts succeeded; otherwise **false**.
## void setAnimScriptsPreviewBuild ( bool build )

Sets a new value indicating if the animation scripts are built in the preview mode.
### Arguments

- *bool* **build** - Set **true** to enable the preview build of the animation scripts; **false** - to disable it.

## bool isAnimScriptsPreviewBuild () const

Returns the current value indicating if the animation scripts are built in the preview mode.
### Return value

**true** if the preview build of the animation scripts is enabled ; otherwise **false**.
## int getNumAnimScriptTypes () const

Returns the current number of animation script types the engine knows.
### Return value

Current number of animation script types
## Event<const char *, const char *, const char *> getEventCustomLibBuild () const

event triggered when a custom animation library has been built. You can subscribe to events via *connect()* and unsubscribe via *disconnect()*. You can also use *[EventConnection](../../../api/library/common/events/class.eventconnection_cpp.md)* and *[EventConnections](../../../api/library/common/events/class.eventconnections_cpp.md)* classes for convenience.
> **Notice:** For more details see the [Event Handling](../../../code/fundamentals/events/index_cpp.md) article.

The event handler signature is as follows: *myhandler(const char * **name**, const char * **path**, const char * **message**)*
<details>
<summary>See Example | Close</summary>

**Usage Example**

```cpp
// implement the CustomLibBuild event handler
void customlibbuild_event_handler(const char * name, const char * path, const char * message)
{
	Log::message("\Handling CustomLibBuild event\n");
}

//////////////////////////////////////////////////////////////////////////////
//  1. Multiple subscriptions can be linked to an instance of the EventConnections
//  class that you can use later to remove all these subscriptions at once
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnections class
EventConnections customlibbuild_event_connections;

// link to this instance when subscribing to an event (subscription to various events can be linked)
publisher->getEventCustomLibBuild().connect(customlibbuild_event_connections, customlibbuild_event_handler);

// other subscriptions are also linked to this EventConnections instance
// (e.g. you can subscribe using lambdas)
publisher->getEventCustomLibBuild().connect(customlibbuild_event_connections, [](const char * name, const char * path, const char * message) {
		Log::message("\Handling CustomLibBuild event (lambda).\n");
	}
);

// ...

// later all of these linked subscriptions can be removed with a single line
customlibbuild_event_connections.disconnectAll();

//////////////////////////////////////////////////////////////////////////////
//  2. You can subscribe and unsubscribe via an instance of the EventConnection
//  class. And toggle this particular connection off and on, when necessary.
//////////////////////////////////////////////////////////////////////////////

// create an instance of the EventConnection class
EventConnection customlibbuild_event_connection;

// subscribe to the CustomLibBuild event with a handler function keeping the connection
publisher->getEventCustomLibBuild().connect(customlibbuild_event_connection, customlibbuild_event_handler);

// ...

// you can temporarily disable a particular event connection to perform certain actions
customlibbuild_event_connection.setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
customlibbuild_event_connection.setEnabled(true);

// ...

// remove subscription to the CustomLibBuild event via the connection
customlibbuild_event_connection.disconnect();

//////////////////////////////////////////////////////////////////////////////
//  3. You can add EventConnection/EventConnections instance as a member of the
//  class that handles the event. In this case all linked subscriptions will be
//  automatically removed when class destructor is called
//////////////////////////////////////////////////////////////////////////////

// Class handling the event
class SomeClass
{
public:
	// instance of the EventConnections class as a class member
	EventConnections e_connections;

	// A CustomLibBuild event handler implemented as a class member
	void event_handler(const char * name, const char * path, const char * message)
	{
		Log::message("\Handling CustomLibBuild event\n");
		// ...
	}
};

SomeClass *sc = new SomeClass();

// ...

// specify a class instance in case a handler method belongs to some class
publisher->getEventCustomLibBuild().connect(sc->e_connections, sc, &SomeClass::event_handler);

// ...

// handler class instance is deleted with all its subscriptions removed automatically
delete sc;

//////////////////////////////////////////////////////////////////////////////
//   4. Subscribe to an event saving a particular connection ID
//   and unsubscribe later by this ID
//////////////////////////////////////////////////////////////////////////////
// instance of the EventConnections class to manage event connections
EventConnections e_connections;

// define a particular connection ID to be used to unsubscribe later
EventConnectionId customlibbuild_handler_id;

// subscribe to the CustomLibBuild event with a lambda handler function and keeping connection ID
customlibbuild_handler_id = publisher->getEventCustomLibBuild().connect(e_connections, [](const char * name, const char * path, const char * message) {
		Log::message("\Handling CustomLibBuild event (lambda).\n");
	}
);

// remove the subscription later using the ID
publisher->getEventCustomLibBuild().disconnect(customlibbuild_handler_id);

//////////////////////////////////////////////////////////////////////////////
//   5. Ignoring all CustomLibBuild events when necessary
//////////////////////////////////////////////////////////////////////////////

// you can temporarily disable the event to perform certain actions without triggering it
publisher->getEventCustomLibBuild().setEnabled(false);

// ... actions to be performed

// and enable it back when necessary
publisher->getEventCustomLibBuild().setEnabled(true);

```

</details>

### Return value

Event instance.
---

## void restoreEachFrame ( )

Restores the original values of every player that is set to give them back each frame. The engine calls it on its own, once per frame.
## void setComponentWritesCollecting ( bool enabled )

Starts or stops collecting the writes made to component fields, which is how the editor learns what a running component changes.
### Arguments

- *bool* **enabled** - true to start collecting, false to stop.

## void fetchComponentWrites ( const Ptr < Blob > & blob )

Takes the writes collected so far and puts them into the specified blob.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../api/library/common/class.blob_cpp.md)> &* **blob** - Blob to put the collected writes into.

## void setSequencerMusicMuted ( bool muted )

Mutes the music channels of every sequence that is playing.
### Arguments

- *bool* **muted** - true to mute the music, false to let it play.

## int getClasses ( Vector < String > & OUT_out_classes ) const

Collects the names of every class the animation system knows and puts them to the **out_classes** buffer.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_out_classes** - Output buffer for the class names. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of class names put to the buffer.
## int getBaseClasses ( Vector < String > & OUT_out_classes ) const

Collects the names of the base classes of the animation system and puts them to the **out_classes** buffer.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_out_classes** - Output buffer for the class names. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of class names put to the buffer.
## int getSingletonClasses ( Vector < String > & OUT_out_classes ) const

Collects the names of the singleton classes that can be animated and puts them to the **out_classes** buffer.
### Arguments

- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_out_classes** - Output buffer for the class names. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of class names put to the buffer.
## const char * getParentClass ( const char * class_name ) const

Returns the class the specified one inherits from.
### Arguments

- *const char ** **class_name** - Name of the class.

### Return value

Name of the parent class.
## int getDerivedClasses ( const char * class_name , Vector < String > & OUT_out_classes ) const

Collects the classes that inherit from the specified one.
### Arguments

- *const char ** **class_name** - Name of the class.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_out_classes** - Output buffer for the class names. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of class names put to the buffer.
## int getClassParameters ( const char * class_name , Vector <int> & OUT_out_parameters ) const

Collects the parameters the specified class exposes to animation.
### Arguments

- *const char ** **class_name** - Name of the class.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **OUT_out_parameters** - Output buffer for the parameters. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of parameters put to the buffer.
## const char * getParameterClass ( AnimParams::PARAM param ) const

Returns the class the specified parameter belongs to.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.

### Return value

Name of the class the parameter belongs to.
## AnimationBind::TYPE getParameterBindType ( AnimParams::PARAM param ) const

Returns the kind of binding a channel needs to animate the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.

### Return value

Kind of binding the parameter needs.
## bool isParameterTarget ( AnimParams::PARAM param , const Ptr < Node > & node ) const

Returns a value indicating if the specified node is a target the parameter can be written into, that is, if the node is of the class the parameter belongs to. It answers whether a target may be accepted before a channel is pointed at it.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **node** - Node to be checked as the target.

### Return value

true if the specified parameter can be animated on the specified node; otherwise, false.
## const char * getParameterName ( AnimParams::PARAM param ) const

Returns the name of the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.

### Return value

Name of the parameter.
## AnimationChannel::TYPE getParameterChannelType ( AnimParams::PARAM param ) const

Returns the type of channel that animates the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.

### Return value

Type of the channel that animates the parameter.
## AnimParams::WIDGET getParameterWidget ( AnimParams::PARAM param ) const

Returns the widget the specified parameter is edited with in the interface.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.

### Return value

Widget the parameter is edited with.
## const char * getParameterItems ( AnimParams::PARAM param ) const

Returns the items of the specified parameter, which is what an enumeration offers to choose from.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.

### Return value

Items of the parameter, when it is an enumeration.
## const char * getParameterNodeType ( AnimParams::PARAM param ) const

Returns the node type the specified parameter accepts.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.

### Return value

Node type the parameter accepts.
## AnimParams::ACCESS getParameterAccess ( AnimParams::PARAM param ) const

Returns the way the specified parameter is reached on its object.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.

### Return value

Way the parameter is reached.
## AnimParams::VEC_COMPONENT getParameterVecComponent ( AnimParams::PARAM param ) const

Returns the component of a vector the specified parameter stands for.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.

### Return value

Component of the vector the parameter stands for.
## const char * getParameterLogicalName ( AnimParams::PARAM param ) const

Returns the logical name of the specified parameter, which groups the components of one value together.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.

### Return value

Logical name of the parameter.
## const char * getParameterKeyName ( AnimParams::PARAM param ) const

Returns the key name the specified parameter is stored under.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.

### Return value

Key name of the parameter.
## const char * getParameterTitle ( AnimParams::PARAM param ) const

Returns the title the specified parameter is shown under in the interface.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.

### Return value

Title of the parameter.
## const char * getParameterMinValue ( AnimParams::PARAM param ) const

Returns the lower bound of the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.

### Return value

Lower bound of the parameter.
## const char * getParameterMaxValue ( AnimParams::PARAM param ) const

Returns the upper bound of the specified parameter.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.

### Return value

Upper bound of the parameter.
## const char * getParameterAssetExtension ( AnimParams::PARAM param ) const

Returns the extension of the assets the specified parameter accepts.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.

### Return value

Extension of the assets the parameter accepts.
## const char * getParameterSlotKindName ( AnimParams::PARAM param ) const

Returns the name of the kind of slot the specified parameter is indexed by, such as a surface or a bone.
### Arguments

- *AnimParams::PARAM* **param** - Parameter to be asked about.

### Return value

Name of the slot kind of the parameter.
## AnimParams::PARAM getParameterByName ( const char * param_name ) const

Returns the parameter that goes by the specified name.
### Arguments

- *const char ** **param_name** - Name of the parameter.

### Return value

Parameter that goes by the specified name.
## AnimParams::PARAM getParameterByReflectionName ( const char * class_name , const char * prop_name ) const

Returns the parameter a class member is animated through, addressed the way the reflection names it.
### Arguments

- *const char ** **class_name** - Name of the class.
- *const char ** **prop_name** - Name of the property as the reflection reports it.

### Return value

Parameter that answers to the specified names.
## bool readParameterValueFloat ( const Ptr < Node > & target , AnimParams::PARAM param , int param_index , int component , const char * param_name , float & out_value ) const

Reads the current value of an animatable parameter straight from a node, which is what recording a key from the scene is built on.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[Node](../../../api/library/nodes/class.node_cpp.md)> &* **target** - Node to read the value from.
- *AnimParams::PARAM* **param** - Parameter to be asked about.
- *int* **param_index** - Slot of the parameter, or -1 when it has none.
- *int* **component** - Component of the value to be read.
- *const char ** **param_name** - Name that addresses the parameter when a number is not enough.
- *float &* **out_value** - Output buffer for the value.

### Return value

true if the value was read; otherwise, false.
## bool readChannelParameterValueFloat ( const Ptr < AnimationChannel > & channel , int component , float & out_value ) const

Reads the current value of the parameter the specified channel animates.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AnimationChannel](../../../api/library/animations/timeline/class.animationchannel_cpp.md)> &* **channel** - Channel to be asked about.
- *int* **component** - Component of the value to be read.
- *float &* **out_value** - Output buffer for the value.

### Return value

true if the value was read; otherwise, false.
## String readChannelParameterValueString ( const Ptr < AnimationChannel > & channel ) const

Reads the current value of the parameter the specified channel animates.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AnimationChannel](../../../api/library/animations/timeline/class.animationchannel_cpp.md)> &* **channel** - Channel to be asked about.

### Return value

Current value of the parameter.
## UGUID readChannelParameterValueUGUID ( const Ptr < AnimationChannel > & channel ) const

Reads the current value of the parameter the specified channel animates.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AnimationChannel](../../../api/library/animations/timeline/class.animationchannel_cpp.md)> &* **channel** - Channel to be asked about.

### Return value

Current value of the parameter.
## Ptr < Node > readChannelParameterValueNode ( const Ptr < AnimationChannel > & channel ) const

Reads the current value of the parameter the specified channel animates.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AnimationChannel](../../../api/library/animations/timeline/class.animationchannel_cpp.md)> &* **channel** - Channel to be asked about.

### Return value

Current value of the parameter.
## int getChannelSlotCount ( const Ptr < AnimationChannel > & channel ) const

Returns how many slots the parameter of the specified channel offers, such as the surfaces of an object or the bones of a skeleton.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AnimationChannel](../../../api/library/animations/timeline/class.animationchannel_cpp.md)> &* **channel** - Channel to be asked about.

### Return value

Number of slots the parameter of the channel offers.
## int getChannelSlotNames ( const Ptr < AnimationChannel > & channel , Vector < String > & OUT_out_names ) const

Collects the names of the slots the parameter of the specified channel offers.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AnimationChannel](../../../api/library/animations/timeline/class.animationchannel_cpp.md)> &* **channel** - Channel to be asked about.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<[String](../../../api/library/common/class.string_cpp.md)> &* **OUT_out_names** - Output buffer for the slot names. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of slot names put to the buffer.
## int getChannelSlotIndex ( const Ptr < AnimationChannel > & channel , const char * name ) const

Looks a slot of the channel parameter up by name and returns the number it takes on the object the channel is currently bound to. It is the counterpart of [getChannelSlotNames()](#getChannelSlotNames_AnimationChannel_VECString_int) for a channel that addresses its slot by name, see [SlotAccess](../../../api/library/animations/timeline/class.animationchannel_cpp.md#SlotAccess).
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AnimationChannel](../../../api/library/animations/timeline/class.animationchannel_cpp.md)> &* **channel** - Channel to be asked about.
- *const char ** **name** - Name of the slot to be looked up.

### Return value

Number of the slot, or -1 if the parameter offers no slots or the object the channel is bound to has none under that name.
## bool isChannelParameterReadable ( const Ptr < AnimationChannel > & channel ) const

Returns a value indicating if the current value of the channel parameter can be read from the scene. It cannot when the object the channel is bound to is not there to be resolved, or when the channel addresses a slot that object does not have.
### Arguments

- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AnimationChannel](../../../api/library/animations/timeline/class.animationchannel_cpp.md)> &* **channel** - Channel to be checked.

### Return value

true if the current value of the channel parameter can be read; otherwise, false.
## int getChannelSupportedProperties ( AnimationChannel::TYPE channel_type , Vector <int> & OUT_out_kinds ) const

Collects the playback properties a channel of the specified type offers, such as the pitch and the fades of a sound.
### Arguments

- *[AnimationChannel::TYPE](../../../api/library/animations/timeline/class.animationchannel_cpp.md#TYPE)* **channel_type** - Type of the channel.
- *[Vector](../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **OUT_out_kinds** - Output buffer for the playback property kinds. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of kinds put to the buffer.
## const char * getChannelPropertyName ( AnimationChannel::PROPERTY kind ) const

Returns the name of the specified playback property.
### Arguments

- *[AnimationChannel::PROPERTY](../../../api/library/animations/timeline/class.animationchannel_cpp.md#PROPERTY)* **kind** - Kind of the playback property.

### Return value

Name of the playback property.
## float getChannelPropertyDefaultValue ( AnimationChannel::PROPERTY kind ) const

Returns the value the specified playback property holds until it is animated.
### Arguments

- *[AnimationChannel::PROPERTY](../../../api/library/animations/timeline/class.animationchannel_cpp.md#PROPERTY)* **kind** - Kind of the playback property.

### Return value

Default value of the playback property.
## float getChannelPropertyMinValue ( AnimationChannel::PROPERTY kind ) const

Returns the lower bound of the specified playback property.
### Arguments

- *[AnimationChannel::PROPERTY](../../../api/library/animations/timeline/class.animationchannel_cpp.md#PROPERTY)* **kind** - Kind of the playback property.

### Return value

Lower bound of the playback property.
## float getChannelPropertyMaxValue ( AnimationChannel::PROPERTY kind ) const

Returns the upper bound of the specified playback property.
### Arguments

- *[AnimationChannel::PROPERTY](../../../api/library/animations/timeline/class.animationchannel_cpp.md#PROPERTY)* **kind** - Kind of the playback property.

### Return value

Upper bound of the playback property.
## bool animToBonesChannel ( const char * anim_path , const Ptr < AnimationChannelBones > & out_channel , float duration ) const

Bakes a skeletal animation file into a bones channel, so that its pose can be edited key by key in the Sequencer.
### Arguments

- *const char ** **anim_path** - Path to the animation file.
- *const [Ptr](../../../api/library/common/class.ptr_cpp.md)<[AnimationChannelBones](../../../api/library/animations/timeline/class.animationchannelbones_cpp.md)> &* **out_channel** - Channel to receive the baked keys.
- *float* **duration** - Length the animation is baked over, in seconds.

### Return value

true if the animation was baked; otherwise, false.
## String convertLegacyTrackToSequence ( const char * track_path , const char * seq_path = "" , bool overwrite = false ) const

Converts a track authored in the legacy Tracker into a sequence. A track that plays other tracks inside itself is converted whole: every nested track becomes a sequence file of its own and the parent receives a sub-sequence channel whose clips point at them, so overwriting rebuilds the entire tree rather than the file that was named. Everything the conversion could not carry over is reported to the console, one line per parameter. The whole picture is in the [Converting Legacy Tracks](../../../editor2/tools/sequencer/track_import/index.md) article.
### Arguments

- *const char ** **track_path** - Path to the legacy `*.track` file to be converted.
- *const char ** **seq_path** - Path the `*.seq` file is to be written to. Left empty, the sequence is written beside the track under the same name. The default value is an empty string.
- *bool* **overwrite** - true to convert the track again and replace a `*.seq` that is already there, false to keep the existing file and write nothing. The default value is false.

### Return value

Path of the sequence file, or an empty string if nothing was written.
## void rebuildAnimScripts ( )

Rebuilds the animation scripts of the project.
## void waitAnimScriptsRebuilding ( )

Blocks until the rebuild of the animation scripts is over.
## const char * getAnimScriptTypeName ( int type_index ) const

Returns the name of an animation script type by its number.
### Arguments

- *int* **type_index** - Number of the animation script type.

### Return value

Name of the animation script type.
