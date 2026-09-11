# RC Files


## General Information


Unigine GUI uses resource files, which define some global settings for GUI. These files are in the XML format and have an RC extension. The RC file should be accompanied by a font file named `font.ttf`, which will be used by default. The font file should be located in the same directory as the RC file, along with other GUI [skin files](../../code/gui/skin/index.md). There can be only one RC file in a folder.


The default RC file for system GUI is `data/core/gui/gui.rc`.


## Syntax


As a correct XML file, an RC file must start with a standard declaration. The second required element is a root tag *resource*. This root element can contain zero or more other elements (tags) specifying the resources.


```xml
<?xml version="1.0" encoding="utf-8"?>
<resource version="1.0">
	<animation expose="6.0" fade_in="8.0" fade_out="4.0"/>
	<default size="14" color="#ddddffff" alpha="1.0"/>
	<focused color="#ffffffff" alpha="1.0"/>
	<disabled color="#869caaff" alpha="0.8"/>
	<transparent color="#869caaff" alpha="0.8"/>
	<tooltip size="13" color="#000000ff" alpha="0.95" time="0.4"/>
</resource>

```


If an RC file is not syntactically correct, Unigine will log the error to the console and the main log file.


> **Notice:** All RC files are treated as having the UTF-8 encoding, even if you specify another one in the declaration.


## Resources


### animation


This tag handles windows animation.


Parameters:


- *expose* Duration of animation played when the object appears. Measured in cycles per second, for example, *expose="6"* means that the duration is a 1/6 of a second.
- *fade_in* Duration of fading in animation played when the object gets focused. Measured in cycles per second.
- *fade_out* Duration of fading out animation played when the object loses focus. Measured in cycles per second.


### default


Default options for all widgets.


Parameters:


- *size* Font size.
- *color* Font color, in #RRGGBBAA format (hexadecimal).
- *alpha* Alpha value, **0.0** means completely transparent.


### focused


Options for widgets in focus.


Parameters:


- *color* Modulation color, in #RRGGBBAA format (hexadecimal).
- *alpha* Alpha value, **0.0** means completely transparent.


### disabled


Options for disabled widgets.


Parameters:


- *color* Modulation color, in #RRGGBBAA format (hexadecimal).
- *alpha* Alpha value, **0.0** means completely transparent.


### transparent


Options for semi-transparent widgets like windows with *blendable="yes"* and comboboxes.


Parameters:


- *color* Modulation color, in #RRGGBBAA format (hexadecimal).
- *alpha* Alpha value, **0.0** means completely transparent.


### tooltip


Options for tooltips.


Parameters:


- *size* Font size.
- *color* Font color, in #RRGGBBAA format (hexadecimal).
- *alpha* Alpha value, **0.0** means completely transparent.
- *time* Delay before the tooltip appears. Measured in cycles per second.
