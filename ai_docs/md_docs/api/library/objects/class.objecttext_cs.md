# ObjectText Class (CS)

**Inherits from:** Object


The class is used to render [flat text](../../../api/library/objects/class.objecttext_cs.md) in a scene.


### Usage Example


Here is an example of creating *ObjectText* that will rotate following a player`s position, while the rotation of a parent stays the same, which will allow a parent node to move freely and drag a text with itself. To try it yourself, you should [create](../../../principles/component_system/component_system_cs/index.md#create) a component named **TextCreator** and copy the code given below. Then [assign](../../../principles/component_system/component_system_cs/index.md#apply) a component to any desired node, which will be a parent node for the *ObjectText*.


<details>
<summary>TextCreator.cs | Close</summary>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using Unigine;

public partial class TextCreator : Component
{
	// Creating a parameter to define a text
	public String textStr;

	private ObjectText text;

	private void Init()
	{
		// Create Object Text defining font and a string
		text = new ObjectText("font.ttf", textStr);
		text.FontSize = 100;
		text.FontResolution = 100;
		// Defining an object of a component as a parent
		text.Parent = this.node;
	}

	private void Update()
	{
		// Rotate a text to always look at a player
		// The pivot point will look at a player, so the text needs a little bit of tweaking
		text.WorldLookAt(Game.Player.WorldPosition);
		// Rotate text a little bit so it shows up properly
		text.Rotate(270, 0, 180);
	}
}

```

</details>


## ObjectText Class

### Properties

## string Text

The text set in the node.
## vec4 TextColor

The color of the text.
## float TextWrapWidth

The text wrap width in units. The text will wrap if its physical size will be greater than the set value.
## int DepthTest

The value indicating if the text object uses depth test.
## int FontOutline

The flag indicating if the text [outline](#setFontOutline_int_void) is enabled.
## int FontVSpacing

The vertical spacing between letters (kerning value). This parameter influences the text's physical size.
## int FontHSpacing

The horizontal spacing between letters (kerning value). This parameter influences the text's physical size.
## int FontResolution

The resolution of the texture into which the text will be rendered. The lower the value, the less detailed will be the text, the less video memory will be required for the texture. It doesn't influence the text's physical size.
## int FontSize

The size of the text font. The more dots, the higher the size of the font. To match dots with a 3D space, there is a set value: **288** dots per unit. For example, if you have the *Arial* font with the size of **20**, the physical height of the letter can be calculated as 20/288=0.0694 units.
## int FontRich

The flag indicating if the rich text is enabled. When enabled, the following tags can be used for text formatting:
- **<b>**text**</b>** specifies a bold text.
- **<i>**text**</i>** specifies an italic text.
- **<br>**text**<br/>** inserts a single line break.
- **<left>**text**</left>** left-aligns the text.
- **<right>**text**</right>** right-aligns the text.
- **<center>**text**</center>** center-aligns the text.
- **<p align=left|right|center|justify>**text**</p>** specifies the alignment of the text within a paragraph: > **Notice:** Text alignment requires text wrapping to be enabled: the value of the [**Wrap Width**](#setTextWrapWidth_float_void) parameter must be greater than 0.

  - *left* - left-aligns the text
  - *right* - right-aligns the text
  - *center* - center-aligns the text
  - *justify* - stretches the lines so that each line has equal width (like in newspapers and magazines)
- **<font size=12 color=magenta face=verdana>** text**</font>** specifies the font face, font size, and color of text.
- **<sub>** text**</sub>** defines subscript text. Subscript text appears half a character below the normal line, and is sometimes rendered in a smaller font.
- **<sup>** text**</sup>** defines superscript text. Superscript text appears half a character above the normal line, and is sometimes rendered in a smaller font.


> **Notice:** **<image/>** and **<table/>** tags are not available.


## string FontName

The path to the TTF font.
> **Notice:** Names of font files for bold, italic and bold italic fonts must have the b, i and bi postfixes correspondingly. For example: `myfontb.ttf`, `myfontbi.ttf`.


## 🔒︎ float TextWidth

The width of the text.
## 🔒︎ float TextHeight

The height of the text.
## 🔒︎ float TextAspect

The text aspect value, the proportional relationship between the text width and height.
## 🔒︎ int TextNumLines

The number of lines in the text.
## Gui.TextDirection TextDirection

The base paragraph direction of the object's text, matching the *Gui::TEXT_DIRECTION_** values: automatic detection from the text content (default), left-to-right, or right-to-left.
### Members

---

## ObjectText ( )

Default constructor. Creates an empty object with no text and font set.
## ObjectText ( string font_name )

Constructor. Creates an object with no text but with the specified font.
### Arguments

- *string* **font_name** - The path to the TTF font relatively to the `data` directory.

## ObjectText ( string font_name , string text )

Constructor. Creates an object with the set font and text.
### Arguments

- *string* **font_name** - The path to the TTF font relatively to the `data` directory.
- *string* **text** - The text (can be either plain or rich).
