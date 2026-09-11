# API Migration (CS)


## Major Changes


What changed at the level of whole classes: what was added, what was given a new name, what was replaced and what is gone. Changes inside a class are listed in the per-class chapters further down the page, and the ones that need explaining have a chapter of their own in [Breaking Changes](../upgrade/migration_api_cs.md#breaking_changes).


### New Classes


- *[Geodetics::Anchor](../api/library/geodetics/geodetics_plugin/class.anchor_cs.md)*
- *[AnimationBindComponent](../api/library/animations/timeline/class.animationbindcomponent_cs.md)*
- *[AnimationChannelEvent](../api/library/animations/timeline/class.animationchannelevent_cs.md)*
- *[AnimationChannelEventState](../api/library/animations/timeline/class.animationchanneleventstate_cs.md)*
- *[AnimationChannelFollowPath](../api/library/animations/timeline/class.animationchannelfollowpath_cs.md)*
- *[AnimationChannelSkeletonAnimation](../api/library/animations/timeline/class.animationchannelskeletonanimation_cs.md)*
- *[AnimationChannelSound](../api/library/animations/timeline/class.animationchannelsound_cs.md)*
- *[AnimationChannelSubSequence](../api/library/animations/timeline/class.animationchannelsubsequence_cs.md)*
- *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)*
- *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)*
- *[SpiderVision::CAVEGroupData](../api/library/plugins/spidervision/class.cavegroupdata_cs.md)*
- *[Cesium](../api/library/plugins/cesium/class.cesium_cs.md)*
- *[CesiumConfig](../api/library/plugins/cesium/class.cesiumconfig_cs.md)*
- *[CustomParameterLayout](../api/library/common/class.customparameterlayout_cs.md)*
- *[ExperimentalBakeNavigation](../api/library/pathfinding/class.experimentalbakenavigation_cs.md)*
- *[ExperimentalNavigation](../api/library/pathfinding/class.experimentalnavigation_cs.md)*
- *[ExperimentalNavigationAvoidance](../api/library/pathfinding/class.experimentalnavigationavoidance_cs.md)*
- *[ExperimentalNavigationBakeQuery](../api/library/pathfinding/class.experimentalnavigationbakequery_cs.md)*
- *[ExperimentalNavigationBakeSettings](../api/library/pathfinding/class.experimentalnavigationbakesettings_cs.md)*
- *[ExperimentalNavigationMesh](../api/library/pathfinding/class.experimentalnavigationmesh_cs.md)*
- *[ExperimentalNavigationMeshAreaVolume](../api/library/pathfinding/class.experimentalnavigationmeshareavolume_cs.md)*
- *[ExperimentalNavigationMeshCorridor](../api/library/pathfinding/class.experimentalnavigationmeshcorridor_cs.md)*
- *[ExperimentalNavigationMeshFilter](../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md)*
- *[ExperimentalNavigationMeshInvoker](../api/library/pathfinding/class.experimentalnavigationmeshinvoker_cs.md)*
- *[ExperimentalNavigationPath](../api/library/pathfinding/class.experimentalnavigationpath_cs.md)*
- *[ExperimentalNavigationPathFetch](../api/library/pathfinding/class.experimentalnavigationpathfetch_cs.md)*
- *[IKInfo](../api/library/animations/skeletal/class.ikinfo_cs.md)*
- *[IKInfoChain](../api/library/animations/skeletal/class.ikinfochain_cs.md)*
- *[IKInfoTwoBone](../api/library/animations/skeletal/class.ikinfotwobone_cs.md)*
- *[InputEventPadAccelerometerMotion](../api/library/controls/class.inputeventpadaccelerometermotion_cs.md)*
- *[InputEventPadGyroscopeMotion](../api/library/controls/class.inputeventpadgyroscopemotion_cs.md)*
- *[InputEventTextEditing](../api/library/controls/class.inputeventtextediting_cs.md)*
- *[JointLimitInfo](../api/library/animations/skeletal/class.jointlimitinfo_cs.md)*
- *[JointLimitInfoCone](../api/library/animations/skeletal/class.jointlimitinfocone_cs.md)*
- *[JointLimitInfoConeAsym](../api/library/animations/skeletal/class.jointlimitinfoconeasym_cs.md)*
- *[JointLimitInfoConeAsymTwist](../api/library/animations/skeletal/class.jointlimitinfoconeasymtwist_cs.md)*
- *[JointLimitInfoConeTwist](../api/library/animations/skeletal/class.jointlimitinfoconetwist_cs.md)*
- *[JointLimitInfoHinge](../api/library/animations/skeletal/class.jointlimitinfohinge_cs.md)*
- *[JointLimitInfoHingeTwist](../api/library/animations/skeletal/class.jointlimitinfohingetwist_cs.md)*
- *[JointLimitInfoTwist](../api/library/animations/skeletal/class.jointlimitinfotwist_cs.md)*
- *[JointLimitSetInfo](../api/library/animations/skeletal/class.jointlimitsetinfo_cs.md)*
- *[LookAtChainInfo](../api/library/animations/skeletal/class.lookatchaininfo_cs.md)*
- *[LookAtInfo](../api/library/animations/skeletal/class.lookatinfo_cs.md)*
- *[Weather::Planet](../api/library/plugins/weather/class.planet_cs.md)*
- *[RTSPStreamer](../api/library/plugins/rtspstreamer/class.rtspstreamer_cs.md)*
- *[ScenarioManager::ScenarioManager](../api/library/plugins/scenariomanager/class.scenariomanager_cs.md)*
- *AssetDependencyReplacement* (Editor API)
- *AssetDependencyReplacer* (Editor API)
- *FileDependencies* (Editor API)
- *FileDependencyWalker* (Editor API)
- *NodeFileDependencies* (Editor API)


### Renamed Classes


- The *NodeAnimationPlayback* node class has been renamed as *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cs.md)*.
- The *AnimationModifier* class and its 23 typed subclasses have been renamed as *[AnimationChannel](../api/library/animations/timeline/class.animationchannel_cs.md)* and its subclasses. The rename is mechanical - the *Modifier* part of the name became *Channel*, and nothing else about these classes changed except that **Copy()** is now **AssignFrom()**. <details> <summary>Complete list of renamed classes | close</summary> | UNIGINE 2.21 | UNIGINE 2.22 | |---|---| | *AnimationModifier* | *[AnimationChannel](../api/library/animations/timeline/class.animationchannel_cs.md)* | | *AnimationModifierBones* | *[AnimationChannelBones](../api/library/animations/timeline/class.animationchannelbones_cs.md)* | | *AnimationModifierBool* | *[AnimationChannelBool](../api/library/animations/timeline/class.animationchannelbool_cs.md)* | | *AnimationModifierDVec2* | *[AnimationChannelDVec2](../api/library/animations/timeline/class.animationchanneldvec2_cs.md)* | | *AnimationModifierDVec3* | *[AnimationChannelDVec3](../api/library/animations/timeline/class.animationchanneldvec3_cs.md)* | | *AnimationModifierDVec4* | *[AnimationChannelDVec4](../api/library/animations/timeline/class.animationchanneldvec4_cs.md)* | | *AnimationModifierDouble* | *[AnimationChannelDouble](../api/library/animations/timeline/class.animationchanneldouble_cs.md)* | | *AnimationModifierFVec2* | *[AnimationChannelFVec2](../api/library/animations/timeline/class.animationchannelfvec2_cs.md)* | | *AnimationModifierFVec3* | *[AnimationChannelFVec3](../api/library/animations/timeline/class.animationchannelfvec3_cs.md)* | | *AnimationModifierFVec4* | *[AnimationChannelFVec4](../api/library/animations/timeline/class.animationchannelfvec4_cs.md)* | | *AnimationModifierFloat* | *[AnimationChannelFloat](../api/library/animations/timeline/class.animationchannelfloat_cs.md)* | | *AnimationModifierIVec2* | *[AnimationChannelIVec2](../api/library/animations/timeline/class.animationchannelivec2_cs.md)* | | *AnimationModifierIVec3* | *[AnimationChannelIVec3](../api/library/animations/timeline/class.animationchannelivec3_cs.md)* | | *AnimationModifierIVec4* | *[AnimationChannelIVec4](../api/library/animations/timeline/class.animationchannelivec4_cs.md)* | | *AnimationModifierInfo* | *[AnimationChannelInfo](../api/library/animations/timeline/class.animationchannelinfo_cs.md)* | | *AnimationModifierInt* | *[AnimationChannelInt](../api/library/animations/timeline/class.animationchannelint_cs.md)* | | *AnimationModifierNode* | *[AnimationChannelNode](../api/library/animations/timeline/class.animationchannelnode_cs.md)* | | *AnimationModifierQuat* | *[AnimationChannelQuat](../api/library/animations/timeline/class.animationchannelquat_cs.md)* | | *AnimationModifierScalar* | *[AnimationChannelScalar](../api/library/animations/timeline/class.animationchannelscalar_cs.md)* | | *AnimationModifierString* | *[AnimationChannelString](../api/library/animations/timeline/class.animationchannelstring_cs.md)* | | *AnimationModifierUGUID* | *[AnimationChannelUGUID](../api/library/animations/timeline/class.animationchanneluguid_cs.md)* | | *AnimationModifierVec2* | *[AnimationChannelVec2](../api/library/animations/timeline/class.animationchannelvec2_cs.md)* | | *AnimationModifierVec3* | *[AnimationChannelVec3](../api/library/animations/timeline/class.animationchannelvec3_cs.md)* | | *AnimationModifierVec4* | *[AnimationChannelVec4](../api/library/animations/timeline/class.animationchannelvec4_cs.md)* | </details>


### Replaced Classes


These classes are gone and their work is done by a different class with a different API - see [Sequencer Replaces the Tracker](../upgrade/migration_api_cs.md#sequencer_migration) for what the migration involves.


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| *AnimationTrack* | *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)* |
| *AnimationPlayback* | *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)* |
| *AnimationModifierTrack* | *[AnimationChannelSubSequence](../api/library/animations/timeline/class.animationchannelsubsequence_cs.md)* |
| *AnimationObject* | *[AnimationBind](../api/library/animations/timeline/class.animationbind_cs.md)* |
| *AnimationObjectNode* | *[AnimationBindNode](../api/library/animations/timeline/class.animationbindnode_cs.md)* |
| *AnimationObjectMaterial* | *[AnimationBindMaterial](../api/library/animations/timeline/class.animationbindmaterial_cs.md)* |
| *AnimationObjectPropertyParameter* | *[AnimationBindPropertyParameter](../api/library/animations/timeline/class.animationbindpropertyparameter_cs.md)* |
| *AnimationObjectRuntime* | *[AnimationBindRuntime](../api/library/animations/timeline/class.animationbindruntime_cs.md)* |
| *AnimationObjectTrack* | *[AnimationChannelSubSequence](../api/library/animations/timeline/class.animationchannelsubsequence_cs.md)* |


### Removed Classes


Removed with no replacement.


- *AnimationFrame*
- *AnimationMask*
- *AnimationModifierMat4*


## Breaking Changes


### Sequencer Replaces the Tracker


Animation over time used to be authored in the *Tracker*. In 2.22 that job belongs to the *[Sequencer](../editor2/tools/sequencer/index.md)* - a more modern and more convenient tool - and the animation API has been reshaped to match it. Skeletal animation, the animation graph and *[AnimScript](../api/library/animations/skeletal/class.animscript_cs.md)* are a separate subject and are not affected by this chapter, apart from the changes listed in [AnimScript Class](../upgrade/migration_api_cs.md#animscript_class).


> **Notice:** The *Tracker* itself is still there, and `*.track` files still play - see [Running Tracks in Application](../editor2/tools/tracker/run/index.md). This chapter is about the animation classes, which have been reshaped around the *[Sequencer](../editor2/tools/sequencer/index.md)*.


The model is now the following:


- An *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)* is one animation, stored in a `*.seq` file. It is content only and holds no scene objects.
- An *[AnimationChannel](../api/library/animations/timeline/class.animationchannel_cs.md)* is one animated parameter inside the sequence - one row of the timeline. Its typed subclasses carry the keys.
- An *[AnimationBind](../api/library/animations/timeline/class.animationbind_cs.md)* says which objects a channel drives. The bind classes existed in 2.21 as well, but now they are the only way a channel reaches the scene.
- Playback is a player: either the *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)* class, or the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cs.md)* node that keeps one and ticks it. In 2.21 a playback was also saved to a `*.uplay` file of its own; in 2.22 a player is created in code or set up on the node, and has no file.


#### Classes


