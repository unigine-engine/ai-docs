# Scripts


This type of node is used to write a *[UnigineScript](../../../../code/uniginescript/index.md)* logic in an ULON-based material file. The *Script* node specifies a single script that can be used in different *[Expression](../../../../code/formats/materials_formats/ulon_materials/expressions.md)* nodes.


The syntax is the following:


```cpp
Script script_name =
#{
    // UnigineScript code
#}

```


As a node�s value you must specify a *[UnigineScript](../../../../code/uniginescript/index.md)*-based code enclosed in **"#{"** and **"#}"**.


## Usage Examples


The script node is usually used as a script value for the *[Expression](../../../../code/formats/materials_formats/ulon_materials/expressions.md)* node.


```cpp
Script named_script =
#{
    // UnigineScript code
#}

Expression expression_name = named_script

```


You can also specify a path to an external script file (in **usc** or **h** format) or the name of a different *Script* node inside this material:


```cpp
Script external_script = "some/path/to/your/script.usc";	// script.usc consists of some UnigineScript code

Script linked_script = external_script

Expression RENDER_CALLBACK_* = linked_script

```


To include the code of a different script use the following marker: **#script script_name**.


```cpp
Script a =
#{
        // UnigineScript code A
#}

Script b =
#{
        // UnigineScript code B
        #script a
#}

// the result script b will look like this:
Script b =
#{
        // UnigineScript code B
        // UnigineScript code A
#}

```
