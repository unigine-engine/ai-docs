# Unigine::AnimationSequence Class (CPP)

**Header:** #include <UnigineAnimation.h>


An animation sequence holds one animation authored in the [Sequencer](../../../../editor2/tools/sequencer/index.md): the [channels](../../../../editor2/tools/sequencer/channels/index.md) that drive parameters over time, the groups these channels are arranged in, and the settings the animation was saved with. It is the runtime face of a `*.seq` asset and it is content only: playing it back is the job of the [AnimationSequencePlayer](../../../../api/library/animations/timeline/class.animationsequenceplayer_cpp.md) class or of the [NodeSequencePlayer](../../../../api/library/nodes/class.nodesequenceplayer_cpp.md) node.


A sequence keeps its channels by value, so *[getChannels()](../../../...md#getChannels_VECAnimationChannel_int)* and *[findChannelByName()](../../../...md#findChannelByName_cstr_AnimationChannel)* hand out copies. Editing a channel is therefore a round trip: take the copy, change it, and put it back with *[updateChannel()](../../../...md#updateChannel_AnimationChannel_int)*, which finds the stored channel by its ID.


Channel groups are folders. They set the order the channels are shown in and switch whole branches off, and a group that is disabled mutes every channel and every group below it.


For playing a sequence from code, and for retargeting one per instance, see the [Runtime Playback](../../../../editor2/tools/sequencer/runtime/index_cpp.md) article.


## AnimationSequence Class

### Enums

## EDITOR_SCENE_APPLY_MODE

Scene apply mode. It decides whether editing the sequence in the Sequencer writes the animated values into the scene. Runtime playback ignores this setting.
| Name | Description |
|---|---|
| **EDITOR_SCENE_APPLY_MODE_ON_CHANGE** = 0 | Every animated object takes the value its curve holds under the playhead, applied each time the frame changes. Between those changes the objects are left alone and can be moved by hand. |
| **EDITOR_SCENE_APPLY_MODE_ALWAYS_APPLY** = 1 | The Sequencer writes into the scene every frame and fully owns the animated parameters, so any change made from outside is overwritten on the next frame. |
| **EDITOR_SCENE_APPLY_MODE_NO_APPLY** = 2 | The Sequencer never writes to the scene, so curves can be inspected and edited without disturbing it. |

## ORIGINALS_RESTORE_MODE

Originals restore mode. It decides what becomes of the animated parameters once the sequence stops driving them.
| Name | Description |
|---|---|
| **ORIGINALS_RESTORE_MODE_NEVER** = 0 | The animated parameters keep whatever values the sequence applied last. Use it when the animation is meant to change the world for good. |
| **ORIGINALS_RESTORE_MODE_ON_STOP** = 1 | The original values are captured before the first change and put back when playback stops, so the scene returns to the state it was in before the sequence ran. |
| **ORIGINALS_RESTORE_MODE_EACH_FRAME** = 2 | The animation plays as an overlay: the original values are restored at the start of every frame and the sequence is applied on top, so the game logic underneath still reads the original values. |

### Members

## UGUID getGUID () const

Returns the current GUID of the sequence. It identifies the sequence itself, while the file this sequence is stored in is identified by *[getFileGUID()](../../../...md#getFileGUID_UGUID)*.
### Return value

Current GUID of the sequence
## UGUID getFileGUID () const

Returns the current GUID of the file the sequence is stored in. A sequence built in memory and never given a path has no file of its own, so this GUID stays empty.
### Return value

Current GUID of the file the sequence is stored in
## void setName ( const char * name )

Sets a new name of the sequence.
### Arguments

- *const char ** **name** - The name of the sequence

## const char * getName () const

Returns the current name of the sequence.
### Return value

Current name of the sequence
## int getNumChannels () const

Returns the current total number of channels in the sequence. Channels that belong to a nested sequence are counted by that sequence, not by this one.
### Return value

Current number of channels in the sequence
## int getNumChannelGroups () const

Returns the current total number of channel groups in the sequence, at all nesting levels.
### Return value

Current number of channel groups in the sequence
## void setManualDuration ( float duration )

Sets a new manual duration of the sequence, in seconds. The sequence never lasts less than this value, so a shorter animation is padded with empty time at the end, while content that runs past it still plays in full.
### Arguments

- *float* **duration** - The manual duration of the sequence, in seconds

## float getManualDuration () const

Returns the current manual duration of the sequence, in seconds. The sequence never lasts less than this value, so a shorter animation is padded with empty time at the end, while content that runs past it still plays in full.
### Return value

Current manual duration of the sequence, in seconds
## float getDuration () const

Returns the current total duration of the sequence, in seconds. It spans the content of all channels and is never shorter than the manual duration.
### Return value

Current duration of the sequence, in seconds
## void setSpeed ( float speed )

Sets a new playback speed of the sequence. It is an authoring setting saved in the file and used by the Sequencer preview, while a player keeps a speed of its own.
### Arguments

- *float* **speed** - The playback speed of the sequence

## float getSpeed () const

Returns the current playback speed of the sequence. It is an authoring setting saved in the file and used by the Sequencer preview, while a player keeps a speed of its own.
### Return value

Current playback speed of the sequence
## void setLoop ( bool loop )

Sets a new value indicating if the sequence is set to loop. It is an authoring setting saved in the file, while a player keeps a loop flag of its own.
### Arguments

- *bool* **loop** - Set **true** to enable looping; **false** - to disable it.

## bool isLoop () const

Returns the current value indicating if the sequence is set to loop. It is an authoring setting saved in the file, while a player keeps a loop flag of its own.
### Return value

**true** if looping is enabled ; otherwise **false**.
## void setDefaultOriginalsRestoreMode ( AnimationSequence::ORIGINALS_RESTORE_MODE mode )

Sets a new default restore mode for the original values of the animated parameters. A player adopts this mode unless another one is set on the player itself.
### Arguments

- *[AnimationSequence::ORIGINALS_RESTORE_MODE](../../../../api/library/animations/timeline/class.animationsequence_cpp.md#ORIGINALS_RESTORE_MODE)* **mode** - The default restore mode for the original values

## AnimationSequence::ORIGINALS_RESTORE_MODE getDefaultOriginalsRestoreMode () const

Returns the current default restore mode for the original values of the animated parameters. A player adopts this mode unless another one is set on the player itself.
### Return value

Current default restore mode for the original values
## void setEditorSceneApplyMode ( AnimationSequence::EDITOR_SCENE_APPLY_MODE mode )

Sets a new scene apply mode used while the sequence is edited. It shapes the Sequencer preview only, as a sequence played at run time always drives its targets.
### Arguments

- *[AnimationSequence::EDITOR_SCENE_APPLY_MODE](../../../../api/library/animations/timeline/class.animationsequence_cpp.md#EDITOR_SCENE_APPLY_MODE)* **mode** - The scene apply mode used while the sequence is edited

## AnimationSequence::EDITOR_SCENE_APPLY_MODE getEditorSceneApplyMode () const

Returns the current scene apply mode used while the sequence is edited. It shapes the Sequencer preview only, as a sequence played at run time always drives its targets.
### Return value

Current scene apply mode used while the sequence is edited
## void setEditorFps ( float fps )

Sets a new frame rate the Sequencer timeline is measured in, in frames per second. It maps frames to real time, so changing it relabels the timeline without moving any key.
### Arguments

- *float* **fps** - The frame rate the Sequencer timeline is measured in, in frames per second

## float getEditorFps () const

Returns the current frame rate the Sequencer timeline is measured in, in frames per second. It maps frames to real time, so changing it relabels the timeline without moving any key.
### Return value

Current frame rate the Sequencer timeline is measured in, in frames per second
## void setEditorShowFrames ( bool frames )

Sets a new value indicating if the Sequencer timeline is measured in frames instead of seconds.
### Arguments

- *bool* **frames** - Set **true** to enable the frame time format; **false** - to disable it.

## bool isEditorShowFrames () const

Returns the current value indicating if the Sequencer timeline is measured in frames instead of seconds.
### Return value

**true** if the frame time format is enabled ; otherwise **false**.
## void setEditorSnapEnabled ( bool enabled )

Sets a new value indicating if snapping is enabled in the Sequencer.
### Arguments

- *bool* **enabled** - Set **true** to enable snapping in the Sequencer; **false** - to disable it.

## bool isEditorSnapEnabled () const

Returns the current value indicating if snapping is enabled in the Sequencer.
### Return value

**true** if snapping in the Sequencer is enabled ; otherwise **false**.
## void setEditorSnapToFrames ( bool frames )

Sets a new value indicating if the Sequencer snaps keys and clips to frame boundaries.
### Arguments

- *bool* **frames** - Set **true** to enable snapping to frame boundaries; **false** - to disable it.

## bool isEditorSnapToFrames () const

Returns the current value indicating if the Sequencer snaps keys and clips to frame boundaries.
### Return value

**true** if snapping to frame boundaries is enabled ; otherwise **false**.
## void setEditorSnapToOthers ( bool others )

Sets a new value indicating if the Sequencer snaps keys and clips to the ones that are already on the timeline.
### Arguments

- *bool* **others** - Set **true** to enable snapping to the keys and clips that are already on the timeline; **false** - to disable it.

## bool isEditorSnapToOthers () const

Returns the current value indicating if the Sequencer snaps keys and clips to the ones that are already on the timeline.
### Return value

**true** if snapping to the keys and clips that are already on the timeline is enabled ; otherwise **false**.
## void setEditorSnapToValueGrid ( bool grid )

Sets a new value indicating if the Sequencer snaps key values to the value grid.
### Arguments

- *bool* **grid** - Set **true** to enable snapping to the value grid; **false** - to disable it.

## bool isEditorSnapToValueGrid () const

Returns the current value indicating if the Sequencer snaps key values to the value grid.
### Return value

**true** if snapping to the value grid is enabled ; otherwise **false**.
## void setEditorValueGridStep ( float step )

Sets a new step of the value grid that key values are snapped to.
### Arguments

- *float* **step** - The step of the value grid used in the Sequencer

## float getEditorValueGridStep () const

Returns the current step of the value grid that key values are snapped to.
### Return value

Current step of the value grid used in the Sequencer
## void setEditorRangeStart ( float start )

Sets a new start of the playback range shown in the Sequencer, in seconds. A negative value stands for the beginning of the sequence, and the range is limited only when at least one of its two ends is set.
### Arguments

- *float* **start** - The start of the playback range shown in the Sequencer, in seconds

## float getEditorRangeStart () const

Returns the current start of the playback range shown in the Sequencer, in seconds. A negative value stands for the beginning of the sequence, and the range is limited only when at least one of its two ends is set.
### Return value

Current start of the playback range shown in the Sequencer, in seconds
## void setEditorRangeEnd ( float end )

Sets a new end of the playback range shown in the Sequencer, in seconds. A negative value stands for the end of the sequence, and the range is limited only when at least one of its two ends is set.
### Arguments

- *float* **end** - The end of the playback range shown in the Sequencer, in seconds

## float getEditorRangeEnd () const

Returns the current end of the playback range shown in the Sequencer, in seconds. A negative value stands for the end of the sequence, and the range is limited only when at least one of its two ends is set.
### Return value

Current end of the playback range shown in the Sequencer, in seconds
## void setPath ( const char * path )

Sets a new path to the file the sequence is stored in. Setting the path registers the file in the virtual file system, which is what gives the sequence its file GUID. A sequence that has no path yet reads it back as a null value.
### Arguments

- *const char ** **path** - The path to the file the sequence is stored in

## const char * getPath () const

Returns the current path to the file the sequence is stored in. Setting the path registers the file in the virtual file system, which is what gives the sequence its file GUID. A sequence that has no path yet reads it back as a null value.
### Return value

Current path to the file the sequence is stored in
---

## AnimationSequence ( )

Constructor. Creates an empty sequence with default settings.
## void resolveAllChannels ( )

Resolves the animated parameter of every channel of the sequence anew, walking into the sequences embedded in it. Call it when the parameters the channels refer to may have changed.
## void assignFrom ( const Ptr < AnimationSequence > & other , bool fresh_placement_identity )

Copies the whole content and all settings of the specified sequence into this one. The GUID and the file GUID of this sequence are kept, so it keeps its own identity. Set **fresh_placement_identity** to true when the copy is to be used alongside the source, so that the two are told apart where the same sequence is nested in both.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationSequence](../../../../api/library/animations/timeline/class.animationsequence_cpp.md)> &* **other** - Source sequence to copy the content and the settings from.
- *bool* **fresh_placement_identity** - true to give the copied nested placements identities of their own, false to keep the ones of the source. The default value is false.

## void addChannel ( const Ptr < AnimationChannel > & channel )

Adds a copy of the specified channel to the sequence. The channel keeps its own ID when that ID is still free, and gets a new one otherwise.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationChannel](../../../../api/library/animations/timeline/class.animationchannel_cpp.md)> &* **channel** - Channel to be added.

## int getChannels ( Vector < Ptr < AnimationChannel >> & OUT_out_channels ) const

Collects all channels of the sequence and puts them to the **out_channels** buffer. The buffer receives copies, so changing one of them has no effect on the sequence until it is put back with *[updateChannel()](../../../...md#updateChannel_AnimationChannel_int)*.
### Arguments

- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationChannel](../../../../api/library/animations/timeline/class.animationchannel_cpp.md)>> &* **OUT_out_channels** - Output buffer for the channels of the sequence. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of channels put to the buffer.
## Ptr < AnimationChannel > findChannelByName ( const char * name ) const

Searches the sequence for a channel by the custom name given to it in the Sequencer. Custom names are not required to be unique: when several channels share one, the first of them is returned and a warning is written to the log.
### Arguments

- *const char ** **name** - Custom name of the channel to be found.

### Return value

Copy of the channel with the specified custom name, or NULL (null in C#) if there is no such channel.
## int findChannelGroupByName ( const char * name ) const

Searches the sequence for a channel group by its name. Group names are not required to be unique: when several groups share one, the first of them is returned and a warning is written to the log.
### Arguments

- *const char ** **name** - Name of the channel group to be found.

### Return value

ID of the channel group with the specified name, or 0 if there is no such group.
## int getChannelGroupChannels ( int group_id , Vector < Ptr < AnimationChannel >> & OUT_out_channels ) const

Collects the channels that belong to the specified channel group and puts their copies to the **out_channels** buffer. Only the channels of the group itself are collected, not those of the groups nested in it.
### Arguments

- *int* **group_id** - Channel group ID.
- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<[Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationChannel](../../../../api/library/animations/timeline/class.animationchannel_cpp.md)>> &* **OUT_out_channels** - Output buffer for the channels that belong to the group. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of channels put to the buffer.
## int getChannelGroupChildren ( int parent_id , Vector <int> & OUT_out_group_ids ) const

Collects the channel groups nested directly in the specified one and puts their IDs to the **out_group_ids** buffer. Groups deeper in the branch are reached by repeating the call for each child.
### Arguments

- *int* **parent_id** - ID of the parent channel group.
- *[Vector](../../../../api/library/containers/vector/class.vector_cpp.md)<int> &* **OUT_out_group_ids** - Output buffer for the IDs of the child groups. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

### Return value

Number of group IDs put to the buffer.
## bool updateChannel ( const Ptr < AnimationChannel > & channel )

Writes the content of the specified channel back into the sequence. The channel to be replaced is found by ID, which is how a copy taken from the sequence returns to it after being edited.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationChannel](../../../../api/library/animations/timeline/class.animationchannel_cpp.md)> &* **channel** - Channel carrying the new content.

### Return value

true if the sequence has a channel with the same ID and it was updated; otherwise, false.
## void removeChannel ( const Ptr < AnimationChannel > & channel )

Removes the channel with the same ID as the specified one from the sequence.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationChannel](../../../../api/library/animations/timeline/class.animationchannel_cpp.md)> &* **channel** - Channel to be removed.

## Ptr < AnimationChannel > copyChannelByID ( int channel_id ) const

Returns a copy of the channel with the specified ID.
### Arguments

- *int* **channel_id** - Channel ID.

### Return value

Copy of the channel with the specified ID, or NULL (null in C#) if there is no such channel.
## int addChannelGroup ( int parent_id )

Adds an empty channel group to the sequence. Group IDs start at 1 and are never reused, so 0 is what a search reports for a group that does not exist. A group added under a disabled parent is muted from the start.
### Arguments

- *int* **parent_id** - ID of the group the new one is to be nested in, or a negative value to put it at the top level.

### Return value

ID of the new channel group.
## void removeChannelGroup ( int group_id , bool keep_children )

Removes the specified channel group. Removing a group never removes channels: the ones it held move up to the parent of the removed group.
### Arguments

- *int* **group_id** - ID of the channel group to be removed.
- *bool* **keep_children** - true to keep the nested groups and move them up to the parent of the removed one, false to remove the whole branch.

## int getChannelGroupID ( int index ) const

Returns the ID of a channel group by its number in the list of groups of the sequence. The number has nothing to do with nesting or display order, it only enumerates the groups the sequence has.
### Arguments

- *int* **index** - Channel group number in the list of groups of the sequence.

### Return value

Channel group ID, or -1 if the number is out of range.
## bool containsChannelGroup ( int group_id ) const

Returns a value indicating if the sequence has a channel group with the specified ID.
### Arguments

- *int* **group_id** - Channel group ID.

### Return value

true if the sequence has a channel group with the specified ID; otherwise, false.
## int getChannelGroupParent ( int group_id ) const

Returns the group the specified channel group is nested in.
### Arguments

- *int* **group_id** - Channel group ID.

### Return value

ID of the parent group, or -1 if the group is at the top level.
## void setChannelGroupParent ( int group_id , int parent_id )

Moves the specified channel group into another one. Moving a group under a disabled parent mutes it along with everything it holds.
### Arguments

- *int* **group_id** - ID of the channel group to be moved.
- *int* **parent_id** - ID of the group to nest it in, or a negative value to move it to the top level.

## int getChannelGroupOrder ( int group_id ) const

Returns the display order of the specified channel group among the groups that share its parent.
### Arguments

- *int* **group_id** - Channel group ID.

### Return value

Display order of the channel group among the groups of the same parent.
## void setChannelGroupOrder ( int group_id , int order )

Sets the display order of the specified channel group among the groups that share its parent.
### Arguments

- *int* **group_id** - Channel group ID.
- *int* **order** - Display order of the group among the groups of the same parent.

## const char * getChannelGroupName ( int group_id ) const

Returns the name of the specified channel group.
### Arguments

- *int* **group_id** - Channel group ID.

### Return value

Name of the channel group.
## void setChannelGroupName ( int group_id , const char * name )

Sets the name of the specified channel group.
### Arguments

- *int* **group_id** - Channel group ID.
- *const char ** **name** - Name of the channel group.

## bool isChannelGroupEnabled ( int group_id ) const

Returns a value indicating if the specified channel group is enabled. The flag reports the state of this group alone, while a group nested in a disabled one is muted regardless of it.
### Arguments

- *int* **group_id** - Channel group ID.

### Return value

true if the specified channel group is enabled; otherwise, false.
## void setChannelGroupEnabled ( int group_id , bool enabled )

Enables or mutes the specified channel group. Muting a group mutes every channel it holds and every group nested in it, exactly as if each of them were muted by hand.
### Arguments

- *int* **group_id** - Channel group ID.
- *bool* **enabled** - true to enable the group, false to mute it.

## bool isChannelGroupCollapsed ( int group_id ) const

Returns a value indicating if the specified channel group is shown collapsed in the Sequencer.
### Arguments

- *int* **group_id** - Channel group ID.

### Return value

true if the specified channel group is collapsed in the Sequencer; otherwise, false.
## void setChannelGroupCollapsed ( int group_id , bool collapsed )

Collapses or expands the specified channel group in the Sequencer. It affects the way the group is shown and does not change what the sequence plays.
### Arguments

- *int* **group_id** - Channel group ID.
- *bool* **collapsed** - true to collapse the group in the Sequencer, false to expand it.

## void setChannelGroupID ( int channel_id , int group_id )

Puts the specified channel into a channel group. Moving a channel into a disabled group mutes it.
### Arguments

- *int* **channel_id** - Channel ID.
- *int* **group_id** - ID of the group to put the channel in, or a negative value to take it out of any group.

## void setChannelOrder ( int channel_id , int order )

Sets the display order of the specified channel. The order is also the priority of the channel: where two channels drive the same target, the one that sits higher in the list wins, and a lower number means a higher place.
### Arguments

- *int* **channel_id** - Channel ID.
- *int* **order** - Display order of the channel.

## void renumberDisplayOrder ( )

Renumbers the display order of all channels and groups into a dense sequence, walking the tree from top to bottom, and stores the channels in that order. Call it after moving rows around, so that the priority of the channels that share a target follows what is shown.
## void clear ( )

Clears the sequence, removing all its channels and groups and putting every setting back to its default value.
## bool containsClipFileGUID ( const UGUID & file_guid ) const

Returns a value indicating if the specified sequence file is used anywhere in this composition, at any depth of nesting. It is the check that keeps a sequence from being nested in itself.
### Arguments

- *const [UGUID](../../../../api/library/filesystem/class.uguid_cpp.md) &* **file_guid** - GUID of the sequence file to be looked for.

### Return value

true if the sequence file with the specified GUID is used by a clip of this sequence or of any sequence nested in it; otherwise, false.
## void adoptEmbeddedClipSequences ( )

Takes ownership of the sequences embedded in the clips of this one, so that they live and die with it. Sequences that a clip refers to by file are not affected, as they belong to their own assets.
## void adoptEmbeddedChild ( const Ptr < AnimationSequence > & child )

Takes ownership of the specified sequence, making this one responsible for deleting it. The caller gives up ownership by the same call, so the child must not be released on its own afterwards.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[AnimationSequence](../../../../api/library/animations/timeline/class.animationsequence_cpp.md)> &* **child** - Sequence to be taken over.

## bool save ( )

Saves the sequence to the file it points at. The call fails when the path is not set or does not name a `*.seq` file.
### Return value

true if the sequence was saved successfully; otherwise, false.
## bool load ( )

Loads the sequence from the file it points at, replacing everything it currently holds. The call fails when the path is not set, does not name a `*.seq` file, or cannot be read.
### Return value

true if the sequence was loaded successfully; otherwise, false.
## bool loadDataOnly ( )

Loads the sequence from its file and leaves the sequences its clips refer to unresolved. It reads a file for inspection, such as gathering what it depends on, and the result is not meant to be played.
### Return value

true if the data was loaded successfully; otherwise, false.
## void saveToBlob ( const Ptr < Blob > & blob )

Saves the sequence to the specified blob, which is how it is passed around without a file.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../../api/library/common/class.blob_cpp.md)> &* **blob** - Blob to save the sequence to.

## bool loadFromBlob ( const Ptr < Blob > & blob )

Loads the sequence from the specified blob, replacing everything it currently holds.
### Arguments

- *const [Ptr](../../../../api/library/common/class.ptr_cpp.md)<[Blob](../../../../api/library/common/class.blob_cpp.md)> &* **blob** - Blob to load the sequence from.

### Return value

true if the sequence was loaded successfully; otherwise, false.