The classes that made up a track are replaced as follows.


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| *AnimationTrack* | *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)* |
| *AnimationPlayback* | *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)* |
| *NodeAnimationPlayback* | *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cs.md)* |
| *AnimationModifier* and its typed subclasses | *[AnimationChannel](../api/library/animations/timeline/class.animationchannel_cs.md)* and its typed subclasses. The rename is mechanical - *AnimationModifierFloat* becomes *[AnimationChannelFloat](../api/library/animations/timeline/class.animationchannelfloat_cs.md)*, and so on for every type. The complete list is in [Major Changes](../upgrade/migration_api_cs.md#major_changes). |
| *AnimationModifierTrack* | *[AnimationChannelSubSequence](../api/library/animations/timeline/class.animationchannelsubsequence_cs.md)* |
| *AnimationObject*, *AnimationObjectNode*, *AnimationObjectMaterial*, *AnimationObjectPropertyParameter*, *AnimationObjectRuntime* | The corresponding *[AnimationBind](../api/library/animations/timeline/class.animationbind_cs.md)* classes. In 2.21 the two hierarchies existed side by side; the *AnimationObject* one has been removed. |
| *AnimationModifierMat4*, *AnimationFrame*, *AnimationMask* | Removed with no direct replacement. |


#### Renamed Methods


Two methods of the *[Animations](../api/library/animations/class.animations_cs.md)* class were renamed along with the classes they mention, and the copying method of every curve and every channel was renamed as well.


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| **Animations.GetParameterModifierType()** | *[*Animations.GetParameterChannelType()*](../api/library/animations/class.animations_cs.md#getParameterChannelType_int_int)* |
| **Animations.AnimToBonesModifier()** | *[*Animations.AnimToBonesChannel()*](../api/library/animations/class.animations_cs.md#animToBonesChannel_cstr_AnimationChannelBones_float_int)* |
| **Copy()** of every *AnimationCurve* and *AnimationModifier* class | **AssignFrom()** of the corresponding *[AnimationCurve](../api/library/animations/timeline/class.animationcurve_cs.md)* and *[AnimationChannel](../api/library/animations/timeline/class.animationchannel_cs.md)* class |


#### Uniform Time Became Constant Speed


The uniform time switch that the floating-point modifier classes carried in 2.21 is gone. The behaviour itself stayed and moved to the *[AnimationChannel](../api/library/animations/timeline/class.animationchannel_cs.md)* base class under a name that says what it does: the curve is measured along its own length and the playhead is remapped through that measurement, so the value travels at a constant speed while the total duration holds.


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| **UpdateUniformTime()** of the floating-point modifiers | *[*AnimationChannel.SetConstantSpeed()*](../api/library/animations/timeline/class.animationchannel_cs.md#setConstantSpeed_int_int_void)* |
| **IsUniformTime()** of the floating-point modifiers | *[*AnimationChannel.IsConstantSpeed*](../api/library/animations/timeline/class.animationchannel_cs.md#IsConstantSpeed)* |


Two questions the old pair could not answer come with it: *[*IsConstantSpeedSupported*](../api/library/animations/timeline/class.animationchannel_cs.md#IsConstantSpeedSupported)* tells whether the channel carries the setting at all, and *[*GetConstantSpeedTime()*](../api/library/animations/timeline/class.animationchannel_cs.md#getConstantSpeedTime_float_float)* returns the moment the curve is sampled at for a given moment on the timeline.


> **Notice:** The setting is offered where the value has a length to measure: a floating-point number, a vector of floats or doubles and a followed path. A rotation carries it in the angles modes only, since the segments of a quaternion rotation are spherical blends already, and an integer channel does not carry it at all. Code that switched uniform time on unconditionally should ask **IsConstantSpeedSupported** first.


#### Key Type and Tangent Setters Take a Value/Time Ratio


The setters that shape a key gained a trailing argument on every curve class: the number of units of value that make up one unit of time. It is taken into account when the two handles of an [aligned](../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE_ALIGNED) key are made collinear - the handles are brought into a common space through this ratio, aligned there and converted back, so a curve drawn with value and time on different scales still shows the pair as one straight line.


The argument has a default of 1.0f, which measures value and time on the same scale and reproduces the 2.21 behaviour, so existing calls keep compiling and keep their result. Pass the ratio the curve is actually drawn with when an aligned key has to look aligned to the eye.


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| **SetKeyType( int, KEY_TYPE )** | **SetKeyType( int, KEY_TYPE, float )** |
| **SetKeyLeftTangent( int, vec2 )** | **SetKeyLeftTangent( int, vec2, float )** |
| **SetKeyRightTangent( int, vec2 )** | **SetKeyRightTangent( int, vec2, float )** |
| **SetTypeOfAllKeys( KEY_TYPE )** | **SetTypeOfAllKeys( KEY_TYPE, float )** |


The same argument was added to the per-component setters of *[AnimationChannel](../api/library/animations/timeline/class.animationchannel_cs.md)*: *[*SetComponentKeyType()*](../api/library/animations/timeline/class.animationchannel_cs.md#setComponentKeyType_int_int_int_float_void)*, *[*SetComponentKeyLeftTangent()*](../api/library/animations/timeline/class.animationchannel_cs.md#setComponentKeyLeftTangent_int_int_vec2_float_void)* and *[*SetComponentKeyRightTangent()*](../api/library/animations/timeline/class.animationchannel_cs.md#setComponentKeyRightTangent_int_int_vec2_float_void)*.


#### Converting Existing Tracks


A `*.track` file does not have to be rebuilt by hand. *[*Animations.ConvertLegacyTrackToSequence()*](../api/library/animations/class.animations_cs.md#convertLegacyTrackToSequence_cstr_cstr_int_String)* converts one into a `*.seq` and returns the path it wrote; the *[Sequencer](../editor2/tools/sequencer/index.md)* offers the same conversion in the menu next to *Save*. A track that plays other tracks inside itself is converted whole, every nested track becoming a sequence of its own.


Most parameters become the channel one would expect. The one worth knowing about is a position track with **follow X / Y / Z**: it becomes an *[AnimationChannelFollowPath](../api/library/animations/timeline/class.animationchannelfollowpath_cs.md)*, a channel new in 2.22 that carries the trajectory and the aim together and writes both the position and the rotation of its node. A track's **const velocity** arrives as the constant speed setting described above, and its **unit_time** as the speed of the sequence.


Everything the conversion could not carry over is reported to the console, one line per parameter. What to expect there is described in the [Converting Legacy Tracks](../editor2/tools/sequencer/track_import/index.md) article.


#### Bindings Address Many Targets


In 2.21 a binding pointed at one object, named by a description: a node ID and a name, a material GUID, a surface index. In 2.22 a binding is a query that resolves to any number of targets, so the setters take collections and patterns, and the getters ask for a resolved target by its number.


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| **AnimationObjectNode.SetNode()** | *[*AnimationBindNode.SetNodes()*](../api/library/animations/timeline/class.animationbindnode_cs.md#setNodes_VECNode_void)* |
| **AnimationObjectNode.GetNode()** | *[*AnimationBindNode.GetTargetResolvedNode()*](../api/library/animations/timeline/class.animationbindnode_cs.md#getTargetResolvedNode_int_Node)* |
| **SetObjectDescription()**, **SetNodeDescription()** | **SetObjects()**, **SetNodes()** |
| **SetMaterialDescription()**, **SetPropertyDescription()** | **SetAssets()** |
| **SetSurfaceDescription()** | **SetSurfacePattern()** |


How the query is built - what it matches by and how far it searches - is described in the *[AnimationBind](../api/library/animations/timeline/class.animationbind_cs.md)* class reference.


#### No Registry of Loaded Animations


The *[Animations](../api/library/animations/class.animations_cs.md)* class no longer keeps lists of loaded tracks, playbacks and animation objects. Everything that walked those lists has been removed: **LoadTrack()**, **GetTrackByPath()**, **GetNumTracks()**, the playback counterparts, the *AnimationObject* accessors, the four events reporting additions and removals, and the *Animations::RESULT* enumeration returned by the loading and saving methods. The full list is in [Animations Class](../upgrade/migration_api_cs.md#animations_class).


A sequence is loaded and saved through the sequence itself, and playing it is the player's job.


| UNIGINE 2.21 | ```cpp // load the track through the registry and find it by path Animations::loadTrack("animations/door.utrack"); AnimationTrackPtr track = Animations::getTrackByPath("animations/door.utrack"); AnimationPlaybackPtr playback = AnimationPlayback::create(); playback->setTrack(track); playback->setLoop(false); playback->setSpeed(1.0f); playback->play(); ``` ```csharp // load the track through the registry and find it by path Animations.LoadTrack("animations/door.utrack"); AnimationTrack track = Animations.GetTrackByPath("animations/door.utrack"); AnimationPlayback playback = new AnimationPlayback(); playback.SetTrack(track); playback.Loop = false; playback.Speed = 1.0f; playback.Play(); ``` |
|---|---|
| UNIGINE 2.22 | ```cpp // the player takes the sequence file directly AnimationSequencePlayerPtr player = AnimationSequencePlayer::create("animations/door.seq"); player->setLoop(false); player->setSpeed(1.0f); player->setAutoTick(true);   // let the Engine advance it every frame player->play(); ``` ```csharp // the player takes the sequence file directly AnimationSequencePlayer player = new AnimationSequencePlayer("animations/door.seq"); player.Loop = false; player.Speed = 1.0f; player.AutoTick = true;   // let the Engine advance it every frame player.Play(); ``` |


To build or edit a sequence in memory rather than load one, create an *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)*, add channels to it with *[*AddChannel()*](../api/library/animations/timeline/class.animationsequence_cs.md#addChannel_AnimationChannel_void)* and hand it to a player. A channel taken out of a sequence is a copy, so an edited channel has to be put back with *[*UpdateChannel()*](../api/library/animations/timeline/class.animationsequence_cs.md#updateChannel_AnimationChannel_int)*.


More on playing sequences from code is in the [Runtime Playback](../editor2/tools/sequencer/runtime/index_cs.md) article.


### Material Overlap Became Transparent Order


The boolean *overlap* option of a material has been replaced with *transparent_order* - a choice of three points in the frame where the transparent part of the material is drawn. Instead of asking whether to draw on top of everything, a material now says when it is drawn.


| UNIGINE 2.22 | Value | When the transparency is drawn |
|---|---|---|
| ***Before SSR*** | 0 | The default. Takes part in screen-space reflections and in every post effect. |
| ***Before Post*** | 1 | Invisible to screen-space reflections, still receives tonemapping and TAA. There was no equivalent in 2.21. |
| ***After Post*** | 2 | Drawn after tonemapping and TAA. This is what *overlap* used to do. |


Materials in your project are converted when you upgrade it: *overlap = true* becomes *After Post*, *overlap = false* becomes *Before SSR*, and the same conversion is applied to *material.overlap* keys of animation channels. Code is not converted - the calls have to be rewritten.


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| **Overlap = true** | *[*TransparentOrder = Material.TRANSPARENT_ORDER.AFTER_POST*](../api/library/rendering/class.material_cs.md#setTransparentOrder_int_void)* |
| **Overlap = false** | *[*TransparentOrder = Material.TRANSPARENT_ORDER.BEFORE_SSR*](../api/library/rendering/class.material_cs.md#setTransparentOrder_int_void)* |
| **Overlap** | *[*TransparentOrder*](../api/library/rendering/class.material_cs.md#getTransparentOrder_int)* |
| ***OPTION_OVERLAP*** | *[**OPTION_TRANSPARENT_ORDER**](../api/library/rendering/class.material_cs.md#OPTION_TRANSPARENT_ORDER)* |


> **Notice:** The new option took the second place in the material option list, so the values of every *OPTION_** constant after *OPTION_TRANSPARENT* shifted by one. Code that stores an option by its number rather than by its name has to be checked.


In shaders the *GET_OPTION_OVERLAP* define became *GET_OPTION_TRANSPARENT_ORDER* and now carries 0, 1 or 2.


### Property File Setters Report Failure


A file GUID identifies a property uniquely, and the setters now refuse a GUID that another property already holds instead of accepting it silently.


In C# the ***FilePath*** and ***FileGUID*** properties are read-only now, and assigning to them no longer compiles. Use the new methods and check what they return.


| UNIGINE 2.21 | ```csharp property.FilePath = "properties/door.prop"; ``` |
|---|---|
| UNIGINE 2.22 | ```csharp if (!property.SetFilePath("properties/door.prop")) { // another property already holds this file } ``` |


### State Machines Addressed by Index


An *[AnimScript](../api/library/animations/skeletal/class.animscript_cs.md)* state machine used to be named by a string in every call. In 2.22 it is addressed by an index, which turns one lookup per call into one lookup per state machine, and the API around state machines grew from five methods to thirty.


Take the index once with *[*FindStateMachineByName()*](../api/library/animations/skeletal/class.animscript_cs.md#findStateMachineByName_cstr_int)* - or with *[*FindStateMachine()*](../api/library/animations/skeletal/class.animscript_cs.md#findStateMachine_cstr_int)* if you address a nested machine by its path - and pass it everywhere afterwards.


| UNIGINE 2.21 | ```cpp if (anim_script->isStateMachineInTransition("locomotion")) float p = anim_script->getStateMachineTransitionProgress("locomotion"); ``` ```csharp if (animScript.IsStateMachineInTransition("locomotion")) float p = animScript.GetStateMachineTransitionProgress("locomotion"); ``` |
|---|---|
| UNIGINE 2.22 | ```cpp int sm = anim_script->findStateMachineByName("locomotion"); if (anim_script->isStateMachineInTransition(sm)) float p = anim_script->getStateMachineTransitionProgress(sm); ``` ```csharp int sm = animScript.FindStateMachineByName("locomotion"); if (animScript.IsStateMachineInTransition(sm)) float p = animScript.GetStateMachineTransitionProgress(sm); ``` |


Four of the five methods have an index-taking counterpart of the same name. The fifth, **IsStateMachineActive()**, is gone: use *[*IsStateMachineRelevant()*](../api/library/animations/skeletal/class.animscript_cs.md#isStateMachineRelevant_int_bool)* to tell whether a state machine takes part in the current pose. Everything the class gained is listed in [AnimScript Class](../upgrade/migration_api_cs.md#animscript_class).


### Experimental Navigation


2.22 adds a second navigation system, available as **experimental** functionality. It runs beside the existing one and offers capabilities the older system does not have. Nothing in the older API has changed: *[Navigation](../api/library/pathfinding/class.navigation_cs.md)*, *[NavigationMesh](../api/library/pathfinding/class.navigationmesh_cs.md)*, *[NavigationSector](../api/library/pathfinding/class.navigationsector_cs.md)*, the obstacles and *PathFinding* keep every method they had in 2.21, so a project that uses them needs no migration at all.


What has been added:


- The *[ExperimentalNavigation](../api/library/pathfinding/class.experimentalnavigation_cs.md)* class - the entry point of the system - together with *[ExperimentalNavigationMesh](../api/library/pathfinding/class.experimentalnavigationmesh_cs.md)*, *[ExperimentalNavigationMeshAreaVolume](../api/library/pathfinding/class.experimentalnavigationmeshareavolume_cs.md)* and *[ExperimentalNavigationMeshInvoker](../api/library/pathfinding/class.experimentalnavigationmeshinvoker_cs.md)* nodes.
- Path querying and following: *[ExperimentalNavigationPath](../api/library/pathfinding/class.experimentalnavigationpath_cs.md)*, *[ExperimentalNavigationPathFetch](../api/library/pathfinding/class.experimentalnavigationpathfetch_cs.md)*, *[ExperimentalNavigationMeshCorridor](../api/library/pathfinding/class.experimentalnavigationmeshcorridor_cs.md)*, *[ExperimentalNavigationMeshFilter](../api/library/pathfinding/class.experimentalnavigationmeshfilter_cs.md)* and *[ExperimentalNavigationAvoidance](../api/library/pathfinding/class.experimentalnavigationavoidance_cs.md)*.
- Baking: *[ExperimentalBakeNavigation](../api/library/pathfinding/class.experimentalbakenavigation_cs.md)*, *[ExperimentalNavigationBakeQuery](../api/library/pathfinding/class.experimentalnavigationbakequery_cs.md)* and *[ExperimentalNavigationBakeSettings](../api/library/pathfinding/class.experimentalnavigationbakesettings_cs.md)*.


The classes that already existed gained a few entry points into the new system, all of them additions:


- *[*Node.IsExperimentalNavigation()*](../api/library/nodes/class.node_cs.md#isExperimentalNavigation_int)*, together with the new node types in *[Node::TYPE](../api/library/nodes/class.node_cs.md#EXPERIMENTAL_NAVIGATION_MESH)*.
- Per-surface flags on *[Object](../api/library/objects/class.object_cs.md)* that say whether a surface takes part in the bake and what it contributes: *[*SetExperimentalNavigation()*](../api/library/objects/class.object_cs.md#setExperimentalNavigation_int_int_void)*, *[*SetExperimentalNavigationArea()*](../api/library/objects/class.object_cs.md#setExperimentalNavigationArea_int_int_void)* and *[*SetExperimentalNavigationBakeMask()*](../api/library/objects/class.object_cs.md#setExperimentalNavigationBakeMask_int_int_void)*, each with a getter.
- The same three flags on *[TerrainDetailMask](../api/library/objects/landscape_terrain/class.terraindetailmask_cs.md)*, so a landscape detail can be baked as its own area, plus *[*SetExperimentalNavigationMinValue()*](../api/library/objects/landscape_terrain/class.terraindetailmask_cs.md#setExperimentalNavigationMinValue_float_void)* for the mask value the detail starts to count from.
- *[*World.SetExperimentalNavigationSettings()*](../api/library/engine/class.world_cs.md#setExperimentalNavigationSettings_cstr_void)* and its getter.
- *[*NavigationMesh.GetBakeSettings()*](../api/library/pathfinding/class.navigationmesh_cs.md#getBakeSettings_ExperimentalNavigationBakeSettings)*.
- The *[Property::PARAMETER_MASK_EXPERIMENTAL_NAVIGATION_BAKE](../api/library/common/class.property_cs.md#PARAMETER_MASK_EXPERIMENTAL_NAVIGATION_BAKE)* parameter mask.


For what the system does and how to set it up, see [Experimental Navigation](../objects/navigations/experimental/index.md).


### Skeleton Control Rig


Procedural control over a skeleton has been added, and it is an addition only - no existing skeletal animation API has changed. The new classes describe what a control rig node is to do, and are passed to the corresponding nodes of the animation graph:


- Inverse kinematics - *[IKInfo](../api/library/animations/skeletal/class.ikinfo_cs.md)*, *[IKInfoChain](../api/library/animations/skeletal/class.ikinfochain_cs.md)*, *[IKInfoTwoBone](../api/library/animations/skeletal/class.ikinfotwobone_cs.md)*.
- Joint limits - *[JointLimitInfo](../api/library/animations/skeletal/class.jointlimitinfo_cs.md)* and its cone, twist and hinge variants, collected in a *[JointLimitSetInfo](../api/library/animations/skeletal/class.jointlimitsetinfo_cs.md)*.
- Look-at - *[LookAtInfo](../api/library/animations/skeletal/class.lookatinfo_cs.md)* and *[LookAtChainInfo](../api/library/animations/skeletal/class.lookatchaininfo_cs.md)*.


## AmbientSource Class


#### New Properties


- *[**PitchShift**](../api/library/sounds/class.ambientsource_cs.md#PitchShift)*


## AnimationBind Class


#### New Functions


- *[**AddTarget**( AnimationBind.MATCH_BY )](../api/library/animations/timeline/class.animationbind_cs.md#addTarget_int_int)*
- *[**DuplicateTarget**( int )](../api/library/animations/timeline/class.animationbind_cs.md#duplicateTarget_int_int)*
- *[**GetNumTargetInheritanceMatches**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getNumTargetInheritanceMatches_int_int)*
- *[**GetNumTargetMatches**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getNumTargetMatches_int_int)*
- *[**GetResolvedAssetGUID**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getResolvedAssetGUID_int_UGUID)*
- *[**GetResolvedNodeID**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getResolvedNodeID_int_int)*
- *[**GetTargetAssetAccess**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetAssetAccess_int_int)*
- *[**GetTargetAssetFileGUID**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetAssetFileGUID_int_UGUID)*
- *[**GetTargetAssetName**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetAssetName_int_cstr)*
- *[**GetTargetAssetRuntimeGUID**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetAssetRuntimeGUID_int_UGUID)*
- *[**GetTargetComponentGUID**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetComponentGUID_int_UGUID)*
- *[**GetTargetInheritRootGUID**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetInheritRootGUID_int_UGUID)*
- *[**GetTargetLiveNodeID**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetLiveNodeID_int_int)*
- *[**GetTargetMatchBy**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetMatchBy_int_int)*
- *[**GetTargetMatchName**( int, int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetMatchName_int_int_cstr)*
- *[**GetTargetNamePattern**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetNamePattern_int_cstr)*
- *[**GetTargetNodeAccess**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetNodeAccess_int_int)*
- *[**GetTargetNodeID**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetNodeID_int_int)*
- *[**GetTargetNodeName**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetNodeName_int_cstr)*
- *[**GetTargetNodeReferenceGUID**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetNodeReferenceGUID_int_UGUID)*
- *[**GetTargetNodeType**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetNodeType_int_int)*
- *[**GetTargetPropertyGUID**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetPropertyGUID_int_UGUID)*
- *[**GetTargetRefInnerID**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetRefInnerID_int_int)*
- *[**GetTargetScope**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetScope_int_int)*
- *[**GetTargetSubtreeRootAccess**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetSubtreeRootAccess_int_int)*
- *[**GetTargetSubtreeRootID**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetSubtreeRootID_int_int)*
- *[**GetTargetSubtreeRootLiveNodeID**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetSubtreeRootLiveNodeID_int_int)*
- *[**GetTargetSubtreeRootName**( int )](../api/library/animations/timeline/class.animationbind_cs.md#getTargetSubtreeRootName_int_cstr)*
- *[**IsTargetNodeTypeIsGroup**( int )](../api/library/animations/timeline/class.animationbind_cs.md#isTargetNodeTypeIsGroup_int_int)*
- *[**Load**( Blob )](../api/library/animations/timeline/class.animationbind_cs.md#load_Blob_void)*
- *[**MoveTarget**( int, int )](../api/library/animations/timeline/class.animationbind_cs.md#moveTarget_int_int_void)*
- *[**MoveTargets**( int[], int )](../api/library/animations/timeline/class.animationbind_cs.md#moveTargets_VECint_int_void)*
- *[**RemoveTarget**( int )](../api/library/animations/timeline/class.animationbind_cs.md#removeTarget_int_void)*
- *[**Save**( Blob )](../api/library/animations/timeline/class.animationbind_cs.md#save_Blob_void)*
- *[**SetTargetAsset**( int, UGUID, UGUID )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetAsset_int_UGUID_UGUID_void)*
- *[**SetTargetAssetAccess**( int, AnimationBind.ASSET_ACCESS )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetAssetAccess_int_int_void)*
- *[**SetTargetAssetFileGUID**( int, UGUID )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetAssetFileGUID_int_UGUID_void)*
- *[**SetTargetAssetName**( int, string )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetAssetName_int_cstr_void)*
- *[**SetTargetComponentGUID**( int, UGUID )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetComponentGUID_int_UGUID_void)*
- *[**SetTargetInheritRootGUID**( int, UGUID )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetInheritRootGUID_int_UGUID_void)*
- *[**SetTargetMatchBy**( int, AnimationBind.MATCH_BY )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetMatchBy_int_int_void)*
- *[**SetTargetNamePattern**( int, string )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetNamePattern_int_cstr_void)*
- *[**SetTargetNode**( int, Node )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetNode_int_Node_void)*
- *[**SetTargetNodeAccess**( int, AnimationBind.NODE_ACCESS )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetNodeAccess_int_int_void)*
- *[**SetTargetNodeDescription**( int, int, string )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetNodeDescription_int_int_cstr_void)*
- *[**SetTargetNodeReferenceGUID**( int, UGUID )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetNodeReferenceGUID_int_UGUID_void)*
- *[**SetTargetNodeType**( int, int )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetNodeType_int_int_void)*
- *[**SetTargetNodeTypeIsGroup**( int, bool )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetNodeTypeIsGroup_int_int_void)*
- *[**SetTargetPropertyGUID**( int, UGUID )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetPropertyGUID_int_UGUID_void)*
- *[**SetTargetRefInnerID**( int, int )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetRefInnerID_int_int_void)*
- *[**SetTargetScope**( int, AnimationBind.QUERY_SCOPE )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetScope_int_int_void)*
- *[**SetTargetSubtreeRoot**( int, int, string )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetSubtreeRoot_int_int_cstr_void)*
- *[**SetTargetSubtreeRootAccess**( int, AnimationBind.NODE_ACCESS )](../api/library/animations/timeline/class.animationbind_cs.md#setTargetSubtreeRootAccess_int_int_void)*


#### New Properties


- *[**NumTargets**](../api/library/animations/timeline/class.animationbind_cs.md#NumTargets)*


#### New Enums


- *[**ASSET_ACCESS**](../api/library/animations/timeline/class.animationbind_cs.md#ASSET_ACCESS)*
- *[**MATCH_BY**](../api/library/animations/timeline/class.animationbind_cs.md#MATCH_BY)*
- *[**NODE_ACCESS**](../api/library/animations/timeline/class.animationbind_cs.md#NODE_ACCESS)*
- *[**NODE_TYPE_GROUP**](../api/library/animations/timeline/class.animationbind_cs.md#NODE_TYPE_GROUP)*
- *[**QUERY_SCOPE**](../api/library/animations/timeline/class.animationbind_cs.md#QUERY_SCOPE)*
- *[**TYPE.ANIMATION_BIND_COMPONENT**](../api/library/animations/timeline/class.animationbind_cs.md#ANIMATION_BIND_COMPONENT)*


## AnimationBindMaterial Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***SetMaterialDescription**( UGUID, UGUID )* | Removed. Use *[**setAssets()**](../api/library/animations/timeline/class.animationbindmaterial_cs.md#setAssets_VECUGUID_void)* instead. |
| ***SetObjectDescription**( int, string )* | Removed. Use *[**setObjects()**](../api/library/animations/timeline/class.animationbindmaterial_cs.md#setObjects_VECNode_void)* instead. |
| ***SetSurfaceDescription**( string, int )* | Removed. Use *[**setSurfacePattern()**](../api/library/animations/timeline/class.animationbindmaterial_cs.md#setSurfacePattern_cstr_void)* instead. |
| ***Material*** | Removed. |
| ***MaterialDescriptionFileGUID*** | Removed. |
| ***MaterialDescriptionGUID*** | Removed. |
| ***Object*** | Removed. |
| ***ObjectDescriptionID*** | Removed. |
| ***ObjectDescriptionName*** | Removed. |
| ***SurfaceDescriptionIndex*** | Removed. |
| ***SurfaceDescriptionName*** | Removed. |


#### New Functions


- *[**GetNumTargetSurfaceMatches**( int )](../api/library/animations/timeline/class.animationbindmaterial_cs.md#getNumTargetSurfaceMatches_int_int)*
- *[**GetTargetResolvedObject**( int )](../api/library/animations/timeline/class.animationbindmaterial_cs.md#getTargetResolvedObject_int_Object)*
- *[**SetAssets**( UGUID[] )](../api/library/animations/timeline/class.animationbindmaterial_cs.md#setAssets_VECUGUID_void)*
- *[**SetObjects**( Node[] )](../api/library/animations/timeline/class.animationbindmaterial_cs.md#setObjects_VECNode_void)*


#### New Properties


- *[**SurfacePattern**](../api/library/animations/timeline/class.animationbindmaterial_cs.md#SurfacePattern)*


#### New Enums


- *[**ACCESS.UNKNOWN**](../api/library/animations/timeline/class.animationbindmaterial_cs.md#ACCESS_UNKNOWN)*


## AnimationBindNode Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***SetNodeDescription**( int, string )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cs.md)* for the query it is built from. |
| ***Node*** | Removed. |
| ***NodeDescriptionID*** | Removed. |
| ***NodeDescriptionName*** | Removed. |


#### New Functions


- *[**GetTargetResolvedNode**( int )](../api/library/animations/timeline/class.animationbindnode_cs.md#getTargetResolvedNode_int_Node)*
- *[**SetNodes**( Node[] )](../api/library/animations/timeline/class.animationbindnode_cs.md#setNodes_VECNode_void)*


## AnimationBindPropertyParameter Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***SetNodeDescription**( int, string )* | Removed. Use *[**setNodes()**](../api/library/animations/timeline/class.animationbindpropertyparameter_cs.md#setNodes_VECNode_void)* instead. |
| ***SetPropertyDescription**( UGUID, UGUID )* | Removed. Use *[**setAssets()**](../api/library/animations/timeline/class.animationbindpropertyparameter_cs.md#setAssets_VECUGUID_void)* instead. |
| ***SetSurfaceDescription**( string, int )* | Removed. Use *[**setSurfacePattern()**](../api/library/animations/timeline/class.animationbindpropertyparameter_cs.md#setSurfacePattern_cstr_void)* instead. |
| ***Node*** | Removed. |
| ***NodeDescriptionID*** | Removed. |
| ***NodeDescriptionName*** | Removed. |
| ***Property*** | Removed. |
| ***PropertyDescriptionFileGUID*** | Removed. |
| ***PropertyDescriptionGUID*** | Removed. |
| ***PropertyParameter*** | Removed. |
| ***SurfaceDescriptionIndex*** | Removed. |
| ***SurfaceDescriptionName*** | Removed. |


#### New Functions


- *[**GetNumTargetSurfaceMatches**( int )](../api/library/animations/timeline/class.animationbindpropertyparameter_cs.md#getNumTargetSurfaceMatches_int_int)*
- *[**GetTargetResolvedNode**( int )](../api/library/animations/timeline/class.animationbindpropertyparameter_cs.md#getTargetResolvedNode_int_Node)*
- *[**GetTargetResolvedProperty**( int )](../api/library/animations/timeline/class.animationbindpropertyparameter_cs.md#getTargetResolvedProperty_int_Property)*
- *[**SetAssets**( UGUID[] )](../api/library/animations/timeline/class.animationbindpropertyparameter_cs.md#setAssets_VECUGUID_void)*
- *[**SetNodes**( Node[] )](../api/library/animations/timeline/class.animationbindpropertyparameter_cs.md#setNodes_VECNode_void)*


#### New Properties


- *[**SurfacePattern**](../api/library/animations/timeline/class.animationbindpropertyparameter_cs.md#SurfacePattern)*


#### New Enums


- *[**ACCESS.UNKNOWN**](../api/library/animations/timeline/class.animationbindpropertyparameter_cs.md#ACCESS_UNKNOWN)*


## AnimationBindRuntime Class


#### New Properties


- *[**AmbientSource**](../api/library/animations/timeline/class.animationbindruntime_cs.md#AmbientSource)*
- *[**AnimScript**](../api/library/animations/timeline/class.animationbindruntime_cs.md#AnimScript)*
- *[**Body**](../api/library/animations/timeline/class.animationbindruntime_cs.md#Body)*
- *[**Camera**](../api/library/animations/timeline/class.animationbindruntime_cs.md#Camera)*
- *[**Gui**](../api/library/animations/timeline/class.animationbindruntime_cs.md#Gui)*
- *[**Joint**](../api/library/animations/timeline/class.animationbindruntime_cs.md#Joint)*
- *[**LensFlare**](../api/library/animations/timeline/class.animationbindruntime_cs.md#LensFlare)*
- *[**ParticleModifier**](../api/library/animations/timeline/class.animationbindruntime_cs.md#ParticleModifier)*
- *[**Property**](../api/library/animations/timeline/class.animationbindruntime_cs.md#Property)*
- *[**RenderEnvironmentPreset**](../api/library/animations/timeline/class.animationbindruntime_cs.md#RenderEnvironmentPreset)*
- *[**Sequence**](../api/library/animations/timeline/class.animationbindruntime_cs.md#Sequence)*
- *[**Shape**](../api/library/animations/timeline/class.animationbindruntime_cs.md#Shape)*
- *[**Viewport**](../api/library/animations/timeline/class.animationbindruntime_cs.md#Viewport)*
- *[**Window**](../api/library/animations/timeline/class.animationbindruntime_cs.md#Window)*


## AnimationCurve Class


#### New Functions


- *[**WrapSourceTime**( float, float, AnimationCurve.EXTRAPOLATION, AnimationCurve.EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurve_cs.md#wrapSourceTime_float_float_int_int_float)*


#### New Enums


- *[**EXTRAPOLATION**](../api/library/animations/timeline/class.animationcurve_cs.md#EXTRAPOLATION)*
- *[**KEY_TYPE.ALIGNED**](../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE_ALIGNED)*
- *[**KEY_TYPE.AUTO_FLAT**](../api/library/animations/timeline/class.animationcurve_cs.md#KEY_TYPE_AUTO_FLAT)*


## AnimationCurveBool Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***Copy**( AnimationCurveBool )* | Renamed. Use *[**AssignFrom**](../api/library/animations/timeline/class.animationcurvebool_cs.md#assignFrom_AnimationCurveBool_void)* instead. |
| ***SetKeyType**( int, AnimationCurve.KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |
| ***SetKeyLeftTangent**( int, vec2 )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |
| ***SetKeyRightTangent**( int, vec2 )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |
| ***SetTypeOfAllKeys**( AnimationCurve.KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |


#### New Functions


- *[**AssignFrom**( AnimationCurveBool )](../api/library/animations/timeline/class.animationcurvebool_cs.md#assignFrom_AnimationCurveBool_void)*


#### New Properties


- *[**PostInfinity**](../api/library/animations/timeline/class.animationcurvebool_cs.md#PostInfinity)*
- *[**PreInfinity**](../api/library/animations/timeline/class.animationcurvebool_cs.md#PreInfinity)*


## AnimationCurveDouble Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***Copy**( AnimationCurveDouble )* | Renamed. Use *[**AssignFrom**](../api/library/animations/timeline/class.animationcurvedouble_cs.md#assignFrom_AnimationCurveDouble_void)* instead. |
| ***SetKeyType**( int, AnimationCurve.KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |
| ***SetKeyLeftTangent**( int, vec2 )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |
| ***SetKeyRightTangent**( int, vec2 )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |
| ***SetTypeOfAllKeys**( AnimationCurve.KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |


#### New Functions


- *[**AssignFrom**( AnimationCurveDouble )](../api/library/animations/timeline/class.animationcurvedouble_cs.md#assignFrom_AnimationCurveDouble_void)*


#### New Properties


- *[**PostInfinity**](../api/library/animations/timeline/class.animationcurvedouble_cs.md#PostInfinity)*
- *[**PreInfinity**](../api/library/animations/timeline/class.animationcurvedouble_cs.md#PreInfinity)*


## AnimationCurveFloat Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***Copy**( AnimationCurveFloat )* | Renamed. Use *[**AssignFrom**](../api/library/animations/timeline/class.animationcurvefloat_cs.md#assignFrom_AnimationCurveFloat_void)* instead. |
| ***SetKeyType**( int, AnimationCurve.KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |
| ***SetKeyLeftTangent**( int, vec2 )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |
| ***SetKeyRightTangent**( int, vec2 )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |
| ***SetTypeOfAllKeys**( AnimationCurve.KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |


#### New Functions


- *[**AssignFrom**( AnimationCurveFloat )](../api/library/animations/timeline/class.animationcurvefloat_cs.md#assignFrom_AnimationCurveFloat_void)*


#### New Properties


- *[**PostInfinity**](../api/library/animations/timeline/class.animationcurvefloat_cs.md#PostInfinity)*
- *[**PreInfinity**](../api/library/animations/timeline/class.animationcurvefloat_cs.md#PreInfinity)*


## AnimationCurveInt Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***Copy**( AnimationCurveInt )* | Renamed. Use *[**AssignFrom**](../api/library/animations/timeline/class.animationcurveint_cs.md#assignFrom_AnimationCurveInt_void)* instead. |
| ***SetKeyType**( int, AnimationCurve.KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |
| ***SetKeyLeftTangent**( int, vec2 )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |
| ***SetKeyRightTangent**( int, vec2 )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |
| ***SetTypeOfAllKeys**( AnimationCurve.KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |


#### New Functions


- *[**AssignFrom**( AnimationCurveInt )](../api/library/animations/timeline/class.animationcurveint_cs.md#assignFrom_AnimationCurveInt_void)*


#### New Properties


- *[**PostInfinity**](../api/library/animations/timeline/class.animationcurveint_cs.md#PostInfinity)*
- *[**PreInfinity**](../api/library/animations/timeline/class.animationcurveint_cs.md#PreInfinity)*


## AnimationCurveQuat Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***Copy**( AnimationCurveQuat )* | Renamed. Use *[**AssignFrom**](../api/library/animations/timeline/class.animationcurvequat_cs.md#assignFrom_AnimationCurveQuat_void)* instead. |


#### New Functions


- *[**AssignFrom**( AnimationCurveQuat )](../api/library/animations/timeline/class.animationcurvequat_cs.md#assignFrom_AnimationCurveQuat_void)*


#### New Properties


- *[**PostInfinity**](../api/library/animations/timeline/class.animationcurvequat_cs.md#PostInfinity)*
- *[**PreInfinity**](../api/library/animations/timeline/class.animationcurvequat_cs.md#PreInfinity)*


## AnimationCurveScalar Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***Copy**( AnimationCurveScalar )* | Renamed. Use *[**AssignFrom**](../api/library/animations/timeline/class.animationcurvescalar_cs.md#assignFrom_AnimationCurveScalar_void)* instead. |
| ***SetKeyType**( int, AnimationCurve.KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |
| ***SetKeyLeftTangent**( int, vec2 )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |
| ***SetKeyRightTangent**( int, vec2 )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |
| ***SetTypeOfAllKeys**( AnimationCurve.KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cs.md#sequencer_migration_tangent_ratio). |


#### New Functions


- *[**AssignFrom**( AnimationCurveScalar )](../api/library/animations/timeline/class.animationcurvescalar_cs.md#assignFrom_AnimationCurveScalar_void)*


#### New Properties


- *[**PostInfinity**](../api/library/animations/timeline/class.animationcurvescalar_cs.md#PostInfinity)*
- *[**PreInfinity**](../api/library/animations/timeline/class.animationcurvescalar_cs.md#PreInfinity)*


## AnimationCurveString Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***Copy**( AnimationCurveString )* | Renamed. Use *[**AssignFrom**](../api/library/animations/timeline/class.animationcurvestring_cs.md#assignFrom_AnimationCurveString_void)* instead. |


#### New Functions


- *[**AssignFrom**( AnimationCurveString )](../api/library/animations/timeline/class.animationcurvestring_cs.md#assignFrom_AnimationCurveString_void)*


#### New Properties


- *[**PostInfinity**](../api/library/animations/timeline/class.animationcurvestring_cs.md#PostInfinity)*
- *[**PreInfinity**](../api/library/animations/timeline/class.animationcurvestring_cs.md#PreInfinity)*


## AnimationCurveUGUID Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***Copy**( AnimationCurveUGUID )* | Renamed. Use *[**AssignFrom**](../api/library/animations/timeline/class.animationcurveuguid_cs.md#assignFrom_AnimationCurveUGUID_void)* instead. |


#### New Functions


- *[**AssignFrom**( AnimationCurveUGUID )](../api/library/animations/timeline/class.animationcurveuguid_cs.md#assignFrom_AnimationCurveUGUID_void)*


#### New Properties


- *[**PostInfinity**](../api/library/animations/timeline/class.animationcurveuguid_cs.md#PostInfinity)*
- *[**PreInfinity**](../api/library/animations/timeline/class.animationcurveuguid_cs.md#PreInfinity)*


## Animations Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***AnimToBonesModifier**( string, AnimationModifierBones, float )* | Renamed. Use *[**AnimToBonesChannel**](../api/library/animations/class.animations_cs.md#animToBonesChannel_cstr_AnimationChannelBones_float_int)* instead. |
| ***CheckUtrackTypes**( )* | Removed. |
| ***ContainsObject**( int )* | Removed together with the *AnimationObject* class. Bindings are the *[AnimationBind](../api/library/animations/timeline/class.animationbind_cs.md)* classes now. |
| ***ContainsPlayback**( UGUID )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cs.md)* node. |
| ***ContainsTrack**( UGUID )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)*. |
| ***ConvertToUanims**( string, string[] )* | Removed. |
| ***ConvertToUanims**( string[], string[] )* | Removed. |
| ***GetObjectByID**( int )* | Removed together with the *AnimationObject* class. Bindings are the *[AnimationBind](../api/library/animations/timeline/class.animationbind_cs.md)* classes now. |
| ***GetObjectByIndex**( int )* | Removed together with the *AnimationObject* class. Bindings are the *[AnimationBind](../api/library/animations/timeline/class.animationbind_cs.md)* classes now. |
| ***GetObjectIndex**( AnimationObject )* | Removed together with the *AnimationObject* class. Bindings are the *[AnimationBind](../api/library/animations/timeline/class.animationbind_cs.md)* classes now. |
| ***GetParameterModifierType**( AnimParams.PARAM )* | Renamed. Use *[**GetParameterChannelType**](../api/library/animations/class.animations_cs.md#getParameterChannelType_int_int)* instead. |
| ***GetPlaybackByFileGUID**( UGUID )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cs.md)* node. |
| ***GetPlaybackByGUID**( UGUID )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cs.md)* node. |
| ***GetPlaybackByIndex**( int )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cs.md)* node. |
| ***GetPlaybackByPath**( string )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cs.md)* node. |
| ***GetPlaybackIndex**( AnimationPlayback )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cs.md)* node. |
| ***GetTrackByFileGUID**( UGUID )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)*. |
| ***GetTrackByGUID**( UGUID )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)*. |
| ***GetTrackByIndex**( int )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)*. |
| ***GetTrackByPath**( string )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)*. |
| ***GetTrackIndex**( AnimationTrack )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)*. |
| ***LoadPlayback**( string )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cs.md)* node. |
| ***LoadPlaybacks**( )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cs.md)* node. |
| ***LoadTrack**( string )* | Removed. Assign a path with *[**AnimationSequence::setPath()**](../api/library/animations/timeline/class.animationsequence_cs.md#setPath_cstr_void)* and call *[**AnimationSequence::load()**](../api/library/animations/timeline/class.animationsequence_cs.md#load_int)*. |
| ***LoadTracks**( )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)*. |
| ***ReloadTrack**( string )* | Removed. Call *[**AnimationSequence::load()**](../api/library/animations/timeline/class.animationsequence_cs.md#load_int)* again. |
| ***ReloadTracks**( )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)*. |
| ***SavePlayback**( AnimationPlayback, string )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cs.md)* node. |
| ***SaveTrack**( AnimationTrack, string )* | Removed. Use *[**AnimationSequence::save()**](../api/library/animations/timeline/class.animationsequence_cs.md#save_int)* instead. |
| ***SaveTrackPrecomputed**( AnimationTrack, int, bool, string )* | Removed. |
| ***UnloadTracks**( )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)*. |
| ***EventObjectAdded*** | Removed together with the *AnimationObject* class. Bindings are the *[AnimationBind](../api/library/animations/timeline/class.animationbind_cs.md)* classes now. |
| ***EventObjectRemoved*** | Removed together with the *AnimationObject* class. Bindings are the *[AnimationBind](../api/library/animations/timeline/class.animationbind_cs.md)* classes now. |
| ***EventTrackAdded*** | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)*. |
| ***EventTrackRemoved*** | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)*. |
| ***NumObjects*** | Removed together with the *AnimationObject* class. Bindings are the *[AnimationBind](../api/library/animations/timeline/class.animationbind_cs.md)* classes now. |
| ***NumPlaybacks*** | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cs.md)* node. |
| ***NumTracks*** | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cs.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cs.md)*. |
| ***RESULT.NEW_PLAYBACK_LOADED*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT.NEW_TRACK_LOADED*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT.PLAYBACK_ERROR*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT.PLAYBACK_IS_ALREADY_LOADED*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT.PLAYBACK_SAVED*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT.TRACK_ERROR*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT.TRACK_IS_ALREADY_LOADED*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT.TRACK_RELOADED*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT.TRACK_SAVED*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT.TRACK_UNLOADED*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT*** | Removed together with the loading and saving methods that returned it. |


#### New Functions


- *[**AnimToBonesChannel**( string, AnimationChannelBones, float )](../api/library/animations/class.animations_cs.md#animToBonesChannel_cstr_AnimationChannelBones_float_int)*
- *[**ConvertLegacyTrackToSequence**( string, string, bool )](../api/library/animations/class.animations_cs.md#convertLegacyTrackToSequence_cstr_cstr_int_String)*
- *[**FetchComponentWrites**( Blob )](../api/library/animations/class.animations_cs.md#fetchComponentWrites_Blob_void)*
- *[**GetBaseClasses**( string[] )](../api/library/animations/class.animations_cs.md#getBaseClasses_VECString_int)*
- *[**GetChannelPropertyDefaultValue**( AnimationChannel.PROPERTY )](../api/library/animations/class.animations_cs.md#getChannelPropertyDefaultValue_int_float)*
- *[**GetChannelPropertyMaxValue**( AnimationChannel.PROPERTY )](../api/library/animations/class.animations_cs.md#getChannelPropertyMaxValue_int_float)*
- *[**GetChannelPropertyMinValue**( AnimationChannel.PROPERTY )](../api/library/animations/class.animations_cs.md#getChannelPropertyMinValue_int_float)*
- *[**GetChannelPropertyName**( AnimationChannel.PROPERTY )](../api/library/animations/class.animations_cs.md#getChannelPropertyName_int_cstr)*
- *[**GetChannelSlotCount**( AnimationChannel )](../api/library/animations/class.animations_cs.md#getChannelSlotCount_AnimationChannel_int)*
- *[**GetChannelSlotIndex**( AnimationChannel, string )](../api/library/animations/class.animations_cs.md#getChannelSlotIndex_AnimationChannel_cstr_int)*
- *[**GetChannelSlotNames**( AnimationChannel, string[] )](../api/library/animations/class.animations_cs.md#getChannelSlotNames_AnimationChannel_VECString_int)*
- *[**GetChannelSupportedProperties**( AnimationChannel.TYPE, int[] )](../api/library/animations/class.animations_cs.md#getChannelSupportedProperties_int_VECint_int)*
- *[**GetParameterAccess**( AnimParams.PARAM )](../api/library/animations/class.animations_cs.md#getParameterAccess_int_int)*
- *[**GetParameterAssetExtension**( AnimParams.PARAM )](../api/library/animations/class.animations_cs.md#getParameterAssetExtension_int_cstr)*
- *[**GetParameterBindType**( AnimParams.PARAM )](../api/library/animations/class.animations_cs.md#getParameterBindType_int_int)*
- *[**GetParameterByReflectionName**( string, string )](../api/library/animations/class.animations_cs.md#getParameterByReflectionName_cstr_cstr_int)*
- *[**GetParameterChannelType**( AnimParams.PARAM )](../api/library/animations/class.animations_cs.md#getParameterChannelType_int_int)*
- *[**GetParameterClass**( AnimParams.PARAM )](../api/library/animations/class.animations_cs.md#getParameterClass_int_cstr)*
- *[**GetParameterItems**( AnimParams.PARAM )](../api/library/animations/class.animations_cs.md#getParameterItems_int_cstr)*
- *[**GetParameterKeyName**( AnimParams.PARAM )](../api/library/animations/class.animations_cs.md#getParameterKeyName_int_cstr)*
- *[**GetParameterLogicalName**( AnimParams.PARAM )](../api/library/animations/class.animations_cs.md#getParameterLogicalName_int_cstr)*
- *[**GetParameterMaxValue**( AnimParams.PARAM )](../api/library/animations/class.animations_cs.md#getParameterMaxValue_int_cstr)*
- *[**GetParameterMinValue**( AnimParams.PARAM )](../api/library/animations/class.animations_cs.md#getParameterMinValue_int_cstr)*
- *[**GetParameterNodeType**( AnimParams.PARAM )](../api/library/animations/class.animations_cs.md#getParameterNodeType_int_cstr)*
- *[**GetParameterSlotKindName**( AnimParams.PARAM )](../api/library/animations/class.animations_cs.md#getParameterSlotKindName_int_cstr)*
- *[**GetParameterTitle**( AnimParams.PARAM )](../api/library/animations/class.animations_cs.md#getParameterTitle_int_cstr)*
- *[**GetParameterVecComponent**( AnimParams.PARAM )](../api/library/animations/class.animations_cs.md#getParameterVecComponent_int_int)*
- *[**GetParameterWidget**( AnimParams.PARAM )](../api/library/animations/class.animations_cs.md#getParameterWidget_int_int)*
- *[**IsChannelParameterReadable**( AnimationChannel )](../api/library/animations/class.animations_cs.md#isChannelParameterReadable_AnimationChannel_int)*
- *[**IsParameterTarget**( AnimParams.PARAM, Node )](../api/library/animations/class.animations_cs.md#isParameterTarget_int_Node_int)*
- *[**ReadChannelParameterValueFloat**( AnimationChannel, int, out float )](../api/library/animations/class.animations_cs.md#readChannelParameterValueFloat_AnimationChannel_int_float_int)*
- *[**ReadChannelParameterValueNode**( AnimationChannel )](../api/library/animations/class.animations_cs.md#readChannelParameterValueNode_AnimationChannel_Node)*
- *[**ReadChannelParameterValueString**( AnimationChannel )](../api/library/animations/class.animations_cs.md#readChannelParameterValueString_AnimationChannel_String)*
- *[**ReadChannelParameterValueUGUID**( AnimationChannel )](../api/library/animations/class.animations_cs.md#readChannelParameterValueUGUID_AnimationChannel_UGUID)*
- *[**ReadParameterValueFloat**( Node, AnimParams.PARAM, int, int, string, out float )](../api/library/animations/class.animations_cs.md#readParameterValueFloat_Node_int_int_int_cstr_float_int)*
- *[**RestoreEachFrame**( )](../api/library/animations/class.animations_cs.md#restoreEachFrame_void)*
- *[**SetComponentWritesCollecting**( bool )](../api/library/animations/class.animations_cs.md#setComponentWritesCollecting_int_void)*
- *[**SetSequencerMusicMuted**( bool )](../api/library/animations/class.animations_cs.md#setSequencerMusicMuted_int_void)*


#### New Properties


- *[**AnimScriptsPreviewBuild**](../api/library/animations/class.animations_cs.md#AnimScriptsPreviewBuild)*
- *[**MemoryUsage**](../api/library/animations/class.animations_cs.md#MemoryUsage)*


## AnimScript Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***GetStateMachineCurrentStateName**( string )* | Set of arguments changed - see [State Machines Addressed by Index](../upgrade/migration_api_cs.md#animscript_state_machines). |
| ***GetStateMachinePreviousStateName**( string )* | Set of arguments changed - see [State Machines Addressed by Index](../upgrade/migration_api_cs.md#animscript_state_machines). |
| ***GetStateMachineTransitionProgress**( string )* | Set of arguments changed - see [State Machines Addressed by Index](../upgrade/migration_api_cs.md#animscript_state_machines). |
| ***IsStateMachineActive**( string )* | Removed. Use *[**isStateMachineRelevant()**](../api/library/animations/skeletal/class.animscript_cs.md#isStateMachineRelevant_int_bool)* to tell whether a state machine takes part in the current pose. |
| ***IsStateMachineInTransition**( string )* | Set of arguments changed - see [State Machines Addressed by Index](../upgrade/migration_api_cs.md#animscript_state_machines). |


#### New Functions


- *[**FindStateMachine**( string )](../api/library/animations/skeletal/class.animscript_cs.md#findStateMachine_cstr_int)*
- *[**FindStateMachineByName**( string )](../api/library/animations/skeletal/class.animscript_cs.md#findStateMachineByName_cstr_int)*
- *[**FindStateMachineState**( int, string )](../api/library/animations/skeletal/class.animscript_cs.md#findStateMachineState_int_cstr_int)*
- *[**GetStateMachineAnimLength**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineAnimLength_int_float)*
- *[**GetStateMachineAnimTime**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineAnimTime_int_float)*
- *[**GetStateMachineAnimTimeFraction**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineAnimTimeFraction_int_float)*
- *[**GetStateMachineAnimTimeRemaining**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineAnimTimeRemaining_int_float)*
- *[**GetStateMachineAnimTimeRemainingFraction**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineAnimTimeRemainingFraction_int_float)*
- *[**GetStateMachineCurrentState**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineCurrentState_int_int)*
- *[**GetStateMachineCurrentStateName**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineCurrentStateName_int_cstr)*
- *[**GetStateMachineName**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineName_int_cstr)*
- *[**GetStateMachineNumStates**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineNumStates_int_int)*
- *[**GetStateMachineNumTransitionConditions**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineNumTransitionConditions_int_int)*
- *[**GetStateMachineOwnerStateName**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineOwnerStateName_int_cstr)*
- *[**GetStateMachineParent**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineParent_int_int)*
- *[**GetStateMachinePath**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachinePath_int_cstr)*
- *[**GetStateMachinePreviousState**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachinePreviousState_int_int)*
- *[**GetStateMachinePreviousStateName**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachinePreviousStateName_int_cstr)*
- *[**GetStateMachineStateName**( int, int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineStateName_int_int_cstr)*
- *[**GetStateMachineStateTime**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineStateTime_int_float)*
- *[**GetStateMachineTransitionConditionName**( int, int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineTransitionConditionName_int_int_cstr)*
- *[**GetStateMachineTransitionDuration**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineTransitionDuration_int_float)*
- *[**GetStateMachineTransitionProgress**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineTransitionProgress_int_float)*
- *[**GetStateMachineTransitionTime**( int )](../api/library/animations/skeletal/class.animscript_cs.md#getStateMachineTransitionTime_int_float)*
- *[**IsStateMachineAnimEnded**( int )](../api/library/animations/skeletal/class.animscript_cs.md#isStateMachineAnimEnded_int_bool)*
- *[**IsStateMachineInTransition**( int )](../api/library/animations/skeletal/class.animscript_cs.md#isStateMachineInTransition_int_bool)*
- *[**IsStateMachineRelevant**( int )](../api/library/animations/skeletal/class.animscript_cs.md#isStateMachineRelevant_int_bool)*
- *[**SetStateMachineState**( int, int, float )](../api/library/animations/skeletal/class.animscript_cs.md#setStateMachineState_int_int_float_void)*
- *[**SetStateMachineStateAtTime**( int, int, float, float )](../api/library/animations/skeletal/class.animscript_cs.md#setStateMachineStateAtTime_int_int_float_float_void)*


#### New Properties


- *[**NumStateMachines**](../api/library/animations/skeletal/class.animscript_cs.md#NumStateMachines)*
- *[**RootMotionDeltaPosition**](../api/library/animations/skeletal/class.animscript_cs.md#RootMotionDeltaPosition)*
- *[**RootMotionDeltaRotation**](../api/library/animations/skeletal/class.animscript_cs.md#RootMotionDeltaRotation)*


## BootConfig Class


#### New Functions


- *[**AddFallbackFont**( string )](../api/library/engine/class.bootconfig_cs.md#addFallbackFont_cstr_int)*
- *[**AddFontFallback**( int, string )](../api/library/engine/class.bootconfig_cs.md#addFontFallback_int_cstr_void)*
- *[**AddGlobalFontFallback**( string )](../api/library/engine/class.bootconfig_cs.md#addGlobalFontFallback_cstr_void)*
- *[**GetFallbackFontName**( int )](../api/library/engine/class.bootconfig_cs.md#getFallbackFontName_int_cstr)*
- *[**GetFontFallback**( int, int )](../api/library/engine/class.bootconfig_cs.md#getFontFallback_int_int_cstr)*
- *[**GetGlobalFontFallback**( int )](../api/library/engine/class.bootconfig_cs.md#getGlobalFontFallback_int_cstr)*
- *[**GetNumFontFallbacks**( int )](../api/library/engine/class.bootconfig_cs.md#getNumFontFallbacks_int_int)*
- *[**RemoveFontFallback**( int, int )](../api/library/engine/class.bootconfig_cs.md#removeFontFallback_int_int_void)*
- *[**RemoveGlobalFontFallback**( int )](../api/library/engine/class.bootconfig_cs.md#removeGlobalFontFallback_int_void)*
- *[**SetFontFallback**( int, int, string )](../api/library/engine/class.bootconfig_cs.md#setFontFallback_int_int_cstr_void)*
- *[**SetGlobalFontFallback**( int, string )](../api/library/engine/class.bootconfig_cs.md#setGlobalFontFallback_int_cstr_void)*


#### New Properties


- *[**NumFallbackFonts**](../api/library/engine/class.bootconfig_cs.md#NumFallbackFonts)*
- *[**NumGlobalFontFallbacks**](../api/library/engine/class.bootconfig_cs.md#NumGlobalFontFallbacks)*


## Console Class


#### New Functions


- *[**GetNumPresetNames**( string )](../api/library/engine/class.console_cs.md#getNumPresetNames_cstr_int)*
- *[**GetPresetName**( string, int )](../api/library/engine/class.console_cs.md#getPresetName_cstr_int_cstr)*


## CustomSystemProxy Class


New methods should be implemented in case you inherit from the *CustomSystemProxy* Class.


#### New Functions


- *[**isIMETextInputEnabled**( )](../api/library/engine/class.customsystemproxy_cs.md#isIMETextInputEnabled_bool)*
- *[**setIMETextInputEnabled**( bool )](../api/library/engine/class.customsystemproxy_cs.md#setIMETextInputEnabled_bool_void)*
- *[**setIMETextInputRect**( int, int, int, int )](../api/library/engine/class.customsystemproxy_cs.md#setIMETextInputRect_int_int_int_int_void)*


## Editor Class


#### New Functions


- *[**GetIntersection**( WorldBoundFrustum, Node[], Node[] )](../api/library/engine/class.editor_cs.md#getIntersection_WorldBoundFrustum_VECNode_VECNode_int)*


## EngineWindowViewport Class


#### New Functions


- *[**CalculateEngineRenderResolution**( out ivec2, out ivec2, out ivec2 )](../api/library/gui/class.enginewindowviewport_cs.md#calculateEngineRenderResolution_ivec2_ivec2_ivec2_void)*


## Ffp Class


#### New Enums


- *[**TEXTURE_SAMPLE_BINDLESS**](../api/library/rendering/class.ffp_cs.md#TEXTURE_SAMPLE_BINDLESS)*


## FMOD::Bus Class


#### New Properties


- *[**PortIndex**](../api/library/plugins/fmod/class.bus_cs.md#PortIndex)*


#### New Enums


- *[**PORT_INDEX**](../api/library/plugins/fmod/class.bus_cs.md#PORT_INDEX)*


## FMOD::EventInstance Class


#### New Functions


- *[**SetParameterWithLabel**( string, string, bool )](../api/library/plugins/fmod/class.eventinstance_cs.md#setParameterWithLabel_cstr_cstr_bool_void)*


## FMOD::FMOD Class


#### New Functions


- *[**LoadOutputPlugin**( string )](../api/library/plugins/fmod/class.fmod_cs.md#loadOutputPlugin_cstr_void)*


## FMOD::FMODCore Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| *[**CreateSound**( string, FMODEnums.FMOD_MODE )](../api/library/plugins/fmod/class.fmodcore_cs.md#createSound_cstr_int_Sound)* | Parameter name changed. |


#### New Functions


- *[**CreateSound**( Blob, FMODEnums.FMOD_MODE )](../api/library/plugins/fmod/class.fmodcore_cs.md#createSound_Blob_int_Sound)*


## FMOD::FMODStudio Class


#### New Functions


- *[**GetGlobalParameter**( string )](../api/library/plugins/fmod/class.fmodstudio_cs.md#getGlobalParameter_cstr_float)*
- *[**SetGlobalParameter**( string, float )](../api/library/plugins/fmod/class.fmodstudio_cs.md#setGlobalParameter_cstr_float_void)*
- *[**SetGlobalParameterWithLabel**( string, string, bool )](../api/library/plugins/fmod/class.fmodstudio_cs.md#setGlobalParameterWithLabel_cstr_cstr_bool_void)*


## Geodetics::Converter Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***GEODETIC_MODE.GEODETICS_PLUGIN_EPSG*** | Removed. Use *[**GEODETIC_MODE.PROJECTED**](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#GEODETIC_MODE_PROJECTED)* together with *[**PROJECTION_MODE.EPSG**](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#PROJECTION_MODE_EPSG)* instead. |
| ***GEODETIC_MODE.GEODETICS_PLUGIN_WKT2*** | Removed. Use *[**GEODETIC_MODE.PROJECTED**](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#GEODETIC_MODE_PROJECTED)* together with *[**PROJECTION_MODE.WKT2**](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#PROJECTION_MODE_WKT2)* instead. |
| *[**GeocentricEulerToGeodeticEuler**( dvec3, vec3 )](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#geocentricEulerToGeodeticEuler_dvec3_vec3_vec3)* | Parameter name changed. |
| *[**GeocentricToGeodetic**( dvec3, double, double )](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#geocentricToGeodetic_dvec3_double_double_dvec3)* | Parameter name changed. |
| *[**GeodeticEulerToGeocentricEuler**( dvec3, vec3 )](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#geodeticEulerToGeocentricEuler_dvec3_vec3_vec3)* | Parameter name changed. |
| *[**GeodeticEulerToRotation**( dvec3, vec3 )](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#geodeticEulerToRotation_dvec3_vec3_quat)* | Parameter name changed. |
| *[**GeodeticToGeocentric**( dvec3, double, double )](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#geodeticToGeocentric_dvec3_double_double_dvec3)* | Parameter name changed. |
| *[**GeodeticToWorld**( dvec3 )](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#geodeticToWorld_dvec3_Vec3)* | Parameter name changed. |
| *[**GetZeroBasis**( dvec3 )](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#getZeroBasis_dvec3_Mat4)* | Parameter name changed. |
| *[**GetZeroRotation**( dvec3 )](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#getZeroRotation_dvec3_quat)* | Parameter name changed. |
| *[**GetZeroUpDirection**( dvec3 )](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#getZeroUpDirection_dvec3_vec3)* | Parameter name changed. |
| *[**RotationToGeodeticEuler**( dvec3, quat )](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#rotationToGeodeticEuler_dvec3_quat_vec3)* | Parameter name changed. |
| *[**GetOrigin**( )](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#getOrigin_dvec3)* | Return value type changed. |


#### New Functions


- *[**GetAnchor**( )](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#getAnchor_Anchor)*


#### New Properties


- *[**ProjectionMode**](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#ProjectionMode)*


#### New Enums


- *[**GEODETIC_MODE.ANCHOR**](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#GEODETIC_MODE_ANCHOR)*
- *[**GEODETIC_MODE.PROJECTED**](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#GEODETIC_MODE_PROJECTED)*
- *[**PROJECTION_MODE**](../api/library/geodetics/geodetics_plugin/class.converter_cs.md#PROJECTION_MODE)*


## Geodetics::Transformer Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| *[**GeodeticToWorldPosition**( dvec3, bool )](../api/library/geodetics/geodetics_plugin/class.transformer_cs.md#geodeticToWorldPosition_dvec3_bool_dvec3)* | Parameter name changed. |
| *[**GeodeticToWorld**( dvec3, bool )](../api/library/geodetics/geodetics_plugin/class.transformer_cs.md#geodeticToWorld_dvec3_bool_dmat4)* | Parameter name changed. |
| *[**SetProjectionEpsg**( int, dvec3, string, bool )](../api/library/geodetics/geodetics_plugin/class.transformer_cs.md#setProjectionEpsg_int_dvec3_cstr_bool_int)* | Parameter name changed. |
| *[**SetProjectionWkt**( string, dvec3, string, bool )](../api/library/geodetics/geodetics_plugin/class.transformer_cs.md#setProjectionWkt_cstr_dvec3_cstr_bool_int)* | Parameter name changed. |


## Gui Class


#### New Properties


- *[**GlobalCursorMode**](../api/library/gui/class.gui_cs.md#GlobalCursorMode)*
- *[**GlobalTextDirection**](../api/library/gui/class.gui_cs.md#GlobalTextDirection)*


#### New Enums


- *[**CursorMode**](../api/library/gui/class.gui_cs.md#CursorMode)*
- *[**TextDirection**](../api/library/gui/class.gui_cs.md#TextDirection)*


## Input Class


#### New Functions


- *[**SetIMETextInputRect**( int, int, int, int )](../api/library/controls/class.input_cs.md#setIMETextInputRect_int_int_int_int_void)*


#### New Properties


- *[**EventTextEditing**](../api/library/controls/class.input_cs.md#EventTextEditing)*
- *[**IMEEnabled**](../api/library/controls/class.input_cs.md#IMEEnabled)*


## InputEvent Class


#### New Enums


- *[**TYPE.INPUT_EVENT_PAD_ACCELEROMETER_MOTION**](../api/library/controls/class.inputevent_cs.md#INPUT_EVENT_PAD_ACCELEROMETER_MOTION)*
- *[**TYPE.INPUT_EVENT_PAD_GYROSCOPE_MOTION**](../api/library/controls/class.inputevent_cs.md#INPUT_EVENT_PAD_GYROSCOPE_MOTION)*
- *[**TYPE.INPUT_EVENT_TEXT_EDITING**](../api/library/controls/class.inputevent_cs.md#INPUT_EVENT_TEXT_EDITING)*


## InputEventPadButton Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***InputEventPadButton**( ulong, ivec2, InputEventJoyButton.ACTION, int, Input.GAMEPAD_BUTTON )* | Renamed. Use *[**InputEventPadButton**](../api/library/controls/class.inputeventpadbutton_cs.md#InputEventPadButton_ulonglong_constMathivec2_InputEventPadButtonACTION_int_InputGAMEPAD_BUTTON)* instead. |


## InputGamePad Class


#### New Functions


- *[**SetLightColor**( vec3 )](../api/library/controls/class.inputgamepad_cs.md#setLightColor_vec3_void)*


#### New Properties


- *[**Acceleration**](../api/library/controls/class.inputgamepad_cs.md#Acceleration)*
- *[**AngularVelocity**](../api/library/controls/class.inputgamepad_cs.md#AngularVelocity)*
- *[**IsAccelerationSupported**](../api/library/controls/class.inputgamepad_cs.md#IsAccelerationSupported)*
- *[**IsAngularVelocitySupported**](../api/library/controls/class.inputgamepad_cs.md#IsAngularVelocitySupported)*
- *[**IsLightSupported**](../api/library/controls/class.inputgamepad_cs.md#IsLightSupported)*


## InputVRDevice Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***CanReportBatteryValue**( )* | Renamed. Use *[**IsBatteryValid**](../api/library/controls/class.inputvrdevice_cs.md#isBatteryValid_int)* instead. |
| ***IsCharging*** | Renamed. Use *[**IsBatteryCharging**](../api/library/controls/class.inputvrdevice_cs.md#IsBatteryCharging)* instead. |


#### New Properties


- *[**IsBatteryCharging**](../api/library/controls/class.inputvrdevice_cs.md#IsBatteryCharging)*
- *[**IsBatteryPluggedIn**](../api/library/controls/class.inputvrdevice_cs.md#IsBatteryPluggedIn)*
- *[**IsBatteryValid**](../api/library/controls/class.inputvrdevice_cs.md#IsBatteryValid)*


## Light Class


#### New Properties


- *[**SpecularRoughnessOffset**](../api/library/lights/class.light_cs.md#SpecularRoughnessOffset)*


## LightEnvironmentProbe Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***RenderAboveVoxelProbes*** | Removed. |


#### New Properties


- *[**GrabDynamicInterleaved**](../api/library/lights/class.lightenvironmentprobe_cs.md#GrabDynamicInterleaved)*
- *[**GrabDynamicInterleavedColorClamping**](../api/library/lights/class.lightenvironmentprobe_cs.md#GrabDynamicInterleavedColorClamping)*
- *[**GrabDynamicReprojection**](../api/library/lights/class.lightenvironmentprobe_cs.md#GrabDynamicReprojection)*


#### New Enums


- *[**GRAB_DYNAMIC_REPROJECTION**](../api/library/lights/class.lightenvironmentprobe_cs.md#GRAB_DYNAMIC_REPROJECTION)*
- *[**LAST_STEP_MODE.UNDERLYING_PROBES**](../api/library/lights/class.lightenvironmentprobe_cs.md#LAST_STEP_MODE_UNDERLYING_PROBES)*
- *[**GRAB_DYNAMIC_INTERLEAVED**](../api/library/lights/class.lightenvironmentprobe_cs.md#GRAB_DYNAMIC_INTERLEAVED)*
- *[**GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING**](../api/library/lights/class.lightenvironmentprobe_cs.md#GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING)*


## LightVoxelProbe Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***BakeVisibilityEnvironmentProbe*** | Removed. |


## LightWorld Class


#### New Properties


- *[**ShadowCascadeOriginMode**](../api/library/lights/class.lightworld_cs.md#ShadowCascadeOriginMode)*
- *[**ShadowCascadeOriginPosition**](../api/library/lights/class.lightworld_cs.md#ShadowCascadeOriginPosition)*
- *[**ShadowCascadePlacementMode**](../api/library/lights/class.lightworld_cs.md#ShadowCascadePlacementMode)*
- *[**ShadowFilterFar**](../api/library/lights/class.lightworld_cs.md#ShadowFilterFar)*


#### New Enums


- *[**SHADOW_CASCADE_ORIGIN_MODE**](../api/library/lights/class.lightworld_cs.md#SHADOW_CASCADE_ORIGIN_MODE)*
- *[**SHADOW_CASCADE_PLACEMENT_MODE**](../api/library/lights/class.lightworld_cs.md#SHADOW_CASCADE_PLACEMENT_MODE)*


## Material Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***OPTION_OVERLAP*** | Renamed. Use *[**OPTION_TRANSPARENT_ORDER**](../api/library/rendering/class.material_cs.md#OPTION_TRANSPARENT_ORDER)* instead - see [Material Overlap Became Transparent Order](../upgrade/migration_api_cs.md#transparent_order). |
| *[**CreateShaderCache**( bool, bool )](../api/library/rendering/class.material_cs.md#createShaderCache_int_int_void)* | Set of arguments changed. |
| ***Overlap*** | Removed. Use *[**TransparentOrder**](../api/library/rendering/class.material_cs.md#TransparentOrder)* instead - see [Material Overlap Became Transparent Order](../upgrade/migration_api_cs.md#transparent_order). |
| ***TEXTURE_SOURCE_GBUFFER_MATERIAL_MASK*** | Renamed. Use *[**TEXTURE_SOURCE_GBUFFER_SURFACE_ID**](../api/library/rendering/class.material_cs.md#TEXTURE_SOURCE_GBUFFER_SURFACE_ID)* instead. |
| ***TEXTURE_SOURCE_REFLECTION_CUBE*** | Removed. |


#### New Functions


- *[**CreateShaderCache**( bool, bool )](../api/library/rendering/class.material_cs.md#createShaderCache_int_int_void)*
- *[**GetCustomParameterFloat**( int )](../api/library/rendering/class.material_cs.md#getCustomParameterFloat_int_float)*
- *[**GetCustomParameterFloat**( string )](../api/library/rendering/class.material_cs.md#getCustomParameterFloat_cstr_float)*
- *[**GetCustomParameterInt**( int )](../api/library/rendering/class.material_cs.md#getCustomParameterInt_int_int)*
- *[**GetCustomParameterInt**( string )](../api/library/rendering/class.material_cs.md#getCustomParameterInt_cstr_int)*
- *[**GetCustomParameterUInt**( int )](../api/library/rendering/class.material_cs.md#getCustomParameterUInt_int_uint)*
- *[**GetCustomParameterUInt**( string )](../api/library/rendering/class.material_cs.md#getCustomParameterUInt_cstr_uint)*
- *[**GetTexture**( int, float )](../api/library/rendering/class.material_cs.md#getTexture_int_float_Texture)*
- *[**IsCustomParameterOverridden**( int )](../api/library/rendering/class.material_cs.md#isCustomParameterOverridden_int_int)*
- *[**IsCustomParametersSupported**( )](../api/library/rendering/class.material_cs.md#isCustomParametersSupported_int)*
- *[**ResetCustomParameter**( int )](../api/library/rendering/class.material_cs.md#resetCustomParameter_int_void)*
- *[**ResetCustomParameters**( )](../api/library/rendering/class.material_cs.md#resetCustomParameters_void)*
- *[**SetCustomParameterFloat**( int, float )](../api/library/rendering/class.material_cs.md#setCustomParameterFloat_int_float_void)*
- *[**SetCustomParameterFloat**( string, float )](../api/library/rendering/class.material_cs.md#setCustomParameterFloat_cstr_float_void)*
- *[**SetCustomParameterInt**( int, int )](../api/library/rendering/class.material_cs.md#setCustomParameterInt_int_int_void)*
- *[**SetCustomParameterInt**( string, int )](../api/library/rendering/class.material_cs.md#setCustomParameterInt_cstr_int_void)*
- *[**SetCustomParameterUInt**( int, uint )](../api/library/rendering/class.material_cs.md#setCustomParameterUInt_int_uint_void)*
- *[**SetCustomParameterUInt**( string, uint )](../api/library/rendering/class.material_cs.md#setCustomParameterUInt_cstr_uint_void)*


#### New Properties


- *[**FeatureBits**](../api/library/rendering/class.material_cs.md#FeatureBits)*
- *[**MaterialID**](../api/library/rendering/class.material_cs.md#MaterialID)*
- *[**TransparentOrder**](../api/library/rendering/class.material_cs.md#TransparentOrder)*


#### New Enums


- *[**OPTION_TRANSPARENT_ORDER**](../api/library/rendering/class.material_cs.md#OPTION_TRANSPARENT_ORDER)*
- *[**TEXTURE_SOURCE_GBUFFER_REACTIVE_MASK**](../api/library/rendering/class.material_cs.md#TEXTURE_SOURCE_GBUFFER_REACTIVE_MASK)*
- *[**TRANSPARENT_ORDER**](../api/library/rendering/class.material_cs.md#TRANSPARENT_ORDER)*
- *[**TEXTURE_SOURCE_GBUFFER_SURFACE_ID**](../api/library/rendering/class.material_cs.md#TEXTURE_SOURCE_GBUFFER_SURFACE_ID)*
- *[**TEXTURE_SOURCE_LINEAR_DEPTH_OLD**](../api/library/rendering/class.material_cs.md#TEXTURE_SOURCE_LINEAR_DEPTH_OLD)*
- *[**TEXTURE_SOURCE_MIXED_REALITY_BLEND_MASK_COLOR**](../api/library/rendering/class.material_cs.md#TEXTURE_SOURCE_MIXED_REALITY_BLEND_MASK_COLOR)*
- *[**TEXTURE_SOURCE_SURFACE_ID_DECAL**](../api/library/rendering/class.material_cs.md#TEXTURE_SOURCE_SURFACE_ID_DECAL)*
- *[**TEXTURE_SOURCE_SURFACE_ID_SCENE**](../api/library/rendering/class.material_cs.md#TEXTURE_SOURCE_SURFACE_ID_SCENE)*
- *[**TEXTURE_SOURCE_SURFACE_ID_TRANSPARENT**](../api/library/rendering/class.material_cs.md#TEXTURE_SOURCE_SURFACE_ID_TRANSPARENT)*
- *[**TEXTURE_SOURCE_VISUALIZER_QUAD_OVERDRAW**](../api/library/rendering/class.material_cs.md#TEXTURE_SOURCE_VISUALIZER_QUAD_OVERDRAW)*
- *[**TEXTURE_SOURCE_VISUALIZER_VERTEX_DENSITY**](../api/library/rendering/class.material_cs.md#TEXTURE_SOURCE_VISUALIZER_VERTEX_DENSITY)*
- *[**TEXTURE_SOURCE_WBUFFER_CAUSTICS**](../api/library/rendering/class.material_cs.md#TEXTURE_SOURCE_WBUFFER_CAUSTICS)*
- *[**MATERIAL_ID**](../api/library/rendering/class.material_cs.md#MATERIAL_ID)*


## Materials Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***CreateShaderCache**( )* | Removed. Use *[**CreateShaderCacheAsync**( )](../api/library/rendering/class.materials_cs.md#createShaderCacheAsync_void)* and *[**CreateShaderCacheForce**( )](../api/library/rendering/class.materials_cs.md#createShaderCacheForce_void)* instead. |


#### New Functions


- *[**CreateShaderCacheAsync**( )](../api/library/rendering/class.materials_cs.md#createShaderCacheAsync_void)*
- *[**CreateShaderCacheForce**( )](../api/library/rendering/class.materials_cs.md#createShaderCacheForce_void)*
- *[**GetMaterialFeatureBits**( uint )](../api/library/rendering/class.materials_cs.md#getMaterialFeatureBits_uint_uint)*
- *[**GetMaterialMask**( uint )](../api/library/rendering/class.materials_cs.md#getMaterialMask_uint_uint)*


#### New Properties


- *[**MaterialParameters**](../api/library/rendering/class.materials_cs.md#MaterialParameters)*


## Math Common Functions


#### New Functions


- *[**Logit**( float )](../api/library/math/cs/mathcommon_cs.md#Logit_float_float)*
- *[**Logit**( double )](../api/library/math/cs/mathcommon_cs.md#Logit_double_double)*
- *[**Sigmoid**( float )](../api/library/math/cs/mathcommon_cs.md#Sigmoid_float_float)*
- *[**Sigmoid**( double )](../api/library/math/cs/mathcommon_cs.md#Sigmoid_double_double)*


#### New Properties


- *[**LOG10_D**](../api/library/math/cs/mathcommon_cs.md#LOG10_D)*
- *[**LOG2_D**](../api/library/math/cs/mathcommon_cs.md#LOG2_D)*


## NavigationMesh Class


#### New Properties


- *[**BakeSettings**](../api/library/pathfinding/class.navigationmesh_cs.md#BakeSettings)*


## Node Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***TYPE.NODE_ANIMATION_PLAYBACK*** | Renamed. Use *[**TYPE.NODE_SEQUENCE_PLAYER**](../api/library/nodes/class.node_cs.md#NODE_SEQUENCE_PLAYER)* instead. |


#### New Properties


- *[**IsExperimentalNavigation**](../api/library/nodes/class.node_cs.md#IsExperimentalNavigation)*


#### New Enums


- *[**TYPE.EXPERIMENTAL_NAVIGATION_BEGIN**](../api/library/nodes/class.node_cs.md#EXPERIMENTAL_NAVIGATION_BEGIN)*
- *[**TYPE.EXPERIMENTAL_NAVIGATION_END**](../api/library/nodes/class.node_cs.md#EXPERIMENTAL_NAVIGATION_END)*
- *[**TYPE.EXPERIMENTAL_NAVIGATION_MESH**](../api/library/nodes/class.node_cs.md#EXPERIMENTAL_NAVIGATION_MESH)*
- *[**TYPE.EXPERIMENTAL_NAVIGATION_MESH_AREA_VOLUME**](../api/library/nodes/class.node_cs.md#EXPERIMENTAL_NAVIGATION_MESH_AREA_VOLUME)*
- *[**TYPE.EXPERIMENTAL_NAVIGATION_MESH_INVOKER**](../api/library/nodes/class.node_cs.md#EXPERIMENTAL_NAVIGATION_MESH_INVOKER)*
- *[**TYPE.NODE_SEQUENCE_PLAYER**](../api/library/nodes/class.node_cs.md#NODE_SEQUENCE_PLAYER)*


## NodeSkeletonPose Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***GetAnimScript**( )* | Removed. Use the *[**AnimScript**](../api/library/nodes/class.nodeskeletonpose_cs.md#AnimScript)* property instead. |


#### New Functions


- *[**GetLayerJointObjectTransform**( int, int )](../api/library/nodes/class.nodeskeletonpose_cs.md#getLayerJointObjectTransform_int_int_mat4)*
- *[**IsLayerAnimationStreaming**( int )](../api/library/nodes/class.nodeskeletonpose_cs.md#isLayerAnimationStreaming_int_int)*
- *[**RenderLayerIKChainDebug**( int, IKInfoChain, Mat4 )](../api/library/nodes/class.nodeskeletonpose_cs.md#renderLayerIKChainDebug_int_IKInfoChain_Mat4_void)*
- *[**RenderLayerJointConeAsymLimitDebug**( int, JointLimitInfoConeAsym, Mat4 )](../api/library/nodes/class.nodeskeletonpose_cs.md#renderLayerJointConeAsymLimitDebug_int_JointLimitInfoConeAsym_Mat4_void)*
- *[**RenderLayerJointConeAsymTwistLimitDebug**( int, JointLimitInfoConeAsymTwist, Mat4 )](../api/library/nodes/class.nodeskeletonpose_cs.md#renderLayerJointConeAsymTwistLimitDebug_int_JointLimitInfoConeAsymTwist_Mat4_void)*
- *[**RenderLayerJointConeLimitDebug**( int, JointLimitInfoCone, Mat4 )](../api/library/nodes/class.nodeskeletonpose_cs.md#renderLayerJointConeLimitDebug_int_JointLimitInfoCone_Mat4_void)*
- *[**RenderLayerJointConeTwistLimitDebug**( int, JointLimitInfoConeTwist, Mat4 )](../api/library/nodes/class.nodeskeletonpose_cs.md#renderLayerJointConeTwistLimitDebug_int_JointLimitInfoConeTwist_Mat4_void)*
- *[**RenderLayerJointHingeLimitDebug**( int, JointLimitInfoHinge, Mat4 )](../api/library/nodes/class.nodeskeletonpose_cs.md#renderLayerJointHingeLimitDebug_int_JointLimitInfoHinge_Mat4_void)*
- *[**RenderLayerJointHingeTwistLimitDebug**( int, JointLimitInfoHingeTwist, Mat4 )](../api/library/nodes/class.nodeskeletonpose_cs.md#renderLayerJointHingeTwistLimitDebug_int_JointLimitInfoHingeTwist_Mat4_void)*
- *[**RenderLayerJointLimitSetDebug**( int, JointLimitSetInfo, Mat4 )](../api/library/nodes/class.nodeskeletonpose_cs.md#renderLayerJointLimitSetDebug_int_JointLimitSetInfo_Mat4_void)*
- *[**RenderLayerJointTwistLimitDebug**( int, JointLimitInfoTwist, Mat4 )](../api/library/nodes/class.nodeskeletonpose_cs.md#renderLayerJointTwistLimitDebug_int_JointLimitInfoTwist_Mat4_void)*
- *[**RenderLayerLookAtChainDebug**( int, LookAtChainInfo, Mat4 )](../api/library/nodes/class.nodeskeletonpose_cs.md#renderLayerLookAtChainDebug_int_LookAtChainInfo_Mat4_void)*
- *[**RenderLayerLookAtDebug**( int, LookAtInfo, Mat4 )](../api/library/nodes/class.nodeskeletonpose_cs.md#renderLayerLookAtDebug_int_LookAtInfo_Mat4_void)*
- *[**RenderLayerTwoBoneIKDebug**( int, IKInfoTwoBone, Mat4 )](../api/library/nodes/class.nodeskeletonpose_cs.md#renderLayerTwoBoneIKDebug_int_IKInfoTwoBone_Mat4_void)*
- *[**SetLayerJointObjectTransform**( int, int, mat4 )](../api/library/nodes/class.nodeskeletonpose_cs.md#setLayerJointObjectTransform_int_int_mat4_void)*
- *[**SetLayerJointObjectTransformPreserveChildren**( int, int, mat4 )](../api/library/nodes/class.nodeskeletonpose_cs.md#setLayerJointObjectTransformPreserveChildren_int_int_mat4_void)*
- *[**SolveLayerIKChain**( int, IKInfoChain )](../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerIKChain_int_IKInfoChain_void)*
- *[**SolveLayerJointConeAsymLimit**( int, JointLimitInfoConeAsym )](../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerJointConeAsymLimit_int_JointLimitInfoConeAsym_void)*
- *[**SolveLayerJointConeAsymTwistLimit**( int, JointLimitInfoConeAsymTwist )](../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerJointConeAsymTwistLimit_int_JointLimitInfoConeAsymTwist_void)*
- *[**SolveLayerJointConeLimit**( int, JointLimitInfoCone )](../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerJointConeLimit_int_JointLimitInfoCone_void)*
- *[**SolveLayerJointConeTwistLimit**( int, JointLimitInfoConeTwist )](../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerJointConeTwistLimit_int_JointLimitInfoConeTwist_void)*
- *[**SolveLayerJointHingeLimit**( int, JointLimitInfoHinge )](../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerJointHingeLimit_int_JointLimitInfoHinge_void)*
- *[**SolveLayerJointHingeTwistLimit**( int, JointLimitInfoHingeTwist )](../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerJointHingeTwistLimit_int_JointLimitInfoHingeTwist_void)*
- *[**SolveLayerJointTwistLimit**( int, JointLimitInfoTwist )](../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerJointTwistLimit_int_JointLimitInfoTwist_void)*
- *[**SolveLayerLookAt**( int, LookAtInfo )](../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerLookAt_int_LookAtInfo_void)*
- *[**SolveLayerLookAtChain**( int, LookAtChainInfo )](../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerLookAtChain_int_LookAtChainInfo_void)*
- *[**SolveLayerTwoBoneIK**( int, IKInfoTwoBone )](../api/library/nodes/class.nodeskeletonpose_cs.md#solveLayerTwoBoneIK_int_IKInfoTwoBone_void)*


#### New Properties


- *[**AnimScript**](../api/library/nodes/class.nodeskeletonpose_cs.md#AnimScript)*


## ObjectCloudLayer Class


#### New Properties


- *[**CloudspaceTransform**](../api/library/objects/class.objectcloudlayer_cs.md#CloudspaceTransform)*


## ObjectMeshSkinned Class


#### New Functions


- *[**LoadAsyncRender**( )](../api/library/objects/class.objectmeshskinned_cs.md#loadAsyncRender_int)*
- *[**LoadForceRender**( )](../api/library/objects/class.objectmeshskinned_cs.md#loadForceRender_int)*


## ObjectMeshSkinnedLegacy Class


#### New Functions


- *[**IsLayerAnimationStreaming**( int )](../api/library/objects/class.objectmeshskinnedlegacy_cs.md#isLayerAnimationStreaming_int_int)*
- *[**LoadAsyncRender**( )](../api/library/objects/class.objectmeshskinnedlegacy_cs.md#loadAsyncRender_int)*
- *[**LoadForceRender**( )](../api/library/objects/class.objectmeshskinnedlegacy_cs.md#loadForceRender_int)*
- *[**ResetLayerToBindPose**( int )](../api/library/objects/class.objectmeshskinnedlegacy_cs.md#resetLayerToBindPose_int_void)*
- *[**ResetLayerToRestPose**( int )](../api/library/objects/class.objectmeshskinnedlegacy_cs.md#resetLayerToRestPose_int_void)*


## ObjectText Class


#### New Properties


- *[**TextDirection**](../api/library/objects/class.objecttext_cs.md#TextDirection)*


## Profiler Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| *[**SetValue**( string, string, float, float, float[], Profiler.COUNTER_VR_FLAG, bool )](../api/library/engine/class.profiler_cs.md#setValue_cstr_cstr_float_float_float_int_int_void)* | Set of arguments changed. |
| *[**SetValue**( string, string, int, int, float[], Profiler.COUNTER_VR_FLAG, bool )](../api/library/engine/class.profiler_cs.md#setValue_cstr_cstr_int_int_float_int_int_void)* | Set of arguments changed. |


#### New Functions


- *[**SetValue**( string, string, float, float, float[], Profiler.COUNTER_VR_FLAG, bool )](../api/library/engine/class.profiler_cs.md#setValue_cstr_cstr_float_float_float_int_int_void)*
- *[**SetValue**( string, string, int, int, float[], Profiler.COUNTER_VR_FLAG, bool )](../api/library/engine/class.profiler_cs.md#setValue_cstr_cstr_int_int_float_int_int_void)*


#### New Enums


- *[**COUNTER_VR_FLAG**](../api/library/engine/class.profiler_cs.md#COUNTER_VR_FLAG)*


## Property Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***FileGUID*** | Read-only now. Use *[**SetFileGUID**](../api/library/common/class.property_cs.md#setFileGUID_UGUID_int)* and check the result. |
| ***FilePath*** | Read-only now. Use *[**SetFilePath**](../api/library/common/class.property_cs.md#setFilePath_cstr_int)* and check the result. |


#### New Functions


- *[**SetFileGUID**( UGUID )](../api/library/common/class.property_cs.md#setFileGUID_UGUID_int)*
- *[**SetFilePath**( string )](../api/library/common/class.property_cs.md#setFilePath_cstr_int)*


#### New Enums


- *[**PARAMETER_MASK_EXPERIMENTAL_NAVIGATION_BAKE**](../api/library/common/class.property_cs.md#PARAMETER_MASK_EXPERIMENTAL_NAVIGATION_BAKE)*


## Render Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| *[**AddParameter**( string, Render.RENDER_PARAMETER, bool, UGUID )](../api/library/rendering/class.render_cs.md#addParameter_cstr_int_int_UGUID_int)* | Set of arguments changed. |


#### New Functions


- *[**AddParameter**( string, Render.RENDER_PARAMETER, bool, UGUID )](../api/library/rendering/class.render_cs.md#addParameter_cstr_int_int_UGUID_int)*
- *[**CalculateEngineRenderResolution**( int, int, ivec2, out ivec2, out ivec2, out ivec2 )](../api/library/rendering/class.render_cs.md#calculateEngineRenderResolution_int_int_ivec2_ivec2_ivec2_ivec2_void)*
- *[**CloneParameter**( int )](../api/library/rendering/class.render_cs.md#cloneParameter_int_int)*
- *[**FindParameter**( string )](../api/library/rendering/class.render_cs.md#findParameter_cstr_int)*
- *[**GetParameterBool**( int )](../api/library/rendering/class.render_cs.md#getParameterBool_int_int)*
- *[**GetParameterBool**( string )](../api/library/rendering/class.render_cs.md#getParameterBool_cstr_int)*
- *[**GetParameterDefineName**( int )](../api/library/rendering/class.render_cs.md#getParameterDefineName_int_cstr)*
- *[**GetParameterFloat**( int )](../api/library/rendering/class.render_cs.md#getParameterFloat_int_float)*
- *[**GetParameterFloat**( string )](../api/library/rendering/class.render_cs.md#getParameterFloat_cstr_float)*
- *[**GetParameterFloat2**( int )](../api/library/rendering/class.render_cs.md#getParameterFloat2_int_vec2)*
- *[**GetParameterFloat2**( string )](../api/library/rendering/class.render_cs.md#getParameterFloat2_cstr_vec2)*
- *[**GetParameterFloat3**( int )](../api/library/rendering/class.render_cs.md#getParameterFloat3_int_vec3)*
- *[**GetParameterFloat3**( string )](../api/library/rendering/class.render_cs.md#getParameterFloat3_cstr_vec3)*
- *[**GetParameterFloat4**( int )](../api/library/rendering/class.render_cs.md#getParameterFloat4_int_vec4)*
- *[**GetParameterFloat4**( string )](../api/library/rendering/class.render_cs.md#getParameterFloat4_cstr_vec4)*
- *[**GetParameterGUID**( int )](../api/library/rendering/class.render_cs.md#getParameterGUID_int_UGUID)*
- *[**GetParameterInt**( int )](../api/library/rendering/class.render_cs.md#getParameterInt_int_int)*
- *[**GetParameterInt**( string )](../api/library/rendering/class.render_cs.md#getParameterInt_cstr_int)*
- *[**GetParameterInt2**( int )](../api/library/rendering/class.render_cs.md#getParameterInt2_int_ivec2)*
- *[**GetParameterInt2**( string )](../api/library/rendering/class.render_cs.md#getParameterInt2_cstr_ivec2)*
- *[**GetParameterInt3**( int )](../api/library/rendering/class.render_cs.md#getParameterInt3_int_ivec3)*
- *[**GetParameterInt3**( string )](../api/library/rendering/class.render_cs.md#getParameterInt3_cstr_ivec3)*
- *[**GetParameterInt4**( int )](../api/library/rendering/class.render_cs.md#getParameterInt4_int_ivec4)*
- *[**GetParameterInt4**( string )](../api/library/rendering/class.render_cs.md#getParameterInt4_cstr_ivec4)*
- *[**GetParameterName**( int )](../api/library/rendering/class.render_cs.md#getParameterName_int_cstr)*
- *[**GetParameterShaderName**( int )](../api/library/rendering/class.render_cs.md#getParameterShaderName_int_cstr)*
- *[**GetParameterType**( int )](../api/library/rendering/class.render_cs.md#getParameterType_int_int)*
- *[**GetStreamingAnimationHoldCount**( string )](../api/library/rendering/class.render_cs.md#getStreamingAnimationHoldCount_cstr_int)*
- *[**GetStreamingAnimationHoldCount**( UGUID )](../api/library/rendering/class.render_cs.md#getStreamingAnimationHoldCount_UGUID_int)*
- *[**HoldStreamingAnimation**( string )](../api/library/rendering/class.render_cs.md#holdStreamingAnimation_cstr_int)*
- *[**HoldStreamingAnimation**( UGUID )](../api/library/rendering/class.render_cs.md#holdStreamingAnimation_UGUID_int)*
- *[**IsParameterDynamic**( int )](../api/library/rendering/class.render_cs.md#isParameterDynamic_int_int)*
- *[**IsParameterFloat**( int )](../api/library/rendering/class.render_cs.md#isParameterFloat_int_int)*
- *[**IsStreamingAnimationExist**( string )](../api/library/rendering/class.render_cs.md#isStreamingAnimationExist_cstr_int)*
- *[**IsStreamingAnimationExist**( UGUID )](../api/library/rendering/class.render_cs.md#isStreamingAnimationExist_UGUID_int)*
- *[**IsStreamingAnimationHeld**( string )](../api/library/rendering/class.render_cs.md#isStreamingAnimationHeld_cstr_int)*
- *[**IsStreamingAnimationHeld**( UGUID )](../api/library/rendering/class.render_cs.md#isStreamingAnimationHeld_UGUID_int)*
- *[**IsStreamingAnimationLoaded**( string )](../api/library/rendering/class.render_cs.md#isStreamingAnimationLoaded_cstr_int)*
- *[**IsStreamingAnimationLoaded**( UGUID )](../api/library/rendering/class.render_cs.md#isStreamingAnimationLoaded_UGUID_int)*
- *[**IsValidSurfaceMaterialParameterName**( string )](../api/library/rendering/class.render_cs.md#isValidSurfaceMaterialParameterName_cstr_int)*
- *[**LoadStreamingAnimationAsync**( string )](../api/library/rendering/class.render_cs.md#loadStreamingAnimationAsync_cstr_ConstMeshSkinnedAnimation)*
- *[**LoadStreamingAnimationAsync**( UGUID )](../api/library/rendering/class.render_cs.md#loadStreamingAnimationAsync_UGUID_ConstMeshSkinnedAnimation)*
- *[**LoadStreamingAnimationForce**( string )](../api/library/rendering/class.render_cs.md#loadStreamingAnimationForce_cstr_ConstMeshSkinnedAnimation)*
- *[**LoadStreamingAnimationForce**( UGUID )](../api/library/rendering/class.render_cs.md#loadStreamingAnimationForce_UGUID_ConstMeshSkinnedAnimation)*
- *[**MoveParameter**( int, int )](../api/library/rendering/class.render_cs.md#moveParameter_int_int_void)*
- *[**GetNumParameters**( )](../api/library/rendering/class.render_cs.md#getNumParameters_int)*
- *[**RemoveParameter**( int )](../api/library/rendering/class.render_cs.md#removeParameter_int_void)*
- *[RENDER_DYNAMIC_RESOLUTION_DIMENSION.HORIZONTAL](../api/library/rendering/class.render_cs.md#RENDER_DYNAMIC_RESOLUTION_DIMENSION_HORIZONTAL)*
- *[RENDER_DYNAMIC_RESOLUTION_DIMENSION.UNIFORM](../api/library/rendering/class.render_cs.md#RENDER_DYNAMIC_RESOLUTION_DIMENSION_UNIFORM)*
- *[RENDER_DYNAMIC_RESOLUTION_DIMENSION.VERTICAL](../api/library/rendering/class.render_cs.md#RENDER_DYNAMIC_RESOLUTION_DIMENSION_VERTICAL)*
- *[RENDER_PARAMETER.BOOL](../api/library/rendering/class.render_cs.md#RENDER_PARAMETER_BOOL)*
- *[RENDER_PARAMETER.FLOAT](../api/library/rendering/class.render_cs.md#RENDER_PARAMETER_FLOAT)*
- *[RENDER_PARAMETER.FLOAT2](../api/library/rendering/class.render_cs.md#RENDER_PARAMETER_FLOAT2)*
- *[RENDER_PARAMETER.FLOAT3](../api/library/rendering/class.render_cs.md#RENDER_PARAMETER_FLOAT3)*
- *[RENDER_PARAMETER.FLOAT4](../api/library/rendering/class.render_cs.md#RENDER_PARAMETER_FLOAT4)*
- *[RENDER_PARAMETER.INT](../api/library/rendering/class.render_cs.md#RENDER_PARAMETER_INT)*
- *[RENDER_PARAMETER.INT2](../api/library/rendering/class.render_cs.md#RENDER_PARAMETER_INT2)*
- *[RENDER_PARAMETER.INT3](../api/library/rendering/class.render_cs.md#RENDER_PARAMETER_INT3)*
- *[RENDER_PARAMETER.INT4](../api/library/rendering/class.render_cs.md#RENDER_PARAMETER_INT4)*
- *[**ResetStreamingAnimationHold**( string )](../api/library/rendering/class.render_cs.md#resetStreamingAnimationHold_cstr_void)*
- *[**ResetStreamingAnimationHold**( UGUID )](../api/library/rendering/class.render_cs.md#resetStreamingAnimationHold_UGUID_void)*
- *[**SetParameterBool**( int, bool )](../api/library/rendering/class.render_cs.md#setParameterBool_int_int_void)*
- *[**SetParameterBool**( string, bool )](../api/library/rendering/class.render_cs.md#setParameterBool_cstr_int_void)*
- *[**SetParameterDynamic**( int, bool )](../api/library/rendering/class.render_cs.md#setParameterDynamic_int_int_void)*
- *[**SetParameterFloat**( int, float )](../api/library/rendering/class.render_cs.md#setParameterFloat_int_float_void)*
- *[**SetParameterFloat**( string, float )](../api/library/rendering/class.render_cs.md#setParameterFloat_cstr_float_void)*
- *[**SetParameterFloat2**( int, vec2 )](../api/library/rendering/class.render_cs.md#setParameterFloat2_int_vec2_void)*
- *[**SetParameterFloat2**( string, vec2 )](../api/library/rendering/class.render_cs.md#setParameterFloat2_cstr_vec2_void)*
- *[**SetParameterFloat3**( int, vec3 )](../api/library/rendering/class.render_cs.md#setParameterFloat3_int_vec3_void)*
- *[**SetParameterFloat3**( string, vec3 )](../api/library/rendering/class.render_cs.md#setParameterFloat3_cstr_vec3_void)*
- *[**SetParameterFloat4**( int, vec4 )](../api/library/rendering/class.render_cs.md#setParameterFloat4_int_vec4_void)*
- *[**SetParameterFloat4**( string, vec4 )](../api/library/rendering/class.render_cs.md#setParameterFloat4_cstr_vec4_void)*
- *[**SetParameterInt**( int, int )](../api/library/rendering/class.render_cs.md#setParameterInt_int_int_void)*
- *[**SetParameterInt**( string, int )](../api/library/rendering/class.render_cs.md#setParameterInt_cstr_int_void)*
- *[**SetParameterInt2**( int, ivec2 )](../api/library/rendering/class.render_cs.md#setParameterInt2_int_ivec2_void)*
- *[**SetParameterInt2**( string, ivec2 )](../api/library/rendering/class.render_cs.md#setParameterInt2_cstr_ivec2_void)*
- *[**SetParameterInt3**( int, ivec3 )](../api/library/rendering/class.render_cs.md#setParameterInt3_int_ivec3_void)*
- *[**SetParameterInt3**( string, ivec3 )](../api/library/rendering/class.render_cs.md#setParameterInt3_cstr_ivec3_void)*
- *[**SetParameterInt4**( int, ivec4 )](../api/library/rendering/class.render_cs.md#setParameterInt4_int_ivec4_void)*
- *[**SetParameterInt4**( string, ivec4 )](../api/library/rendering/class.render_cs.md#setParameterInt4_cstr_ivec4_void)*
- *[**SetParameterName**( int, string )](../api/library/rendering/class.render_cs.md#setParameterName_int_cstr_void)*
- *[**SetParameterType**( int, Render.RENDER_PARAMETER )](../api/library/rendering/class.render_cs.md#setParameterType_int_int_void)*
- *[**SwapParameters**( int, int )](../api/library/rendering/class.render_cs.md#swapParameters_int_int_void)*
- *[**UnholdStreamingAnimation**( string )](../api/library/rendering/class.render_cs.md#unholdStreamingAnimation_cstr_int)*
- *[**UnholdStreamingAnimation**( UGUID )](../api/library/rendering/class.render_cs.md#unholdStreamingAnimation_UGUID_int)*
- *[VIEWPORT_MODE.PANORAMA_FISHEYE_KANNALA_BRANDT](../api/library/rendering/class.render_cs.md#VIEWPORT_MODE_PANORAMA_FISHEYE_KANNALA_BRANDT)*


#### New Properties


- *[**DOFJitterSamples**](../api/library/rendering/class.render_cs.md#DOFJitterSamples)*
- *[**DOFMipmapByBlurIntensity**](../api/library/rendering/class.render_cs.md#DOFMipmapByBlurIntensity)*
- *[**DOFSamplingMode**](../api/library/rendering/class.render_cs.md#DOFSamplingMode)*
- *[**DOFTAAFrameCount**](../api/library/rendering/class.render_cs.md#DOFTAAFrameCount)*
- *[**DOFTAAFramesVelocityThreshold**](../api/library/rendering/class.render_cs.md#DOFTAAFramesVelocityThreshold)*
- *[**DynamicResolutionAlignmentEnabled**](../api/library/rendering/class.render_cs.md#DynamicResolutionAlignmentEnabled)*
- *[**DynamicResolutionCooldownFrames**](../api/library/rendering/class.render_cs.md#DynamicResolutionCooldownFrames)*
- *[**DynamicResolutionDimension**](../api/library/rendering/class.render_cs.md#DynamicResolutionDimension)*
- *[**DynamicResolutionDownFrames**](../api/library/rendering/class.render_cs.md#DynamicResolutionDownFrames)*
- *[**DynamicResolutionDownThreshold**](../api/library/rendering/class.render_cs.md#DynamicResolutionDownThreshold)*
- *[**DynamicResolutionEnabled**](../api/library/rendering/class.render_cs.md#DynamicResolutionEnabled)*
- *[**DynamicResolutionScaleMax**](../api/library/rendering/class.render_cs.md#DynamicResolutionScaleMax)*
- *[**DynamicResolutionScaleMin**](../api/library/rendering/class.render_cs.md#DynamicResolutionScaleMin)*
- *[**DynamicResolutionStep**](../api/library/rendering/class.render_cs.md#DynamicResolutionStep)*
- *[**DynamicResolutionTargetFPS**](../api/library/rendering/class.render_cs.md#DynamicResolutionTargetFPS)*
- *[**DynamicResolutionUpFrames**](../api/library/rendering/class.render_cs.md#DynamicResolutionUpFrames)*
- *[**DynamicResolutionUpThreshold**](../api/library/rendering/class.render_cs.md#DynamicResolutionUpThreshold)*
- *[**DynamicResolutionWarmupFrames**](../api/library/rendering/class.render_cs.md#DynamicResolutionWarmupFrames)*
- *[**EnvironmentMoonAngularSize**](../api/library/rendering/class.render_cs.md#EnvironmentMoonAngularSize)*
- *[**EnvironmentSunAngularSize**](../api/library/rendering/class.render_cs.md#EnvironmentSunAngularSize)*
- *[**EventChangedParameters**](../api/library/rendering/class.render_cs.md#EventChangedParameters)*
- *[**EventStreamingAnimationLoaded**](../api/library/rendering/class.render_cs.md#EventStreamingAnimationLoaded)*
- *[**EventStreamingAnimationUnloaded**](../api/library/rendering/class.render_cs.md#EventStreamingAnimationUnloaded)*
- *[**IndirectSpecularTemporalFilteringAngleDependence**](../api/library/rendering/class.render_cs.md#IndirectSpecularTemporalFilteringAngleDependence)*
- *[**IndirectSpecularTemporalFilteringColorClampingGrazing**](../api/library/rendering/class.render_cs.md#IndirectSpecularTemporalFilteringColorClampingGrazing)*
- *[**IndirectSpecularTemporalFilteringFrameCountGrazing**](../api/library/rendering/class.render_cs.md#IndirectSpecularTemporalFilteringFrameCountGrazing)*
- *[**LocalTonemapperDetailContrastIntensity**](../api/library/rendering/class.render_cs.md#LocalTonemapperDetailContrastIntensity)*
- *[**LocalTonemapperDetailContrastRadius**](../api/library/rendering/class.render_cs.md#LocalTonemapperDetailContrastRadius)*
- *[**LocalTonemapperUseDetailContrast**](../api/library/rendering/class.render_cs.md#LocalTonemapperUseDetailContrast)*
- *[**NumParameters**](../api/library/rendering/class.render_cs.md#NumParameters)*
- *[**PanoramaFisheyeKannalaBrandtChromaticAberration**](../api/library/rendering/class.render_cs.md#PanoramaFisheyeKannalaBrandtChromaticAberration)*
- *[**PanoramaFisheyeKannalaBrandtCoefficients**](../api/library/rendering/class.render_cs.md#PanoramaFisheyeKannalaBrandtCoefficients)*
- *[**PanoramaFisheyeKannalaBrandtFocalLength**](../api/library/rendering/class.render_cs.md#PanoramaFisheyeKannalaBrandtFocalLength)*
- *[**PanoramaFisheyeKannalaBrandtImageCircleRadius**](../api/library/rendering/class.render_cs.md#PanoramaFisheyeKannalaBrandtImageCircleRadius)*
- *[**PanoramaFisheyeKannalaBrandtImageDimensions**](../api/library/rendering/class.render_cs.md#PanoramaFisheyeKannalaBrandtImageDimensions)*
- *[**PanoramaFisheyeKannalaBrandtPrincipalPoint**](../api/library/rendering/class.render_cs.md#PanoramaFisheyeKannalaBrandtPrincipalPoint)*
- *[**PanoramaFisheyeKannalaBrandtSkew**](../api/library/rendering/class.render_cs.md#PanoramaFisheyeKannalaBrandtSkew)*
- *[**PanoramaFisheyeKannalaBrandtTangentialDistortion**](../api/library/rendering/class.render_cs.md#PanoramaFisheyeKannalaBrandtTangentialDistortion)*
- *[**PanoramaFisheyeKannalaBrandtVignettingCoefficient5**](../api/library/rendering/class.render_cs.md#PanoramaFisheyeKannalaBrandtVignettingCoefficient5)*
- *[**PanoramaFisheyeKannalaBrandtVignettingCoefficients**](../api/library/rendering/class.render_cs.md#PanoramaFisheyeKannalaBrandtVignettingCoefficients)*
- *[**PanoramaForceDisableScreenSpaceEffects**](../api/library/rendering/class.render_cs.md#PanoramaForceDisableScreenSpaceEffects)*
- *[**SkyOffset**](../api/library/rendering/class.render_cs.md#SkyOffset)*
- *[**StreamingAnimationCacheRAM**](../api/library/rendering/class.render_cs.md#StreamingAnimationCacheRAM)*
- *[**StreamingAnimationsMode**](../api/library/rendering/class.render_cs.md#StreamingAnimationsMode)*
- *[**StreamingMeshCacheRAM**](../api/library/rendering/class.render_cs.md#StreamingMeshCacheRAM)*
- *[**StreamingMeshCacheVRAM**](../api/library/rendering/class.render_cs.md#StreamingMeshCacheVRAM)*
- *[**StreamingMeshSkinnedCacheRAM**](../api/library/rendering/class.render_cs.md#StreamingMeshSkinnedCacheRAM)*
- *[**StreamingMeshSkinnedCacheVRAM**](../api/library/rendering/class.render_cs.md#StreamingMeshSkinnedCacheVRAM)*
- *[**StreamingTextureCacheVRAM**](../api/library/rendering/class.render_cs.md#StreamingTextureCacheVRAM)*
- *[**SurfaceIDMultilayered**](../api/library/rendering/class.render_cs.md#SurfaceIDMultilayered)*
- *[**SurfaceParameters**](../api/library/rendering/class.render_cs.md#SurfaceParameters)*
- *[**WaterGeometryProgressionFovMin**](../api/library/rendering/class.render_cs.md#WaterGeometryProgressionFovMin)*
- *[**WaterGeometryProgressionFovScale**](../api/library/rendering/class.render_cs.md#WaterGeometryProgressionFovScale)*


#### New Enums


- *[**VIEWPORT_MODE.PANORAMA_FISHEYE_KANNALA_BRANDT**](../api/library/rendering/class.render_cs.md#VIEWPORT_MODE_PANORAMA_FISHEYE_KANNALA_BRANDT)*
- *[**DOF_SAMPLING_MODE**](../api/library/rendering/class.render_cs.md#DOF_SAMPLING_MODE)*
- *[**RENDER_DYNAMIC_RESOLUTION_DIMENSION**](../api/library/rendering/class.render_cs.md#RENDER_DYNAMIC_RESOLUTION_DIMENSION)*
- *[**SURFACE_ID**](../api/library/rendering/class.render_cs.md#SURFACE_ID)*


## RenderEnvironmentPreset Class


#### New Properties


- *[**HazePhysicalVisibilityThreshold**](../api/library/rendering/class.renderenvironmentpreset_cs.md#HazePhysicalVisibilityThreshold)*


## Renderer Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***TextureGBufferMaterialMask*** | Renamed. Use *[**TextureGBufferSurfaceID**](../api/library/rendering/class.renderer_cs.md#TextureGBufferSurfaceID)* instead. |


#### New Functions


- *[**UseReactiveMask**( )](../api/library/rendering/class.renderer_cs.md#useReactiveMask_int)*


#### New Properties


- *[**OutputResolution**](../api/library/rendering/class.renderer_cs.md#OutputResolution)*
- *[**RenderResolution**](../api/library/rendering/class.renderer_cs.md#RenderResolution)*
- *[**RenderResolutionMax**](../api/library/rendering/class.renderer_cs.md#RenderResolutionMax)*
- *[**RenderResolutionMin**](../api/library/rendering/class.renderer_cs.md#RenderResolutionMin)*
- *[**TextureGBufferReactiveMask**](../api/library/rendering/class.renderer_cs.md#TextureGBufferReactiveMask)*
- *[**TextureGBufferSurfaceID**](../api/library/rendering/class.renderer_cs.md#TextureGBufferSurfaceID)*
- *[**TextureSurfaceIDDecal**](../api/library/rendering/class.renderer_cs.md#TextureSurfaceIDDecal)*
- *[**TextureSurfaceIDScene**](../api/library/rendering/class.renderer_cs.md#TextureSurfaceIDScene)*
- *[**TextureSurfaceIDTransparent**](../api/library/rendering/class.renderer_cs.md#TextureSurfaceIDTransparent)*
- *[**TextureSurfaceIDWater**](../api/library/rendering/class.renderer_cs.md#TextureSurfaceIDWater)*


## SkeletonRetargeter Class


#### New Properties


- *[**FirstFileGUID**](../api/library/animations/skeletal/class.skeletonretargeter_cs.md#FirstFileGUID)*
- *[**SecondFileGUID**](../api/library/animations/skeletal/class.skeletonretargeter_cs.md#SecondFileGUID)*


## SoundSource Class


#### New Properties


- *[**PitchShift**](../api/library/sounds/class.soundsource_cs.md#PitchShift)*


## Sounds Class


#### New Functions


- *[**GetSampleWaveform**( string, int, float[] )](../api/library/engine/class.sounds_cs.md#getSampleWaveform_cstr_int_VECfloat_float)*


## SpiderVision::DebugData Class


#### New Properties


- *[**DebugStereo**](../api/library/plugins/spidervision/class.debugdata_cs.md#DebugStereo)*


## SpiderVision::DisplaysConfig Class


#### New Properties


- *[**HeadPosition**](../api/library/plugins/spidervision/class.displaysconfig_cs.md#HeadPosition)*
- *[**HeadRotation**](../api/library/plugins/spidervision/class.displaysconfig_cs.md#HeadRotation)*


## SpiderVision::GroupData Class


#### New Functions


- *[**Copy**( GroupData )](../api/library/plugins/spidervision/class.groupdata_cs.md#copy_GroupData_void)*
- *[**Generate**( )](../api/library/plugins/spidervision/class.groupdata_cs.md#generate_void)*
- *[**Refresh**( )](../api/library/plugins/spidervision/class.groupdata_cs.md#refresh_void)*


#### New Enums


- *[**GROUP_TYPE.CAVE**](../api/library/plugins/spidervision/class.groupdata_cs.md#CAVE)*


## SpiderVision::Manager Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***SetGroupViewOffset**( int, Vec3 )* | Removed. |
| ***SetViewportViewOffset**( int, Vec3 )* | Removed. |
| ***Enabled*** | Removed. |


#### New Functions


- *[**GetViewportCustomPlayer**( int )](../api/library/plugins/spidervision/class.spidervision_manager_cs.md#getViewportCustomPlayer_int_Player)*


## SpiderVision::ViewportData Class


#### New Properties


- *[**PixelDensity**](../api/library/plugins/spidervision/class.viewportdata_cs.md#PixelDensity)*
- *[**RenderMode**](../api/library/plugins/spidervision/class.viewportdata_cs.md#RenderMode)*
- *[**SwapEyesInStereoMode**](../api/library/plugins/spidervision/class.viewportdata_cs.md#SwapEyesInStereoMode)*


#### New Enums


- *[**RENDER_MODE**](../api/library/plugins/spidervision/class.viewportdata_cs.md#RENDER_MODE)*


## SpiderVision::WallGroupData Class


#### New Properties


- *[**PixelDensity**](../api/library/plugins/spidervision/class.wallgroupdata_cs.md#PixelDensity)*


## TerrainDetailMask Class


#### New Properties


- *[**ExperimentalNavigation**](../api/library/objects/landscape_terrain/class.terraindetailmask_cs.md#ExperimentalNavigation)*
- *[**ExperimentalNavigationArea**](../api/library/objects/landscape_terrain/class.terraindetailmask_cs.md#ExperimentalNavigationArea)*
- *[**ExperimentalNavigationBakeMask**](../api/library/objects/landscape_terrain/class.terraindetailmask_cs.md#ExperimentalNavigationBakeMask)*
- *[**ExperimentalNavigationMinValue**](../api/library/objects/landscape_terrain/class.terraindetailmask_cs.md#ExperimentalNavigationMinValue)*


## Texture Class


#### New Enums


- *[**FORMAT_MAPPING_MASK**](../api/library/rendering/class.texture_cs.md#FORMAT_MAPPING_MASK)*


## VR Class


#### New Properties


- *[**EmulationMirrorCrop**](../api/library/vr/class.vr_cs.md#EmulationMirrorCrop)*
- *[**EmulationMirrorCropOffset**](../api/library/vr/class.vr_cs.md#EmulationMirrorCropOffset)*
- *[**EmulationMirrorMode**](../api/library/vr/class.vr_cs.md#EmulationMirrorMode)*
- *[**FoveatedMode**](../api/library/vr/class.vr_cs.md#FoveatedMode)*
- *[**MirrorCrop**](../api/library/vr/class.vr_cs.md#MirrorCrop)*
- *[**MirrorCropOffset**](../api/library/vr/class.vr_cs.md#MirrorCropOffset)*
- *[**PeripheralRenderingDebugGazeOverrideCoord**](../api/library/vr/class.vr_cs.md#PeripheralRenderingDebugGazeOverrideCoord)*
- *[**PeripheralRenderingDebugGazeOverrideMode**](../api/library/vr/class.vr_cs.md#PeripheralRenderingDebugGazeOverrideMode)*
- *[**ProfilerBackgroundAlpha**](../api/library/vr/class.vr_cs.md#ProfilerBackgroundAlpha)*
- *[**ProfilerPosition**](../api/library/vr/class.vr_cs.md#ProfilerPosition)*
- *[**ShowProfiler**](../api/library/vr/class.vr_cs.md#ShowProfiler)*
- *[**ShowProfilerMemory**](../api/library/vr/class.vr_cs.md#ShowProfilerMemory)*
- *[**ShowProfilerMisc**](../api/library/vr/class.vr_cs.md#ShowProfilerMisc)*
- *[**ShowProfilerPerformance**](../api/library/vr/class.vr_cs.md#ShowProfilerPerformance)*


#### New Enums


- *[**FOVEATED_MODE**](../api/library/vr/class.vr_cs.md#FOVEATED_MODE)*
- *[**PERIPHERAL_RENDERING_DEBUG_GAZE_OVERRIDE_MODE**](../api/library/vr/class.vr_cs.md#PERIPHERAL_RENDERING_DEBUG_GAZE_OVERRIDE_MODE)*
- *[**PROFILER_POSITION**](../api/library/vr/class.vr_cs.md#PROFILER_POSITION)*
- *[**SHOW_PROFILER**](../api/library/vr/class.vr_cs.md#SHOW_PROFILER)*


## Viewport Class


#### New Properties


- *[**PanoramaFisheyeKannalaBrandtChromaticAberration**](../api/library/rendering/class.viewport_cs.md#PanoramaFisheyeKannalaBrandtChromaticAberration)*
- *[**PanoramaFisheyeKannalaBrandtCoefficients**](../api/library/rendering/class.viewport_cs.md#PanoramaFisheyeKannalaBrandtCoefficients)*
- *[**PanoramaFisheyeKannalaBrandtFocalLength**](../api/library/rendering/class.viewport_cs.md#PanoramaFisheyeKannalaBrandtFocalLength)*
- *[**PanoramaFisheyeKannalaBrandtImageCircleRadius**](../api/library/rendering/class.viewport_cs.md#PanoramaFisheyeKannalaBrandtImageCircleRadius)*
- *[**PanoramaFisheyeKannalaBrandtImageDimensions**](../api/library/rendering/class.viewport_cs.md#PanoramaFisheyeKannalaBrandtImageDimensions)*
- *[**PanoramaFisheyeKannalaBrandtPrincipalPoint**](../api/library/rendering/class.viewport_cs.md#PanoramaFisheyeKannalaBrandtPrincipalPoint)*
- *[**PanoramaFisheyeKannalaBrandtSkew**](../api/library/rendering/class.viewport_cs.md#PanoramaFisheyeKannalaBrandtSkew)*
- *[**PanoramaFisheyeKannalaBrandtTangentialDistortion**](../api/library/rendering/class.viewport_cs.md#PanoramaFisheyeKannalaBrandtTangentialDistortion)*
- *[**PanoramaFisheyeKannalaBrandtVignettingCoefficient5**](../api/library/rendering/class.viewport_cs.md#PanoramaFisheyeKannalaBrandtVignettingCoefficient5)*
- *[**PanoramaFisheyeKannalaBrandtVignettingCoefficients**](../api/library/rendering/class.viewport_cs.md#PanoramaFisheyeKannalaBrandtVignettingCoefficients)*
- *[**PanoramaForceDisableScreenSpaceEffects**](../api/library/rendering/class.viewport_cs.md#PanoramaForceDisableScreenSpaceEffects)*


#### New Enums


- *[**SKIP_AUTO_EXPOSURE_ADAPTATION_TIME**](../api/library/rendering/class.viewport_cs.md#SKIP_AUTO_EXPOSURE_ADAPTATION_TIME)*
- *[**SKIP_AUTO_WHITE_BALANCE_ADAPTATION_TIME**](../api/library/rendering/class.viewport_cs.md#SKIP_AUTO_WHITE_BALANCE_ADAPTATION_TIME)*


## Visualizer Class


#### New Functions


- *[**ClearNodeTypeIcons**( )](../api/library/engine/class.visualizer_cs.md#clearNodeTypeIcons_void)*
- *[**SetNodeTypeIcon**( Node.TYPE, string )](../api/library/engine/class.visualizer_cs.md#setNodeTypeIcon_int_cstr_int)*


## Weather::Manager Class


#### New Properties


- *[**Planet**](../api/library/plugins/weather/class.weather_manager_cs.md#Planet)*


## Widget Class


#### New Properties


- *[**TextDirection**](../api/library/gui/class.widget_cs.md#TextDirection)*


## WidgetEditLine Class


#### New Properties


- *[**CursorMode**](../api/library/gui/class.widgeteditline_cs.md#CursorMode)*


## WidgetEditText Class


#### New Properties


- *[**CursorMode**](../api/library/gui/class.widgetedittext_cs.md#CursorMode)*


## WidgetTreeBox Class


#### New Functions


- *[**ClearIcons**( )](../api/library/gui/class.widgettreebox_cs.md#clearIcons_void)*
- *[**SetIcon**( int, string )](../api/library/gui/class.widgettreebox_cs.md#setIcon_int_cstr_int)*


## Decal Class


#### New Functions


- *[**GetSurfaceRenderCustomParameterFloat**( int )](../api/library/decals/class.decal_cs.md#getSurfaceRenderCustomParameterFloat_int_float)*
- *[**GetSurfaceRenderCustomParameterFloat**( string )](../api/library/decals/class.decal_cs.md#getSurfaceRenderCustomParameterFloat_cstr_float)*
- *[**GetSurfaceRenderCustomParameterInt**( int )](../api/library/decals/class.decal_cs.md#getSurfaceRenderCustomParameterInt_int_int)*
- *[**GetSurfaceRenderCustomParameterInt**( string )](../api/library/decals/class.decal_cs.md#getSurfaceRenderCustomParameterInt_cstr_int)*
- *[**GetSurfaceRenderCustomParameterUInt**( int )](../api/library/decals/class.decal_cs.md#getSurfaceRenderCustomParameterUInt_int_uint)*
- *[**GetSurfaceRenderCustomParameterUInt**( string )](../api/library/decals/class.decal_cs.md#getSurfaceRenderCustomParameterUInt_cstr_uint)*
- *[**IsSurfaceRenderCustomParameterOverridden**( int )](../api/library/decals/class.decal_cs.md#isSurfaceRenderCustomParameterOverridden_int_bool)*
- *[**ResetSurfaceRenderCustomParameter**( int )](../api/library/decals/class.decal_cs.md#resetSurfaceRenderCustomParameter_int_void)*
- *[**ResetSurfaceRenderCustomParameters**( )](../api/library/decals/class.decal_cs.md#resetSurfaceRenderCustomParameters_void)*
- *[**SetSurfaceRenderCustomParameterFloat**( int, float )](../api/library/decals/class.decal_cs.md#setSurfaceRenderCustomParameterFloat_int_float_void)*
- *[**SetSurfaceRenderCustomParameterFloat**( string, float )](../api/library/decals/class.decal_cs.md#setSurfaceRenderCustomParameterFloat_cstr_float_void)*
- *[**SetSurfaceRenderCustomParameterInt**( int, int )](../api/library/decals/class.decal_cs.md#setSurfaceRenderCustomParameterInt_int_int_void)*
- *[**SetSurfaceRenderCustomParameterInt**( string, int )](../api/library/decals/class.decal_cs.md#setSurfaceRenderCustomParameterInt_cstr_int_void)*
- *[**SetSurfaceRenderCustomParameterUInt**( int, uint )](../api/library/decals/class.decal_cs.md#setSurfaceRenderCustomParameterUInt_int_uint_void)*
- *[**SetSurfaceRenderCustomParameterUInt**( string, uint )](../api/library/decals/class.decal_cs.md#setSurfaceRenderCustomParameterUInt_cstr_uint_void)*


## LightProj Class


#### New Properties


- *[**UseEnvironmentColor**](../api/library/lights/class.lightproj_cs.md#UseEnvironmentColor)*


## Object Class


#### New Functions


- *[**GetExperimentalNavigation**( int )](../api/library/objects/class.object_cs.md#getExperimentalNavigation_int_int)*
- *[**GetExperimentalNavigationArea**( int )](../api/library/objects/class.object_cs.md#getExperimentalNavigationArea_int_int)*
- *[**GetExperimentalNavigationBakeMask**( int )](../api/library/objects/class.object_cs.md#getExperimentalNavigationBakeMask_int_int)*
- *[**GetSurfaceRenderCustomParameterFloat**( int, int )](../api/library/objects/class.object_cs.md#getSurfaceRenderCustomParameterFloat_int_int_float)*
- *[**GetSurfaceRenderCustomParameterFloat**( int, string )](../api/library/objects/class.object_cs.md#getSurfaceRenderCustomParameterFloat_int_cstr_float)*
- *[**GetSurfaceRenderCustomParameterInt**( int, int )](../api/library/objects/class.object_cs.md#getSurfaceRenderCustomParameterInt_int_int_int)*
- *[**GetSurfaceRenderCustomParameterInt**( int, string )](../api/library/objects/class.object_cs.md#getSurfaceRenderCustomParameterInt_int_cstr_int)*
- *[**GetSurfaceRenderCustomParameterUInt**( int, int )](../api/library/objects/class.object_cs.md#getSurfaceRenderCustomParameterUInt_int_int_uint)*
- *[**GetSurfaceRenderCustomParameterUInt**( int, string )](../api/library/objects/class.object_cs.md#getSurfaceRenderCustomParameterUInt_int_cstr_uint)*
- *[**IsSurfaceRenderCustomParameterOverridden**( int, int )](../api/library/objects/class.object_cs.md#isSurfaceRenderCustomParameterOverridden_int_int_bool)*
- *[**ResetSurfaceRenderCustomParameter**( int, int )](../api/library/objects/class.object_cs.md#resetSurfaceRenderCustomParameter_int_int_void)*
- *[**ResetSurfaceRenderCustomParameters**( int )](../api/library/objects/class.object_cs.md#resetSurfaceRenderCustomParameters_int_void)*
- *[**SetExperimentalNavigation**( bool, int )](../api/library/objects/class.object_cs.md#setExperimentalNavigation_int_int_void)*
- *[**SetExperimentalNavigationArea**( int, int )](../api/library/objects/class.object_cs.md#setExperimentalNavigationArea_int_int_void)*
- *[**SetExperimentalNavigationBakeMask**( int, int )](../api/library/objects/class.object_cs.md#setExperimentalNavigationBakeMask_int_int_void)*
- *[**SetSurfaceRenderCustomParameterFloat**( int, int, float )](../api/library/objects/class.object_cs.md#setSurfaceRenderCustomParameterFloat_int_int_float_void)*
- *[**SetSurfaceRenderCustomParameterFloat**( int, string, float )](../api/library/objects/class.object_cs.md#setSurfaceRenderCustomParameterFloat_int_cstr_float_void)*
- *[**SetSurfaceRenderCustomParameterInt**( int, int, int )](../api/library/objects/class.object_cs.md#setSurfaceRenderCustomParameterInt_int_int_int_void)*
- *[**SetSurfaceRenderCustomParameterInt**( int, string, int )](../api/library/objects/class.object_cs.md#setSurfaceRenderCustomParameterInt_int_cstr_int_void)*
- *[**SetSurfaceRenderCustomParameterUInt**( int, int, uint )](../api/library/objects/class.object_cs.md#setSurfaceRenderCustomParameterUInt_int_int_uint_void)*
- *[**SetSurfaceRenderCustomParameterUInt**( int, string, uint )](../api/library/objects/class.object_cs.md#setSurfaceRenderCustomParameterUInt_int_cstr_uint_void)*


## ObjectMeshCluster Class


#### New Functions


- *[**GetInstanceCustomParameterFloat**( int, int, int )](../api/library/objects/class.objectmeshcluster_cs.md#getInstanceCustomParameterFloat_int_int_int_float)*
- *[**GetInstanceCustomParameterFloat**( int, int, string )](../api/library/objects/class.objectmeshcluster_cs.md#getInstanceCustomParameterFloat_int_int_cstr_float)*
- *[**GetInstanceCustomParameterInt**( int, int, int )](../api/library/objects/class.objectmeshcluster_cs.md#getInstanceCustomParameterInt_int_int_int_int)*
- *[**GetInstanceCustomParameterInt**( int, int, string )](../api/library/objects/class.objectmeshcluster_cs.md#getInstanceCustomParameterInt_int_int_cstr_int)*
- *[**GetInstanceCustomParameterUInt**( int, int, int )](../api/library/objects/class.objectmeshcluster_cs.md#getInstanceCustomParameterUInt_int_int_int_uint)*
- *[**GetInstanceCustomParameterUInt**( int, int, string )](../api/library/objects/class.objectmeshcluster_cs.md#getInstanceCustomParameterUInt_int_int_cstr_uint)*
- *[**HasInstanceCustomParameters**( int, int )](../api/library/objects/class.objectmeshcluster_cs.md#hasInstanceCustomParameters_int_int_int)*
- *[**IsInstanceCustomParameterOverridden**( int, int, int )](../api/library/objects/class.objectmeshcluster_cs.md#isInstanceCustomParameterOverridden_int_int_int_bool)*
- *[**ResetInstanceCustomParameter**( int, int, int )](../api/library/objects/class.objectmeshcluster_cs.md#resetInstanceCustomParameter_int_int_int_void)*
- *[**ResetInstanceCustomParameters**( int, int )](../api/library/objects/class.objectmeshcluster_cs.md#resetInstanceCustomParameters_int_int_void)*
- *[**SetInstanceCustomParameterFloat**( int, int, int, float )](../api/library/objects/class.objectmeshcluster_cs.md#setInstanceCustomParameterFloat_int_int_int_float_void)*
- *[**SetInstanceCustomParameterFloat**( int, int, string, float )](../api/library/objects/class.objectmeshcluster_cs.md#setInstanceCustomParameterFloat_int_int_cstr_float_void)*
- *[**SetInstanceCustomParameterInt**( int, int, int, int )](../api/library/objects/class.objectmeshcluster_cs.md#setInstanceCustomParameterInt_int_int_int_int_void)*
- *[**SetInstanceCustomParameterInt**( int, int, string, int )](../api/library/objects/class.objectmeshcluster_cs.md#setInstanceCustomParameterInt_int_int_cstr_int_void)*
- *[**SetInstanceCustomParameterUInt**( int, int, int, uint )](../api/library/objects/class.objectmeshcluster_cs.md#setInstanceCustomParameterUInt_int_int_int_uint_void)*
- *[**SetInstanceCustomParameterUInt**( int, int, string, uint )](../api/library/objects/class.objectmeshcluster_cs.md#setInstanceCustomParameterUInt_int_int_cstr_uint_void)*


## ObjectWaterGlobal Class


#### New Properties


- *[**BackfaceMaterialID**](../api/library/objects/class.objectwaterglobal_cs.md#BackfaceMaterialID)*


## World Class


#### New Properties


- *[**ExperimentalNavigationSettings**](../api/library/engine/class.world_cs.md#ExperimentalNavigationSettings)*
