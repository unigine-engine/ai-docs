# Text Object


A **Text** object is an object representing a plain text in a 3D space. The text is rendered into a texture that is applied to a flat polygon. It uses trilinear filtering and mipmaps to correctly display the text at any distance. There is no noise influence to the object and it is not distorted by TAA.


The font can be represented as a *TrueType* font (TTF) or as a texture atlas with letters.


![](object_text.png)


### See Also


- The *[ObjectText](../../../api/library/objects/class.objecttext_cpp.md)* class to edit text objects via API


## Adding a Text Object


To add a text object to the scene via UnigineEditor, do the following:


1. [Run](../../../sdk/projects/index_cpp.md#run) the project with UnigineEditor.
2. On the Menu bar, click *Create -> Text*. ![](text_create.png)
3. Place the *Text* object somewhere in the world.


## Editing a Text Object


| Text | Text input field. If the **Rich text** option is enabled, you can use [tags](#tags) for text formatting. |  |  |  |  |
|---|---|---|---|---|---|
| Name | Path to a `*.ttf` file or to a texture atlas with letters. > **Notice:** Names of font files for bold, italic and bold italic fonts must have the `b, i` and `bi` postfixes correspondingly. For example: `myfontb.ttf, myfontbi.ttf`. |  |  |  |  |
| Color | Text color in the RGBA range. |  |  |  |  |
| Wrap Width | Text wrap width in units. The text will wrap if its physical size will be greater than the set value. If 0 is set, text wrapping is disabled. \| ![](wrap_0.png) \| ![](wrap_1.png) \| \|---\|---\| \| *Wrap Width = 0* \| *Wrap Width = 5* \| | ![](wrap_0.png) | ![](wrap_1.png) | *Wrap Width = 0* | *Wrap Width = 5* |
| ![](wrap_0.png) | ![](wrap_1.png) |  |  |  |  |
| *Wrap Width = 0* | *Wrap Width = 5* |  |  |  |  |
| Size | Font size, in dots. The more dots, the higher the size of the font. To match dots with a 3D space, there is a set value: 288 dots per unit. For example, if you have the *Arial* font with the size of 20, the physical height of the letter can be calculated as 20/288=0.0694 units. |  |  |  |  |
| Resolution | Resolution of the texture into which the text will be rendered. The *lower* the value, the less detailed will be the text and the less video memory will be required for the texture. > **Notice:** The resolution doesn't influence the text's physical size. \| ![](resolution_50.png) \| ![](resolution_200.png) \| \|---\|---\| \| *Resolution = 50* \| *Resolution = 200* \| | ![](resolution_50.png) | ![](resolution_200.png) | *Resolution = 50* | *Resolution = 200* |
| ![](resolution_50.png) | ![](resolution_200.png) |  |  |  |  |
| *Resolution = 50* | *Resolution = 200* |  |  |  |  |
| HSpacing | Horizontal spacing between letters (a kerning value). This parameter affects the text's physical size. |  |  |  |  |
| VSpacing | Vertical spacing between letters (a kerning value). This parameter affects the text's physical size. |  |  |  |  |
| Rich text | Flag indicating if the rich text formatting is enabled. The following tags are supported: - **<b>**text**</b>** specifies a bold text. - **<i>**text**</i>** specifies an italic text. - **<br>**text**</br>** inserts a single line break. - **<left>**text**</left>** left-aligns the text. - **<right>**text**</right>** right-aligns the text. - **<center>**text**</center>** center-aligns the text. - **<p align=left\|right\|center\|justify>**text**</p>** specifies the alignment of the text within a paragraph: > **Notice:** Text alignment requires text wrapping to be enabled: the value of the **[Wrap Width](#wrap_width)** parameter must be greater than 0. - left � left-aligns the text - right � right-aligns the text - center � center-aligns the text - justify � stretches the lines so that each line has equal width (like in newspapers and magazines) - **<font size=12 color=magenta face=verdana>** text**</font>** specifies the font face, font size, and color of text. - **<sub>** text**</sub>** defines subscript text. Subscript text appears half a character below the normal line, and is sometimes rendered in a smaller font. - **<sup>** text**</sup>** defines superscript text. Superscript text appears half a character above the normal line, and is sometimes rendered in a smaller font. > **Notice:** **<image/>** and **<table/>** tags are not available. |  |  |  |  |
| Depth Test | Flag indicating if depth test is performed for the text. |  |  |  |  |
| Outline | Flag indicating if the text outline is enabled. The outline looks like the dark shadow in the right lower corner of the text and is displaced by one dot. |  |  |  |  |
