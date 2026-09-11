# API Migration (CPP)


## Major Changes


What changed at the level of whole classes: what was added, what was given a new name, what was replaced and what is gone. Changes inside a class are listed in the per-class chapters further down the page, and the ones that need explaining have a chapter of their own in [Breaking Changes](../upgrade/migration_api_cpp.md#breaking_changes).


### New Classes


- *[Geodetics::Anchor](../api/library/geodetics/geodetics_plugin/class.anchor_cpp.md)*
- *[AnimationBindComponent](../api/library/animations/timeline/class.animationbindcomponent_cpp.md)*
- *[AnimationChannelEvent](../api/library/animations/timeline/class.animationchannelevent_cpp.md)*
- *[AnimationChannelEventState](../api/library/animations/timeline/class.animationchanneleventstate_cpp.md)*
- *[AnimationChannelFollowPath](../api/library/animations/timeline/class.animationchannelfollowpath_cpp.md)*
- *[AnimationChannelSkeletonAnimation](../api/library/animations/timeline/class.animationchannelskeletonanimation_cpp.md)*
- *[AnimationChannelSound](../api/library/animations/timeline/class.animationchannelsound_cpp.md)*
- *[AnimationChannelSubSequence](../api/library/animations/timeline/class.animationchannelsubsequence_cpp.md)*
- *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)*
- *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)*
- *[SpiderVision::CAVEGroupData](../api/library/plugins/spidervision/class.cavegroupdata_cpp.md)*
- *[Cesium](../api/library/plugins/cesium/class.cesium_cpp.md)*
- *[CesiumConfig](../api/library/plugins/cesium/class.cesiumconfig_cpp.md)*
- *[CustomParameterLayout](../api/library/common/class.customparameterlayout_cpp.md)*
- *[ExperimentalBakeNavigation](../api/library/pathfinding/class.experimentalbakenavigation_cpp.md)*
- *[ExperimentalNavigation](../api/library/pathfinding/class.experimentalnavigation_cpp.md)*
- *[ExperimentalNavigationAvoidance](../api/library/pathfinding/class.experimentalnavigationavoidance_cpp.md)*
- *[ExperimentalNavigationBakeQuery](../api/library/pathfinding/class.experimentalnavigationbakequery_cpp.md)*
- *[ExperimentalNavigationBakeSettings](../api/library/pathfinding/class.experimentalnavigationbakesettings_cpp.md)*
- *[ExperimentalNavigationMesh](../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md)*
- *[ExperimentalNavigationMeshAreaVolume](../api/library/pathfinding/class.experimentalnavigationmeshareavolume_cpp.md)*
- *[ExperimentalNavigationMeshCorridor](../api/library/pathfinding/class.experimentalnavigationmeshcorridor_cpp.md)*
- *[ExperimentalNavigationMeshFilter](../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)*
- *[ExperimentalNavigationMeshInvoker](../api/library/pathfinding/class.experimentalnavigationmeshinvoker_cpp.md)*
- *[ExperimentalNavigationPath](../api/library/pathfinding/class.experimentalnavigationpath_cpp.md)*
- *[ExperimentalNavigationPathFetch](../api/library/pathfinding/class.experimentalnavigationpathfetch_cpp.md)*
- *[IKInfo](../api/library/animations/skeletal/class.ikinfo_cpp.md)*
- *[IKInfoChain](../api/library/animations/skeletal/class.ikinfochain_cpp.md)*
- *[IKInfoTwoBone](../api/library/animations/skeletal/class.ikinfotwobone_cpp.md)*
- *[InputEventPadAccelerometerMotion](../api/library/controls/class.inputeventpadaccelerometermotion_cpp.md)*
- *[InputEventPadGyroscopeMotion](../api/library/controls/class.inputeventpadgyroscopemotion_cpp.md)*
- *[InputEventTextEditing](../api/library/controls/class.inputeventtextediting_cpp.md)*
- *[JointLimitInfo](../api/library/animations/skeletal/class.jointlimitinfo_cpp.md)*
- *[JointLimitInfoCone](../api/library/animations/skeletal/class.jointlimitinfocone_cpp.md)*
- *[JointLimitInfoConeAsym](../api/library/animations/skeletal/class.jointlimitinfoconeasym_cpp.md)*
- *[JointLimitInfoConeAsymTwist](../api/library/animations/skeletal/class.jointlimitinfoconeasymtwist_cpp.md)*
- *[JointLimitInfoConeTwist](../api/library/animations/skeletal/class.jointlimitinfoconetwist_cpp.md)*
- *[JointLimitInfoHinge](../api/library/animations/skeletal/class.jointlimitinfohinge_cpp.md)*
- *[JointLimitInfoHingeTwist](../api/library/animations/skeletal/class.jointlimitinfohingetwist_cpp.md)*
- *[JointLimitInfoTwist](../api/library/animations/skeletal/class.jointlimitinfotwist_cpp.md)*
- *[JointLimitSetInfo](../api/library/animations/skeletal/class.jointlimitsetinfo_cpp.md)*
- *[LookAtChainInfo](../api/library/animations/skeletal/class.lookatchaininfo_cpp.md)*
- *[LookAtInfo](../api/library/animations/skeletal/class.lookatinfo_cpp.md)*
- *[Weather::Planet](../api/library/plugins/weather/class.planet_cpp.md)*
- *[RTSPStreamer](../api/library/plugins/rtspstreamer/class.rtspstreamer_cpp.md)*
- *[ScenarioManager::ScenarioManager](../api/library/plugins/scenariomanager/class.scenariomanager_cpp.md)*
- *AssetDependencyReplacement* (Editor API)
- *AssetDependencyReplacer* (Editor API)
- *FileDependencies* (Editor API)
- *FileDependencyWalker* (Editor API)
- *NodeFileDependencies* (Editor API)


### Renamed Classes


- The *NodeAnimationPlayback* node class has been renamed as *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cpp.md)*.
- The *AnimationModifier* class and its 23 typed subclasses have been renamed as *[AnimationChannel](../api/library/animations/timeline/class.animationchannel_cpp.md)* and its subclasses. The rename is mechanical - the *Modifier* part of the name became *Channel*, and nothing else about these classes changed except that **copy()** is now **assignFrom()**. <details> <summary>Complete list of renamed classes | close</summary> | UNIGINE 2.21 | UNIGINE 2.22 | |---|---| | *AnimationModifier* | *[AnimationChannel](../api/library/animations/timeline/class.animationchannel_cpp.md)* | | *AnimationModifierBones* | *[AnimationChannelBones](../api/library/animations/timeline/class.animationchannelbones_cpp.md)* | | *AnimationModifierBool* | *[AnimationChannelBool](../api/library/animations/timeline/class.animationchannelbool_cpp.md)* | | *AnimationModifierDVec2* | *[AnimationChannelDVec2](../api/library/animations/timeline/class.animationchanneldvec2_cpp.md)* | | *AnimationModifierDVec3* | *[AnimationChannelDVec3](../api/library/animations/timeline/class.animationchanneldvec3_cpp.md)* | | *AnimationModifierDVec4* | *[AnimationChannelDVec4](../api/library/animations/timeline/class.animationchanneldvec4_cpp.md)* | | *AnimationModifierDouble* | *[AnimationChannelDouble](../api/library/animations/timeline/class.animationchanneldouble_cpp.md)* | | *AnimationModifierFVec2* | *[AnimationChannelFVec2](../api/library/animations/timeline/class.animationchannelfvec2_cpp.md)* | | *AnimationModifierFVec3* | *[AnimationChannelFVec3](../api/library/animations/timeline/class.animationchannelfvec3_cpp.md)* | | *AnimationModifierFVec4* | *[AnimationChannelFVec4](../api/library/animations/timeline/class.animationchannelfvec4_cpp.md)* | | *AnimationModifierFloat* | *[AnimationChannelFloat](../api/library/animations/timeline/class.animationchannelfloat_cpp.md)* | | *AnimationModifierIVec2* | *[AnimationChannelIVec2](../api/library/animations/timeline/class.animationchannelivec2_cpp.md)* | | *AnimationModifierIVec3* | *[AnimationChannelIVec3](../api/library/animations/timeline/class.animationchannelivec3_cpp.md)* | | *AnimationModifierIVec4* | *[AnimationChannelIVec4](../api/library/animations/timeline/class.animationchannelivec4_cpp.md)* | | *AnimationModifierInfo* | *[AnimationChannelInfo](../api/library/animations/timeline/class.animationchannelinfo_cpp.md)* | | *AnimationModifierInt* | *[AnimationChannelInt](../api/library/animations/timeline/class.animationchannelint_cpp.md)* | | *AnimationModifierNode* | *[AnimationChannelNode](../api/library/animations/timeline/class.animationchannelnode_cpp.md)* | | *AnimationModifierQuat* | *[AnimationChannelQuat](../api/library/animations/timeline/class.animationchannelquat_cpp.md)* | | *AnimationModifierScalar* | *[AnimationChannelScalar](../api/library/animations/timeline/class.animationchannelscalar_cpp.md)* | | *AnimationModifierString* | *[AnimationChannelString](../api/library/animations/timeline/class.animationchannelstring_cpp.md)* | | *AnimationModifierUGUID* | *[AnimationChannelUGUID](../api/library/animations/timeline/class.animationchanneluguid_cpp.md)* | | *AnimationModifierVec2* | *[AnimationChannelVec2](../api/library/animations/timeline/class.animationchannelvec2_cpp.md)* | | *AnimationModifierVec3* | *[AnimationChannelVec3](../api/library/animations/timeline/class.animationchannelvec3_cpp.md)* | | *AnimationModifierVec4* | *[AnimationChannelVec4](../api/library/animations/timeline/class.animationchannelvec4_cpp.md)* | </details>


### Replaced Classes


These classes are gone and their work is done by a different class with a different API - see [Sequencer Replaces the Tracker](../upgrade/migration_api_cpp.md#sequencer_migration) for what the migration involves.


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| *AnimationTrack* | *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)* |
| *AnimationPlayback* | *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)* |
| *AnimationModifierTrack* | *[AnimationChannelSubSequence](../api/library/animations/timeline/class.animationchannelsubsequence_cpp.md)* |
| *AnimationObject* | *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* |
| *AnimationObjectNode* | *[AnimationBindNode](../api/library/animations/timeline/class.animationbindnode_cpp.md)* |
| *AnimationObjectMaterial* | *[AnimationBindMaterial](../api/library/animations/timeline/class.animationbindmaterial_cpp.md)* |
| *AnimationObjectPropertyParameter* | *[AnimationBindPropertyParameter](../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md)* |
| *AnimationObjectRuntime* | *[AnimationBindRuntime](../api/library/animations/timeline/class.animationbindruntime_cpp.md)* |
| *AnimationObjectTrack* | *[AnimationChannelSubSequence](../api/library/animations/timeline/class.animationchannelsubsequence_cpp.md)* |


### Removed Classes


Removed with no replacement.


- *AnimationFrame*
- *AnimationMask*
- *AnimationModifierMat4*


## Breaking Changes


### Sequencer Replaces the Tracker


Animation over time used to be authored in the *Tracker*. In 2.22 that job belongs to the *[Sequencer](../editor2/tools/sequencer/index.md)* - a more modern and more convenient tool - and the animation API has been reshaped to match it. Skeletal animation, the animation graph and *[AnimScript](../api/library/animations/skeletal/class.animscript_cpp.md)* are a separate subject and are not affected by this chapter, apart from the changes listed in [AnimScript Class](../upgrade/migration_api_cpp.md#animscript_class).


> **Notice:** The *Tracker* itself is still there, and `*.track` files still play - see [Running Tracks in Application](../editor2/tools/tracker/run/index.md). This chapter is about the animation classes, which have been reshaped around the *[Sequencer](../editor2/tools/sequencer/index.md)*.


The model is now the following:


- An *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)* is one animation, stored in a `*.seq` file. It is content only and holds no scene objects.
- An *[AnimationChannel](../api/library/animations/timeline/class.animationchannel_cpp.md)* is one animated parameter inside the sequence - one row of the timeline. Its typed subclasses carry the keys.
- An *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* says which objects a channel drives. The bind classes existed in 2.21 as well, but now they are the only way a channel reaches the scene.
- Playback is a player: either the *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)* class, or the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cpp.md)* node that keeps one and ticks it. In 2.21 a playback was also saved to a `*.uplay` file of its own; in 2.22 a player is created in code or set up on the node, and has no file.


#### Classes


