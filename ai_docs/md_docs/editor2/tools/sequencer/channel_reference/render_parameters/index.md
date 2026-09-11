# Render Parameters


A **Render Parameter** channel animates one of your project's own [render parameters](../../../../../content/materials/render_parameters.md) - the custom values declared once for the whole project and read by materials and shaders. Putting one on a curve is how a shader-side effect is driven from a sequence: a dissolve amount, a tint, a wind strength, all of them changing over time without a single object being touched.


These parameters belong to the renderer, not to any object, so the channel has no *Targets* section.


> **Notice:** Render parameters are created outside the Sequencer, in *Settings -> Render -> Custom Parameters*. Until at least one exists there, a Render Parameter channel has nothing to drive.


![Custom render parameters](render_parameters.png)

*Render parameters are declared once for the whole project, each with a name and a type - a float and an int here*


## Choosing the Parameter


The picker offers one entry per value type - **Bool**, **Float**, **Float2** to **Float4**, **Int**, **Int2** to **Int4** - and which parameter of that type is driven is chosen afterwards, in the channel properties.


Two fields do that. **Slot Access** says how the parameter is addressed, and the field under it - renamed to **Param Name** or **Param Index** to match - holds the name or the number:


![Slot Access](render_parameters_channel.png)

*Addressed by name, the field offers the project's render parameters with the type each one holds*


| Slot Access | The field below |
|---|---|
| **By Name** | A list of the project's render parameters, each shown with its type. Picking one also retypes the channel to match that parameter, so the value type never has to be guessed correctly in the menu. |
| **By Index** | The parameter's position in the project list, as a plain number. |

 Best PracticeUse **By Name**. Render parameters are project-wide and their order follows the order they were created in, so an index shifts as soon as one is added or removed - and the channel then drives a different parameter with no warning. A channel is created addressed by index, so this is worth switching straight away.
## See Also


- [Render Settings](../../../../../editor2/settings/render_settings/index.md)
- [Channels](../../../../../editor2/tools/sequencer/channels/index.md)
