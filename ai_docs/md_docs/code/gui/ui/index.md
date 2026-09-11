# UI Files


All GUI elements in Unigine are generated on the fly from UI files, which are in the XML format. These files describe [containers](../../../code/gui/ui/ui_containers.md) and [widgets](../../../code/gui/ui/ui_widgets.md) provided by Unigine. Each of them is described by an XML tag in the UI file.


## UI File Syntax


As a correct XML file, a UI file must start with a standard declaration. The second required element is a root tag *ui*. This root element can contain zero or more other elements (tags) specifying the interface.


```xml
<?xml version="1.0" encoding="utf-8"?>
<ui version="1.0">
</ui>

```


If a UI file is not syntactically correct, Unigine will log the error to the console and the main log file.


> **Notice:** All UI files are treated as having the UTF-8 encoding, even if you specify another one in the declaration.
>  Not all available GUI elements can be defined using XML. Some of them � like manipulators and specialized dialogs and sprites - are set up only via [scripting](../../../api/library/gui/index.md):
>
>
> - [WidgetManipulator](../../../api/library/gui/class.widgetmanipulator_cpp.md)
> - [WidgetManipulatorRotator](../../../api/library/gui/class.widgetmanipulatorrotator_cpp.md)
> - [WidgetManipulatorScaler](../../../api/library/gui/class.widgetmanipulatorscaler_cpp.md)
> - [WidgetManipulatorTranslator](../../../api/library/gui/class.widgetmanipulatortranslator_cpp.md)
> - [WidgetDialogColor](../../../api/library/gui/class.widgetdialogcolor_cpp.md)
> - [WidgetDialogFile](../../../api/library/gui/class.widgetdialogfile_cpp.md)
> - [WidgetDialogImage](../../../api/library/gui/class.widgetdialogimage_cpp.md)
> - [WidgetDialogMessage](../../../api/library/gui/class.widgetdialogmessage_cpp.md)
> - [WidgetSpriteNode](../../../api/library/gui/class.widgetspritenode_cpp.md)
> - [WidgetSpriteShader](../../../api/library/gui/class.widgetspriteshader_cpp.md)
> - [WidgetSpriteVideo](../../../api/library/gui/class.widgetspritevideo_cpp.md)
> - [WidgetSpriteViewport](../../../api/library/gui/class.widgetspriteviewport_cpp.md)


### Attributes


Almost all of the UI file tags have attributes, and it is good to know the following general rules:


