# Material


A **Material** channel animates a parameter of a material, so a surface changes over time. It reaches everything a material is made of: its parameters, its states, its textures, and the options it renders with. All of them are described in [Setting Up Materials](../../../../../editor2/materials_settings/index.md) article.


![Material channels](material_channel.png)

*Three Material channels on one material. The colour one is drawn as a ramp, the two numbers as ordinary curves*


The first choice is **Access**, because it says what the channel points at, and how far the change reaches follows from that:


- **Asset** points at a material file, so the change reaches every object using that material.
- **Surface** points at the material on one object's surface, leaving every other object alone.


![Access](material_channel_access.png)

*Accessdecides what the channel points at, and the fields below it follow that choice*


The rest of the channel follows from that choice, so the two are described apart below. Picking the parameter works the same either way.


## Animating a Material Asset


On **Asset** the target list holds material files, `*.mat` or `*.mgraph`. Animate one and every object wearing it changes together, so a single curve can dim the glass of every lamp in a level.


A target is named in one of two ways:


| **Direct** | Names one material. |
|---|---|
| **By Inheritance** | Takes a material as a root and drives everything inherited from it, however deep the chain runs, so a base material and all of its variants animate as one. See [Hierarchy and Inheritance](../../../../../content/materials/inheritance.md). |


![Asset target](material_channel_asset_target.png)

*A material target is named outright or taken as the root of an inheritance chain*


> **Notice:** An asset list has no **Scope**. A scope narrows a search through the scene, and a material hierarchy is not part of the scene.


This case has a shortcut. Right-click the parameter in the material editor and choose *Set Key in Sequencer*: the channel is created pointing at that material, already addressed [by name](#slot_access), with a key holding the current value.


![Set Key in Sequencer](set_key_in_sequencer_material.png)

*Right-clicking a parameter in the material editor. The channel is created, pointed at this material, and keyed in one step*


> **Notice:** *Set Key in Sequencer* always binds the material as an asset. A channel that has to reach one surface alone is built by hand.


## Animating an Object's Surface


On **Surface** the target list holds objects in the world instead, named the way they are on any other channel: one object, or a rule that finds many. See the [Targets](../../../../../editor2/tools/sequencer/targets/index.md) article.


The engine gives the driven surface an inherited material of its own while the channel runs, and hands it back afterwards, so the shared file and every other object using it are left untouched.


One more field says which surface carries the material, and it changes shape with the target. While the list names one object it is a picker holding the surfaces that object actually has. As soon as a rule describes a set, the matched objects differ from one another and no single list applies, so the field becomes a **Surface Pattern** wildcard with a match count of its own. An empty pattern matches nothing, so write * to take every surface.


![Surface access](surface_access.png)

*A rule and a surface pattern together, each reporting what it found: the rule 14 objects, the pattern*_lod_2five surfaces among them*

 Best PracticeThe two levels of fan-out combine. A rule that finds every object of a type, plus a surface pattern of *, drives every surface of every matched object from a single curve.
## Choosing the Parameter


This part is the same in both modes. The channel is created empty, so the material comes first: the list is filled from the first target named directly, and holds whatever that material declares. However the material editor lays it out, in tabs or in groups of its own, the Sequencer offers it as one list:


- Its **parameters**, as a color, a number, or their vector forms.
- Its **states**. The ones a material keeps for itself are left out.
- Its **textures**, by the file that fills the slot, and only the slots the material lets you edit. A texture cannot blend into another, so these are stepped keys, each holding a texture until the next one. See [Stepped Values](../../../../../editor2/tools/sequencer/channels/index.md#switching_values).


Picking an entry retypes the channel to the kind of value that entry holds, so the value type never has to be guessed correctly in the menu.


With no target named directly there is nothing to read from, and the field falls back to plain text for the name to be typed in. This is normal while a channel is being set up, and the picker returns as soon as a material is named.


> **Notice:** A material's **options**, such as [Two Sided](../../../../../editor2/materials_settings/index.md#two_sided) or the [rendering order](../../../../../editor2/materials_settings/index.md#order), are not in that list. Every material has the same ones rather than declaring its own, so they are picked in the *ENGINE PARAMETERS* half of the picker, each under its own name.


## Addressing the Slot by Index or by Name


A material keeps its parameters, states and textures as numbered lists, so a channel has to say which entry it drives. The **Slot Access** switch says how: **By Name** finds the entry by the name it carries in the material, **By Index** takes the one sitting at a fixed position. The **Parameter** field changes to match, holding a name or a number. A new Material channel already comes addressed by name.


![Slot Access](material_slot_access.png)

*Slot Accessdecides how the entry is addressed, andParameterabove it holds the name or the number*


Prefer **By Name**. A name survives the base material being edited, while a position does not: add an entry or reorder them and the index leads somewhere else. The two failures differ, too. An index that does not exist shows as **(no slot)**, and the channel takes no keys, as described in [Targets](../../../../../editor2/tools/sequencer/targets/index.md#reading). An index that still exists but now leads elsewhere looks perfectly healthy, and the channel drives the wrong entry.


## See Also


- [Setting Up Materials](../../../../../editor2/materials_settings/index.md)
- [Targets](../../../../../editor2/tools/sequencer/targets/index.md)
- [Channels](../../../../../editor2/tools/sequencer/channels/index.md)
