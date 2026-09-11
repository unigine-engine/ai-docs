# Expressions


The expressions are used to specify [UnigineScript](../../../../code/uniginescript/index.md) code to be called on some event or on user demand. They can be used to generate various elements used in the material (e.g., textures, texture arrays, unstructured buffers, etc.) or contain other logic.


As a node value you must specify a UnigineScript-based code enclosed in **"#{"** and **"#}"**. You can also specify a path to an external script file (in **usc** or **h** format) or the name of a *Script* node inside this material.


The syntax is the following:


```cpp
Expression name =
#{
    // UnigineScript code
#}

```


Or


```cpp
Script script_name =
#{
     // UnigineScript code
#}

Expression name = script_name

```


Or


```cpp
Expression name = "some/path/to/your/script.h"		// script.h consists of some UnigineScript code

```


When the name of an expression specified as `RENDER_*` (where * is a name of a [render callback](../../../../api/library/rendering/class.render_cpp.md)) and the current material is set globally or assigned to the main camera, the expression code will be executed automatically at the corresponding stage of the [rendering sequence](../../../../principles/render/sequence/index.md). Materials containing such expressions are called [scriptable](../../../../content/materials/scriptable.md).


It is possible to call an expression via the *[runExpression()](../../../../api/library/rendering/class.material_cpp.md#runExpression_cstr_int_int_int_int)* function of the *Material* class. The expression�s name must be unique.


## Usage Examples


```cpp
Expression RENDER_CALLBACK_BEGIN_SSAO =
#{
        // typical most frequently used parameters passed to the expression when it is called.
        int in_width;
        int in_height;
        int in_depth;
        Material in_material;

        // get a temporary texture
        Texture texture = engine.render.getTemporaryTexture(in_width, in_height);

        // set the modified texture as albedo texture of the material
        in_material->setTexture("albedo", texture);
#}

```
