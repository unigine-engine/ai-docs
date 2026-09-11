# ObjectText Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

**Inherits from:** Object


The class is used to render [flat text](../../../api/library/objects/class.objecttext_usc.md) in a scene.


## ObjectText Class

### Members

## void setText ( string text )

Sets a new text set in the node.
### Arguments

- *string* **text** - The text set in the node.

## const char * getText () const

Returns the current text set in the node.
### Return value

Current text set in the node.
## void setTextColor ( vec4 color )

Sets a new color of the text.
### Arguments

- *vec4* **color** - The color of the text in the RGBA range.

## vec4 getTextColor () const

Returns the current color of the text.
### Return value

Current color of the text in the RGBA range.
## void setTextWrapWidth ( float width )

Sets a new text wrap width in units. The text will wrap if its physical size will be greater than the set value.
### Arguments

- *float* **width** - The [text wrap width](#setTextWrapWidth_float_void) in units. The value of 0 means that text wrapping is disabled.

## float getTextWrapWidth () const

Returns the current text wrap width in units. The text will wrap if its physical size will be greater than the set value.
### Return value

Current [text wrap width](#setTextWrapWidth_float_void) in units. The value of 0 means that text wrapping is disabled.
## void setDepthTest ( int test )

Sets a new value indicating if the text object uses depth test.
### Arguments

- *int* **test** - The value indicating if the text object uses depth test

## int getDepthTest () const

Returns the current value indicating if the text object uses depth test.
### Return value

Current value indicating if the text object uses depth test
## void setFontOutline ( int outline )

Sets a new flag indicating if the text [outline](#setFontOutline_int_void) is enabled.
### Arguments

- *int* **outline** - The value indicating if the text outline is enabled

## int getFontOutline () const

Returns the current flag indicating if the text [outline](#setFontOutline_int_void) is enabled.
### Return value

Current value indicating if the text outline is enabled
## void setFontVSpacing ( int vspacing )

Sets a new vertical spacing between letters (kerning value). This parameter influences the text's physical size.
### Arguments

- *int* **vspacing** - The vertical spacing value.

## int getFontVSpacing () const

Returns the current vertical spacing between letters (kerning value). This parameter influences the text's physical size.
### Return value

Current vertical spacing value.
## void setFontHSpacing ( int hspacing )

Sets a new horizontal spacing between letters (kerning value). This parameter influences the text's physical size.
### Arguments

- *int* **hspacing** - The horizontal spacing value.

## int getFontHSpacing () const

Returns the current horizontal spacing between letters (kerning value). This parameter influences the text's physical size.
### Return value

Current horizontal spacing value.
## void setFontResolution ( int resolution )

Sets a new resolution of the texture into which the text will be rendered. The lower the value, the less detailed will be the text, the less video memory will be required for the texture. It doesn't influence the text's physical size.
### Arguments

- *int* **resolution** - The text font resolution value.

## int getFontResolution () const

Returns the current resolution of the texture into which the text will be rendered. The lower the value, the less detailed will be the text, the less video memory will be required for the texture. It doesn't influence the text's physical size.
### Return value

Current text font resolution value.
## void setFontSize ( int size )

Sets a new size of the text font. The more dots, the higher the size of the font. To match dots with a 3D space, there is a set value: **288** dots per unit. For example, if you have the *Arial* font with the size of **20**, the physical height of the letter can be calculated as 20/288=0.0694 units.
### Arguments

- *int* **size** - The size of the text font, in dots.

## int getFontSize () const

Returns the current size of the text font. The more dots, the higher the size of the font. To match dots with a 3D space, there is a set value: **288** dots per unit. For example, if you have the *Arial* font with the size of **20**, the physical height of the letter can be calculated as 20/288=0.0694 units.
### Return value

Current size of the text font, in dots.
## void setFontRich ( int rich )

Sets a new flag indicating if the rich text is enabled. When enabled, the following tags can be used for text formatting:
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


### Arguments

- *int* **rich** - The value indicating if the rich text is enabled

## int getFontRich () const

Returns the current flag indicating if the rich text is enabled. When enabled, the following tags can be used for text formatting:
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


### Return value

Current value indicating if the rich text is enabled
## void setFontName ( string name )

Sets a new path to the TTF font.
> **Notice:** Names of font files for bold, italic and bold italic fonts must have the b, i and bi postfixes correspondingly. For example: `myfontb.ttf`, `myfontbi.ttf`.


### Arguments

- *string* **name** - The path to the TTF font relative to the `data` directory.

## const char * getFontName () const

Returns the current path to the TTF font.
> **Notice:** Names of font files for bold, italic and bold italic fonts must have the b, i and bi postfixes correspondingly. For example: `myfontb.ttf`, `myfontbi.ttf`.


### Return value

Current path to the TTF font relative to the `data` directory.
## float getTextWidth () const

Returns the current width of the text.
### Return value

Current width of the text, in units.
## float getTextHeight () const

Returns the current height of the text.
### Return value

Current height of the text, in units.
## float getTextAspect () const

Returns the current text aspect value, the proportional relationship between the text width and height.
### Return value

Current proportional relationship between the text width and height.
## int getTextNumLines () const

Returns the current number of lines in the text.
### Return value

Current number of lines in the text.
## void setTextDirection ( int direction )

Sets a new base paragraph direction of the object's text, matching the *Gui::TEXT_DIRECTION_** values: automatic detection from the text content (default), left-to-right, or right-to-left.
### Arguments

- *int* **direction** - The base direction of the object text

## int getTextDirection () const

Returns the current base paragraph direction of the object's text, matching the *Gui::TEXT_DIRECTION_** values: automatic detection from the text content (default), left-to-right, or right-to-left.
### Return value

Current base direction of the object text
---

## static ObjectText ( )

Default constructor. Creates an empty object with no text and font set.
## static ObjectText ( string font_name )

Constructor. Creates an object with no text but with the specified font.
### Arguments

- *string* **font_name** - The path to the TTF font relatively to the `data` directory.

## static ObjectText ( string font_name , string text )

Constructor. Creates an object with the set font and text.
### Arguments

- *string* **font_name** - The path to the TTF font relatively to the `data` directory.
- *string* **text** - The text (can be either plain or rich).
