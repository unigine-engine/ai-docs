# Sequence Channels


A **Channel** is a single row in the Sequencer that animates a specific value. Every kind of value has its own channel type, from a plain number to the texture on a material. The type decides what you place on the row and how the value moves between those points.


This article covers the settings every channel has, and the different kinds of animated values.


## Channel Properties


Every channel carries the same small set of settings, whatever it animates. They appear in the properties panel when the channel is selected:


![Common Channel Parameters](common_channel_parameters.png)

*Common channel parameters. The channel shown here is aCamera Cutsone, so it adds aPreview Aspectof its own below them*


| Property | What it does |
|---|---|
| **Enabled** | Switches the channel off without losing anything: it keeps its keys and simply stops driving its parameter. |
| **Channel** | What this channel animates. It is the same picker a channel is created from, so choosing another entry here retypes the channel. |
| **Custom Name** | A name for the row, replacing the one generated from the parameter. It is more than a label: code looks a channel up by this name, and on an event channel it is the name the event fires under. |
| **Value Type** | *Read-only.* The kind of value this channel animates. |
| **Key Range** | *Read-only.* The time from the first key on this channel to the last. |
| **Status** | *Read-only,* and shown only when something is wrong. |


A channel turns red in the list when what it was built on can no longer be found as it was: a parameter removed or retyped in the project, or a component class or field renamed in code. **Status** names the reason.


> **Notice:** A channel that drives nothing is a different complaint: there the parameter resolves fine and no object was found for it.
>
>
> See **[Targets](../../../../editor2/tools/sequencer/targets/index.md)** artcle for details.


## Channel Types


The type of a channel decides what you put on its row. Most channels take **keys**, and the value travels from one key to the next. A few take **clips** instead, blocks of ready-made content laid out in time.


### Interpolated Values


A curve runs between the keys of these channels, and the shape of that curve is the animation. Their keys carry an interpolation type and tangents, so the value can cut, glide, or ease from one key to the next.


> **Notice:** Placing keys and shaping the curve that runs between them is covered in the [Keys and Curves](../../../../editor2/tools/sequencer/keys/index.md) article.


#### Numbers


One value and one curve. **Camera � FOV**, **Sound Source � Gain** and **Decal � Opacity** are all of this kind.


Where a parameter declares a valid range, the key value field is a slider bounded by that range rather than a free number box.


![Interpolated Number Channel](numbers_interpolated_channel.png)

*APlayer � FOVchannel. The row prints the value under the playhead, and the Inspector reports the type asFloat*


#### Vectors


A vector parameter that holds two, three or four numbers at once (**Node � Position**, **Node � Scale**, **Physics � Gravity**). The channel gets one curve per component, shown as sub-rows of its row, and each component carries its own keys. Channel-wide settings such as extrapolation apply to all of them at once.


The components are independent, so you can key a single axis and leave the rest alone - only Y, for example.


![Vector Channel](vector_channel.png)

*Node � Positionexpanded into its X, Y and Z sub-rows. Each curve is colored after its axis, and the keys of the three axes need not line up in time*


#### Rotations


A rotation parameter such as **Node � Rotation** behaves like a three-component vector: one curve per Euler axis. What it adds is a per-channel **Rotation Mode**, which picks how the orientations between the keys are worked out:


| Mode | Behavior |
|---|---|
| **Quaternion (SLERP)** | Shortest-arc spherical blend between the orientations of the keys, free of gimbal wobble. |
| **Angles XYZ** | Each Euler axis is interpolated on its own and the result is composed in X, Y, Z order. |
| **Angles ZYX** | The same, composed in Z, Y, X order. |


![Rotation Modes](rotation_channel.png)

*Rotation Modeon aNode � Rotationchannel. The Inspector names the typeQuaternion, even though the keys are edited as three Euler curves*

 Best PracticeFor a moving camera, **Quaternion (SLERP)** gives the cleanest arc between shots.
#### Colors


A color parameter such as **Light � Color** behaves like a four-component vector: one curve per RGBA channel. What it adds is the way it is shown and edited.


![Color Channel](color_channel.png)

*AMaterial � albedo_colorchannel. The Dope Sheet draws the ramp, where the checkerboard marks falling alpha, while the Curves editor still shows the four RGBA curves underneath. A selected key opens as aColor Ramp Keywith one time field and a color picker*


In the *Dope Sheet* the channel is drawn as a **color ramp**: a band showing the color over time. A key on that band stands for four keys at once, one per component, so you pick its color instead of typing four numbers.


### Stepped Values


Between two of these values there is nothing worth passing through, so a key holds its value until the next one and then jumps. They carry no tangents, and no choice of key type is offered for them.


Where the value is a number, the *Curves* editor draws it as a staircase. Where it is not, there is nothing to plot at all, and the work is done in the *Dope Sheet*.


#### Whole Numbers


Counts, indices and bit masks are all integers - **Light World � Num Shadow Cascades**, **Camera � Viewport Mask**, **Object Grass � Terrain Masks**. Integer vectors work the same way, one stepped curve per component.


![Stepped Number Channel](numbers_stepped_channel.png)

*Light World � Num Shadow Cascadesstepping from 4 to 10 to 16. The curve holds flat and jumps at each key, and the Inspector reports the type asInt*


#### Booleans


A channel of this kind holds a simple on or off value, such as **Node � Enabled** or **Material � Two Sided**. The row is drawn to match: instead of a line of diamonds, the stretches where the value is on are filled as a bar.


![Bool Channel](bool_channel.png)

*Node � Enabledblinking a light on and off. The spans where the value is on are filled as a bar, and the key value is a checkbox rather than a number*


Double-click a key to flip it. Some parameters are stored as numbers but drive a flag, such as **Material � Transparent**; the sequencer treats them as flags too.


