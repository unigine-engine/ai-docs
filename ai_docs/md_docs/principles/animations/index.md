# Animation System


> **Warning:** The functionality described here is **EXPERIMENTAL** and is **not recommended for production use**. Future releases may bring significant changes to API and features. Backward compatibility of the final production-ready version is not guaranteed.


UNIGINE Animation System (Animations) enables you to create in-game cinematics with a specialized multi-track editor. Animation sequences are defined by creating [Playbacks](#animation_playback), adding [Layers](#animation_layer) to them, and adding *[Tracks](#animation_track)* to these layers with the ability to control the track sequence and blending between different layers. Users can define the makeup of each [Track](#animation_track) by adding [Objects](#animation_object) and [Modifiers](#animation_object) to define changes of objects and their parameters over time based on key frames.


### See Also


- [Animation System API Reference](../../api/library/animations/index.md) for more information on managing animations via code.


## Animation Parameters


Animation System enables you to animate nodes, parameters, widgets, application windows, global rendering and physics parameters, etc. The following data types are supported:


- *int / bool / scalar / float / double*
- *quat*
- *string / uguid*
- *ivec2 / ivec3 / ivec4*
- *Vec2 / vec2 / dvec2*
- *Vec3 / vec3 / dvec3*
- *Vec4 / vec4 / dvec4*
- *Mat4*
- *Node*


The *[Animations](../../api/library/animations/class.animations_cpp.md)* class enables you to get the complete list of classes with parameters available for animation via API, for each parameter you can get its name and data type.


You can also find all parameters available for animation in the `UnigineAnimationParameters.h` file.


## Animation Object


**Animation Object** is an abstract dummy object (proxy) that is modified by a track; it can be a node, material, property, or an arbitrary object from UNIGINE API (like widgets, windows, etc.). Animation Object serves as a bridge connecting tracks with actual objects (certain nodes in the world, certain materials, UI widgets, and windows, etc.) that will be animated. Bindings to the actual objects are stored by the *Animation Objects* themselves.


In order to use a modifier, we should know to which object we are applying it (if it is not a parameter of some singleton class of the engine, like *Game, Render, Physics*, etc.). But we can't use actual objects directly, as this will stick modifiers in tracks to them and will kill flexibility making it impossible to use modifiers and tracks to animate arbitrary objects. Moreover, some objects of the Engine cannot be saved (such as widgets, windows, etc.) as they are created and assigned at run-time.


## Animation Tracks


**Animation Track** is a set of data describing animation of a certain *[Animation Object](#animation_object)* or some global parameters like render or physics settings in case there is no Animation Object assigned.


Each Track has the speed parameter that determines the rate of fetching frames values from the track.


## Animation Modifier


**Animation Modifier** is a modifier for basic types (*INT, FLAG, QUAT, SCALAR, FLOAT, DOUBLE, IVEC2, IVEC3, IVEC4, VEC2, VEC3, VEC4, FVEC2, FVEC3, FVEC4, DVEC2, DVEC3, DVEC4, BONES*). Modifiers use Curves (*[AnimationCurve](../../api/library/animations/timeline/class.animationcurve_cpp.md)*) to change their components over time. A modifier can have a set of 1 to 7 curves depending on the number of its components and their types (e.g. *[AnimationModifierInt](../../api/library/animations/timeline/class.animationmodifierint_cpp.md)* has a single curve, while *[AnimationModifierBones](../../api/library/animations/timeline/class.animationmodifierbones_cpp.md)* has 7: 3 curves for position, 1 for rotation, and 3 for scale).


Parameter description is stored as a pair: **`param_name + access_key`** (index or name). For example to set node position it is enough to store only the parameter name (**node.position**), while for a material parameter a name or index is required to apply a value. The modifier also stores information about the object to which it is applied.


For some modifiers *uniform* time can be used — in this case modifier value changes with a constant rate. For example, normally if a node's position is changed via a wave curve, it'll move with positive and negative acceleration within the different parts of the timeline, but in case of using uniform time the node will move at a constant speed.


## Animation Curves


**Animation Curves** define the dynamics of change of values over time. There are dedicated curves available for basic types: *int, float, double, scalar, flag, quat, string, GUID*.


Each curve is represented by a set of key frames, for each pair of keys an individual interpolation mode can be assigned (if applicable to current values):


- **CONSTANT** - the value of the left key is used for the whole interval between the keys (constant).
- **LINEAR** - the value between the keys is interpolated linearly.
- **SMOOTH** - the value between the keys is interpolated smoothly according to the Bezier curve with symmetrical left and right tangents for each key.
- **BREAK** - the value between the keys is interpolated according to the Bezier curve with left and right tangents for each key controlled independently.


## Animation Playback


**Animation Playback** controls the whole animation and operates with *[Animation Tracks](#animation_track)*. The playback timeline has layers (the higher the layer the greater priority), you can add any number of tracks to these layers. The tracks that belong to the same layer are played sequentially according to their positions on the timeline, while the tracks from different layers are either switched abruptly according to the layer priority or blended together to obtain the final result. For each track you can specify its impact on the final result (weight). The total weight at any point of the timeline of blended tracks is equal to 1.


Playback refers to *[tracks](#animation_playback)* sorted by layers, and defines their sequence and blending.


Each frame we get all modifiers of the track, then take all current values of curves and calculate current parameter values in accordance with key values and interpolation types.


### Animation Playback Node


For your convenience we have added a new **Animation Playback** node (*NodeAnimationPlayback*) to demonstrate the functionality of the new Animation System. This node enables you to:


- **Play** [animation track](#animation_track) files in the new `.utrack` format. You can change playback speed and set a particular time to see the corresponding [animation frame](#animation_frame) applied to the scene. It is also possible to play animations from a predefined start time (*TimeFrom*) to a predefined end time (*TimeTo*).
- **Convert** all old [animation track](#animation_track) files (`.track` format) in the specified folder (or in the whole `data` directory) into the new `.utrack` format. You can also convert an old [animation track](#animation_track) file (`.track`) to the new `.uplay` format to be used directly via code (intermediate `.utrack` file will also be created next to the original).


![](nodeanimationplayback.jpg)


## Animation Masks


**Animation Mask** is represented by a set of [modifiers](#animation_modifier), but without animation curves, i.e.:
**`Animation Mask = Animation Object ID + Animation Parameter Description`**
 This combination is enough to define a modifier for a particular object. Such masks can be used to identify identical parameters in different tracks and perform partial or complete interpolation between tracks with different structures.


## Animation Frames


**Animation Frame** is a combination of an animation mask and a set of values of modifiers calculated for this mask. These frames are passed from tracks to the playback and are blended to obtain the final resulting frame that is finally applied to objects. A frame can be thought of as a vertical slice of values of all tracks and modifiers played at the specified moment.
