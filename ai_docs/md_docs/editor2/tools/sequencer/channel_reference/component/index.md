# Component


A **Component** channel animates a field of one of your own components, C++ or C# alike. Use it when the value you want to drive lives in your game code rather than in a built-in engine parameter. The channel writes the field by the name it carries in code.


## Setting It Up


A Component channel is filled in from the top of its properties down, and the order matters because each choice fills the control below it:


1. **Component** - the component class the channel drives. The list holds every component class in the project, C++ and C# alike.
2. **Targets** - the nodes carrying that component. One named node, or a rule that finds many; the list works the same as on any other channel, so a single curve can drive every instance at once. See the [Targets](../../../../../editor2/tools/sequencer/targets/index.md) article.
3. **Field** - which field of the component to animate. Picking one retypes the channel to that field's value type.


![Component channel](component_channel.png)

*A Component channel filled in: the class, the node carrying it, and the field to animate*


A node can carry several components, including two of the same class. The channel records which one it means along with the class, so the right instance is driven even when a node carries more than one. Where a target carries them in a different order, the channel falls back to the first component of that class it finds there.


> **Notice:** This is why the order matters: the class list narrows once a target resolves. With nothing bound it offers every class in the project, and afterwards only the classes the first target actually carries.


## Which Fields Are Listed


Nearly every field can be animated: a number, a vector, a color, a flag, an enumeration, a mask, and the string, file, node, material and property references. How a field's keys behave follows its type, the same as any other parameter (see the [Channels](../../../../../editor2/tools/sequencer/channels/index.md) article): continuous values interpolate along the curve, discrete ones hold between keys and switch at each one.


![Field picker](component_fields.png)

*TheFieldpicker lists what the class declares, each with the kind of value it holds*


> **Notice:** Three field types are missing from the picker: an array, a struct, and a curve.


## Reading the Value in Code


Nothing has to be written to make this work. The channel writes into the field the component already declares, so the code that uses that field needs no change.


> **Notice:** A C# field takes one more step than a C++ one. Its value goes into a buffer that the managed side drains on the following frame, so a C# component reads it a frame after the sequence produced it.


Two players driving one field do not blend. Their writes are applied in the order they arrive, so the last one wins.


## See Also


- [Targets](../../../../../editor2/tools/sequencer/targets/index.md)
- [Channels](../../../../../editor2/tools/sequencer/channels/index.md)
