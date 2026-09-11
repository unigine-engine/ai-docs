# Localization


The current article describes how to localize the GUI of your project.


### See Also


- The [*Usage Example*](../../../code/gui/usage/index.md) article.


## Fonts


Fonts files are used to correctly display characters of local languages in the Unigine-based project. The font file has a True Type font format and contains all of the local language characters.


To avoid incorrect display of language characters, you should add all of the required font files to your project folder and use the [*engine.gui.setFontPath()*](../../../api/library/gui/class.gui_cpp.md#setFontPath_cstr_int) function when it is necessary to change the font. For example, to translate into Chinese, you should load your English-Chinese[dictionary](#dict) and set the corresponding font as follows:


```cpp
engine.gui.setFontPath("my_project/gui/font_ch.ttf");
```


If the project supports your local language only, you can simply replace 2 font files `font.ttf` (for GUI widgets) and `console.ttf` (for console) in the `data/core/gui` directory with the font files containing the local language characters. The names of Unigine files should be preserved.


## Character Encoding


All of the project files should be saved in UTF-8 encoding.


> **Notice:** The encoding must be UTF-8 without BOM (Byte Order Mark).


## Translation Dictionaries


To support several languages in your project, you need to use dictionaries, which are stored in the XML format. They are used to translate the GUI from one language into another.


> **Notice:** You can store a [*separate dictionary*](#separate_dicts) for each language or you can create a [*single dictionary*](#single_dict) for all supported languages.


### File Formats


Depending on the storage method of dictionaries, you should use the corresponding dictionary file format.


#### Dictionaries Stored in Separate Files


```xml
<?xml version="1.0" encoding="utf-8"?>
<dictionary version="1.00">
	<msg>
		<src>Source string</src>
		<tr>Translated string</tr>
	</msg>
</dictionary>

```


The root tag *dictionary* contains the *msg* child tag, which is used to define a word or phrase to be translated and has the following children:


- *src* - a source string to be translated. > **Notice:** The punctuation marks should be included to the string; otherwise the string won't be translated.
- *tr* - a translation string.


#### Single Dictionary for All Languages


```xml
<?xml version="1.0" encoding="utf-8"?>
<dictionary version="1.00">
	<msg>
		<src>Source string</src>
		<en>String translated to English</en>
		<ch>String translated to Chinese</ch>
		<ru>String translated to Russian</ru>
	</msg>
</dictionary>

```


The root tag *dictionary* contains the *msg* child tag, which is used to define a word or phrase to be translated and has the following children:


- *src* - a source string to be translated. > **Notice:** The punctuation marks should be included to the string; otherwise the string won't be translated.
- *en*, *ch*, *ru* or any other tag that contains a translation string. > **Notice:** You can use any tag to store the translation. You just have to [specify the tag name as the second argument](#load_dict) of the [*engine.gui.addDictionary()*](../../../api/library/gui/class.gui_cpp.md#addDictionary_cstr_cstr_int) function to load the proper translation.


### Managing Locale


To add the dictionary, use the [*engine.gui.addDictionary()*](../../../api/library/gui/class.gui_cpp.md#addDictionary_cstr_cstr_int) function.  To save the last loaded dictionary, use the [*engine.gui.saveDictionary()*](../../../api/library/gui/class.gui_cpp.md#saveDictionary_cstr_cstr_int) function.  This function also allows you to save the currently loaded dictionary into another file.  If you want to modify the dictionary, you can edit the XML file manually or by using the [Xml](../../../api/library/common/class.xml_cpp.md) class functions and then load it.


> **Notice:** Dictionaries cannot be changed in run-time.


If you use a separate dictionary for each language, you should get access to translation as follows:


```cpp
engine.gui.addDictionary("my_project/locale/my_project.ch"); // load English-Chinese dictionary
ui.updateWidgets();

```


Otherwise, you should specify a tag that contains the required translation as the second argument of the [*engine.gui.addDictionary()*](../../../api/library/gui/class.gui_cpp.md#addDictionary_cstr_cstr_int) function:


```cpp
engine.gui.addDictionary("my_project/locale/my_project.locale","ch"); // load the Chinese translation
ui.updateWidgets();

```


The [*updateWidgets()*](../../../api/library/gui/class.userinterface_cpp.md#updateWidgets_void) function is called to change the language after the required dictionary is added.


## Input Methods


Unigine supports IMEs (Input Method Editors) that allow entering Chinese, Japanese and Korean characters by using the Latin keyboard.


> **Notice:** Unigine doesn't support right-to-left and top-to-bottom languages.


To enter Chinese, Japanese or Korean characters, simply change your keyboard layout and start typing.