- All dimensions provided as attribute values are in pixels.
- File names are relative to the [root data directory](../../../principles/filesystem/index_cpp.md#paths).
- Colors are in the Web format, that is, #RRGGBB, or in the #RRGGBBAA format. Here RR, GG, BB, and AA correspond to a hexadecimal color component value�red, green, blue, and alpha, respectively; values range from 00 to FF.
- Boolean values can be set in different forms. For FALSE use: 0, false, no. For TRUE use: 1, true, yes.


Here is an example element with attributes:


```xml
<sprite align="overlap,top,right" pos_x="10" pos_y="-42" texture="data/core/gui/unigine.png"/>
```


### Comments


You can use standard XML comments syntax. Comment blocks will be skipped during processing of a UI file. An example comment:


```xml
<!--
This section will be omitted
-->

```


## Common Attributes


All GUI elements�both [containers](../../../code/gui/ui/ui_containers.md) and [widgets](../../../code/gui/ui/ui_widgets.md) �can have the following attributes.


### name


A unique name of the widget. If the [export](#param_export) flag is set to **yes**, the widget will be referred to in scripts by this name. The name may contain a namespace specification and/or an array index.


```xml
<!-- The following widget will be accessible via scripts as foo::bar -->
<button name="foo::bar" export="yes"/>
<!-- This widget will be accessible via scripts as fooArray[2] -->
<button name="fooArray[2]" export="yes"/>

```


### next


A name of a widget that receives the focus next, if the user presses the TAB key. If this attribute is omitted, the widget that immediately follows the current one will receive the focus.


```xml
<!-- Custom focus order: button_0�-> button_2�-> button_1 -->
<button name="button_0" next="button_2"/>
<button name="button_1" next="button_0"/>
<button name="button_2" next="button_1"/>

```


### align


A set of alignment flags for the widget. Flags are separated by commas. Available flags are:


- **center** Centers the widget in both dimensions in the available space. ![align center](parameters/align_center.png) ```xml <window name="Test::window" width="150" height="150" export="1" sizeable="1"> <text>Window Title</text> <label align="center"> <text size="20">Label Center</text> </label> </window> ```
- **left** Aligns the widget to the left side. ![align left](parameters/align_left.png) ```xml <label align="left"> <text size="20">Label Left</text> </label> ```
- **right** Aligns the widget to the right side. ![align right](parameters/align_right.png) ```xml <label align="right"> <text size="20">Label Right</text> </label> ```
- **top** Aligns the widget to the top. ![align top](parameters/align_top.png) ```xml <label align="top"> <text size="20">Label Top</text> </label> ```
- **bottom** Aligns the widget to the bottom. ![align bottom](parameters/align_bottom.png) ```xml <label align="bottom"> <text size="20">Label Bottom</text> </label> ```
- **expand** Justifies the text in the available space. ![no expand](parameters/align_expand_0.png) ![expand](parameters/align_expand_1.png) ```xml <vscroll name="Test::vscroll_0" export="1" align="expand"/> <vscroll name="Test::vscroll_1" export="1"/> ```
- **overlap** Places the widget over the contents of the parent container. ![overlap](parameters/align_overlap.png) ```xml <label align="left"> <text size="35">Label</text> </label> <button name="Test::button" export="1"  align="overlap"> <text>Button</text> </button> ```
- **background** Places the widget underneath other widgets in the same container. Use this flag together with *[overlap](#overlap)* one.
- **fixed** Places the widget in focus on the background or on the foreground (depending on where it was created). This flag is valid only if *[overlap](#overlap)* flag is also set. Non-fixed overlapping windows can pop over the fixed ones, while the latter cannot do it.


### enabled


A flag that specifies whether the widget is enabled. An enabled widget receives keyboard and mouse events; a disabled widget does not. Some widgets display themselves differently when they are disabled (usually they are dimmed). If a container is disabled, its content is also disabled. Acceptable values:


- **0** or **no** The widget is disabled.
- **1** or **yes** The widget is enabled.


![enabled](parameters/enabled.png)


```xml
<button name="Test::button" export="1"  enabled="1">
	<text size="15">Button Enabled</text>
</button>
<button name="Test::disabled_button" export="1" enabled="0">
	<text size="15">Button Disabled</text>
</button>

```


### hidden


A flag that specifies whether the widget is hidden or not. When a widget is hidden, it is not rendered, and other widgets in the same container are re-arranged. Acceptable values:


- **0** or **no** The widget renders normally.
- **1** or **yes** The widget is hidden.


![not hidden](parameters/hidden_0.png) ![hidden](parameters/hidden_1.png)


```xml
<label>
	<text size="20" rich="1">Label 0</text>
</label>
<button name="Test::button" export="1"  hidden="1">
	<text size="15">Button Hidden</text>
</button>
<label>
	<text size="20" rich="1">Label 1</text>
</label>
<label>
	<text size="20" rich="1">Label 2</text>
</label>
<button name="Test::disabled_button" export="1" hidden="0">
	<text size="15">Button Rendered</text>
</button>

```


### pos_x


The *x* -coordinate of the widget relative to the top left corner of its parent container. It takes effect only if the **overlap** [alignment flag](#param_align) is set.


![pos_x](parameters/pos_x.png)


```xml
<button name="Test::button" export="1" align="overlap" pos_x="40">
	<text size="15">Button</text>
<button>

```


### pos_y


The *y* -coordinate of the widget relative to the top left corner its parent container (Y-values increase top down - higher value results in lower position). It takes effect only if the **overlap** [alignment flag](#param_align) is set.


![pos_y](parameters/pos_y.png)


```xml
<button name="Test::button" export="1" align="overlap" pos_y="30">
	<text size="15">Button</text>
<button>

```


### width


Width of a widget.


### height


Height of a widget.


### export


A flag that specifies whether to export a reference to the widget or not. If yes, the widget will be exported with the name set using the *[name](#param_name)* attribute. The default value is **0**. Acceptable values:


- **0** or **no** (default) The widget will not be exported.
- **1** or **yes** The widget will be exported.


### reference


A flag indicating whether a container is referenced by the [*reference*](#reference) tag. Acceptable values:


- no reference flag or **0** (default) The container will be shown in the UI as usual.
- **1** The container will not be shown in the UI and you will be able to refer it by using the [*reference*](#reference) tag.


## Text Tags and Formatting


There are tags that used for outputting and formatting text.


### text


Many [widgets](../../../code/gui/ui/ui_widgets.md) and [containers](../../../code/gui/ui/ui_containers.md) have a *text* child, which provides some formatting capabilities.


Attributes:


- *rich* Whether the text inside the tag is formatted or plain. The default is **0** (boolean), which corresponds to plain.
- *face* Path to a TrueType font file, which will be used by default. ```xml <text face="fontb.ttf">Text</text> ```
- *size* Default font size (pixels). ```xml <text size="20">Text</text> ```
- *color* Default font color. ```xml <text color="#ff0000">Text</text> ```
- *permanent* Whether a text color should be changed when the widget is disabled (non active), transparent (enabled option on non-active window), or widget loses focus. The default is 0 (not to change the color). For example, when the window is disabled, the second label doesn't change its color. ![no permanent / permanent](parameters/permanent.png) ```xml <window name="Test::window" width="150" height="150" export="1" sizeable="1" enabled="0"> <text>Window Title</text> <label><text permanent="0">Label 0</text></label> <label><text permanent="0">Label 1</text></label> </window> ```
- *outline* Whether the text should be outlined. The default is **0** (boolean), which corresponds to no outlining. ![no outline / outlined](parameters/outline.png) The outlined text is represented on the right picture. ```xml <label><text size="20" outline="1">Label 0</text></label> ```
- *wrap* Whether the text should be wrapped around, if it does not fit width of the container. The default is **0** (boolean), which corresponds to no wrapping. ![wrap](parameters/wrap_1.png) ```xml <label><text size="20" wrap="1">Long text to wrap</text></label> ```
- *hspacing* Horizontal spacing (in pixels) between letters. The default is **0**. ![horizontal spacing](parameters/hspacing.png) ```xml <label align="center"><text size="20" hspacing="8">Text</text></label> ```
- *vspacing* Vertical spacing (in pixels) between text lines. The default is **0**. ![vertical spacing](parameters/vspacing.png) ```xml <label align="center"><text size="20" vspacing="15" rich="1">Text<br/>Text<br/>Text</text></label> ```
- *hoffset* Horizontal text offset (in pixels). The default is **0** (no offset). ![horizontal offset](parameters/hoffset.png) ```xml <label align="center"><text size="20" hoffset="35">Text</text></label> ```
- *voffset* Vertical text offset (in pixels). The default is **0** (no offset). ![vertical offset](parameters/voffset.png) ```xml <label align="center"><text size="20" hoffset="35" voffset="35">Text</text></label> ```
- *translate* Whether the text can be translated. The default is **1** (boolean), which means that the text depends on the selected language.


### font


![font formatting](widgets/font.png)


Enables to change font characteristics of widgets and containers. This tag can be applied to a group of widgets or containers. The list of attributes is the same as for the [*text*](#text) tag except the*translate* attribute. This attribute should be applied to a text or a label individually (see the example below).


> **Notice:** If the *rich* attribute is set to 1, all available [rich text formatting](#rich_text) tags can be applied to the text of any widget inside the group.


Also the font size can be calculated relatively to its current size. For example:


```xml
<font size="+10">Larger</font>
<font size="-4">Smaller</font>
<font size="%200">Same or smaller</font>

```


The following example demonstrates how to apply the font to the group of widgets:


```xml
<vbox>
	<font size="13" rich="1" outline="1">
		<align align="left">
			<label face="fontb.ttf" size="15" color="#ff9900">Labels</label>
			<label translate="1">Label <b>1</b></label><!-- this label can be translated -->
			<label>Label <b>2</b></label>
			<label><font size="17">Label of bigger size</font></label>
			<label>Label <b>4</b></label>
		</align>
	</font>
</vbox>

```


In the result, the following will be shown:


![](widgets/font_group.png)


Font tags can be nested. However, the following restrictions exist:


- If the nested *font* tag is applied to a widget or a container, font properties are not inherited. ```xml <font size="13" rich="1" outline="1"> <align align="left"> <label face="fontb.ttf" size="15" color="#ff9900">Labels</label> <label>Label <b>1</b></label> <font size="20" rich="1"> <label>Label <b>2</b></label> </font> </align> </font> ``` In the result, *Label 2* will not be outlined: ![](widgets/font_widget.png)
- If the *font* tag is applied to the rich text inside a widget or a container, font properties are inherited. > **Notice:** In this case, the list of font attributes will differ. See the details [below](#font_rich). ```xml <font size="13" rich="1" outline="1"> <align align="left"> <label>Label <b>1</b></label> <label><font size="17">Label of bigger size</font></label> </align> </font> ``` In the result, the font characteristics will be inherited: ![](widgets/font_text.png)


### align


Unlike the *align* attribute of the [*text*](#text) tag, the*align* tag can be applied to a group of widgets.


Attributes:


- *align* Acceptable values are center, left, right.


For example:


```xml
<align align="right">
	<label><text>Title1</text></label>
	<edittext name="Test::edittext_1" export="1" width="100" height="100">
		<text>EditLine1</text>
	</edittext>
	<label><text>Title2</text></label>
	<edittext name="Test::edittext_2" export="1" width="100" height="100">
		<text>EditLine2</text>
	</edittext>
</align>

```


All of the elements inside the *align* tag are right-aligned:


![](widgets/align_tag.png)


### Rich Text Formatting


If the *rich* attribute of the [*text*](#text) or [*font*](#font) tag is equal to **1**, **yes** or **true**, the following tags and entities can be used to format the text inside them:


#### br


Line break.


> **Notice:** Both the **<br>** and **<br/>** notations are valid.


```xml
<text rich="1">Text 1 <br/>
Text 2<br>Text 3</text>

```


#### p


Paragraph. Acceptable attributes: *align* with values **center, left, right, justify**.


#### center


Centered alignment. Equivalent to *<p align="center">text</p>*.


#### font


Font characteristics. This tag enables to change default font characteristics. It differs from the *font* tag, which is described above.


> **Notice:** Font tags applied to a rich text can be nested, all font properties are inherited in this case.


Acceptable attributes:


- *face* Path to a TrueType font file.
- *size* Font size (pixels).
- *color* Font color.
- *outline* Whether the text should be outlined. The default is 0 (boolean), which corresponds to no outlining.
- *hspacing* Horizontal spacing (in pixels) between letters. The default is 0.
- *vspacing* Vertical spacing (in pixels) between text lines. The default is 0.
- *spacing* Overall spacing (in pixels) between text lines. The default is 0.


The following example demonstrates how to change the default text characteristics:


```xml
<label>
	<text rich="1">
		<font size="20" color="#ff0000">A big red text</font> and a text of the default style.<br/>
		<font face="fontb.ttf" size="20">You can also change the font face.</font><br/>
		<font color="#00ff00">Here is a green text with a <font size="10">small tail.</font></font>
	</text>
</label>

```


The output will be the following:


![](widgets/font.png)


#### sub


Subscript text.


![subscript text](parameters/sub.png)


```xml
<text size="20" rich="1">Text <sub>Subscript text</sub></text>
```


#### sup


Superscript text.


![subscript text](parameters/sup.png)


```xml
<text size="20" rich="1">Text <sup>Superscript text</sup></text>
```


#### i


Italic font.


#### b


Bold font.


#### bi


Bold Italic font.


#### table


Table. Acceptable attributes:


- *color* Border color.
- *space* Overall spacing (pixels).
- *space_x* Horizontal spacing (pixels). Sets a space between table content and the left and right table borders.
- *space_y* Vertical spacing (pixels). Sets a space between table content and the upper and bottom table borders.
- *offset_x* Horizontal offset of the table.
- *offset_y* Vertical offset of the table.


Children:


- *tr* Table row. Multiple are allowed. Acceptable attribute: Children:

  - *height* Sets a height of the row.

  - *td* Table column. Multiple are allowed. Acceptable attribute:

    - *width* Sets a width of the column.


![](table_tag.png)


```xml
<text size="20" rich="1">
	<table space="10" color="#ffffff">
		<tr height="45">
			<td>Row 0 Column 0</td>
			<td>Row 0 Column 1</td>
		</tr>
		<tr height="45">
			<td>Row 1 Column 0</td>
			<td>Row 1 Column 1</td>
		</tr>
	</table>
</text>

```


#### xy


Sets the fixed coordinates for the text. Acceptable attributes:


- *x* X coordinate of the text.
- *y* Y coordinate of the text.
- *x=%<value>* or *x="%<value>"* X coordinate of the text relative to the current text container.
- *y=%<value>* or *y="%<value>"* Y coordinate of the text relative to the current text container.
- *dx* Text offset along the X axis.
- *dy* Text offset along the Y axis.


```xml
<text size="20" rich="1"><xy x="12" y="24"/>Text</text>
```


Values of the *x* and *y* attributes that are prepended % set the position of the text relative to the size of the current text container in percents. For example:


- *x=%0 y=%0* values correspond to the top left corner of the text container.
- *x=%0 y=%100* values correspond to the bottom left corner of the text container.


and so on:


![](widgets/xy.png)


For example:


```xml
<text rich="1" size="20">
	This is a <xy x="%50" y="%100"/>long text
</text>

```


In this case, the *long text* is positioned relative to the size of the text container as follows:


![](widgets/xy_100.png)


To adjust the text position, use the *dx* and *dy* attributes.


> **Notice:** In the example, the white space between the *"This is a"* and *"long text"* parts isn't taken into account when calculating the position.


#### image


Inserts an image. Acceptable attributes:


- *src* Path to an image.
- *color* Image color multiplier.
- *x* X coordinate of the image.
- *y* Y coordinate of the image.
- *x=%<value>* or *x="%<value>"* X coordinate of the image relative to the current text container.
- *y=%<value>* or *y="%<value>"* Y coordinate of the image relative to the current text container.
- *dx* Image offset along the X axis.
- *dy* Image offset along the Y axis.
- *scale_x=%<value>* or *scale_x="%<value>"* Horizontal scale factor for the image size in percents relative to its current size. By default, a horizontal scale of an image is 100%.
- *scale_y=%<value>* or *scale_y="%<value>"* Vertical scale factor for the image size in percents relative to its current size. By default, a vertical scale of an image is 100%.
- *scale=%<value>* or *scale="%<value>"* Overall scale factor for the image size in percents relative to its current size. By default, a scale of an image is 100%.


Values of the *x* and *y* attributes that are prepended % set the position of the image relative to the size of the current text container in percents. For example:


- *x=%0 y=%0* values correspond to the top left corner of the text container.
- *x=%0 y=%100* values correspond to the bottom left corner of the text container.


and so on:


![](widgets/image.png)


For example:


```xml
<text rich="1" size="15">
	Image with a long description: <image src="brush_square.png" x="%100" y="%100"/>
</text>

```


In this case,the image is positioned relative to the text as follows:


![](widgets/image_100.png)


To adjust the image position, use the *dx* and *dy* attributes.


To scale the image, use the *scale_x*


#### right


Aligns the text that follows this tag to the right border of a widget.


> **Notice:** Both the **<right>** and **<right/>** notations are valid.


![](right_tag.png)


```xml
<text rich="1">Text<right/>Text</text>
```


#### &gt;


The **>** symbol.


#### &lt;


The **<** symbol.


#### &amp;


The **&** symbol.


#### &quot;


The **"** symbol.


#### &apos;


The **'** symbol.


#### &#SYMBOL_DEC_CODE;


Numeric character reference, where **SYMBOL_DEC_CODE** symbol's decimal code (e.g., &#65 = 'A').


## Include Tag


This tag allows including the external `*.ui` file.


> **Notice:** The *name* attribute of widgets and containers defined in the external file must be unique.


Attributes:


- *name* Path to the `*.ui` file to be included.


For example, you can insert one window into another as follows:


```xml
<window name="Test::window" export="1" width="356" height="356">
	<include name="test_01.ui"/>
</window>

```


The included window is described in the `test_01.ui` file:


```xml
<?xml version="1.0" encoding="utf-8"?>
<ui version="1.0">
	<window name="Test::window_2" export="1" width="156" height="156" color="#26DEFF" align="left">
		<label width="70" height="40">
				<text color="#7FC9FF">Included UI</text>
		</label>
	</window>
</ui>

```


This example shows the following:


![include ui](widgets/include.png)


## Reference Tag


This tag serves to refer to containers. The containers, which are referred by the *reference* tag, must have the [*name*](#param_name) attribute.


> **Notice:** The referred container will not be displayed: only its content will be shown.


Attributes:


- *name* A container name to which the reference is made.
- Custom attribute The name of this attribute is a part of the widget name that need to be replaced. The acceptable value of the attribute is a replacement string. This is an optional attribute.


For example, there are the *vbox* container, which is defined as follows:


```xml
<vbox name="Test::vbox" export="0" space="8" reference="1">
	<label><text>Label 0</text></label>
	<label><text>Label 1</text></label>
	<label><text>Label 2</text></label>
</vbox>

```


This container won't be shown in the GUI, because the [*reference*](#param_reference) attribute is set to1. To show the container, add a reference to it:


```xml
<window name="Test::window" export="1" width="356" height="356">
	<reference name="Test::vbox"/>
</window>

```


The result is the following:


![](widgets/reference.png)


If you want to use the same widget (or container) in different parts of your GUI with minimum changes, you can add a reference to it rather than duplicate. To change a child of the widget, first you should define its *name* attribute and set the *export* attribute to 1.


```xml
<vbox name="Test::vbox" reference="1">
	<label name="Test::label_N" export="1"></label>
</vbox>

```


Then you need to add the *reference* tag with the custom attribute. In the example, this attribute named *label_N*. The value of this attribute is a name of an object of the WidgetLabel class that is declared in the script and is subjected to change.


```xml
<window name="Test::window_0" export="1" width="250" height="150" sizeable="1" enabled="1" space_y="10">
	<text align="left">First Window</text>
	<reference name="Test::vbox" label_N="label_0"/>
</window>

<window name="Test::window_1" export="1" width="250" height="150" sizeable="1" enabled="1" space_y="10">
	<text align="left">Second Window </text>
	<reference name="Test::vbox" label_N="label_1"/>
</window>

```


In the script, you should declare widgets as global variables and define necessary properties for the widgets that is subjected to change. Then you need to add root widgets to be rendered via *[Gui::addChild()](../../../api/library/gui/class.gui_cpp.md#addChild_Widget_int_void)*. For example:


```cpp
namespace Test {

	WidgetWindow window_0;
	WidgetWindow window_1;
	WidgetLabel label_0;
	WidgetLabel label_1;
	UserInterface ui;

	void init() {
		ui = new UserInterface(engine.getGui(),"window.ui");

		label_0.setText("The first label"); // text shown in the first window
		label_1.setText("The second label"); // text shown in the second window
	}

	void show(int x,int y) {
		Gui gui = engine.getGui();
		gui.addChild(window_0); // add the first window
		window_0.setPosition(x,y);
		gui.addChild(window_1); // add the second window
		window_1.setPosition(x+100,y);
	}
}

int init() {

	Test::init();
	Test::show(50,50);

	return 1;
}

```


As the result, two windows with different text are shown:


![](examples/reference_custom.png)


Also the name of the widget or container can be defined as an array. To address to the required object, use the following:


```xml
<vbox name="Test::vbox" reference="1">
	<label name="Test::label[NUM]" export="1"></label>
</vbox>
<window name="Test::window" export="1" width="250" height="150" sizeable="1" enabled="1" space_y="10">
	<text align="left">First Window</text>
	<reference name="Test::vbox[NUM]" NUM="0"/>
</window>

```


In the script, you should declare an array of objects of the corresponding widget class:


```cpp
WidgetLabel label[1];

label[0].setText("The first label");

```