The classes that made up a track are replaced as follows.


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| *AnimationTrack* | *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)* |
| *AnimationPlayback* | *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)* |
| *NodeAnimationPlayback* | *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cpp.md)* |
| *AnimationModifier* and its typed subclasses | *[AnimationChannel](../api/library/animations/timeline/class.animationchannel_cpp.md)* and its typed subclasses. The rename is mechanical - *AnimationModifierFloat* becomes *[AnimationChannelFloat](../api/library/animations/timeline/class.animationchannelfloat_cpp.md)*, and so on for every type. The complete list is in [Major Changes](../upgrade/migration_api_cpp.md#major_changes). |
| *AnimationModifierTrack* | *[AnimationChannelSubSequence](../api/library/animations/timeline/class.animationchannelsubsequence_cpp.md)* |
| *AnimationObject*, *AnimationObjectNode*, *AnimationObjectMaterial*, *AnimationObjectPropertyParameter*, *AnimationObjectRuntime* | The corresponding *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* classes. In 2.21 the two hierarchies existed side by side; the *AnimationObject* one has been removed. |
| *AnimationModifierMat4*, *AnimationFrame*, *AnimationMask* | Removed with no direct replacement. |


#### Renamed Methods


Two methods of the *[Animations](../api/library/animations/class.animations_cpp.md)* class were renamed along with the classes they mention, and the copying method of every curve and every channel was renamed as well.


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| **Animations::getParameterModifierType()** | *[*Animations::getParameterChannelType()*](../api/library/animations/class.animations_cpp.md#getParameterChannelType_int_int)* |
| **Animations::animToBonesModifier()** | *[*Animations::animToBonesChannel()*](../api/library/animations/class.animations_cpp.md#animToBonesChannel_cstr_AnimationChannelBones_float_int)* |
| **copy()** of every *AnimationCurve* and *AnimationModifier* class | **assignFrom()** of the corresponding *[AnimationCurve](../api/library/animations/timeline/class.animationcurve_cpp.md)* and *[AnimationChannel](../api/library/animations/timeline/class.animationchannel_cpp.md)* class |


#### Uniform Time Became Constant Speed


The uniform time switch that the floating-point modifier classes carried in 2.21 is gone. The behaviour itself stayed and moved to the *[AnimationChannel](../api/library/animations/timeline/class.animationchannel_cpp.md)* base class under a name that says what it does: the curve is measured along its own length and the playhead is remapped through that measurement, so the value travels at a constant speed while the total duration holds.


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| **updateUniformTime()** of the floating-point modifiers | *[*AnimationChannel::setConstantSpeed()*](../api/library/animations/timeline/class.animationchannel_cpp.md#setConstantSpeed_int_int_void)* |
| **isUniformTime()** of the floating-point modifiers | *[*AnimationChannel::isConstantSpeed()*](../api/library/animations/timeline/class.animationchannel_cpp.md#IsConstantSpeed)* |


Two questions the old pair could not answer come with it: *[*isConstantSpeedSupported()*](../api/library/animations/timeline/class.animationchannel_cpp.md#IsConstantSpeedSupported)* tells whether the channel carries the setting at all, and *[*getConstantSpeedTime()*](../api/library/animations/timeline/class.animationchannel_cpp.md#getConstantSpeedTime_float_float)* returns the moment the curve is sampled at for a given moment on the timeline.


> **Notice:** The setting is offered where the value has a length to measure: a floating-point number, a vector of floats or doubles and a followed path. A rotation carries it in the angles modes only, since the segments of a quaternion rotation are spherical blends already, and an integer channel does not carry it at all. Code that switched uniform time on unconditionally should ask **isConstantSpeedSupported()** first.


#### Key Type and Tangent Setters Take a Value/Time Ratio


The setters that shape a key gained a trailing argument on every curve class: the number of units of value that make up one unit of time. It is taken into account when the two handles of an [aligned](../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_ALIGNED) key are made collinear - the handles are brought into a common space through this ratio, aligned there and converted back, so a curve drawn with value and time on different scales still shows the pair as one straight line.


The argument has a default of 1.0f, which measures value and time on the same scale and reproduces the 2.21 behaviour, so existing calls keep compiling and keep their result. Pass the ratio the curve is actually drawn with when an aligned key has to look aligned to the eye.


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| **setKeyType( int, KEY_TYPE )** | **setKeyType( int, KEY_TYPE, float )** |
| **setKeyLeftTangent( int, vec2 )** | **setKeyLeftTangent( int, vec2, float )** |
| **setKeyRightTangent( int, vec2 )** | **setKeyRightTangent( int, vec2, float )** |
| **setTypeOfAllKeys( KEY_TYPE )** | **setTypeOfAllKeys( KEY_TYPE, float )** |


The same argument was added to the per-component setters of *[AnimationChannel](../api/library/animations/timeline/class.animationchannel_cpp.md)*: *[*setComponentKeyType()*](../api/library/animations/timeline/class.animationchannel_cpp.md#setComponentKeyType_int_int_int_float_void)*, *[*setComponentKeyLeftTangent()*](../api/library/animations/timeline/class.animationchannel_cpp.md#setComponentKeyLeftTangent_int_int_vec2_float_void)* and *[*setComponentKeyRightTangent()*](../api/library/animations/timeline/class.animationchannel_cpp.md#setComponentKeyRightTangent_int_int_vec2_float_void)*.


#### Converting Existing Tracks


A `*.track` file does not have to be rebuilt by hand. *[*Animations::convertLegacyTrackToSequence()*](../api/library/animations/class.animations_cpp.md#convertLegacyTrackToSequence_cstr_cstr_int_String)* converts one into a `*.seq` and returns the path it wrote; the *[Sequencer](../editor2/tools/sequencer/index.md)* offers the same conversion in the menu next to *Save*. A track that plays other tracks inside itself is converted whole, every nested track becoming a sequence of its own.


Most parameters become the channel one would expect. The one worth knowing about is a position track with **follow X / Y / Z**: it becomes an *[AnimationChannelFollowPath](../api/library/animations/timeline/class.animationchannelfollowpath_cpp.md)*, a channel new in 2.22 that carries the trajectory and the aim together and writes both the position and the rotation of its node. A track's **const velocity** arrives as the constant speed setting described above, and its **unit_time** as the speed of the sequence.


Everything the conversion could not carry over is reported to the console, one line per parameter. What to expect there is described in the [Converting Legacy Tracks](../editor2/tools/sequencer/track_import/index.md) article.


#### Bindings Address Many Targets


In 2.21 a binding pointed at one object, named by a description: a node ID and a name, a material GUID, a surface index. In 2.22 a binding is a query that resolves to any number of targets, so the setters take collections and patterns, and the getters ask for a resolved target by its number.


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| **AnimationObjectNode::setNode()** | *[*AnimationBindNode::setNodes()*](../api/library/animations/timeline/class.animationbindnode_cpp.md#setNodes_VECNode_void)* |
| **AnimationObjectNode::getNode()** | *[*AnimationBindNode::getTargetResolvedNode()*](../api/library/animations/timeline/class.animationbindnode_cpp.md#getTargetResolvedNode_int_Node)* |
| **setObjectDescription()**, **setNodeDescription()** | **setObjects()**, **setNodes()** |
| **setMaterialDescription()**, **setPropertyDescription()** | **setAssets()** |
| **setSurfaceDescription()** | **setSurfacePattern()** |


How the query is built - what it matches by and how far it searches - is described in the *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* class reference.


#### No Registry of Loaded Animations


The *[Animations](../api/library/animations/class.animations_cpp.md)* class no longer keeps lists of loaded tracks, playbacks and animation objects. Everything that walked those lists has been removed: **loadTrack()**, **getTrackByPath()**, **getNumTracks()**, the playback counterparts, the *AnimationObject* accessors, the four events reporting additions and removals, and the *Animations::RESULT* enumeration returned by the loading and saving methods. The full list is in [Animations Class](../upgrade/migration_api_cpp.md#animations_class).


A sequence is loaded and saved through the sequence itself, and playing it is the player's job.


| UNIGINE 2.21 | ```cpp // load the track through the registry and find it by path Animations::loadTrack("animations/door.utrack"); AnimationTrackPtr track = Animations::getTrackByPath("animations/door.utrack"); AnimationPlaybackPtr playback = AnimationPlayback::create(); playback->setTrack(track); playback->setLoop(false); playback->setSpeed(1.0f); playback->play(); ``` ```csharp // load the track through the registry and find it by path Animations.LoadTrack("animations/door.utrack"); AnimationTrack track = Animations.GetTrackByPath("animations/door.utrack"); AnimationPlayback playback = new AnimationPlayback(); playback.SetTrack(track); playback.Loop = false; playback.Speed = 1.0f; playback.Play(); ``` |
|---|---|
| UNIGINE 2.22 | ```cpp // the player takes the sequence file directly AnimationSequencePlayerPtr player = AnimationSequencePlayer::create("animations/door.seq"); player->setLoop(false); player->setSpeed(1.0f); player->setAutoTick(true);   // let the Engine advance it every frame player->play(); ``` ```csharp // the player takes the sequence file directly AnimationSequencePlayer player = new AnimationSequencePlayer("animations/door.seq"); player.Loop = false; player.Speed = 1.0f; player.AutoTick = true;   // let the Engine advance it every frame player.Play(); ``` |


To build or edit a sequence in memory rather than load one, create an *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)*, add channels to it with *[*addChannel()*](../api/library/animations/timeline/class.animationsequence_cpp.md#addChannel_AnimationChannel_void)* and hand it to a player. A channel taken out of a sequence is a copy, so an edited channel has to be put back with *[*updateChannel()*](../api/library/animations/timeline/class.animationsequence_cpp.md#updateChannel_AnimationChannel_int)*.


More on playing sequences from code is in the [Runtime Playback](../editor2/tools/sequencer/runtime/index_cpp.md) article.


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
| **setOverlap( true )** | *[*setTransparentOrder( Material::TRANSPARENT_ORDER_AFTER_POST )*](../api/library/rendering/class.material_cpp.md#setTransparentOrder_int_void)* |
| **setOverlap( false )** | *[*setTransparentOrder( Material::TRANSPARENT_ORDER_BEFORE_SSR )*](../api/library/rendering/class.material_cpp.md#setTransparentOrder_int_void)* |
| **isOverlap()** | *[*getTransparentOrder()*](../api/library/rendering/class.material_cpp.md#getTransparentOrder_int)* |
| ***OPTION_OVERLAP*** | *[**OPTION_TRANSPARENT_ORDER**](../api/library/rendering/class.material_cpp.md#OPTION_TRANSPARENT_ORDER)* |


> **Notice:** The new option took the second place in the material option list, so the values of every *OPTION_** constant after *OPTION_TRANSPARENT* shifted by one. Code that stores an option by its number rather than by its name has to be checked.


In shaders the *GET_OPTION_OVERLAP* define became *GET_OPTION_TRANSPARENT_ORDER* and now carries 0, 1 or 2.


### Property File Setters Report Failure


A file GUID identifies a property uniquely, and the setters now refuse a GUID that another property already holds instead of accepting it silently.


In C++ *[**setFilePath()**](../api/library/common/class.property_cpp.md#setFilePath_cstr_int)* and *[**setFileGUID()**](../api/library/common/class.property_cpp.md#setFileGUID_UGUID_int)* return *bool* instead of *void*. Existing code compiles as before, so the result is worth checking where the path or the GUID comes from outside.


### State Machines Addressed by Index


An *[AnimScript](../api/library/animations/skeletal/class.animscript_cpp.md)* state machine used to be named by a string in every call. In 2.22 it is addressed by an index, which turns one lookup per call into one lookup per state machine, and the API around state machines grew from five methods to thirty.


Take the index once with *[*findStateMachineByName()*](../api/library/animations/skeletal/class.animscript_cpp.md#findStateMachineByName_cstr_int)* - or with *[*findStateMachine()*](../api/library/animations/skeletal/class.animscript_cpp.md#findStateMachine_cstr_int)* if you address a nested machine by its path - and pass it everywhere afterwards.


| UNIGINE 2.21 | ```cpp if (anim_script->isStateMachineInTransition("locomotion")) float p = anim_script->getStateMachineTransitionProgress("locomotion"); ``` ```csharp if (animScript.IsStateMachineInTransition("locomotion")) float p = animScript.GetStateMachineTransitionProgress("locomotion"); ``` |
|---|---|
| UNIGINE 2.22 | ```cpp int sm = anim_script->findStateMachineByName("locomotion"); if (anim_script->isStateMachineInTransition(sm)) float p = anim_script->getStateMachineTransitionProgress(sm); ``` ```csharp int sm = animScript.FindStateMachineByName("locomotion"); if (animScript.IsStateMachineInTransition(sm)) float p = animScript.GetStateMachineTransitionProgress(sm); ``` |


Four of the five methods have an index-taking counterpart of the same name. The fifth, **isStateMachineActive()**, is gone: use *[*isStateMachineRelevant()*](../api/library/animations/skeletal/class.animscript_cpp.md#isStateMachineRelevant_int_bool)* to tell whether a state machine takes part in the current pose. Everything the class gained is listed in [AnimScript Class](../upgrade/migration_api_cpp.md#animscript_class).


### Experimental Navigation


2.22 adds a second navigation system, available as **experimental** functionality. It runs beside the existing one and offers capabilities the older system does not have. Nothing in the older API has changed: *[Navigation](../api/library/pathfinding/class.navigation_cpp.md)*, *[NavigationMesh](../api/library/pathfinding/class.navigationmesh_cpp.md)*, *[NavigationSector](../api/library/pathfinding/class.navigationsector_cpp.md)*, the obstacles and *PathFinding* keep every method they had in 2.21, so a project that uses them needs no migration at all.


What has been added:


- The *[ExperimentalNavigation](../api/library/pathfinding/class.experimentalnavigation_cpp.md)* class - the entry point of the system - together with *[ExperimentalNavigationMesh](../api/library/pathfinding/class.experimentalnavigationmesh_cpp.md)*, *[ExperimentalNavigationMeshAreaVolume](../api/library/pathfinding/class.experimentalnavigationmeshareavolume_cpp.md)* and *[ExperimentalNavigationMeshInvoker](../api/library/pathfinding/class.experimentalnavigationmeshinvoker_cpp.md)* nodes.
- Path querying and following: *[ExperimentalNavigationPath](../api/library/pathfinding/class.experimentalnavigationpath_cpp.md)*, *[ExperimentalNavigationPathFetch](../api/library/pathfinding/class.experimentalnavigationpathfetch_cpp.md)*, *[ExperimentalNavigationMeshCorridor](../api/library/pathfinding/class.experimentalnavigationmeshcorridor_cpp.md)*, *[ExperimentalNavigationMeshFilter](../api/library/pathfinding/class.experimentalnavigationmeshfilter_cpp.md)* and *[ExperimentalNavigationAvoidance](../api/library/pathfinding/class.experimentalnavigationavoidance_cpp.md)*.
- Baking: *[ExperimentalBakeNavigation](../api/library/pathfinding/class.experimentalbakenavigation_cpp.md)*, *[ExperimentalNavigationBakeQuery](../api/library/pathfinding/class.experimentalnavigationbakequery_cpp.md)* and *[ExperimentalNavigationBakeSettings](../api/library/pathfinding/class.experimentalnavigationbakesettings_cpp.md)*.


The classes that already existed gained a few entry points into the new system, all of them additions:


- *[*Node::isExperimentalNavigation()*](../api/library/nodes/class.node_cpp.md#isExperimentalNavigation_int)*, together with the new node types in *[Node::TYPE](../api/library/nodes/class.node_cpp.md#EXPERIMENTAL_NAVIGATION_MESH)*.
- Per-surface flags on *[Object](../api/library/objects/class.object_cpp.md)* that say whether a surface takes part in the bake and what it contributes: *[*setExperimentalNavigation()*](../api/library/objects/class.object_cpp.md#setExperimentalNavigation_int_int_void)*, *[*setExperimentalNavigationArea()*](../api/library/objects/class.object_cpp.md#setExperimentalNavigationArea_int_int_void)* and *[*setExperimentalNavigationBakeMask()*](../api/library/objects/class.object_cpp.md#setExperimentalNavigationBakeMask_int_int_void)*, each with a getter.
- The same three flags on *[TerrainDetailMask](../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md)*, so a landscape detail can be baked as its own area, plus *[*setExperimentalNavigationMinValue()*](../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md#setExperimentalNavigationMinValue_float_void)* for the mask value the detail starts to count from.
- *[*World::setExperimentalNavigationSettings()*](../api/library/engine/class.world_cpp.md#setExperimentalNavigationSettings_cstr_void)* and its getter.
- *[*NavigationMesh::getBakeSettings()*](../api/library/pathfinding/class.navigationmesh_cpp.md#getBakeSettings_ExperimentalNavigationBakeSettings)*.
- The *[Property::PARAMETER_MASK_EXPERIMENTAL_NAVIGATION_BAKE](../api/library/common/class.property_cpp.md#PARAMETER_MASK_EXPERIMENTAL_NAVIGATION_BAKE)* parameter mask.


For what the system does and how to set it up, see [Experimental Navigation](../objects/navigations/experimental/index.md).


### Skeleton Control Rig


Procedural control over a skeleton has been added, and it is an addition only - no existing skeletal animation API has changed. The new classes describe what a control rig node is to do, and are passed to the corresponding nodes of the animation graph:


- Inverse kinematics - *[IKInfo](../api/library/animations/skeletal/class.ikinfo_cpp.md)*, *[IKInfoChain](../api/library/animations/skeletal/class.ikinfochain_cpp.md)*, *[IKInfoTwoBone](../api/library/animations/skeletal/class.ikinfotwobone_cpp.md)*.
- Joint limits - *[JointLimitInfo](../api/library/animations/skeletal/class.jointlimitinfo_cpp.md)* and its cone, twist and hinge variants, collected in a *[JointLimitSetInfo](../api/library/animations/skeletal/class.jointlimitsetinfo_cpp.md)*.
- Look-at - *[LookAtInfo](../api/library/animations/skeletal/class.lookatinfo_cpp.md)* and *[LookAtChainInfo](../api/library/animations/skeletal/class.lookatchaininfo_cpp.md)*.


## AmbientSource Class


#### New Functions


- *[**getPitchShift**( )](../api/library/sounds/class.ambientsource_cpp.md#getPitchShift_float)*
- *[**setPitchShift**( float )](../api/library/sounds/class.ambientsource_cpp.md#setPitchShift_float_void)*


## AnimationBind Class


#### New Functions


- *[**addTarget**( AnimationBind::MATCH_BY )](../api/library/animations/timeline/class.animationbind_cpp.md#addTarget_int_int)*
- *[**duplicateTarget**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#duplicateTarget_int_int)*
- *[**getNumTargetInheritanceMatches**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getNumTargetInheritanceMatches_int_int)*
- *[**getNumTargetMatches**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getNumTargetMatches_int_int)*
- *[**getNumTargets**( )](../api/library/animations/timeline/class.animationbind_cpp.md#getNumTargets_int)*
- *[**getResolvedAssetGUID**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getResolvedAssetGUID_int_UGUID)*
- *[**getResolvedNodeID**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getResolvedNodeID_int_int)*
- *[**getTargetAssetAccess**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetAssetAccess_int_int)*
- *[**getTargetAssetFileGUID**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetAssetFileGUID_int_UGUID)*
- *[**getTargetAssetName**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetAssetName_int_cstr)*
- *[**getTargetAssetRuntimeGUID**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetAssetRuntimeGUID_int_UGUID)*
- *[**getTargetComponentGUID**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetComponentGUID_int_UGUID)*
- *[**getTargetInheritRootGUID**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetInheritRootGUID_int_UGUID)*
- *[**getTargetLiveNodeID**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetLiveNodeID_int_int)*
- *[**getTargetMatchBy**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetMatchBy_int_int)*
- *[**getTargetMatchName**( int, int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetMatchName_int_int_cstr)*
- *[**getTargetNamePattern**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetNamePattern_int_cstr)*
- *[**getTargetNodeAccess**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetNodeAccess_int_int)*
- *[**getTargetNodeID**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetNodeID_int_int)*
- *[**getTargetNodeName**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetNodeName_int_cstr)*
- *[**getTargetNodeReferenceGUID**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetNodeReferenceGUID_int_UGUID)*
- *[**getTargetNodeType**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetNodeType_int_int)*
- *[**getTargetPropertyGUID**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetPropertyGUID_int_UGUID)*
- *[**getTargetRefInnerID**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetRefInnerID_int_int)*
- *[**getTargetScope**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetScope_int_int)*
- *[**getTargetSubtreeRootAccess**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetSubtreeRootAccess_int_int)*
- *[**getTargetSubtreeRootID**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetSubtreeRootID_int_int)*
- *[**getTargetSubtreeRootLiveNodeID**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetSubtreeRootLiveNodeID_int_int)*
- *[**getTargetSubtreeRootName**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#getTargetSubtreeRootName_int_cstr)*
- *[**isTargetNodeTypeIsGroup**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#isTargetNodeTypeIsGroup_int_int)*
- *[**load**( const Ptr<Blob> & )](../api/library/animations/timeline/class.animationbind_cpp.md#load_Blob_void)*
- *[**moveTarget**( int, int )](../api/library/animations/timeline/class.animationbind_cpp.md#moveTarget_int_int_void)*
- *[**moveTargets**( const Vector<int> &, int )](../api/library/animations/timeline/class.animationbind_cpp.md#moveTargets_VECint_int_void)*
- *[**removeTarget**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#removeTarget_int_void)*
- *[**save**( const Ptr<Blob> & )](../api/library/animations/timeline/class.animationbind_cpp.md#save_Blob_void)*
- *[**setNumTargets**( int )](../api/library/animations/timeline/class.animationbind_cpp.md#setNumTargets_int_void)*
- *[**setTargetAsset**( int, const UGUID &, const UGUID & )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetAsset_int_UGUID_UGUID_void)*
- *[**setTargetAssetAccess**( int, AnimationBind::ASSET_ACCESS )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetAssetAccess_int_int_void)*
- *[**setTargetAssetFileGUID**( int, const UGUID & )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetAssetFileGUID_int_UGUID_void)*
- *[**setTargetAssetName**( int, const char * )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetAssetName_int_cstr_void)*
- *[**setTargetComponentGUID**( int, const UGUID & )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetComponentGUID_int_UGUID_void)*
- *[**setTargetInheritRootGUID**( int, const UGUID & )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetInheritRootGUID_int_UGUID_void)*
- *[**setTargetMatchBy**( int, AnimationBind::MATCH_BY )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetMatchBy_int_int_void)*
- *[**setTargetNamePattern**( int, const char * )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetNamePattern_int_cstr_void)*
- *[**setTargetNode**( int, const Ptr<Node> & )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetNode_int_Node_void)*
- *[**setTargetNodeAccess**( int, AnimationBind::NODE_ACCESS )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetNodeAccess_int_int_void)*
- *[**setTargetNodeDescription**( int, int, const char * )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetNodeDescription_int_int_cstr_void)*
- *[**setTargetNodeReferenceGUID**( int, const UGUID & )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetNodeReferenceGUID_int_UGUID_void)*
- *[**setTargetNodeType**( int, int )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetNodeType_int_int_void)*
- *[**setTargetNodeTypeIsGroup**( int, bool )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetNodeTypeIsGroup_int_int_void)*
- *[**setTargetPropertyGUID**( int, const UGUID & )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetPropertyGUID_int_UGUID_void)*
- *[**setTargetRefInnerID**( int, int )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetRefInnerID_int_int_void)*
- *[**setTargetScope**( int, AnimationBind::QUERY_SCOPE )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetScope_int_int_void)*
- *[**setTargetSubtreeRoot**( int, int, const char * )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetSubtreeRoot_int_int_cstr_void)*
- *[**setTargetSubtreeRootAccess**( int, AnimationBind::NODE_ACCESS )](../api/library/animations/timeline/class.animationbind_cpp.md#setTargetSubtreeRootAccess_int_int_void)*


#### New Enums


- *[**ASSET_ACCESS**](../api/library/animations/timeline/class.animationbind_cpp.md#ASSET_ACCESS)*
- *[**MATCH_BY**](../api/library/animations/timeline/class.animationbind_cpp.md#MATCH_BY)*
- *[**NODE_ACCESS**](../api/library/animations/timeline/class.animationbind_cpp.md#NODE_ACCESS)*
- *[**NODE_TYPE_GROUP**](../api/library/animations/timeline/class.animationbind_cpp.md#NODE_TYPE_GROUP)*
- *[**QUERY_SCOPE**](../api/library/animations/timeline/class.animationbind_cpp.md#QUERY_SCOPE)*
- *[**ANIMATION_BIND_COMPONENT**](../api/library/animations/timeline/class.animationbind_cpp.md#ANIMATION_BIND_COMPONENT)*


## AnimationBindMaterial Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***getMaterial**( )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* for the query it is built from. |
| ***getMaterialDescriptionFileGUID**( )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* for the query it is built from. |
| ***getMaterialDescriptionGUID**( )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* for the query it is built from. |
| ***getObject**( )* | Removed. Use *[**getTargetResolvedObject()**](../api/library/animations/timeline/class.animationbindmaterial_cpp.md#getTargetResolvedObject_int_Object)* instead. |
| ***getObjectDescriptionID**( )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* for the query it is built from. |
| ***getObjectDescriptionName**( )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* for the query it is built from. |
| ***getSurfaceDescriptionIndex**( )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* for the query it is built from. |
| ***getSurfaceDescriptionName**( )* | Removed. Use *[**getSurfacePattern()**](../api/library/animations/timeline/class.animationbindmaterial_cpp.md#getSurfacePattern_cstr)* instead. |
| ***setMaterialDescription**( const UGUID &, const UGUID & )* | Removed. Use *[**setAssets()**](../api/library/animations/timeline/class.animationbindmaterial_cpp.md#setAssets_VECUGUID_void)* instead. |
| ***setObjectDescription**( int, const char * )* | Removed. Use *[**setObjects()**](../api/library/animations/timeline/class.animationbindmaterial_cpp.md#setObjects_VECNode_void)* instead. |
| ***setSurfaceDescription**( const char *, int )* | Removed. Use *[**setSurfacePattern()**](../api/library/animations/timeline/class.animationbindmaterial_cpp.md#setSurfacePattern_cstr_void)* instead. |


#### New Functions


- *[**getNumTargetSurfaceMatches**( int )](../api/library/animations/timeline/class.animationbindmaterial_cpp.md#getNumTargetSurfaceMatches_int_int)*
- *[**getSurfacePattern**( )](../api/library/animations/timeline/class.animationbindmaterial_cpp.md#getSurfacePattern_cstr)*
- *[**getTargetResolvedObject**( int )](../api/library/animations/timeline/class.animationbindmaterial_cpp.md#getTargetResolvedObject_int_Object)*
- *[**setAssets**( const Vector<UGUID> & )](../api/library/animations/timeline/class.animationbindmaterial_cpp.md#setAssets_VECUGUID_void)*
- *[**setObjects**( const Vector<Ptr<Node>> & )](../api/library/animations/timeline/class.animationbindmaterial_cpp.md#setObjects_VECNode_void)*
- *[**setSurfacePattern**( const char * )](../api/library/animations/timeline/class.animationbindmaterial_cpp.md#setSurfacePattern_cstr_void)*


#### New Enums


- *[**ACCESS_UNKNOWN**](../api/library/animations/timeline/class.animationbindmaterial_cpp.md#ACCESS_UNKNOWN)*


## AnimationBindNode Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***getNode**( )* | Removed. Use *[**getTargetResolvedNode()**](../api/library/animations/timeline/class.animationbindnode_cpp.md#getTargetResolvedNode_int_Node)* instead. |
| ***getNodeDescriptionID**( )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* for the query it is built from. |
| ***getNodeDescriptionName**( )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* for the query it is built from. |
| ***setNode**( const Ptr<Node> & )* | Removed. Use *[**setNodes()**](../api/library/animations/timeline/class.animationbindnode_cpp.md#setNodes_VECNode_void)* instead. |
| ***setNodeDescription**( int, const char * )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* for the query it is built from. |


#### New Functions


- *[**getTargetResolvedNode**( int )](../api/library/animations/timeline/class.animationbindnode_cpp.md#getTargetResolvedNode_int_Node)*
- *[**setNodes**( const Vector<Ptr<Node>> & )](../api/library/animations/timeline/class.animationbindnode_cpp.md#setNodes_VECNode_void)*


## AnimationBindPropertyParameter Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***getNode**( )* | Removed. Use *[**getTargetResolvedNode()**](../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md#getTargetResolvedNode_int_Node)* instead. |
| ***getNodeDescriptionID**( )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* for the query it is built from. |
| ***getNodeDescriptionName**( )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* for the query it is built from. |
| ***getProperty**( )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* for the query it is built from. |
| ***getPropertyDescriptionFileGUID**( )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* for the query it is built from. |
| ***getPropertyDescriptionGUID**( )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* for the query it is built from. |
| ***getPropertyParameter**( )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* for the query it is built from. |
| ***getSurfaceDescriptionIndex**( )* | Removed. A binding resolves to any number of targets in 2.22 - see *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* for the query it is built from. |
| ***getSurfaceDescriptionName**( )* | Removed. Use *[**getSurfacePattern()**](../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md#getSurfacePattern_cstr)* instead. |
| ***setNodeDescription**( int, const char * )* | Removed. Use *[**setNodes()**](../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md#setNodes_VECNode_void)* instead. |
| ***setPropertyDescription**( const UGUID &, const UGUID & )* | Removed. Use *[**setAssets()**](../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md#setAssets_VECUGUID_void)* instead. |
| ***setSurfaceDescription**( const char *, int )* | Removed. Use *[**setSurfacePattern()**](../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md#setSurfacePattern_cstr_void)* instead. |


#### New Functions


- *[**getNumTargetSurfaceMatches**( int )](../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md#getNumTargetSurfaceMatches_int_int)*
- *[**getSurfacePattern**( )](../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md#getSurfacePattern_cstr)*
- *[**getTargetResolvedNode**( int )](../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md#getTargetResolvedNode_int_Node)*
- *[**getTargetResolvedProperty**( int )](../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md#getTargetResolvedProperty_int_Property)*
- *[**setAssets**( const Vector<UGUID> & )](../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md#setAssets_VECUGUID_void)*
- *[**setNodes**( const Vector<Ptr<Node>> & )](../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md#setNodes_VECNode_void)*
- *[**setSurfacePattern**( const char * )](../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md#setSurfacePattern_cstr_void)*


#### New Enums


- *[**ACCESS_UNKNOWN**](../api/library/animations/timeline/class.animationbindpropertyparameter_cpp.md#ACCESS_UNKNOWN)*


## AnimationBindRuntime Class


#### New Functions


- *[**getAmbientSource**( )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#getAmbientSource_AmbientSource)*
- *[**getAnimScript**( )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#getAnimScript_AnimScript)*
- *[**getBody**( )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#getBody_Body)*
- *[**getCamera**( )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#getCamera_Camera)*
- *[**getGui**( )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#getGui_Gui)*
- *[**getJoint**( )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#getJoint_Joint)*
- *[**getLensFlare**( )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#getLensFlare_LightLensFlare)*
- *[**getParticleModifier**( )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#getParticleModifier_ParticleModifier)*
- *[**getProperty**( )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#getProperty_Property)*
- *[**getRenderEnvironmentPreset**( )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#getRenderEnvironmentPreset_RenderEnvironmentPreset)*
- *[**getSequence**( )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#getSequence_AnimationSequence)*
- *[**getShape**( )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#getShape_Shape)*
- *[**getViewport**( )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#getViewport_Viewport)*
- *[**getWindow**( )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#getWindow_EngineWindow)*
- *[**setAmbientSource**( const Ptr<AmbientSource> & )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#setAmbientSource_AmbientSource_void)*
- *[**setAnimScript**( const Ptr<AnimScript> & )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#setAnimScript_AnimScript_void)*
- *[**setBody**( const Ptr<Body> & )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#setBody_Body_void)*
- *[**setCamera**( const Ptr<Camera> & )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#setCamera_Camera_void)*
- *[**setGui**( const Ptr<Gui> & )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#setGui_Gui_void)*
- *[**setJoint**( const Ptr<Joint> & )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#setJoint_Joint_void)*
- *[**setLensFlare**( const Ptr<LightLensFlare> & )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#setLensFlare_LightLensFlare_void)*
- *[**setParticleModifier**( const Ptr<ParticleModifier> & )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#setParticleModifier_ParticleModifier_void)*
- *[**setProperty**( const Ptr<Property> & )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#setProperty_Property_void)*
- *[**setRenderEnvironmentPreset**( const Ptr<RenderEnvironmentPreset> & )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#setRenderEnvironmentPreset_RenderEnvironmentPreset_void)*
- *[**setSequence**( const Ptr<AnimationSequence> & )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#setSequence_AnimationSequence_void)*
- *[**setShape**( const Ptr<Shape> & )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#setShape_Shape_void)*
- *[**setViewport**( const Ptr<Viewport> & )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#setViewport_Viewport_void)*
- *[**setWindow**( const Ptr<EngineWindow> & )](../api/library/animations/timeline/class.animationbindruntime_cpp.md#setWindow_EngineWindow_void)*


## AnimationCurve Class


#### New Functions


- *[**wrapSourceTime**( float, float, AnimationCurve::EXTRAPOLATION, AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurve_cpp.md#wrapSourceTime_float_float_int_int_float)*


#### New Enums


- *[**EXTRAPOLATION**](../api/library/animations/timeline/class.animationcurve_cpp.md#EXTRAPOLATION)*
- *[**KEY_TYPE_ALIGNED**](../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_ALIGNED)*
- *[**KEY_TYPE_AUTO_FLAT**](../api/library/animations/timeline/class.animationcurve_cpp.md#KEY_TYPE_AUTO_FLAT)*


## AnimationCurveBool Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***copy**( const Ptr<AnimationCurveBool> & )* | Renamed. Use *[**assignFrom**](../api/library/animations/timeline/class.animationcurvebool_cpp.md#assignFrom_AnimationCurveBool_void)* instead. |
| ***setKeyType**( int, AnimationCurve::KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |
| ***setKeyLeftTangent**( int, const Math::vec2 & )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |
| ***setKeyRightTangent**( int, const Math::vec2 & )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |
| ***setTypeOfAllKeys**( AnimationCurve::KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |


#### New Functions


- *[**assignFrom**( const Ptr<AnimationCurveBool> & )](../api/library/animations/timeline/class.animationcurvebool_cpp.md#assignFrom_AnimationCurveBool_void)*
- *[**getPostInfinity**( )](../api/library/animations/timeline/class.animationcurvebool_cpp.md#getPostInfinity_int)*
- *[**getPreInfinity**( )](../api/library/animations/timeline/class.animationcurvebool_cpp.md#getPreInfinity_int)*
- *[**setPostInfinity**( AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurvebool_cpp.md#setPostInfinity_int_void)*
- *[**setPreInfinity**( AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurvebool_cpp.md#setPreInfinity_int_void)*


## AnimationCurveDouble Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***copy**( const Ptr<AnimationCurveDouble> & )* | Renamed. Use *[**assignFrom**](../api/library/animations/timeline/class.animationcurvedouble_cpp.md#assignFrom_AnimationCurveDouble_void)* instead. |
| ***setKeyType**( int, AnimationCurve::KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |
| ***setKeyLeftTangent**( int, const Math::vec2 & )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |
| ***setKeyRightTangent**( int, const Math::vec2 & )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |
| ***setTypeOfAllKeys**( AnimationCurve::KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |


#### New Functions


- *[**assignFrom**( const Ptr<AnimationCurveDouble> & )](../api/library/animations/timeline/class.animationcurvedouble_cpp.md#assignFrom_AnimationCurveDouble_void)*
- *[**getPostInfinity**( )](../api/library/animations/timeline/class.animationcurvedouble_cpp.md#getPostInfinity_int)*
- *[**getPreInfinity**( )](../api/library/animations/timeline/class.animationcurvedouble_cpp.md#getPreInfinity_int)*
- *[**setPostInfinity**( AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurvedouble_cpp.md#setPostInfinity_int_void)*
- *[**setPreInfinity**( AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurvedouble_cpp.md#setPreInfinity_int_void)*


## AnimationCurveFloat Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***copy**( const Ptr<AnimationCurveFloat> & )* | Renamed. Use *[**assignFrom**](../api/library/animations/timeline/class.animationcurvefloat_cpp.md#assignFrom_AnimationCurveFloat_void)* instead. |
| ***setKeyType**( int, AnimationCurve::KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |
| ***setKeyLeftTangent**( int, const Math::vec2 & )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |
| ***setKeyRightTangent**( int, const Math::vec2 & )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |
| ***setTypeOfAllKeys**( AnimationCurve::KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |


#### New Functions


- *[**assignFrom**( const Ptr<AnimationCurveFloat> & )](../api/library/animations/timeline/class.animationcurvefloat_cpp.md#assignFrom_AnimationCurveFloat_void)*
- *[**getPostInfinity**( )](../api/library/animations/timeline/class.animationcurvefloat_cpp.md#getPostInfinity_int)*
- *[**getPreInfinity**( )](../api/library/animations/timeline/class.animationcurvefloat_cpp.md#getPreInfinity_int)*
- *[**setPostInfinity**( AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurvefloat_cpp.md#setPostInfinity_int_void)*
- *[**setPreInfinity**( AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurvefloat_cpp.md#setPreInfinity_int_void)*


## AnimationCurveInt Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***copy**( const Ptr<AnimationCurveInt> & )* | Renamed. Use *[**assignFrom**](../api/library/animations/timeline/class.animationcurveint_cpp.md#assignFrom_AnimationCurveInt_void)* instead. |
| ***setKeyType**( int, AnimationCurve::KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |
| ***setKeyLeftTangent**( int, const Math::vec2 & )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |
| ***setKeyRightTangent**( int, const Math::vec2 & )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |
| ***setTypeOfAllKeys**( AnimationCurve::KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |


#### New Functions


- *[**assignFrom**( const Ptr<AnimationCurveInt> & )](../api/library/animations/timeline/class.animationcurveint_cpp.md#assignFrom_AnimationCurveInt_void)*
- *[**getPostInfinity**( )](../api/library/animations/timeline/class.animationcurveint_cpp.md#getPostInfinity_int)*
- *[**getPreInfinity**( )](../api/library/animations/timeline/class.animationcurveint_cpp.md#getPreInfinity_int)*
- *[**setPostInfinity**( AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurveint_cpp.md#setPostInfinity_int_void)*
- *[**setPreInfinity**( AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurveint_cpp.md#setPreInfinity_int_void)*


## AnimationCurveQuat Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***copy**( const Ptr<AnimationCurveQuat> & )* | Renamed. Use *[**assignFrom**](../api/library/animations/timeline/class.animationcurvequat_cpp.md#assignFrom_AnimationCurveQuat_void)* instead. |


#### New Functions


- *[**assignFrom**( const Ptr<AnimationCurveQuat> & )](../api/library/animations/timeline/class.animationcurvequat_cpp.md#assignFrom_AnimationCurveQuat_void)*
- *[**getPostInfinity**( )](../api/library/animations/timeline/class.animationcurvequat_cpp.md#getPostInfinity_int)*
- *[**getPreInfinity**( )](../api/library/animations/timeline/class.animationcurvequat_cpp.md#getPreInfinity_int)*
- *[**setPostInfinity**( AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurvequat_cpp.md#setPostInfinity_int_void)*
- *[**setPreInfinity**( AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurvequat_cpp.md#setPreInfinity_int_void)*


## AnimationCurveScalar Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***copy**( const Ptr<AnimationCurveScalar> & )* | Renamed. Use *[**assignFrom**](../api/library/animations/timeline/class.animationcurvescalar_cpp.md#assignFrom_AnimationCurveScalar_void)* instead. |
| ***setKeyType**( int, AnimationCurve::KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |
| ***setKeyLeftTangent**( int, const Math::vec2 & )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |
| ***setKeyRightTangent**( int, const Math::vec2 & )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |
| ***setTypeOfAllKeys**( AnimationCurve::KEY_TYPE )* | Set of arguments changed - see [Key Type and Tangent Setters Take a Value/Time Ratio](../upgrade/migration_api_cpp.md#sequencer_migration_tangent_ratio). |


#### New Functions


- *[**assignFrom**( const Ptr<AnimationCurveScalar> & )](../api/library/animations/timeline/class.animationcurvescalar_cpp.md#assignFrom_AnimationCurveScalar_void)*
- *[**getPostInfinity**( )](../api/library/animations/timeline/class.animationcurvescalar_cpp.md#getPostInfinity_int)*
- *[**getPreInfinity**( )](../api/library/animations/timeline/class.animationcurvescalar_cpp.md#getPreInfinity_int)*
- *[**setPostInfinity**( AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurvescalar_cpp.md#setPostInfinity_int_void)*
- *[**setPreInfinity**( AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurvescalar_cpp.md#setPreInfinity_int_void)*


## AnimationCurveString Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***copy**( const Ptr<AnimationCurveString> & )* | Renamed. Use *[**assignFrom**](../api/library/animations/timeline/class.animationcurvestring_cpp.md#assignFrom_AnimationCurveString_void)* instead. |


#### New Functions


- *[**assignFrom**( const Ptr<AnimationCurveString> & )](../api/library/animations/timeline/class.animationcurvestring_cpp.md#assignFrom_AnimationCurveString_void)*
- *[**getPostInfinity**( )](../api/library/animations/timeline/class.animationcurvestring_cpp.md#getPostInfinity_int)*
- *[**getPreInfinity**( )](../api/library/animations/timeline/class.animationcurvestring_cpp.md#getPreInfinity_int)*
- *[**setPostInfinity**( AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurvestring_cpp.md#setPostInfinity_int_void)*
- *[**setPreInfinity**( AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurvestring_cpp.md#setPreInfinity_int_void)*


## AnimationCurveUGUID Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***copy**( const Ptr<AnimationCurveUGUID> & )* | Renamed. Use *[**assignFrom**](../api/library/animations/timeline/class.animationcurveuguid_cpp.md#assignFrom_AnimationCurveUGUID_void)* instead. |


#### New Functions


- *[**assignFrom**( const Ptr<AnimationCurveUGUID> & )](../api/library/animations/timeline/class.animationcurveuguid_cpp.md#assignFrom_AnimationCurveUGUID_void)*
- *[**getPostInfinity**( )](../api/library/animations/timeline/class.animationcurveuguid_cpp.md#getPostInfinity_int)*
- *[**getPreInfinity**( )](../api/library/animations/timeline/class.animationcurveuguid_cpp.md#getPreInfinity_int)*
- *[**setPostInfinity**( AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurveuguid_cpp.md#setPostInfinity_int_void)*
- *[**setPreInfinity**( AnimationCurve::EXTRAPOLATION )](../api/library/animations/timeline/class.animationcurveuguid_cpp.md#setPreInfinity_int_void)*


## Animations Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***animToBonesModifier**( const char *, const Ptr<AnimationModifierBones> &, float )* | Renamed. Use *[**animToBonesChannel**](../api/library/animations/class.animations_cpp.md#animToBonesChannel_cstr_AnimationChannelBones_float_int)* instead. |
| ***checkUtrackTypes**( )* | Removed. |
| ***containsObject**( int )* | Removed together with the *AnimationObject* class. Bindings are the *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* classes now. |
| ***containsPlayback**( const UGUID & )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cpp.md)* node. |
| ***containsTrack**( const UGUID & )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)*. |
| ***convertToUanims**( const char *, const Vector<String> & )* | Removed. |
| ***convertToUanims**( const Vector<String> &, const Vector<String> & )* | Removed. |
| ***getEventObjectAdded**( )* | Removed together with the *AnimationObject* class. Bindings are the *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* classes now. |
| ***getEventObjectRemoved**( )* | Removed together with the *AnimationObject* class. Bindings are the *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* classes now. |
| ***getEventTrackAdded**( )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)*. |
| ***getEventTrackRemoved**( )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)*. |
| ***getNumObjects**( )* | Removed together with the *AnimationObject* class. Bindings are the *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* classes now. |
| ***getNumPlaybacks**( )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cpp.md)* node. |
| ***getNumTracks**( )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)*. |
| ***getObjectByID**( int )* | Removed together with the *AnimationObject* class. Bindings are the *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* classes now. |
| ***getObjectByIndex**( int )* | Removed together with the *AnimationObject* class. Bindings are the *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* classes now. |
| ***getObjectIndex**( const Ptr<AnimationObject> & )* | Removed together with the *AnimationObject* class. Bindings are the *[AnimationBind](../api/library/animations/timeline/class.animationbind_cpp.md)* classes now. |
| ***getParameterModifierType**( AnimParams::PARAM )* | Renamed. Use *[**getParameterChannelType**](../api/library/animations/class.animations_cpp.md#getParameterChannelType_int_int)* instead. |
| ***getPlaybackByFileGUID**( const UGUID & )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cpp.md)* node. |
| ***getPlaybackByGUID**( const UGUID & )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cpp.md)* node. |
| ***getPlaybackByIndex**( int )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cpp.md)* node. |
| ***getPlaybackByPath**( const char * )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cpp.md)* node. |
| ***getPlaybackIndex**( const Ptr<AnimationPlayback> & )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cpp.md)* node. |
| ***getTrackByFileGUID**( const UGUID & )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)*. |
| ***getTrackByGUID**( const UGUID & )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)*. |
| ***getTrackByIndex**( int )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)*. |
| ***getTrackByPath**( const char * )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)*. |
| ***getTrackIndex**( const Ptr<AnimationTrack> & )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)*. |
| ***loadPlayback**( const char * )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cpp.md)* node. |
| ***loadPlaybacks**( )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cpp.md)* node. |
| ***loadTrack**( const char * )* | Removed. Assign a path with *[**AnimationSequence::setPath()**](../api/library/animations/timeline/class.animationsequence_cpp.md#setPath_cstr_void)* and call *[**AnimationSequence::load()**](../api/library/animations/timeline/class.animationsequence_cpp.md#load_int)*. |
| ***loadTracks**( )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)*. |
| ***reloadTrack**( const char * )* | Removed. Call *[**AnimationSequence::load()**](../api/library/animations/timeline/class.animationsequence_cpp.md#load_int)* again. |
| ***reloadTracks**( )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)*. |
| ***savePlayback**( const Ptr<AnimationPlayback> &, const char * )* | Removed. A player is no longer an asset: create it with *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)* or use the *[NodeSequencePlayer](../api/library/nodes/class.nodesequenceplayer_cpp.md)* node. |
| ***saveTrack**( const Ptr<AnimationTrack> &, const char * )* | Removed. Use *[**AnimationSequence::save()**](../api/library/animations/timeline/class.animationsequence_cpp.md#save_int)* instead. |
| ***saveTrackPrecomputed**( const Ptr<AnimationTrack> &, int, bool, const char * )* | Removed. |
| ***unloadTracks**( )* | Removed. The Engine no longer keeps a registry of loaded animations. A sequence is loaded through the *[AnimationSequence](../api/library/animations/timeline/class.animationsequence_cpp.md)* class and played by *[AnimationSequencePlayer](../api/library/animations/timeline/class.animationsequenceplayer_cpp.md)*. |
| ***RESULT_NEW_PLAYBACK_LOADED*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT_NEW_TRACK_LOADED*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT_PLAYBACK_ERROR*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT_PLAYBACK_IS_ALREADY_LOADED*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT_PLAYBACK_SAVED*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT_TRACK_ERROR*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT_TRACK_IS_ALREADY_LOADED*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT_TRACK_RELOADED*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT_TRACK_SAVED*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT_TRACK_UNLOADED*** | Removed together with the *Animations::RESULT* enumeration. |
| ***RESULT*** | Removed together with the loading and saving methods that returned it. |


#### New Functions


- *[**animToBonesChannel**( const char *, const Ptr<AnimationChannelBones> &, float )](../api/library/animations/class.animations_cpp.md#animToBonesChannel_cstr_AnimationChannelBones_float_int)*
- *[**convertLegacyTrackToSequence**( const char *, const char *, bool )](../api/library/animations/class.animations_cpp.md#convertLegacyTrackToSequence_cstr_cstr_int_String)*
- *[**fetchComponentWrites**( const Ptr<Blob> & )](../api/library/animations/class.animations_cpp.md#fetchComponentWrites_Blob_void)*
- *[**getBaseClasses**( Vector<String> & )](../api/library/animations/class.animations_cpp.md#getBaseClasses_VECString_int)*
- *[**getChannelPropertyDefaultValue**( AnimationChannel::PROPERTY )](../api/library/animations/class.animations_cpp.md#getChannelPropertyDefaultValue_int_float)*
- *[**getChannelPropertyMaxValue**( AnimationChannel::PROPERTY )](../api/library/animations/class.animations_cpp.md#getChannelPropertyMaxValue_int_float)*
- *[**getChannelPropertyMinValue**( AnimationChannel::PROPERTY )](../api/library/animations/class.animations_cpp.md#getChannelPropertyMinValue_int_float)*
- *[**getChannelPropertyName**( AnimationChannel::PROPERTY )](../api/library/animations/class.animations_cpp.md#getChannelPropertyName_int_cstr)*
- *[**getChannelSlotCount**( const Ptr<AnimationChannel> & )](../api/library/animations/class.animations_cpp.md#getChannelSlotCount_AnimationChannel_int)*
- *[**getChannelSlotIndex**( const Ptr<AnimationChannel> &, const char * )](../api/library/animations/class.animations_cpp.md#getChannelSlotIndex_AnimationChannel_cstr_int)*
- *[**getChannelSlotNames**( const Ptr<AnimationChannel> &, Vector<String> & )](../api/library/animations/class.animations_cpp.md#getChannelSlotNames_AnimationChannel_VECString_int)*
- *[**getChannelSupportedProperties**( AnimationChannel::TYPE, Vector<int> & )](../api/library/animations/class.animations_cpp.md#getChannelSupportedProperties_int_VECint_int)*
- *[**getMemoryUsage**( )](../api/library/animations/class.animations_cpp.md#getMemoryUsage_size_t)*
- *[**getParameterAccess**( AnimParams::PARAM )](../api/library/animations/class.animations_cpp.md#getParameterAccess_int_int)*
- *[**getParameterAssetExtension**( AnimParams::PARAM )](../api/library/animations/class.animations_cpp.md#getParameterAssetExtension_int_cstr)*
- *[**getParameterBindType**( AnimParams::PARAM )](../api/library/animations/class.animations_cpp.md#getParameterBindType_int_int)*
- *[**getParameterByReflectionName**( const char *, const char * )](../api/library/animations/class.animations_cpp.md#getParameterByReflectionName_cstr_cstr_int)*
- *[**getParameterChannelType**( AnimParams::PARAM )](../api/library/animations/class.animations_cpp.md#getParameterChannelType_int_int)*
- *[**getParameterClass**( AnimParams::PARAM )](../api/library/animations/class.animations_cpp.md#getParameterClass_int_cstr)*
- *[**getParameterItems**( AnimParams::PARAM )](../api/library/animations/class.animations_cpp.md#getParameterItems_int_cstr)*
- *[**getParameterKeyName**( AnimParams::PARAM )](../api/library/animations/class.animations_cpp.md#getParameterKeyName_int_cstr)*
- *[**getParameterLogicalName**( AnimParams::PARAM )](../api/library/animations/class.animations_cpp.md#getParameterLogicalName_int_cstr)*
- *[**getParameterMaxValue**( AnimParams::PARAM )](../api/library/animations/class.animations_cpp.md#getParameterMaxValue_int_cstr)*
- *[**getParameterMinValue**( AnimParams::PARAM )](../api/library/animations/class.animations_cpp.md#getParameterMinValue_int_cstr)*
- *[**getParameterNodeType**( AnimParams::PARAM )](../api/library/animations/class.animations_cpp.md#getParameterNodeType_int_cstr)*
- *[**getParameterSlotKindName**( AnimParams::PARAM )](../api/library/animations/class.animations_cpp.md#getParameterSlotKindName_int_cstr)*
- *[**getParameterTitle**( AnimParams::PARAM )](../api/library/animations/class.animations_cpp.md#getParameterTitle_int_cstr)*
- *[**getParameterVecComponent**( AnimParams::PARAM )](../api/library/animations/class.animations_cpp.md#getParameterVecComponent_int_int)*
- *[**getParameterWidget**( AnimParams::PARAM )](../api/library/animations/class.animations_cpp.md#getParameterWidget_int_int)*
- *[**isAnimScriptsPreviewBuild**( )](../api/library/animations/class.animations_cpp.md#isAnimScriptsPreviewBuild_int)*
- *[**isChannelParameterReadable**( const Ptr<AnimationChannel> & )](../api/library/animations/class.animations_cpp.md#isChannelParameterReadable_AnimationChannel_int)*
- *[**isParameterTarget**( AnimParams::PARAM, const Ptr<Node> & )](../api/library/animations/class.animations_cpp.md#isParameterTarget_int_Node_int)*
- *[**readChannelParameterValueFloat**( const Ptr<AnimationChannel> &, int, float & )](../api/library/animations/class.animations_cpp.md#readChannelParameterValueFloat_AnimationChannel_int_float_int)*
- *[**readChannelParameterValueNode**( const Ptr<AnimationChannel> & )](../api/library/animations/class.animations_cpp.md#readChannelParameterValueNode_AnimationChannel_Node)*
- *[**readChannelParameterValueString**( const Ptr<AnimationChannel> & )](../api/library/animations/class.animations_cpp.md#readChannelParameterValueString_AnimationChannel_String)*
- *[**readChannelParameterValueUGUID**( const Ptr<AnimationChannel> & )](../api/library/animations/class.animations_cpp.md#readChannelParameterValueUGUID_AnimationChannel_UGUID)*
- *[**readParameterValueFloat**( const Ptr<Node> &, AnimParams::PARAM, int, int, const char *, float & )](../api/library/animations/class.animations_cpp.md#readParameterValueFloat_Node_int_int_int_cstr_float_int)*
- *[**restoreEachFrame**( )](../api/library/animations/class.animations_cpp.md#restoreEachFrame_void)*
- *[**setAnimScriptsPreviewBuild**( bool )](../api/library/animations/class.animations_cpp.md#setAnimScriptsPreviewBuild_int_void)*
- *[**setComponentWritesCollecting**( bool )](../api/library/animations/class.animations_cpp.md#setComponentWritesCollecting_int_void)*
- *[**setSequencerMusicMuted**( bool )](../api/library/animations/class.animations_cpp.md#setSequencerMusicMuted_int_void)*


## AnimScript Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***getStateMachineCurrentStateName**( const char * )* | Set of arguments changed - see [State Machines Addressed by Index](../upgrade/migration_api_cpp.md#animscript_state_machines). |
| ***getStateMachinePreviousStateName**( const char * )* | Set of arguments changed - see [State Machines Addressed by Index](../upgrade/migration_api_cpp.md#animscript_state_machines). |
| ***getStateMachineTransitionProgress**( const char * )* | Set of arguments changed - see [State Machines Addressed by Index](../upgrade/migration_api_cpp.md#animscript_state_machines). |
| ***isStateMachineActive**( const char * )* | Removed. Use *[**isStateMachineRelevant()**](../api/library/animations/skeletal/class.animscript_cpp.md#isStateMachineRelevant_int_bool)* to tell whether a state machine takes part in the current pose. |
| ***isStateMachineInTransition**( const char * )* | Set of arguments changed - see [State Machines Addressed by Index](../upgrade/migration_api_cpp.md#animscript_state_machines). |


#### New Functions


- *[**findStateMachine**( const char * )](../api/library/animations/skeletal/class.animscript_cpp.md#findStateMachine_cstr_int)*
- *[**findStateMachineByName**( const char * )](../api/library/animations/skeletal/class.animscript_cpp.md#findStateMachineByName_cstr_int)*
- *[**findStateMachineState**( int, const char * )](../api/library/animations/skeletal/class.animscript_cpp.md#findStateMachineState_int_cstr_int)*
- *[**getNumStateMachines**( )](../api/library/animations/skeletal/class.animscript_cpp.md#getNumStateMachines_int)*
- *[**getRootMotionDeltaPosition**( )](../api/library/animations/skeletal/class.animscript_cpp.md#getRootMotionDeltaPosition_vec3)*
- *[**getRootMotionDeltaRotation**( )](../api/library/animations/skeletal/class.animscript_cpp.md#getRootMotionDeltaRotation_quat)*
- *[**getStateMachineAnimLength**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineAnimLength_int_float)*
- *[**getStateMachineAnimTime**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineAnimTime_int_float)*
- *[**getStateMachineAnimTimeFraction**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineAnimTimeFraction_int_float)*
- *[**getStateMachineAnimTimeRemaining**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineAnimTimeRemaining_int_float)*
- *[**getStateMachineAnimTimeRemainingFraction**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineAnimTimeRemainingFraction_int_float)*
- *[**getStateMachineCurrentState**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineCurrentState_int_int)*
- *[**getStateMachineCurrentStateName**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineCurrentStateName_int_cstr)*
- *[**getStateMachineName**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineName_int_cstr)*
- *[**getStateMachineNumStates**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineNumStates_int_int)*
- *[**getStateMachineNumTransitionConditions**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineNumTransitionConditions_int_int)*
- *[**getStateMachineOwnerStateName**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineOwnerStateName_int_cstr)*
- *[**getStateMachineParent**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineParent_int_int)*
- *[**getStateMachinePath**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachinePath_int_cstr)*
- *[**getStateMachinePreviousState**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachinePreviousState_int_int)*
- *[**getStateMachinePreviousStateName**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachinePreviousStateName_int_cstr)*
- *[**getStateMachineStateName**( int, int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineStateName_int_int_cstr)*
- *[**getStateMachineStateTime**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineStateTime_int_float)*
- *[**getStateMachineTransitionConditionName**( int, int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineTransitionConditionName_int_int_cstr)*
- *[**getStateMachineTransitionDuration**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineTransitionDuration_int_float)*
- *[**getStateMachineTransitionProgress**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineTransitionProgress_int_float)*
- *[**getStateMachineTransitionTime**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#getStateMachineTransitionTime_int_float)*
- *[**isStateMachineAnimEnded**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#isStateMachineAnimEnded_int_bool)*
- *[**isStateMachineInTransition**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#isStateMachineInTransition_int_bool)*
- *[**isStateMachineRelevant**( int )](../api/library/animations/skeletal/class.animscript_cpp.md#isStateMachineRelevant_int_bool)*
- *[**setStateMachineState**( int, int, float )](../api/library/animations/skeletal/class.animscript_cpp.md#setStateMachineState_int_int_float_void)*
- *[**setStateMachineStateAtTime**( int, int, float, float )](../api/library/animations/skeletal/class.animscript_cpp.md#setStateMachineStateAtTime_int_int_float_float_void)*


## BootConfig Class


#### New Functions


- *[**addFallbackFont**( const char * )](../api/library/engine/class.bootconfig_cpp.md#addFallbackFont_cstr_int)*
- *[**addFontFallback**( int, const char * )](../api/library/engine/class.bootconfig_cpp.md#addFontFallback_int_cstr_void)*
- *[**addGlobalFontFallback**( const char * )](../api/library/engine/class.bootconfig_cpp.md#addGlobalFontFallback_cstr_void)*
- *[**getFallbackFontName**( int )](../api/library/engine/class.bootconfig_cpp.md#getFallbackFontName_int_cstr)*
- *[**getFontFallback**( int, int )](../api/library/engine/class.bootconfig_cpp.md#getFontFallback_int_int_cstr)*
- *[**getGlobalFontFallback**( int )](../api/library/engine/class.bootconfig_cpp.md#getGlobalFontFallback_int_cstr)*
- *[**getNumFontFallbacks**( int )](../api/library/engine/class.bootconfig_cpp.md#getNumFontFallbacks_int_int)*
- *[**getNumFallbackFonts**( )](../api/library/engine/class.bootconfig_cpp.md#getNumFallbackFonts_int)*
- *[**getNumGlobalFontFallbacks**( )](../api/library/engine/class.bootconfig_cpp.md#getNumGlobalFontFallbacks_int)*
- *[**removeFontFallback**( int, int )](../api/library/engine/class.bootconfig_cpp.md#removeFontFallback_int_int_void)*
- *[**removeGlobalFontFallback**( int )](../api/library/engine/class.bootconfig_cpp.md#removeGlobalFontFallback_int_void)*
- *[**setFontFallback**( int, int, const char * )](../api/library/engine/class.bootconfig_cpp.md#setFontFallback_int_int_cstr_void)*
- *[**setGlobalFontFallback**( int, const char * )](../api/library/engine/class.bootconfig_cpp.md#setGlobalFontFallback_int_cstr_void)*


## Console Class


#### New Functions


- *[**getNumPresetNames**( const char * )](../api/library/engine/class.console_cpp.md#getNumPresetNames_cstr_int)*
- *[**getPresetName**( const char *, int )](../api/library/engine/class.console_cpp.md#getPresetName_cstr_int_cstr)*


## ComponentSystem Class


#### New Functions


- *[**hasComponentByClassGUID**( int, const UGUID & )](../api/library/common/logic/component_system/cpp/class.componentsystem_cpp.md#hasComponentByClassGUID_int_const_UGUID_ref_bool)*
- *[**isInitialized**( )](../api/library/common/logic/component_system/cpp/class.componentsystem_cpp.md#isInitialized_bool)*


## CustomSystemProxy Class


New methods should be implemented in case you inherit from the *CustomSystemProxy* Class.


#### New Functions


- *[**isIMETextInputEnabled**( )](../api/library/engine/class.customsystemproxy_cpp.md#isIMETextInputEnabled_bool)*
- *[**setIMETextInputEnabled**( bool )](../api/library/engine/class.customsystemproxy_cpp.md#setIMETextInputEnabled_bool_void)*
- *[**setIMETextInputRect**( int, int, int, int )](../api/library/engine/class.customsystemproxy_cpp.md#setIMETextInputRect_int_int_int_int_void)*


## Editor Class


#### New Functions


- *[**getIntersection**( const Math::WorldBoundFrustum &, Vector<Ptr<Node>> &, Vector<Ptr<Node>> & )](../api/library/engine/class.editor_cpp.md#getIntersection_WorldBoundFrustum_VECNode_VECNode_int)*


## EngineWindowViewport Class


#### New Functions


- *[**calculateEngineRenderResolution**( Math::ivec2 &, Math::ivec2 &, Math::ivec2 & )](../api/library/gui/class.enginewindowviewport_cpp.md#calculateEngineRenderResolution_ivec2_ivec2_ivec2_void)*


## Ffp Class


#### New Enums


- *[**TEXTURE_SAMPLE_BINDLESS**](../api/library/rendering/class.ffp_cpp.md#TEXTURE_SAMPLE_BINDLESS)*


## FMOD::Bus Class


#### New Functions


- *[**getPortIndex**( )](../api/library/plugins/fmod/class.bus_cpp.md#getPortIndex_int)*
- *[**setPortIndex**( Bus::PORT_INDEX )](../api/library/plugins/fmod/class.bus_cpp.md#setPortIndex_int_void)*


#### New Enums


- *[**PORT_INDEX**](../api/library/plugins/fmod/class.bus_cpp.md#PORT_INDEX)*


## FMOD::EventInstance Class


#### New Functions


- *[**setParameterWithLabel**( const char *, const char *, bool )](../api/library/plugins/fmod/class.eventinstance_cpp.md#setParameterWithLabel_cstr_cstr_bool_void)*


## FMOD::FMOD Class


#### New Functions


- *[**loadOutputPlugin**( const char * )](../api/library/plugins/fmod/class.fmod_cpp.md#loadOutputPlugin_cstr_void)*


## FMOD::FMODCore Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| *[**createSound**( const char *, FMODEnums::FMOD_MODE )](../api/library/plugins/fmod/class.fmodcore_cpp.md#createSound_cstr_int_Sound)* | Parameter name changed. |


#### New Functions


- *[**createSound**( const Ptr<Blob> &, FMODEnums::FMOD_MODE )](../api/library/plugins/fmod/class.fmodcore_cpp.md#createSound_Blob_int_Sound)*


## FMOD::FMODStudio Class


#### New Functions


- *[**getGlobalParameter**( const char * )](../api/library/plugins/fmod/class.fmodstudio_cpp.md#getGlobalParameter_cstr_float)*
- *[**setGlobalParameter**( const char *, float )](../api/library/plugins/fmod/class.fmodstudio_cpp.md#setGlobalParameter_cstr_float_void)*
- *[**setGlobalParameterWithLabel**( const char *, const char *, bool )](../api/library/plugins/fmod/class.fmodstudio_cpp.md#setGlobalParameterWithLabel_cstr_cstr_bool_void)*


## Geodetics::Converter Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***GEODETIC_MODE_GEODETICS_PLUGIN_EPSG*** | Removed. Use *[**GEODETIC_MODE_PROJECTED**](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#GEODETIC_MODE_PROJECTED)* together with *[**PROJECTION_MODE_EPSG**](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#PROJECTION_MODE_EPSG)* instead. |
| ***GEODETIC_MODE_GEODETICS_PLUGIN_WKT2*** | Removed.Use *[**GEODETIC_MODE_PROJECTED**](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#GEODETIC_MODE_PROJECTED)* together with *[**PROJECTION_MODE_WKT2**](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#PROJECTION_MODE_WKT2)* instead. |
| *[**geocentricEulerToGeodeticEuler**( const Math::dvec3 &, const Math::vec3 & )](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#geocentricEulerToGeodeticEuler_dvec3_vec3_vec3)* | Parameter name changed. |
| *[**geocentricToGeodetic**( const Math::dvec3 &, double, double )](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#geocentricToGeodetic_dvec3_double_double_dvec3)* | Parameter name changed. |
| *[**geodeticEulerToGeocentricEuler**( const Math::dvec3 &, const Math::vec3 & )](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#geodeticEulerToGeocentricEuler_dvec3_vec3_vec3)* | Parameter name changed. |
| *[**geodeticEulerToRotation**( const Math::dvec3 &, const Math::vec3 & )](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#geodeticEulerToRotation_dvec3_vec3_quat)* | Parameter name changed. |
| *[**geodeticToGeocentric**( const Math::dvec3 &, double, double )](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#geodeticToGeocentric_dvec3_double_double_dvec3)* | Parameter name changed. |
| *[**geodeticToWorld**( const Math::dvec3 & )](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#geodeticToWorld_dvec3_Vec3)* | Parameter name changed. |
| *[**getZeroBasis**( const Math::dvec3 & )](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#getZeroBasis_dvec3_Mat4)* | Parameter name changed. |
| *[**getZeroRotation**( const Math::dvec3 & )](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#getZeroRotation_dvec3_quat)* | Parameter name changed. |
| *[**getZeroUpDirection**( const Math::dvec3 & )](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#getZeroUpDirection_dvec3_vec3)* | Parameter name changed. |
| *[**rotationToGeodeticEuler**( const Math::dvec3 &, const Math::quat & )](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#rotationToGeodeticEuler_dvec3_quat_vec3)* | Parameter name changed. |
| *[**getOrigin**( )](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#getOrigin_dvec3)* | Return value type changed. |


#### New Functions


- *[**getAnchor**( )](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#getAnchor_Anchor)*
- *[**getProjectionMode**( )](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#getProjectionMode_int)*


#### New Enums


- *[**GEODETIC_MODE_ANCHOR**](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#GEODETIC_MODE_ANCHOR)*
- *[**GEODETIC_MODE_PROJECTED**](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#GEODETIC_MODE_PROJECTED)*
- *[**PROJECTION_MODE**](../api/library/geodetics/geodetics_plugin/class.converter_cpp.md#PROJECTION_MODE)*


## Geodetics::Transformer Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| *[**geodeticToWorldPosition**( const Math::dvec3 &, bool )](../api/library/geodetics/geodetics_plugin/class.transformer_cpp.md#geodeticToWorldPosition_dvec3_bool_dvec3)* | Parameter name changed. |
| *[**geodeticToWorld**( const Math::dvec3 &, bool )](../api/library/geodetics/geodetics_plugin/class.transformer_cpp.md#geodeticToWorld_dvec3_bool_dmat4)* | Parameter name changed. |
| *[**setProjectionEpsg**( int, const Math::dvec3 &, const char *, bool )](../api/library/geodetics/geodetics_plugin/class.transformer_cpp.md#setProjectionEpsg_int_dvec3_cstr_bool_int)* | Parameter name changed. |
| *[**setProjectionWkt**( const char *, const Math::dvec3 &, const char *, bool )](../api/library/geodetics/geodetics_plugin/class.transformer_cpp.md#setProjectionWkt_cstr_dvec3_cstr_bool_int)* | Parameter name changed. |


## Gui Class


#### New Functions


- *[**getGlobalCursorMode**( )](../api/library/gui/class.gui_cpp.md#getGlobalCursorMode_int)*
- *[**setGlobalCursorMode**( Gui::CursorMode )](../api/library/gui/class.gui_cpp.md#setGlobalCursorMode_int_void)*
- *[**getGlobalTextDirection**( )](../api/library/gui/class.gui_cpp.md#getGlobalTextDirection_int)*
- *[**setGlobalTextDirection**( Gui::TextDirection )](../api/library/gui/class.gui_cpp.md#setGlobalTextDirection_int_void)*


#### New Enums


- *[**CursorMode**](../api/library/gui/class.gui_cpp.md#CursorMode)*
- *[**TextDirection**](../api/library/gui/class.gui_cpp.md#TextDirection)*


## Input Class


#### New Functions


- *[**getEventTextEditing**( )](../api/library/controls/class.input_cpp.md#getEventTextEditing_Event)*
- *[**isIMEEnabled**( )](../api/library/controls/class.input_cpp.md#isIMEEnabled_int)*
- *[**setIMEEnabled**( bool )](../api/library/controls/class.input_cpp.md#setIMEEnabled_int_void)*
- *[**setIMETextInputRect**( int, int, int, int )](../api/library/controls/class.input_cpp.md#setIMETextInputRect_int_int_int_int_void)*


## InputEvent Class


#### New Enums


- *[**TYPE::INPUT_EVENT_PAD_ACCELEROMETER_MOTION**](../api/library/controls/class.inputevent_cpp.md#INPUT_EVENT_PAD_ACCELEROMETER_MOTION)*
- *[**TYPE::INPUT_EVENT_PAD_GYROSCOPE_MOTION**](../api/library/controls/class.inputevent_cpp.md#INPUT_EVENT_PAD_GYROSCOPE_MOTION)*
- *[**TYPE::INPUT_EVENT_TEXT_EDITING**](../api/library/controls/class.inputevent_cpp.md#INPUT_EVENT_TEXT_EDITING)*


## InputEventPadButton Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| *[**InputEventPadButton**( )](../api/library/controls/class.inputeventpadbutton_cpp.md#InputEventPadButton_ulonglong_constMathivec2_InputEventPadButtonACTION_int_InputGAMEPAD_BUTTON)* | Set of arguments changed. |


## InputGamePad Class


#### New Functions


- *[**getAcceleration**( )](../api/library/controls/class.inputgamepad_cpp.md#getAcceleration_vec3)*
- *[**getAngularVelocity**( )](../api/library/controls/class.inputgamepad_cpp.md#getAngularVelocity_vec3)*
- *[**isAccelerationSupported**( )](../api/library/controls/class.inputgamepad_cpp.md#isAccelerationSupported_int)*
- *[**isAngularVelocitySupported**( )](../api/library/controls/class.inputgamepad_cpp.md#isAngularVelocitySupported_int)*
- *[**isLightSupported**( )](../api/library/controls/class.inputgamepad_cpp.md#isLightSupported_int)*
- *[**setLightColor**( const Math::vec3 & )](../api/library/controls/class.inputgamepad_cpp.md#setLightColor_vec3_void)*


## InputVRDevice Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***canReportBatteryValue**( )* | Renamed. Use *[**isBatteryValid**](../api/library/controls/class.inputvrdevice_cpp.md#isBatteryValid_int)* instead. |
| ***isCharging**( )* | Renamed. Use *[**isBatteryCharging**](../api/library/controls/class.inputvrdevice_cpp.md#isBatteryCharging_int)* instead. |


#### New Functions


- *[**isBatteryCharging**( )](../api/library/controls/class.inputvrdevice_cpp.md#isBatteryCharging_int)*
- *[**isBatteryPluggedIn**( )](../api/library/controls/class.inputvrdevice_cpp.md#isBatteryPluggedIn_int)*
- *[**isBatteryValid**( )](../api/library/controls/class.inputvrdevice_cpp.md#isBatteryValid_int)*


## Json Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| *[**getString**( )](../api/library/common/class.json_cpp.md#getString_cstr)* | Return value type changed. |


## Light Class


#### New Functions


- *[**getSpecularRoughnessOffset**( )](../api/library/lights/class.light_cpp.md#getSpecularRoughnessOffset_float)*
- *[**setSpecularRoughnessOffset**( float )](../api/library/lights/class.light_cpp.md#setSpecularRoughnessOffset_float_void)*


## LightEnvironmentProbe Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***isRenderAboveVoxelProbes**( )* | Removed. |
| ***setRenderAboveVoxelProbes**( bool )* | Removed. |


#### New Functions


- *[**getGrabDynamicInterleaved**( )](../api/library/lights/class.lightenvironmentprobe_cpp.md#getGrabDynamicInterleaved_int)*
- *[**setGrabDynamicInterleaved**( LightEnvironmentProbe::GRAB_DYNAMIC_INTERLEAVED )](../api/library/lights/class.lightenvironmentprobe_cpp.md#setGrabDynamicInterleaved_int_void)*
- *[**getGrabDynamicInterleavedColorClamping**( )](../api/library/lights/class.lightenvironmentprobe_cpp.md#getGrabDynamicInterleavedColorClamping_int)*
- *[**setGrabDynamicInterleavedColorClamping**( LightEnvironmentProbe::GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING )](../api/library/lights/class.lightenvironmentprobe_cpp.md#setGrabDynamicInterleavedColorClamping_int_void)*
- *[**getGrabDynamicReprojection**( )](../api/library/lights/class.lightenvironmentprobe_cpp.md#getGrabDynamicReprojection_int)*
- *[**setGrabDynamicReprojection**( LightEnvironmentProbe::GRAB_DYNAMIC_REPROJECTION )](../api/library/lights/class.lightenvironmentprobe_cpp.md#setGrabDynamicReprojection_int_void)*


#### New Enums


- *[**GRAB_DYNAMIC_REPROJECTION**](../api/library/lights/class.lightenvironmentprobe_cpp.md#GRAB_DYNAMIC_REPROJECTION)*
- *[**LAST_STEP_MODE_UNDERLYING_PROBES**](../api/library/lights/class.lightenvironmentprobe_cpp.md#LAST_STEP_MODE_UNDERLYING_PROBES)*
- *[**GRAB_DYNAMIC_INTERLEAVED**](../api/library/lights/class.lightenvironmentprobe_cpp.md#GRAB_DYNAMIC_INTERLEAVED)*
- *[**GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING**](../api/library/lights/class.lightenvironmentprobe_cpp.md#GRAB_DYNAMIC_INTERLEAVED_COLOR_CLAMPING)*


## LightVoxelProbe Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***isBakeVisibilityEnvironmentProbe**( )* | Removed. |
| ***setBakeVisibilityEnvironmentProbe**( bool )* | Removed. |


## LightWorld Class


#### New Functions


- *[**getShadowCascadeOriginMode**( )](../api/library/lights/class.lightworld_cpp.md#getShadowCascadeOriginMode_int)*
- *[**setShadowCascadeOriginMode**( LightWorld::SHADOW_CASCADE_ORIGIN_MODE )](../api/library/lights/class.lightworld_cpp.md#setShadowCascadeOriginMode_int_void)*
- *[**getShadowCascadeOriginPosition**( )](../api/library/lights/class.lightworld_cpp.md#getShadowCascadeOriginPosition_Vec3)*
- *[**setShadowCascadeOriginPosition**( const Math::Vec3 & )](../api/library/lights/class.lightworld_cpp.md#setShadowCascadeOriginPosition_Vec3_void)*
- *[**getShadowCascadePlacementMode**( )](../api/library/lights/class.lightworld_cpp.md#getShadowCascadePlacementMode_int)*
- *[**setShadowCascadePlacementMode**( LightWorld::SHADOW_CASCADE_PLACEMENT_MODE )](../api/library/lights/class.lightworld_cpp.md#setShadowCascadePlacementMode_int_void)*
- *[**getShadowFilterFar**( )](../api/library/lights/class.lightworld_cpp.md#getShadowFilterFar_float)*
- *[**setShadowFilterFar**( float )](../api/library/lights/class.lightworld_cpp.md#setShadowFilterFar_float_void)*


#### New Enums


- *[**SHADOW_CASCADE_ORIGIN_MODE**](../api/library/lights/class.lightworld_cpp.md#SHADOW_CASCADE_ORIGIN_MODE)*
- *[**SHADOW_CASCADE_PLACEMENT_MODE**](../api/library/lights/class.lightworld_cpp.md#SHADOW_CASCADE_PLACEMENT_MODE)*


## Material Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***OPTION_OVERLAP*** | Renamed. Use *[**OPTION_TRANSPARENT_ORDER**](../api/library/rendering/class.material_cpp.md#OPTION_TRANSPARENT_ORDER)* instead - see [Material Overlap Became Transparent Order](../upgrade/migration_api_cpp.md#transparent_order). |
| *[**createShaderCache**( bool, bool )](../api/library/rendering/class.material_cpp.md#createShaderCache_int_int_void)* | Set of arguments changed. |
| ***isOverlap**( )* | Removed. Use *[**getTransparentOrder**( )](../api/library/rendering/class.material_cpp.md#getTransparentOrder_int)* instead - see [Material Overlap Became Transparent Order](../upgrade/migration_api_cpp.md#transparent_order). |
| ***setOverlap**( bool )* | Removed. Use *[**setTransparentOrder**( Material::TRANSPARENT_ORDER )](../api/library/rendering/class.material_cpp.md#setTransparentOrder_int_void)* instead - see [Material Overlap Became Transparent Order](../upgrade/migration_api_cpp.md#transparent_order). |
| ***TEXTURE_SOURCE_GBUFFER_MATERIAL_MASK*** | Renamed. Use *[**TEXTURE_SOURCE_GBUFFER_SURFACE_ID**](../api/library/rendering/class.material_cpp.md#TEXTURE_SOURCE_GBUFFER_SURFACE_ID)* instead. |
| ***TEXTURE_SOURCE_REFLECTION_CUBE*** | Removed. |


#### New Functions


- *[**createShaderCache**( bool, bool )](../api/library/rendering/class.material_cpp.md#createShaderCache_int_int_void)*
- *[**getFeatureBits**( )](../api/library/rendering/class.material_cpp.md#getFeatureBits_uint)*
- *[**getCustomParameterFloat**( const char * )](../api/library/rendering/class.material_cpp.md#getCustomParameterFloat_cstr_float)*
- *[**getCustomParameterFloat**( int )](../api/library/rendering/class.material_cpp.md#getCustomParameterFloat_int_float)*
- *[**getCustomParameterInt**( const char * )](../api/library/rendering/class.material_cpp.md#getCustomParameterInt_cstr_int)*
- *[**getCustomParameterInt**( int )](../api/library/rendering/class.material_cpp.md#getCustomParameterInt_int_int)*
- *[**getCustomParameterUInt**( const char * )](../api/library/rendering/class.material_cpp.md#getCustomParameterUInt_cstr_uint)*
- *[**getCustomParameterUInt**( int )](../api/library/rendering/class.material_cpp.md#getCustomParameterUInt_int_uint)*
- *[**getTexture**( int, float )](../api/library/rendering/class.material_cpp.md#getTexture_int_float_Texture)*
- *[**isCustomParameterOverridden**( int )](../api/library/rendering/class.material_cpp.md#isCustomParameterOverridden_int_int)*
- *[**isCustomParametersSupported**( )](../api/library/rendering/class.material_cpp.md#isCustomParametersSupported_int)*
- *[**getMaterialID**( )](../api/library/rendering/class.material_cpp.md#getMaterialID_uint)*
- *[**resetCustomParameter**( int )](../api/library/rendering/class.material_cpp.md#resetCustomParameter_int_void)*
- *[**resetCustomParameters**( )](../api/library/rendering/class.material_cpp.md#resetCustomParameters_void)*
- *[**setCustomParameterFloat**( const char *, float )](../api/library/rendering/class.material_cpp.md#setCustomParameterFloat_cstr_float_void)*
- *[**setCustomParameterFloat**( int, float )](../api/library/rendering/class.material_cpp.md#setCustomParameterFloat_int_float_void)*
- *[**setCustomParameterInt**( const char *, int )](../api/library/rendering/class.material_cpp.md#setCustomParameterInt_cstr_int_void)*
- *[**setCustomParameterInt**( int, int )](../api/library/rendering/class.material_cpp.md#setCustomParameterInt_int_int_void)*
- *[**setCustomParameterUInt**( const char *, unsigned int )](../api/library/rendering/class.material_cpp.md#setCustomParameterUInt_cstr_uint_void)*
- *[**setCustomParameterUInt**( int, unsigned int )](../api/library/rendering/class.material_cpp.md#setCustomParameterUInt_int_uint_void)*
- *[**getTransparentOrder**( )](../api/library/rendering/class.material_cpp.md#getTransparentOrder_int)*
- *[**setTransparentOrder**( Material::TRANSPARENT_ORDER )](../api/library/rendering/class.material_cpp.md#setTransparentOrder_int_void)*


#### New Enums


- *[**OPTION_TRANSPARENT_ORDER**](../api/library/rendering/class.material_cpp.md#OPTION_TRANSPARENT_ORDER)*
- *[**TEXTURE_SOURCE_GBUFFER_REACTIVE_MASK**](../api/library/rendering/class.material_cpp.md#TEXTURE_SOURCE_GBUFFER_REACTIVE_MASK)*
- *[**TRANSPARENT_ORDER**](../api/library/rendering/class.material_cpp.md#TRANSPARENT_ORDER)*
- *[**TEXTURE_SOURCE_GBUFFER_SURFACE_ID**](../api/library/rendering/class.material_cpp.md#TEXTURE_SOURCE_GBUFFER_SURFACE_ID)*
- *[**TEXTURE_SOURCE_LINEAR_DEPTH_OLD**](../api/library/rendering/class.material_cpp.md#TEXTURE_SOURCE_LINEAR_DEPTH_OLD)*
- *[**TEXTURE_SOURCE_MIXED_REALITY_BLEND_MASK_COLOR**](../api/library/rendering/class.material_cpp.md#TEXTURE_SOURCE_MIXED_REALITY_BLEND_MASK_COLOR)*
- *[**TEXTURE_SOURCE_SURFACE_ID_DECAL**](../api/library/rendering/class.material_cpp.md#TEXTURE_SOURCE_SURFACE_ID_DECAL)*
- *[**TEXTURE_SOURCE_SURFACE_ID_SCENE**](../api/library/rendering/class.material_cpp.md#TEXTURE_SOURCE_SURFACE_ID_SCENE)*
- *[**TEXTURE_SOURCE_SURFACE_ID_TRANSPARENT**](../api/library/rendering/class.material_cpp.md#TEXTURE_SOURCE_SURFACE_ID_TRANSPARENT)*
- *[**TEXTURE_SOURCE_VISUALIZER_QUAD_OVERDRAW**](../api/library/rendering/class.material_cpp.md#TEXTURE_SOURCE_VISUALIZER_QUAD_OVERDRAW)*
- *[**TEXTURE_SOURCE_VISUALIZER_VERTEX_DENSITY**](../api/library/rendering/class.material_cpp.md#TEXTURE_SOURCE_VISUALIZER_VERTEX_DENSITY)*
- *[**TEXTURE_SOURCE_WBUFFER_CAUSTICS**](../api/library/rendering/class.material_cpp.md#TEXTURE_SOURCE_WBUFFER_CAUSTICS)*
- *[**MATERIAL_ID**](../api/library/rendering/class.material_cpp.md#MATERIAL_ID)*


## Materials Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***createShaderCache**( )* | Removed. Use *[**createShaderCacheAsync**( )](../api/library/rendering/class.materials_cpp.md#createShaderCacheAsync_void)* and *[**createShaderCacheForce**( )](../api/library/rendering/class.materials_cpp.md#createShaderCacheForce_void)* instead. |


#### New Functions


- *[**createShaderCacheAsync**( )](../api/library/rendering/class.materials_cpp.md#createShaderCacheAsync_void)*
- *[**createShaderCacheForce**( )](../api/library/rendering/class.materials_cpp.md#createShaderCacheForce_void)*
- *[**getMaterialFeatureBits**( unsigned int )](../api/library/rendering/class.materials_cpp.md#getMaterialFeatureBits_uint_uint)*
- *[**getMaterialMask**( unsigned int )](../api/library/rendering/class.materials_cpp.md#getMaterialMask_uint_uint)*
- *[**getMaterialParameters**( )](../api/library/rendering/class.materials_cpp.md#getMaterialParameters_CustomParameterLayout)*


## Math Common Functions


#### New Functions


- *[**logit**( float )](../api/library/math/math.common_cpp.md#logit_float_float)*
- *[**logit**( double )](../api/library/math/math.common_cpp.md#logit_double_double)*
- *[**sigmoid**( float )](../api/library/math/math.common_cpp.md#sigmoid_float_float)*
- *[**sigmoid**( double )](../api/library/math/math.common_cpp.md#sigmoid_double_double)*


## NavigationMesh Class


#### New Functions


- *[**getBakeSettings**( )](../api/library/pathfinding/class.navigationmesh_cpp.md#getBakeSettings_ExperimentalNavigationBakeSettings)*


## Node Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***NODE_ANIMATION_PLAYBACK*** | Renamed. Use *[**NODE_SEQUENCE_PLAYER**](../api/library/nodes/class.node_cpp.md#NODE_SEQUENCE_PLAYER)* instead. |


#### New Functions


- *[**isExperimentalNavigation**( )](../api/library/nodes/class.node_cpp.md#isExperimentalNavigation_int)*


#### New Enums


- *[**EXPERIMENTAL_NAVIGATION_BEGIN**](../api/library/nodes/class.node_cpp.md#EXPERIMENTAL_NAVIGATION_BEGIN)*
- *[**EXPERIMENTAL_NAVIGATION_END**](../api/library/nodes/class.node_cpp.md#EXPERIMENTAL_NAVIGATION_END)*
- *[**EXPERIMENTAL_NAVIGATION_MESH**](../api/library/nodes/class.node_cpp.md#EXPERIMENTAL_NAVIGATION_MESH)*
- *[**EXPERIMENTAL_NAVIGATION_MESH_AREA_VOLUME**](../api/library/nodes/class.node_cpp.md#EXPERIMENTAL_NAVIGATION_MESH_AREA_VOLUME)*
- *[**EXPERIMENTAL_NAVIGATION_MESH_INVOKER**](../api/library/nodes/class.node_cpp.md#EXPERIMENTAL_NAVIGATION_MESH_INVOKER)*
- *[**NODE_SEQUENCE_PLAYER**](../api/library/nodes/class.node_cpp.md#NODE_SEQUENCE_PLAYER)*


## NodeSkeletonPose Class


#### New Functions


- *[**getLayerJointObjectTransform**( int, int )](../api/library/nodes/class.nodeskeletonpose_cpp.md#getLayerJointObjectTransform_int_int_mat4)*
- *[**isLayerAnimationStreaming**( int )](../api/library/nodes/class.nodeskeletonpose_cpp.md#isLayerAnimationStreaming_int_int)*
- *[**renderLayerIKChainDebug**( int, const Ptr<ConstIKInfoChain> &, const Math::Mat4 & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#renderLayerIKChainDebug_int_IKInfoChain_Mat4_void)*
- *[**renderLayerJointConeAsymLimitDebug**( int, const Ptr<ConstJointLimitInfoConeAsym> &, const Math::Mat4 & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#renderLayerJointConeAsymLimitDebug_int_JointLimitInfoConeAsym_Mat4_void)*
- *[**renderLayerJointConeAsymTwistLimitDebug**( int, const Ptr<ConstJointLimitInfoConeAsymTwist> &, const Math::Mat4 & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#renderLayerJointConeAsymTwistLimitDebug_int_JointLimitInfoConeAsymTwist_Mat4_void)*
- *[**renderLayerJointConeLimitDebug**( int, const Ptr<ConstJointLimitInfoCone> &, const Math::Mat4 & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#renderLayerJointConeLimitDebug_int_JointLimitInfoCone_Mat4_void)*
- *[**renderLayerJointConeTwistLimitDebug**( int, const Ptr<ConstJointLimitInfoConeTwist> &, const Math::Mat4 & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#renderLayerJointConeTwistLimitDebug_int_JointLimitInfoConeTwist_Mat4_void)*
- *[**renderLayerJointHingeLimitDebug**( int, const Ptr<ConstJointLimitInfoHinge> &, const Math::Mat4 & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#renderLayerJointHingeLimitDebug_int_JointLimitInfoHinge_Mat4_void)*
- *[**renderLayerJointHingeTwistLimitDebug**( int, const Ptr<ConstJointLimitInfoHingeTwist> &, const Math::Mat4 & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#renderLayerJointHingeTwistLimitDebug_int_JointLimitInfoHingeTwist_Mat4_void)*
- *[**renderLayerJointLimitSetDebug**( int, const Ptr<ConstJointLimitSetInfo> &, const Math::Mat4 & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#renderLayerJointLimitSetDebug_int_JointLimitSetInfo_Mat4_void)*
- *[**renderLayerJointTwistLimitDebug**( int, const Ptr<ConstJointLimitInfoTwist> &, const Math::Mat4 & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#renderLayerJointTwistLimitDebug_int_JointLimitInfoTwist_Mat4_void)*
- *[**renderLayerLookAtChainDebug**( int, const Ptr<ConstLookAtChainInfo> &, const Math::Mat4 & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#renderLayerLookAtChainDebug_int_LookAtChainInfo_Mat4_void)*
- *[**renderLayerLookAtDebug**( int, const Ptr<ConstLookAtInfo> &, const Math::Mat4 & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#renderLayerLookAtDebug_int_LookAtInfo_Mat4_void)*
- *[**renderLayerTwoBoneIKDebug**( int, const Ptr<ConstIKInfoTwoBone> &, const Math::Mat4 & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#renderLayerTwoBoneIKDebug_int_IKInfoTwoBone_Mat4_void)*
- *[**setLayerJointObjectTransform**( int, int, const Math::mat4 & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#setLayerJointObjectTransform_int_int_mat4_void)*
- *[**setLayerJointObjectTransformPreserveChildren**( int, int, const Math::mat4 & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#setLayerJointObjectTransformPreserveChildren_int_int_mat4_void)*
- *[**solveLayerIKChain**( int, const Ptr<ConstIKInfoChain> & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerIKChain_int_IKInfoChain_void)*
- *[**solveLayerJointConeAsymLimit**( int, const Ptr<ConstJointLimitInfoConeAsym> & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerJointConeAsymLimit_int_JointLimitInfoConeAsym_void)*
- *[**solveLayerJointConeAsymTwistLimit**( int, const Ptr<ConstJointLimitInfoConeAsymTwist> & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerJointConeAsymTwistLimit_int_JointLimitInfoConeAsymTwist_void)*
- *[**solveLayerJointConeLimit**( int, const Ptr<ConstJointLimitInfoCone> & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerJointConeLimit_int_JointLimitInfoCone_void)*
- *[**solveLayerJointConeTwistLimit**( int, const Ptr<ConstJointLimitInfoConeTwist> & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerJointConeTwistLimit_int_JointLimitInfoConeTwist_void)*
- *[**solveLayerJointHingeLimit**( int, const Ptr<ConstJointLimitInfoHinge> & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerJointHingeLimit_int_JointLimitInfoHinge_void)*
- *[**solveLayerJointHingeTwistLimit**( int, const Ptr<ConstJointLimitInfoHingeTwist> & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerJointHingeTwistLimit_int_JointLimitInfoHingeTwist_void)*
- *[**solveLayerJointTwistLimit**( int, const Ptr<ConstJointLimitInfoTwist> & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerJointTwistLimit_int_JointLimitInfoTwist_void)*
- *[**solveLayerLookAt**( int, const Ptr<ConstLookAtInfo> & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerLookAt_int_LookAtInfo_void)*
- *[**solveLayerLookAtChain**( int, const Ptr<ConstLookAtChainInfo> & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerLookAtChain_int_LookAtChainInfo_void)*
- *[**solveLayerTwoBoneIK**( int, const Ptr<ConstIKInfoTwoBone> & )](../api/library/nodes/class.nodeskeletonpose_cpp.md#solveLayerTwoBoneIK_int_IKInfoTwoBone_void)*


## ObjectCloudLayer Class


#### New Functions


- *[**getCloudspaceTransform**( )](../api/library/objects/class.objectcloudlayer_cpp.md#getCloudspaceTransform_Mat4)*
- *[**setCloudspaceTransform**( const Math::Mat4 & )](../api/library/objects/class.objectcloudlayer_cpp.md#setCloudspaceTransform_Mat4_void)*


## ObjectMeshSkinned Class


#### New Functions


- *[**loadAsyncRender**( )](../api/library/objects/class.objectmeshskinned_cpp.md#loadAsyncRender_int)*
- *[**loadForceRender**( )](../api/library/objects/class.objectmeshskinned_cpp.md#loadForceRender_int)*


## ObjectMeshSkinnedLegacy Class


#### New Functions


- *[**isLayerAnimationStreaming**( int )](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md#isLayerAnimationStreaming_int_int)*
- *[**loadAsyncRender**( )](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md#loadAsyncRender_int)*
- *[**loadForceRender**( )](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md#loadForceRender_int)*
- *[**resetLayerToBindPose**( int )](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md#resetLayerToBindPose_int_void)*
- *[**resetLayerToRestPose**( int )](../api/library/objects/class.objectmeshskinnedlegacy_cpp.md#resetLayerToRestPose_int_void)*


## ObjectText Class


#### New Functions


- *[**getTextDirection**( )](../api/library/objects/class.objecttext_cpp.md#getTextDirection_int)*
- *[**setTextDirection**( Gui::TextDirection )](../api/library/objects/class.objecttext_cpp.md#setTextDirection_int_void)*


## Profiler Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| *[**setValue**( const char *, const char *, float, float, float *, Profiler::COUNTER_VR_FLAG, bool )](../api/library/engine/class.profiler_cpp.md#setValue_cstr_cstr_float_float_float_int_int_void)* | Set of arguments changed. |
| *[**setValue**( const char *, const char *, int, int, float *, Profiler::COUNTER_VR_FLAG, bool )](../api/library/engine/class.profiler_cpp.md#setValue_cstr_cstr_int_int_float_int_int_void)* | Set of arguments changed. |


#### New Functions


- *[**setValue**( const char *, const char *, float, float, float *, Profiler::COUNTER_VR_FLAG, bool )](../api/library/engine/class.profiler_cpp.md#setValue_cstr_cstr_float_float_float_int_int_void)*
- *[**setValue**( const char *, const char *, int, int, float *, Profiler::COUNTER_VR_FLAG, bool )](../api/library/engine/class.profiler_cpp.md#setValue_cstr_cstr_int_int_float_int_int_void)*


#### New Enums


- *[**COUNTER_VR_FLAG**](../api/library/engine/class.profiler_cpp.md#COUNTER_VR_FLAG)*


## Property Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***setFileGUID**( const UGUID & )* | Return value type changed. |
| ***setFilePath**( const char * )* | Return value type changed. |


#### New Enums


- *[**PARAMETER_MASK_EXPERIMENTAL_NAVIGATION_BAKE**](../api/library/common/class.property_cpp.md#PARAMETER_MASK_EXPERIMENTAL_NAVIGATION_BAKE)*


## Render Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| *[**addParameter**( const char *, Render::RENDER_PARAMETER, bool, const UGUID & )](../api/library/rendering/class.render_cpp.md#addParameter_cstr_int_int_UGUID_int)* | Set of arguments changed. |


#### New Functions


- *[**addParameter**( const char *, Render::RENDER_PARAMETER, bool, const UGUID & )](../api/library/rendering/class.render_cpp.md#addParameter_cstr_int_int_UGUID_int)*
- *[**calculateEngineRenderResolution**( int, int, const Math::ivec2 &, Math::ivec2 &, Math::ivec2 &, Math::ivec2 & )](../api/library/rendering/class.render_cpp.md#calculateEngineRenderResolution_int_int_ivec2_ivec2_ivec2_ivec2_void)*
- *[**cloneParameter**( int )](../api/library/rendering/class.render_cpp.md#cloneParameter_int_int)*
- *[**getDOFJitterSamples**( )](../api/library/rendering/class.render_cpp.md#getDOFJitterSamples_int)*
- *[**setDOFJitterSamples**( int )](../api/library/rendering/class.render_cpp.md#setDOFJitterSamples_int_void)*
- *[**getDOFMipmapByBlurIntensity**( )](../api/library/rendering/class.render_cpp.md#getDOFMipmapByBlurIntensity_float)*
- *[**setDOFMipmapByBlurIntensity**( float )](../api/library/rendering/class.render_cpp.md#setDOFMipmapByBlurIntensity_float_void)*
- *[**getDOFSamplingMode**( )](../api/library/rendering/class.render_cpp.md#getDOFSamplingMode_int)*
- *[**setDOFSamplingMode**( Render::DOF_SAMPLING_MODE )](../api/library/rendering/class.render_cpp.md#setDOFSamplingMode_int_void)*
- *[**getDOFTAAFrameCount**( )](../api/library/rendering/class.render_cpp.md#getDOFTAAFrameCount_float)*
- *[**setDOFTAAFrameCount**( float )](../api/library/rendering/class.render_cpp.md#setDOFTAAFrameCount_float_void)*
- *[**getDOFTAAFramesVelocityThreshold**( )](../api/library/rendering/class.render_cpp.md#getDOFTAAFramesVelocityThreshold_float)*
- *[**setDOFTAAFramesVelocityThreshold**( float )](../api/library/rendering/class.render_cpp.md#setDOFTAAFramesVelocityThreshold_float_void)*
- *[**isDynamicResolutionAlignmentEnabled**( )](../api/library/rendering/class.render_cpp.md#isDynamicResolutionAlignmentEnabled_int)*
- *[**setDynamicResolutionAlignmentEnabled**( bool )](../api/library/rendering/class.render_cpp.md#setDynamicResolutionAlignmentEnabled_int_void)*
- *[**getDynamicResolutionCooldownFrames**( )](../api/library/rendering/class.render_cpp.md#getDynamicResolutionCooldownFrames_int)*
- *[**setDynamicResolutionCooldownFrames**( int )](../api/library/rendering/class.render_cpp.md#setDynamicResolutionCooldownFrames_int_void)*
- *[**getDynamicResolutionDimension**( )](../api/library/rendering/class.render_cpp.md#getDynamicResolutionDimension_int)*
- *[**setDynamicResolutionDimension**( Render::RENDER_DYNAMIC_RESOLUTION_DIMENSION )](../api/library/rendering/class.render_cpp.md#setDynamicResolutionDimension_int_void)*
- *[**getDynamicResolutionDownFrames**( )](../api/library/rendering/class.render_cpp.md#getDynamicResolutionDownFrames_int)*
- *[**setDynamicResolutionDownFrames**( int )](../api/library/rendering/class.render_cpp.md#setDynamicResolutionDownFrames_int_void)*
- *[**getDynamicResolutionDownThreshold**( )](../api/library/rendering/class.render_cpp.md#getDynamicResolutionDownThreshold_float)*
- *[**setDynamicResolutionDownThreshold**( float )](../api/library/rendering/class.render_cpp.md#setDynamicResolutionDownThreshold_float_void)*
- *[**isDynamicResolutionEnabled**( )](../api/library/rendering/class.render_cpp.md#isDynamicResolutionEnabled_int)*
- *[**setDynamicResolutionEnabled**( bool )](../api/library/rendering/class.render_cpp.md#setDynamicResolutionEnabled_int_void)*
- *[**getDynamicResolutionScaleMax**( )](../api/library/rendering/class.render_cpp.md#getDynamicResolutionScaleMax_float)*
- *[**setDynamicResolutionScaleMax**( float )](../api/library/rendering/class.render_cpp.md#setDynamicResolutionScaleMax_float_void)*
- *[**getDynamicResolutionScaleMin**( )](../api/library/rendering/class.render_cpp.md#getDynamicResolutionScaleMin_float)*
- *[**setDynamicResolutionScaleMin**( float )](../api/library/rendering/class.render_cpp.md#setDynamicResolutionScaleMin_float_void)*
- *[**getDynamicResolutionStep**( )](../api/library/rendering/class.render_cpp.md#getDynamicResolutionStep_float)*
- *[**setDynamicResolutionStep**( float )](../api/library/rendering/class.render_cpp.md#setDynamicResolutionStep_float_void)*
- *[**getDynamicResolutionTargetFPS**( )](../api/library/rendering/class.render_cpp.md#getDynamicResolutionTargetFPS_int)*
- *[**setDynamicResolutionTargetFPS**( int )](../api/library/rendering/class.render_cpp.md#setDynamicResolutionTargetFPS_int_void)*
- *[**getDynamicResolutionUpFrames**( )](../api/library/rendering/class.render_cpp.md#getDynamicResolutionUpFrames_int)*
- *[**setDynamicResolutionUpFrames**( int )](../api/library/rendering/class.render_cpp.md#setDynamicResolutionUpFrames_int_void)*
- *[**getDynamicResolutionUpThreshold**( )](../api/library/rendering/class.render_cpp.md#getDynamicResolutionUpThreshold_float)*
- *[**setDynamicResolutionUpThreshold**( float )](../api/library/rendering/class.render_cpp.md#setDynamicResolutionUpThreshold_float_void)*
- *[**getDynamicResolutionWarmupFrames**( )](../api/library/rendering/class.render_cpp.md#getDynamicResolutionWarmupFrames_int)*
- *[**setDynamicResolutionWarmupFrames**( int )](../api/library/rendering/class.render_cpp.md#setDynamicResolutionWarmupFrames_int_void)*
- *[**getEnvironmentMoonAngularSize**( )](../api/library/rendering/class.render_cpp.md#getEnvironmentMoonAngularSize_float)*
- *[**getEnvironmentSunAngularSize**( )](../api/library/rendering/class.render_cpp.md#getEnvironmentSunAngularSize_float)*
- *[**getEventChangedParameters**( )](../api/library/rendering/class.render_cpp.md#getEventChangedParameters_Event)*
- *[**getEventStreamingAnimationLoaded**( )](../api/library/rendering/class.render_cpp.md#getEventStreamingAnimationLoaded_Event)*
- *[**getEventStreamingAnimationUnloaded**( )](../api/library/rendering/class.render_cpp.md#getEventStreamingAnimationUnloaded_Event)*
- *[**findParameter**( const char * )](../api/library/rendering/class.render_cpp.md#findParameter_cstr_int)*
- *[**getParameterBool**( const char * )](../api/library/rendering/class.render_cpp.md#getParameterBool_cstr_int)*
- *[**getParameterBool**( int )](../api/library/rendering/class.render_cpp.md#getParameterBool_int_int)*
- *[**getParameterDefineName**( int )](../api/library/rendering/class.render_cpp.md#getParameterDefineName_int_cstr)*
- *[**getParameterFloat**( const char * )](../api/library/rendering/class.render_cpp.md#getParameterFloat_cstr_float)*
- *[**getParameterFloat**( int )](../api/library/rendering/class.render_cpp.md#getParameterFloat_int_float)*
- *[**getParameterFloat2**( const char * )](../api/library/rendering/class.render_cpp.md#getParameterFloat2_cstr_vec2)*
- *[**getParameterFloat2**( int )](../api/library/rendering/class.render_cpp.md#getParameterFloat2_int_vec2)*
- *[**getParameterFloat3**( const char * )](../api/library/rendering/class.render_cpp.md#getParameterFloat3_cstr_vec3)*
- *[**getParameterFloat3**( int )](../api/library/rendering/class.render_cpp.md#getParameterFloat3_int_vec3)*
- *[**getParameterFloat4**( const char * )](../api/library/rendering/class.render_cpp.md#getParameterFloat4_cstr_vec4)*
- *[**getParameterFloat4**( int )](../api/library/rendering/class.render_cpp.md#getParameterFloat4_int_vec4)*
- *[**getParameterGUID**( int )](../api/library/rendering/class.render_cpp.md#getParameterGUID_int_UGUID)*
- *[**getParameterInt**( const char * )](../api/library/rendering/class.render_cpp.md#getParameterInt_cstr_int)*
- *[**getParameterInt**( int )](../api/library/rendering/class.render_cpp.md#getParameterInt_int_int)*
- *[**getParameterInt2**( const char * )](../api/library/rendering/class.render_cpp.md#getParameterInt2_cstr_ivec2)*
- *[**getParameterInt2**( int )](../api/library/rendering/class.render_cpp.md#getParameterInt2_int_ivec2)*
- *[**getParameterInt3**( const char * )](../api/library/rendering/class.render_cpp.md#getParameterInt3_cstr_ivec3)*
- *[**getParameterInt3**( int )](../api/library/rendering/class.render_cpp.md#getParameterInt3_int_ivec3)*
- *[**getParameterInt4**( const char * )](../api/library/rendering/class.render_cpp.md#getParameterInt4_cstr_ivec4)*
- *[**getParameterInt4**( int )](../api/library/rendering/class.render_cpp.md#getParameterInt4_int_ivec4)*
- *[**getParameterName**( int )](../api/library/rendering/class.render_cpp.md#getParameterName_int_cstr)*
- *[**getParameterShaderName**( int )](../api/library/rendering/class.render_cpp.md#getParameterShaderName_int_cstr)*
- *[**getParameterType**( int )](../api/library/rendering/class.render_cpp.md#getParameterType_int_int)*
- *[**getStreamingAnimationHoldCount**( const char * )](../api/library/rendering/class.render_cpp.md#getStreamingAnimationHoldCount_cstr_int)*
- *[**getStreamingAnimationHoldCount**( const UGUID & )](../api/library/rendering/class.render_cpp.md#getStreamingAnimationHoldCount_UGUID_int)*
- *[**holdStreamingAnimation**( const char * )](../api/library/rendering/class.render_cpp.md#holdStreamingAnimation_cstr_int)*
- *[**holdStreamingAnimation**( const UGUID & )](../api/library/rendering/class.render_cpp.md#holdStreamingAnimation_UGUID_int)*
- *[**isIndirectSpecularTemporalFilteringAngleDependence**( )](../api/library/rendering/class.render_cpp.md#isIndirectSpecularTemporalFilteringAngleDependence_int)*
- *[**setIndirectSpecularTemporalFilteringAngleDependence**( bool )](../api/library/rendering/class.render_cpp.md#setIndirectSpecularTemporalFilteringAngleDependence_int_void)*
- *[**getIndirectSpecularTemporalFilteringColorClampingGrazing**( )](../api/library/rendering/class.render_cpp.md#getIndirectSpecularTemporalFilteringColorClampingGrazing_float)*
- *[**setIndirectSpecularTemporalFilteringColorClampingGrazing**( float )](../api/library/rendering/class.render_cpp.md#setIndirectSpecularTemporalFilteringColorClampingGrazing_float_void)*
- *[**getIndirectSpecularTemporalFilteringFrameCountGrazing**( )](../api/library/rendering/class.render_cpp.md#getIndirectSpecularTemporalFilteringFrameCountGrazing_float)*
- *[**setIndirectSpecularTemporalFilteringFrameCountGrazing**( float )](../api/library/rendering/class.render_cpp.md#setIndirectSpecularTemporalFilteringFrameCountGrazing_float_void)*
- *[**isParameterDynamic**( int )](../api/library/rendering/class.render_cpp.md#isParameterDynamic_int_int)*
- *[**isParameterFloat**( int )](../api/library/rendering/class.render_cpp.md#isParameterFloat_int_int)*
- *[**isStreamingAnimationExist**( const char * )](../api/library/rendering/class.render_cpp.md#isStreamingAnimationExist_cstr_int)*
- *[**isStreamingAnimationExist**( const UGUID & )](../api/library/rendering/class.render_cpp.md#isStreamingAnimationExist_UGUID_int)*
- *[**isStreamingAnimationHeld**( const char * )](../api/library/rendering/class.render_cpp.md#isStreamingAnimationHeld_cstr_int)*
- *[**isStreamingAnimationHeld**( const UGUID & )](../api/library/rendering/class.render_cpp.md#isStreamingAnimationHeld_UGUID_int)*
- *[**isStreamingAnimationLoaded**( const char * )](../api/library/rendering/class.render_cpp.md#isStreamingAnimationLoaded_cstr_int)*
- *[**isStreamingAnimationLoaded**( const UGUID & )](../api/library/rendering/class.render_cpp.md#isStreamingAnimationLoaded_UGUID_int)*
- *[**isValidSurfaceMaterialParameterName**( const char * )](../api/library/rendering/class.render_cpp.md#isValidSurfaceMaterialParameterName_cstr_int)*
- *[**loadStreamingAnimationAsync**( const char * )](../api/library/rendering/class.render_cpp.md#loadStreamingAnimationAsync_cstr_ConstMeshSkinnedAnimation)*
- *[**loadStreamingAnimationAsync**( const UGUID & )](../api/library/rendering/class.render_cpp.md#loadStreamingAnimationAsync_UGUID_ConstMeshSkinnedAnimation)*
- *[**loadStreamingAnimationForce**( const char * )](../api/library/rendering/class.render_cpp.md#loadStreamingAnimationForce_cstr_ConstMeshSkinnedAnimation)*
- *[**loadStreamingAnimationForce**( const UGUID & )](../api/library/rendering/class.render_cpp.md#loadStreamingAnimationForce_UGUID_ConstMeshSkinnedAnimation)*
- *[**getLocalTonemapperDetailContrastIntensity**( )](../api/library/rendering/class.render_cpp.md#getLocalTonemapperDetailContrastIntensity_float)*
- *[**setLocalTonemapperDetailContrastIntensity**( float )](../api/library/rendering/class.render_cpp.md#setLocalTonemapperDetailContrastIntensity_float_void)*
- *[**getLocalTonemapperDetailContrastRadius**( )](../api/library/rendering/class.render_cpp.md#getLocalTonemapperDetailContrastRadius_int)*
- *[**setLocalTonemapperDetailContrastRadius**( int )](../api/library/rendering/class.render_cpp.md#setLocalTonemapperDetailContrastRadius_int_void)*
- *[**isLocalTonemapperUseDetailContrast**( )](../api/library/rendering/class.render_cpp.md#isLocalTonemapperUseDetailContrast_int)*
- *[**setLocalTonemapperUseDetailContrast**( bool )](../api/library/rendering/class.render_cpp.md#setLocalTonemapperUseDetailContrast_int_void)*
- *[**moveParameter**( int, int )](../api/library/rendering/class.render_cpp.md#moveParameter_int_int_void)*
- *[**getNumParameters**( )](../api/library/rendering/class.render_cpp.md#getNumParameters_int)*
- *[**getPanoramaFisheyeKannalaBrandtChromaticAberration**( )](../api/library/rendering/class.render_cpp.md#getPanoramaFisheyeKannalaBrandtChromaticAberration_float)*
- *[**setPanoramaFisheyeKannalaBrandtChromaticAberration**( float )](../api/library/rendering/class.render_cpp.md#setPanoramaFisheyeKannalaBrandtChromaticAberration_float_void)*
- *[**getPanoramaFisheyeKannalaBrandtCoefficients**( )](../api/library/rendering/class.render_cpp.md#getPanoramaFisheyeKannalaBrandtCoefficients_vec4)*
- *[**setPanoramaFisheyeKannalaBrandtCoefficients**( const Math::vec4 & )](../api/library/rendering/class.render_cpp.md#setPanoramaFisheyeKannalaBrandtCoefficients_vec4_void)*
- *[**getPanoramaFisheyeKannalaBrandtFocalLength**( )](../api/library/rendering/class.render_cpp.md#getPanoramaFisheyeKannalaBrandtFocalLength_vec2)*
- *[**setPanoramaFisheyeKannalaBrandtFocalLength**( const Math::vec2 & )](../api/library/rendering/class.render_cpp.md#setPanoramaFisheyeKannalaBrandtFocalLength_vec2_void)*
- *[**getPanoramaFisheyeKannalaBrandtImageCircleRadius**( )](../api/library/rendering/class.render_cpp.md#getPanoramaFisheyeKannalaBrandtImageCircleRadius_float)*
- *[**setPanoramaFisheyeKannalaBrandtImageCircleRadius**( float )](../api/library/rendering/class.render_cpp.md#setPanoramaFisheyeKannalaBrandtImageCircleRadius_float_void)*
- *[**getPanoramaFisheyeKannalaBrandtImageDimensions**( )](../api/library/rendering/class.render_cpp.md#getPanoramaFisheyeKannalaBrandtImageDimensions_vec2)*
- *[**setPanoramaFisheyeKannalaBrandtImageDimensions**( const Math::vec2 & )](../api/library/rendering/class.render_cpp.md#setPanoramaFisheyeKannalaBrandtImageDimensions_vec2_void)*
- *[**getPanoramaFisheyeKannalaBrandtPrincipalPoint**( )](../api/library/rendering/class.render_cpp.md#getPanoramaFisheyeKannalaBrandtPrincipalPoint_vec2)*
- *[**setPanoramaFisheyeKannalaBrandtPrincipalPoint**( const Math::vec2 & )](../api/library/rendering/class.render_cpp.md#setPanoramaFisheyeKannalaBrandtPrincipalPoint_vec2_void)*
- *[**getPanoramaFisheyeKannalaBrandtSkew**( )](../api/library/rendering/class.render_cpp.md#getPanoramaFisheyeKannalaBrandtSkew_float)*
- *[**setPanoramaFisheyeKannalaBrandtSkew**( float )](../api/library/rendering/class.render_cpp.md#setPanoramaFisheyeKannalaBrandtSkew_float_void)*
- *[**getPanoramaFisheyeKannalaBrandtTangentialDistortion**( )](../api/library/rendering/class.render_cpp.md#getPanoramaFisheyeKannalaBrandtTangentialDistortion_vec2)*
- *[**setPanoramaFisheyeKannalaBrandtTangentialDistortion**( const Math::vec2 & )](../api/library/rendering/class.render_cpp.md#setPanoramaFisheyeKannalaBrandtTangentialDistortion_vec2_void)*
- *[**getPanoramaFisheyeKannalaBrandtVignettingCoefficient5**( )](../api/library/rendering/class.render_cpp.md#getPanoramaFisheyeKannalaBrandtVignettingCoefficient5_float)*
- *[**setPanoramaFisheyeKannalaBrandtVignettingCoefficient5**( float )](../api/library/rendering/class.render_cpp.md#setPanoramaFisheyeKannalaBrandtVignettingCoefficient5_float_void)*
- *[**getPanoramaFisheyeKannalaBrandtVignettingCoefficients**( )](../api/library/rendering/class.render_cpp.md#getPanoramaFisheyeKannalaBrandtVignettingCoefficients_vec4)*
- *[**setPanoramaFisheyeKannalaBrandtVignettingCoefficients**( const Math::vec4 & )](../api/library/rendering/class.render_cpp.md#setPanoramaFisheyeKannalaBrandtVignettingCoefficients_vec4_void)*
- *[**isPanoramaForceDisableScreenSpaceEffects**( )](../api/library/rendering/class.render_cpp.md#isPanoramaForceDisableScreenSpaceEffects_int)*
- *[**setPanoramaForceDisableScreenSpaceEffects**( bool )](../api/library/rendering/class.render_cpp.md#setPanoramaForceDisableScreenSpaceEffects_int_void)*
- *[**removeParameter**( int )](../api/library/rendering/class.render_cpp.md#removeParameter_int_void)*
- *[RENDER_DYNAMIC_RESOLUTION_DIMENSION_HORIZONTAL](../api/library/rendering/class.render_cpp.md#RENDER_DYNAMIC_RESOLUTION_DIMENSION_HORIZONTAL)*
- *[RENDER_DYNAMIC_RESOLUTION_DIMENSION_UNIFORM](../api/library/rendering/class.render_cpp.md#RENDER_DYNAMIC_RESOLUTION_DIMENSION_UNIFORM)*
- *[RENDER_DYNAMIC_RESOLUTION_DIMENSION_VERTICAL](../api/library/rendering/class.render_cpp.md#RENDER_DYNAMIC_RESOLUTION_DIMENSION_VERTICAL)*
- *[RENDER_PARAMETER_BOOL](../api/library/rendering/class.render_cpp.md#RENDER_PARAMETER_BOOL)*
- *[RENDER_PARAMETER_FLOAT](../api/library/rendering/class.render_cpp.md#RENDER_PARAMETER_FLOAT)*
- *[RENDER_PARAMETER_FLOAT2](../api/library/rendering/class.render_cpp.md#RENDER_PARAMETER_FLOAT2)*
- *[RENDER_PARAMETER_FLOAT3](../api/library/rendering/class.render_cpp.md#RENDER_PARAMETER_FLOAT3)*
- *[RENDER_PARAMETER_FLOAT4](../api/library/rendering/class.render_cpp.md#RENDER_PARAMETER_FLOAT4)*
- *[RENDER_PARAMETER_INT](../api/library/rendering/class.render_cpp.md#RENDER_PARAMETER_INT)*
- *[RENDER_PARAMETER_INT2](../api/library/rendering/class.render_cpp.md#RENDER_PARAMETER_INT2)*
- *[RENDER_PARAMETER_INT3](../api/library/rendering/class.render_cpp.md#RENDER_PARAMETER_INT3)*
- *[RENDER_PARAMETER_INT4](../api/library/rendering/class.render_cpp.md#RENDER_PARAMETER_INT4)*
- *[**resetStreamingAnimationHold**( const char * )](../api/library/rendering/class.render_cpp.md#resetStreamingAnimationHold_cstr_void)*
- *[**resetStreamingAnimationHold**( const UGUID & )](../api/library/rendering/class.render_cpp.md#resetStreamingAnimationHold_UGUID_void)*
- *[**setParameterBool**( const char *, bool )](../api/library/rendering/class.render_cpp.md#setParameterBool_cstr_int_void)*
- *[**setParameterBool**( int, bool )](../api/library/rendering/class.render_cpp.md#setParameterBool_int_int_void)*
- *[**setParameterDynamic**( int, bool )](../api/library/rendering/class.render_cpp.md#setParameterDynamic_int_int_void)*
- *[**setParameterFloat**( const char *, float )](../api/library/rendering/class.render_cpp.md#setParameterFloat_cstr_float_void)*
- *[**setParameterFloat**( int, float )](../api/library/rendering/class.render_cpp.md#setParameterFloat_int_float_void)*
- *[**setParameterFloat2**( const char *, const Math::vec2 & )](../api/library/rendering/class.render_cpp.md#setParameterFloat2_cstr_vec2_void)*
- *[**setParameterFloat2**( int, const Math::vec2 & )](../api/library/rendering/class.render_cpp.md#setParameterFloat2_int_vec2_void)*
- *[**setParameterFloat3**( const char *, const Math::vec3 & )](../api/library/rendering/class.render_cpp.md#setParameterFloat3_cstr_vec3_void)*
- *[**setParameterFloat3**( int, const Math::vec3 & )](../api/library/rendering/class.render_cpp.md#setParameterFloat3_int_vec3_void)*
- *[**setParameterFloat4**( const char *, const Math::vec4 & )](../api/library/rendering/class.render_cpp.md#setParameterFloat4_cstr_vec4_void)*
- *[**setParameterFloat4**( int, const Math::vec4 & )](../api/library/rendering/class.render_cpp.md#setParameterFloat4_int_vec4_void)*
- *[**setParameterInt**( const char *, int )](../api/library/rendering/class.render_cpp.md#setParameterInt_cstr_int_void)*
- *[**setParameterInt**( int, int )](../api/library/rendering/class.render_cpp.md#setParameterInt_int_int_void)*
- *[**setParameterInt2**( const char *, const Math::ivec2 & )](../api/library/rendering/class.render_cpp.md#setParameterInt2_cstr_ivec2_void)*
- *[**setParameterInt2**( int, const Math::ivec2 & )](../api/library/rendering/class.render_cpp.md#setParameterInt2_int_ivec2_void)*
- *[**setParameterInt3**( const char *, const Math::ivec3 & )](../api/library/rendering/class.render_cpp.md#setParameterInt3_cstr_ivec3_void)*
- *[**setParameterInt3**( int, const Math::ivec3 & )](../api/library/rendering/class.render_cpp.md#setParameterInt3_int_ivec3_void)*
- *[**setParameterInt4**( const char *, const Math::ivec4 & )](../api/library/rendering/class.render_cpp.md#setParameterInt4_cstr_ivec4_void)*
- *[**setParameterInt4**( int, const Math::ivec4 & )](../api/library/rendering/class.render_cpp.md#setParameterInt4_int_ivec4_void)*
- *[**setParameterName**( int, const char * )](../api/library/rendering/class.render_cpp.md#setParameterName_int_cstr_void)*
- *[**setParameterType**( int, Render::RENDER_PARAMETER )](../api/library/rendering/class.render_cpp.md#setParameterType_int_int_void)*
- *[**getSkyOffset**( )](../api/library/rendering/class.render_cpp.md#getSkyOffset_float)*
- *[**setSkyOffset**( float )](../api/library/rendering/class.render_cpp.md#setSkyOffset_float_void)*
- *[**getStreamingAnimationCacheRAM**( )](../api/library/rendering/class.render_cpp.md#getStreamingAnimationCacheRAM_int)*
- *[**setStreamingAnimationCacheRAM**( int )](../api/library/rendering/class.render_cpp.md#setStreamingAnimationCacheRAM_int_void)*
- *[**getStreamingAnimationsMode**( )](../api/library/rendering/class.render_cpp.md#getStreamingAnimationsMode_int)*
- *[**setStreamingAnimationsMode**( Render::STREAMING_MODE )](../api/library/rendering/class.render_cpp.md#setStreamingAnimationsMode_int_void)*
- *[**getStreamingMeshCacheRAM**( )](../api/library/rendering/class.render_cpp.md#getStreamingMeshCacheRAM_int)*
- *[**setStreamingMeshCacheRAM**( int )](../api/library/rendering/class.render_cpp.md#setStreamingMeshCacheRAM_int_void)*
- *[**getStreamingMeshCacheVRAM**( )](../api/library/rendering/class.render_cpp.md#getStreamingMeshCacheVRAM_int)*
- *[**setStreamingMeshCacheVRAM**( int )](../api/library/rendering/class.render_cpp.md#setStreamingMeshCacheVRAM_int_void)*
- *[**getStreamingMeshSkinnedCacheRAM**( )](../api/library/rendering/class.render_cpp.md#getStreamingMeshSkinnedCacheRAM_int)*
- *[**setStreamingMeshSkinnedCacheRAM**( int )](../api/library/rendering/class.render_cpp.md#setStreamingMeshSkinnedCacheRAM_int_void)*
- *[**getStreamingMeshSkinnedCacheVRAM**( )](../api/library/rendering/class.render_cpp.md#getStreamingMeshSkinnedCacheVRAM_int)*
- *[**setStreamingMeshSkinnedCacheVRAM**( int )](../api/library/rendering/class.render_cpp.md#setStreamingMeshSkinnedCacheVRAM_int_void)*
- *[**getStreamingTextureCacheVRAM**( )](../api/library/rendering/class.render_cpp.md#getStreamingTextureCacheVRAM_int)*
- *[**setStreamingTextureCacheVRAM**( int )](../api/library/rendering/class.render_cpp.md#setStreamingTextureCacheVRAM_int_void)*
- *[**isSurfaceIDMultilayered**( )](../api/library/rendering/class.render_cpp.md#isSurfaceIDMultilayered_int)*
- *[**setSurfaceIDMultilayered**( bool )](../api/library/rendering/class.render_cpp.md#setSurfaceIDMultilayered_int_void)*
- *[**getSurfaceParameters**( )](../api/library/rendering/class.render_cpp.md#getSurfaceParameters_CustomParameterLayout)*
- *[**swapParameters**( int, int )](../api/library/rendering/class.render_cpp.md#swapParameters_int_int_void)*
- *[**unholdStreamingAnimation**( const char * )](../api/library/rendering/class.render_cpp.md#unholdStreamingAnimation_cstr_int)*
- *[**unholdStreamingAnimation**( const UGUID & )](../api/library/rendering/class.render_cpp.md#unholdStreamingAnimation_UGUID_int)*
- *[VIEWPORT_MODE_PANORAMA_FISHEYE_KANNALA_BRANDT](../api/library/rendering/class.render_cpp.md#VIEWPORT_MODE_PANORAMA_FISHEYE_KANNALA_BRANDT)*
- *[**getWaterGeometryProgressionFovMin**( )](../api/library/rendering/class.render_cpp.md#getWaterGeometryProgressionFovMin_float)*
- *[**setWaterGeometryProgressionFovMin**( float )](../api/library/rendering/class.render_cpp.md#setWaterGeometryProgressionFovMin_float_void)*
- *[**getWaterGeometryProgressionFovScale**( )](../api/library/rendering/class.render_cpp.md#getWaterGeometryProgressionFovScale_float)*
- *[**setWaterGeometryProgressionFovScale**( float )](../api/library/rendering/class.render_cpp.md#setWaterGeometryProgressionFovScale_float_void)*


#### New Enums


- *[**VIEWPORT_MODE_PANORAMA_FISHEYE_KANNALA_BRANDT**](../api/library/rendering/class.render_cpp.md#VIEWPORT_MODE_PANORAMA_FISHEYE_KANNALA_BRANDT)*
- *[**DOF_SAMPLING_MODE**](../api/library/rendering/class.render_cpp.md#DOF_SAMPLING_MODE)*
- *[**RENDER_DYNAMIC_RESOLUTION_DIMENSION**](../api/library/rendering/class.render_cpp.md#RENDER_DYNAMIC_RESOLUTION_DIMENSION)*
- *[**SURFACE_ID**](../api/library/rendering/class.render_cpp.md#SURFACE_ID)*


## RenderEnvironmentPreset Class


#### New Functions


- *[**getHazePhysicalVisibilityThreshold**( )](../api/library/rendering/class.renderenvironmentpreset_cpp.md#getHazePhysicalVisibilityThreshold_float)*
- *[**setHazePhysicalVisibilityThreshold**( float )](../api/library/rendering/class.renderenvironmentpreset_cpp.md#setHazePhysicalVisibilityThreshold_float_void)*


## Renderer Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***getTextureGBufferMaterialMask**( )* | Renamed. Use *[**getTextureGBufferSurfaceID**](../api/library/rendering/class.renderer_cpp.md#getTextureGBufferSurfaceID_Texture)* instead. |


#### New Functions


- *[**getOutputResolution**( )](../api/library/rendering/class.renderer_cpp.md#getOutputResolution_ivec2)*
- *[**getRenderResolution**( )](../api/library/rendering/class.renderer_cpp.md#getRenderResolution_ivec2)*
- *[**getRenderResolutionMax**( )](../api/library/rendering/class.renderer_cpp.md#getRenderResolutionMax_ivec2)*
- *[**getRenderResolutionMin**( )](../api/library/rendering/class.renderer_cpp.md#getRenderResolutionMin_ivec2)*
- *[**getTextureGBufferReactiveMask**( )](../api/library/rendering/class.renderer_cpp.md#getTextureGBufferReactiveMask_Texture)*
- *[**getTextureGBufferSurfaceID**( )](../api/library/rendering/class.renderer_cpp.md#getTextureGBufferSurfaceID_Texture)*
- *[**getTextureSurfaceIDDecal**( )](../api/library/rendering/class.renderer_cpp.md#getTextureSurfaceIDDecal_Texture)*
- *[**getTextureSurfaceIDScene**( )](../api/library/rendering/class.renderer_cpp.md#getTextureSurfaceIDScene_Texture)*
- *[**getTextureSurfaceIDTransparent**( )](../api/library/rendering/class.renderer_cpp.md#getTextureSurfaceIDTransparent_Texture)*
- *[**getTextureSurfaceIDWater**( )](../api/library/rendering/class.renderer_cpp.md#getTextureSurfaceIDWater_Texture)*
- *[**useReactiveMask**( )](../api/library/rendering/class.renderer_cpp.md#useReactiveMask_int)*


## SkeletonRetargeter Class


#### New Functions


- *[**getFirstFileGUID**( )](../api/library/animations/skeletal/class.skeletonretargeter_cpp.md#getFirstFileGUID_UGUID)*
- *[**getSecondFileGUID**( )](../api/library/animations/skeletal/class.skeletonretargeter_cpp.md#getSecondFileGUID_UGUID)*


## SoundSource Class


#### New Functions


- *[**getPitchShift**( )](../api/library/sounds/class.soundsource_cpp.md#getPitchShift_float)*
- *[**setPitchShift**( float )](../api/library/sounds/class.soundsource_cpp.md#setPitchShift_float_void)*


## Sounds Class


#### New Functions


- *[**getSampleWaveform**( const char *, int, Vector<float> & )](../api/library/engine/class.sounds_cpp.md#getSampleWaveform_cstr_int_VECfloat_float)*


## SpiderVision::DebugData Class


#### New Functions


- *[**isDebugStereo**( )](../api/library/plugins/spidervision/class.debugdata_cpp.md#isDebugStereo_int)*
- *[**setDebugStereo**( bool )](../api/library/plugins/spidervision/class.debugdata_cpp.md#setDebugStereo_int_void)*


## SpiderVision::DisplaysConfig Class


#### New Functions


- *[**getEventHeadTransformChanged**( )](../api/library/plugins/spidervision/class.displaysconfig_cpp.md#EventHeadTransformChanged)*
- *[**getHeadPosition**( )](../api/library/plugins/spidervision/class.displaysconfig_cpp.md#getHeadPosition_vec3)*
- *[**setHeadPosition**( const Math::vec3 & )](../api/library/plugins/spidervision/class.displaysconfig_cpp.md#setHeadPosition_vec3_void)*
- *[**getHeadRotation**( )](../api/library/plugins/spidervision/class.displaysconfig_cpp.md#getHeadRotation_quat)*
- *[**setHeadRotation**( const Math::quat & )](../api/library/plugins/spidervision/class.displaysconfig_cpp.md#setHeadRotation_quat_void)*


## SpiderVision::GroupData Class


#### New Enums


- *[**GROUP_TYPE::CAVE**](../api/library/plugins/spidervision/class.groupdata_cpp.md#CAVE)*


## SpiderVision::Manager Class


| UNIGINE 2.21 | UNIGINE 2.22 |
|---|---|
| ***isEnabled**( )* | Removed. |
| ***setEnabled**( bool )* | Removed. |
| ***setGroupViewOffset**( int, const Math::Vec3 & )* | Removed. |
| ***setViewportViewOffset**( int, const Math::Vec3 & )* | Removed. |


#### New Functions


- *[**getViewportCustomPlayer**( int )](../api/library/plugins/spidervision/class.spidervision_manager_cpp.md#getViewportCustomPlayer_int_Player)*


## SpiderVision::ViewportData Class


#### New Functions


- *[**getPixelDensity**( )](../api/library/plugins/spidervision/class.viewportdata_cpp.md#getPixelDensity_float)*
- *[**setPixelDensity**( float )](../api/library/plugins/spidervision/class.viewportdata_cpp.md#setPixelDensity_float_void)*
- *[**getRenderMode**( )](../api/library/plugins/spidervision/class.viewportdata_cpp.md#getRenderMode_int)*
- *[**setRenderMode**( ViewportData::RENDER_MODE )](../api/library/plugins/spidervision/class.viewportdata_cpp.md#setRenderMode_int_void)*
- *[**isSwapEyesInStereoMode**( )](../api/library/plugins/spidervision/class.viewportdata_cpp.md#isSwapEyesInStereoMode_int)*
- *[**setSwapEyesInStereoMode**( bool )](../api/library/plugins/spidervision/class.viewportdata_cpp.md#setSwapEyesInStereoMode_int_void)*


#### New Enums


- *[**RENDER_MODE**](../api/library/plugins/spidervision/class.viewportdata_cpp.md#RENDER_MODE)*


## SpiderVision::WallGroupData Class


#### New Functions


- *[**getPixelDensity**( )](../api/library/plugins/spidervision/class.wallgroupdata_cpp.md#getPixelDensity_float)*
- *[**setPixelDensity**( float )](../api/library/plugins/spidervision/class.wallgroupdata_cpp.md#setPixelDensity_float_void)*


## TerrainDetailMask Class


#### New Functions


- *[**getExperimentalNavigationArea**( )](../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md#getExperimentalNavigationArea_int)*
- *[**getExperimentalNavigationBakeMask**( )](../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md#getExperimentalNavigationBakeMask_int)*
- *[**getExperimentalNavigationMinValue**( )](../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md#getExperimentalNavigationMinValue_float)*
- *[**isExperimentalNavigation**( )](../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md#isExperimentalNavigation_int)*
- *[**setExperimentalNavigation**( bool )](../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md#setExperimentalNavigation_int_void)*
- *[**setExperimentalNavigationArea**( int )](../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md#setExperimentalNavigationArea_int_void)*
- *[**setExperimentalNavigationBakeMask**( int )](../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md#setExperimentalNavigationBakeMask_int_void)*
- *[**setExperimentalNavigationMinValue**( float )](../api/library/objects/landscape_terrain/class.terraindetailmask_cpp.md#setExperimentalNavigationMinValue_float_void)*


## Texture Class


#### New Enums


- *[**FORMAT_MAPPING_MASK**](../api/library/rendering/class.texture_cpp.md#FORMAT_MAPPING_MASK)*


## UGUID Class


#### New Functions


- *[**lexicographicalLess**( const UGUID &, const UGUID & )](../api/library/filesystem/class.uguid_cpp.md#lexicographicalLess_const_UGUID_ref_const_UGUID_ref_bool)*


## VR Class


#### New Functions


- *[**getEmulationMirrorCrop**( )](../api/library/vr/class.vr_cpp.md#getEmulationMirrorCrop_float)*
- *[**setEmulationMirrorCrop**( float )](../api/library/vr/class.vr_cpp.md#setEmulationMirrorCrop_float_void)*
- *[**getEmulationMirrorCropOffset**( )](../api/library/vr/class.vr_cpp.md#getEmulationMirrorCropOffset_vec2)*
- *[**setEmulationMirrorCropOffset**( const Math::vec2 & )](../api/library/vr/class.vr_cpp.md#setEmulationMirrorCropOffset_vec2_void)*
- *[**getEmulationMirrorMode**( )](../api/library/vr/class.vr_cpp.md#getEmulationMirrorMode_int)*
- *[**setEmulationMirrorMode**( VR::MIRROR_MODE )](../api/library/vr/class.vr_cpp.md#setEmulationMirrorMode_int_void)*
- *[**getFoveatedMode**( )](../api/library/vr/class.vr_cpp.md#getFoveatedMode_int)*
- *[**getMirrorCrop**( )](../api/library/vr/class.vr_cpp.md#getMirrorCrop_float)*
- *[**setMirrorCrop**( float )](../api/library/vr/class.vr_cpp.md#setMirrorCrop_float_void)*
- *[**getMirrorCropOffset**( )](../api/library/vr/class.vr_cpp.md#getMirrorCropOffset_vec2)*
- *[**setMirrorCropOffset**( const Math::vec2 & )](../api/library/vr/class.vr_cpp.md#setMirrorCropOffset_vec2_void)*
- *[**getPeripheralRenderingDebugGazeOverrideCoord**( )](../api/library/vr/class.vr_cpp.md#getPeripheralRenderingDebugGazeOverrideCoord_vec2)*
- *[**setPeripheralRenderingDebugGazeOverrideCoord**( const Math::vec2 & )](../api/library/vr/class.vr_cpp.md#setPeripheralRenderingDebugGazeOverrideCoord_vec2_void)*
- *[**getPeripheralRenderingDebugGazeOverrideMode**( )](../api/library/vr/class.vr_cpp.md#getPeripheralRenderingDebugGazeOverrideMode_int)*
- *[**setPeripheralRenderingDebugGazeOverrideMode**( VR::PERIPHERAL_RENDERING_DEBUG_GAZE_OVERRIDE_MODE )](../api/library/vr/class.vr_cpp.md#setPeripheralRenderingDebugGazeOverrideMode_int_void)*
- *[**getProfilerBackgroundAlpha**( )](../api/library/vr/class.vr_cpp.md#getProfilerBackgroundAlpha_int)*
- *[**setProfilerBackgroundAlpha**( int )](../api/library/vr/class.vr_cpp.md#setProfilerBackgroundAlpha_int_void)*
- *[**getProfilerPosition**( )](../api/library/vr/class.vr_cpp.md#getProfilerPosition_int)*
- *[**setProfilerPosition**( VR::PROFILER_POSITION )](../api/library/vr/class.vr_cpp.md#setProfilerPosition_int_void)*
- *[**getShowProfiler**( )](../api/library/vr/class.vr_cpp.md#getShowProfiler_int)*
- *[**setShowProfiler**( VR::SHOW_PROFILER )](../api/library/vr/class.vr_cpp.md#setShowProfiler_int_void)*
- *[**isShowProfilerMemory**( )](../api/library/vr/class.vr_cpp.md#isShowProfilerMemory_int)*
- *[**setShowProfilerMemory**( bool )](../api/library/vr/class.vr_cpp.md#setShowProfilerMemory_int_void)*
- *[**isShowProfilerMisc**( )](../api/library/vr/class.vr_cpp.md#isShowProfilerMisc_int)*
- *[**setShowProfilerMisc**( bool )](../api/library/vr/class.vr_cpp.md#setShowProfilerMisc_int_void)*
- *[**isShowProfilerPerformance**( )](../api/library/vr/class.vr_cpp.md#isShowProfilerPerformance_int)*
- *[**setShowProfilerPerformance**( bool )](../api/library/vr/class.vr_cpp.md#setShowProfilerPerformance_int_void)*


#### New Enums


- *[**FOVEATED_MODE**](../api/library/vr/class.vr_cpp.md#FOVEATED_MODE)*
- *[**PERIPHERAL_RENDERING_DEBUG_GAZE_OVERRIDE_MODE**](../api/library/vr/class.vr_cpp.md#PERIPHERAL_RENDERING_DEBUG_GAZE_OVERRIDE_MODE)*
- *[**PROFILER_POSITION**](../api/library/vr/class.vr_cpp.md#PROFILER_POSITION)*
- *[**SHOW_PROFILER**](../api/library/vr/class.vr_cpp.md#SHOW_PROFILER)*


## Viewport Class


#### New Functions


- *[**getPanoramaFisheyeKannalaBrandtChromaticAberration**( )](../api/library/rendering/class.viewport_cpp.md#getPanoramaFisheyeKannalaBrandtChromaticAberration_float)*
- *[**setPanoramaFisheyeKannalaBrandtChromaticAberration**( float )](../api/library/rendering/class.viewport_cpp.md#setPanoramaFisheyeKannalaBrandtChromaticAberration_float_void)*
- *[**getPanoramaFisheyeKannalaBrandtCoefficients**( )](../api/library/rendering/class.viewport_cpp.md#getPanoramaFisheyeKannalaBrandtCoefficients_vec4)*
- *[**setPanoramaFisheyeKannalaBrandtCoefficients**( const Math::vec4 & )](../api/library/rendering/class.viewport_cpp.md#setPanoramaFisheyeKannalaBrandtCoefficients_vec4_void)*
- *[**getPanoramaFisheyeKannalaBrandtFocalLength**( )](../api/library/rendering/class.viewport_cpp.md#getPanoramaFisheyeKannalaBrandtFocalLength_vec2)*
- *[**setPanoramaFisheyeKannalaBrandtFocalLength**( const Math::vec2 & )](../api/library/rendering/class.viewport_cpp.md#setPanoramaFisheyeKannalaBrandtFocalLength_vec2_void)*
- *[**getPanoramaFisheyeKannalaBrandtImageCircleRadius**( )](../api/library/rendering/class.viewport_cpp.md#getPanoramaFisheyeKannalaBrandtImageCircleRadius_float)*
- *[**setPanoramaFisheyeKannalaBrandtImageCircleRadius**( float )](../api/library/rendering/class.viewport_cpp.md#setPanoramaFisheyeKannalaBrandtImageCircleRadius_float_void)*
- *[**getPanoramaFisheyeKannalaBrandtImageDimensions**( )](../api/library/rendering/class.viewport_cpp.md#getPanoramaFisheyeKannalaBrandtImageDimensions_vec2)*
- *[**setPanoramaFisheyeKannalaBrandtImageDimensions**( const Math::vec2 & )](../api/library/rendering/class.viewport_cpp.md#setPanoramaFisheyeKannalaBrandtImageDimensions_vec2_void)*
- *[**getPanoramaFisheyeKannalaBrandtPrincipalPoint**( )](../api/library/rendering/class.viewport_cpp.md#getPanoramaFisheyeKannalaBrandtPrincipalPoint_vec2)*
- *[**setPanoramaFisheyeKannalaBrandtPrincipalPoint**( const Math::vec2 & )](../api/library/rendering/class.viewport_cpp.md#setPanoramaFisheyeKannalaBrandtPrincipalPoint_vec2_void)*
- *[**getPanoramaFisheyeKannalaBrandtSkew**( )](../api/library/rendering/class.viewport_cpp.md#getPanoramaFisheyeKannalaBrandtSkew_float)*
- *[**setPanoramaFisheyeKannalaBrandtSkew**( float )](../api/library/rendering/class.viewport_cpp.md#setPanoramaFisheyeKannalaBrandtSkew_float_void)*
- *[**getPanoramaFisheyeKannalaBrandtTangentialDistortion**( )](../api/library/rendering/class.viewport_cpp.md#getPanoramaFisheyeKannalaBrandtTangentialDistortion_vec2)*
- *[**setPanoramaFisheyeKannalaBrandtTangentialDistortion**( const Math::vec2 & )](../api/library/rendering/class.viewport_cpp.md#setPanoramaFisheyeKannalaBrandtTangentialDistortion_vec2_void)*
- *[**getPanoramaFisheyeKannalaBrandtVignettingCoefficient5**( )](../api/library/rendering/class.viewport_cpp.md#getPanoramaFisheyeKannalaBrandtVignettingCoefficient5_float)*
- *[**setPanoramaFisheyeKannalaBrandtVignettingCoefficient5**( float )](../api/library/rendering/class.viewport_cpp.md#setPanoramaFisheyeKannalaBrandtVignettingCoefficient5_float_void)*
- *[**getPanoramaFisheyeKannalaBrandtVignettingCoefficients**( )](../api/library/rendering/class.viewport_cpp.md#getPanoramaFisheyeKannalaBrandtVignettingCoefficients_vec4)*
- *[**setPanoramaFisheyeKannalaBrandtVignettingCoefficients**( const Math::vec4 & )](../api/library/rendering/class.viewport_cpp.md#setPanoramaFisheyeKannalaBrandtVignettingCoefficients_vec4_void)*
- *[**isPanoramaForceDisableScreenSpaceEffects**( )](../api/library/rendering/class.viewport_cpp.md#isPanoramaForceDisableScreenSpaceEffects_int)*
- *[**setPanoramaForceDisableScreenSpaceEffects**( bool )](../api/library/rendering/class.viewport_cpp.md#setPanoramaForceDisableScreenSpaceEffects_int_void)*


#### New Enums


- *[**SKIP_AUTO_EXPOSURE_ADAPTATION_TIME**](../api/library/rendering/class.viewport_cpp.md#SKIP_AUTO_EXPOSURE_ADAPTATION_TIME)*
- *[**SKIP_AUTO_WHITE_BALANCE_ADAPTATION_TIME**](../api/library/rendering/class.viewport_cpp.md#SKIP_AUTO_WHITE_BALANCE_ADAPTATION_TIME)*


## Visualizer Class


#### New Functions


- *[**clearNodeTypeIcons**( )](../api/library/engine/class.visualizer_cpp.md#clearNodeTypeIcons_void)*
- *[**setNodeTypeIcon**( Node::TYPE, const char * )](../api/library/engine/class.visualizer_cpp.md#setNodeTypeIcon_int_cstr_int)*


## Weather::Manager Class


#### New Functions


- *[**getPlanet**( )](../api/library/plugins/weather/class.weather_manager_cpp.md#getPlanet_Planet)*


## Widget Class


#### New Functions


- *[**getTextDirection**( )](../api/library/gui/class.widget_cpp.md#getTextDirection_int)*
- *[**setTextDirection**( Gui::TextDirection )](../api/library/gui/class.widget_cpp.md#setTextDirection_int_void)*


## WidgetEditLine Class


#### New Functions


- *[**getCursorMode**( )](../api/library/gui/class.widgeteditline_cpp.md#getCursorMode_int)*
- *[**setCursorMode**( Gui::CursorMode )](../api/library/gui/class.widgeteditline_cpp.md#setCursorMode_int_void)*


## WidgetEditText Class


#### New Functions


- *[**getCursorMode**( )](../api/library/gui/class.widgetedittext_cpp.md#getCursorMode_int)*
- *[**setCursorMode**( Gui::CursorMode )](../api/library/gui/class.widgetedittext_cpp.md#setCursorMode_int_void)*


## WidgetTreeBox Class


#### New Functions


- *[**clearIcons**( )](../api/library/gui/class.widgettreebox_cpp.md#clearIcons_void)*
- *[**setIcon**( int, const char * )](../api/library/gui/class.widgettreebox_cpp.md#setIcon_int_cstr_int)*


## Decal Class


#### New Functions


- *[**getSurfaceRenderCustomParameterFloat**( const char * )](../api/library/decals/class.decal_cpp.md#getSurfaceRenderCustomParameterFloat_cstr_float)*
- *[**getSurfaceRenderCustomParameterFloat**( int )](../api/library/decals/class.decal_cpp.md#getSurfaceRenderCustomParameterFloat_int_float)*
- *[**getSurfaceRenderCustomParameterInt**( const char * )](../api/library/decals/class.decal_cpp.md#getSurfaceRenderCustomParameterInt_cstr_int)*
- *[**getSurfaceRenderCustomParameterInt**( int )](../api/library/decals/class.decal_cpp.md#getSurfaceRenderCustomParameterInt_int_int)*
- *[**getSurfaceRenderCustomParameterUInt**( const char * )](../api/library/decals/class.decal_cpp.md#getSurfaceRenderCustomParameterUInt_cstr_uint)*
- *[**getSurfaceRenderCustomParameterUInt**( int )](../api/library/decals/class.decal_cpp.md#getSurfaceRenderCustomParameterUInt_int_uint)*
- *[**isSurfaceRenderCustomParameterOverridden**( int )](../api/library/decals/class.decal_cpp.md#isSurfaceRenderCustomParameterOverridden_int_bool)*
- *[**resetSurfaceRenderCustomParameter**( int )](../api/library/decals/class.decal_cpp.md#resetSurfaceRenderCustomParameter_int_void)*
- *[**resetSurfaceRenderCustomParameters**( )](../api/library/decals/class.decal_cpp.md#resetSurfaceRenderCustomParameters_void)*
- *[**setSurfaceRenderCustomParameterFloat**( const char *, float )](../api/library/decals/class.decal_cpp.md#setSurfaceRenderCustomParameterFloat_cstr_float_void)*
- *[**setSurfaceRenderCustomParameterFloat**( int, float )](../api/library/decals/class.decal_cpp.md#setSurfaceRenderCustomParameterFloat_int_float_void)*
- *[**setSurfaceRenderCustomParameterInt**( const char *, int )](../api/library/decals/class.decal_cpp.md#setSurfaceRenderCustomParameterInt_cstr_int_void)*
- *[**setSurfaceRenderCustomParameterInt**( int, int )](../api/library/decals/class.decal_cpp.md#setSurfaceRenderCustomParameterInt_int_int_void)*
- *[**setSurfaceRenderCustomParameterUInt**( const char *, unsigned int )](../api/library/decals/class.decal_cpp.md#setSurfaceRenderCustomParameterUInt_cstr_uint_void)*
- *[**setSurfaceRenderCustomParameterUInt**( int, unsigned int )](../api/library/decals/class.decal_cpp.md#setSurfaceRenderCustomParameterUInt_int_uint_void)*


## LightProj Class


#### New Functions


- *[**isUseEnvironmentColor**( )](../api/library/lights/class.lightproj_cpp.md#isUseEnvironmentColor_int)*
- *[**setUseEnvironmentColor**( bool )](../api/library/lights/class.lightproj_cpp.md#setUseEnvironmentColor_int_void)*


## Object Class


#### New Functions


- *[**getExperimentalNavigation**( int )](../api/library/objects/class.object_cpp.md#getExperimentalNavigation_int_int)*
- *[**getExperimentalNavigationArea**( int )](../api/library/objects/class.object_cpp.md#getExperimentalNavigationArea_int_int)*
- *[**getExperimentalNavigationBakeMask**( int )](../api/library/objects/class.object_cpp.md#getExperimentalNavigationBakeMask_int_int)*
- *[**getSurfaceRenderCustomParameterFloat**( int, int )](../api/library/objects/class.object_cpp.md#getSurfaceRenderCustomParameterFloat_int_int_float)*
- *[**getSurfaceRenderCustomParameterFloat**( int, const char * )](../api/library/objects/class.object_cpp.md#getSurfaceRenderCustomParameterFloat_int_cstr_float)*
- *[**getSurfaceRenderCustomParameterInt**( int, int )](../api/library/objects/class.object_cpp.md#getSurfaceRenderCustomParameterInt_int_int_int)*
- *[**getSurfaceRenderCustomParameterInt**( int, const char * )](../api/library/objects/class.object_cpp.md#getSurfaceRenderCustomParameterInt_int_cstr_int)*
- *[**getSurfaceRenderCustomParameterUInt**( int, int )](../api/library/objects/class.object_cpp.md#getSurfaceRenderCustomParameterUInt_int_int_uint)*
- *[**getSurfaceRenderCustomParameterUInt**( int, const char * )](../api/library/objects/class.object_cpp.md#getSurfaceRenderCustomParameterUInt_int_cstr_uint)*
- *[**isSurfaceRenderCustomParameterOverridden**( int, int )](../api/library/objects/class.object_cpp.md#isSurfaceRenderCustomParameterOverridden_int_int_bool)*
- *[**resetSurfaceRenderCustomParameter**( int, int )](../api/library/objects/class.object_cpp.md#resetSurfaceRenderCustomParameter_int_int_void)*
- *[**resetSurfaceRenderCustomParameters**( int )](../api/library/objects/class.object_cpp.md#resetSurfaceRenderCustomParameters_int_void)*
- *[**setExperimentalNavigation**( bool, int )](../api/library/objects/class.object_cpp.md#setExperimentalNavigation_int_int_void)*
- *[**setExperimentalNavigationArea**( int, int )](../api/library/objects/class.object_cpp.md#setExperimentalNavigationArea_int_int_void)*
- *[**setExperimentalNavigationBakeMask**( int, int )](../api/library/objects/class.object_cpp.md#setExperimentalNavigationBakeMask_int_int_void)*
- *[**setSurfaceRenderCustomParameterFloat**( int, int, float )](../api/library/objects/class.object_cpp.md#setSurfaceRenderCustomParameterFloat_int_int_float_void)*
- *[**setSurfaceRenderCustomParameterFloat**( int, const char *, float )](../api/library/objects/class.object_cpp.md#setSurfaceRenderCustomParameterFloat_int_cstr_float_void)*
- *[**setSurfaceRenderCustomParameterInt**( int, int, int )](../api/library/objects/class.object_cpp.md#setSurfaceRenderCustomParameterInt_int_int_int_void)*
- *[**setSurfaceRenderCustomParameterInt**( int, const char *, int )](../api/library/objects/class.object_cpp.md#setSurfaceRenderCustomParameterInt_int_cstr_int_void)*
- *[**setSurfaceRenderCustomParameterUInt**( int, int, unsigned int )](../api/library/objects/class.object_cpp.md#setSurfaceRenderCustomParameterUInt_int_int_uint_void)*
- *[**setSurfaceRenderCustomParameterUInt**( int, const char *, unsigned int )](../api/library/objects/class.object_cpp.md#setSurfaceRenderCustomParameterUInt_int_cstr_uint_void)*


## ObjectMeshCluster Class


#### New Functions


- *[**getInstanceCustomParameterFloat**( int, int, const char * )](../api/library/objects/class.objectmeshcluster_cpp.md#getInstanceCustomParameterFloat_int_int_cstr_float)*
- *[**getInstanceCustomParameterFloat**( int, int, int )](../api/library/objects/class.objectmeshcluster_cpp.md#getInstanceCustomParameterFloat_int_int_int_float)*
- *[**getInstanceCustomParameterInt**( int, int, const char * )](../api/library/objects/class.objectmeshcluster_cpp.md#getInstanceCustomParameterInt_int_int_cstr_int)*
- *[**getInstanceCustomParameterInt**( int, int, int )](../api/library/objects/class.objectmeshcluster_cpp.md#getInstanceCustomParameterInt_int_int_int_int)*
- *[**getInstanceCustomParameterUInt**( int, int, const char * )](../api/library/objects/class.objectmeshcluster_cpp.md#getInstanceCustomParameterUInt_int_int_cstr_uint)*
- *[**getInstanceCustomParameterUInt**( int, int, int )](../api/library/objects/class.objectmeshcluster_cpp.md#getInstanceCustomParameterUInt_int_int_int_uint)*
- *[**hasInstanceCustomParameters**( int, int )](../api/library/objects/class.objectmeshcluster_cpp.md#hasInstanceCustomParameters_int_int_int)*
- *[**isInstanceCustomParameterOverridden**( int, int, int )](../api/library/objects/class.objectmeshcluster_cpp.md#isInstanceCustomParameterOverridden_int_int_int_bool)*
- *[**resetInstanceCustomParameter**( int, int, int )](../api/library/objects/class.objectmeshcluster_cpp.md#resetInstanceCustomParameter_int_int_int_void)*
- *[**resetInstanceCustomParameters**( int, int )](../api/library/objects/class.objectmeshcluster_cpp.md#resetInstanceCustomParameters_int_int_void)*
- *[**setInstanceCustomParameterFloat**( int, int, const char *, float )](../api/library/objects/class.objectmeshcluster_cpp.md#setInstanceCustomParameterFloat_int_int_cstr_float_void)*
- *[**setInstanceCustomParameterFloat**( int, int, int, float )](../api/library/objects/class.objectmeshcluster_cpp.md#setInstanceCustomParameterFloat_int_int_int_float_void)*
- *[**setInstanceCustomParameterInt**( int, int, const char *, int )](../api/library/objects/class.objectmeshcluster_cpp.md#setInstanceCustomParameterInt_int_int_cstr_int_void)*
- *[**setInstanceCustomParameterInt**( int, int, int, int )](../api/library/objects/class.objectmeshcluster_cpp.md#setInstanceCustomParameterInt_int_int_int_int_void)*
- *[**setInstanceCustomParameterUInt**( int, int, const char *, unsigned int )](../api/library/objects/class.objectmeshcluster_cpp.md#setInstanceCustomParameterUInt_int_int_cstr_uint_void)*
- *[**setInstanceCustomParameterUInt**( int, int, int, unsigned int )](../api/library/objects/class.objectmeshcluster_cpp.md#setInstanceCustomParameterUInt_int_int_int_uint_void)*


## ObjectWaterGlobal Class


#### New Functions


- *[**getBackfaceMaterialID**( )](../api/library/objects/class.objectwaterglobal_cpp.md#getBackfaceMaterialID_uint)*


## World Class


#### New Functions


- *[**getExperimentalNavigationSettings**( )](../api/library/engine/class.world_cpp.md#getExperimentalNavigationSettings_String)*
- *[**setExperimentalNavigationSettings**( const char * )](../api/library/engine/class.world_cpp.md#setExperimentalNavigationSettings_cstr_void)*