#### Enumerations


Some values are a choice among fixed options - **Light Omni � Shape Type**, **Camera � Projection Mode**, **Render � Tonemapper Mode**. The channel shows the named options rather than a raw number, and its keys step from one to the next: there is no halfway between Low and High.


![Enumeration Channel](enumeration_channel.png)

*Light Omni � Shape Typestepping through its options. The key value is picked from the list the parameter itself declares, and the row prints the name of the option under the playhead*


#### References and Text


An asset, a node or a piece of text cannot be blended at all - there is no value between two materials or two nodes. **Decal � Material GUID**, **Player Persecutor � Target** and **Node � Name** are channels of this kind.


![Discrete Values Channel](discrete_channel.png)

*Player Persecutor � Targetswitching which node the camera follows. There is nothing numeric to plot, so the curve stays flat and the work is done in the Dope Sheet; the key value is a node picker*


The key value field matches what is being referenced: an asset picker, a node picker, or a plain text box.


### Channels That Hold Clips


Six kinds of channel work the other way round. Instead of keys they take clips, and each clip carries a piece of content that already exists: a sound, a stretch of character animation, a camera, another sequence, or a span during which an event is held open.


![Channels holding clips](clips.png)

*A sequence holding both kinds.Camera Cuts,Skeletal Animation,MusicandEvent Rangecarry clips, whileNode � Positionat the bottom carries keys*


How clips are trimmed, retimed and blended is covered in the [**Clips**](../../../../editor2/tools/sequencer/clips/index.md) article, and each of these channels has an article of its own in the [**Channel Reference**](../../../../editor2/tools/sequencer/channel_reference/index.md).


## Extrapolation


The keys of a channel cover only a stretch of the timeline, from the first key to the last. **Extrapolation** decides what the value does outside that stretch, and you set it per side with the **Pre Infinity** and **Post Infinity** properties. This is how a channel controls the whole timeline without keying every moment of it.


Say you keyed a light's brightness only between second 2 and second 5. Extrapolation decides what happens before and after:


| Mode | Behavior |
|---|---|
| **Constant** | Holds the edge value. The default: dark until second 2, bright after second 5. |
| **Linear** | Continues along the slope of the two edge keys, so the light keeps brightening past second 5. |
| **Cycle** | Repeats the keyed range end to end, looping the 2-to-5 change over the whole timeline. |
| **Ping-Pong** | Repeats it mirrored, so the change plays forward, then backward, and so on. |

  ![](extrapolation_constant.png)
*Constant: the edge value is held, so the curve runs flat before the first key and after the last.*

  ![](extrapolation_linear.png)
*Linear: the slope of the edge keys carries on, so the value keeps rising past the last key and falls away before the first.*

  ![](extrapolation_cycle.png)
*Cycle: the keyed range repeats end to end, jumping back to the first value each time it comes round.*

  ![](extrapolation_ping_pong.png)
*Ping-Pong: the keyed range repeats mirrored, running forward and then backward in turn.*


## Constant Speed


Keys divide the timeline into stretches, and each stretch takes the time between its keys however far the value travels in it. Where one stretch moves a node a metre and the next moves it fifty, the motion changes speed at the key between them.


**Constant Speed** evens that out. The curve is measured along its own length, and the playhead is remapped through that measurement, so the value travels at a constant speed rather than in constant time. The keys still say where the value goes; what changes is the pace between them.


The property sits with the channel's other settings, and appears only on channels whose value has a length to measure - a floating-point number, a vector of floats or doubles, and a [followed path](../../../../editor2/tools/sequencer/channel_reference/follow_path/index.md). A rotation carries it in the **Angles XYZ** and **Angles ZYX** modes, where each Euler axis is interpolated on its own; in **Quaternion (SLERP)** the segments are already spherical blends and the option is absent. An integer channel does not carry it, and neither does one holding a texture or a name, since there is no distance from one of those to the next.

 Best PracticeReach for it when an even glide matters more than the exact timing of each key - a camera or a prop gliding along a keyed path.
## Parameter Slots


Usually the target is the whole address. A node has one position, so a **Node � Position** channel knows where to write the moment it has its node.


Other parameters belong not to the object as a whole but to a part of it - one surface out of several, one joint of a skeleton, one parameter of a material. Naming the object no longer says which part is meant, so the channel carries one more piece of address: its **slot**.


Where a parameter needs one, a slot field appears under **Channel**. It is named after the part it picks, and it lists what the target actually has. Where a list is only numbered rather than named, the slot reads as a plain number.


Where the part can be addressed both ways, a **Slot Access** field sits above it and the field below sets the index or the name. **By Index** animates the slot at a fixed numeric position, so the channel keeps writing to the third surface whatever it is called. **By Name** finds the slot by its name on each bound target, which is what one channel driving several objects needs when their parts sit in a different order.


![Parameter Slots](parameter_slots.png)

*AnObject � Min Visible Distancechannel. The field is namedSurfaceafter the part it picks, and lists the surfaces this object has, by number and by name*


> **Notice:** If the object has no slots of that kind at all, the field says so and the channel takes no keys. Point it at an object that has them, or the row will stay empty.


## Channel Priority


Where two channels write the same parameter of the same target, the higher one in the list wins.


Where the writing is done by a clip, blending takes over: a clip carries a weight, so it can take part of the value and leave the rest to the row below. How that blend behaves depends on the kind of clip, and is covered in the [Clips](../../../../editor2/tools/sequencer/clips/index.md) article and in each channel's own article.


## See Also


- [Keys and Curves](../../../../editor2/tools/sequencer/keys/index.md)
- [Targets and Binding](../../../../editor2/tools/sequencer/targets/index.md)
- [Sequencer Editor](../../../../editor2/tools/sequencer/editor/index.md)
