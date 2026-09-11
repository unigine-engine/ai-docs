# Property


A **Property** channel animates one parameter of a property - a value declared in a `*.prop` file and read by your own code or by the engine.


The same property lives in three places at once: in its file, on a node it is assigned to, and on a single surface of a node. Which of them the channel edits is up to you, and it decides how far the change reaches. So the channel is filled in from the top down: where the property is taken from, which objects, which of their properties, and finally which parameter inside it.


## Where the Property Is Taken From


The **Access** setting is the first choice, and everything below it follows from it:


![Access](property_access.png)

*Accessdecides where the property is taken from, and the fields below it follow that choice*


| Access | The target list holds | What it changes |
|---|---|---|
| **Asset** | `*.prop` files. **Direct** names one; **By Inheritance** takes one as a root and drives everything inherited from it. | The property file itself, so everything using it changes together. |
| **Node** | Nodes, named or found by a rule. | The property assigned to the node. |
| **Surface** | Nodes, named or found by a rule. | The property assigned to one surface of the node. |


The list itself works the same as on any other channel, so one channel can drive a whole set at once. See the [Targets](../../../../../editor2/tools/sequencer/targets/index.md) article.


Taking the property from a surface leaves one more thing to say, which surface, and that field sits below the list. While the list names one object it is a picker holding the surfaces that object actually has; as soon as the list describes a set, it becomes a **Surface Pattern** wildcard with a match count of its own. An empty pattern matches nothing, so write * to take every surface.


## Which Parameter Inside It


A property holds many parameters, so a **Param Path** field at the bottom says which one the channel drives. Entries read as *Title (Type)*, and a parameter that sits inside a structure is shown as the whole path to it.


![Param Path](param_path_example.png)

*The property is named above, soParam Pathoffers the parameters that property actually has, each with the kind of value it holds*


Picking here can **retype the channel**: a parameter that calls for a different kind of value rebuilds the channel to match. Keys already placed are carried over - by time, and by as many components as the new type accepts. Anything that cannot be carried over, such as the extra components when a vector becomes a single number, is reported in the console.


> **Notice:** A Property channel is created in the opposite order to the one you think in. The picker asks for the **value type** first - *Property Parameter -> Value Float*, *Value Int*, *Value Color* and so on - and only afterwards, in the channel properties, does **Param Path** name the parameter itself.
>
>
> A wrong guess costs nothing. Picking the parameter in **Param Path** rebuilds the channel to the type that parameter needs.


## See Also


- [Targets](../../../../../editor2/tools/sequencer/targets/index.md)
- [Channels](../../../../../editor2/tools/sequencer/channels/index.md)
